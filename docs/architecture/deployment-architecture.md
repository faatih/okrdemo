# Deployment Architecture

### Deployment Strategy

**Frontend Deployment:**
- **Platform:** Vercel
- **Build Command:** `npm run build`
- **CDN/Edge:** Vercel Edge Network (automatic)

**Backend Deployment:**
- **Platform:** Vercel Serverless Functions
- **Deployment Method:** Git push to main branch (automatic)

### Environments

| Environment | URL | Purpose |
|-------------|-----|---------|
| Development | http://localhost:3000 | Local development |
| Preview | https://okrdemo-git-[branch].vercel.app | PR previews |
| Production | https://okrdemo.vercel.app | Live pilot |

---
