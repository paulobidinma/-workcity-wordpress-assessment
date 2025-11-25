# Workcity — Knowledge Panel strategy

This document explains how Workcity can trigger or strengthen a Google Knowledge Panel (KP) for the brand and its owned entities. It focuses on the practical, high-impact steps: building a robust entity profile, required structured data (schema), consistent brand signals, press & authority signals, and the ideal `About` page hierarchy.

---

## How Google decides to show a Knowledge Panel (brief)

- Google uses a network of corroborated, structured signals (Knowledge Graph data sources, authoritative websites, structured data, public records, and high-quality media coverage) to identify a distinct entity. When Google has enough high-confidence signals for an entity (and user intent supports it), it may display a Knowledge Panel.
- The KP is not a manual product you 'apply' for — you build the entity and a reliable trail of signals that let Google match queries to the entity.

---

## 1) How Workcity can trigger or strengthen a Knowledge Panel ✅

1. Establish canonical authoritative sources for the Brand entity:
   - Create / confirm an entry in Wikidata and ensure it references official website, social profiles, and public registrations.
   - Ensure the official website, About page, and Press pages clearly declare legal full name, business type, founding date, addresses, and official logos.

2. Structured data across the site (and key pages):
   - Add Organization, LocalBusiness (if applicable), and WebSite schema with consistent identifiers (url, sameAs links, logo, contactPoint).
   - Use `sameAs` for verified social profiles, Wikipedia (if available), LinkedIn company page, Crunchbase, and any official registry.

3. High-quality, authoritative citations:
   - Secure mentions and profiles in high-authority places (Wikipedia, Wikidata, major press, trade publications, government registries).
   - Publish byline or contributed pieces with author biography linking back to the brand entity.

4. Consistency and canonicalization:
   - Ensure canonical URLs, HTTPS, and consistent domain/subdomain usage. Remove duplicate or conflicting canonical signals.

5. Public records and registry listings:
   - Use business registries, trademark records, and official directories where possible — Google uses these as corroboration.

6. Maintain ownership signals in Google accounts:
   - Verify ownership of Google My Business/Business Profile (if the brand has physical presence) and claim Knowledge Graph features where applicable.

7. Local & product/people sub-entities:
   - If you want panels for sub-entities (locations, founders, key products), treat each as its own entity and repeat the above pattern.

Priority: get Wikidata/Wikipedia (if appropriate), consistent `sameAs` links, and Organization schema in place before chasing press/coverage. These yield the highest leverage.

---

## 2) Entity-building steps (practical checklist) 🧭

1. Audit existing references
   - Search the web for the brand name, variations and check existing Knowledge Graph entries, Wikipedia, Wikidata, and directory profiles.

2. Create or improve a Wikidata entry
   - Provide authoritative references for every statement, include official URL, logo, headquarters, inception date, and notable people.

3. (When applicable) Create a neutral, well-sourced Wikipedia page
   - Follow Wikipedia notability rules — use third-party reliable sources; avoid PR-style language.

4. Publish canonical About & Contact pages
   - These are primary sources Google uses for entity facts — make them authoritative, factual, and structured.

5. Add & validate structured data (schema.org)
   - Organization + logo + sameAs + contactPoint at site root.
   - For local offices: LocalBusiness with address and opening hours.

6. Create profiles on authoritative external services
   - LinkedIn (company), Crunchbase, government registries, industry associations.

7. Build press & media presence
   - Earn consistent coverage on recognized publishers; prioritize coverage that includes entity name, description and links to the official site.

8. Monitor & iterate
   - Use Search Console, Crawl logs, and Knowledge Graph explorers to confirm signals are recognized.

---

## 3) Schema requirements — what to add (examples) 🔧

At minimum, add machine-readable schema for the Brand and key people/locations. Use JSON-LD embedded in the <head> or just before </body>.

