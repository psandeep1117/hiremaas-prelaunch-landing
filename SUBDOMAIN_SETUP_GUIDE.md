# HireMass Subdomain Setup Guide

## What Was Created

### Folder Structure
```
MSAAS/
├── CNAME (fixed: now says "hiremass.com")
├── index.html (main site)
├── manager/
│   └── index.html (m.hiremass.com manager interface)
├── api/
│   └── README.md (api.hiremass.com documentation)
├── DNS_SETUP.md (this setup guide)
└── .git/
```

## Quick Start (4 Steps)

### 1. Fix DNS in Namecheap (5 minutes)
See `DNS_SETUP.md` for full details. Add these records:

```
m     → CNAME → psandeep1117.github.io
api   → CNAME → [choose your API host]
```

### 2. Commit Changes to GitHub
```bash
git add .
git commit -m "Add subdomains: m.hiremass.com (manager) and api.hiremass.com (API)"
git push origin main
```

### 3. Enable GitHub Pages (if not already)
- Go to MSAAS repo → Settings → Pages
- Source: main branch, / (root folder)
- Custom domain: Leave blank (Namecheap handles it)

### 4. Wait for DNS Propagation
- Takes 5-30 minutes
- Test with: `nslookup m.hiremass.com`

## What Each Subdomain Does

### m.hiremass.com (Manager Interface)
- **Status**: Live dashboard ready
- **Files**: `/manager/index.html`
- **Purpose**: Manager login and control center
- **Route**: GitHub Pages serves from `/manager` folder
- **Next**: Add authentication, real dashboard features

### api.hiremass.com (API Backend)
- **Status**: Configuration ready, no backend yet
- **Files**: `/api/README.md` (documentation placeholder)
- **Purpose**: REST API for manager and frontend
- **Route**: Configure in DNS (see DNS_SETUP.md for options)
- **Next**: Choose API host (Vercel, custom server, etc.), deploy backend

## GitHub Pages Routing

GitHub Pages automatically routes subdomains:
- `hiremass.com` → serves `/index.html`
- `m.hiremass.com` → serves `/manager/index.html`
- `api.hiremass.com` → (points to external API server, not served by GitHub Pages)

This works because:
1. Namecheap DNS records point both to `psandeep1117.github.io`
2. GitHub Pages checks the `Host` header
3. Routes to `/` for main domain, `/manager` for subdomain

## API Setup Options

Choose based on your needs:

### Option 1: Vercel (Recommended)
- Free tier available
- Easy deployment
- Built for serverless APIs
- Steps: 
  1. Push API code to `/api` folder (or separate repo)
  2. Deploy to Vercel
  3. Add DNS CNAME: `api` → `cname.vercel-dns.com`

### Option 2: GitHub Pages + Netlify Functions
- GitHub Pages for frontend
- Netlify Functions for serverless API
- Steps:
  1. Create account on Netlify
  2. Deploy to Netlify
  3. Connect custom domain in Netlify settings

### Option 3: Custom Server
- Full control
- More setup required
- Steps:
  1. Set up your server
  2. Deploy API there
  3. Add DNS A record: `api` → `[your-server-ip]`

### Option 4: Keep on GitHub Pages
- Simple, everything in one place
- Limitations: Can't serve dynamic APIs
- Works for: Static JSON endpoints, redirects

## File Descriptions

| File | Purpose |
|------|---------|
| `CNAME` | Tells GitHub Pages domain is hiremass.com |
| `index.html` | Main marketing site |
| `manager/index.html` | Manager dashboard interface |
| `api/README.md` | API documentation and DNS setup |
| `DNS_SETUP.md` | Detailed DNS configuration steps |
| `SUBDOMAIN_SETUP_GUIDE.md` | This file |

## Next Steps

1. **Configure DNS** (DNS_SETUP.md)
2. **Push to GitHub**
3. **Test subdomains** after DNS propagates
4. **Build manager features** (authentication, real dashboard)
5. **Deploy API backend** (choose hosting option)
6. **Connect manager → API** with fetch/axios calls

## Testing Checklist

After DNS propagates:
```bash
# Test main site
curl https://hiremass.com

# Test manager subdomain
curl https://m.hiremass.com

# Test API DNS (should resolve, backend not yet live)
nslookup api.hiremass.com

# Or in browser:
# https://hiremass.com → main site
# https://m.hiremass.com → manager dashboard
```

## Support

If subdomains don't work:
1. Check DNS in Namecheap (verify records exist)
2. Wait for propagation (5-30 min)
3. Clear browser cache
4. Check GitHub Pages settings
5. Verify CNAME file exists and shows "hiremass.com"

---

**Last Updated**: 2026-09-02
**Status**: Subdomains structure ready, DNS configuration pending
