---
title: "Pointing Your Domain to GitHub Pages"
toc: true
toc_label: "Unique Title"
toc_icon: "heart"  # corresponding Font Awesome icon name (without fa prefix)
categories:
  - Blogging
tags:
  - jekyll
  - github page
---

This guide will walk you through the process of pointing a custom domain from your domain registrar to GitHub Pages. We'll cover each step in detail, from DNS configuration to SSL setup.

## Basic Steps

1. Setting up your GitHub Pages repository
2. Configuring DNS records (A records and CNAME)
3. Adding your domain to GitHub Pages settings
4. Creating a CNAME file in your repository
5. Setting up SSL/HTTPS

## 1. Preparing Your GitHub Pages Repository

Before configuring your domain, you need to ensure GitHub Pages is activated for your repository.

1. Log in to GitHub and open your website repository
2. Go to **Settings** of the repository
3. Scroll down to the **GitHub Pages** section
4. Under **Source**, select the branch you want to use (typically `main` or `master`)
5. Click **Save**

GitHub Pages will automatically provide you with a URL in the format `username.github.io` or `username.github.io/repository-name`.

## 2. Configuring DNS at Your Domain Registrar

There are two ways to point your domain to GitHub Pages:

### Option 1: Using A Records (for apex domain)

If you want to use an apex domain (like `example.com` instead of `www.example.com`), you need to create A records:

1. Log in to your account at your domain registrar
2. Find the DNS management or Name Server section
3. Add the following A records:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
```

Where:
- `@` represents the apex domain
- The IP addresses are GitHub Pages servers

### Option 2: Using a CNAME Record (for subdomain)

If you want to use a subdomain, such as `www.example.com`:

1. Add a CNAME record:

```
CNAME    www    username.github.io
```

Replace `username` with your GitHub username.

### Configure Both (Recommended)

To ensure both your apex domain and www subdomain work:

1. Add A records for the apex domain as instructed above
2. Add a CNAME record for the www subdomain

## 3. Adding Your Domain in GitHub Pages Settings

1. Return to your GitHub repository
2. Go to **Settings** → **Pages**
3. In the **Custom domain** field, enter your domain (e.g., `example.com`)
4. Click **Save**

## 4. Creating a CNAME File in Your Repository

1. In your repository, create a new file named exactly `CNAME` (all capital letters)
2. In this file, write only your domain on a single line:

```
example.com
```

3. Commit this file to your repository (typically to the `main` or `master` branch)

## 5. Setting Up SSL/HTTPS

GitHub Pages provides free SSL through Let's Encrypt:

1. In **Settings** → **Pages**, wait until DNS is properly configured
2. Check the **Enforce HTTPS** box

Note: It may take up to 24 hours for GitHub Pages to provision an SSL certificate for your domain.

## Verifying Your Configuration

After setup is complete, you can check if your domain is properly pointed:

1. Open a browser and navigate to your domain
2. Ensure your GitHub Pages website displays correctly
3. Check if HTTPS is working (look for the lock icon in the address bar)

## Troubleshooting Common Issues

### Website Not Displaying or Shows Error Message

1. **Check if DNS has propagated**: It can take up to 48 hours for DNS to fully propagate
2. **Verify GitHub Pages configuration**: Make sure the source branch is correctly selected
3. **Check CNAME file**: Ensure the CNAME file has the correct name and contains your domain

### Cannot Enable HTTPS

1. **Wait for DNS propagation**: GitHub needs to verify domain ownership before issuing SSL
2. **Double-check DNS configuration**: Make sure A records and CNAME are set up correctly
3. **Remove and re-add the domain**: Try removing the domain from GitHub Pages settings, save, then add it again

### Redirection Between www and non-www Not Working

1. **Configure both record types**: Make sure you've set up both A records and CNAME
2. **Check CNAME file**: The CNAME file should contain only one version of your domain (typically the apex domain)

## Keeping Email Working

If you're using email with this domain, make sure to preserve your MX records when configuring DNS.

## Conclusion

Pointing a custom domain to GitHub Pages is an excellent way to personalize your website. While the process may take some time to complete, the end result is a professional website with your own domain and HTTPS security.

Remember that DNS changes can take up to 48 hours to complete, so be patient if your website doesn't work immediately. If you're still experiencing issues after 48 hours, double-check your configuration and refer to GitHub Pages documentation for additional support.