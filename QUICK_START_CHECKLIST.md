# Quick Start Checklist: iPages → Cloudflare Integration

## Before You Start
- [ ] Have access to iPages account
- [ ] Have access to Cloudflare account
- [ ] Know where thebalancebarn.cc is hosted

---

## Step 1: Get Cloudflare Nameservers (5 minutes)

- [ ] Log into Cloudflare
- [ ] Click on thebalancebarn.com
- [ ] Find and copy the two nameservers (e.g., `anna.ns.cloudflare.com`)
- [ ] Write them down:
  - Nameserver 1: ___________________________
  - Nameserver 2: ___________________________

---

## Step 2: Update iPages Nameservers (10 minutes)

- [ ] Log into iPages.com
- [ ] Go to Domain Management
- [ ] Select thebalancebarn.com
- [ ] Find Nameserver settings
- [ ] Change to "Custom Nameservers"
- [ ] Enter your Cloudflare nameservers
- [ ] Save changes
- [ ] Wait 2-24 hours for propagation

---

## Step 3: Find Your Hosting Details (5 minutes)

In Cloudflare, check thebalancebarn.cc DNS records:

- [ ] Look for A record or CNAME record
- [ ] Write down the IP or hostname:
  - Type: ___________________________
  - Points to: ___________________________

---

## Step 4: Configure DNS in Cloudflare (10 minutes)

For thebalancebarn.com in Cloudflare:

- [ ] Add A or CNAME record for root domain (@)
  - Use same IP/hostname as thebalancebarn.cc
  - Enable proxy (orange cloud)

- [ ] Add CNAME for www
  - Points to: thebalancebarn.com
  - Enable proxy (orange cloud)

- [ ] Remove any old DNS records pointing to iPages/WordPress

---

## Step 5: Configure Your Hosting (15 minutes)

- [ ] Log into your hosting control panel
- [ ] Add thebalancebarn.com as addon/alias domain
- [ ] Point to same files/directory as thebalancebarn.cc
- [ ] Update SSL certificate if needed

---

## Step 6: Configure Cloudflare SSL (5 minutes)

- [ ] Go to SSL/TLS settings in Cloudflare
- [ ] Set to "Flexible" or "Full" (depending on hosting)
- [ ] Enable "Always Use HTTPS"
- [ ] Wait 5-10 minutes

---

## Step 7: Test & Verify (10 minutes)

- [ ] Clear browser cache
- [ ] Visit http://thebalancebarn.com
- [ ] Visit https://thebalancebarn.com
- [ ] Visit https://www.thebalancebarn.com
- [ ] Confirm all show your desired website (not WordPress)

---

## If Something's Wrong:

**Still seeing WordPress?**
1. Wait longer (DNS can take 24-48 hours)
2. Check DNS records point to correct hosting
3. Clear browser cache / try incognito mode
4. Purge Cloudflare cache

**SSL errors?**
1. Check SSL/TLS mode in Cloudflare
2. Enable "Always Use HTTPS"
3. Wait 10 minutes and try again

**Nothing works?**
1. Verify nameservers changed at iPages
2. Check nameserver propagation: whatsmydns.net
3. Review IPAGES_CLOUDFLARE_INTEGRATION.md for detailed help

---

## Current Status Tracker

Date started: ___________________________

- Nameservers updated at iPages: ___________________________
- DNS propagated (check whatsmydns.net): ___________________________
- DNS configured in Cloudflare: ___________________________
- Hosting configured: ___________________________
- SSL working: ___________________________
- Website live: ___________________________

---

## Notes & Issues

(Use this space to track any problems or questions)

_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________
