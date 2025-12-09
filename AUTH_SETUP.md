# Firebase Authentication Setup Guide

## Error: "auth/configuration-not-found"

This error occurs when Firebase Authentication is not enabled in your Firebase project.

## Steps to Fix:

### 1. Enable Firebase Authentication
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your **cmms-y-404fe** project
3. In the left sidebar, go to **Authentication** (under Build section)
4. Click **Get started** or **Enable**
5. You'll see different sign-in methods

### 2. Enable Email/Password Authentication
1. Click on the **Sign-in method** tab
2. Click on **Email/Password**
3. Toggle **Enable** to ON
4. Make sure "Email/Password" is enabled (not just "Email link")
5. Click **Save**

### 3. (Optional) Enable Other Sign-In Methods
You can also enable:
- Google Sign-in
- GitHub Sign-in
- Anonymous Sign-in

For now, Email/Password is enough for your app.

### 4. Create Firestore Database (if not done already)
1. Go to **Firestore Database** in the left sidebar
2. Click **Create Database**
3. Choose your region and start in **Test mode**
4. Click **Enable**

### 5. Update Firestore Security Rules
1. Go to **Firestore Database** → **Rules** tab
2. Replace rules with:

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

## After Setup:

1. Refresh your app in the browser
2. Try clicking **Login**
3. Create a new account with email/password
4. You should be redirected to the profile page

## If Error Still Occurs:

Check browser console (F12) for more detailed error messages. Common issues:
- Authentication method not enabled
- CORS issues (shouldn't happen with Firebase)
- API key not authorized for Authentication
- Browser cache (try hard refresh: Ctrl+Shift+R)

## Firebase Console Location:
- Project: cmms-y-404fe
- URL: https://console.firebase.google.com/project/cmms-y-404fe
