# Fix "Missing or insufficient permissions" Error

## The Problem:
Your Firestore database has security rules that prevent users from creating posts.

## The Solution (5 minutes):

### Step 1: Open Firebase Console
Go to: https://console.firebase.google.com/project/cmms-y-404fe/firestore

### Step 2: Click on the "Rules" Tab
- You should see your current Firestore rules
- They probably say "deny read, write: if false" or similar

### Step 3: Replace ALL the rules with this:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow authenticated users to read all posts
    match /posts/{document=**} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.author == request.auth.token.email;
      allow update, delete: if request.auth != null && resource.data.author == request.auth.token.email;
    }
  }
}
```

### Step 4: Click "Publish"
- Wait for the confirmation message

### Step 5: Go back to your app and try again
- Refresh the page (F5)
- Go to Posts page
- Click "Add Post"
- Fill in title and content
- Click Submit

---

## What These Rules Mean:

- **read**: Any logged-in user can see all posts ✅
- **create**: Logged-in users can create posts (their email is saved as author) ✅
- **update/delete**: Only the author can edit or delete their own posts ✅
- **Not logged in**: You can't do anything ❌

---

## If You Still Get the Error:

1. Make sure you're **logged in** (check the Login button - should say "Logout")
2. Do a **hard refresh** (Ctrl+Shift+R)
3. Check the **Rules tab** - make sure the new rules were published (no error message)
4. Open **browser console** (F12) and look for error details

---

## Important Notes:

- These rules are suitable for a school social media app
- Users can only edit/delete their own posts
- Anonymous users cannot post (they must log in first)
- This is more secure than "test mode" rules

