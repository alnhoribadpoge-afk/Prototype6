# 🚀 QUICK START - GitHub Centralized Sync (5 Minutes)

## ✅ What You Need to Know

Your TNHS Enrollment System is **READY** for GitHub centralized sync. This means:

✅ Students can create accounts on any device  
✅ Data automatically saves to GitHub  
✅ Admin can see all students from all devices  
✅ Data never gets lost  
✅ Everything syncs automatically  

---

## 🎯 5-Minute Setup

### Step 1: Create GitHub Repository (2 min)

1. Go to: **https://github.com/new**
2. Fill in:
   - **Repository name**: `tnhs-enrollment-data`
   - **Description**: TNHS Enrollment System
   - **Visibility**: Public
3. Click **Create repository**

### Step 2: Get Your GitHub Token (2 min)

1. Go to: **https://github.com/settings/tokens**
2. Click **Generate new token**
3. Name it: `TNHS_Token`
4. Check: `repo` checkbox
5. Click **Generate token**
6. **Copy the token** (save it somewhere safe!)

### Step 3: Configure Application (1 min)

1. Open: **index.html** in a text editor
2. Find: `const GITHUB_CONFIG = {` (around line 200)
3. Replace these values:
   ```javascript
   owner: 'YOUR_USERNAME',        // Your GitHub username
   token: 'YOUR_TOKEN',           // Your token from Step 2
   ```

**Example:**
```javascript
const GITHUB_CONFIG = {
  enabled: true,
  owner: 'john_doe',                    // ← Your GitHub username
  repo: 'tnhs-enrollment-data',
  branch: 'main',
  token: 'ghp_abc123xyz789...',        // ← Your token
  dataPath: 'data/students.json',
  backupPath: 'data/backup/',
  syncInterval: 60000,
  autoSync: true
};
```

---

## ✅ Done! Now Test It

### Test 1: Create Student Account
1. Open `index.html` in browser
2. Click **"Apply Now"**
3. Fill form and submit
4. ✅ Data saved to GitHub!

### Test 2: Admin Login
1. Click **"Admin"**
2. Login: `admin` / `admin123`
3. ✅ You see the student you created!

### Test 3: Cross-Device
1. Open `index.html` in **different browser**
2. Admin login
3. ✅ You see the same student!

---

## 🎉 That's It!

Your system is now:
- ✅ Saving all data to GitHub
- ✅ Syncing across devices automatically
- ✅ Backing up data daily
- ✅ Ready for production

---

## 📚 Need More Help?

- **Setup Guide**: Read `GITHUB_SETUP_CHECKLIST.md`
- **Complete Guide**: Read `GITHUB_CENTRALIZED_SYNC.md`
- **Testing**: Read `QUICK_TEST_GUIDE.md`
- **Troubleshooting**: Read `GITHUB_SETUP_CHECKLIST.md` (Troubleshooting section)

---

## 🔧 Quick Commands

### Check if GitHub is connected
```javascript
// Open browser console (F12) and paste:
loadFromGitHub().then(data => {
  console.log(data ? '✅ Connected!' : '❌ Failed');
});
```

### View all students
```javascript
console.log(users);
```

### Manual sync
```javascript
autoSyncToGitHub();
```

---

## ⚠️ Important: Protect Your Token

**DO NOT** share your token or commit it to GitHub!

If you accidentally exposed it:
1. Go to: https://github.com/settings/tokens
2. Delete the exposed token
3. Generate a new one
4. Update your application

---

## 🎯 How It Works

```
Device 1 (Laptop)
├─ Student creates account
├─ Data saved to GitHub
└─ ✅ Done!
        ↓
    GitHub Repository
    (Central storage)
        ↓
Device 2 (Desktop)
├─ Admin logs in
├─ Loads data from GitHub
└─ ✅ Sees all students!
```

---

## 📞 Support

| Issue | Solution |
|-------|----------|
| "401 Unauthorized" | Generate new token at https://github.com/settings/tokens |
| "404 Not Found" | Check repository name and file path |
| Data not syncing | Check internet connection, refresh page |
| Token exposed | Revoke token immediately, generate new one |

---

**Version**: 1.0  
**Status**: ✅ Ready to Use

**Next**: Follow the 3 steps above, then test it!
