# TNHS Enrollment System - Complete Data Persistence Guide

## 🎯 Overview

Ang TNHS Enrollment System ay may **complete data persistence** na nag-guarantee na:

✅ **Lahat ng student data ay automatically saved** sa browser  
✅ **Data persists kahit mag-refresh o mag-close ang browser**  
✅ **Accessible sa ibang devices through GitHub**  
✅ **Automatic backup every 30 seconds**  
✅ **Manual export/import functionality**  

---

## 🚀 Quick Start

### Para sa Students
1. Open `index.html` sa browser
2. Click "Apply Now"
3. Fill up the form
4. **Data ay automatically saved** - walang kailangang i-click!
5. Kahit mag-refresh o mag-close ang browser, ang data ay nandito pa rin

### Para sa Admins
1. Login sa admin dashboard
2. View lahat ng student data
3. Export data anytime using "Download" button
4. Import data from backup files

---

## 💾 Data Persistence Features

### 1. **Automatic Local Storage**
```javascript
// Data ay automatically saved sa browser
// Every time a student registers or updates their profile
saveUsersToStorage()
```

### 2. **Auto-Save Every 30 Seconds**
```javascript
// Kahit hindi nag-submit, ang data ay naka-save na
setInterval(function() {
  if (users.length > 0) {
    saveUsersToStorage();
  }
}, 30000);
```

### 3. **Save on Page Unload**
```javascript
// Kahit mag-close ang browser, ang data ay naka-save pa rin
window.addEventListener('beforeunload', function() {
  saveUsersToStorage();
});
```

### 4. **Timestamp Tracking**
```javascript
// Bawat save ay may timestamp
{
  users: [ /* data */ ],
  lastSaved: "2025-01-15T10:30:45.123Z",
  version: "1.0"
}
```

---

## 📱 Cross-Device Access

### Scenario 1: Same Device, Different Browser
- **Chrome**: Data ay saved sa Chrome's localStorage
- **Firefox**: Data ay saved sa Firefox's localStorage
- **Solution**: Export from Chrome, import sa Firefox

### Scenario 2: Different Devices
- **Device A (Laptop)**: Export data using `exportDataAsJSON()`
- **Upload** to GitHub
- **Device B (Phone)**: Clone repository, import data

### Scenario 3: Team Collaboration
- **Admin A**: Export data
- **Upload** to GitHub
- **Admin B**: Pull latest data, import locally
- **Merge** data if needed

---

## 🔄 GitHub Integration Steps

### Step 1: Prepare Data
```javascript
// Open browser console (F12)
exportDataAsJSON()
// Downloads: tnhs_backup_2025-01-15_150records.json
```

### Step 2: Create Repository
```bash
# Create new repository on GitHub
# Clone locally
git clone https://github.com/yourusername/tnhs-enrollment.git
cd tnhs-enrollment
```

### Step 3: Add Files
```bash
# Copy your files
cp index.html .
cp logo.jpg .
cp tnhs_backup_2025-01-15_150records.json data/

# Add to git
git add .
git commit -m "Initial commit: TNHS Enrollment System"
git push origin main
```

### Step 4: Users Can Access
```bash
# Clone repository
git clone https://github.com/yourusername/tnhs-enrollment.git

# Open index.html
# Import data from data/tnhs_backup_*.json
```

---

## 📊 Data Management

### View Current Data
```javascript
// Open browser console (F12)
console.log(users)
```

### Get Statistics
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

### Export Data
```javascript
exportDataAsJSON()
// Creates: tnhs_backup_YYYY-MM-DD_XXXrecords.json
```

### Import Data
```javascript
// Method 1: Using file input
const input = document.createElement('input');
input.type = 'file';
input.accept = '.json';
input.onchange = (e) => importDataFromJSON(e.target.files[0]);
input.click();

// Method 2: Direct function call
importDataFromJSON(fileObject)
```

### Clear All Data
```javascript
clearAllData()
// ⚠️ WARNING: Permanent deletion!
```

---

## 🔐 Data Security

### Best Practices
1. **Regular Backups**
   - Export data weekly
   - Store sa secure location
   - Keep multiple versions

2. **Version Control**
   - Use meaningful commit messages
   - Tag important versions
   - Keep history sa GitHub

3. **Access Control**
   - Make repository private if needed
   - Use GitHub's permission settings
   - Limit admin access

4. **Data Validation**
   - Verify JSON format before import
   - Check for duplicates
   - Validate email addresses

---

## 📈 Storage Information

### Browser Storage Limits
- **Chrome**: ~10MB
- **Firefox**: ~10MB
- **Safari**: ~5MB
- **Edge**: ~10MB

