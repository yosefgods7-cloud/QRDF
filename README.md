# ReadFlow - Mobile-First PDF Reading PWA

A fast, offline-first PDF reader Progressive Web App designed for smooth continuous reading and efficient handling of large libraries.

## 📁 File Structure

```
/workspace/
├── index.html           # Main application (single-file app)
├── manifest.json        # PWA manifest for installability
├── service-worker.js    # Offline caching and network interception
├── icons/
│   ├── icon-192.png     # 192x192 app icon
│   └── icon-512.png     # 512x512 app icon
└── README.md            # This file
```

## 🚀 GitHub Pages Deployment

1. **Push to GitHub repository:**
   ```bash
   git add .
   git commit -m "Initial ReadFlow PWA"
   git push origin main
   ```

2. **Enable GitHub Pages:**
   - Go to repository Settings → Pages
   - Source: Deploy from branch
   - Branch: main / root
   - Save

3. **Access your PWA:**
   - URL: `https://<username>.github.io/<repo>/`
   - The app will be installable on mobile devices

## ✅ Test Checklist

### PWA Requirements
- [ ] Opens without network (after first load)
- [ ] Shows "Add to Home Screen" prompt
- [ ] Works in standalone mode (no browser UI)
- [ ] manifest.json validates

### Core Functionality
- [ ] Import multiple PDFs via batch selection
- [ ] PDFs stored in IndexedDB
- [ ] Library displays with metadata
- [ ] Filter tabs work
- [ ] Selection mode for batch operations
- [ ] Delete removes from UI and IndexedDB

### Reader Performance
- [ ] First page renders quickly
- [ ] Continuous vertical scroll
- [ ] No lag with large PDFs
- [ ] Only visible pages rendered
- [ ] Resume from last page works
- [ ] Auto-advance to next PDF

### Memory Management
- [ ] Maximum 3 PDFs in memory buffer
- [ ] Oldest PDF evicted when moving forward
- [ ] Next PDF preloaded at 70-80% progress

### Gestures & UX
- [ ] Tap right side scrolls up
- [ ] Tap left side scrolls down
- [ ] Tap center toggles controls

### Security
- [ ] Set 6-digit passcode via settings
- [ ] Lock screen appears on reload
- [ ] Correct passcode unlocks app

### Offline Support
- [ ] Works after disconnecting network
- [ ] Service worker active

## 🔧 Technical Notes

### Storage Schema (IndexedDB)
- id, name, size, order, status, lastPage, totalPages, progress, priority, blob

### Buffer Strategy
- Slot 1: Previous PDF
- Slot 2: Current PDF  
- Slot 3: Next PDF (preloaded)

### Virtual Scrolling
- Only renders visible pages + 2 page buffer
- Destroys off-screen canvases

## ⚠️ Known Limitations

1. PDF blobs have IndexedDB size limits
2. Very large PDFs (500MB+) may cause quota issues
3. First load requires network for PDF.js CDN
4. Passcode uses localStorage (basic security)
