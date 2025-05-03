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

## Table of Contents

1. [Setting Up Google Analytics 4](#setting-up-google-analytics-4)
2. [Setting Up Google Tag Manager](#setting-up-google-tag-manager)
3. [Integrating Google Analytics and Tag Manager with Jekyll](#integrating-with-jekyll)
4. [Tracking Custom Events](#tracking-custom-events)
5. [Testing Your Implementation](#testing-your-implementation)
6. [Troubleshooting](#troubleshooting)

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

## Setting Up Google Tag Manager

### Step 1: Create a Google Tag Manager Account

1. Go to [Google Tag Manager](https://tagmanager.google.com/) and sign in with your Google account
2. Click "Create Account"
3. Enter an account name and select your country
4. Enter a container name (your blog name) and select "Web" as the target platform
5. Click "Create" and accept the Terms of Service

### Step 2: Get Your GTM Snippet

After creating your account and container, Google Tag Manager will provide you with two code snippets:
1. A script to be placed in the `<head>` of your HTML
2. A noscript fallback to be placed immediately after the opening `<body>` tag

Copy these codes for later use.

## Integrating with Jekyll

### Method 1: Direct Implementation in Theme Files

#### Step 1: Add Google Analytics to Your Jekyll Site

1. Open your Jekyll project and navigate to the `_includes` folder
2. Create or edit a file called `google-analytics.html` with the following content:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXX');
</script>
```

Replace `G-XXXXXXX` with your actual Google Analytics Measurement ID.

#### Step 2: Add Google Tag Manager to Your Jekyll Site

1. In your `_includes` folder, create a file called `google-tag-manager-head.html` with the following content:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
<!-- End Google Tag Manager -->
```

2. Create another file called `google-tag-manager-body.html` with:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

Replace `GTM-XXXXXXX` with your actual Google Tag Manager Container ID.

#### Step 3: Include the Code in Your Layout Files

1. Open your `_layouts/default.html` file (or your base layout file)
2. Add the Google Analytics and Google Tag Manager head code before the closing `</head>` tag:

```html
{% if jekyll.environment == 'production' %}
  {% include google-analytics.html %}
  {% include google-tag-manager-head.html %}
{% endif %}
</head>
```

3. Add the Google Tag Manager body code right after the opening `<body>` tag:

```html
<body>
{% if jekyll.environment == 'production' %}
  {% include google-tag-manager-body.html %}
{% endif %}
```

Note: The conditional `if jekyll.environment == 'production'` ensures tracking only happens in production, not during local development.

### Method 2: Using _config.yml Settings

#### Step 1: Update Your _config.yml File

Add your tracking IDs to your `_config.yml` file:

```yaml
# Analytics
google_analytics: G-XXXXXXX
google_tag_manager: GTM-XXXXXXX
```

#### Step 2: Create Include Files That Use These Settings

In your Google Analytics include file:

```html
{% if site.google_analytics %}
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id={{ site.google_analytics }}"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', '{{ site.google_analytics }}');
</script>
{% endif %}
```

For Google Tag Manager, create similar includes that use `{{ site.google_tag_manager }}`.

### Method 3: Using a Jekyll Analytics Plugin

You can also use the [jekyll-analytics](https://github.com/hendrikschneider/jekyll-analytics) plugin:

1. Add the plugin to your `Gemfile`:
```ruby
group :jekyll_plugins do
  gem 'jekyll-analytics'
end
```

2. Run `bundle install`

3. Configure in `_config.yml`:
```yaml
jekyll_analytics:
  GoogleAnalytics:
    id: G-XXXXXXX
  GoogleTagManager:
    id: GTM-XXXXXXX
```

## Tracking Custom Events

### Basic Event Tracking with GA4

To track custom events with Google Analytics 4, use the following JavaScript:

```javascript
gtag('event', 'button_click', {
  'event_category': 'engagement',
  'event_label': 'newsletter_signup'
});
```

### Setting Up Custom Events in GTM

1. Log in to your Google Tag Manager account
2. Click on "Tags" > "New"
3. Choose "Google Analytics: GA4 Event" as your tag type
4. Enter your GA4 Measurement ID and configure your event parameters
5. Set up a trigger (e.g., click, form submission, etc.)
6. Save and publish your container

### Common Events to Track on a Blog

Here are some useful events to track on your Jekyll blog:

1. **Post Engagement**

```javascript
// Track when user scrolls 75% of an article
document.addEventListener('DOMContentLoaded', function() {
  let articleRead = false;
  window.addEventListener('scroll', function() {
    if (!articleRead) {
      const article = document.querySelector('article');
      if (article) {
        const articleHeight = article.offsetHeight;
        const scrollPosition = window.scrollY + window.innerHeight;
        const scrollThreshold = article.offsetTop + (articleHeight * 0.75);
        
        if (scrollPosition > scrollThreshold) {
          articleRead = true;
          gtag('event', 'scroll_depth', {
            'event_category': 'engagement',
            'event_label': document.title,
            'percent': '75'
          });
        }
      }
    }
  });
});
```

2. **Time on Page**

```javascript
// Track time spent on page
document.addEventListener('DOMContentLoaded', function() {
  let timeSpent = 0;
  const timeInterval = setInterval(function() {
    timeSpent += 30;
    if (timeSpent === 30) {
      gtag('event', 'time_on_page', {
        'event_category': 'engagement',
        'event_label': document.title,
        'value': 30
      });
    } else if (timeSpent === 180) {
      gtag('event', 'time_on_page', {
        'event_category': 'engagement',
        'event_label': document.title,
        'value': 180
      });
      clearInterval(timeInterval);
    }
  }, 30000); // Check every 30 seconds
});
```

3. **Link Clicks**

```javascript
// Track outbound link clicks
document.addEventListener('DOMContentLoaded', function() {
  const links = document.querySelectorAll('a[href^="http"]');
  links.forEach(function(link) {
    if (!link.hostname.includes(window.location.hostname)) {
      link.addEventListener('click', function(e) {
        gtag('event', 'outbound_link_click', {
          'event_category': 'outbound',
          'event_label': link.href
        });
      });
    }
  });
});
```

### Including Custom Event Scripts in Jekyll

Create a new file in your `_includes` folder called `custom-events.html` with your event tracking code:

```html
<script>
  document.addEventListener('DOMContentLoaded', function() {
    // Your event tracking code here
  });
</script>
```

Then include this file in your layout:

```html
{% if jekyll.environment == 'production' %}
  {% include custom-events.html %}
{% endif %}
```

## Testing Your Implementation

### Testing GA4 Implementation

1. Install the [Google Analytics Debugger](https://chrome.google.com/webstore/detail/google-analytics-debugger/jnkmfdileelhofjcijamephohjechhna) Chrome extension
2. Open your blog and check the console for GA4 events
3. In GA4, go to "Realtime" view to see if your visit is being tracked

### Testing GTM Implementation

1. Install the [Google Tag Assistant](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk) Chrome extension
2. Visit your blog and activate Tag Assistant
3. Verify that your GTM container is correctly installed
4. Use "Preview mode" in Google Tag Manager to test your tags and triggers

## Troubleshooting

### Common Issues and Solutions

1. **No Data in Google Analytics**
   - Ensure your tracking code is correctly implemented
   - Check that your site is being served in production mode
   - Clear browser cache and cookies
   - Disable ad blockers that might block analytics scripts

2. **GTM Not Firing Tags**
   - Check for JavaScript errors in the console
   - Verify trigger conditions are being met
   - Test in GTM Preview mode

3. **Custom Events Not Appearing**
   - Check browser console for JavaScript errors
   - Verify the event code is executing using console.log
   - Ensure events are properly configured in GTM

### Advanced Debugging

For more complex issues, use the Google Analytics Debugger extension and check for:
- Proper initialization of gtag
- Event parameters being correctly passed
- Any JavaScript errors preventing execution

## Conclusion

With Google Analytics 4 and Google Tag Manager properly set up on your Jekyll blog, you'll be able to gather valuable insights about your visitors and how they interact with your content. Use this data to refine your content strategy and improve user engagement.

Remember to respect user privacy and include appropriate privacy notices and cookie consent mechanisms as required by regulations such as GDPR and CCPA.

Happy tracking!