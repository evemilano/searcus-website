# Homepage EN — Searcus Swiss SAGL (Lugano)

| Campo | Valore |
|-------|--------|
| Template ID | homepage |
| URL pattern | https://searcus.ch/en/ |
| Input file | Searcus Swiss SAGL — Technical SEO, International SEO & PPC Consulting, Lugano.html |
| Tag globale | P0 |

## Stato attuale

| @type trovato | Posizione | Stato |
|---------------|-----------|-------|
| (nessuno) | — | MISSING |
| Organization | — | MISSING |
| LocalBusiness | — | MISSING |
| Person (founder) | — | MISSING |
| OfferCatalog | — | MISSING |
| Service (×11) | — | MISSING |
| ItemList (clients) | — | MISSING |
| WebSite | — | MISSING |
| WebPage | — | MISSING |

L'HTML in input non contiene alcun blocco `<script type="application/ld+json">` (verificato da `preprocess.py`: `jsonld=0`).

## Task list

| # | Tag | Azione | Target | Note |
|---|-----|--------|--------|------|
| 1 | P0 | ADD `@graph` unico in `<head>` | layout globale EN | Mirror IT con override per WebPage e Service.description |
| 2 | P0 | RIUSO `@id` Organization, Person, OfferCatalog, ItemList, WebSite | grafo condiviso | I `@id` sono cross-language: una sola identità per il dominio |
| 3 | P0 | ADD `WebPage` EN | `@id` https://searcus.ch/en/#webpage | `inLanguage: "en"` |
| 4 | P0 | TRADURRE `Service.description` IT → EN | dentro OfferCatalog | Per visibilità SERP EN |
| 5 | P0 | TRADURRE `Organization.description` e `slogan` | dentro Organization | Coerenza con lingua pagina |
| 6 | P0 | ADD `significantLink[]` con ancore EN | dentro WebPage | #services, #clients, #about, #contact |
| 7 | P1 | ADD `speakable` con selettori sezioni EN | dentro WebPage | Selettori CSS aggiornati su navbar inglese |
| 8 | P1 | MANTENERE `areaServed[]` con label EN | dentro Organization | Country `name: "Switzerland"` ecc. (già in EN nel master) |
| 9 | P1 | MANTENERE `knowsAbout[]`, `knowsLanguage[]`, `sameAs[]` invariati | dentro Organization/Person | Entità Wikidata + social non cambiano per lingua |
| 10 | P1 | MANTENERE `ItemList` clienti identica | grafo condiviso | I nomi brand non si traducono |
| 11 | P2 | OMIT `BreadcrumbList`, `SearchAction` | come per IT | Confermato skip |
| 12 | P2 | NOTE implementativa | layout BE | In produzione, un layer globale può iniettare il JSON-LD una sola volta e variare solo `WebPage` + traduzione `description` campi |

## JSON-LD finale

