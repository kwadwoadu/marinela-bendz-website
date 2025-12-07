# Marinela Bendz - Website Development Rules

This document governs all code development for the MarinelaBendz.com website.

---

## Tech Stack

| Component | Technology | Version |
|-----------|------------|---------|
| Framework | Astro | Latest |
| Styling | Tailwind CSS | v3.x |
| CMS | Decap CMS | Latest |
| Forms | Tally.so | Embed |
| Hosting | Cloudflare Pages | - |
| Analytics | GA4 | - |

---

## Project Structure

```
website/
├── astro.config.mjs
├── tailwind.config.mjs
├── package.json
├── public/
│   ├── admin/              # Decap CMS
│   │   ├── index.html
│   │   └── config.yml
│   ├── images/
│   └── favicon.ico
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── Hero.astro
│   │   ├── Services.astro
│   │   ├── About.astro
│   │   └── Contact.astro
│   ├── pages/
│   │   └── index.astro
│   ├── content/            # CMS-editable content
│   │   └── config.ts
│   └── styles/
│       └── global.css
└── CLAUDE.md               # This file
```

---

## Development Rules

### Code Quality
- TypeScript preferred for type safety
- Components should be self-contained
- No inline styles - use Tailwind classes
- Mobile-first responsive approach

### Performance Requirements
- Lighthouse Performance: >90
- Lighthouse SEO: 100
- First Contentful Paint: <1.5s
- Largest Contentful Paint: <2.5s
- No layout shift (CLS: 0)

### Accessibility
- WCAG 2.1 AA compliance
- Semantic HTML elements
- Alt text on all images
- Keyboard navigation support
- Sufficient color contrast

---

## Styling Guidelines

### Tailwind Configuration
```javascript
// tailwind.config.mjs
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: {
    extend: {
      colors: {
        // Define brand colors here
        primary: '#...',
        secondary: '#...',
      },
      fontFamily: {
        serif: ['Playfair Display', 'serif'],
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
}
```

### CSS Principles
- Use Tailwind utility classes
- Extract components for repeated patterns
- Follow brand guidelines in `/docs/brand-guidelines.md`
- Generous whitespace (Scandinavian minimalism)

---

## Component Guidelines

### Naming Convention
- PascalCase for components: `Hero.astro`
- Descriptive, single-responsibility names
- Props interface at top of file

### Component Structure
```astro
---
// Props interface
interface Props {
  title: string;
  subtitle?: string;
}

const { title, subtitle } = Astro.props;
---

<section class="...">
  <!-- Component markup -->
</section>
```

---

## SEO Implementation

### Required Meta Tags
```astro
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>{title} | Marinela Bendz</title>
  <meta name="description" content={description} />

  <!-- OpenGraph -->
  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={image} />
  <meta property="og:type" content="website" />

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image" />

  <!-- Canonical -->
  <link rel="canonical" href={canonicalURL} />
</head>
```

### Structured Data
- LocalBusiness schema
- Service schema
- BreadcrumbList (if multi-page)

---

## Decap CMS Configuration

### Content Collections
```yaml
# public/admin/config.yml
backend:
  name: github
  repo: [owner]/[repo]
  branch: main

collections:
  - name: "pages"
    label: "Pages"
    files:
      - label: "Home"
        name: "home"
        file: "src/content/home.json"
        fields:
          - { label: "Hero Title", name: "heroTitle", widget: "string" }
          - { label: "Hero Subtitle", name: "heroSubtitle", widget: "text" }
          # ... more fields
```

### Editable Content
- Headlines and subheadlines
- Service descriptions
- Pricing
- Contact information
- Images

---

## Tally.so Integration

### Embed Code
```astro
<iframe
  data-tally-src="https://tally.so/embed/FORM_ID?hideTitle=1"
  width="100%"
  height="500"
  frameborder="0"
  title="Contact Form"
></iframe>
<script src="https://tally.so/widgets/embed.js"></script>
```

### Form Fields
- Name (required)
- Email (required)
- Phone (optional)
- Service interest (dropdown)
- Budget range (dropdown)
- Message (textarea)

---

## Deployment

### Cloudflare Pages
- Connect to GitHub repository
- Build command: `npm run build`
- Build output: `dist`
- Auto-deploy on push to `main`

### Environment Variables
```
# If needed for CMS
PUBLIC_CMS_REPO=owner/repo
```

---

## Commands

```bash
# Development
npm run dev

# Build
npm run build

# Preview build
npm run preview
```

---

## File References

| Reference | Location |
|-----------|----------|
| Brand Guidelines | `/docs/brand-guidelines.md` |
| Site Structure | `/docs/site-structure.md` |
| Inspiration | `/inspiration/CLAUDE.md` |
| Roadmap | `/roadmap/roadmap.md` |

---

## Forbidden Practices

- No jQuery or heavy JS libraries
- No inline CSS
- No images without alt text
- No hardcoded content (use CMS)
- No console.log in production
- No blocking render resources

---

*Last updated: December 7, 2025*
