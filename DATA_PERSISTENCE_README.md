# Data Persistence Guide - TNHS Enrollment System

## Overview
Your TNHS Enrollment System now includes **automatic data persistence** using browser localStorage. This means all student data created or modified will be saved locally and persist even after closing the browser.

## How It Works

### Automatic Data Saving
- **Student Registration**: When a student completes the signup form, their data is automatically saved to localStorage
- **SF1 Form Submission**: When a student submits their SF1 form, the data is automatically saved
- **Admin Actions**: Any changes made by admins (section changes, etc.) are automatically saved

### Data Storage Location
- Data is stored in the browser's **localStorage** under the key: `tnhs_users`
- Each browser/device has its own separate storage
- Data persists across browser sessions until manually cleared

## Available Functions

### For Admins/Developers

#### 1. **Export Data as JSON Backup**
```javascript
exportDataAsJSON()
```
- Downloads all student data as a JSON file
- Filename format: `tnhs_backup_YYYY-MM-DD.json`
- Use this to create backups before uploading to GitHub

#### 2. **Import Data from JSON**
```javascript
importDataFromJSON(file)
```
- Restores student data from a previously exported JSON file
- Useful for migrating data between devices or browsers

#### 3. **Clear All Data**
```javascript
clearAllData()
```
- ⚠️ **WARNING**: Permanently deletes all student data from localStorage
- Shows a confirmation dialog before deletion
- Cannot be undone

#### 4. **Save Data Manually**
```javascript
saveUsersToStorage()
```
- Manually saves current data to localStorage
- Automatically called after every student registration/update

#### 5. **Load Data Manually**
```javascript
loadUsersFromStorage()
```
- Manually loads data from localStorage
- Automatically called when the page loads

## GitHub Upload Instructions

### Before Uploading to GitHub:

1. **Export Your Data**
   - Open the browser console (F12)
   - Run: `exportDataAsJSON()`
   - This downloads a backup file

2. **Create a Data Folder** (Optional)
   - Create a `data/` folder in your GitHub repository
   - Upload the exported JSON file there
   - Add instructions for users to import the data

3. **Add to .gitignore** (Optional)
   - If you want to exclude data files from Git:
   ```
   data/
   *.json
   ```

### After Uploading to GitHub:

1. **Users can import data** by:
   - Opening the application
   - Using the import function to load the JSON backup file
   - Or starting fresh with new registrations

## Important Notes

### Data Limitations
- **Browser-specific**: Data is stored per browser/device
- **Storage limit**: Most browsers allow ~5-10MB of localStorage
- **Not encrypted**: Data is stored in plain text in localStorage
- **Not synced**: Data doesn't sync across different browsers or devices

### Best Practices
1. **Regular Backups**: Export data regularly using `exportDataAsJSON()`
2. **Version Control**: Keep backup files in your GitHub repository
3. **Documentation**: Document the data structure for future reference
4. **Testing**: Test data import/export before production use

## Data Structure

Each student record contains:
```javascript
{
  userId: "TNHS...",
  lrn: "12-digit number",
  email: "student@tnhs.edu.ph",
  password: "generated password",
  firstName: "First Name",
  middleName: "Middle Name",
  lastName: "Last Name",
  contact: "09XXXXXXXXX",
  applicantLevel: "Junior/Senior High School",
  gradeLevel: "7-12",
  strand: "STEM/ABM/HUMSS/GAS/TVL-ICT/TVL-HE/TVL-SMAW/TVL-AS",
  section: "Section Name",
  gender: "Male/Female",
  studentStatus: "Old/New Student",
  lastSchool: "School Name",
  sf1Submitted: true/false,
  sf1Data: { /* detailed SF1 form data */ }
}
```

## Troubleshooting

### Data Not Saving?
1. Check browser console for errors (F12)
2. Ensure localStorage is enabled in browser settings
3. Check if storage quota is exceeded
4. Try clearing browser cache and reloading

### Data Lost After Browser Update?
- Browser updates may clear localStorage
- Always keep backups using `exportDataAsJSON()`

### Import Not Working?
1. Ensure JSON file is valid and properly formatted
2. Check browser console for error messages
3. Try exporting and re-importing a test file

## Console Commands Reference

Open browser console (F12) and use these commands:

```javascript
// View all stored data
console.log(users);

// Export data
exportDataAsJSON();

// Clear all data
clearAllData();

// Check storage size
console.log(localStorage.getItem('tnhs_users').length + ' bytes');

// View specific student
console.log(users.find(u => u.email === 'student@email.com'));
```

## Support

For issues or questions about data persistence:
1. Check the browser console for error messages
2. Verify localStorage is enabled
3. Try exporting and re-importing data
4. Contact the development team with error details

---

**Last Updated**: 2025
**Version**: 1.0
