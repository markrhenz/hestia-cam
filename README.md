# 🔥 Hestia Cam - Monorepo

Free P2P baby monitor PWA with AI motion detection.

## 📁 Structure

```
hestia-cam/
├── hestia-cam-main/      # Frontend PWA (deploy to Netlify)
└── hestia-cam-server/    # PeerJS server (deploy to Render)
```

## 🚀 Deployment

### Frontend (Netlify)
1. Connect to Git
2. Set base directory: `hestia-cam/hestia-cam-main`
3. Publish directory: `.`
4. Deploy

### Backend (Render)
1. Connect to Git
2. Set root directory: `hestia-cam/hestia-cam-server`
3. Build command: `npm install`
4. Start command: `npm start`
5. Deploy

## 🔧 Local Development

### Frontend
```bash
cd hestia-cam-main
python3 -m http.server 8000
```

### Backend
```bash
cd hestia-cam-server
npm install
npm start
```

## 📱 Features

- ✅ Peer-to-peer video streaming
- ✅ AI face detection (TensorFlow.js)
- ✅ Sound level monitoring
- ✅ Low-light mode
- ✅ QR code connection
- ✅ PWA (installable)
- ✅ Push notifications

## 💰 Cost

- Frontend: FREE (Netlify)
- Backend: FREE (Render)
- Total: ₱0/month

---

Built for personal use with newborn baby. No cloud storage, all P2P.