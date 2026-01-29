# CLAUDE.md - AI Assistant Guide for RM2PT Website

## Project Overview

**RM2PT** (Requirements Modeling and Automatic Prototyping) is a CASE tool website built with Jekyll. The site documents and provides resources for the RM2PT tool, which generates prototypes from UML requirements models complemented by OCL formal contracts.

- **Website URL**: http://rm2pt.com
- **Site Description**: "Automatic Prototyping for Requirements Validation"
- **Contact**: yilongyang@buaa.edu.cn / rm2pt@yilong.io
- **Maintained by**: Software Engineering Institute at Beihang University (BUAA)
- **GitHub**: https://github.com/yylonly

## Technology Stack

- **Static Site Generator**: Jekyll (GitHub Pages compatible via `github-pages` gem)
- **Ruby Version**: 2.7.2 (see `.ruby-version`)
- **CSS Framework**: UIKit 3.x (loaded from `/assets/css/uikit.min.css`)
- **JavaScript**: UIKit JS + UIKit Icons (`/assets/js/uikit.min.js`, `/assets/js/uikit-icons.min.js`)
- **Markdown**: Kramdown with GitHub Flavored Markdown (GFM)
- **Syntax Highlighting**: Rouge
- **Package Manager**: Bundler with gems from `gems.ruby-china.com`
- **Analytics**: Google Analytics (UA-42915048-5)

## Directory Structure

```
rm2pt-website/
├── _config.yml          # Jekyll site configuration (restart server after changes)
├── _data/
│   └── navigation.yml   # Main navigation menu structure (3-level hierarchy)
├── _includes/           # Reusable HTML components
│   ├── head.html        # HTML head with UIKit CSS/JS + Google Analytics
│   ├── header.html      # Navigation bar (desktop) + off-canvas menu (mobile)
│   ├── footer.html      # Site footer
│   ├── img.html         # Image include helper
│   ├── video.html       # Video embed helper
│   ├── disqus_comments.html  # Disqus commenting (if enabled)
│   └── google-analytics.html # GA tracking code
├── _layouts/            # Page templates (all extend default.html)
│   ├── default.html     # Base layout with uk-container wrapper
│   ├── home.html        # Homepage layout
│   ├── page.html        # Standard page with breadcrumb navigation
│   ├── post.html        # Blog post layout
│   ├── category.html    # Category listing
│   └── sitemap.html     # Sitemap layout
├── _posts/              # Blog-style content (7 categories)
│   ├── CaseStudy/       # RM2PT case studies (ATM, CoCoME, LibMS, Loan)
│   ├── Cloud/           # Cloud-related documentation
│   ├── DevOps/          # CI/CD, Git, IDE documentation
│   ├── Documentation/   # Developer documentation
│   ├── Others/          # Miscellaneous content
│   ├── Programming/     # Programming guides
│   └── System/          # System administration
├── _sass/               # SCSS stylesheets
│   └── mcloud/          # Custom theme styles
├── assets/              # Static assets
│   ├── css/uikit.min.css
│   └── js/uikit.min.js, uikit-icons.min.js
├── data/                # Research documents and resources
│   ├── *.pdf            # Research papers (ICSE, RE, FMAC, etc.)
│   ├── *.jar            # Java libraries
│   └── imgs/, wiiu/     # Additional resources
├── imgs/                # Image assets (organized by feature)
│   ├── InputGen/        # InputGen tool images
│   ├── RM2Doc/          # RM2Doc feature images
│   ├── RM2DM/           # RM2DM feature images
│   ├── RM2EIS/          # RM2EIS feature images
│   ├── RM2MS/           # RM2MS feature images
│   ├── RapidMS/         # RapidMS feature images
│   ├── ValidGen/        # ValidGen feature images
│   ├── RM2PTDevInstall/ # Developer installation images
│   └── [case study images at root level]
├── page/                # Static pages (main content)
│   ├── about.md         # About page with team information
│   ├── download.md      # Downloads page (current v1.2.3)
│   ├── sitemap.md       # Sitemap page
│   ├── casestudy/       # Case study detail pages
│   ├── tutorial/        # Tutorials
│   │   ├── user/        # 9 user tutorials
│   │   └── dev/         # Developer tutorials
│   ├── overview/        # Overview pages (fund, seminar, publication)
│   ├── inputgen/        # InputGen + InitialGPT documentation
│   ├── rm2doc/          # RM2Doc documentation
│   ├── rm2dm/           # RM2DM documentation
│   ├── rm2eis/          # RM2EIS documentation
│   ├── rm2ms/           # RM2MS documentation
│   ├── rapidms/         # RapidMS documentation
│   ├── validgen/        # ValidGen documentation
│   ├── istar/           # iStar modeler
│   ├── ocl2nl/          # OCL to Natural Language
│   └── UseCaseEditor/   # Use Case Editor
├── propocess/           # (Note: appears to be typo for "process")
├── index.md             # Homepage content (layout: home)
├── Gemfile              # Ruby dependencies
├── mcloud.gemspec       # Gem specification
└── favicon.ico          # Site favicon
```