Example: Organization JSON-LD (core fields)

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Workcity",
  "url": "https://workcity.example",
  "logo": "https://workcity.example/assets/logo.png",
  "sameAs": [
    "https://twitter.com/workcity",
    "https://www.linkedin.com/company/workcity",
    "https://www.wikidata.org/entity/Q12345"
  ],
  "contactPoint": [{
    "@type": "ContactPoint",
    "telephone": "+1-555-555-5555",
    "contactType": "customer service",
    "areaServed": "US"
  }]
}
```

Also consider:
- Person schema for founders/key executives (include sameAs links to person pages, LinkedIn, and Wikidata/QID if present).
- LocalBusiness schema for offices with structured address, geo coordinates and opening hours.
- WebSite schema + potentialAction SearchAction for site search/autocomplete.

Technical notes:
- Use canonical URLs (no redirects) inside schema values.
- Validate with Google Rich Results and Schema.org validators and re-run the URL Inspection test in Search Console.

---

## 4) Brand identity consistency signals (what Google looks for) 🎯

Google infers entity confidence from consistent facts repeated across independent, authoritative sources.

Key signals to align:

- Name consistency: official full legal name + brand short name variants used consistently across site and profiles.
- Logo and images: stable, high-quality logo in site root and in structured data.
- Canonical site & home page: clearly show official brand identity (legal address, headquarters, or registered country).
- SameAs network: social profiles, directory listings, Wikidata/QID and Wikipedia link back to the canonical site.
- Structured pages for people/products/locations: separate pages with consistent canonicalization and schema.
- Ownership signals: press releases, authorship bios, domain verification with Google-owned properties.

Small inconsistencies (different legal names, multiple public registries listing slightly different names or addresses, mismatched logos) lower entity confidence.

---

## 5) Press & authority signals (how to get them and why they matter) 📰

Why they matter:
- High-quality, independent references are crucial to show that the entity is notable and that sources corroborate its facts. Google heavily weights reputable publishers, government registries, and encyclopedic sources.

Actionable ways to build authority:

1. Earn coverage on top-tier & industry publications — interview features, case studies, product reviews.
2. Submit factual listings to business registries, industry bodies and trade registries.
3. Use press pages on the website with canonical press releases and source links (with explicit dates and citations).
4. Encourage journalists to include canonical links to the brand site when covering Workcity.
5. Secure third-party profiles and directories (Crunchbase, Glassdoor, LinkedIn company page, local government business registry).

Signals that help KPs:
- Publications that use the brand name in titles, open summaries that mention key facts (founding year, HQ, notable people), and link to the official site.
- Structured mentions (e.g., author bylines linking to person pages with Person schema) help associate people with the brand.

Note: Artificially created or low-quality press mentions (spammy links, low-authority outlets) do not help and can confuse entity signals.

---

## 6) About page hierarchy — a single authoritative source example 🏛️

Your About page is the primary canonical source for entity facts. Use a clear hierarchy so Google and downstream data consumers can reliably extract facts.

Recommended structure (order matters):

1. Page title and H1 — brand full legal name (short brand name in H2 if needed)
2. Short descriptive meta description and an opening 1–2 sentence description (who you are, what you do, where you operate)
3. Quick facts / At-a-glance (structured block):
   - Founded: YYYY
   - Headquarters: City, Country
   - Legal entity type: e.g., Private Company
   - Website: canonical URL
   - Logo: visible and meta-linked (JSON-LD)
4. Notable people — short bios with Person schema and links to full profile pages for each
5. Contact and official channels — contactPoint, media/press email and links to verified social profiles
6. Press & awards — highlights and links to authoritative coverage
7. Legal / registrations — company registration numbers, trademarks, regulators (if relevant)
8. Links to policies (privacy, terms) and location pages (LocalBusiness schema for offices)

Design tips:
- Keep facts machine-readable: use definition lists or short key/value blocks that are easy to scrape.
- Avoid marketing puffery; use neutral, factual language for entity facts (for better use in Knowledge Graph). Reserve storytelling lower on the page.

---

## Final checklist — fast implementation (first 30 days)

- [ ] Create or update Wikidata entry (references + official site link)
- [ ] Add Organization JSON-LD on homepage and About page; include `sameAs` links
- [ ] Publish structured, neutral About page using recommended hierarchy
- [ ] Claim and verify Google Business Profile if applicable; ensure NAP consistency
- [ ] Identify top 3 authoritative publications to target for coverage and outreach
- [ ] Update LinkedIn, Crunchbase, industry directories and register in public registries
- [ ] Monitor Search Console, Knowledge Graph explorers and Wikidata for updates

---

If you'd like I can now:

- convert this into a one-page checklist PDF the team can hand to dev and comms, or
- produce a starter JSON-LD snippet and About page HTML template tailored to Workcity (provide domain and key facts and I’ll generate it).
