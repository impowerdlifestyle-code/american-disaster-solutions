# Schema.org Structured Data Audit
## americandisastersolutions.com
**Audit Date:** 2026-03-26

---

## Executive Summary

The site has a solid foundation of structured data across 7 pages with JSON-LD format used consistently (good). The homepage carries the most robust schema (LocalBusiness + WebSite), and BreadcrumbList is deployed on 6 of 7 pages. However, there are several validation issues, missing recommended properties, cross-page consistency gaps, and significant schema opportunities being left on the table.

**Overall score: 6.5/10** -- Good foundation, but meaningful improvements available.

---

## Page-by-Page Analysis

---

### 1. index.html (Homepage)

**Existing Schema Blocks:**

#### Block 1: LocalBusiness (lines 22-108)
- **@context:** `https://schema.org` -- PASS
- **@type:** `LocalBusiness` -- PASS
- **@id:** `https://americandisastersolutions.com/#organization` -- PASS

**Validation Results:**

| Property | Status | Notes |
|----------|--------|-------|
| name | PASS | "American Disaster Solutions" |
| url | PASS | Absolute URL |
| telephone | PASS | E.164 format (+18005135237) |
| email | PASS | |
| address | PASS | Complete PostalAddress |
| geo | PASS | GeoCoordinates present |
| image | PASS | Absolute URL |
| logo | WARNING | Uses `IMG_8259.webp` (a photo) instead of the actual logo file `ads-logo.png` |
| openingHoursSpecification | PASS | 24/7 correctly expressed |
| priceRange | PASS | |
| areaServed | PASS | 19 states listed |
| founder | PASS | Two Person objects |
| aggregateRating | PASS | ratingValue 5.0, reviewCount 3 |
| review | PASS | 3 reviews matching reviewCount |
| sameAs | WARNING | Only 2 social profiles. Missing `https://x.com/americandisaster` which appears in site footer |
| alternateName | PASS | "ADS" |

**Issues Found:**

1. **WARNING -- Logo property uses a photo, not the logo.** The `logo` property is set to `IMG_8259.webp` but the actual site logo is `/images/ads-logo.png`. This should be the official company logo.

2. **WARNING -- Incomplete sameAs.** The X/Twitter profile `https://x.com/americandisaster` is linked in the footer but missing from `sameAs`.

3. **INFO -- areaServed uses `"@type": "State"`.** The `State` type is valid in Schema.org but is from the administrative area vocabulary. Using `"@type": "AdministrativeArea"` is more broadly recognized. Current usage is acceptable.

4. **MISSING -- No `foundingDate` property.** Recommended for LocalBusiness.

5. **MISSING -- No `numberOfEmployees` property.** Recommended for trust signals.

6. **MISSING -- Reviews lack `datePublished`.** Google recommends `datePublished` on Review objects for rich result eligibility.

#### Block 2: WebSite (lines 110-117)
- **@context:** `https://schema.org` -- PASS
- **@type:** `WebSite` -- PASS

| Property | Status | Notes |
|----------|--------|-------|
| name | PASS | |
| url | PASS | |
| potentialAction (SearchAction) | MISSING | Recommended if site has search functionality |

**MISSING -- No BreadcrumbList on homepage.** Every other page has one. While optional for the homepage, including it provides consistency.

---

### 2. about.html

**Existing Schema Blocks:**

#### Block 1: BreadcrumbList (lines 22-30)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > About Us -- PASS
- **URLs:** Absolute -- PASS

**Issues Found:**

1. **MISSING -- No Organization/LocalBusiness reference.** The About page describes the company extensively but has no Organization schema. While the homepage carries the primary entity, an `@id` reference back to the Organization would strengthen entity association.

2. **MISSING -- No WebPage schema.** The About page is a strong candidate for `WebPage` with `@type: "AboutPage"` -- a specific Schema.org type designed for this purpose.

---

### 3. services.html

**Existing Schema Blocks:**

