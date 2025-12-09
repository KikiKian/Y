# Firebase Firestore Setup Guide

## Issue: "Failed to submit post"

This error typically occurs due to missing Firestore database or incorrect security rules.

## Steps to Fix:

### 1. Create a Firestore Database
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your "cmms-y-404fe" project
3. Go to **Firestore Database** in the left sidebar
4. Click **Create Database**
5. Choose:
   - Location: Choose your region (e.g., us-east1)
   - Start in **test mode** (temporarily allows all read/write for 30 days)
6. Click **Enable**

### 2. Update Firestore Security Rules (Important for Production)

Once the database is created:

1. Go to **Firestore Database** → **Rules** tab
2. Replace the default rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow authenticated users to create and read posts
    match /posts/{document=**} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.author == request.auth.token.email;
      allow update, delete: if request.auth != null && resource.data.author == request.auth.token.email;
    }
  }
}
```

3. Click **Publish**

### 3. Create the "posts" Collection (if needed)

If you get a "posts collection doesn't exist" error:

1. Go to **Firestore Database** → **Data** tab
2. Click **Start Collection**
3. Collection ID: `posts`
4. Add a test document (optional):
   - Document ID: `test`
   - Fields:
     - `title` (string): "Test Post"
     - `content` (string): "This is a test"
     - `timestamp` (number): 1702000000000
     - `author` (string): "test@example.com"

### 4. Test the Application

1. Go back to your app and refresh
2. Click "Login" and create an account
3. Go to Posts page
4. Click "Add Post" and submit a post

If you still get errors, check:
- Browser Console (F12) for detailed error messages
- Firebase Console → Firestore → Rules for any issues
- Ensure you're logged in before submitting posts

## Security Note

Test mode rules should NOT be used in production. Always use proper authentication-based rules like those shown above.
