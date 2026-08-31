# File and Video Preview Application

A web-based application for previewing files and capturing video from a device camera. This application provides a user-friendly interface (in Arabic) for selecting folders and recording camera footage, with backend integration for data collection.

## 📋 Overview

This is a lightweight HTML5 application that enables users to:
- Browse and select folders/files from their device
- Capture photos/videos using the device camera
- Send collected data to a remote backend server

The interface is presented in Arabic (العربية) for Arabic-speaking users.

## ✨ Features

### File Preview (`📁 معاينة الملفات`)
- Opens a directory/folder browser dialog
- Displays selected files with their names and sizes in bytes
- Sends file information to the backend server for processing
- Provides user feedback on successful transmission

### Video Capture (`▶️ تشغيل الفيديو (كاميرا)`)
- Requests camera access from the user's device
- Captures a photo from the video stream after 1-second stabilization delay
- Converts the captured frame to JPEG format
- Sends the image data to the backend server
- Provides user feedback on successful capture and transmission

## 🚀 Quick Start

### Prerequisites
- A modern web browser with support for:
  - HTML5 File API (`webkitdirectory`)
  - WebRTC (`getUserMedia`)
  - Fetch API
  - Canvas API
  - Base64 encoding

### Configuration

Before using this application, you must configure the backend server URL:

**In `index.html`, update the endpoint URL:**
```javascript
// Replace 'your-ngrok-url.ngrok.io' with your actual backend server
fetch('https://your-ngrok-url.ngrok.io/collect', { ... })
```

### Usage

1. Open `index.html` in a web browser
2. Grant any necessary permissions:
   - **File access:** Allow the browser to access your file system
   - **Camera access:** Allow the browser to use your device camera
3. Click on either button:
   - **📁 معاينة الملفات** - Select files to preview and send
   - **▶️ تشغيل الفيديو (كاميرا)** - Capture and send a photo

## 🔧 Technical Architecture

### Dependencies
- None! This is vanilla JavaScript with no external libraries or frameworks.

### JavaScript Functions

#### `log(msg)`
Displays messages in the output area of the page.

**Parameters:**
- `msg` (string): The message to display

**Returns:** void

**Usage:**
```javascript
log('This message will appear on the page');
```

#### `fileBtn.onclick` Handler
Initializes the file browser when the user clicks the file preview button.

**Process:**
1. Creates a hidden `<input type="file">` element
2. Enables `webkitdirectory` mode for folder selection
3. Iterates through selected files
4. Formats file information (name, size)
5. Sends data via POST request to backend
6. Displays confirmation to user

#### `videoBtn.onclick` Handler
Initializes the camera and captures a photo when the user clicks the video button.

**Process:**
1. Requests camera access using `getUserMedia`
2. Creates a video element to stream camera input
3. Waits 1 second for stabilization
4. Draws video frame to canvas
5. Converts canvas to JPEG data URL
6. Stops camera stream and releases device
7. Sends image data to backend via POST request
8. Displays confirmation to user

### Data Format

#### Files Request
```json
{
  "type": "files",
  "data": "📂 الملفات المختارة:\n- filename.txt (1024 بايت)\n- image.png (2048 بايت)"
}
```

#### Photo Request
```json
{
  "type": "photo",
  "data": "data:image/jpeg;base64,/9j/4AAQSkZJRg..."
}
```

## ⚠️ Security Considerations

### Important Notes

1. **URL Configuration:** The hardcoded ngrok URL must be replaced with your actual backend server before deployment.

2. **Browser Permissions:** The application requests sensitive permissions:
   - File system access (for folder browsing)
   - Camera access (for photo capture)
   - Users must explicitly grant these permissions

3. **Data Transmission:**
   - File lists are sent as plain text JSON
   - Images are sent as Base64-encoded JPEG data
   - Implement HTTPS in production to encrypt data in transit
   - Verify CORS policies are properly configured on the backend

4. **Privacy:**
   - No data is stored locally in the browser
   - All data is immediately sent to the backend
   - Implement proper privacy policies and user consent mechanisms

5. **Error Handling:**
   - Camera access errors are logged to the user
   - Network errors should be handled on the backend
   - Consider adding timeout handling for failed requests

## 🔌 Backend Integration

### API Endpoint

**URL:** `https://your-ngrok-url.ngrok.io/collect`

**Method:** POST

**Content-Type:** application/json

### Request Body Structure

All requests have the following structure:
```json
{
  "type": "files" | "photo",
  "data": "<file_list_or_image_data>"
}
```

### Response Handling

The current implementation does not process server responses. Consider adding:
- Response validation
- Error handling with retry logic
- User feedback for failed requests
- Timeout handling

## 🐛 Browser Compatibility

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| File API | ✅ | ✅ | ✅ | ✅ |
| WebRTC | ✅ | ✅ | ✅ | ✅ |
| Canvas | ✅ | ✅ | ✅ | ✅ |
| Fetch API | ✅ | ✅ | ✅ | ✅ |
| webkitdirectory | ✅ | ✅ | ❌ (Limited) | ✅ |

## 📝 Code Style

- **Language:** JavaScript ES5 (compatible with older browsers)
- **Documentation:** JSDoc comments for functions
- **Comments:** Inline comments for complex logic
- **Formatting:** 4-space indentation

## 🤝 Contributing

When updating this code, ensure:
1. Add JSDoc comments for all functions
2. Add inline comments for complex logic
3. Maintain backward compatibility with older browsers
4. Test file and camera functionality
5. Update this README if adding new features

## 📄 License

[Add your license information here]

## 📞 Support

For issues or questions, please contact [support information]

## 🗂️ File Structure

```
├── index.html          # Main application file
└── README.md          # This file
```

## 🚧 Future Enhancements

- Add video recording functionality (not just photo capture)
- Implement file upload progress indicators
- Add retry logic for failed network requests
- Support multiple file selection modes
- Add internationalization (i18n) for other languages
- Implement error recovery mechanisms
- Add request timeout handling
- Support for batch processing

---

**Last Updated:** August 31, 2026  
**Version:** 1.0  
**Status:** Stable