#### Block 1: Service array (lines 22-31)
Six `Service` objects in a JSON array.

| Service | serviceType | name | description | provider @id | areaServed |
|---------|-------------|------|-------------|--------------|------------|
| Emergency Roof Tarping | PASS | PASS | PASS | PASS | 19 states |
| Storm Damage Cleanup | PASS | PASS | PASS | PASS | 19 states |
| Property Board-Up | PASS | PASS | PASS | PASS | 19 states |
| Water Extraction | PASS | PASS | PASS | PASS | 19 states |
| Tree and Debris Removal | PASS | PASS | PASS | PASS | 19 states |
| Insurance Documentation | PASS | PASS | PASS | PASS | 19 states |

**Validation for each Service:**
- **@context:** `https://schema.org` -- PASS (present on each object in array)
- **@type:** `Service` -- PASS
- **provider @id reference:** `https://americandisastersolutions.com/#organization` -- PASS (correctly references homepage LocalBusiness)

**Issues Found:**

1. **WARNING -- Redundant @context in array.** Each Service object in the array repeats `"@context":"https://schema.org"`. While not technically invalid, when using a JSON array, the `@context` only needs to appear once or the array should be wrapped in a `@graph` structure.

2. **MISSING -- No `url` property on Service objects.** Each service should link to its canonical URL (even if they are all on `/services`, use anchor fragments like `https://americandisastersolutions.com/services#emergency-roof-tarping`).

3. **MISSING -- No `image` property on Service objects.** Each service card has an associated image in the HTML that should be referenced in the schema.

4. **MISSING -- No `offers` or `hasOfferCatalog`.** Optional but helpful for conveying that these services are available for purchase/booking.

#### Block 2: BreadcrumbList (lines 32-41)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > Services -- PASS
- **URLs:** Absolute -- PASS

---

### 4. contact.html

**Existing Schema Blocks:**

#### Block 1: FAQPage (lines 22-39)
- **@context:** `https://schema.org` -- PASS
- **@type:** `FAQPage` -- PASS
- **mainEntity:** 10 Question/Answer pairs -- PASS

| Property | Status | Notes |
|----------|--------|-------|
| mainEntity | PASS | Array of 10 Question objects |
| Each Question.name | PASS | Text strings present |
| Each Question.acceptedAnswer | PASS | Answer type with text |

**Issues Found:**

1. **INFO -- FAQPage on a commercial site.** Since August 2023, Google has restricted FAQ rich results to government and healthcare sites only. American Disaster Solutions is a commercial entity, so this FAQPage markup will NOT generate Google rich results. However, it is still beneficial for AI/LLM citation and discovery (ChatGPT, Perplexity, Gemini, etc.), so keeping it is recommended. This is not a critical issue.

2. **WARNING -- FAQPage is on the Contact page, not a dedicated FAQ page.** The FAQ content is rendered on `contact.html` but the FAQPage schema implies this IS the FAQ page. Consider whether a dedicated `/faq` page would better serve SEO.

#### Block 2: BreadcrumbList (lines 40-49)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > Contact -- PASS

**MISSING -- No ContactPage schema.** This is a prime candidate for `WebPage` with `@type: "ContactPage"`.

---

### 5. team.html

**Existing Schema Blocks:**

#### Block 1: BreadcrumbList (lines 22-31)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > Our Team -- PASS

**Issues Found:**

1. **MISSING -- No Person schema for team members.** The page features 5 named team members with roles, descriptions, and contact info. This is a major missed opportunity. Person schema with `worksFor` referencing the Organization would strengthen entity signals significantly.

2. **WARNING -- Team photo alt text swap.** The alt text for Amber Sewell's photo says `"Bonnie Roberts - Documentation & Claims"` and Bonnie Roberts' photo says `"Amber Sewell - Documentation & Claims"`. While not a schema issue per se, this indicates the photos may be swapped (line 116 and 129), which would propagate incorrect data if Person schema with images is added.

---

### 6. privacy.html

