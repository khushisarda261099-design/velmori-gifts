# Velmori Gifts - Project Specification & Status

This document provides a comprehensive overview of the **Velmori Gifts** codebase. It is designed to help AI agents and developers understand the architecture, design patterns, and structure of the project efficiently without reading the entire codebase, saving token usage.

---

## 🚀 Project Overview
* **Project Name:** Velmori Gifts
* **Description:** A premium, elegant, and highly interactive single-page landing website for a boutique gift shop specializing in curated hampers, handmade bouquets, jewellery, and custom gifts.
* **Founder:** Ruchita Tawade
* **Contact Info:** +91 93566 64679 / WhatsApp link integrated.

---

## 🛠️ Technology Stack
1. **HTML5:** Semantic markup structure.
2. **CSS3 (Vanilla):** Custom styles, layout structures (Flexbox & Grid), and modern transitions/animations. No external frameworks (like Bootstrap or Tailwind) are used.
3. **Vanilla JavaScript:** 
   - Interactive canvas particle rendering (falling petals).
   - Scroll-based animations using the `IntersectionObserver` API.
4. **Typography (Google Fonts):**
   - *Cormorant Garamond*: Serif font for headings, logos, and italic emphasizes.
   - *Lato*: Sans-serif font for readability in body copy, labels, and stats.
   - *Dancing Script*: Cursive font for script-like decorative accents.

---

## 🎨 Design System & Customizations

### 1. Color Palette (CSS Variables)
Defined in the `:root` selector at the top of [index.html](file:///c:/Users/aditi/Desktop/velmori%20gifts/velmori-gifts/index.html#L10-L14):
* `--blush`: `#F5D5C8` (Accent backgrounds)
* `--cream`: `#FDF6F0` (Main page background)
* `--gold`: `#C9A84C` (Primary highlights & borders)
* `--gold2`: `#E8CC80` (Secondary marquee text color)
* `--rose`: `#B56070` (Secondary icons/labels)
* `--rose2`: `#D4889A` (Secondary hover accent)
* `--taupe`: `#8B7B6B` (Muted description/body text)
* `--dark`: `#3D2B2B` (Primary text & dark backgrounds)
* `--white`: `#FFFDF9` (Alternative block backgrounds)
* `--deep`: `#2A1A1A` (Footer/deep dark sections)

### 2. Fonts
* Google Fonts are loaded via `<link>` in the HTML `<head>`.
* Smooth scrolling is enabled globally (`html { scroll-behavior: smooth }`).

---

## 📂 Codebase Directory Structure
```
velmori-gifts/
├── index.html        # Core file: Contains all markup, styles, and script logic.
├── README.md         # Public README for repository overview and deployment info.
└── build.md          # This file (AI developer guidelines & project status).
```

---

## 🏗️ Detailed Architecture of `index.html`

### 1. Styles Block (`<style>` in `<head>`) — Lines 8 to 196
* Implements a responsive layout using media queries targeting screens up to `700px` wide.
* Custom keyframe animations:
  - `pulse`: Subtle glow pulsing for the hero badge.
  - `float`: Floating bounce effect on the central "VG" hero badge.
  - `sparkle-anim`: Flashing sparkle effect surrounding the hero badge.
  - `scrollLine`: Animated line guide at the bottom of the hero section.
  - `marquee`: Infinite horizontal text scrolling strip.

### 2. Markup Structure (`<body>`) — Lines 198 to 480
* **Canvas Element (`#petals-canvas`):** A fixed background canvas covering the viewport with low opacity (`0.5`) to create a soft falling petal background.
* **Navigation Bar (`.nav`):** Fixed-top container with frosted glass (`backdrop-filter`) effect, brand logo, and a WhatsApp CTA button.
* **Hero Section (`.hero`):** 
  - Radial gradient background with decorative absolute-positioned circles.
  - Interactive central brand badge with floating leaf divider and animated custom star sparkles.
  - Main CTA button linking to WhatsApp and a secondary click-to-call link.
* **Marquee Strip (`.marquee-strip`):** Seamless infinitely loop-scrolled text list of product categories.
* **About Section (`.about`):** Grid layout depicting brand philosophy accompanied by absolute-positioned circular badges ("✦ Handmade", "Made with Love ♡") and key metrics (100+ Happy Customers, 50+ Gift Designs, 5★ Rated).
* **Products Grid (`.products`):** Multi-column CSS grid rendering product cards.
  - **🚨 CRITICAL NOTE (Token Saving):** The product card `<img>` tags utilize inline Base64 data URIs (`src="data:image/jpeg;base64,..."`). These strings are **extremely long** (contributing to ~1MB of `index.html`'s size). **Do not inspect or output the content between lines 315 and 395 in full detail unless explicitly modified, to avoid consuming excessive context window tokens.**
* **Process Flow (`.process`):** Steps outlining order completion (We Connect -> We Curate -> We Wrap -> Delivered) linked together via an absolute-positioned border line.
* **Testimonials (`.testimonials`):** Review grid with custom quotation marks and styled ratings.
* **Contact Card (`.contact`):** Darker visual card highlighting Ruchita Tawade, showing a detailed description of services, call detail, and a large WhatsApp CTA button.
* **Footer (`footer`):** Minimal copyright note.

### 3. JavaScript Logic (`<script>` at footer) — Lines 482 to 546
* **Petal Fall Animation:**
  - Standard JavaScript OOP using a `Petal` class managing variables: position (`x`, `y`), size, speed, wind drift, rotation, wobble, and color variations.
  - Animation loop run via `requestAnimationFrame`.
  - Resize event listener resetting canvas bounds dynamically.
* **Scroll-driven Entry Animations:**
  - Configures an `IntersectionObserver` observing elements with classes `.product-card`, `.testi-card`, `.process-step`, and `.about-inner>div`.
  - Uses CSS transitions to trigger a slide-up and fade-in animation (`translateY(0)` + `opacity: 1`) once elements cross the `10%` visibility threshold.

---

## ⚡ Developer & AI Interaction Guidelines

> [!WARNING]
> **Token Optimization Alert:**
> When editing `index.html`, avoid loading the whole file or matching/replacing chunks containing the `<img>` tags in the products grid. Instead, perform target edits by specifying line ranges (e.g. editing variables in the `<style>` block at lines 10-15 or changing script variables in the `<script>` block at lines 480-540).

### 🛠️ Common Modification Tasks
1. **Adjusting Colors:** Edit the CSS Custom Properties in the `:root` block (lines 10-14).
2. **Adding/Removing Products:** Update elements within `.products-grid` (lines 310-399). Keep in mind that using external image URLs instead of long Base64 strings can reduce the HTML file size drastically.
3. **Updating Contacts/Pricing:** Change text variables inside `.contact-card` (lines 459-470) and modify the WhatsApp message query string (`text=Hi%20Ruchita...`).
4. **Tweaking Animation Speed/Quantity:** Modify the petal list generator `for (let i = 0; i < 40; i++)` (line 528) or edit property variables inside the `Petal` class.
