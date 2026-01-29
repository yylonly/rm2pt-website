# CLAUDE.md - AI Assistant Guide for RM2PT Website

## Project Overview

**RM2PT** (Requirements Modeling and Automatic Prototyping) is a CASE tool website built with Jekyll. The site documents and provides resources for the RM2PT tool, which generates prototypes from UML requirements models complemented by OCL formal contracts.

- **Website URL**: http://rm2pt.com
- **Contact**: yilongyang@buaa.edu.cn / rm2pt@yilong.io
- **Maintained by**: Software Engineering Institute at Beihang University (BUAA)

## Technology Stack

- **Static Site Generator**: Jekyll (GitHub Pages compatible)
- **Ruby Version**: 2.7.2 (see `.ruby-version`)
- **CSS Framework**: UIKit (not Bootstrap, despite Gemfile references)
- **Markdown**: Kramdown with GitHub Flavored Markdown (GFM)
- **Syntax Highlighting**: Rouge
- **Package Manager**: Bundler with gems from `gems.ruby-china.com`

## Directory Structure

```
rm2pt-website/
├── _config.yml          # Jekyll site configuration
├── _data/
│   └── navigation.yml   # Main navigation menu structure
├── _includes/           # Reusable HTML components
│   ├── head.html        # HTML head with UIKit CSS/JS
│   ├── header.html      # Navigation bar and off-canvas menu
│   ├── footer.html      # Site footer
│   ├── img.html         # Image include helper
│   └── video.html       # Video embed helper
├── _layouts/            # Page templates
│   ├── default.html     # Base layout
│   ├── home.html        # Homepage layout
│   ├── page.html        # Standard page layout
│   ├── post.html        # Blog post layout
│   ├── category.html    # Category listing
│   └── sitemap.html     # Sitemap layout
├── _posts/              # Blog-style content (categorized)
│   ├── CaseStudy/       # RM2PT case studies (ATM, CoCoME, etc.)
│   ├── Cloud/           # Cloud-related documentation
│   ├── DevOps/          # CI/CD, Git, IDE documentation
│   ├── Documentation/   # Developer documentation
│   ├── Others/          # Miscellaneous content
│   ├── Programming/     # Programming guides
│   └── System/          # System administration
├── _sass/               # SCSS stylesheets
│   └── mcloud/          # Custom theme styles
├── assets/              # Static assets (CSS, JS)
│   └── css/uikit.min.css
├── data/                # PDF documents, JAR files
├── imgs/                # Image assets (organized by feature)
│   ├── RM2Doc/          # RM2Doc feature images
│   ├── RM2DM/           # RM2DM feature images
│   ├── RM2MS/           # RM2MS feature images
│   └── ...
├── page/                # Static pages (main content)
│   ├── about.md         # About page
│   ├── download.md      # Downloads page
│   ├── casestudy/       # Case study pages
│   ├── tutorial/        # User and developer tutorials
│   │   ├── user/        # User tutorials
│   │   └── dev/         # Developer tutorials
│   ├── rm2doc/          # RM2Doc feature documentation
│   ├── rm2dm/           # RM2DM feature documentation
│   ├── rm2eis/          # RM2EIS feature documentation
│   ├── rm2ms/           # RM2MS feature documentation
│   ├── rapidms/         # RapidMS feature documentation
│   ├── validgen/        # ValidGen feature documentation
│   ├── inputgen/        # InputGen feature documentation
│   └── overview/        # Overview pages
├── index.md             # Homepage content
├── Gemfile              # Ruby dependencies
└── mcloud.gemspec       # Gem specification (theme)
```

## Key Configuration Files

### `_config.yml`
- `title`: "Requirements Modeling and Automatic Prototyping"
- `shorttitle`: "RM2PT"
- `baseurl`: "" (root deployment)
- `url`: "http://rm2pt.com"
- `permalink`: `/:categories/:title/`

### `_data/navigation.yml`
Defines the hierarchical navigation menu structure with sections:
- Overview (Fund, Seminar, Publication)
- Get Started (User/Developer Tutorials)
- Case Studies
- Advanced Features (Requirements Modeling, Validation, Code Generation)
- Research
- Documentation
- Downloads
- About

## Content Conventions

### Page Front Matter
Standard page front matter:
```yaml
---
layout: page
title: Page Title
permalink: /url-path/
---
```

### Post Front Matter
Posts in `_posts/` follow Jekyll naming convention `YYYY-MM-DD-title.md`:
```yaml
---
layout: post
title: Post Title
description: Brief description
date: 2021-05-24 14:43:17.000000000 +08:00
type: post
img: /imgs/image.png
categories: [CaseStudy]
---
```

