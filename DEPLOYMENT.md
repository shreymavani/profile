# Deployment Guide - Shrey Mavani Portfolio

Quick guide to deploy your portfolio website to various platforms.

---

## 🚀 Option 1: GitHub Pages (Recommended - Free & Easy)

### Steps:
1. **Create a GitHub repository**
   ```bash
   cd /Users/smavani/personal/portfolio-website
   git init
   git add .
   git commit -m "Initial commit: Senior FAANG-level portfolio"
   ```

2. **Create repo on GitHub** (via website)
   - Go to github.com/new
   - Name it: `portfolio-website` or `shreymavani.github.io`
   - Don't initialize with README

3. **Push to GitHub**
   ```bash
   git remote add origin https://github.com/ShreyMavani/portfolio-website.git
   git branch -M main
   git push -u origin main
   ```

4. **Enable GitHub Pages**
   - Go to repository Settings → Pages
   - Source: Deploy from branch
   - Branch: main / (root)
   - Click Save

5. **Access your site**
   - URL: `https://shreymavani.github.io/portfolio-website/`
   - Or if repo is `shreymavani.github.io`: `https://shreymavani.github.io/`

### Custom Domain (Optional)
1. Buy domain (Namecheap, GoDaddy, etc.)
2. Add CNAME file with your domain
3. Configure DNS A records:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
4. Add custom domain in GitHub Pages settings

---

## 🚀 Option 2: Vercel (Professional - Free)

### Steps:
1. **Install Vercel CLI**
   ```bash
   npm install -g vercel
   ```

2. **Deploy**
   ```bash
   cd /Users/smavani/personal/portfolio-website
   vercel
   ```

3. **Follow prompts**
   - Login with GitHub
   - Select deployment settings
   - Done! Get instant URL

### Features:
- ✅ Automatic HTTPS
- ✅ CDN globally distributed
- ✅ Auto-deploy on git push
- ✅ Free custom domain
- ✅ Preview deployments

---

## 🚀 Option 3: Netlify (Great for CI/CD)

