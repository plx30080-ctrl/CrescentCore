# Firebase Security Rules Fix

## Problem
Getting `PERMISSION_DENIED` error when trying to connect to Firebase Realtime Database.

## Solution

### Step 1: Open Firebase Console
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: **hours-reporting-eaecc**

### Step 2: Navigate to Realtime Database Rules
1. In the left sidebar, click **"Realtime Database"**
2. Click the **"Rules"** tab at the top

### Step 3: Update Security Rules

Replace your current rules with one of these options:

#### Option A: Open Access (for development/testing)
**⚠️ WARNING: This allows anyone to read/write your database. Only use for development!**

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

#### Option B: Authenticated Users Only (recommended for production)
```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

#### Option C: Specific Path Access
```json
{
  "rules": {
    "weeks": {
      ".read": true,
      ".write": true
    }
  }
}
```

### Step 4: Publish the Rules
1. Click the **"Publish"** button
2. Wait for confirmation that rules were updated

### Step 5: Test Your Application
1. Refresh your application page
2. You should now see the data load successfully

## Current Rules Check

Your current rules might look like this (default):
```json
{
  "rules": {
    ".read": false,
    ".write": false
  }
}
```

This blocks all access, which is why you're getting the permission error.

## Recommended Approach

For a production app, you should:
1. Start with Option A to verify everything works
2. Implement Firebase Authentication in your app
3. Switch to Option B for secure, authenticated access
4. Consider more granular rules based on user roles

## Need to Add Authentication Later?

If you want to add authentication, you'll need to:
1. Enable Firebase Authentication in your Firebase Console
2. Add authentication to your React app
3. Update the security rules to use `auth != null`

For now, **Option A or Option C** will get your app working immediately.
