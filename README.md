# Offer Negotiation Simulator

<p align="center">
  <img src="https://img.shields.io/badge/Type-Static%20HTML%20App-14B8A6?style=for-the-badge" alt="Type">
  <img src="https://img.shields.io/badge/License-MIT-14B8A6?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/Version-1.0.0-14B8A6?style=for-the-badge" alt="Version">
</p>

A premium SaaS-style wizard tool that helps senior GRC engineers and tech professionals negotiate $150K–$250K+ compensation packages. The simulator calculates your leverage score and generates tailored negotiation emails — no AI required, just smart templates and proven strategies.

---

## Table of Contents

- [Features](#features)
- [Quick Start](#quick-start)
- [How It Works](#how-it-works)
- [The Four Steps](#the-four-steps)
- [Leverage Score Explained](#leverage-score-explained)
- [Email Generation](#email-generation)
- [Phrase Bank](#phrase-bank)
- [Customization](#customization)
- [Browser Support](#browser-support)
- [Accessibility](#accessibility)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Development](#development)
- [License](#license)

---

## Features

### Core Functionality
- **4-Step Wizard Flow** — Intuitive step-by-step process from offer details to final email
- **Leverage Score Calculator** — Quantifies your negotiation power on a 0-100 scale
- **Smart Email Generator** — Creates professionally-toned negotiation emails
- **Copy-to-Clipboard** — One-click copying for emails and individual phrases
- **Hash-Based Routing** — Bookmarkable URLs for each step (#step1, #step2, etc.)

### Visual Design
- **Nexus Dark Mode** — Premium dark theme as default
- **Light Mode Toggle** — Seamless light/dark theme switching
- **Satoshi + Instrument Serif Typography** — Distinctive Fontshare font pairing
- **Animated SVG Gauge** — Smooth circular progress visualization
- **Smooth Transitions** — Fade + slide animations between steps (300ms)
- **Responsive Layout** — Mobile-first, optimized for 375px to 1280px+

### User Experience
- **Form Validation** — Prevents advancing without required fields
- **Salary Formatting** — Automatic comma formatting on blur
- **Conditional Fields** — Competing offer field appears contextually
- **Progress Indicator** — Visual progress bar with percentage fill
- **Accordion Phrase Bank** — Expandable sections with copyable chips
- **Persistent Theme** — Respects system `prefers-color-scheme` preference

---

## Quick Start

### Option 1: Open Directly
```bash
# Simply open the HTML file in your browser
open offer-negotiation-simulator.html
# or on Windows
start offer-negotiation-simulator.html
```

### Option 2: Local Server (Recommended for Development)
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .

# Using PHP
php -S localhost:8000
```
Then visit `http://localhost:8000`

---

## How It Works

The Offer Negotiation Simulator guides you through a structured 4-step process:

1. **Enter Your Offer Details** — Company, role, salary, bonuses, equity, location
2. **Assess Your Situation** — Current salary, walk-away minimum, target, employment status
3. **Calibrate Your Tone** — Choose between Collaborative, Confident, or Diplomatic approaches
4. **Get Your Results** — Leverage score visualization + tailored negotiation email

---

## The Four Steps

### Step 1: Offer Details
Collects the compensation package being offered:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| Company Name | Text | Yes | Target company |
| Role Title | Text | Yes | Position title |
| Base Salary | Number | Yes | Annual base in USD |
| Signing Bonus | Number | No | One-time signing amount |
| Equity/RSUs | Text | No | e.g., "$50K over 4 years" |
| PTO Days | Number | No | Paid time off days |
| Work Location | Radio | Yes | Remote / Hybrid / On-site |
| Benefits Tier | Select | No | Excellent / Good / Average / Poor |

### Step 2: Your Situation
Assesses your negotiation leverage:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| Current Base Salary | Number | Yes | Your current annual base |
| Walk-Away Minimum | Number | Yes | Lowest you'll accept (kept private) |
| Target Base Salary | Number | Yes | Your desired salary |
| Employment Status | Radio | Yes | Employed / Actively interviewing / Have competing offer / Unemployed |
| Competing Offer Base | Number | Conditional | Shown when "Have competing offer" is selected |
| Years of Experience | Number | Yes | Total professional experience (0-50) |
| Time Pressure | Radio | Yes | Low / Medium / High urgency |
| Top Performer | Radio | Yes | Yes / No / N/A |

### Step 3: Tone Calibration
Sets the email tone and context:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| Email Tone | Radio | Yes | Collaborative & Warm / Confident & Direct / Diplomatic & Strategic |
| Custom Context | Textarea | No | Any additional context for the email |

**Tone Descriptions:**
- **Collaborative & Warm** — Best when you love the company and don't want to risk the relationship
- **Confident & Direct** — Best when you have leverage or a competing offer
- **Diplomatic & Strategic** — Best for ambiguous situations or first offers from dream companies

### Step 4: Results
Displays your leverage analysis and generated email:

- **Leverage Score Card** — Animated circular gauge (0-100) with breakdown
- **Negotiation Email** — Professionally formatted with subject line
- **Phrase Bank** — Copyable opening softeners, anchoring phrases, and closing bridges

---

## Leverage Score Explained

The leverage score (0-100) is calculated based on seven factors:

| Factor | Points | Condition |
|--------|--------|-----------|
| Competing Offer | +30 | "Have competing offer" selected |
| Employed Status | +15 | "Employed" selected (not actively seeking) |
| Below Target | +10 | Offered base < target base |
| Above Walk-Away | +10 | Offered base > walk-away minimum |
| Low Time Pressure | +10 | "Low" time pressure selected |
| Senior Experience | +10 | 5+ years of experience |
| Top Performer | +10 | "Yes" selected |

**Score Labels:**
| Score Range | Label | Visual Style |
|-------------|-------|--------------|
| 0–30 | Thin Ice | Red tint |
| 31–55 | Negotiable | Yellow tint |
| 56–75 | Strong Position | Teal tint |
| 76–100 | Commanding | Bright teal |

---

## Email Generation

The generated email follows a proven structure:

1. **Subject Line** — Concise, professional negotiation subject
2. **Salutation** — Personalized to the company/recruiter
3. **Opening** — Expresses enthusiasm (uses Opening Softeners)
4. **Body** — References market data, leverage points, and specific offers
5. **Closing** — Professional bridge to next steps (uses Closing Bridges)

**Required Phrases** (integrated naturally):
- "directionally aligned"
- "get creative"
- "competitive with market"
- "excited about the opportunity"

**Tone Adjustments:**
- **Collaborative** — More "we" language, relationship-focused
- **Confident** — Direct statements, confident framing
- **Diplomatic** — Strategic language, carefully hedged

---

## Phrase Bank

Three collapsible accordion sections with copyable phrase chips:

### 1. Opening Softeners
Polite phrases to express enthusiasm without committing:
- "I'm very excited about this opportunity..."
- "First, I want to say how much I'm looking forward to..."
- "I appreciate you sharing these details with me..."
- "Thank you for this offer — I'm genuinely thrilled..."
- "I wanted to start by expressing my enthusiasm for..."

### 2. Anchoring Phrases
Data-driven statements to establish your value:
- "Based on my research and market data..."
- "Given my experience and the current market for..."
- "Considering my track record with..."
- "According to industry benchmarks for..."
- "My research indicates that similar roles in..."

### 3. Closing Bridges
Professional transitions to continued negotiation:
- "I'm confident we can find a number that works for both sides..."
- "I hope we can continue the conversation about..."
- "I'm looking forward to finding a creative solution..."
- "I'd love to explore how we might make this work..."
- "I believe there's a path forward that benefits everyone..."

---

## Customization

### Theme Colors
Edit the CSS custom properties in `:root`:

```css
:root {
  --bg-primary: #0A0A0B;
  --bg-surface: #111113;
  --bg-elevated: #1A1A1D;
  --text-primary: #FAFAFA;
  --text-secondary: #A1A1AA;
  --accent-primary: #14B8A6;
  /* ... more variables */
}
```

### Fonts
Fonts are loaded from Fontshare CDN. To change:
1. Update the Google Fonts link in `<head>`
2. Modify `--font-body` and `--font-display` in CSS

### Leverage Calculation
Edit the `calculateLeverage()` function in JavaScript:

```javascript
function calculateLeverage(data) {
  let score = 0;
  // Adjust scoring logic here
  return Math.min(100, Math.max(0, score));
}
```

### Email Templates
Edit the template strings in the email generation section:

```javascript
const emailTemplates = {
  collaborative: `...`,
  confident: `...`,
  diplomatic: `...`
};
```

---

## Browser Support

| Browser | Version | Status |
|---------|---------|--------|
| Chrome | 80+ | ✅ Supported |
| Firefox | 75+ | ✅ Supported |
| Safari | 13+ | ✅ Supported |
| Edge | 80+ | ✅ Supported |
| Mobile Safari | 13+ | ✅ Supported |
| Chrome Mobile | 80+ | ✅ Supported |

---

## Accessibility

This app follows **WCAG AA** guidelines:

- **Color Contrast** — All text meets 4.5:1 contrast ratio minimum
- **Focus States** — Visible focus indicators on all interactive elements
- **Form Labels** — All inputs have associated labels
- **ARIA Attributes** — Proper roles and labels for screen readers
- **Keyboard Navigation** — Full keyboard operability
- **Semantic HTML** — Proper heading hierarchy and landmark regions

---

## Project Structure

```
Offer Negotiation Simulator/
├── .gitignore              # Git ignore rules
├── SPEC.md                 # Detailed specification document
├── README.md               # This file
├── package.json            # Node.js dependencies (for testing)
└── offer-negotiation-simulator.html  # The complete application (single file)
```

---

## Tech Stack

| Category | Technology | Purpose |
|----------|------------|---------|
| Core | HTML5 + CSS3 + Vanilla JS | Application logic and rendering |
| Fonts | Fontshare (Satoshi, Instrument Serif) | Typography |
| Icons | Lucide Icons (CDN) | UI iconography |
| Build | None required | Single-file deployment |

**No frameworks, no build tools, no dependencies to install.**

---

## Development

### Running Locally
```bash
# Clone the repository
git clone https://github.com/AnandSundar/Offer-Negotiation-Simulator.git
cd Offer-Negotiation-Simulator

# Start a local server
python -m http.server 8000
# or
npx serve .

# Open in browser
open http://localhost:8000
```

### Testing
Simply open `offer-negotiation-simulator.html` in different browsers and devices. Test:
- [ ] All form inputs accept and validate correctly
- [ ] Navigation between all steps works
- [ ] Theme toggle switches correctly
- [ ] Copy-to-clipboard functions work
- [ ] Accordion expand/collapse animations smooth
- [ ] Responsive breakpoints display correctly

### Deployment
Since this is a single HTML file, deployment options include:

1. **GitHub Pages** — Push to `gh-pages` branch
2. **Netlify Drop** — Drag and drop the folder
3. **Vercel** — `vercel deploy`
4. **Any static host** — S3, Cloudflare Pages, etc.

---

## License

MIT License — feel free to use, modify, and distribute.

---

<p align="center">
  <strong>Built for negotiators who know their worth.</strong>
</p>