### Method A: Drag & Drop
1. Go to [netlify.com/drop](https://app.netlify.com/drop)
2. Drag the entire `portfolio-website` folder
3. Done! Get instant URL

### Method B: Git Integration
1. Push code to GitHub (see Option 1)
2. Go to [netlify.com](https://netlify.com)
3. Click "New site from Git"
4. Connect GitHub repository
5. Deploy settings:
   - Build command: (leave empty)
   - Publish directory: `.`
6. Click "Deploy site"

### Features:
- ✅ Automatic HTTPS
- ✅ Form handling (if you add forms later)
- ✅ Serverless functions support
- ✅ Free custom domain
- ✅ Instant rollbacks

---

## 🚀 Option 4: AWS S3 + CloudFront (Enterprise)

### Steps:
1. **Create S3 Bucket**
   ```bash
   aws s3 mb s3://shreymavani-portfolio
   ```

2. **Upload files**
   ```bash
   cd /Users/smavani/personal/portfolio-website
   aws s3 sync . s3://shreymavani-portfolio --exclude ".git/*"
   ```

3. **Enable Static Website Hosting**
   ```bash
   aws s3 website s3://shreymavani-portfolio \
     --index-document index.html \
     --error-document index.html
   ```

4. **Set Bucket Policy** (make public)
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [{
       "Sid": "PublicReadGetObject",
       "Effect": "Allow",
       "Principal": "*",
       "Action": "s3:GetObject",
       "Resource": "arn:aws:s3:::shreymavani-portfolio/*"
     }]
   }
   ```

5. **Create CloudFront Distribution** (Optional - for HTTPS & CDN)
   - Go to CloudFront console
   - Create distribution
   - Origin: Your S3 bucket
   - Enable HTTPS
   - Add custom domain (optional)

### Features:
- ✅ Full control
- ✅ CloudFront CDN
- ✅ Custom SSL certificates
- ✅ Professional setup
- 💰 ~$0.50-5/month

---

## 🌐 Custom Domain Setup

### If using GitHub Pages:
1. **Add CNAME file** to repository root:
   ```
   shreymavani.com
   ```

2. **Configure DNS** at your registrar:
   ```
   Type: A
   Host: @
   Value: 185.199.108.153
   
   Type: A
   Host: @
   Value: 185.199.109.153
   
   Type: A
   Host: @
   Value: 185.199.110.153
   
   Type: A
   Host: @
   Value: 185.199.111.153
   
   Type: CNAME
   Host: www
   Value: shreymavani.github.io
   ```

### If using Vercel/Netlify:
1. Go to domain settings in dashboard
2. Add custom domain
3. Follow DNS configuration instructions provided
4. Usually just need to add:
   ```
   Type: A
   Host: @
   Value: (provided IP)
   
   Type: CNAME
   Host: www
   Value: (provided domain)
   ```

---

## 📊 Recommended Domain Names

### Available (as of Jan 2026):
- `shreymavani.com` - Professional, personal brand
- `mavani.dev` - Developer-focused, trendy
- `shreymavani.io` - Tech-focused
- `shreyworks.dev` - Showcase work

### Domain Registrars:
1. **Namecheap** - Good prices, easy interface
2. **Google Domains** - Clean, integrated with Google services
3. **Cloudflare** - Best prices, built-in CDN
4. **GoDaddy** - Popular, good support

---

## 🔧 Post-Deployment Checklist

### ✅ Functionality
- [ ] All navigation links work
- [ ] Dark mode toggle works
- [ ] Mobile menu works
- [ ] Smooth scrolling works
- [ ] Animations trigger properly
- [ ] Contact links work
- [ ] All images/icons load

### ✅ SEO
- [ ] Add meta description
- [ ] Add Open Graph tags
- [ ] Add Twitter Card tags
- [ ] Submit sitemap to Google
- [ ] Add Google Analytics (optional)

### ✅ Performance
- [ ] Test on mobile devices
- [ ] Test on different browsers
- [ ] Check page load speed (GTmetrix, PageSpeed Insights)
- [ ] Verify HTTPS works

### ✅ Professional
- [ ] Update LinkedIn with portfolio URL
- [ ] Update resume with portfolio URL
- [ ] Share on Twitter/social media
- [ ] Add to GitHub profile README

---

## 📈 Analytics Setup (Optional)

### Google Analytics 4
1. Create GA4 property at analytics.google.com
2. Get measurement ID (G-XXXXXXXXXX)
3. Add to `<head>` in index.html:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### Plausible (Privacy-friendly alternative)
1. Sign up at plausible.io
2. Add to `<head>`:

```html
<script defer data-domain="shreymavani.com" src="https://plausible.io/js/script.js"></script>
```

---

## 🔒 Security Best Practices

### Content Security Policy (Add to index.html head)
```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; 
               style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; 
               font-src 'self' https://fonts.gstatic.com; 
               img-src 'self' https://cdn.jsdelivr.net data:; 
               script-src 'self' 'unsafe-inline';">
```

### Add to GitHub Pages (create _headers file)
```
/*
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  X-XSS-Protection: 1; mode=block
  Referrer-Policy: strict-origin-when-cross-origin
```

---

## 🎯 Quick Deploy Commands

### GitHub Pages
```bash
git add .
git commit -m "Update portfolio"
git push
```

### Vercel
```bash
vercel --prod
```

### Netlify
```bash
netlify deploy --prod
```

### AWS S3
```bash
aws s3 sync . s3://shreymavani-portfolio --delete
aws cloudfront create-invalidation --distribution-id XXX --paths "/*"
```

---

## 💡 Pro Tips

1. **Use Git branches** for testing changes
2. **Set up auto-deploy** via GitHub Actions
3. **Add SSL certificate** for custom domain (free via Let's Encrypt)
4. **Monitor uptime** with UptimeRobot or Pingdom
5. **Use Cloudflare** for additional CDN and DDoS protection
6. **Compress images** before uploading (already using SVG)
7. **Test mobile** on real devices, not just browser tools

---

## 📞 Support Resources

- **GitHub Pages**: docs.github.com/pages
- **Vercel**: vercel.com/docs
- **Netlify**: docs.netlify.com
- **AWS**: docs.aws.amazon.com/s3

---

**Ready to deploy!** Choose your platform and go live! 🚀

**Recommendation**: Start with GitHub Pages (free, easy) or Vercel (professional, free).
