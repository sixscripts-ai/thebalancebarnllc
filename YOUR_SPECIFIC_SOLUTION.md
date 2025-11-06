# Your Specific Solution: Point thebalancebarn.com to Cloudflare Pages

## Current Setup
- **thebalancebarn.cc** → Points to `balancebarn.pages.dev` (Cloudflare Pages)
- **thebalancebarn.com** → On iPages showing WordPress site (unwanted)
- **Cloudflare Nameservers**: `koa.ns.cloudflare.com` and `sonia.ns.cloudflare.com`

## Goal
Make thebalancebarn.com show the same Cloudflare Pages site as thebalancebarn.cc

---

## Step-by-Step Solution

### Step 1: Update Nameservers at iPages (15 minutes + propagation time)

1. Log into **iPages.com**
2. Go to **Domain Management** or **My Domains**
3. Click on **thebalancebarn.com**
4. Find **Nameservers** or **DNS Settings**
5. Change to **Custom Nameservers**
6. Enter these EXACT nameservers:
   ```
   koa.ns.cloudflare.com
   sonia.ns.cloudflare.com
   ```
7. **Save changes**
8. **Wait 2-24 hours** for DNS propagation (usually faster)

**Check propagation**: https://www.whatsmydns.net/#NS/thebalancebarn.com

---

### Step 2: Add thebalancebarn.com to Cloudflare Pages (10 minutes)

This is the key step! You need to tell your Cloudflare Pages project to accept thebalancebarn.com.

1. Log into **Cloudflare Dashboard**
2. Go to **Workers & Pages** (in left sidebar)
3. Click on your **balancebarn** Pages project
4. Go to **Custom domains** tab
5. Click **Set up a custom domain**
6. Enter: `thebalancebarn.com`
7. Click **Continue**
8. Cloudflare will automatically create the DNS records
9. Also add `www.thebalancebarn.com` if you want www to work

**OR if DNS records need to be manual:**

---

### Step 2 Alternative: Manually Add DNS Records (if needed)

If Cloudflare doesn't auto-create DNS, do this manually:

1. In Cloudflare, make sure you're viewing **thebalancebarn.com** (not .cc)
2. Go to **DNS** → **Records**
3. Add these records:

**For root domain:**
```
Type: CNAME
Name: @ (or thebalancebarn.com)
Target: balancebarn.pages.dev
Proxy status: Proxied (orange cloud)
TTL: Auto
```

**For www:**
```
Type: CNAME
Name: www
Target: balancebarn.pages.dev
Proxy status: Proxied (orange cloud)
TTL: Auto
```

---

### Step 3: Verify It's Working

After nameservers have propagated (check whatsmydns.net):

1. **Clear browser cache** or use incognito mode
2. Visit: https://thebalancebarn.com
3. Visit: https://www.thebalancebarn.com
4. Both should show your Cloudflare Pages site (same as thebalancebarn.cc)

---

## Why This Works

- **Cloudflare Pages** hosts your website at `balancebarn.pages.dev`
- **thebalancebarn.cc** already points there via CNAME
- **thebalancebarn.com** will now ALSO point there via CNAME
- Both domains will show the same website

---

## Troubleshooting

### Still Seeing WordPress Site?

**Causes:**
1. **Nameservers not updated yet**
   - Check: https://www.whatsmydns.net/#NS/thebalancebarn.com
   - Should show `koa.ns.cloudflare.com` and `sonia.ns.cloudflare.com`
   - Wait longer if still showing iPages nameservers

2. **Browser cache**
   - Clear cache or use incognito/private browsing
   - Try different browser

3. **Domain not added to Pages project**
   - Go to Workers & Pages → balancebarn → Custom domains
   - Make sure thebalancebarn.com is listed
   - Status should be "Active"

4. **DNS not configured**
   - Check Cloudflare DNS for thebalancebarn.com
   - Should have CNAME pointing to balancebarn.pages.dev

### SSL Errors?

1. In Cloudflare, go to **SSL/TLS** settings for thebalancebarn.com
2. Set to **Full** (Pages has SSL)
3. Enable **Always Use HTTPS**
4. Wait 5-10 minutes

### "Website not found" on Pages?

The domain isn't added to your Pages project:
1. Workers & Pages → balancebarn → Custom domains
2. Add thebalancebarn.com
3. Cloudflare will handle the DNS automatically

---

## Quick Checklist

- [ ] Updated nameservers at iPages to Cloudflare nameservers
- [ ] Waited for DNS propagation (check whatsmydns.net)
- [ ] Added thebalancebarn.com to Cloudflare Pages custom domains
- [ ] DNS records in Cloudflare point to balancebarn.pages.dev
- [ ] Cleared browser cache
- [ ] Tested https://thebalancebarn.com
- [ ] Tested https://www.thebalancebarn.com

---

## Timeline Expectations

- **Nameserver update at iPages**: Immediate
- **DNS propagation**: 2-24 hours (usually 2-4 hours)
- **Adding custom domain in Pages**: Immediate
- **SSL certificate provisioning**: 5-15 minutes

**Total time**: Usually 2-4 hours, max 24 hours

---

## Important Notes

- **Do NOT delete thebalancebarn.cc** - both domains can coexist and point to the same Pages site
- **Pages custom domains** is the key - the domain must be added there, not just in DNS
- **Once working**, you can optionally set up a redirect from .cc to .com (or vice versa) if you only want one primary domain