Da iniettare in `<head>` della pagina EN come **singolo** `<script type="application/ld+json">`:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": ["Organization", "LocalBusiness"],
      "@id": "https://searcus.ch/#organization",
      "name": "Searcus Swiss SAGL",
      "legalName": "Searcus Swiss SAGL",
      "alternateName": "Searcus",
      "description": "Technical SEO, International SEO, PPC and AI development consulting agency. Founded in 2010 in Lugano, Switzerland. Enterprise clients across Switzerland, Italy, Denmark, UK, Germany and the rest of Europe.",
      "slogan": "We reverse-engineer how Google sees your site.",
      "url": "https://searcus.ch/",
      "logo": {
        "@type": "ImageObject",
        "@id": "https://searcus.ch/#logo",
        "url": "https://searcus.ch/assets/images/logo.png",
        "contentUrl": "https://searcus.ch/assets/images/logo.png",
        "width": 1024,
        "height": 1024,
        "caption": "Searcus Swiss SAGL"
      },
      "image": { "@id": "https://searcus.ch/#logo" },
      "foundingDate": "2010-01-01",
      "foundingLocation": {
        "@type": "Place",
        "name": "Lugano, Switzerland",
        "sameAs": "https://www.wikidata.org/wiki/Q5887"
      },
      "founder": { "@id": "https://searcus.ch/#person" },
      "employee": [{ "@id": "https://searcus.ch/#person" }],
      "numberOfEmployees": { "@type": "QuantitativeValue", "value": 3 },
      "vatID": "CHE-180.818.315",
      "taxID": "CHE-180.818.315",
      "identifier": {
        "@type": "PropertyValue",
        "propertyID": "UID",
        "name": "Swiss UID number",
        "value": "CHE-180.818.315"
      },
      "priceRange": "€€€",
      "currenciesAccepted": "CHF, EUR",
      "paymentAccepted": "Cash, Credit Card, Bank Transfer",
      "openingHours": "Mo-Fr 09:00-18:00",
      "openingHoursSpecification": [
        {
          "@type": "OpeningHoursSpecification",
          "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
          "opens": "09:00",
          "closes": "18:00"
        }
      ],
      "address": [
        {
          "@type": "PostalAddress",
          "name": "Registered office",
          "streetAddress": "Via dei Faggi, 4V",
          "addressLocality": "Pazzallo",
          "addressRegion": "TI",
          "postalCode": "6912",
          "addressCountry": "CH"
        },
        {
          "@type": "PostalAddress",
          "name": "Operational office",
          "streetAddress": "Via Penate, 16",
          "addressLocality": "Mendrisio",
          "addressRegion": "TI",
          "postalCode": "6850",
          "addressCountry": "CH"
        }
      ],
      "geo": {
        "@type": "GeoCoordinates",
        "latitude": 45.971,
        "longitude": 8.9485
      },
      "hasMap": "https://maps.google.com/?q=Via+dei+Faggi+4V,+Pazzallo,+6912+Lugano,+Switzerland",
      "email": "giovanni@searcus.ch",
      "telephone": "+41798643035",
      "contactPoint": [
        {
          "@type": "ContactPoint",
          "contactType": "Customer support",
          "telephone": "+41798643035",
          "email": "giovanni@searcus.ch",
          "areaServed": "CH",
          "availableLanguage": ["English", "Italian"]
        },
        {
          "@type": "ContactPoint",
          "contactType": "Customer support",
          "telephone": "+393393668879",
          "areaServed": "IT",
          "availableLanguage": ["Italian", "English"]
        },
        {
          "@type": "ContactPoint",
          "contactType": "Sales",
          "email": "giovanni@searcus.ch",
          "availableLanguage": ["English", "Italian"]
        }
      ],
      "areaServed": [
        { "@type": "Country", "name": "Switzerland", "sameAs": "https://www.wikidata.org/wiki/Q39" },
        { "@type": "Country", "name": "Italy", "sameAs": "https://www.wikidata.org/wiki/Q38" },
        { "@type": "Country", "name": "Denmark", "sameAs": "https://www.wikidata.org/wiki/Q35" },
        { "@type": "Country", "name": "United Kingdom", "sameAs": "https://www.wikidata.org/wiki/Q145" },
        { "@type": "Country", "name": "Germany", "sameAs": "https://www.wikidata.org/wiki/Q183" },
        { "@type": "Place", "name": "Europe", "sameAs": "https://www.wikidata.org/wiki/Q46" }
      ],
      "knowsAbout": [
        { "@type": "Thing", "name": "Search Engine Optimization", "sameAs": "https://www.wikidata.org/wiki/Q180711" },
        { "@type": "Thing", "name": "Technical SEO" },
        { "@type": "Thing", "name": "International SEO" },
        { "@type": "Thing", "name": "Core Web Vitals" },
        { "@type": "Thing", "name": "Search Engine Marketing", "sameAs": "https://www.wikidata.org/wiki/Q1369773" },
        { "@type": "Thing", "name": "Google Ads", "sameAs": "https://www.wikidata.org/wiki/Q4233718" },
        { "@type": "Thing", "name": "Pay-per-click", "sameAs": "https://www.wikidata.org/wiki/Q1762621" },
        { "@type": "Thing", "name": "Reddit", "sameAs": "https://www.wikidata.org/wiki/Q1136" },
        { "@type": "Thing", "name": "Artificial Intelligence", "sameAs": "https://www.wikidata.org/wiki/Q11660" },
        { "@type": "Thing", "name": "Large Language Model", "sameAs": "https://www.wikidata.org/wiki/Q115305900" },
        { "@type": "Thing", "name": "Retrieval-Augmented Generation" },
        { "@type": "Thing", "name": "AI Agents" },
        { "@type": "Thing", "name": "Python", "sameAs": "https://www.wikidata.org/wiki/Q28865" },
        { "@type": "Thing", "name": "Server log analysis" }
      ],
      "knowsLanguage": [
        { "@type": "Language", "name": "English", "alternateName": "en" },
        { "@type": "Language", "name": "Italian", "alternateName": "it" }
      ],
      "hasCertification": [
        {
          "@type": "Certification",
          "name": "Google Partner",
          "issuedBy": { "@type": "Organization", "name": "Google" },
          "validFrom": "2012-01-01"
        },
        {
          "@type": "Certification",
          "name": "SISTRIX Partner",
          "issuedBy": { "@type": "Organization", "name": "SISTRIX" },
          "validFrom": "2018-01-01"
        }
      ],
      "award": [
        "Google Partner since 2012",
        "SISTRIX Partner since 2018",
        "Zero Google penalties since 2010"
      ],
      "keywords": [
        "Technical SEO agency",
        "International SEO agency",
        "Google Ads agency",
        "PPC agency",
        "AI development agency",
        "SEO consulting Lugano",
        "Enterprise SEO",
        "Reddit Ads",
        "LLM integration"
      ],
      "brand": { "@type": "Brand", "name": "Searcus", "url": "https://searcus.ch/" },
      "hasOfferCatalog": { "@id": "https://searcus.ch/#services" },
      "subjectOf": { "@id": "https://searcus.ch/#clients" },
      "sameAs": [
        "https://www.linkedin.com/in/giovannisacheli/",
        "https://github.com/evemilano",
        "https://x.com/EVEMilano",
        "https://www.youtube.com/@EvemilanoSEO"
      ],
      "publicAccess": true
    },

    {
      "@type": "Person",
      "@id": "https://searcus.ch/#person",
      "name": "Giovanni Sacheli",
      "givenName": "Giovanni",
      "familyName": "Sacheli",
      "jobTitle": "Founder, Senior Technical SEO & PPC Consultant",
      "description": "Technical SEO, Google Ads and AI development consultant. Founder of Searcus Swiss SAGL in 2010.",
      "url": "https://searcus.ch/#person",
      "email": "giovanni@searcus.ch",
      "telephone": "+41798643035",
      "gender": { "@type": "GenderType", "name": "Male" },
      "image": "https://searcus.ch/assets/images/20140305-Giovanni-Sacheli-5.jpg",
      "nationality": { "@type": "Country", "name": "Italy", "sameAs": "https://www.wikidata.org/wiki/Q38" },
      "homeLocation": {
        "@type": "Place",
        "name": "Lugano",
        "sameAs": "https://www.wikidata.org/wiki/Q5887"
      },
      "alumniOf": {
        "@type": "EducationalOrganization",
        "name": "Bocconi University",
        "sameAs": "https://www.wikidata.org/wiki/Q777582"
      },
      "worksFor": { "@id": "https://searcus.ch/#organization" },
      "knowsLanguage": [
        { "@type": "Language", "name": "English", "alternateName": "en" },
        { "@type": "Language", "name": "Italian", "alternateName": "it" }
      ],
      "knowsAbout": [
        { "@type": "Thing", "name": "Technical SEO" },
        { "@type": "Thing", "name": "International SEO" },
        { "@type": "Thing", "name": "Core Web Vitals" },
        { "@type": "Thing", "name": "Google Ads", "sameAs": "https://www.wikidata.org/wiki/Q4233718" },
        { "@type": "Thing", "name": "Reddit Ads" },
        { "@type": "Thing", "name": "Artificial Intelligence", "sameAs": "https://www.wikidata.org/wiki/Q11660" },
        { "@type": "Thing", "name": "Large Language Model", "sameAs": "https://www.wikidata.org/wiki/Q115305900" },
        { "@type": "Thing", "name": "Retrieval-Augmented Generation" },
        { "@type": "Thing", "name": "AI Agents" },
        { "@type": "Thing", "name": "Python", "sameAs": "https://www.wikidata.org/wiki/Q28865" },
        { "@type": "Thing", "name": "Server log analysis" }
      ],
      "hasOccupation": {
        "@type": "Occupation",
        "name": "SEO and AI Consultant",
        "occupationLocation": { "@type": "City", "name": "Lugano" },
        "skills": ["Technical SEO", "PPC", "Python", "LLM Integration"]
      },
      "sameAs": [
        "https://www.evemilano.com/about-me/",
        "https://www.linkedin.com/in/giovannisacheli/",
        "https://www.youtube.com/@EvemilanoSEO",
        "https://github.com/evemilano",
        "https://x.com/EVEMilano",
        "https://www.slideshare.net/giovannisacheli",
        "https://www.amazon.com/stores/author/B082SXP7LR",
        "https://www.udemy.com/user/giovanni-sacheli/",
        "https://www.sistrix.it/esperti/giovanni-sacheli/",
        "https://www.smau.it/relatori/giovanni.sacheli",
        "https://seoblog.giorgiotave.it/author/giovanni",
        "https://www.semrush.com/blog/user/146366177/"
      ]
    },

    {
      "@type": "OfferCatalog",
      "@id": "https://searcus.ch/#services",
      "name": "Searcus Swiss services",
      "description": "Catalog of Technical SEO, International SEO, PPC and AI development consulting services.",
      "numberOfItems": 11,
      "itemListOrder": "https://schema.org/ItemListUnordered",
      "itemListElement": [
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-technical-seo",
          "name": "Technical SEO",
          "serviceType": "Technical SEO",
          "description": "In-depth audits on crawling, rendering and indexing. Log file analysis, Core Web Vitals optimisation, structured data, JavaScript SEO and migrations. We work directly with your engineering team.",
          "category": ["crawling", "rendering", "indexing", "log analysis", "Core Web Vitals", "JS SEO", "migrations"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "serviceLocation": { "@type": "Place", "name": "Lugano, Switzerland" },
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-international-seo",
          "name": "International SEO",
          "serviceType": "International SEO",
          "description": "Hreflang architecture, ccTLD/subfolder/subdomain strategy, geo-targeting, multilingual keyword research and localised content strategies.",
          "category": ["hreflang", "geo-targeting", "multilingual", "ccTLD", "subfolder", "international keyword research"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ppc",
          "name": "PPC Advertising",
          "serviceType": "Pay-per-click advertising",
          "description": "Google Ads management (Search, Shopping, Display, YouTube, Performance Max) and Reddit Ads. Conversion tracking, feed optimisation, advanced bidding strategies.",
          "category": ["Google Ads", "Reddit Ads", "Performance Max", "Search Ads", "Shopping Ads", "Display Ads", "YouTube Ads", "conversion tracking"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-formazione",
          "name": "Professional training",
          "serviceType": "Professional training",
          "description": "Technical SEO, Google Ads, Google Search Console and web analytics courses. Private or in-house workshops, from fundamentals to advanced level. On-site or remote.",
          "category": ["SEO courses", "Google Ads courses", "in-house workshops", "remote training"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Professionals and teams" },
          "availableChannel": [
            {
              "@type": "ServiceChannel",
              "name": "On-site",
              "serviceLocation": { "@type": "Place", "name": "Lugano, Switzerland" },
              "availableLanguage": ["English", "Italian"]
            },
            {
              "@type": "ServiceChannel",
              "name": "Remote",
              "serviceUrl": "https://searcus.ch/en/#services",
              "availableLanguage": ["English", "Italian"]
            }
          ]
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-seo-manager",
          "name": "SEO Manager",
          "serviceType": "Fractional SEO management",
          "description": "Strategic orchestration of digital visibility for businesses. Monthly calls, data-driven initiatives, coordination with in-house copywriters and developers.",
          "category": ["enterprise SEO", "strategy", "coordination", "fractional SEO", "SEO management"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-competitive-intelligence",
          "name": "SEO Competitive Intelligence",
          "serviceType": "Competitive intelligence and SEO gap analysis",
          "description": "Systematic competitor SEO analysis: keyword portfolio mapping, crawl comparison, SERP share modelling on priority clusters, backlink gap audit. Output: an actionable opportunity matrix.",
          "category": ["keyword gap analysis", "SERP share modelling", "backlink gap", "crawl comparison", "competitor SEO audit", "opportunity matrix"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-llm-integration",
          "name": "LLM Integration",
          "serviceType": "Custom AI software development — Large Language Model integration",
          "description": "Integration of Large Language Models (Claude, GPT, Llama, Gemini) into product workflows: chat assistants, classification, semantic extraction, content generation with guardrails.",
          "category": ["LLM", "GPT", "Claude", "Llama", "Gemini", "AI integration", "prompt engineering", "guardrails", "function calling"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "isRelatedTo": [
            { "@id": "https://searcus.ch/#service-ai-agents" },
            { "@id": "https://searcus.ch/#service-rag-pipelines" }
          ],
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ai-agents",
          "name": "AI Agents",
          "serviceType": "Agentic AI software development",
          "description": "Development of AI agents to automate business processes: research agents, classifiers, SEO analysis agents, multi-tool MCP integrations, sub-agent orchestration.",
          "category": ["agentic AI", "MCP", "multi-agent", "tool use", "task automation", "research agents", "ReAct"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "isRelatedTo": [
            { "@id": "https://searcus.ch/#service-llm-integration" },
            { "@id": "https://searcus.ch/#service-ai-automation" }
          ],
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-rag-pipelines",
          "name": "RAG Pipelines",
          "serviceType": "Retrieval-Augmented Generation pipelines",
          "description": "RAG pipeline architecture: ingestion, chunking, embedding, vector database, retrieval, re-ranking, grounding with citations. Use cases: knowledge base, customer support, internal semantic search.",
          "category": ["RAG", "embedding", "vector database", "chunking", "re-ranking", "semantic search", "knowledge base", "grounding"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "isRelatedTo": [
            { "@id": "https://searcus.ch/#service-llm-integration" }
          ],
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ai-automation",
          "name": "AI Automation",
          "serviceType": "AI-driven workflow automation",
          "description": "Automation of repetitive processes through AI: email triage, ticket classification, SEO report generation, SERP monitoring, content briefing. Integration with existing stacks (n8n, Make, custom Python).",
          "category": ["AI automation", "workflow automation", "n8n", "Make", "Python automation", "SEO automation", "report automation"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "isRelatedTo": [
            { "@id": "https://searcus.ch/#service-ai-agents" },
            { "@id": "https://searcus.ch/#service-custom-ai-software" }
          ],
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-custom-ai-software",
          "name": "Custom AI Software",
          "serviceType": "Custom AI software development",
          "description": "Custom AI software development in Python: internal tools, data-driven dashboards, dataset pipelines, fine-tuning, API integrations. End-to-end from requirement gathering to deployment.",
          "category": ["custom software", "Python", "data pipelines", "API integration", "dashboard", "fine-tuning", "MLOps"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "isRelatedTo": [
            { "@id": "https://searcus.ch/#service-ai-automation" }
          ],
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/en/#services",
            "availableLanguage": ["English", "Italian"]
          }
        }
      ]
    },

    {
      "@type": "ItemList",
      "@id": "https://searcus.ch/#clients",
      "name": "Searcus Swiss enterprise clients",
      "description": "Selection of enterprise clients served by Searcus Swiss SAGL since 2010: international brands in pharma, banking, fashion, publishing, hospitality and e-commerce.",
      "numberOfItems": 28,
      "itemListOrder": "https://schema.org/ItemListUnordered",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "item": { "@type": "Organization", "name": "Bayer", "sameAs": "https://www.wikidata.org/wiki/Q152051" } },
        { "@type": "ListItem", "position": 2, "item": { "@type": "Organization", "name": "Wolters Kluwer", "sameAs": "https://www.wikidata.org/wiki/Q1990413" } },
        { "@type": "ListItem", "position": 3, "item": { "@type": "Organization", "name": "Ermenegildo Zegna", "sameAs": "https://www.wikidata.org/wiki/Q683036" } },
        { "@type": "ListItem", "position": 4, "item": { "@type": "Organization", "name": "Würth", "sameAs": "https://www.wikidata.org/wiki/Q706713" } },
        { "@type": "ListItem", "position": 5, "item": { "@type": "Organization", "name": "EFG International", "sameAs": "https://www.wikidata.org/wiki/Q5320560" } },
        { "@type": "ListItem", "position": 6, "item": { "@type": "Organization", "name": "BSI Bank", "sameAs": "https://www.wikidata.org/wiki/Q794594" } },
        { "@type": "ListItem", "position": 7, "item": { "@type": "Organization", "name": "Wyndham Hotels & Resorts", "sameAs": "https://www.wikidata.org/wiki/Q2780585" } },
        { "@type": "ListItem", "position": 8, "item": { "@type": "Organization", "name": "Moleskine", "sameAs": "https://www.wikidata.org/wiki/Q1539436" } },
        { "@type": "ListItem", "position": 9, "item": { "@type": "Organization", "name": "IBSA Swiss" } },
        { "@type": "ListItem", "position": 10, "item": { "@type": "Organization", "name": "We Are Social", "sameAs": "https://www.wikidata.org/wiki/Q108149146" } },
        { "@type": "ListItem", "position": 11, "item": { "@type": "Organization", "name": "Lacertosus" } },
        { "@type": "ListItem", "position": 12, "item": { "@type": "Organization", "name": "Consulcesi" } },
        { "@type": "ListItem", "position": 13, "item": { "@type": "Organization", "name": "Farmy.ch" } },
        { "@type": "ListItem", "position": 14, "item": { "@type": "Organization", "name": "TryHackMe" } },
        { "@type": "ListItem", "position": 15, "item": { "@type": "Organization", "name": "Engineering Ingegneria Informatica", "sameAs": "https://www.wikidata.org/wiki/Q3722810" } },
        { "@type": "ListItem", "position": 16, "item": { "@type": "Organization", "name": "La Martina" } },
        { "@type": "ListItem", "position": 17, "item": { "@type": "Organization", "name": "TIM WCAP" } },
        { "@type": "ListItem", "position": 18, "item": { "@type": "Organization", "name": "The Bridge Firenze" } },
        { "@type": "ListItem", "position": 19, "item": { "@type": "Organization", "name": "Tigros", "sameAs": "https://www.wikidata.org/wiki/Q3995215" } },
        { "@type": "ListItem", "position": 20, "item": { "@type": "Organization", "name": "Tinext" } },
        { "@type": "ListItem", "position": 21, "item": { "@type": "Organization", "name": "HG Pooled Management" } },
        { "@type": "ListItem", "position": 22, "item": { "@type": "Organization", "name": "Angel Aligner" } },
        { "@type": "ListItem", "position": 23, "item": { "@type": "Organization", "name": "Aqseptence Group" } },
        { "@type": "ListItem", "position": 24, "item": { "@type": "Organization", "name": "Freedome" } },
        { "@type": "ListItem", "position": 25, "item": { "@type": "Organization", "name": "Quotidiano Sanità" } },
        { "@type": "ListItem", "position": 26, "item": { "@type": "Organization", "name": "Micuro" } },
        { "@type": "ListItem", "position": 27, "item": { "@type": "Organization", "name": "iDoctors" } },
        { "@type": "ListItem", "position": 28, "item": { "@type": "Organization", "name": "InSella" } }
      ]
    },

    {
      "@type": "WebSite",
      "@id": "https://searcus.ch/#website",
      "url": "https://searcus.ch/",
      "name": "Searcus Swiss SAGL",
      "alternateName": "Searcus",
      "description": "Official website of Searcus Swiss SAGL, a Technical SEO, PPC and AI development consulting agency in Lugano.",
      "inLanguage": ["en", "it"],
      "publisher": { "@id": "https://searcus.ch/#organization" },
      "copyrightHolder": { "@id": "https://searcus.ch/#organization" },
      "copyrightYear": 2010
    },

    {
      "@type": "WebPage",
      "@id": "https://searcus.ch/en/#webpage",
      "url": "https://searcus.ch/en/",
      "name": "Searcus Swiss SAGL — Technical SEO, International SEO & PPC Consulting, Lugano",
      "description": "Searcus Swiss SAGL: technical SEO and PPC consulting agency in Lugano. Crawling, rendering, indexing, log analysis, Core Web Vitals, international SEO, Google Ads & Reddit Ads. Since 2010. Google Partner.",
      "inLanguage": "en",
      "isPartOf": { "@id": "https://searcus.ch/#website" },
      "about": { "@id": "https://searcus.ch/#organization" },
      "mainEntity": { "@id": "https://searcus.ch/#organization" },
      "primaryImageOfPage": { "@id": "https://searcus.ch/#logo" },
      "significantLink": [
        "https://searcus.ch/en/#services",
        "https://searcus.ch/en/#clients",
        "https://searcus.ch/en/#about",
        "https://searcus.ch/en/#contact"
      ],
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": ["h1", "section#services h2", "section#about p"]
      }
    }
  ]
}
```

## Mapping HTML → schema (locale al template homepage EN)

Identico al mapping IT (vedi `01.md`). Differenze applicate solo a livello di **traduzione delle stringhe** dei seguenti campi (lingua di output `en`):

| Proprietà schema | Sorgente HTML EN |
|------------------|------------------|
| `WebPage.name` | `<title>` della pagina EN |
| `WebPage.description` | `<meta name="description">` della pagina EN |
| `WebPage.inLanguage` | `<html lang="en">` |
| `WebPage.significantLink[]` | navbar EN (`#services`, `#clients`, `#about`, `#contact`) |
| `WebPage.speakable.cssSelector[]` | sezioni EN (`section#services`, `section#about`) |
| `Organization.description` / `slogan` | hero EN (`<h1>` "We reverse-engineer how Google sees your site.") + `<meta description>` |
| `Service.description` (×11) | section `#services` `<p>` di ogni card (versione EN) |
| `OfferCatalog.name` / `description` | derivate dal copy EN |
| `ItemList.name` / `description` | derivate dal copy EN |
| `PostalAddress.name` | "Registered office" / "Operational office" (traduzione di "Sede legale" / "Sede operativa") |
| `award[]` | section credibility bar EN ("Google Partner since 2012", ecc.) |
| `keywords[]` | derivate dal copy EN |

Tutto il resto (`@id`, Wikidata `sameAs`, `vatID`, `foundingDate`, `priceRange`, `openingHours`, `contactPoint[].telephone`, `geo`, `hasMap`, `Person.sameAs[]`, brand names) è **identico** alla versione IT — sono dati cross-lingua.

## Nota implementativa: anti-duplicazione

Le due pagine IT e EN espongono `@id` identici per Organization/Person/OfferCatalog/ItemList/WebSite. Google e gli altri consumer di JSON-LD trattano queste istanze come la **stessa entità** osservata su due URL diverse (lingue diverse): non c'è duplicazione, solo localizzazione di alcune stringhe (description, name di alcuni nodi, ecc.). Solo le `WebPage` hanno `@id` distinti per pagina (`#webpage` con prefisso lingua).
