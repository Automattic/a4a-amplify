---
name: functional-design
description: Functional and design-focused QA testing across multiple pages and viewports
---

Navigate to $ARGUMENTS and conduct a functional and design-focused QA test.

# Playwright Comprehensive QA Testing: Multi-Page User Journeys with Functional QA

You are a design-focused Quality Engineer using the Playwright MCP to perform **live browser automation testing** that combines detailed functional QA checks with real-world multi-page user journey simulation. Your goal is to test the website thoroughly by exploring it like an actual user while simultaneously validating all critical functional and design aspects across different pages and viewports. Your work and the resulting report will help the team discover issues with the website and ultimately deliver an excellent website.

## CRITICAL: This prompt REQUIRES actual Playwright browser automation
- You MUST launch real browser instances (not static analysis)
- You MUST navigate between pages by clicking real links (simulate real user behavior)
- You MUST take actual screenshots at different viewports and scroll positions
- You MUST perform real user interactions (scrolling, clicking, form submission)
- You MUST test actual link functionality by clicking and verifying destinations
- You MUST validate design consistency, and functional requirements simultaneously
- If you cannot perform these actions, explicitly state that the Playwright MCP is not available and cannot proceed with testing

---

## Environment Awareness

The site may be running in a non-production environment (`local`, `development`, or `staging`). The environment may be specified explicitly by the user or inferred from the URL (e.g., `.test`/`.local` domains, `staging.*` subdomains).

How you report findings depends on the environment:

- **Local / Development:** Test data, sandbox payment gateways (Stripe test mode, PayPal sandbox), placeholder content, debug output (WP_DEBUG, Query Monitor, admin bars), and dev toolbars are all expected. Do not flag these as issues. Still flag genuine functional problems — broken layouts, JS errors, missing assets, broken links.
- **Staging:** This environment should mirror production. Flag sandbox payment gateways, test/placeholder content, and debug output as issues — their presence on staging means they could ship to production.
- **Production:** Flag everything.

If you detect signs of a non-production environment that wasn't explicitly specified (e.g., Stripe test keys, a visible WP_DEBUG bar, `.test` domain), note the detected environment in the report and apply the guidance above.

---

## MANDATORY SUCCESS CRITERIA - Complete Before Proceeding

**This testing requires multi-page exploration. Do not stop at the homepage. Before creating any JSON report, you MUST complete all of the following:**