### Image References
- Store images in `/imgs/` or feature-specific subdirectories
- Reference with absolute paths: `/imgs/feature/image.png`
- For pages in subdirectories, use relative paths: `../../imgs/feature/image.png`

### Navigation Links
- `ispage: true` indicates a direct page link
- `subsection_url` defines the URL segment
- Use `../../../advs/` pattern for linking to advanced features from nested locations

## Development Workflow

### Local Development
```bash
# Install dependencies
gem install bundler jekyll

# Install project gems
bundle install

# Run local server
bundle exec jekyll serve
```
The site will be available at `http://localhost:4000`

### Adding Content

#### New Page
1. Create markdown file in appropriate `/page/` subdirectory
2. Add front matter with `layout: page`, `title`, and `permalink`
3. If navigation is needed, update `_data/navigation.yml`

#### New Post/Article
1. Create file in `_posts/Category/YYYY-MM-DD-title.md`
2. Add required front matter including `categories`
3. Posts are automatically indexed by category

#### New Feature Documentation
1. Create directory under `/page/` (e.g., `/page/newfeature/`)
2. Create main documentation file (e.g., `newfeature.md`)
3. Store related images in `/imgs/NewFeature/`
4. Add navigation entry in `_data/navigation.yml` under Advanced Features

### Adding Images
1. Place images in `/imgs/` or appropriate subdirectory
2. Use consistent naming (kebab-case or descriptive names)
3. Optimize images before committing (large images slow the site)

## Important Patterns

### UIKit CSS Classes
The site uses UIKit framework (not Bootstrap). Common classes:
- `uk-container` - Content container
- `uk-card` - Card component
- `uk-navbar` - Navigation bar
- `uk-article` - Article wrapper
- `uk-breadcrumb` - Breadcrumb navigation
- `uk-visible@m` / `uk-hidden@m` - Responsive visibility

### Layout Inheritance
```
default.html
├── home.html (homepage)
├── page.html (standard pages)
├── post.html (blog posts)
├── category.html (category listings)
└── sitemap.html (sitemap)
```

### Liquid Template Variables
- `{{ site.title }}` - Site title
- `{{ site.description }}` - Site description
- `{{ page.title }}` - Current page title
- `{{ content }}` - Page content
- `{{ site.data.navigation }}` - Navigation data

## Common Tasks for AI Assistants

### Update Downloads
Edit `/page/download.md` to update:
- Version numbers
- Download links (GitHub releases)
- Platform-specific instructions

### Add New Tool/Feature Page
1. Create directory: `/page/toolname/`
2. Create main page: `/page/toolname/toolname.md`
3. Add images to: `/imgs/ToolName/`
4. Update `_data/navigation.yml` in appropriate section
5. Use `permalink: /toolname/` or appropriate URL

### Update Navigation
Edit `_data/navigation.yml`:
- `section_name` / `section_url` for main sections
- `sub_name` / `subsection_url` for subsections
- `name` / `subsubsection_url` for sub-subsections
- Set `ispage: true` for direct links

### Add Case Study
1. Create post in `_posts/CaseStudy/YYYY-MM-DD-name.md`
2. Include: Use Case Diagram, System Sequence Diagrams, Conceptual Class Diagram, Main Contracts
3. Add images to `/imgs/`
4. Link to GitHub case study repository

### Update Team Information
Edit `/page/about.md` to add/update team members in appropriate research groups

## Build and Deployment

The site is configured for GitHub Pages deployment:
- Uses `github-pages` gem for compatibility
- No custom build step required
- Push to main branch triggers automatic deployment

## Troubleshooting

### Common Issues
1. **Jekyll serve fails**: Check Ruby version (2.7.2) and run `bundle install`
2. **Missing styles**: Ensure UIKit CSS is loaded from `/assets/css/uikit.min.css`
3. **Broken navigation**: Verify `_data/navigation.yml` YAML syntax
4. **Image not displaying**: Check path (absolute from root or correct relative path)

### Gem Source Note
The Gemfile uses Chinese mirror `gems.ruby-china.com`. For international use, may need to change to `rubygems.org`.

## File Naming Conventions

- Markdown files: `lowercase-with-hyphens.md`
- Image files: `descriptive-name.png` or `feature-component.png`
- Directories: `lowercase` or `CamelCase` (existing mixed convention)
- Posts: `YYYY-MM-DD-title.md`

## Related Repositories

- **RM2PT Releases**: https://github.com/RM2PT/Release
- **Case Studies**: https://github.com/RM2PT/CaseStudies
