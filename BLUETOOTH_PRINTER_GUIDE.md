# 58mm Bluetooth Thermal Receipt Printer Integration Guide

## Overview
Your AXON-ERP app now supports direct printing to 58mm Bluetooth thermal receipt printers. Users can select a printer and print receipts directly from the OrderDetailsScreen.

## Installation Status ✅

### Packages Installed:
- ✅ `react-native-thermal-receipt-printer` - Core Bluetooth thermal printer library
- ✅ `expo-print` - PDF printing fallback (already installed)

## How It Works

### 1. **Print Button Workflow**
When a user clicks the **"Print"** button on OrderDetailsScreen:

```
Click Print
   ↓
Print Modal Opens (2 Options)
   ├─ Option 1: Bluetooth Thermal Printer
   │  ├─ Scan available devices
   │  ├─ Select/Connect printer
   │  └─ Print receipt directly
   │
   └─ Option 2: PDF Print
      └─ Print or save as PDF
```

### 2. **Bluetooth Printer Connection**

#### Features:
- 🔍 **Auto-scan** for available Bluetooth devices
- 📱 **Device list** showing all nearby printers
- ✅ **Connection status** indicator
- 🖨️ **Direct printing** to 58mm thermal printers
- 📋 **Receipt formatting** optimized for thermal printers

#### Supported Printer Types:
- 58mm Thermal Receipt Printers
- Common brands: 
  - Zebra (ZSB series)
  - TSC (TTP series)
  - Xprinter
  - GOOJPRT
  - Star Micronics
  - Epson

### 3. **Receipt Format**

The receipt is automatically formatted for 58mm thermal printers:

```
============================
           AXON ERP
============================
Invoice: ORD-001
Date: 12/15/2024
Cashier: John Doe
Customer: ABC Corp
Phone: 03001234567
----------------------------
Item              Qty   Price
----------------------------
Product Name      2     Rs 500.00
----------------------------
Subtotal: Rs 1000.00
Tax: Rs 0.00
Discount: Rs 0.00
============================
TOTAL: Rs 1000.00
============================
           Thank You!
```

## User Guide

### Using the Bluetooth Printer

#### Step 1: Prepare the Printer
1. Turn on your 58mm Bluetooth thermal printer
2. Enable Bluetooth on both printer and device
3. Pair devices in system settings (if not already paired)

#### Step 2: Print Receipt
1. Complete your order in OrderDetailsScreen
2. Click the **"Print"** button (bottom right)
3. In the modal, select **"Thermal Printer (Bluetooth)"**
4. Wait for device scan to complete
5. Select your printer from the list
6. Click **"Print via Bluetooth"**

#### Step 3: Troubleshooting

| Issue | Solution |
|-------|----------|
| No devices found | Check if Bluetooth is on; Bring printer closer; Restart app |
| Connection fails | Ensure printer is paired; Check printer batteries; Restart printer |
| Print quality issues | Check paper roll; Adjust printer darkness settings |
| App crashes | Grant Bluetooth permissions when prompted |

### Android Permissions Required

The app will request the following permissions:
- `BLUETOOTH_CONNECT` - To connect to printers
- `BLUETOOTH_SCAN` - To scan for devices
- `ACCESS_FINE_LOCATION` - For Bluetooth discovery

**Grant all permissions** when prompted for full functionality.

## Developer Reference

### Key Files Modified

1. **[screens/OrderDetailsScreen.js](screens/OrderDetailsScreen.js)**
   - Added Bluetooth printer state management
   - New print modal with device selection
   - Bluetooth and PDF print methods

2. **[utils/bluetoothPrinter.js](utils/bluetoothPrinter.js)**
   - Bluetooth service layer
   - Device management
   - Receipt formatting for 58mm printers

### State Variables

```javascript
const [showPrintModal, setShowPrintModal] = useState(false);
const [availableDevices, setAvailableDevices] = useState([]);
const [selectedDevice, setSelectedDevice] = useState(null);
const [isLoadingDevices, setIsLoadingDevices] = useState(false);
const [isPrinting, setIsPrinting] = useState(false);
const [printError, setPrintError] = useState(null);
```

### Key Functions

#### `scanBluetoothDevices()`
Scans for available Bluetooth thermal printers
- Returns array of devices with name and address

#### `connectToDevice(device)`
Connects to selected printer
- Parameters: device object with address and name
- Updates `selectedDevice` state

#### `handleBluetoothPrint()`
Sends receipt data to printer
- Formats receipt for 58mm thermal printer
- Shows loading indicator during printing
- Displays success/error message

#### `handlePDFPrint()`
Alternative PDF printing
- Uses expo-print
- Allows saving as PDF or using system printer

## Customization

### Change Receipt Format

Edit the receipt format in `handleBluetoothPrint()`:

```javascript
const receiptData = {
  header: "YOUR COMPANY NAME",
  invoiceNo: orderNo || "N/A",
  dateTime: new Date().toLocaleString(),
  customerName: customerName,
  customerPhone: customerPhone || "N/A",
  cashierName: cashierName,
  items: details.map((item) => ({
    item_name: item.item_name,
    order_qty: item.order_qty,
    unit_price: item.unit_price,
    amount: item.amount,
  })),
  subtotal: totalAmount,
  tax: 0,
  discount: 0,
  total: totalAmount,
  footer: "Thank you for your purchase!",
};
```

### Adjust Printer Line Width

In `[utils/bluetoothPrinter.js](utils/bluetoothPrinter.js)`, modify:

```javascript
const LINE_WIDTH = 32; // Change based on your printer
```

For 58mm printers, 32 characters per line is standard.

## Testing on Emulator

**Note:** Bluetooth printers won't work on Android emulator. Test on:
- Physical Android device
- iOS device (with BLE printer support)
- Expo Go app on real device

## Troubleshooting

### Android 12+ Issues
- Grant Bluetooth permissions explicitly
- Check manifest permissions:
  ```xml
  <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
  <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  ```

### iOS Issues
- Ensure printer supports BLE (Bluetooth Low Energy)
- Some older 58mm printers may not be compatible
- Test with known compatible printer models

### Paper/Quality Issues
- Check thermal printer paper is correctly loaded
- Adjust printer darkness/intensity settings
- Clean printer head if lines appear
- Ensure paper width matches 58mm specification

## Future Enhancements

Consider adding:
- [ ] Printer settings (darkness, temperature)
- [ ] Multiple receipt copies
- [ ] Receipt templates selection
- [ ] Print history/logs
- [ ] Automatic printer detection
- [ ] QR code on receipts
- [ ] Barcode support
- [ ] Network printer support (WiFi)

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Review printer documentation
3. Check Bluetooth connectivity on device
4. Review app logs in terminal

---

**Last Updated:** January 30, 2026
**Package Version:** react-native-thermal-receipt-printer ^latest
**Tested on:** Android 10+, Expo 54.0.32
