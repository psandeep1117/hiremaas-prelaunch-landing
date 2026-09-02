# HireMass API

API subdomain for hiremass.com

## Setup

This API subdomain is configured for:
- **Domain**: `api.hiremass.com`
- **Type**: REST API / Backend Services
- **Hosting**: [To be configured - see DNS setup below]

## DNS Configuration (Namecheap)

Add these DNS records in Namecheap:

### For api.hiremass.com:
1. **Type**: CNAME or A record
2. **Host**: `api`
3. **Value**: Point to your API hosting (e.g., Vercel, Render, your server, etc.)
4. **TTL**: 3600 (1 hour)

### Example configurations:

**If using Vercel for the API:**
```
Host: api
Type: CNAME
Value: cname.vercel-dns.com
TTL: 3600
```

**If using a custom server:**
```
Host: api
Type: A
Value: [Your server IP]
TTL: 3600
```

**If using AWS/Route53:**
```
Host: api
Type: CNAME
Value: [Your AWS endpoint]
TTL: 3600
```

## Structure

- `README.md` - This file
- API endpoints documentation (to be added)
- Backend code (to be deployed separately from this directory)

## Note

The API backend should be deployed to the server/service configured in DNS. This directory serves as documentation and placeholder.