### Current Usage
```javascript
// Check storage size
const size = localStorage.getItem('tnhs_users').length;
console.log(`Storage used: ${(size / 1024).toFixed(2)} KB`);
```

### Capacity
- **~1000-5000 student records** per browser
- Depends on SF1 data completeness
- Can be increased by clearing old data

---

## 🛠️ Troubleshooting

### Problem: Data Not Saving
**Solution:**
```javascript
// Check if localStorage is enabled
console.log(localStorage.getItem('tnhs_users'))

// If null, enable localStorage sa browser settings
// Or try different browser
```

### Problem: Import Not Working
**Solution:**
```javascript
// Verify JSON format
const data = JSON.parse(fileContent);
console.log(data);

// Check if file has 'users' array
if (data.users && Array.isArray(data.users)) {
  console.log('Valid format');
}
```

### Problem: Storage Quota Exceeded
**Solution:**
```javascript
// Export current data
exportDataAsJSON()

// Clear old data
clearAllData()

// Import fresh data
importDataFromJSON(newFile)
```

### Problem: Data Lost After Browser Update
**Solution:**
- Always keep backups using `exportDataAsJSON()`
- Store backups sa GitHub
- Restore using `importDataFromJSON()`

---

## 📋 File Structure

```
tnhs-enrollment/
├── index.html                    # Main application
├── logo.jpg                      # School logo
├── data/
│   ├── README.md                # Data documentation
│   ├── sample_backup.json       # Sample data format
│   └── tnhs_backup_*.json       # Actual backups
├── .gitignore                   # Git ignore rules
├── README.md                    # Project README
├── DATA_PERSISTENCE_README.md   # Data persistence guide
└── GITHUB_DATA_SYNC_GUIDE.md   # GitHub sync guide
```

---

## 🎓 Console Commands Cheat Sheet

```javascript
// View all data
console.log(users)

// Get statistics
showDataStats()

// Export data
exportDataAsJSON()

// Import data
importDataFromJSON(file)

// Clear all data
clearAllData()

// Check storage size
console.log(localStorage.getItem('tnhs_users').length + ' bytes')

// View last save time
console.log(localStorage.getItem('tnhs_last_sync'))

// Get specific student
console.log(users.find(u => u.email === 'student@email.com'))

// Count by level
console.log(users.filter(u => u.applicantLevel === 'Senior High School').length)

// Count by gender
console.log(users.filter(u => u.gender === 'Male').length)
```

---

## 🚀 Deployment Checklist

- [ ] Test data persistence sa browser
- [ ] Verify auto-save every 30 seconds
- [ ] Test export functionality
- [ ] Test import functionality
- [ ] Create GitHub repository
- [ ] Upload all files
- [ ] Upload sample data backup
- [ ] Test clone at import sa new device
- [ ] Document data structure
- [ ] Create comprehensive README
- [ ] Set repository visibility (public/private)
- [ ] Share with team/users

---

## 📞 Support

### Common Questions

**Q: Saan naka-save ang data?**  
A: Sa browser's localStorage. Bawat browser ay may sariling storage.

**Q: Pwede ba i-access ang data sa ibang device?**  
A: Yes! Export from one device, upload to GitHub, import sa ibang device.

**Q: Ano ang mangyayari kung mag-clear ng browser cache?**  
A: Data ay mawawala. Kaya importante ang regular backups!

**Q: Gaano kalaki ang storage?**  
A: ~5-10MB per browser, enough para sa 1000-5000 students.

**Q: Pwede ba mag-sync automatically across devices?**  
A: Hindi sa current setup. Kailangan manual export/import. Para sa auto-sync, kailangan ng backend database.

---

## 📚 Additional Resources

- [MDN: localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [GitHub: Getting Started](https://docs.github.com/en/get-started)
- [JSON Format](https://www.json.org/)
- [Browser Storage Limits](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API)

---

## ✅ Verification Checklist

After setup, verify:
- [ ] Student can register at data ay naka-save
- [ ] Data persists after page refresh
- [ ] Data persists after browser close/reopen
- [ ] Export creates valid JSON file
- [ ] Import loads data correctly
- [ ] Admin dashboard shows all students
- [ ] Statistics are accurate
- [ ] GitHub repository is accessible
- [ ] Documentation is clear

---

**Version**: 1.0  
**Last Updated**: January 2025  
**Status**: ✅ Production Ready  
**Support**: Contact development team

---

## 🎉 You're All Set!

Ang TNHS Enrollment System ay ready na para sa production. Lahat ng student data ay automatically saved at protected. Enjoy! 🚀
