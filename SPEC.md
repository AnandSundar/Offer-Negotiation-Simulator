# Offer Negotiation Simulator — SPEC.md

## 1. Project Overview

**Project Name:** Offer Negotiation Simulator
**Type:** Single-file static HTML web application
**Core Functionality:** A premium SaaS-style wizard tool that helps senior GRC engineers and tech professionals negotiate $150K–$250K+ compensation packages by calculating leverage score and generating tailored negotiation emails.
**Target Users:** Senior GRC engineers and tech professionals negotiating high-value roles

---

## 2. Visual & Rendering Specification

### Scene Setup
- **Layout:** Multi-step wizard with hash-based routing (#step1 → #step2 → #step3 → #step4 → #result)
- **Navigation:** Step progress indicator with percentage fill bar at top
- **Transitions:** Fade + slide animations between steps (300ms ease-out)

### Color Palette (Nexus Dark Mode)
- **Background Primary:** `#0A0A0B` (near-black)
- **Background Surface:** `#111113` (cards, inputs)
- **Background Elevated:** `#1A1A1D` (hover states, borders)
- **Text Primary:** `#FAFAFA` (headings, important text)
- **Text Secondary:** `#A1A1AA` (labels, descriptions)
- **Text Muted:** `#71717A` (placeholders, hints)
- **Accent Primary:** `#14B8A6` (teal-500 — buttons, focus, progress)
- **Accent Hover:** `#0D9488` (teal-600)
- **Accent Muted:** `rgba(20, 184, 166, 0.15)` (subtle backgrounds)
- **Error:** `#EF4444` (validation errors)
- **Warning:** `#F59E0B` (caution states)
- **Success:** `#22C55E` (confirmation)

### Typography
- **Body Font:** Satoshi (Fontshare) — `https://www.fontshare.com/fonts/satoshi`
- **Headline Font:** Instrument Serif (Fontshare) — `https://www.fontshare.com/fonts/instrument-serif`
- **Type Scale:**
  - `--text-xs`: clamp(0.75rem, 0.7rem + 0.25vw, 0.875rem)
  - `--text-sm`: clamp(0.875rem, 0.8rem + 0.35vw, 0.9375rem)
  - `--text-base`: clamp(1rem, 0.95rem + 0.25vw, 1.0625rem)
  - `--text-lg`: clamp(1.125rem, 1rem + 0.5vw, 1.25rem)
  - `--text-xl`: clamp(1.25rem, 1.1rem + 0.75vw, 1.5rem)
  - `--text-2xl`: clamp(1.5rem, 1.25rem + 1.25vw, 2rem)
  - `--text-hero`: clamp(2.5rem, 2rem + 2.5vw, 4rem)

### Spacing System
- `--space-1`: 0.25rem
- `--space-2`: 0.5rem
- `--space-3`: 0.75rem
- `--space-4`: 1rem
- `--space-6`: 1.5rem
- `--space-8`: 2rem
- `--space-12`: 3rem
- `--space-16`: 4rem

### Light Mode Overrides
- **Background Primary:** `#FAFAFA`
- **Background Surface:** `#FFFFFF`
- **Background Elevated:** `#F4F4F5`
- **Text Primary:** `#18181B`
- **Text Secondary:** `#52525B`
- **Text Muted:** `#A1A1AA`

### Components
- **Header:** Logo (SVG briefcase + upward arrow) left, light/dark toggle right
- **Progress Bar:** Step indicator with animated fill percentage
- **Form Inputs:** Dark surface, teal focus ring, error states in red
- **Buttons:** Primary (teal fill), Secondary (ghost with border), disabled states
- **Cards:** Surface background with subtle border, no colored left borders
- **Radio Buttons:** Custom teal dot indicator
- **Dropdown:** Custom styled select with teal accent
- **Accordion:** Collapsible sections with chevron rotation animation

### Animations
- **Step Transition:** opacity 0→1 + translateY(20px→0), 300ms ease-out
- **Progress Bar Fill:** width transition 400ms ease-out
- **Leverage Gauge:** SVG stroke-dashoffset animation, count-up from 0 to final score (1.5s)
- **Phrase Chip Copy:** scale(0.95)→scale(1) pulse, "Copied!" tooltip fade
- **Email Copy:** button icon swap to checkmark, 2s duration

---

## 3. Application Flow Specification

### Hash Routes
- `#step1` — Offer Details (default/initial)
- `#step2` — Your Situation
- `#step3` — Tone Calibration
- `#step4` → `#result` — Results (Leverage Card + Email)

### Step 1: Offer Details
**Fields:**
| Field | Type | Required | Validation |
|-------|------|----------|------------|
| Company name | text | Yes | min 1 char |
| Role title | text | Yes | min 1 char |
| Base salary offered | number | Yes | > 0, formatted with commas on blur |
| Signing bonus offered | number | No | >= 0 |
| Equity/RSUs | text | No | placeholder: "$50K over 4 years" |
| PTO days | number | No | 0-365 |
| Work location | radio | Yes | Remote / Hybrid / On-site |
| Benefits tier | select | No | Excellent / Good / Average / Poor |

### Step 2: Your Situation
**Fields:**
| Field | Type | Required | Validation |
|-------|------|----------|------------|
| Current base salary | number | Yes | > 0 |
| Walk-away minimum | number | Yes | > 0 |
| Target base salary | number | Yes | > 0 |
| Employment status | radio | Yes | Employed / Actively interviewing / Have competing offer / Unemployed |
| Competing offer base | number | Conditional | Shown if "Have competing offer", >= 0 |
| Years of experience | number | Yes | 0-50 |
| Time pressure | radio | Yes | Low / Medium / High |
| Top performer | radio | Yes | Yes / No / N/A |

**Micro-copy:** Under walk-away: "This stays private — it's just for calculating your leverage."
**Empty state:** Competing offer field: "Even a verbal offer counts. Don't undersell yourself."

### Step 3: Tone Calibration
**Fields:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| Email tone | radio | Yes | Collaborative & Warm / Confident & Direct / Diplomatic & Strategic |
| Custom context | textarea | No | Placeholder: "Anything else the email should reference?" |

**Tone Descriptions:**
- **Collaborative & Warm:** "best when you love the company and don't want to risk the relationship"
- **Confident & Direct:** "best when you have leverage or a competing offer"
- **Diplomatic & Strategic:** "best for ambiguous situations or first offers from dream companies"

### Step 4 / Result: Results Page
**Layout:** Two-column split (left: Leverage Score, right: Generated Email)

#### Leverage Score Card (Left)
**Calculation (0-100 points):**
| Factor | Points | Condition |
|--------|--------|-----------|
| Competing offer | +30 | If "Have competing offer" selected |
| Employed | +15 | If "Employed" (not actively job-seeking) |
| Below target | +10 | If offered base < target base |
| Above walk-away | +10 | If offered base > walk-away minimum |
| Low time pressure | +10 | If "Low" selected |
| 5+ years experience | +10 | If years >= 5 |
| Top performer | +10 | If "Yes" selected |

**Score Labels:**
- 0–30: "Thin Ice" (red tint)
- 31–55: "Negotiable" (yellow tint)
- 56–75: "Strong Position" (teal tint)
- 76–100: "Commanding" (bright teal)

**Display:**
- Animated SVG circular gauge (stroke-dashoffset animation)
- Count-up number animation to final score
- 3-4 bullet points explaining leverage in plain language

#### Generated Email (Right)
**Required Phrases (integrated naturally):**
- "directionally aligned"
- "get creative"
- "competitive with market"
- "excited about the opportunity"

**Rules:**
- Competing offer: reference tactfully, no ultimatum
- Employed: subtly reinforce stability
- Below walk-away: firm but warm pushback
- Tone from Step 3 adjusts formality/word choice

**Structure:**
- Subject line
- Salutation
- 3-4 body paragraphs
- Professional closing

**Actions:**
- "Copy to Clipboard" button → shows checkmark on success
- "Regenerate with different tone" → returns to Step 3

#### Phrase Bank (Below Email)
**Collapsible Accordion (3 sections):**
1. **Opening Softeners:** 4-5 phrases like "I'm very excited about this opportunity…"
2. **Anchoring Phrases:** 4-5 phrases like "Based on my research and market data…"
3. **Closing Bridges:** 4-5 phrases like "I'm confident we can find a number that works for both sides…"

**Phrase Chips:** Copyable with pulse animation + "Copied!" tooltip

---

## 4. Interaction Specification

### Navigation
- "Continue" button advances to next step (validates current step first)
- "Back" button on all steps except Step 1
- Step indicator shows current step and progress percentage
- Hash-based URL updates for each step

### Form Validation
- Required fields highlighted with `--color-error` border
- Inline error message below invalid fields
- Continue button disabled until step is valid

### Light/Dark Toggle
- Sun icon (light mode) / Moon icon (dark mode)
- Persists to `prefers-color-scheme` media query
- Toggle button in top-right header

### Copy Interactions
- Email copy: button text changes to checkmark for 2 seconds
- Phrase chips: scale pulse animation, "Copied!" tooltip

### Accordion
- Click header to expand/collapse
- Chevron icon rotates 180° on expand
- Smooth height animation

---

## 5. Technical Specification

### Dependencies (CDN)
- **Fonts:** Fontshare — Satoshi, Instrument Serif
- **Icons:** Lucide Icons (CDN)

### File Structure
- Single file: `offer-negotiation-simulator.html`
- No external assets required

### Browser Support
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile-first responsive (375px minimum, 1280px desktop)

### Accessibility (WCAG AA)
- All text contrast ratios ≥ 4.5:1
- Focus visible states on all interactive elements
- Proper form labels and ARIA attributes
- Keyboard navigable

---

## 6. Acceptance Criteria

### Visual Checkpoints
- [ ] Dark mode first with proper Nexus palette
- [ ] Light/dark toggle functional with sun/moon icons
- [ ] Typography uses Satoshi body + Instrument Serif headlines
- [ ] Progress bar shows step percentage
- [ ] Step transitions are smooth (fade + slide)

### Functional Checkpoints
- [ ] All 4 steps navigable via Continue/Back buttons
- [ ] Hash routing updates URL correctly
- [ ] Form validation prevents advancing with missing required fields
- [ ] Salary fields format with commas
- [ ] Conditional competing offer field appears when selected
- [ ] Leverage score calculates correctly (0-100)
- [ ] SVG gauge animates with count-up
- [ ] Email generates based on inputs and tone
- [ ] Email copy button works with visual feedback
- [ ] Phrase bank accordion expands/collapses
- [ ] Phrase chips are copyable with animation

### Responsive Checkpoints
- [ ] 375px: Single column, stacked layout
- [ ] 1280px: Two-column results layout (Leverage + Email side by side)