## Key Configuration (`_config.yml`)

**Important**: Changes to `_config.yml` require server restart.

```yaml
title: Requirements Modeling and Automatic Prototyping
shorttitle: RM2PT
description: Automatic Prototyping for Requirements Validation
date: 2013-2023
email: yilongyang@buaa.edu.cn
url: "http://rm2pt.com"
baseurl: ""
github_username: yylonly
permalink: /:categories/:title/

markdown: kramdown
highlighter: rouge
kramdown:
  input: GFM
  hard_wrap: false
  syntax_highlighter: rouge

plugins:
  - jekyll-feed
```

## Navigation Structure (`_data/navigation.yml`)

Three-level hierarchy with special URL patterns:

```yaml
# Level 1: Section
- section_name: "Section Name"
  section_url: "url-segment"
  ispage: true  # Direct link (no dropdown)

# Level 2: Subsection
  subsectons:  # Note: typo in actual file, "subsectons" not "subsections"
    - sub_name: "Subsection Name"
      subsection_url: "sub-url"

# Level 3: Sub-subsection
      subsubsection:
        - name: "Item Name"
          subsubsection_url: "../../../advs/feature"  # Relative URL pattern
          ispage: true
```

**Navigation Sections:**
1. Overview (Fund, Seminar, Publication)
2. Get Started (User/Developer Tutorials)
3. Case Studies (direct link)
4. Advanced Features (Requirements Modeling, Validation, Code Generation tools)
5. Research (MDA Foundation, Applications, ASE, ISE)
6. Documentation (User/Developer docs)
7. Downloads (direct link)
8. About (direct link)

## Content Conventions

### Page Front Matter
```yaml
---
layout: page
title: Page Title
permalink: /url-path/
level: [Optional, Breadcrumb, Levels]  # Used in breadcrumb navigation
---
```

### Post Front Matter
Posts follow Jekyll naming: `_posts/Category/YYYY-MM-DD-title.md`
```yaml
---
layout: post
title: Post Title
description: Brief description for listings
date: 2021-05-24 14:43:17.000000000 +08:00
type: post
img: /imgs/thumbnail.jpg  # Thumbnail image
categories: [CaseStudy]   # Must match folder name
---
```

### Image Patterns

**Absolute paths** (recommended for root-level pages):
```markdown
![Alt text](/imgs/feature/image.png)
<img src="/imgs/feature/image.png" alt="Alt text" style="zoom: 50%;" />
```

**Relative paths** (for pages in subdirectories like `/page/feature/`):
```markdown
<img src="../../imgs/Feature/image.png" alt="Alt text" width="80%" height="80%" />
```

**Common inline styles:**
- `style="zoom: 50%;"` - Scale images
- `width="80%" height="80%"` - Percentage sizing
- `class="center"` - Center alignment

### OCL Contract Code Blocks
Case studies use fenced code blocks for OCL contracts:
````markdown
```
Contract SystemName::operationName(param: Type) : ReturnType {
    definition:
        variable:Type = Expression
    precondition:
        condition
    postcondition:
        result = value
}
```
````

## Development Workflow

### Local Development
```bash
# Install dependencies
gem install bundler jekyll

# Install project gems (uses gems.ruby-china.com mirror)
bundle install

# Run local server
bundle exec jekyll serve

# Server runs at http://localhost:4000
# Note: _config.yml changes require restart
```

### Adding New Content

#### New Page
1. Create: `/page/feature/feature.md`
2. Front matter: `layout: page`, `title`, `permalink: /feature/`
3. Images: `/imgs/Feature/`
4. Update `_data/navigation.yml` if needed

