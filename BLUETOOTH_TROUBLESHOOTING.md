# 🔧 Bluetooth Printer - Troubleshooting Guide

## Problem: "No Bluetooth devices found" or Not Showing Devices

### ✅ Solution - Step by Step

#### **Step 1: Check Phone Settings**
```
1. Go to Settings
2. Open Bluetooth
3. Toggle Bluetooth ON (should show blue icon)
4. You should see "Bluetooth is on"
```

#### **Step 2: Check Printer is Paired**
```
In Bluetooth Settings:
1. Look for "Paired devices" section
2. Your printer should be listed here
3. If NOT listed, pair it:
   - Make printer Bluetooth discoverable
     (Hold Bluetooth button for 3-5 seconds)
   - Tap "Available devices"
   - Select printer from list
   - Enter PIN (usually 0000 or 1234)
   - Tap "Pair"
```

#### **Step 3: Grant App Permissions**
```
IMPORTANT! This is often the issue.

Method 1: When using app
- Click Print button
- If it asks for permissions, tap "Allow All" or "Allow"

Method 2: Manual permission grant
1. Go to Settings
2. Apps → All Apps
3. Find "AXON-ERP"
4. Tap "Permissions"
5. Enable these permissions:
   ✓ Bluetooth
   ✓ Location
   ✓ Nearby devices (if available)
6. Restart app
```

#### **Step 4: Restart Everything**
```
1. Turn OFF Bluetooth on phone
2. Turn OFF your printer
3. Wait 10 seconds
4. Turn ON printer
5. Wait for it to initialize (light stops blinking)
6. Turn ON Bluetooth on phone
7. Open app
8. Click Print
9. Click "Rescan Devices"
```

---

## Updated Fix - What Changed

### **Improved Bluetooth Scanning**
- Now shows **paired devices** automatically
- Scans for both bonded (paired) and available devices
- Better error messages with helpful hints

### **Better Permission Handling**
- Clearly shows what permissions are needed
- Asks for permission when Print is clicked
- Tells you if permissions are denied and how to fix it

### **Enhanced Error Messages**
- Shows specific steps to fix common issues
- Explains what to check (printer on, Bluetooth enabled, etc.)
- Provides "Rescan" button to try again

### **Info Box**
- Reminds users to pair printer in Bluetooth settings first
- Shows at top of print modal

---

## Checklist Before Printing

✅ **Hardware**
- [ ] Printer is powered ON
- [ ] Printer has paper loaded
- [ ] Printer is charged/has battery

✅ **Bluetooth**
- [ ] Phone Bluetooth is ON
- [ ] Printer Bluetooth is ON
- [ ] Printer is within 5-10 meters of phone

✅ **Pairing**
- [ ] Printer is paired in Settings → Bluetooth
- [ ] Shows in "Paired devices" list
- [ ] No other devices trying to connect

✅ **Permissions**
- [ ] App has Bluetooth permission (check Settings → Apps → AXON-ERP → Permissions)
- [ ] App has Location permission
- [ ] Permissions were granted when app asked

✅ **App**
- [ ] App is updated to latest version
- [ ] App was restarted after permissions change
- [ ] Order has items added

---

## Step-by-Step Print Process (Updated)

### **Step 1: Create Order**
```
Add items to order in app
- Item 1
- Item 2
- etc.
```

### **Step 2: Click Print**
```
Click [🖨 Print] button (bottom right)
→ Print Modal opens
→ Shows info box "Make sure printer is paired"
```

### **Step 3: Permissions Request**
```
If first time, app asks for permissions:
- Bluetooth
- Location
- Nearby devices

Tap "Allow" for all
```

### **Step 4: Scan Devices**
```
Bluetooth Printer section shows:
- Loading spinner and "Scanning devices..."
- Wait 2-3 seconds
```

### **Step 5: Select Device**
```
After scan completes:
✅ Shows list of paired printers
  - Select your printer
  - Tap on it to select
```

### **Step 6: Connect**
```
App automatically connects when you tap device
- Shows loading spinner
- Shows "Connected: PRINTER-NAME" ✓
```

### **Step 7: Print**
```
Click [Print via Bluetooth] button
- Shows "Printing..." spinner
- Receipt prints on thermal paper! 🖨️
- Modal closes
```

---

## Common Issues & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| No devices shown | Permissions not granted | Tap "Allow" when asked, or grant in Settings |
| No devices shown | Printer not paired | Pair printer in Settings → Bluetooth first |
| No devices shown | Bluetooth off on phone | Turn on Bluetooth in Settings |
| No devices shown | Bluetooth off on printer | Turn on printer |
| Connection fails | Bluetooth range too far | Move printer closer (within 5m) |
| Connection fails | Printer is frozen | Restart printer |
| Permission error | App doesn't have permission | Go to Settings → Apps → AXON-ERP → Permissions, enable all |
| Still not working | Multiple issues | Restart phone and printer completely |

---

## If Still Having Issues

### **Try This Nuclear Option:**

1. **Restart Everything**
   ```
   Phone:
   - Turn off Bluetooth
   - Wait 10 seconds
   - Turn on Bluetooth
   
   Printer:
   - Turn off (all the way off)
   - Wait 30 seconds
   - Turn on
   - Wait for it to fully initialize
   ```

2. **Re-pair Printer**
   ```
   Settings → Bluetooth
   - If printer already paired, tap ⚙ next to it
   - Select "Unpair"
   - Make printer discoverable
   - Scan for devices
   - Pair again
   ```

3. **Check Permissions**
   ```
   Settings → Apps → All Apps → AXON-ERP
   → Permissions
   → Check all are enabled:
     ✓ Bluetooth
     ✓ Location
     ✓ Phone (if present)
   ```

4. **Force Close App**
   ```
   Settings → Apps → AXON-ERP
   → Advanced (or ⋮ menu)
   → Force Stop
   
   Then reopen app
   ```

5. **Clear App Cache**
   ```
   Settings → Apps → AXON-ERP
   → Storage → Clear Cache
   (NOT Clear Data)
   
   Reopen app
   ```

---

## Technical Details

### **What Was Fixed**

1. **Better Permission Requests**
   - Now checks if permissions are granted
   - Shows helpful error message if not
   - Tells user how to grant permissions

2. **Device Detection**
   - Gets bonded (paired) devices from phone
   - Filters out non-printer devices
   - Shows device address for debugging

3. **Better Error Messages**
   - Multi-line error messages with specific steps
   - Suggests what to check
   - Provides "Rescan" button to retry

4. **Logging**
   - Console logs all steps for debugging
   - Shows in terminal when you run `npm start`
   - Helps identify where issue is

### **How It Works Now**

```
User clicks Print
    ↓
App checks permissions
    ├─ Not granted?
    │  └─ Request from user
    │     └─ Show helpful message if denied
    │
    └─ Granted?
       └─ Scan for devices
          ├─ Get paired devices
          ├─ Get scanned devices
          └─ Combine & show list
             └─ User selects
                └─ Auto-connect
                   └─ User prints
```

---

## Next Steps

1. **Update your app** with these fixes
2. **Restart app** completely
3. **Grant permissions** when asked
4. **Try printing** again

If still having issues, check:
- Phone Bluetooth Settings (is printer paired?)
- App Permissions (are they all enabled?)
- Printer Power (is it really on?)
- Distance (are they close enough?)

---

**Status:** ✅ Fixed  
**Version:** Updated with better permission & device handling  
**Date:** January 30, 2026
