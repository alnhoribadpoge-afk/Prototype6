# Student Data - Backup & Recovery

## 📁 Folder Contents

This folder contains student data backups para sa TNHS Enrollment System.

### Files

- **sample_backup.json** - Sample data format (2 student records)
- **tnhs_backup_*.json** - Actual student data backups

---

## 📋 Data Format

Each backup file contains:

```json
{
  "users": [
    {
      "userId": "TNHS20250115001",
      "lrn": "123456789012",
      "email": "student@tnhs.edu.ph",
      "password": "SecurePassword",
      "firstName": "Juan",
      "middleName": "de la",
      "lastName": "Cruz",
      "contact": "09123456789",
      "applicantLevel": "Senior High School",
      "gradeLevel": "11",
      "strand": "STEM",
      "section": "STEM-A",
      "gender": "Male",
      "studentStatus": "New Student",
      "lastSchool": "Sample High School",
      "sf1Submitted": true,
      "sf1Data": { /* detailed SF1 information */ }
    }
  ],
  "exportDate": "2025-01-15T10:30:45.123Z",
  "totalRecords": 150,
  "version": "1.0"
}
```

---

## 🔄 How to Use

### Import Data
1. Open `index.html` sa browser
2. Open browser console (F12)
3. Run: `importDataFromJSON(file)`
4. Select ang JSON file from this folder
5. Data ay automatically loaded at saved

### Export Data
1. Open browser console (F12)
2. Run: `exportDataAsJSON()`
3. File ay automatically downloaded
4. Save sa folder na ito

---

## 📊 Data Fields Explained

| Field | Description | Example |
|-------|-------------|---------|
| userId | Unique student ID | TNHS20250115001 |
| lrn | Learner Reference Number | 123456789012 |
| email | Student email | juan@tnhs.edu.ph |
| password | Login password | SecurePass123 |
| firstName | Given name | Juan |
| middleName | Middle name | de la |
| lastName | Family name | Cruz |
| contact | Phone number | 09123456789 |
| applicantLevel | JHS or SHS | Senior High School |
| gradeLevel | Grade 7-12 | 11 |
| strand | SHS strand | STEM |
| section | Class section | STEM-A |
| gender | Male/Female | Male |
| studentStatus | Old/New student | New Student |
| lastSchool | Previous school | Sample High School |
| sf1Submitted | SF1 form status | true/false |
| sf1Data | Detailed SF1 info | { /* object */ } |

---

## 🔐 Security Notes

- ⚠️ **Do NOT share** backup files publicly
- 🔒 Keep backups sa **secure location**
- 📝 **Verify** file integrity before import
- 🗂️ **Organize** backups by date
- 💾 **Keep multiple** versions

---

## 📈 Backup Schedule

Recommended backup frequency:
- **Daily**: Export at end of day
- **Weekly**: Archive important backups
- **Monthly**: Long-term storage

---

## 🆘 Recovery Procedures

### If Data is Lost
1. Check GitHub repository para sa latest backup
2. Download ang latest backup file
3. Open `index.html` sa browser
4. Import ang backup file
5. Verify data ay complete

### If File is Corrupted
1. Try importing older backup
2. Check file format (must be valid JSON)
3. Validate using JSON validator
4. Contact support if needed

---

## 📞 Support

For issues with data recovery:
1. Check file format
2. Verify JSON validity
3. Try different browser
4. Contact development team

---

**Last Updated**: January 2025  
**Version**: 1.0
