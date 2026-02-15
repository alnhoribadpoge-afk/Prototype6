# GitHub Data Sync Guide - TNHS Enrollment System

## 🎯 Layunin (Objective)
Siguraduhin na lahat ng student data ay:
- ✅ Automatically saved sa browser (localStorage)
- ✅ Persistent kahit mag-refresh o mag-close ng browser
- ✅ Accessible sa ibang devices (through GitHub)
- ✅ Backed up sa GitHub repository

---

## 📱 How Data Persistence Works

### 1. **Local Storage (Browser)**
- Data ay automatically saved sa browser's localStorage
- Persists kahit mag-close ang browser
- Accessible lang sa same browser/device

### 2. **Auto-Save Features**
```javascript
// Auto-save every 30 seconds
setInterval(function() {
  if (users.length > 0) {
    saveUsersToStorage();
  }
}, 30000);

// Save on page unload (when closing browser)
window.addEventListener('beforeunload', function() {
  saveUsersToStorage();
});
```

### 3. **Data Format**
```javascript
{
  users: [ /* array ng student records */ ],
  lastSaved: "2025-01-15T10:30:45.123Z",
  version: "1.0"
}
```

---

## 🔄 Step-by-Step: Upload to GitHub

### Step 1: Export Data from Browser
```javascript
// Open browser console (F12) at i-run:
exportDataAsJSON()
```
- Ito ay mag-download ng file: `tnhs_backup_YYYY-MM-DD_XXXrecords.json`
- Ang file ay may lahat ng student data

### Step 2: Create GitHub Repository Structure
```
your-repo/
├── index.html
├── logo.jpg
├── data/
│   ├── README.md
│   └── tnhs_backup_2025-01-15_150records.json
├── .gitignore
└── README.md
```

### Step 3: Add .gitignore (Optional)
```
# .gitignore
node_modules/
*.log
.DS_Store
```

### Step 4: Upload to GitHub
```bash
git add .
git commit -m "Initial commit: TNHS Enrollment System with student data"
git push origin main
```

### Step 5: Users Can Import Data
1. Clone ang repository
2. Open `index.html` sa browser
3. Open browser console (F12)
4. Run: `importDataFromJSON(file)` with the backup JSON file
5. Data ay automatically loaded at saved

---

## 💾 Data Backup & Recovery

### Automatic Backups
- Data ay automatically saved every 30 seconds
- Data ay saved on page unload
- Data ay saved after every student registration

### Manual Backup
```javascript
// Export data anytime
exportDataAsJSON()

// This creates a file like:
// tnhs_backup_2025-01-15_150records.json
```

### Recovery from Backup
```javascript
// Import data from backup file
importDataFromJSON(backupFile)

// Or upload the file through the admin dashboard
```

---

## 🌐 Cross-Device Sync

### Option 1: Manual Sync (Recommended)
1. **Device A**: Export data using `exportDataAsJSON()`
2. **Upload** the JSON file to GitHub
3. **Device B**: Clone repository and import data using `importDataFromJSON()`

### Option 2: Cloud Sync (Advanced)
For automatic sync across devices, you can integrate:
- Google Drive API
- Dropbox API
- Firebase Realtime Database
- AWS S3

---

## 📊 Console Commands Reference

### View All Data
```javascript
console.log(users)
```

### Export Data
```javascript
exportDataAsJSON()
```

### Import Data
```javascript
// Create file input
const input = document.createElement('input');
input.type = 'file';
input.accept = '.json';
input.onchange = (e) => importDataFromJSON(e.target.files[0]);
input.click();
```

### View Statistics
```javascript
showDataStats()
// Output:
// {
//   totalStudents: 150,
//   jhsStudents: 50,
//   shsStudents: 100,
//   sf1Completed: 75,
//   maleStudents: 80,
//   femaleStudents: 70,
//   lastSaved: "2025-01-15T10:30:45.123Z"
// }
```

### Clear All Data
```javascript
clearAllData()
// ⚠️ WARNING: This will delete all data!
```

### Check Storage Size
```javascript
const size = localStorage.getItem('tnhs_users').length;
console.log(`Storage used: ${(size / 1024).toFixed(2)} KB`);
```

---

## 🔐 Data Security Tips

### 1. **Regular Backups**
- Export data weekly using `exportDataAsJSON()`
- Store backups sa secure location

### 2. **Version Control**
- Keep multiple backup versions sa GitHub
- Use meaningful commit messages

### 3. **Access Control**
- Make repository private if sensitive data
- Use GitHub's access control features

### 4. **Data Encryption** (Optional)
For sensitive data, consider:
- Encrypting JSON files before upload
- Using GitHub's encrypted secrets

---

## 🚀 Deployment Checklist

- [ ] Test data persistence sa browser
- [ ] Export sample data successfully
- [ ] Create GitHub repository
- [ ] Upload index.html at logo.jpg
- [ ] Upload data backup JSON file
- [ ] Test import functionality
- [ ] Document data structure
- [ ] Create README with instructions
- [ ] Set repository to public/private as needed
- [ ] Share repository link with users

---

## 📝 README Template for GitHub

```markdown
# TNHS Enrollment System

Student enrollment system para sa Taguig National High School.

## Features
- Student registration
- SF1 form submission
- Admin dashboard
- Automatic data persistence
- Data backup & recovery

## How to Use

### For Students
1. Open `index.html` sa browser
2. Click "Apply Now"
3. Fill up the form
4. Data ay automatically saved

### For Admins
1. Login using admin credentials
2. View student data sa dashboard
3. Export data using "Download" button

### Data Backup
```bash
# Export data
# Open browser console (F12) at i-run:
exportDataAsJSON()

# Import data
importDataFromJSON(backupFile)
```

## Data Storage
- Data ay stored sa browser's localStorage
- Persists kahit mag-close ang browser
- Accessible sa same browser/device

## Backup Files
- `data/tnhs_backup_*.json` - Student data backups

## Support
For issues or questions, contact the development team.
```

---

## 🔧 Troubleshooting

### Data Not Saving?
1. Check browser console for errors (F12)
2. Ensure localStorage is enabled
3. Check storage quota: `console.log(localStorage.getItem('tnhs_users').length)`

### Import Not Working?
1. Verify JSON file format
2. Check browser console for errors
3. Ensure file is valid JSON

### Storage Quota Exceeded?
1. Export current data
2. Clear old data: `clearAllData()`
3. Import fresh data

### Data Lost After Browser Update?
1. Always keep backups using `exportDataAsJSON()`
2. Store backups sa GitHub
3. Restore from backup using `importDataFromJSON()`

---

## 📈 Scalability

### Current Limits
- Browser localStorage: ~5-10MB
- Supports ~1000-5000 student records

### For Larger Scale
Consider migrating to:
- Backend database (MySQL, PostgreSQL)
- Cloud services (Firebase, AWS)
- API-based architecture

---

## 📞 Support & Documentation

### Console Commands
```javascript
// View all available functions
console.log({
  saveUsersToStorage,
  loadUsersFromStorage,
  exportDataAsJSON,
  importDataFromJSON,
  clearAllData,
  getDataStats,
  showDataStats
})
```

### Useful Links
- [MDN: localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [GitHub: How to use](https://docs.github.com/en)
- [JSON Format](https://www.json.org/)

---

**Last Updated**: January 2025
**Version**: 1.0
**Status**: Production Ready ✅
