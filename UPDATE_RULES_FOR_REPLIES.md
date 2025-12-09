# Update Firestore Rules for Reply Threads

## Important: Update your Firestore Security Rules

Your current rules don't allow replies. Replace them with this:

### Step 1: Open Firebase Console Rules
Go to: https://console.firebase.google.com/project/cmms-y-404fe/firestore/rules

### Step 2: Replace ALL rules with this:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Posts collection - allow authenticated users to read and create
    match /posts/{postId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null && request.resource.data.author == request.auth.token.email;
      allow update, delete: if request.auth != null && resource.data.author == request.auth.token.email;
      
      // Replies subcollection - allow authenticated users to read and create
      match /replies/{replyId} {
        allow read: if request.auth != null;
        allow create: if request.auth != null && request.resource.data.author == request.auth.token.email;
        allow update, delete: if request.auth != null && resource.data.author == request.auth.token.email;
      }
    }
  }
}
```

### Step 3: Click "Publish"
Wait for confirmation.

### Step 4: Refresh Your App
Go back to the app and test the reply feature!

---

## How Replies Work:

- Click the **💬 Replies** button on any post
- See all replies and the timestamp
- Write a reply and click **Post Reply**
- Your email is saved as the author
- Only you can edit/delete your replies

---

## If You Get Permission Errors:

1. Make sure you're **logged in** first
2. Do a **hard refresh** (Ctrl+Shift+R)
3. Check that the rules were **published** (no error in Rules tab)
