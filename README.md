# Dita Frontend - React Web Interface

Frontend aplikasi web untuk Dita AI Assistant menggunakan React + Vite.

## 🚀 Quick Start

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 📦 Dependencies

- **React 18** - UI library
- **Vite** - Build tool & dev server
- **Tailwind CSS** - Utility-first CSS framework
- **Framer Motion** - Animation library
- **Web Audio API** - Audio recording & playback

## 🎨 Components

### VoiceOrb (`src/components/VoiceOrb.jsx`)
Komponen utama untuk visualisasi voice interaction:
- Animated orb dengan gradient colors
- Waveform visualization
- Audio level reactive animations
- Different states (idle, listening, speaking)

### useVoiceChat Hook (`src/hooks/useVoiceChat.js`)
Custom React hook untuk handling:
- WebSocket connection ke backend
- Audio recording dengan MediaRecorder API
- Audio format conversion (WebM → WAV)
- Audio playback dari server response
- State management (recording, processing, etc.)

## 🔧 Configuration

### WebSocket URL
Edit di `src/hooks/useVoiceChat.js`:
```javascript
const WEBSOCKET_URL = 'ws://localhost:8000/ws/voice'
```

### Audio Recording Settings
```javascript
audio: {
  channelCount: 1,
  sampleRate: 16000,
  echoCancellation: true,
  noiseSuppression: true,
}
```

## 🎭 Styling

Menggunakan Tailwind CSS dengan custom theme:

### Colors
- Primary gradient: `#667eea` → `#764ba2`
- Listening state: Blue (`#3b82f6`)
- Speaking state: Purple (`#a855f7`)

### Animations
- Fade in animations
- Pulse effects
- Framer Motion untuk smooth transitions

## 🏗️ Project Structure

```
src/
├── components/
│   └── VoiceOrb.jsx       # Main voice orb component
├── hooks/
│   └── useVoiceChat.js    # WebSocket & audio logic
├── App.jsx                # Main app component
├── App.css                # App-specific styles
├── index.css              # Global styles + Tailwind
└── main.jsx               # Entry point
```

## 🔊 Audio Processing

### Recording Flow
1. Request microphone permission
2. Create MediaRecorder with WebM format
3. Collect audio chunks
4. On stop: Convert to WAV format
5. Encode to base64
6. Send via WebSocket

### Playback Flow
1. Receive base64 audio from server
2. Decode to Blob
3. Create audio URL
4. Play with HTML5 Audio API

## 🐛 Debugging

### Check WebSocket Connection
```javascript
// In browser console
console.log(wsRef.current.readyState)
// 0: CONNECTING, 1: OPEN, 2: CLOSING, 3: CLOSED
```

### Check Audio Recording
```javascript
// Check if microphone is accessible
navigator.mediaDevices.getUserMedia({ audio: true })
  .then(() => console.log('Mic OK'))
  .catch(err => console.error('Mic error:', err))
```

## 📱 Browser Support

- Chrome/Edge: ✅ Full support
- Firefox: ✅ Full support
- Safari: ⚠️ Limited (WebM format issues)
- Mobile browsers: ⚠️ Testing required

## 🔐 Security Notes

- Microphone access requires user permission
- HTTPS required in production (or localhost)
- WebSocket over WSS in production

## 🚀 Production Build

```bash
# Build
npm run build

# Output in: dist/

# Serve with any static server
npx serve dist
```

## 📊 Performance

- Lazy loading not implemented (small app)
- Audio chunks buffered in memory
- WebSocket keep-alive every 30s

## 🎯 Future Improvements

- [ ] Add wakeword detection in browser
- [ ] Support multiple languages
- [ ] Add conversation history
- [ ] Improve mobile responsiveness
- [ ] Add dark/light theme toggle
- [ ] Add settings panel
- [ ] Implement retry logic for failed connections

## 🔗 Related Files

- Backend API: `../Project Dita/backend/main.py`
- Configuration: `../Project Dita/config.yaml`
- Main README: `../README.md`

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.
