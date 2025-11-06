# iPages to Cloudflare Domain Integration Guide

## Problem Statement
You have:
- **thebalancebarn.com** - Registered on iPages.com (showing unwanted WordPress site)
- **thebalancebarn.cc** - On Cloudflare (showing your actual desired website)

**Goal**: Make thebalancebarn.com show your actual website instead of the WordPress site.

## Solution Overview

There are two main approaches:

### Option 1: Point thebalancebarn.com to the Same Hosting (Recommended)
Configure thebalancebarn.com to point to the same server/hosting as thebalancebarn.cc

### Option 2: Redirect thebalancebarn.com to thebalancebarn.cc
Set up a permanent redirect from .com to .cc

---

## Step-by-Step Instructions

### Phase 1: Get Your Cloudflare Nameservers

1. Log into your Cloudflare account
2. Click on **thebalancebarn.com** in your site list
3. Go to the **DNS** tab or **Overview** page
4. Look for the Cloudflare nameservers (they look like):
   ```
   anna.ns.cloudflare.com
   brad.ns.cloudflare.com
   ```
   (Names will vary - write these down!)

### Phase 2: Update Nameservers at iPages

1. Log into your **iPages.com** account
2. Navigate to **My Domains** or **Domain Management**
3. Find **thebalancebarn.com** and click on it
4. Look for **Nameservers** or **DNS Settings**
5. Choose **Use Custom Nameservers**
6. Replace the iPages nameservers with your Cloudflare nameservers
7. Save changes

**Important**: DNS propagation can take 24-48 hours, but usually completes within a few hours.

### Phase 3: Configure DNS in Cloudflare

Once nameservers are updated, you need to set up DNS records in Cloudflare.

#### Option A: Point to Same Hosting as thebalancebarn.cc

1. In Cloudflare, go to **DNS** settings for thebalancebarn.com
2. Find out where thebalancebarn.cc points to:
   - Check DNS records for thebalancebarn.cc
   - Look for the A record or CNAME that points to your hosting
3. Create the same DNS records for thebalancebarn.com:

   **Example if using an IP address:**
   ```
   Type: A
   Name: @ (or thebalancebarn.com)
   IPv4 address: [Your hosting IP - same as thebalancebarn.cc uses]
   Proxy status: Proxied (orange cloud)
   TTL: Auto
   ```

   **Example if using a hostname:**
   ```
   Type: CNAME
   Name: @
   Target: [Your hosting domain - same as thebalancebarn.cc uses]
   Proxy status: Proxied (orange cloud)
   TTL: Auto
   ```

4. Add a www record too:
   ```
   Type: CNAME
   Name: www
   Target: thebalancebarn.com
   Proxy status: Proxied (orange cloud)
   TTL: Auto
   ```

#### Option B: Redirect to thebalancebarn.cc

If you want thebalancebarn.com to redirect to thebalancebarn.cc:

1. First, set up a basic DNS record:
   ```
   Type: A
   Name: @
   IPv4 address: 192.0.2.1 (dummy IP - will be handled by Page Rule)
   Proxy status: Proxied (orange cloud)
   ```

2. Then create a Page Rule:
   - Go to **Rules** → **Page Rules** in Cloudflare
   - Click **Create Page Rule**
   - URL pattern: `*thebalancebarn.com/*`
   - Setting: **Forwarding URL**
   - Status Code: **301 - Permanent Redirect**
   - Destination URL: `https://thebalancebarn.cc/$2`
   - Save

### Phase 4: Configure Hosting (If Using Option A)

If your hosting is separate from Cloudflare, you need to:

1. Log into your hosting control panel (where thebalancebarn.cc is hosted)
2. Add **thebalancebarn.com** as an additional domain/alias
3. Point it to the same directory/files as thebalancebarn.cc
4. Ensure SSL certificate covers both domains (or use Cloudflare SSL)

---

## Troubleshooting

### Issue: Still Seeing WordPress Site

**Causes:**
1. **Nameservers haven't propagated yet**
   - Wait 24-48 hours
   - Check propagation: https://www.whatsmydns.net/

2. **DNS records pointing to wrong place**
   - Verify your A/CNAME records in Cloudflare point to correct hosting
   - Compare with thebalancebarn.cc DNS records

3. **Caching**
   - Clear browser cache
   - Try incognito/private browsing
   - Clear Cloudflare cache: Caching → Configuration → Purge Everything

4. **Hosting not configured**
   - Ensure your hosting account knows about thebalancebarn.com
   - Add it as an addon/parked domain

### Issue: SSL/HTTPS Errors

1. In Cloudflare, go to **SSL/TLS** settings
2. Set SSL mode to **Flexible** (if hosting doesn't have SSL) or **Full** (if it does)
3. Enable **Always Use HTTPS**
4. Wait a few minutes for changes to propagate

### Issue: Can't Find Where thebalancebarn.cc is Hosted

1. Check DNS records for thebalancebarn.cc in Cloudflare
2. Look for A records - the IP address is your hosting
3. Do a DNS lookup: `nslookup thebalancebarn.cc`
4. Check hosting bills/emails for clues

---

## Verification Steps

After completing setup, verify it's working:

1. **Check Nameservers**:
   ```bash
   nslookup -type=NS thebalancebarn.com
   ```
   Should show Cloudflare nameservers

2. **Check DNS Resolution**:
   ```bash
   nslookup thebalancebarn.com
   ```
   Should show your hosting IP or Cloudflare proxy IP

3. **Test in Browser**:
   - Visit http://thebalancebarn.com
   - Visit https://thebalancebarn.com
   - Visit https://www.thebalancebarn.com
   - All should show your desired website

4. **Check Cloudflare Dashboard**:
   - Should show traffic/requests for thebalancebarn.com
   - Analytics should start populating

---

## Quick Reference: Common iPages Steps

### Finding Nameserver Settings in iPages:

1. Log in to iPages control panel
2. Click **Domains** in the menu
3. Find thebalancebarn.com and click **Manage**
4. Look for **Nameservers** section
5. Click **Change** or **Edit**
6. Select **Use custom nameservers**
7. Enter Cloudflare nameservers
8. Save and confirm

**Note**: iPages may show warnings about losing iPages services (email, etc.) - this is expected.

---

## Need More Help?

If you're still stuck, check:
- Current DNS settings for thebalancebarn.cc in Cloudflare
- Current DNS settings for thebalancebarn.com in Cloudflare
- Where thebalancebarn.cc is actually hosted
- Any error messages you're seeing

The most common issue is that DNS hasn't propagated yet - patience is key!