**Existing Schema Blocks:**

#### Block 1: BreadcrumbList (lines 22-31)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > Privacy Policy -- PASS

**Issues Found:**

1. **LOW PRIORITY -- No WebPage schema.** Could add `WebPage` type but this is low priority for a privacy policy page.

---

### 7. terms.html

**Existing Schema Blocks:**

#### Block 1: BreadcrumbList (lines 22-31)
- **@context:** `https://schema.org` -- PASS
- **@type:** `BreadcrumbList` -- PASS
- **Structure:** Home > Terms of Service -- PASS

**Issues Found:**

1. **LOW PRIORITY -- No WebPage schema.** Same as privacy page -- low priority.

---

## Cross-Page Consistency Check

| Check | Status | Notes |
|-------|--------|-------|
| Organization name consistent | PASS | "American Disaster Solutions" everywhere |
| Phone number consistent | PASS | (800) 513-5ADS / +18005135237 |
| Address consistent | PASS | 4033 County Road 392, Stephenville, TX 76401 |
| @id reference consistent | PASS | Services reference `/#organization` from homepage |
| BreadcrumbList format consistent | PASS | Same structure across all pages |
| Footer description consistency | WARNING | Homepage/services/contact footer says "Headquartered in Texas, deployed nationwide..." while team/privacy/terms footer says "Texas-based emergency tarping..." -- minor, not a schema issue but worth noting |
| Logo file consistency | FAIL | Schema `logo` uses `IMG_8259.webp` but actual logo across all pages is `ads-logo.png` |

---

## Missing Schema Opportunities (Prioritized)

### CRITICAL PRIORITY

**1. Homepage: Fix logo property**
The logo in LocalBusiness schema points to a photo, not the actual logo.

**2. Homepage: Add datePublished to Reviews**
Without `datePublished`, reviews are less likely to generate rich result stars.

### HIGH PRIORITY

**3. Team page: Add Person schema**
Five team members with names, roles, email, descriptions -- perfect for Person markup.

**4. About page: Add AboutPage schema**
Google recognizes the `AboutPage` WebPage type for entity understanding.

**5. Contact page: Add ContactPage schema**
Same benefit as above for contact page entity recognition.

**6. Homepage: Add sameAs for X/Twitter**

### MEDIUM PRIORITY

**7. Services page: Add image and url to Service objects**

**8. All pages: Add WebPage schema with mainEntity references**

**9. Homepage: Wrap Service schema in @graph instead of repeated @context**

### LOW PRIORITY

**10. Consider adding SiteNavigationElement schema**

**11. Privacy/Terms: Add WebPage schema (minimal SEO value)**

---

## Generated JSON-LD Fixes

### Fix 1: Homepage LocalBusiness -- Corrected logo + sameAs + review dates