#### New Case Study
1. Create: `_posts/CaseStudy/YYYY-MM-DD-name.md`
2. Required sections:
   - Use Case Diagram
   - System Sequence Diagrams
   - Conceptual Class Diagram
   - Main Contracts (OCL code blocks)
3. Add images to `/imgs/` with naming: `casename-diagram-type.png`
4. Link to: https://github.com/RM2PT/CaseStudies

#### New Advanced Feature Tool
1. Create directory: `/page/toolname/`
2. Create pages: `toolname.md`, `toolname-tutorial.md`
3. Images: `/imgs/ToolName/`
4. Navigation: Add to "Advanced Features" section in `_data/navigation.yml`
5. Use relative URL pattern: `../../../advs/toolname`

### Update Downloads
Edit `/page/download.md`:
- Current version: 1.2.3
- Update GitHub release links
- Platform links: MacOS, Windows, Linux
- DevPack offline package link

## UIKit Framework Reference

### Common Classes
```html
<!-- Layout -->
<div class="uk-container">           <!-- Content container -->
<nav class="uk-navbar">              <!-- Navigation bar -->
<article class="uk-article">         <!-- Article wrapper -->

<!-- Navigation -->
<ul class="uk-breadcrumb">           <!-- Breadcrumb navigation -->
<ul class="uk-nav uk-nav-default">   <!-- Default nav list -->
<div class="uk-navbar-dropdown">     <!-- Dropdown menu -->
<div id="offcanvas-nav" uk-offcanvas><!-- Mobile off-canvas menu -->

<!-- Responsive -->
<div class="uk-visible@m">           <!-- Visible on medium+ screens -->
<div class="uk-hidden@m">            <!-- Hidden on medium+ screens -->

<!-- Typography -->
<p class="uk-text-lead">             <!-- Lead paragraph -->
<span class="uk-text-bold">          <!-- Bold text -->
<span class="uk-text-lighter">       <!-- Lighter text -->

<!-- Components -->
<span uk-icon="check">               <!-- Icon -->
<a class="uk-logo">                  <!-- Logo link -->
```

### Layout Hierarchy
```
default.html (base: uk-container wrapper)
├── home.html (index.md)
├── page.html (uk-article + uk-breadcrumb)
├── post.html (blog posts)
├── category.html (post listings)
└── sitemap.html
```

## Common Tasks for AI Assistants

### Update Team Information
Edit `/page/about.md` - organized by research groups:
- BUAA Software Group (main team)
- NEPU Group, BUAA GUI Group, BJUT Group, MPI Group, GXNU Group, ECNU Group

### Fix Navigation Links
Common issue: Items without `subsubsection_url` show as disabled (grayed out).
To enable: Add `subsubsection_url` and `ispage: true`

### Add Tutorial
1. Create in `/page/tutorial/user/` or `/page/tutorial/dev/`
2. Follow naming: `descriptive-name.md`
3. Add to navigation under "Get Started" section

## Build and Deployment

- **Platform**: GitHub Pages
- **Gem**: `github-pages` for compatibility
- **Deployment**: Automatic on push to main branch
- **No build step**: Jekyll builds automatically

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Jekyll serve fails | Check Ruby version (2.7.2), run `bundle install`, ensure `webrick` gem |
| Missing styles | Verify `/assets/css/uikit.min.css` exists and loads |
| Broken navigation | Check `_data/navigation.yml` YAML syntax (watch for typo "subsectons") |
| Image not showing | Check path - use absolute `/imgs/` or relative `../../imgs/` |
| Config changes not applied | Restart `jekyll serve` |
| Gem source issues | Change `gems.ruby-china.com` to `rubygems.org` for international use |

## File Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Pages | lowercase-hyphenated | `create-new-project.md` |
| Posts | YYYY-MM-DD-title | `2021-05-24-atm.md` |
| Images | feature-description | `atm-ucd.png`, `rm2doc-overview.png` |
| Directories | lowercase or CamelCase | `inputgen/`, `RM2Doc/` |

## Related Resources

- **RM2PT Releases**: https://github.com/RM2PT/Release
- **Case Studies**: https://github.com/RM2PT/CaseStudies
- **InputGen UpdateSite**: https://github.com/RM2PT/InputGen-UpdateSite
- **Contact**: rm2pt@yilong.io
