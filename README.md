# QR Inventory App

A cross-platform React Native application for managing inventory using QR codes. Create containers, add items, generate QR codes, and track transfers seamlessly across iOS and Android.

## Features

- 📱 **Cross-platform**: Works on both iOS and Android
- 📦 **Container Management**: Create and organize containers
- 📋 **Item Tracking**: Add, edit, and remove items with quantities
- 📱 **QR Code Generation**: Generate printable QR codes for each container
- 📷 **QR Code Scanning**: Instantly access containers by scanning QR codes
- 📤 **Transfer Tracking**: Track when items are given to others
- 📊 **Transaction History**: Complete audit trail of all changes
- 💾 **Offline Storage**: All data stored locally using AsyncStorage

## Project Structure

```
qr-inventory-app/
├── App.tsx                           # Main app component with navigation
├── package.json                      # Dependencies and scripts
├── app.json                         # Expo configuration
├── tsconfig.json                    # TypeScript configuration
├── babel.config.js                  # Babel configuration
├── metro.config.js                  # Metro bundler configuration
├── types/
│   └── index.ts                     # TypeScript type definitions
├── services/
│   ├── StorageService.ts            # Data persistence and management
│   └── QRService.ts                 # QR code generation and parsing
└── screens/
    ├── ContainersScreen.tsx         # Main containers list
    ├── ContainerDetailScreen.tsx    # Individual container view
    ├── CreateContainerScreen.tsx    # Create new container
    ├── EditContainerScreen.tsx      # Edit existing container
    ├── AddItemScreen.tsx           # Add item to container
    ├── EditItemScreen.tsx          # Edit existing item
    ├── QRScannerScreen.tsx         # QR code scanner
    ├── PrintQRScreen.tsx           # QR code display and printing
    ├── TransactionHistoryScreen.tsx # Container transaction history
    ├── HistoryScreen.tsx           # Global activity history
    └── SettingsScreen.tsx          # App settings
```

## Installation

1. **Prerequisites**:
   - Node.js (v16 or later)
   - npm or yarn
   - Expo CLI (`npm install -g @expo/cli`)
   - For iOS development: Xcode
   - For Android development: Android Studio

2. **Clone and setup**:
   ```bash
   git clone https://github.com/Mr615-TN/QR_CODE_APP.git
   cd QR_CODE_APP
   
   # Install dependencies
   npm install
   ```

3. **Install additional required packages**:
   ```bash
   npx expo install expo-camera expo-barcode-scanner
   npx expo install react-native-qrcode-svg react-native-svg
   npx expo install expo-print expo-sharing expo-file-system
   npx expo install @react-native-async-storage/async-storage
   ```

## Development

### Start the development server:
```bash
npx expo start
```

### Run on specific platforms:
```bash
# iOS Simulator
npx expo start --ios

# Android Emulator
npx expo start --android

# Web browser
npx expo start --web
```

### Build for production:
```bash
# iOS
npx expo build:ios

# Android
npx expo build:android
```

## Usage Guide

### Getting Started
1. **Create Your First Container**:
   - Tap "New Container" on the home screen
   - Enter a descriptive name (e.g., "Kitchen Pantry", "Tool Shed")
   - Add an optional description
   - Tap "Create Container"

2. **Add Items**:
   - Open a container
   - Tap "+ Add Item"
   - Enter item name, description, and quantity
   - Tap "Add Item"

3. **Generate QR Code**:
   - In container view, tap "QR Code"
   - Print or share the QR code
   - Attach the printed QR code to your physical container

### Key Features

#### QR Code Workflow
1. **Generate**: Each container gets a unique QR code
2. **Print**: Print QR codes and attach to physical containers
3. **Scan**: Use the Scanner tab to quickly access any container
4. **Manage**: Instantly view and edit container contents

#### Item Management
- **Add Items**: Track name, description, and quantity
- **Edit Items**: Update any item details or quantities
- **Transfer Items**: Record when giving items to others
- **Remove Items**: Delete items completely

#### Transaction History
- **Automatic Tracking**: Every change is automatically logged
- **Detailed Records**: See who received transferred items
- **Complete Audit**: Full history of all container activities