Replace the existing LocalBusiness block in `index.html` (lines 22-108) with:

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "@id": "https://americandisastersolutions.com/#organization",
  "name": "American Disaster Solutions",
  "alternateName": "ADS",
  "description": "Headquartered in Texas, American Disaster Solutions provides nationwide catastrophe response, emergency tarping, and disaster cleanup services. Carrier-conscious operations with rapid deployment capability.",
  "url": "https://americandisastersolutions.com/",
  "telephone": "+18005135237",
  "email": "kyle@americandisastersolutions.com",
  "image": "https://americandisastersolutions.com/images/IMG_8259.webp",
  "logo": {
    "@type": "ImageObject",
    "url": "https://americandisastersolutions.com/images/ads-logo.png",
    "width": 512,
    "height": 512
  },
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "4033 County Road 392",
    "addressLocality": "Stephenville",
    "addressRegion": "TX",
    "postalCode": "76401",
    "addressCountry": "US"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 32.2207,
    "longitude": -98.2025
  },
  "areaServed": [
    {"@type": "State", "name": "Texas"},
    {"@type": "State", "name": "Louisiana"},
    {"@type": "State", "name": "Mississippi"},
    {"@type": "State", "name": "Alabama"},
    {"@type": "State", "name": "Florida"},
    {"@type": "State", "name": "Georgia"},
    {"@type": "State", "name": "South Carolina"},
    {"@type": "State", "name": "North Carolina"},
    {"@type": "State", "name": "Virginia"},
    {"@type": "State", "name": "Tennessee"},
    {"@type": "State", "name": "Arkansas"},
    {"@type": "State", "name": "Oklahoma"},
    {"@type": "State", "name": "Kansas"},
    {"@type": "State", "name": "Missouri"},
    {"@type": "State", "name": "Kentucky"},
    {"@type": "State", "name": "Indiana"},
    {"@type": "State", "name": "Illinois"},
    {"@type": "State", "name": "Ohio"},
    {"@type": "State", "name": "California"}
  ],
  "openingHoursSpecification": {
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"],
    "opens": "00:00",
    "closes": "23:59"
  },
  "priceRange": "$$",
  "sameAs": [
    "https://facebook.com/americandisastersolutions",
    "https://instagram.com/americandisastersolutions",
    "https://x.com/americandisaster"
  ],
  "founder": [
    {"@type": "Person", "name": "Josh Wilson"},
    {"@type": "Person", "name": "Kyle Sewell"}
  ],
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "5.0",
    "reviewCount": "3",
    "bestRating": "5",
    "worstRating": "1"
  },
  "review": [
    {
      "@type": "Review",
      "author": {"@type": "Person", "name": "Michael Rodriguez"},
      "datePublished": "2025-06-15",
      "reviewRating": {"@type": "Rating", "ratingValue": "5", "bestRating": "5"},
      "reviewBody": "After the tornado tore through our neighborhood, ADS had tarps on our roof within 3 hours of my call. They saved us from thousands in additional water damage."
    },
    {
      "@type": "Review",
      "author": {"@type": "Person", "name": "Sarah Livingston"},
      "datePublished": "2025-08-22",
      "reviewRating": {"@type": "Rating", "ratingValue": "5", "bestRating": "5"},
      "reviewBody": "We manage 40+ rental properties. When the hailstorm hit, ADS tarped all our damaged roofs in under 48 hours. Their coordination and professionalism is second to none."
    },
    {
      "@type": "Review",
      "author": {"@type": "Person", "name": "James Thompson"},
      "datePublished": "2025-10-03",
      "reviewRating": {"@type": "Rating", "ratingValue": "5", "bestRating": "5"},
      "reviewBody": "They handled the debris removal from a massive tree that fell on our building. Clean, efficient, and they even helped with the insurance paperwork."
    }
  ]
}
```

**NOTE:** The `datePublished` values above are placeholders. Replace them with the actual dates the reviews were received.


### Fix 2: About page -- Add AboutPage schema

Add this new `<script type="application/ld+json">` block to `about.html` `<head>`, alongside the existing BreadcrumbList:

```json
{
  "@context": "https://schema.org",
  "@type": "AboutPage",
  "name": "About American Disaster Solutions",
  "description": "American Disaster Solutions is headquartered in Texas but built to respond nationwide. Rapid, carrier-conscious temporary roofing for property owners and insurance partners.",
  "url": "https://americandisastersolutions.com/about",
  "mainEntity": {
    "@id": "https://americandisastersolutions.com/#organization"
  }
}
```


### Fix 3: Contact page -- Add ContactPage schema

Add this new `<script type="application/ld+json">` block to `contact.html` `<head>`:

```json
{
  "@context": "https://schema.org",
  "@type": "ContactPage",
  "name": "Contact American Disaster Solutions",
  "description": "Request emergency disaster service or book a consultation with American Disaster Solutions. 24/7 hotline: (800) 513-5ADS.",
  "url": "https://americandisastersolutions.com/contact",
  "mainEntity": {
    "@id": "https://americandisastersolutions.com/#organization"
  }
}
```


### Fix 4: Team page -- Add Person schema for all team members

Add this new `<script type="application/ld+json">` block to `team.html` `<head>`:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Person",
      "name": "Josh Wilson",
      "jobTitle": "CEO / Co-Founder",
      "description": "A bold leader with a vision to transform how America responds to natural disasters. With over two decades building and scaling companies in the restoration industry.",
      "email": "josh@americandisastersolutions.com",
      "image": "https://americandisastersolutions.com/team-photos/josh.jpg",
      "worksFor": {
        "@id": "https://americandisastersolutions.com/#organization"
      }
    },
    {
      "@type": "Person",
      "name": "Kyle Sewell",
      "jobTitle": "COO & Co-Founder",
      "description": "15+ years mobilizing and managing field teams for large-scale storm response, adhering to strict quality and safety standards.",
      "email": "kyle@americandisastersolutions.com",
      "image": "https://americandisastersolutions.com/team-photos/kyle.jpg",
      "worksFor": {
        "@id": "https://americandisastersolutions.com/#organization"
      }
    },
    {
      "@type": "Person",
      "name": "Zane Mason",
      "jobTitle": "President",
      "description": "Provides executive leadership and strategic direction for American Disaster Solutions. Oversees all company operations, growth initiatives, and ensures the highest standards of service delivery.",
      "email": "zane@americandisastersolutions.com",
      "image": "https://americandisastersolutions.com/team-photos/zane-hq.webp",
      "worksFor": {
        "@id": "https://americandisastersolutions.com/#organization"
      }
    },
    {
      "@type": "Person",
      "name": "Amber Sewell",
      "jobTitle": "Documentation & Claims",
      "description": "Oversees accurate and timely documentation of all work, providing insurance paperwork and claims handling to expedite the process for policyholders.",
      "email": "amber@americandisastersolutions.com",
      "image": "https://americandisastersolutions.com/team-photos/amber.jpg",
      "worksFor": {
        "@id": "https://americandisastersolutions.com/#organization"
      }
    },
    {
      "@type": "Person",
      "name": "Bonnie Roberts",
      "jobTitle": "Documentation & Claims",
      "description": "Meticulous attention to detail and understanding of insurance requirements helps expedite the claims process while ensuring full compliance.",
      "email": "bonnie@americandisastersolutions.com",
      "image": "https://americandisastersolutions.com/team-photos/bonnie.jpg",
      "worksFor": {
        "@id": "https://americandisastersolutions.com/#organization"
      }
    }
  ]
}
```

