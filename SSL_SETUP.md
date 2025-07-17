# SSL Certificate Setup Guide for hizirceylan.me

This guide will help you set up SSL certificate for your custom domain `hizirceylan.me` with GitHub Pages and Namecheap.

## 📋 Prerequisites

- [x] Domain purchased from Namecheap: `hizirceylan.me`
- [x] GitHub Student Developer Pack activated
- [x] GitHub repository with portfolio website
- [x] 1-year SSL certificate from Namecheap

## 🌐 Step 1: Configure DNS Settings in Namecheap

### 1.1 Login to Namecheap Dashboard
1. Go to [Namecheap.com](https://www.namecheap.com)
2. Login to your account
3. Navigate to "Domain List" → Select your domain `hizirceylan.me`

### 1.2 Configure DNS Records
In the DNS management section, add the following records:

#### A Records (GitHub Pages IP addresses):
```
Type: A Record
Host: @
Value: 185.199.108.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.109.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.110.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.111.153
TTL: Automatic
```

#### CNAME Record (for www subdomain):
```
Type: CNAME Record
Host: www
Value: hizir-ceylan.github.io
TTL: Automatic
```

### 1.3 Save DNS Changes
- Click "Save all changes"
- DNS propagation may take 24-48 hours

## 🐙 Step 2: Configure GitHub Pages

### 2.1 Repository Setup
1. Ensure your repository name is `hizir-ceylan` (matches your GitHub username)
2. Make sure `CNAME` file exists in the root with content: `hizirceylan.me`

### 2.2 Enable GitHub Pages
1. Go to your repository: `https://github.com/hizir-ceylan/hizir-ceylan`
2. Click on "Settings" tab
3. Scroll down to "Pages" section

### 2.3 Configure Custom Domain
1. In the "Custom domain" field, enter: `hizirceylan.me`
2. Click "Save"
3. Check "Enforce HTTPS" (this will be available after SSL is provisioned)

## 🔒 Step 3: SSL Certificate Configuration

### 3.1 GitHub Pages Automatic SSL
GitHub Pages automatically provides SSL certificates via Let's Encrypt for custom domains. Once your DNS is configured:

1. GitHub will automatically detect your custom domain
2. SSL certificate will be provisioned within 24 hours
3. "Enforce HTTPS" option will become available

### 3.2 Using Namecheap SSL Certificate (Alternative)

If you want to use the SSL certificate from Namecheap instead of GitHub's automatic SSL:

#### Generate CSR (Certificate Signing Request):
```bash
openssl req -new -newkey rsa:2048 -nodes -keyout hizirceylan.me.key -out hizirceylan.me.csr
```

#### Fill in the details:
- Country Name: TR
- State: Your state
- City: Your city
- Organization: Your name or organization
- Organizational Unit: IT Department
- Common Name: **hizirceylan.me** (Important!)
- Email: Your email address

#### Submit CSR to Namecheap:
1. Login to Namecheap
2. Go to SSL Certificates
3. Upload the CSR file
4. Complete domain validation
5. Download the certificate files

**Note**: GitHub Pages doesn't support custom SSL certificate upload, so this option would require using a different hosting provider like Cloudflare Pages or Netlify.

## ⚡ Step 4: Enable Cloudflare (Recommended for Advanced SSL)

For enhanced security and performance, consider using Cloudflare:

### 4.1 Add Site to Cloudflare
1. Sign up at [Cloudflare.com](https://www.cloudflare.com)
2. Add your domain `hizirceylan.me`
3. Copy the provided nameservers

### 4.2 Update Nameservers in Namecheap
1. In Namecheap dashboard, go to Domain List
2. Click "Manage" next to your domain
3. Change nameservers to Cloudflare's nameservers
4. Save changes

### 4.3 Configure Cloudflare DNS
Add these records in Cloudflare:
```
Type: CNAME
Name: @
Target: hizir-ceylan.github.io
Proxy status: Proxied (orange cloud)

Type: CNAME
Name: www
Target: hizir-ceylan.github.io
Proxy status: Proxied (orange cloud)
```

### 4.4 SSL/TLS Settings in Cloudflare
1. Go to SSL/TLS → Overview
2. Select "Full (strict)" encryption mode
3. Enable "Always Use HTTPS"
4. Enable "HTTP Strict Transport Security (HSTS)"

## 🧪 Step 5: Testing and Verification

### 5.1 DNS Propagation Check
Use online tools to check DNS propagation:
- [whatsmydns.net](https://www.whatsmydns.net)
- [dnschecker.org](https://dnschecker.org)

### 5.2 SSL Certificate Verification
Check SSL certificate status:
- [SSL Labs SSL Test](https://www.ssllabs.com/ssltest/)
- [SSL Checker](https://www.sslshopper.com/ssl-checker.html)

### 5.3 Website Accessibility Test
1. Visit `https://hizirceylan.me` in your browser
2. Check for the padlock icon in the address bar
3. Verify certificate details by clicking the padlock

## 🔧 Troubleshooting

### Common Issues and Solutions:

#### 1. "DNS does not resolve" error
- **Solution**: Wait for DNS propagation (up to 48 hours)
- Check DNS records are correctly configured

#### 2. "Certificate not yet created" warning
- **Solution**: Wait for GitHub to provision SSL certificate (up to 24 hours)
- Ensure DNS is properly configured

#### 3. Mixed content warnings
- **Solution**: Ensure all resources (images, scripts, etc.) use HTTPS
- Update any hardcoded HTTP links to HTTPS

#### 4. "Enforce HTTPS" option not available
- **Solution**: Wait for SSL certificate to be provisioned
- Check that DNS records are correctly pointing to GitHub Pages

## 📚 Additional Resources

- [GitHub Pages Custom Domain Documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Namecheap DNS Management Guide](https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain/)
- [Cloudflare SSL Setup Guide](https://developers.cloudflare.com/ssl/)

## 📞 Support

If you encounter issues:
1. Check GitHub Pages status: [githubstatus.com](https://www.githubstatus.com)
2. Contact Namecheap support for DNS-related issues
3. Contact Cloudflare support for SSL-related issues (if using Cloudflare)

---

## 🎉 Final Checklist

- [ ] DNS records configured in Namecheap
- [ ] CNAME file added to repository
- [ ] GitHub Pages enabled with custom domain
- [ ] SSL certificate provisioned and working
- [ ] Website accessible via HTTPS
- [ ] All links and resources use HTTPS
- [ ] SSL certificate verified with online tools

**Congratulations!** Your portfolio website should now be live at `https://hizirceylan.me` with a valid SSL certificate! 🎊