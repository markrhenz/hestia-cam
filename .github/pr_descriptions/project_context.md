🔥 HESTIA CAM - PROJECT CONTEXT

## 📋 PROJECT OVERVIEW

**Project Name:** Hestia Cam
**Type:** Progressive Web App (PWA) Baby Monitor
**Status:** In Development - Deployment Phase
**Primary Goal:** Free P2P baby monitor for personal use with newborn baby
**Secondary Goal:** Potential future monetization if successful

---

## 🎯 THE GOAL

### Primary Objective:
Build a **completely free, privacy-first baby monitor** that works peer-to-peer between two devices (camera phone + viewer phone) without requiring cloud services, subscriptions, or expensive hardware.

### Why This Project Exists:
- Commercial baby monitors cost ₱7,000-20,000 + subscription fees
- Existing apps (Nanit, Baby Buddy) charge monthly subscriptions
- Privacy concerns with cloud-based video storage
- User (Mark) has a newborn baby and needs a reliable monitoring solution
- User is broke but has time (40-60 hours/week) to build this

### Success Criteria:
1. Works reliably for monitoring baby in real-time  
2. No subscription fees or hidden costs  
3. Video stays local (peer-to-peer only)  
4. Motion and sound detection alerts  
5. Easy to set up (QR code connection)  
6. Works on any smartphone with browser

---

## 🛠️ TECHNICAL ARCHITECTURE

### Core Technologies:

**Frontend:**
- HTML5, CSS3, JavaScript (vanilla - no frameworks)  
- Progressive Web App (PWA) with service worker  
- WebRTC for peer-to-peer video streaming  
- Web Audio API for sound detection  
- Canvas API for motion detection

**Backend/Signaling:**
- PeerJS server on Render.com (free tier)  
- Acts as signaling server only (no video passes through)  
- WebSocket connections for peer discovery

**Deployment:**
- Frontend: Netlify (free tier, auto-deploys from GitHub)  
- Backend: Render.com (free tier, handles PeerJS signaling)  
- UptimeRobot: Keeps Render server awake (pings every 5 min)

**External Libraries:**
- PeerJS v1.5.4 (WebRTC wrapper, peer-to-peer connections)  
- QRCode.js (generates QR codes for easy connection sharing)

---

## ��️ THE PROCESS

### Development Phases:

**Phase 1: Initial Build (COMPLETED)**
- Basic P2P video streaming  
- Camera/Viewer mode selection  
- Simple connection via manual ID entry  
- Low-light mode filter

**Phase 2: Feature Enhancement (COMPLETED)**
- Motion detection (canvas-based frame comparison)  
- Sound detection (Web Audio API with volume monitoring)  
- Browser notifications for alerts  
- Two-way audio support  
- Photo capture  
- Video recording (30min max)  
- Camera flip (front/back)  
- QR code generation for easy sharing  
- Permission explanation screens

**Phase 3: UI/UX Improvements (COMPLETED)**
- Collapsible QR code and debug logs  
- Modern gradient design  
- Status bar with connection states  
- Real-time stats (sound level, connection quality)  
- Toggle controls for all features  
- Fullscreen viewer mode

**Phase 4: PWA Implementation (COMPLETED)**
- Service worker for offline capability  
- Manifest file for "Add to Home Screen"  
- Icon references (icons pending creation)  
- Push notification support

**Phase 5: Deployment Setup (CURRENT)**
- GitHub repository connected to Netlify  
- Render.com PeerJS server configured  
- Path mismatch bug fixed (client now uses `/peerjs/myapp`)  
- Error handling and debug mode added  
- Loading screen implemented

**Phase 6: Testing & Refinement (NEXT)**
- Real-world testing with baby  
- Fine-tune motion/sound thresholds  
- Fix any connection stability issues  
- Optimize for battery life

**Phase 7: Optional Monetization (FUTURE)**
- Market research completed (competitor analysis)  
- Monetization strategy defined (freemium model)  
- Distribution channels identified  
- Not priority until proven to work for personal use

---

## 🔧 TOOLS & SERVICES

### Development Tools:
- **Code Editor:** Any (VS Code recommended)  
- **Version Control:** Git + GitHub  
- **Testing:** Browser DevTools (Chrome/Firefox)  
- **Design:** Canva (for icons/assets)

