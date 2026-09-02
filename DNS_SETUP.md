# DNS Setup for HireMass Subdomains

## Overview
You have three domains to configure in Namecheap:
1. **hiremass.com** (main site - already configured)
2. **m.hiremass.com** (manager interface)
3. **api.hiremass.com** (API backend)

## Namecheap DNS Configuration

### Step 1: Go to Namecheap Dashboard
- Log in to your Namecheap account
- Find **hiremass.com** in your domains list
- Click "Manage" next to the domain

### Step 2: Configure DNS Records

Click on "Advanced DNS" tab and add these records:

#### Main Site (already configured)
```
Type: CNAME
Host: @
Value: psandeep1117.github.io
TTL: 3600
```

#### Manager Subdomain (m.hiremass.com)
```
Type: CNAME
Host: m
Value: psandeep1117.github.io
TTL: 3600
```

#### API Subdomain (api.hiremass.com)
Choose ONE option based on where you'll host the API:

**Option A: GitHub Pages (same as main)**
```
Type: CNAME
Host: api
Value: psandeep1117.github.io
TTL: 3600
```

**Option B: Vercel (recommended for APIs)**
```
Type: CNAME
Host: api
Value: cname.vercel-dns.com
TTL: 3600
```

**Option C: Custom Server**
```
Type: A
Host: api
Value: [YOUR_SERVER_IP]
TTL: 3600
```

**Option D: AWS/Netlify/Render**
```
Type: CNAME
Host: api
Value: [SERVICE_PROVIDED_DOMAIN]
TTL: 3600
```

## GitHub Pages Configuration

### For m.hiremass.com:
GitHub Pages will automatically route to `m.hiremass.com` if:
1. DNS CNAME record for `m` points to `psandeep1117.github.io`
2. The `/manager` folder exists in your repo (already created)
3. GitHub Pages is enabled in repo settings

### Verify in GitHub:
1. Go to your MSAAS repo settings
2. Scroll to "Pages" section
3. Source: Deploy from a branch
4. Branch: main (or your default branch)
5. Folder: / (root)

## DNS Propagation

After setting DNS records:
- **Immediate**: Changes are made in Namecheap
- **5-30 minutes**: DNS propagates globally
- **Test**: Use `nslookup` or `dig`:
  ```
  nslookup m.hiremass.com
  nslookup api.hiremass.com
  ```

## Verification Checklist

- [ ] CNAME record for `m` created in Namecheap
- [ ] CNAME/A record for `api` created in Namecheap
- [ ] `/manager` folder exists with index.html
- [ ] `/api` folder exists with README.md
- [ ] DNS propagated (test with nslookup)
- [ ] m.hiremass.com loads manager interface
- [ ] api.hiremass.com resolves to your API host

## Troubleshooting

**Subdomain not working after DNS update?**
1. Wait 5-30 minutes for DNS propagation
2. Clear browser cache (Ctrl+Shift+Delete)
3. Verify DNS with: `nslookup m.hiremass.com`
4. Check GitHub Pages settings are enabled

**CNAME conflicts?**
- Each subdomain needs its own DNS record
- Use `Host: m` for m.hiremass.com (not `Host: m.hiremass.com`)
- Use `Host: api` for api.hiremass.com (not `Host: api.hiremass.com`)

**API subdomain not connecting?**
- Verify API host is running and accessible
- Check firewall/security group rules
- Confirm DNS record points to correct host
