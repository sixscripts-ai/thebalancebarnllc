# The Balance Barn LLC - Domain Integration Documentation

This repository contains documentation for integrating The Balance Barn's iPages-registered domain with Cloudflare.

## Documentation Files

- **[IPAGES_CLOUDFLARE_INTEGRATION.md](./IPAGES_CLOUDFLARE_INTEGRATION.md)** - Complete integration guide with detailed explanations, troubleshooting, and multiple approaches
- **[QUICK_START_CHECKLIST.md](./QUICK_START_CHECKLIST.md)** - Step-by-step checklist to follow during the migration process

## Quick Overview

### The Goal
Migrate thebalancebarn.com from iPages to Cloudflare so it displays the same website as thebalancebarn.cc.

### Current Situation
- **thebalancebarn.com** - Registered on iPages, showing unwanted WordPress site
- **thebalancebarn.cc** - On Cloudflare with the actual desired website

### The Solution
1. Update nameservers at iPages to point to Cloudflare
2. Configure DNS records in Cloudflare to point to your hosting
3. Configure hosting to serve content for both domains
4. Verify everything works

## Getting Started

1. Read the [Quick Start Checklist](./QUICK_START_CHECKLIST.md) first
2. Refer to the [Full Integration Guide](./IPAGES_CLOUDFLARE_INTEGRATION.md) for detailed help
3. Follow the steps in order
4. Be patient - DNS changes can take 24-48 hours to fully propagate

## Common Issues

- **Still seeing old WordPress site**: DNS hasn't propagated yet or browser cache
- **SSL errors**: Configure SSL/TLS settings in Cloudflare
- **404 errors**: Hosting not configured for the new domain

See the full troubleshooting section in the integration guide.

## Support

For questions or issues with this integration, refer to the troubleshooting sections in the documentation files.
