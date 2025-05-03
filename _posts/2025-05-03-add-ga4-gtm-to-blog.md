---
title: "Adding Google Analytics 4 and Google Tag Manager to Your Jekyll Blog"
toc: true
toc_label: "Table of Content"
toc_icon: "heart"  # corresponding Font Awesome icon name (without fa prefix)
categories:
  - Blogging
tags:
  - ga4
  - gtm
---

This guide will walk you through the process of setting up Google Analytics 4 (GA4) and Google Tag Manager (GTM) on your Jekyll blog to track visitor behavior, custom events, and optimize your content strategy.

## Setting Up Google Analytics 4

### Step 1: Create a Google Analytics Account

1. Go to [Google Analytics](https://analytics.google.com/) and sign in with your Google account
2. Click "Start measuring"
3. Enter an account name (this could be your name or company name)
4. Configure your data sharing settings and click "Next"

### Step 2: Set Up a Property

1. Enter a property name (typically your blog name)
2. Select your reporting time zone and currency
3. Click "Show advanced options" if you want to create a Universal Analytics property alongside GA4
4. Click "Next"

### Step 3: Enter Business Information

1. Select your industry category
2. Select your business size and how you intend to use Google Analytics
3. Click "Create"

### Step 4: Set Up Data Collection

1. Select "Web" as your platform
2. Enter your website URL, stream name (usually your site name), and choose your enhanced measurement settings
3. Click "Create stream"
4. Take note of your Measurement ID (it looks like G-XXXXXXX)
