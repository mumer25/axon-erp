# Quick Reference: Bluetooth Thermal Printer Setup

## Installation ✅ DONE
```bash
npm install react-native-thermal-receipt-printer
```

## Files Modified/Created

| File | Changes |
|------|---------|
| `screens/OrderDetailsScreen.js` | Added Bluetooth printer modal and functions |
| `utils/bluetoothPrinter.js` | New service layer for printer management |
| `package.json` | Added `react-native-thermal-receipt-printer` |

## Print Flow

```
OrderDetailsScreen
  ├─ Click Print Button
  └─ handlePrintInvoice()
     └─ showPrintOptions()
        └─ Print Modal Opens
           ├─ Option 1: Bluetooth Thermal (58mm)
           │  ├─ scanBluetoothDevices()
           │  ├─ connectToDevice()
           │  └─ handleBluetoothPrint()
           │
           └─ Option 2: PDF Print
              └─ handlePDFPrint()
```

## Key Functions in OrderDetailsScreen.js

### `showPrintOptions()`
Opens print modal and scans devices
- Calls `scanBluetoothDevices()`

### `scanBluetoothDevices()`
Finds available Bluetooth printers
- Returns device list with name + address
- Shows loading spinner

### `connectToDevice(device)`
Connects to selected printer
- Validates connection
- Updates UI with connected device

### `handleBluetoothPrint()`
Sends formatted receipt to printer
- Prepares receipt data
- Sends via ThermalPrinter.printBluetooth()
- Shows success/error alert

## Android Permissions Required

Add to `app.json` or request at runtime:
```json
"permissions": [
  "android.permission.BLUETOOTH_CONNECT",
  "android.permission.BLUETOOTH_SCAN",
  "android.permission.ACCESS_FINE_LOCATION"
]
```

## Testing

### Physical Device (Android)
1. Enable Bluetooth on both device + printer
2. Pair printer in system settings
3. Run app: `npm start` then select Android
4. Click Print → Select Printer → Print

### Emulator
- Bluetooth won't work on emulator
- Use physical device for testing

## Common Issues & Fixes

### "No Bluetooth devices found"
- ✓ Turn on printer Bluetooth
- ✓ Bring printer closer (within 5m)
- ✓ Unpair and re-pair device
- ✓ Click "Rescan Devices"

### "Permission denied"
- ✓ Grant permissions when prompted
- ✓ Check Settings > Apps > Permissions
- ✓ For Android 12+, need runtime permissions

### "Connection failed"
- ✓ Restart printer and device
- ✓ Check printer battery
- ✓ Re-pair Bluetooth device
- ✓ Try different printer if available

### "Print stuck/not printing"
- ✓ Check paper loaded correctly
- ✓ Restart printer
- ✓ Check printer darkness setting
- ✓ Restart app

## Receipt Format (58mm)

```
═══════════════════════════════
           AXON ERP
═══════════════════════════════
Invoice: ORD-001
Cashier: John Doe
Customer: ABC Corp
───────────────────────────────
Item              Qty   Price
───────────────────────────────
Product Name       2    Rs 500
───────────────────────────────
Subtotal:            Rs 1000.00
Tax:                 Rs 0.00
Total:               Rs 1000.00
═══════════════════════════════
         Thank You!
═══════════════════════════════
```

## Supported Printers

✅ 58mm Bluetooth Thermal Printers including:
- Zebra ZSB Series
- TSC TTP Series  
- Xprinter
- GOOJPRT
- Star Micronics
- Epson TM Series

## State Variables

```javascript
showPrintModal        // Modal visibility
availableDevices      // List of found printers
selectedDevice        // Currently selected printer
isLoadingDevices      // Scanning in progress
isPrinting            // Printing in progress
printError            // Error message if any
```

## For More Details

See: [BLUETOOTH_PRINTER_GUIDE.md](BLUETOOTH_PRINTER_GUIDE.md)

---

**Ready to use!** 🎉

Click Print button in OrderDetailsScreen to start printing directly to your 58mm Bluetooth thermal printer.
