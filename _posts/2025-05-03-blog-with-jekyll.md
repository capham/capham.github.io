---
title: "Create free blog with Jekyll and Github"
categories:
  - Edge Case
tags:
  - jekyll
  - github page
---


# 📝 Create Free Blog with Jekyll and GitHub Pages

If you're looking to create a **fast**, **free**, and **customizable** blog without relying on third-party platforms, using **Jekyll** and **GitHub Pages** is a great option. This setup allows you to host a static site directly from a GitHub repository — no servers, no databases, and no monthly fees.

## 🚧 Basic Steps to Create Your Blog

1. **Install Required Tools**
   - Install [Ruby](https://www.ruby-lang.org/)
   - Install [Bundler](https://bundler.io/) and [Jekyll](https://jekyllrb.com/)
   - Create a free [GitHub](https://github.com) account

2. **Set Up a Jekyll Project**
   ```bash
   jekyll new my-blog
   cd my-blog
   bundle install
   ```

3. **Choose a Jekyll Theme**

   One of the most popular and polished themes is **Minimal Mistakes**.

4. **Add Your Theme**

   Add the Minimal Mistakes theme via Gem:

   ```ruby
   # in Gemfile
   gem "minimal-mistakes-jekyll"
   ```

   And in `_config.yml`:

   ```yaml
   theme: minimal-mistakes-jekyll
   ```

5. **Customize Content**
   - Use Markdown files (`.md`) to create posts and pages
   - Update `_config.yml` to set your site title, description, and navigation
   - Use folders like `_posts`, `_layouts`, and `_includes` to organize content

6. **Deploy with GitHub Pages**
   - Push your site to a GitHub repo
   - Enable GitHub Pages in repository settings (usually set branch to `main` or `gh-pages`)
   - Your blog will be live at: `https://yourusername.github.io/your-repo-name`

---

## 🌟 About Minimal Mistakes

**Minimal Mistakes** is a powerful, clean, and highly customizable Jekyll theme. It supports:

- Multiple layouts and page types
- Built-in support for SEO, social sharing, and comments
- Responsive design with mobile-friendly UX
- Easy configuration with YAML files

It’s perfect for personal blogs, portfolios, or documentation websites. Check it out here: [Minimal Mistakes Demo](https://mmistakes.github.io/minimal-mistakes/)

---

## ✅ Final Thoughts

Creating a blog with **Jekyll** and **GitHub Pages** is a great way to learn web development basics while owning your content. With a theme like **Minimal Mistakes**, you can focus more on writing and less on design and infrastructure.

