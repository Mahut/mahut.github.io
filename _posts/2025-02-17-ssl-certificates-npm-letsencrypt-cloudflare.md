---
layout: post
title: Creating SSL Certificate in Nginx Proxy Manager
description: How to generate and auto-renew Let's Encrypt SSL certificates in Nginx Proxy Manager using Cloudflare DNS validation
summary:
comments: true
tags: [homelab, nginx-proxy-manager, cloudflare, ssl, lets-encrypt]
---

If you self-hosted and/or have a homelab, you'll need to expose some services to the Internet. This guide provides step-by-step instructions for creating SSL certificates for your services in [Nginx Proxy Manager (NPM)](https://nginxproxymanager.com/). 
We'll use [Let's Encrypt](https://letsencrypt.org/fr/) as the certificate authority and [Cloudflare](https://www.cloudflare.com/fr-fr/)'s DNS validation method.

## Prerequisites

{: .indented-list}
- Nginx Proxy Manager installed and running
- A domain managed through Cloudflare
- Access to your Cloudflare admin dashboard
- DNS records properly set up in Cloudflare

## Getting the Cloudflare API Token

First, create an API token that NPM will use to validate your domain ownership. From your Cloudflare dashboard:

{: .indented-list}
1. Navigate to **API Tokens** in the menu
2. Click **Create Token**
3. Select **Custom Token**
4. Configure these settings:
  - Name: "MyHomeLab-ApiToken" (or any descriptive name)
  - Permissions: Zone → DNS → Edit
  - Zone Resources: Your specific domain(s)
5. Create and copy your token

## Setting Up the Certificate in NPM

Now let's create the SSL certificate in Nginx Proxy Manager:

{: .indented-list}
1. Go to your NPM dashboard
2. Navigate to **SSL Certificates**
3. Click **Add SSL Certificate**
4. Configure the certificate:

### Domain Settings

{: .indented-list}
- Primary domain: `example.com`
- Wildcard domain: `*.example.com`

### DNS Challenge Configuration

{: .indented-list}
- Check "Use a DNS Challenge"
- DNS Provider: Cloudflare
- API Token: Paste your Cloudflare token
- Propagation Time: 120 seconds

Click Save and NPM will:

{: .indented-list}
- Verify your domain through Cloudflare
- Generate the SSL certificate
- Set up automatic renewal

## Security Tips

A few important security notes:

{: .indented-list}
- Limit the API token to only the domains you need
- Keep your API token secure
- Check certificate renewal status periodically
- Review NPM logs for any certificate issues