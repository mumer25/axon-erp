# 🎯 Quick Checklist - Bluetooth Printer Setup

## Before You Start - Prepare Printer (One Time Only)

### 1️⃣ Printer Setup
```
☐ Printer is powered ON (check power light)
☐ Printer has paper loaded
☐ Printer Bluetooth is enabled
☐ Make printer discoverable (hold BT button 3-5 sec)
```

### 2️⃣ Phone Setup
```
☐ Phone Bluetooth is ON (Settings → Bluetooth)
☐ Phone is close to printer (within 5-10 meters)
```

### 3️⃣ Pair Printer (Do This ONCE)
```
Settings → Bluetooth:
  ☐ Click "Available devices" or "Scan"
  ☐ Select your printer name
  ☐ Enter PIN (usually 0000 or 1234)
  ☐ Tap "Pair"
  ☐ Wait for "Paired" status to appear

Your printer should now show under "Paired devices"
```

### 4️⃣ Open App
```
☐ Open AXON-ERP app
☐ Navigate to an order
☐ Add items to order
```

---

## When You're Ready to Print - Follow These Steps

### Step 1: Click Print Button
```
In OrderDetailsScreen, bottom right:
Click [🖨 Print] button
```

### Step 2: Choose Bluetooth Option
```
Print Modal opens with 2 options:
  ☐ Select "🖨 Thermal Printer (Bluetooth)"
  ☐ Modal shows your paired printers
```

### Step 3: Grant Permission (First Time Only)
```
App may ask for permissions:
  ☐ Bluetooth
  ☐ Location
  ☐ Nearby Devices

Click "Allow All" or "Allow"
(Only asked once)
```

### Step 4: Select Printer
```
Device list shows:
  ☐ Look for your printer name
  ☐ Tap on it to select
  ☐ Tap again to connect
  ☐ Wait for "Connected ✓" to appear
```

### Step 5: Print Receipt
```
After connected:
  ☐ Click [Print via Bluetooth] button
  ☐ Shows "Printing..." spinner
  ☐ Receipt prints on thermal paper! 🖨️
  ☐ Modal closes automatically
  ☐ Success message appears
```

---

## If Something Goes Wrong - Troubleshooting

### ❌ No Devices Shown in List

**Most Likely:** Printer not paired

```
Fix:
1. Close app
2. Go to Settings → Bluetooth
3. Check if your printer is under "Paired devices"

If NOT paired:
  ☐ Make printer discoverable
  ☐ Tap "Available devices" / "Scan"
  ☐ Select your printer
  ☐ Enter PIN
  ☐ Tap Pair

Then reopen app
```

### ❌ "Permission Denied" Error

**Most Likely:** App doesn't have permission

```
Fix:
1. Go to Settings → Apps
2. Find "AXON-ERP"
3. Tap "Permissions"
4. Enable these:
   ☐ Bluetooth
   ☐ Location
   ☐ Nearby devices (if present)
5. Restart app
6. Try printing again
```

### ❌ No Bluetooth on Phone

**Most Likely:** Bluetooth is turned off

```
Fix:
1. Swipe down from top (notification bar)
2. Look for Bluetooth icon
3. ☐ Tap to turn ON (icon should light up)
4. Check it shows "Bluetooth is on"
5. Try printing again
```

### ❌ Printer Not Responding

**Most Likely:** Printer is off or frozen

```
Fix:
1. ☐ Turn OFF printer completely
2. ☐ Wait 30 seconds
3. ☐ Turn ON printer
4. ☐ Wait for light to stop blinking (initialization done)
5. ☐ Try printing again
```

### ❌ Still Not Working?

**Do the Nuclear Restart:**
```
1. Phone:
   ☐ Turn OFF Bluetooth
   ☐ Wait 10 seconds
   ☐ Turn ON Bluetooth

2. Printer:
   ☐ Turn OFF (complete shutdown)
   ☐ Wait 30 seconds
   ☐ Turn ON
   ☐ Wait for initialization

3. App:
   ☐ Close app completely
   ☐ Reopen app
   ☐ Try printing again
```

---

## Permission Checklist

Make sure app has these permissions:

```
Settings → Apps → AXON-ERP → Permissions:

☐ Bluetooth (Required)
☐ Location (Required for Bluetooth)
☐ Nearby devices (If available)

If any show "Not allowed":
  1. Tap to enable
  2. Tap "Allow" or "Allow this time"
  3. Restart app
```

---

## Success Indicators ✅

### App is Ready When:
```
☐ Printer appears in device list
☐ "Connected: [PRINTER-NAME]" message shows
☐ [Print via Bluetooth] button is clickable
```

### Print Successful When:
```
☐ "Printing..." spinner appears
☐ Receipt prints on thermal paper
☐ Modal closes automatically
☐ "Success" message appears
☐ Paper comes out of printer
```

---

## Device List Should Look Like This:

```
📱 Available Devices:

☐ PRINTER-58MM-ABC
   00:11:22:33:44:55
   
☐ THERMAL-PRINTER-XYZ
   AA:BB:CC:DD:EE:FF
   
(Your paired printer should be here)
```

---

## Environment Checklist

```
Hardware:
  ☐ Printer powered ON
  ☐ Paper loaded in printer
  ☐ Printer not too far (within 10m)
  ☐ No obstacles between phone and printer

Phone:
  ☐ Bluetooth enabled in Settings
  ☐ Battery level adequate (>20%)
  ☐ Not in airplane mode
  ☐ Date/time set correctly

App:
  ☐ Latest version installed
  ☐ Permissions granted
  ☐ App fully closed then reopened
```

---

## Quick Reference

| What | Where | Action |
|------|-------|--------|
| Pair printer | Settings → Bluetooth | One time setup |
| Check pairing | Settings → Bluetooth → Paired devices | Should show printer |
| Grant permissions | Settings → Apps → AXON-ERP → Permissions | Enable all |
| Print receipt | OrderDetailsScreen → [Print] button | Follow 5-step process |
| Turn on Bluetooth | Settings → Bluetooth | Toggle ON |
| Enable printer BT | On printer device | Hold BT button 3-5 sec |

---

## Common Questions

**Q: Why does it ask for permission?**
A: Android requires permission to access Bluetooth. Grant it once, then it remembers.

**Q: Do I pair every time?**
A: No! Pair once in Settings, then printer stays paired. App just connects to it.

**Q: Why no devices showing?**
A: Most common: Printer not paired. Go to Settings → Bluetooth and pair it first.

**Q: Can I use multiple printers?**
A: Yes! Pair multiple printers, then select which one to print to in the app.

**Q: What if printer is far away?**
A: Bluetooth range is about 10 meters. Move printer closer if not connecting.

---

## Need More Help?

Read these guides:

1. **Quick fixes:** [BLUETOOTH_TROUBLESHOOTING.md](BLUETOOTH_TROUBLESHOOTING.md)
2. **Detailed guide:** [BLUETOOTH_PRINTER_GUIDE.md](BLUETOOTH_PRINTER_GUIDE.md)
3. **What was fixed:** [PERMISSION_FIX_SUMMARY.md](PERMISSION_FIX_SUMMARY.md)

---

**Last Updated:** January 30, 2026  
**Status:** ✅ Updated with permission fixes  

**Follow this checklist and your printer should work!** 🖨️