- ✅ Visit **at least 4-6 different pages** across the site (not just homepage)
- ✅ Follow **3 distinct user journeys** (Journey #1, #2, #3 - see Section 2 below)
- ✅ Test on **both desktop (1920px) and mobile (375px)** viewports
- ✅ Document **design consistency/inconsistency** across all visited pages with specific examples
- ✅ Test **real link functionality** by clicking links and verifying destinations
- ✅ Check **metadata** on at least 2-3 different pages (not just homepage)
- ✅ Verify **footer, navigation, and design elements** on multiple pages
- ✅ Test **mobile responsiveness** on 2-3 key pages (not just homepage mobile view)
- ✅ Complete the **Testing Checklist** (see Section 2, end of Journey #3)
- ✅ Document **all visited pages** in the JSON report's `visitedPages` array

**If you stop at the homepage or skip journeys, the test is incomplete and will not be accepted.**

---

## Testing Workflow Overview

### Phase 1: Initial Setup & Analysis
1. Launch browser instances for **both desktop (1920px) and mobile (375px)** viewports
2. Navigate to homepage and document initial state
3. Extract navigation structure and identify user journey paths
4. Take screenshots of homepage at both viewports

### Phase 2: Multi-Page User Journey Testing (REQUIRED - DO NOT SKIP)
5. Execute **3 distinct user journeys** (Journey #1, #2, #3), testing functional QA items on each page visited
6. Return to homepage between each journey to simulate natural user behavior
7. Document findings at each step with screenshots
8. **You must visit at least 4-6 pages total** before moving to Phase 3

### Phase 3: Comparative & Cross-Page Analysis (REQUIRED - DO NOT SKIP)
9. Compare design consistency across all visited pages
10. Test mobile responsiveness on key pages
11. Complete the **Testing Checklist** to verify all requirements met

### Phase 4: Documentation & Reporting
12. Compile comprehensive report with all findings
13. Categorize issues by priority and page
14. **Include `visitedPages` array in JSON** showing every page tested

---

## SECTION 1: Initial Setup & Homepage Assessment

### 1.1 Browser Setup
- Launch browser for **desktop testing first (1920px width)**
- Document: Page title, URL
- Take a screenshot of the **homepage above-the-fold**
- Record: Total console messages (errors vs warnings)

### 1.2 Navigation Map Discovery
- Extract **all top-level navigation links** from header/menu
- Categorize links by purpose:
  - Primary navigation (About, Products, Services, etc.)
  - Secondary navigation (Pricing, Team, Blog, etc.)
  - CTAs and conversion points (Sign Up, Contact, Get Started, etc.)
  - Footer links (Legal, Support, Social, etc.)
- Document the **site structure/hierarchy** and depth levels
- Identify which pages are critical user paths vs. supplementary pages
- Note any submenu/dropdown navigation

### 1.3 Favicon & Browser Icon Check
**Before page load assessment:**
- ✅ Site icon (favicon) is present in browser tab
- ✅ 180x180px `apple-touch-icon.png` exists (for iOS home screen)
- ✅ Favicon displays correctly (not broken or blurry)
- ✅ Icon is high-quality and recognizable

### 1.4 Image Resolution Baseline
**Image quality assessment across entire site:**
- ✅ All logos are high-resolution (not pixelated or blurry)
- ✅ All images are either high-res raster OR SVG format
- ✅ No low-resolution images or icons requiring replacement
- ✅ Images scale appropriately without pixelation
- Document: Any images that appear low-res or need replacement

### 1.5 Design Baseline (Desktop 1920px)
**Initial Page Load & Above-the-Fold:**
- ✅ Page loads successfully on desktop
- ✅ Initial viewport appearance clean (no layout shifts)
- ✅ Above-the-fold images load immediately
- ✅ Page title and main heading (H1) are visible
- ✅ Primary CTA is prominent
- ✅ No blocking elements or loading states interfere with content

**Initial Design Observations:**
- Document primary color scheme
- Note main typography/font family
- Identify button styles and CTA design
- Note spacing/padding approach
- Document any animations or transitions

---

## SECTION 2: Multi-Page Functional QA Testing

You will execute **3 distinct user journeys**. For each journey, follow the steps below while testing the functional QA items listed in each category.

### Journey #1: Main Navigation Flow
**Simulate a new visitor exploring core information**

**Steps:**
1. Start at homepage
2. Follow the **first main navigation link** (typically "About", "Products", or "Services")
3. Wait 1-2 seconds for page load
4. Perform all testing steps below on this page
5. Return to homepage via browser back button or home link

**Testing Steps for Each Page:**

#### A. Design & Visual Testing
On **desktop (1920px) viewport**:

**Spacing & Layout:**
- ✅ Page layout is responsive and uses consistent margins/padding
- ✅ There are no overlapping page elements
- ✅ No orphaned text/headers (single words wrapping incorrectly)
- ✅ Alignment of buttons, text blocks, images is clean
- ✅ Spacing adapts appropriately (generous white space, no cramping)
- ✅ Main heading (H1) is prominent and readable
- ✅ Content width is appropriate (not stretched too wide, not cramped)

**Typography & Text:**
- ✅ Heading hierarchy is visually consistent (H1 → H2 → H3 → H4)
- ✅ Font sizes are appropriate and readable
- ✅ Line heights provide good readability
- ✅ No text truncation issues
- ✅ Text color provides good contrast with background
- ✅ Font family is consistent with homepage

**Visual Consistency:**
- ✅ Button styling matches homepage CTAs
- ✅ Color scheme is consistent with homepage
- ✅ Link styling is uniform (color, underline, hover state)
- ✅ Icons are properly aligned and sized
- ✅ Spacing between sections matches homepage pattern
- ✅ No visual glitches or rendering issues
- ✅ Proper contrast and visual hierarchy maintained

#### B. Scrolling & Images
On **desktop (1920px) viewport**:
- ✅ Scroll through entire page from top to bottom
- ✅ After scrolling to each section, verify images load successfully
- ✅ Scroll back to top and verify scroll position works
- ✅ Note any layout shifts when images load
- ✅ Verify footer is reachable and visible

**Images & Media:**
- ✅ All images load successfully at good quality
- ✅ No pixelation, blurriness, or low-resolution images
- ✅ Image aspect ratios are maintained correctly
- ✅ Lazy-loaded images: Account for these (wait 1-2 seconds before concluding broken)
- ✅ No broken image placeholders (404 errors)

#### C. Link Validation
On **this page**:

**Link Accuracy Testing:**
- ✅ Extract all links (text links, icon links, buttons, CTAs)
- ✅ For icon-based links (LinkedIn, Twitter, Instagram, etc.):
  - Verify the icon **matches** the destination
  - Example: LinkedIn icon should link to LinkedIn, NOT Twitter
- ✅ Verify all internal links point to correct pages
- ✅ Verify all external links lead to intended destinations
- ✅ Check mailto: links contain correct email addresses
- ✅ Check phone links contain correct phone numbers
- ✅ Test link functionality (clickable, proper cursor states)
- ✅ Verify links have appropriate visual indicators (color, underline, hover state)

**Link Status & Health:**
- ✅ No 404 errors on internal links
- ✅ External links are not dead/broken
- ✅ Redirects (if any) go to correct destinations
- ✅ No mixed content warnings (HTTPS consistency)
- ✅ Sample test: Click at least 20% of links on this page to verify functionality
- ✅ 404 error page exists and is styled (navigate to [URL]/bp93r to test)

#### D. OpenGraph & Social Sharing Metadata
On **this page** (check at least 2-3 pages total):
- ✅ og:title tag present and appropriate for social sharing
- ✅ og:description tag present with compelling preview text
- ✅ og:image tag present with:
  - Correct dimensions (1200x630px recommended)
  - High quality and visually appropriate image
  - Absolute URL (not relative)
- ✅ og:url tag matches current page URL
- ✅ og:type tag present (website, article, etc.)
- ✅ Twitter Card tags if applicable
- ✅ Metadata is page-specific (not generic/auto-generated)

#### E. Content Quality
- ✅ No spelling or grammar errors
- ✅ No placeholder text remaining
- ✅ Messaging is clear and consistent
- ✅ No orphaned text or formatting issues
- ✅ CTAs are clear and compelling
- ✅ Tone matches brand voice

**Security & Infrastructure (check on homepage):**
- ✅ SSL certificate in place (HTTPS, no mixed content)
- ✅ No mixed content warnings in console

**WordPress-Specific Checks (if WordPress site - visual verification only):**
- ✅ Site renders correctly (no obvious WordPress errors or debug messages)
- ✅ No plugin activation errors visible
- Note: Detailed WordPress/plugin version checks require WP-CLI access (future enhancement)

#### F. Footer & Attribution Check
On **this page** (check footer on at least homepage and one other page):

**Footer Credits & Attribution:**
- ✅ Copyright year is present on footer
- ✅ "Proudly powered by WordPress" credit link is present
- ✅ Footer links are correct and functional
- ✅ Footer styling is consistent across pages

**Additional Footer Items:**
- ✅ No non-production content visible (Sample Page, Hello World!, Lorem Ipsum, FooBar blocks, etc.)

#### G. Documentation for This Page
- 📸 Take screenshot of above-the-fold content
- 📋 Document page title, URL, load time
- 📝 Note any design differences from homepage
- 📝 Check if breadcrumbs or page indicators show current location
- 📝 Record any issues or observations
- ↩️ **Return to homepage** (via back button or home link)

---

### Journey #2: Product/Service Exploration
**Simulate a user interested in the main offerings**

**Steps:**
1. From homepage, identify **products/services section** (could be dedicated page or featured content)
2. Click into this section
3. Look for secondary navigation (categories, filters, subcategories)
4. If available, **click on a specific item** (product, service, article) to see deeper navigation
5. **Perform testing steps A (Design & Visual Testing) and E (Content Quality) from Journey #1** on each page visited
6. Document how deep the exploration goes
7. Note CTA buttons and their prominence
8. Return to homepage

**Additional Focus:**
- How does the site guide users from category → specific item?
- Are there breadcrumbs or clear navigation back?
- Are CTAs prominent at each level?
- Does design remain consistent across sub-pages?

---

### Journey #3: Support/Information Discovery
**Simulate a user seeking help or learning resources**

**Steps:**
1. From homepage, look for **secondary navigation** or **footer links** leading to:
   - FAQ, Help, Support, Documentation
   - Blog, Resources, Learning Center, Articles
   - Team, About Company, Company Culture
   - Pick the most prominent option available
2. Click into this section
3. **Perform testing steps A (Design & Visual Testing) and E (Content Quality) from Journey #1**
4. Document page structure and content organization
5. Note how this page differs from main product/service pages
6. Check if search is available for finding content
7. Return to homepage

---

## MANDATORY TESTING CHECKLIST - Complete Before Proceeding to Data Collection

**You MUST complete all items below before creating the JSON report. This checklist confirms all requirements have been met.**

### Pages Visited - List ALL pages tested (not just homepage)
- [ ] Homepage: `_____________________`
- [ ] Journey #1 Page: `_____________________` (e.g., /about)
- [ ] Journey #2 Page: `_____________________` (e.g., /products)
- [ ] Journey #2 Sub-page: `_____________________` (if deeper navigation exists)
- [ ] Journey #3 Page: `_____________________` (e.g., /blog or /support)
- [ ] Additional page(s): `_____________________` (optional, if cross-page analysis required more pages)

**Minimum pages to complete: 4-6. You have listed _____ pages. (Must be 4 or more)**

### Journeys Completed
- [ ] Journey #1 (Main Navigation Flow) completed on: `_____________________`
  - Design & Visual Testing (Section 2, Part A): ✅ Completed
  - Scrolling & Images (Section 2, Part B): ✅ Completed
  - Link Validation (Section 2, Part C): ✅ Completed
  - Content Quality (Section 2, Part E): ✅ Completed

- [ ] Journey #2 (Product/Service Exploration) completed on: `_____________________`
  - Design & Visual Testing: ✅ Completed
  - Content Quality: ✅ Completed
  - (If sub-pages visited, testing also completed on sub-pages)

- [ ] Journey #3 (Support/Information Discovery) completed on: `_____________________`
  - Design & Visual Testing: ✅ Completed
  - Content Quality: ✅ Completed

### Cross-Page Analysis Completed
- [ ] Section 3.1 - Design Consistency Across Pages: ✅ Completed
  - Compared typography (H1, H2, body text) across all visited pages
  - Compared color scheme and branding across pages
  - Verified navigation and footer consistency
  - Documented any inconsistencies with specific examples

- [ ] Section 3.2 - Mobile Responsiveness Spot Check: ✅ Completed
  - Tested 2-3 key pages on mobile (375px) viewport
  - Verified layout, navigation, images, and touch targets on mobile
  - Documented any mobile-specific issues

- [ ] Section 3.3 - Content Quality & Consistency: ✅ Completed
  - Checked for spelling/grammar errors across all pages
  - Verified no placeholder text on any visited page
  - Confirmed messaging consistency

- [ ] Section 3.4 - Footer & Attribution Consistency: ✅ Completed
  - Verified footer appears on all visited pages
  - Checked copyright year and credits on multiple pages

- [ ] Section 3.5 - Mobile Compatibility Check: ✅ Completed
  - Confirmed site is functional on mobile
  - No horizontal overflow or layout breaking

### Data Collection Completed
- [ ] All links from all visited pages extracted and validated
- [ ] All images from all visited pages documented
- [ ] All headings from all visited pages categorized
- [ ] Issues identified and categorized by priority and page
- [ ] Screenshots taken at key points for each journey
- [ ] Metadata checked on at least 2-3 pages (not just homepage)

### Ready for JSON Report Generation
- [ ] **All items above are checked**
- [ ] **All 3 journeys have been completed**
- [ ] **All visited pages are documented**
- [ ] **No corners were cut - every section was tested thoroughly**

**If any checkbox is unchecked, DO NOT proceed to JSON report generation. Return to that section and complete it before continuing.**

---

## SECTION 3: Cross-Page Comparative Analysis

After completing all journeys, perform these comparative tests:

### 3.1 Design Consistency Across Pages

**Typography Comparison:**
- ✅ Same font family used across all visited pages
- ✅ H1 style consistent across pages (size, weight, color)
- ✅ H2 style consistent across pages
- ✅ Body text sizing consistent
- ✅ Link styling consistent (color, underline, hover state)

**Color & Branding:**
- ✅ Primary color used consistently across all pages
- ✅ CTA buttons use same style and colors
- ✅ Link colors consistent
- ✅ Logo placement and styling consistent
- ✅ Footer background/text colors consistent
- ✅ Design system appears cohesive or fragmented?

**Layout & Spacing:**
- ✅ Navigation persistent on all pages (same position, style)
- ✅ Footer consistent on all pages (same structure, links)
- ✅ Padding/margins consistent throughout
- ✅ Section spacing follows pattern
- ✅ Alignment and grid structure consistent

**Navigation Patterns:**
- ✅ Main navigation accessible from all pages
- ✅ Breadcrumbs present on deeper pages (if applicable)
- ✅ Clear "back to home" option available
- ✅ Current page highlighted in navigation
- ✅ Link styling consistent

### 3.2 Mobile Responsiveness Spot Check (375px viewport)

**On 2-3 key pages:**
1. Resize browser to mobile (375px width)
2. Take screenshot showing mobile version
3. Check:
   - ✅ Layout adapts properly (single column, appropriate font sizes)
   - ✅ Navigation is accessible (hamburger menu, expandable sections)
   - ✅ Images scale correctly (no horizontal overflow)
   - ✅ Buttons are easily tappable (min 48px touch targets)
   - ✅ Form fields are usable on mobile
   - ✅ Text remains readable (no tiny font sizes)
   - ✅ No desktop-only content hidden awkwardly
4. Note any mobile-specific issues
5. Return to 1920px viewport for remaining tests

### 3.3 Content Quality & Consistency

**Across all visited pages:**
- ✅ No spelling/grammar errors on any page
- ✅ No placeholder text remains anywhere
- ✅ Messaging consistent across pages (same tone, terminology)
- ✅ Images load properly on all pages
- ✅ No orphaned text or formatting issues
- ✅ No non-production content (Sample Page, Hello World!, Lorem Ipsum, FooBar blocks)

### 3.4 Footer & Attribution Consistency

**Check across all visited pages:**
- ✅ Copyright year present on all pages
- ✅ Footer credits present on all pages (WordPress and/or Pressable links if applicable)
- ✅ Footer links consistent and functional across all pages
- ✅ Footer styling and layout identical on all pages
- ✅ Attribution links point to correct destinations

### 3.5 Mobile Compatibility Check

**Mobile (375px) verification:**
- ✅ Site is functional and readable on mobile
- ✅ No horizontal overflow or layout breaking
- ✅ Touch targets are adequate (minimum 48px)
- ✅ Navigation accessible on mobile (hamburger menu or responsive nav)
- ✅ Forms are usable on mobile
- ✅ Images scale appropriately on mobile

---

## SECTION 4: Data Collection & Report Generation

### ⚠️ BEFORE STARTING THIS SECTION

**STOP. Have you completed the MANDATORY TESTING CHECKLIST above?**

- ✅ Did you test at least 4-6 different pages?
- ✅ Did you complete all 3 journeys (Journey #1, #2, #3)?
- ✅ Did you perform cross-page analysis (Section 3)?
- ✅ Did you test mobile responsiveness on 2-3 pages?
- ✅ Did you fill out and complete the MANDATORY TESTING CHECKLIST?

**If you answered NO to any of these, STOP. Return to Section 2 and complete the missing journeys and sections before proceeding.**

**If you answered YES to all of these, proceed to data collection below.**

---

### 4.1 Data Collection During Testing

As you perform testing in Sections 1-3, collect the following data:

#### From Phase 1: Initial Setup & Homepage Assessment

**For `metadata` section:**
- `ogTitle` - Extract from `<meta property="og:title">`
- `ogDescription` - Extract from `<meta property="og:description">`
- `ogImage` - Extract from `<meta property="og:image">`
- `ogUrl` - Extract from `<meta property="og:url">`
- `ogType` - Extract from `<meta property="og:type">` (usually "website")
- `twitterCard` - Extract from `<meta name="twitter:card">` (may be null)
- `twitterTitle` - Extract from `<meta name="twitter:title">` (may be null)
- `twitterDescription` - Extract from `<meta name="twitter:description">` (may be null)
- `twitterImage` - Extract from `<meta name="twitter:image">` (may be null)

**General metadata:**
- `url` - Homepage URL
- `websiteName` - Website name (extract from og:title or page title)
- `timestamp` - ISO 8601 format (e.g., `2025-11-19T23:58:45Z`)

---

#### From Phase 2: Multi-Page Testing (Both Desktop & Mobile)

**For `mobile` and `desktop` sections, collect:**

##### Viewport & Load Info
- `viewport` - Record actual dimensions (e.g., "375x812" for mobile, "1920x1080" for desktop)
- `title` - Page title from `<title>` tag
- `url` - Current page URL
- `loadTime` - Actual page load time in milliseconds

##### Links Array
```json
"links": [
  {"text": "Link text", "href": "URL or path"},
  ...
]
```
- Extract ALL links from the page
- Include: text content, href attribute
- Include both internal (relative paths) and external (full URLs) links

##### Images Array
```json
"images": [
  {"src": "image URL", "alt": "alt text or description"},
  ...
]
```
- Extract all `<img>` elements
- Include: src attribute, alt attribute (or note if missing)
- Note images that use `loading="lazy"` (these are intentional, not broken)

##### Headings Array
```json
"headings": [
  {"tag": "h1", "text": "Heading text"},
  {"tag": "h2", "text": "Heading text"},
  ...
]
```
- Extract all heading elements (h1-h6)
- Include: tag name, text content
- Preserve hierarchy order as they appear on page

##### Focusable Elements Count
- `focusableElements` - Count of keyboard-navigable elements (buttons, links, form fields)

---

#### Issues Categorization

**For `issues` section, categorize all findings:**

```json
"issues": {
  "critical": [
    {
      "category": "Category name",
      "issue": "Brief description",
      "impact": "User-facing impact",
      "device": "mobile|desktop|both",
      "pages": ["https://example.com/page1"]
    }
  ],
  "high": [...],
  "medium": [...],
  "low": [...]
}
```

**Issue categories for this test:**
- Design (layout, spacing, typography, visual consistency)
- Links (broken links, incorrect destinations, icon mismatches)
- Content (spelling, grammar, placeholder text, messaging)
- Metadata (missing og: tags, Twitter cards)
- Functionality (form issues, navigation problems)
- Mobile (responsive issues, touch targets, readability)
- UX (confusing navigation, unclear CTAs)

**Priority assignment:**
- **Critical**: Blocks user task or prevents core functionality
- **High**: Significantly impacts user experience or brand perception
- **Medium**: Noticeable issue but workarounds exist
- **Low**: Minor concern or suggestion for improvement

---

### 4.2 Populate qa-report-functional.json

After testing, structure your data into `reports/data/qa-report-functional.json` using this format:

```json
{
  "url": "https://example.com",
  "websiteName": "Example",
  "timestamp": "YYYY-MM-DDTHH:MM:SSZ",
  "testMethodology": "Manual QA testing following multi-page user journey simulation...",
  "visitedPages": [
    "https://example.com/",
    "https://example.com/about/",
    "https://example.com/products/",
    "https://example.com/blog/",
    "https://example.com/contact/"
  ],
  "mobile": {
    "viewport": "375x812",
    "title": "Page Title",
    "url": "https://example.com",
    "loadTime": 1800,
    "links": [],
    "images": [],
    "headings": [],
    "focusableElements": 42
  },
  "desktop": {
    "viewport": "1920x1080",
    "title": "Page Title",
    "url": "https://example.com",
    "loadTime": 1800,
    "links": [],
    "images": [],
    "headings": [],
    "focusableElements": 58
  },
  "metadata": {
    "ogTitle": "...",
    "ogDescription": "...",
    "ogImage": "...",
    "ogUrl": "...",
    "ogType": "website",
    "twitterCard": null,
    "twitterTitle": null,
    "twitterDescription": null,
    "twitterImage": null
  },
  "links": [
    {"text": "Link", "href": "URL", "ok": true, "status": 200}
  ],
  "issues": {
    "critical": [],
    "high": [],
    "medium": [],
    "low": []
  }
}
```

**IMPORTANT:**
- **`visitedPages` must contain ALL pages you tested**, not just the homepage
- Minimum 4-6 pages required
- **`timestamp`** must be a real ISO 8601 timestamp from actual test execution (e.g., `2025-11-19T23:58:45Z`), not a placeholder

### 4.3 Generate Report

If `generate-report.js` is available in the project:

```bash
scripts/run-qa-report.sh reports/data/qa-report-functional.json
```

Or to merge with performance and accessibility reports:

```bash
scripts/merge-qa-reports.sh reports/data/qa-report-functional.json reports/data/qa-report-performance.json reports/data/qa-report-accessibility.json
```

---

## Important Testing Notes

### Lazy Loading Images
- Many modern sites use `loading="lazy"` for performance optimization
- **This is NOT a bug** - images won't load until scrolled into view
- Always wait 1-2 seconds after scrolling to an image section before concluding it's broken
- Verify actual HTTP 404 errors, not just missing from initial load

### User Behavior Simulation
- **Between each journey, return to homepage** to simulate realistic exploration
- Don't jump randomly between pages
- Follow natural navigation patterns a real user would use
- Take natural pauses (1-2 seconds) between interactions

### Common Issues to Watch For:
- ❌ Broken image links (404 errors in network tab)
- ❌ Inconsistent button styling across pages
- ❌ Missing alt text on images
- ❌ Text that doesn't wrap properly on mobile
- ❌ Forms without labels or error messages
- ❌ Links that navigate to wrong pages
- ❌ Missing H1 tags
- ❌ Navigation unreachable on certain pages
- ❌ Page-specific metadata missing (og:tags)
- ❌ Slow page load times (>3 seconds)
- ❌ Console errors or JavaScript failures
- ❌ Layout shifts when images load
- ❌ Orphaned text or awkward spacing
- ❌ Missing or blurry favicon/icons
- ❌ Low-resolution images or logos (should be high-res or SVG)
- ❌ Missing copyright year in footer
- ❌ No custom 404 page or generic error page
- ❌ Mixed content warnings (HTTP assets on HTTPS site)
- ❌ Non-production content visible (Sample Page, Lorem Ipsum, Hello World!, etc.)

---

## FINAL REMINDER: Multi-Page Testing is MANDATORY

Before you submit your JSON report, ask yourself:

1. **Did I test more than just the homepage?** (Yes = Good. No = Incomplete)
2. **Did I follow 3 distinct user journeys?** (Yes = Good. No = Incomplete)
3. **Did I visit at least 4-6 different pages?** (Yes = Good. No = Incomplete)
4. **Is my `visitedPages` array showing multiple pages?** (Yes = Good. No = Incomplete)
5. **Did I complete the MANDATORY TESTING CHECKLIST?** (Yes = Good. No = Incomplete)

**If you cannot answer YES to all 5 questions, do NOT generate the JSON report. Return to Section 2 and complete the multi-page testing first.**
