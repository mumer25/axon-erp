# Bluetooth Thermal Printer Integration - Architecture

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    AXON-ERP App                             │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  OrderDetailsScreen                                          │
│  ├─ Displays order items                                    │
│  ├─ Calculates totals                                       │
│  └─ [Print Button] ──→ showPrintOptions()                  │
│                                                              │
│  ┌──────────────────── Print Modal ────────────────────────┐ │
│  │                                                           │ │
│  │  Option 1: Bluetooth Thermal Printer                    │ │
│  │  ├─ scanBluetoothDevices()  → [Loading...]            │ │
│  │  ├─ [Device List]  → Device 1, Device 2               │ │
│  │  ├─ connectToDevice() → Connection established        │ │
│  │  └─ handleBluetoothPrint() → Sending...               │ │
│  │                                                           │ │
│  │  Option 2: PDF Print                                    │ │
│  │  └─ handlePDFPrint() → System print dialog            │ │
│  │                                                           │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                              │
└─────────────────────────────────────────────────────────────┘
         │                                        │
         └────────────────┬─────────────────────┘
                          │
        ┌─────────────────┴──────────────────┐
        │                                     │
        ▼                                     ▼
┌──────────────────┐          ┌──────────────────────────┐
│  Bluetooth API   │          │  Thermal Printer Service │
│                  │          │  (bluetoothPrinter.js)   │
│  • Scan Devices  │          │                          │
│  • Connect       │          │  • Format Receipt        │
│  • Disconnect    │          │  • Text Alignment        │
│  • Permissions   │          │  • 58mm Formatting       │
└──────────────────┘          └──────────────────────────┘
        │                                     │
        └─────────────────┬─────────────────┘
                          │
                          ▼
        ┌────────────────────────────────┐
        │    58mm Thermal Printer         │
        │                                 │
        │  ┌───────────────────────────┐  │
        │  │ AXON ERP - RECEIPT        │  │
        │  │ Invoice: ORD-001          │  │
        │  │ Item 1        Qty: 2      │  │
        │  │ Item 2        Qty: 1      │  │
        │  │ Total: Rs 1500            │  │
        │  │ Thank You!                │  │
        │  └───────────────────────────┘  │
        │     [Paper rolls out]            │
        └────────────────────────────────┘
```

## Component Flow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                  User Action: Press Print                    │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
            ┌────────────────────────────┐
            │  handlePrintInvoice()       │
            │  - Shows print options      │
            │  - Scans devices            │
            └─────────┬──────────────────┘
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
   [Bluetooth]               [PDF/System]
   Thermal Print             Print
        │                           │
        ▼                           ▼
┌─────────────────────┐   ┌──────────────────┐
│ scanBluetoothDevices│   │ handlePDFPrint() │
│                     │   │                  │
│ 1. Request perms    │   │ 1. Load config   │
│ 2. Scan for devices │   │ 2. Generate HTML │
│ 3. Return list      │   │ 3. Print via SDK │
└────────┬────────────┘   └──────────────────┘
         │
         ▼
   [Device List UI]
         │
         ▼
┌─────────────────────┐
│ connectToDevice()    │
│                     │
│ 1. Connect to addr  │
│ 2. Store selection  │
│ 3. Update UI        │
└────────┬────────────┘
         │
         ▼
   [Printer Connected]
         │
         ▼
┌──────────────────────────┐
│ handleBluetoothPrint()    │
│                          │
│ 1. Prepare receipt data  │
│ 2. Format for 58mm       │
│ 3. Send via Bluetooth    │
│ 4. Show completion       │
└──────────────────────────┘
```

## Data Flow

```
OrderDetailsScreen State
    │
    ├─ details[] ─────────┐
    │                      │
    ├─ totalAmount ───────┤
    │                      │
    ├─ customer ──────────┼──→ Receipt Data
    │                      │
    ├─ customerName ──────┤   {
    │                      │    header: "AXON ERP",
    └─ customerPhone ─────┤    invoiceNo: "ORD-001",
                          │    items: [{...}],
    Bluetooth State       │    subtotal: 1500,
    │                      │    total: 1500
    ├─ selectedDevice ────┤   }
    │                      │
    ├─ availableDevices ──┼──→ Format Function
    │                      │   (bluetoothPrinter.
    ├─ isPrinting ────────┤    formatReceiptFor58mm)
    │                      │
    └─ printError ────────┘   ▼
                        [Formatted Text]
                        32 chars/line
                        58mm optimal
                             │
                             ▼
                    ThermalPrinter.
                    printBluetooth()
                             │
                             ▼
                        [Printer Device]
                        Receipt prints!
```

## UI Components