**IMPORTANT NOTE on team photo assignment:** In the HTML source, Amber Sewell's card (line 116) uses the image `bonnie.jpg` and Bonnie Roberts' card (line 129) uses `amber.jpg`. The alt text is also swapped. The Person schema above assumes the **file names match the person** (amber.jpg = Amber, bonnie.jpg = Bonnie). Verify the actual photos match the correct person and swap if needed.


### Fix 5: Services page -- Improved Service schema with @graph wrapper

Replace the existing Service array block in `services.html` (lines 22-31) with:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Service",
      "serviceType": "Emergency Roof Tarping",
      "name": "Emergency Roof Tarping",
      "description": "Rapid roof tarping with commercial-grade UV-resistant tarps using non-invasive sandbag and invasive naildown methods. Sub-4-hour response.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/2022-10-17-12-30-56-408.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    },
    {
      "@type": "Service",
      "serviceType": "Storm Damage Cleanup",
      "name": "Disaster Cleanup",
      "description": "Full-scale debris removal, hazardous material handling, and site clearing for residential and commercial properties after storms.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/2022-11-14-11-46-20-285.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    },
    {
      "@type": "Service",
      "serviceType": "Property Board-Up",
      "name": "Board-Up & Securing",
      "description": "Secure damaged structures against weather, vandalism, and unauthorized entry with reinforced materials.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/2022-11-19-14-58-13-444.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    },
    {
      "@type": "Service",
      "serviceType": "Water Extraction",
      "name": "Water Extraction & Drying",
      "description": "Industrial-grade water removal, structural drying, dehumidification, and mold prevention for flooded properties.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/2022-11-19-14-57-06-177.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    },
    {
      "@type": "Service",
      "serviceType": "Tree and Debris Removal",
      "name": "Tree & Debris Removal",
      "description": "Safe removal of fallen trees, construction debris, and storm-generated waste for residential and commercial properties.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/2022-10-06-17-58-07-021.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    },
    {
      "@type": "Service",
      "serviceType": "Insurance Documentation",
      "name": "Insurance Documentation",
      "description": "Detailed photo documentation, damage assessments, and reports to streamline insurance claims. Direct coordination with adjusters.",
      "url": "https://americandisastersolutions.com/services",
      "image": "https://americandisastersolutions.com/images/IMG_8258.webp",
      "provider": {"@id": "https://americandisastersolutions.com/#organization"},
      "areaServed": {"@type": "Country", "name": "United States"}
    }
  ]
}
```

**Changes from original:**
- Wrapped in `@graph` with single `@context` (cleaner, no redundancy)
- Added `url` to each Service
- Added `image` to each Service (matching the HTML card images)
- Simplified `areaServed` to `Country: United States` (since they serve 19+ states, this is cleaner; the full state list is already on the LocalBusiness)


---

## Non-Schema HTML Issue Detected

**Team page photo/alt text swap (team.html):**
- Line 116: `<img src="/team-photos/bonnie.jpg" alt="Amber Sewell - Documentation & Claims">` -- The `src` says `bonnie.jpg` but the alt says Amber Sewell
- Line 129: `<img src="/team-photos/amber.jpg" alt="Bonnie Roberts - Documentation & Claims">` -- The `src` says `amber.jpg` but the alt says Bonnie Roberts

Either the file names or the alt text are swapped. This should be corrected before adding Person schema with image URLs.

---

## Summary of All Issues

| # | Page | Severity | Issue |
|---|------|----------|-------|
| 1 | index.html | WARNING | `logo` property uses a photo (`IMG_8259.webp`) instead of actual logo (`ads-logo.png`) |
| 2 | index.html | WARNING | `sameAs` missing X/Twitter profile URL |
| 3 | index.html | WARNING | Reviews missing `datePublished` property |
| 4 | index.html | INFO | No `foundingDate` on LocalBusiness |
| 5 | about.html | HIGH | No AboutPage schema -- missed opportunity for entity recognition |
| 6 | about.html | INFO | No Organization reference via @id |
| 7 | services.html | WARNING | Redundant `@context` in JSON array (use `@graph` instead) |
| 8 | services.html | MEDIUM | Service objects missing `url` and `image` properties |
| 9 | contact.html | INFO | FAQPage will not generate Google rich results (commercial site) -- still useful for AI/LLM |
| 10 | contact.html | MEDIUM | No ContactPage schema |
| 11 | team.html | HIGH | No Person schema for 5 named team members |
| 12 | team.html | WARNING | Photo/alt text swap between Amber Sewell and Bonnie Roberts |
| 13 | privacy.html | LOW | No WebPage schema (low priority) |
| 14 | terms.html | LOW | No WebPage schema (low priority) |
| 15 | index.html | LOW | No BreadcrumbList (all other pages have one) |

---

## Implementation Priority

1. **Immediate** -- Fix logo property in LocalBusiness (index.html)
2. **Immediate** -- Add datePublished to Review objects (index.html)
3. **Immediate** -- Add missing X/Twitter to sameAs (index.html)
4. **This week** -- Add Person schema to team.html (after verifying photo swap)
5. **This week** -- Fix photo/alt text swap on team.html
6. **This week** -- Add AboutPage schema to about.html
7. **This week** -- Add ContactPage schema to contact.html
8. **Next sprint** -- Refactor Service array to use @graph wrapper with url/image
9. **Low priority** -- Add WebPage schema to privacy.html and terms.html