#### Data Management
- **Local Storage**: All data stored on your device
- **No Internet Required**: Works completely offline
- **Export Options**: Share QR codes as PDFs
- **Data Safety**: Clear all data option in settings

## Architecture

### Core Components

1. **StorageService**: Handles all data persistence using AsyncStorage
   - Container CRUD operations
   - Item management within containers
   - Transaction logging
   - Data validation and error handling

2. **QRService**: Manages QR code functionality
   - QR data generation and parsing
   - Printable HTML generation
   - PDF creation for sharing
   - Data validation

3. **Navigation**: Stack and tab-based navigation
   - Bottom tabs for main sections
   - Stack navigation for detailed views
   - Deep linking support for QR scanning

### Data Models

```typescript
// Container: Main organizational unit
Container {
  id: string;
  name: string;
  description?: string;
  items: Item[];
  createdDate: string;
  lastModified: string;
  qrCodeData?: string;
}

// Item: Individual inventory items
Item {
  id: string;
  name: string;
  quantity: number;
  description?: string;
  addedDate: string;
  lastModified: string;
}

// Transaction: Activity tracking
Transaction {
  id: string;
  containerId: string;
  itemId: string;
  type: 'add' | 'remove' | 'update' | 'transfer';
  quantity: number;
  recipientName?: string;
  recipientContact?: string;
  notes?: string;
  timestamp: string;
}
```

## Development Notes

### Key Technologies
- **React Native**: Cross-platform mobile development
- **TypeScript**: Type safety and better development experience
- **Expo**: Simplified React Native development and deployment
- **React Navigation**: Navigation library for React Native
- **AsyncStorage**: Local data persistence
- **Expo Camera/Barcode Scanner**: QR code scanning
- **React Native QRCode SVG**: QR code generation

### Design Principles
- **Modular Architecture**: Separate concerns with services and screens
- **Type Safety**: Full TypeScript implementation
- **Offline First**: No internet dependency
- **User Experience**: Intuitive interface with clear feedback
- **Data Integrity**: Comprehensive validation and error handling

### Performance Considerations
- **Lazy Loading**: Screens load data only when needed
- **Efficient Rendering**: FlatList for large item collections
- **Memory Management**: Proper cleanup and state management
- **Storage Optimization**: JSON-based local storage with compression

## Customization

### Adding New Features
1. **New Screen**: Create in `screens/` directory
2. **Update Navigation**: Add routes in `App.tsx`
3. **Update Types**: Add interfaces in `types/index.ts`
4. **Service Methods**: Add to appropriate service class

### Styling
- All styles use StyleSheet for performance
- Consistent color scheme with CSS variables
- Responsive design for different screen sizes
- Platform-specific adaptations where needed

### Configuration
- **app.json**: Expo and build configuration
- **tsconfig.json**: TypeScript compiler settings
- **babel.config.js**: JavaScript transpilation
- **metro.config.js**: Metro bundler configuration

## Troubleshooting

### Common Issues

1. **Camera Permission Denied**:
   - Check device settings
   - Restart the app
   - Reinstall if necessary

2. **QR Code Not Scanning**:
   - Ensure good lighting
   - Hold camera steady
   - Check QR code isn't damaged

3. **Data Not Persisting**:
   - Check AsyncStorage permissions
   - Verify device storage space
   - Try clearing app data and starting fresh

4. **Build Errors**:
   - Clear node_modules and reinstall
   - Check Expo CLI version
   - Verify all dependencies are installed

### Debug Mode
Enable debug logging by setting `__DEV__` flag:
```typescript
if (__DEV__) {
  console.log('Debug info:', data);
}
```

## Contributing

### Code Standards
- Use TypeScript for all new code
- Follow React Native best practices
- Add proper error handling
- Include JSDoc comments for public methods
- Write tests for critical functionality

### Pull Request Process
1. Fork the repository
2. Create a feature branch
3. Make changes with proper testing
4. Update documentation
5. Submit pull request with detailed description

## License

MIT License - Feel free to use this code for personal or commercial projects.

## Support

For issues, questions, or contributions:
1. Check existing documentation
2. Search closed issues
3. Create new issue with detailed description
4. Include device info and error logs