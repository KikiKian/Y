# Firebase Authentication Setup - Quick Steps

## You're seeing this message because Authentication is not enabled in your Firebase project.

### QUICK FIX (5 minutes):

1. **Open Firebase Console**
   - Go to: https://console.firebase.google.com/project/cmms-y-404fe/authentication

2. **Click "Get started" button**
   - You'll see sign-in method options

3. **Find "Email/Password"**
   - It should be in the list of authentication providers

4. **Click on "Email/Password"**
   - A modal will open with options

5. **Toggle "Enable" to ON**
   - Make sure the toggle is blue/enabled

6. **Keep the second toggle ON too** (Email link sign-in)
   - This is fine to leave enabled

7. **Click "Save"**
   - Wait for confirmation

8. **Go back to your app and refresh**
   - The authentication error should be gone!

---

## If you're stuck on step 1:

**Direct link to Firebase Console:**
```
https://console.firebase.google.com/project/cmms-y-404fe/authentication
```

Copy and paste this into your browser address bar.

---

## After Enabling:

You should be able to:
- ✅ Sign up with email/password
- ✅ Log in
- ✅ View your profile
- ✅ Create posts

---

## Troubleshooting:

**If you still see the error after enabling:**
1. Do a **hard refresh** of your browser (Ctrl+Shift+R on Windows)
2. Check that the Email/Password toggle is actually blue/ON
3. Check browser console (F12) for any error messages

**Your Firebase Project ID:**
- Project: `cmms-y-404fe`
- Auth Domain: `cmms-y-404fe.firebaseapp.com`

These are already configured in your code, so you just need to enable the service in Firebase Console.