### Hosting & Infrastructure:
- **Frontend Hosting:** Netlify (free, HTTPS, auto-deploy)  
- **Backend Server:** Render.com (free tier, sleeps when idle)  
- **Server Monitoring:** UptimeRobot (ping every 5 min)  
- **Domain (optional):** Namecheap (optional)

### Libraries & APIs:
- **PeerJS:** WebRTC abstraction — client & server must match path `/peerjs/myapp`  
- **STUN Servers:** Google's free STUN  
- **TURN Server:** OpenRelay (public test server; not for production)  
- **QRCode.js:** QR code generator

---

## 📊 CURRENT STATUS

### What's Working:
✅ Complete HTML/CSS/JS codebase (650+ lines)  
✅ PeerJS integration with proper error handling  
✅ Motion detection algorithm  
✅ Sound detection with cry alerts  
✅ QR code generation  
✅ Two-way audio/video streaming  
✅ Photo/video capture  
✅ Service worker for PWA  
✅ Manifest file for install  
✅ Netlify deployment config  
✅ Debug mode with error catching

### Critical Issues Fixed:
✅ Path mismatch (was `/peerjs`, now `/peerjs/myapp`)  
✅ Incomplete functions (startCamera/startViewer)  
✅ Missing motion/sound detection implementations  
✅ Cut-off artifact code restored  
✅ CDN library loading with fallback  
✅ Loading screen to catch errors

### Pending Tasks:
⚠️ Create icon files (192x192 and 512x512 PNG)  
⚠️ Deploy to production and test  
⚠️ Setup UptimeRobot monitoring  
⚠️ Real-world testing with baby  
⚠️ Fine-tune detection thresholds  
⚠️ Resolve current white screen issue

### Known Limitations:
- Render free tier sleeps (needs UptimeRobot)  
- First connection takes 30-60 sec (server wake)  
- TURN server is public test (not for heavy use)  
- No authentication (anyone with link can view)  
- No cloud recording (all local)  
- Requires internet for initial pairing (P2P after)

---

## 🎨 DESIGN DECISIONS

### Why PWA instead of Native App?
- Zero app store fees, instant updates, cross-platform, faster dev.

### Why Peer-to-Peer?
- Privacy-first, no bandwidth costs, direct low-latency streaming.

### Why This Tech Stack?
- Vanilla JS (no build tools), PeerJS (simplifies WebRTC), Netlify + Render (free tiers).

---

## 💰 COST ANALYSIS
- Frontend: FREE (Netlify)  
- Backend: FREE (Render)  
- Server Monitoring: FREE (UptimeRobot)  
- Domain (optional): ₱650/year

Potential future costs: paid TURN server, payment gateway, marketing.

---

## 🔐 SECURITY & PRIVACY

Current: HTTPS enforced (Netlify), P2P streams (no cloud), no tracking.  
Limitations: no password protection, public TURN, no rate limiting — acceptable for personal use; plan for improvements before public release.

---

## 📱 USER FLOW

Camera Device: start camera → grant permissions → show QR/link.  
Viewer Device: open site → scan QR or paste link → view stream.

Alert Flow: motion/sound triggers browser notification → parent checks stream.

---

## 🐛 DEBUGGING (White screen)
Steps performed: loading screen, lib detection, global error handler, CDN fallbacks. Next: check console/logs and Render logs for server issues.

---

## 📈 ROADMAP (brief)
Immediate: fix white screen, create icons, deploy, test with baby.  
Short/Medium/Long term: stability, battery optimization, TWA/Play Store, optional monetization.

---

## 📚 KEY FILES
- `index.html`, `manifest.json`, `sw.js`, `netlify.toml`, `server.js`, `package.json`  
- Pending: icons (192/512)

---

## 🔗 IMPORTANT URLS
- Frontend: https://hestiacam.netlify.app  
- Backend: https://hestia-cam-operator.onrender.com

---

## 🎯 BOTTOM LINE
Private P2P baby monitor PWA — privacy-first, low-cost, in active development. Next steps: fix white screen, finalize deployment, test with baby.

---

If you want, I can (after you create the PR) add a short checklist to the PR description with the exact QA steps (Lighthouse audits, camera test, smoke CI) and a quick merge/release rollback plan.