```
OrderDetailsScreen
│
├─ SafeAreaView
│  └─ KeyboardAvoidingView
│     ├─ HeaderCard
│     │  ├─ Customer Name
│     │  └─ [+] Add Items Button
│     │
│     ├─ FlatList (Order Items)
│     │  └─ ItemCard (repeated)
│     │     ├─ Item Name
│     │     ├─ Qty Controls (+/-)
│     │     └─ Amount
│     │
│     └─ BottomBarContainer
│        ├─ Totals Section
│        │  ├─ Total Items
│        │  └─ Total Amount
│        │
│        └─ Buttons Row
│           ├─ [Completed] Button
│           └─ [Print] Button ──→ showPrintOptions()
│
└─ Modal (Print Options)
   └─ Overlay
      └─ ModalContent
         ├─ ModalHeader
         │  ├─ "Print Receipt" Title
         │  └─ [X] Close Button
         │
         ├─ ScrollView
         │  │
         │  ├─ PrintOption (Bluetooth)
         │  │  ├─ Option Title
         │  │  ├─ Device List
         │  │  │  └─ DeviceItem (repeating)
         │  │  │     ├─ Device Icon
         │  │  │     ├─ Device Name
         │  │  │     └─ Device Address
         │  │  │
         │  │  └─ [Print via Bluetooth] Button
         │  │
         │  ├─ Divider
         │  │
         │  └─ PrintOption (PDF)
         │     ├─ Option Title
         │     └─ [Print PDF] Button
         │
         └─ Loading States
            ├─ Scanning...
            ├─ Connecting...
            └─ Printing...
```

## State Management

```
OrderDetailsScreen Component State:

Order Data (existing)
  details: OrderItem[]
  totalAmount: number
  customer: {
    id, name, phone, orderNo, orderDate
  }
  isSynced: boolean
  cashierName: string
  cashierEmail: string

Bluetooth Printer State (new)
  showPrintModal: boolean
    └─ Controls modal visibility
  
  availableDevices: Device[]
    └─ [{ name: string, address: string }, ...]
  
  selectedDevice: Device | null
    └─ { name: string, address: string }
  
  isLoadingDevices: boolean
    └─ Scanning/connecting in progress
  
  isPrinting: boolean
    └─ Receipt being printed
  
  printError: string | null
    └─ Error message if any

Type Definitions:
  Device = { name: string, address: string }
  OrderItem = {
    line_id: number
    item_name: string
    order_qty: number
    unit_price: number
    amount: number
  }
  ReceiptData = {
    header: string
    invoiceNo: string
    dateTime: string
    customerName: string
    customerPhone: string
    cashierName: string
    items: Item[]
    subtotal: number
    tax: number
    discount: number
    total: number
    footer: string
  }
```

## Function Call Hierarchy

```
handlePrintInvoice()
│
└─ showPrintOptions()
   │
   ├─ setShowPrintModal(true)
   └─ scanBluetoothDevices()
      │
      ├─ bluetoothPrinter.requestPermissions()
      ├─ ThermalPrinter.getBluetoothDevices()
      └─ setAvailableDevices(devices)

User selects device:
│
└─ connectToDevice(device)
   │
   ├─ ThermalPrinter.connectPrinter(address)
   ├─ setSelectedDevice(device)
   └─ Alert.alert("Connected")

User clicks Print:
│
└─ handleBluetoothPrint()
   │
   ├─ Prepare receiptData {
   │    header, invoiceNo, items, totals, etc.
   │  }
   │
   ├─ ThermalPrinter.printBluetooth(
   │    address, receiptData
   │  )
   │
   └─ Alert.alert("Success!")

Alternative - PDF Print:
│
└─ handlePDFPrint()
   │
   ├─ getQRConfig()
   ├─ generateInvoiceHTML(config)
   └─ Print.printAsync({html})
```

## Error Handling Flow

```
Action: Scan Devices
  │
  ├─ try
  │  ├─ Request permissions
  │  ├─ Get devices
  │  └─ setAvailableDevices()
  │
  └─ catch (error)
     └─ setPrintError(error.message)
        └─ Display error to user
           with [Rescan] button

Action: Connect Device
  │
  ├─ try
  │  ├─ Call connectPrinter()
  │  └─ setSelectedDevice()
  │
  └─ catch (error)
     └─ Alert with error
        └─ User can try again

Action: Print
  │
  ├─ try
  │  ├─ Format receipt
  │  ├─ Send to printer
  │  └─ setShowPrintModal(false)
  │
  └─ catch (error)
     └─ Alert with error
        └─ Modal stays open
           for retry
```

## File Structure

```
AXON-ERP/
├─ screens/
│  └─ OrderDetailsScreen.js ⭐ [MODIFIED]
│     ├─ 1600+ lines
│     ├─ Bluetooth printer functions
│     ├─ Print modal UI
│     └─ All styles
│
├─ utils/
│  └─ bluetoothPrinter.js ⭐ [NEW]
│     ├─ BluetoothThermalPrinter class
│     ├─ Device management
│     ├─ Receipt formatting
│     └─ 400+ lines
│
├─ package.json ⭐ [MODIFIED]
│  └─ Added: react-native-thermal-receipt-printer
│
├─ IMPLEMENTATION_COMPLETE.md ✨ [NEW]
├─ BLUETOOTH_PRINTER_GUIDE.md ✨ [NEW]
├─ PRINTER_QUICK_START.md ✨ [NEW]
│
└─ [other files unchanged]
```

---

**This architecture provides:**
- ✅ Modular design (separation of concerns)
- ✅ Easy to test each component
- ✅ Clean error handling
- ✅ Responsive UI with loading states
- ✅ User-friendly modal interface
- ✅ Fallback PDF printing option
