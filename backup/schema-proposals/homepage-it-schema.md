# Homepage IT — Searcus Swiss SAGL (Lugano)

| Campo | Valore |
|-------|--------|
| Template ID | homepage |
| URL pattern | https://searcus.ch/it/ |
| Input file | Searcus Swiss SAGL — Consulenza Technical SEO, International SEO e PPC, Lugano.html |
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
| ItemList (clienti) | — | MISSING |
| WebSite | — | MISSING |
| WebPage | — | MISSING |

L'HTML in input non contiene alcun blocco `<script type="application/ld+json">` (verificato da `preprocess.py`: `jsonld=0`). Tutto il markup è da introdurre ex novo.

## Task list

| # | Tag | Azione | Target | Note |
|---|-----|--------|--------|------|
| 1 | P0 | ADD `@graph` unico in `<head>` | layout globale | Un solo `<script application/ld+json>` per pagina; `@id` riusabili da altre pagine future |
| 2 | P0 | ADD `Organization` + `LocalBusiness` combinato | `@id` https://searcus.ch/#organization | Sottotipo `ProfessionalService` scartato (deprecato come tipo generico da schema.org) |
| 3 | P0 | ADD `Person` founder Giovanni Sacheli | `@id` https://searcus.ch/#person | `sameAs` verso evemilano.com/about-me/ e profili social |
| 4 | P0 | ADD `WebSite` + `WebPage` | `@id` #website, #webpage | `inLanguage: "it"` (senza regione, come confermato) |
| 5 | P0 | ADD `OfferCatalog` con 11 `Service` | `@id` https://searcus.ch/#services | 6 servizi dal sito + 5 sotto-servizi AI dev |
| 6 | P0 | ADD `ItemList` clienti enterprise (28 brand) | `@id` https://searcus.ch/#clients | Sezione `#clienti` (marquee); confermato diritto a citarli |
| 7 | P0 | ADD doppio `ContactPoint` (+41 CH, +39 IT) | dentro Organization | Mercato CH + mercato IT come da scelta utente |
| 8 | P0 | ADD doppio `PostalAddress` (Pazzallo + Mendrisio) | dentro Organization | Sede legale + sede operativa |
| 9 | P0 | ADD `areaServed[]` con 6 entità | dentro Organization | CH, IT, DK, GB, DE, Europe — con `sameAs` Wikidata |
| 10 | P0 | ADD `hasCertification` (Google Partner, SISTRIX Partner) | dentro Organization | Dal credibility bar in homepage |
| 11 | P0 | ADD `identifier` UID Svizzera (PropertyValue) + `vatID` | dentro Organization | CHE-180.818.315 — da footer |
| 12 | P0 | ADD `openingHoursSpecification` Mo-Fr 09:00–18:00 | dentro Organization | Pattern operativo, costante |
| 13 | P0 | ADD `priceRange: €€€` | dentro Organization | Coerente con evemilano.com (fascia premium) |
| 14 | P0 | ADD `foundingDate: 2010-01-01` + `foundingLocation` (Lugano) | dentro Organization | Da hero ("dal 2010") |
| 15 | P0 | ADD `geo` (lat/lon Pazzallo) + `hasMap` | dentro Organization | Coerenza con sede legale |
| 16 | P0 | ADD `knowsAbout[]` (Wikidata) | dentro Organization | SEO, SEM, AI, LLM, RAG, Python, ecc. |
| 17 | P0 | ADD `knowsLanguage` (it, en) | dentro Organization | Multilingua |
| 18 | P0 | ADD `sameAs[]` social aziendali/founder | dentro Organization | LinkedIn azienda + LinkedIn founder + GitHub + X + YouTube |
| 19 | P0 | ADD `logo` ImageObject + `image` riferimento | dentro Organization | URL placeholder — asset logo Searcus da fornire |
| 20 | P1 | ADD `brand` Brand "Searcus" | dentro Organization | Coerente con uso di "Searcus" come alternateName |
| 21 | P1 | ADD `slogan` | dentro Organization | "Analizziamo come Google vede il tuo sito." da hero |
| 22 | P1 | ADD `numberOfEmployees: 3` | dentro Organization | Da profilo.json sezione chi-siamo |
| 23 | P1 | ADD `award[]` | dentro Organization | Google Partner 2012, SISTRIX Partner 2018, Zero penalizzazioni |
| 24 | P1 | ADD `currenciesAccepted`, `paymentAccepted` | dentro Organization | CHF/EUR; Cash/Credit Card/Bank Transfer |
| 25 | P1 | ADD `speakable` SpeakableSpecification | dentro WebPage | Selettori CSS per H1/H2 + Chi siamo |
| 26 | P1 | ADD `significantLink[]` | dentro WebPage | 4 ancore: #servizi, #clienti, #chi-siamo, #contatti |
| 27 | P1 | ADD `audience` BusinessAudience "Enterprise" | dentro ogni Service | Coerente con copy "medie e grandi aziende" |
| 28 | P1 | ADD `availableChannel` ServiceChannel | dentro ogni Service | URL + lingue disponibili |
| 29 | P1 | ADD `isRelatedTo[]` tra Service AI | cross-link tra LLM/Agents/RAG | Aiuta motori a capire il cluster AI |
| 30 | P2 | OMIT `BreadcrumbList` | layout | Confermato skip (single-page, una sola entry) |
| 31 | P2 | OMIT `SearchAction` su WebSite | layout | Confermato skip (no search interno) |
| 32 | P2 | OMIT `aggregateRating` / `review` | Organization | Nessuna review pubblica disponibile sul sito attualmente |
| 33 | P2 | ADD `hreflang` annotation cross-link Page | dentro WebPage (futuro) | `inLanguage` + WebSite contenente entrambe le lingue gestisce; in più, link HTML hreflang già presenti |

Tag ammessi: P0 (rich-result critico / validazione bloccante), P1 (raccomandato), P2 (nice-to-have).

## JSON-LD finale

Da iniettare in `<head>` come **singolo** `<script type="application/ld+json">`:

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
      "description": "Agenzia di consulenza Technical SEO, International SEO, PPC e AI development. Fondata nel 2010 a Lugano, Svizzera. Clienti enterprise in Svizzera, Italia, Danimarca, UK, Germania e resto d'Europa.",
      "slogan": "Analizziamo come Google vede il tuo sito.",
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
        "name": "Lugano, Svizzera",
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
        "name": "Numero UID Svizzera",
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
          "name": "Sede legale",
          "streetAddress": "Via dei Faggi, 4V",
          "addressLocality": "Pazzallo",
          "addressRegion": "TI",
          "postalCode": "6912",
          "addressCountry": "CH"
        },
        {
          "@type": "PostalAddress",
          "name": "Sede operativa",
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
          "availableLanguage": ["Italian", "English"]
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
          "availableLanguage": ["Italian", "English"]
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
        { "@type": "Language", "name": "Italian", "alternateName": "it" },
        { "@type": "Language", "name": "English", "alternateName": "en" }
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
        "Google Partner dal 2012",
        "SISTRIX Partner dal 2018",
        "Zero penalizzazioni Google dal 2010"
      ],
      "keywords": [
        "Agenzia Technical SEO",
        "Agenzia International SEO",
        "Agenzia Google Ads",
        "Agenzia PPC",
        "Agenzia AI Development",
        "Consulenza SEO Lugano",
        "SEO enterprise",
        "Reddit Ads",
        "LLM Integration"
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
      "description": "Consulente Technical SEO, Google Ads e AI development. Fondatore di Searcus Swiss SAGL nel 2010.",
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
        "name": "Università Commerciale Luigi Bocconi",
        "sameAs": "https://www.wikidata.org/wiki/Q777582"
      },
      "worksFor": { "@id": "https://searcus.ch/#organization" },
      "knowsLanguage": [
        { "@type": "Language", "name": "Italian", "alternateName": "it" },
        { "@type": "Language", "name": "English", "alternateName": "en" }
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
      "name": "Servizi Searcus Swiss",
      "description": "Catalogo dei servizi di consulenza Technical SEO, International SEO, PPC e AI development.",
      "numberOfItems": 11,
      "itemListOrder": "https://schema.org/ItemListUnordered",
      "itemListElement": [
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-technical-seo",
          "name": "Technical SEO",
          "serviceType": "Technical SEO",
          "description": "Audit approfonditi su crawling, rendering e indexing. Log file analysis, ottimizzazione Core Web Vitals, dati strutturati, JavaScript SEO e migrazioni. Lavoriamo direttamente con il team di sviluppo.",
          "category": ["crawling", "rendering", "indexing", "log analysis", "Core Web Vitals", "JS SEO", "migrazioni"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "serviceLocation": { "@type": "Place", "name": "Lugano, Svizzera" },
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-international-seo",
          "name": "International SEO",
          "serviceType": "International SEO",
          "description": "Architettura hreflang, strategia ccTLD/subfolder/subdomain, geo-targeting, keyword research multilingua e strategie di contenuto localizzate.",
          "category": ["hreflang", "geo-targeting", "multilingua", "ccTLD", "subfolder", "international keyword research"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ppc",
          "name": "PPC Advertising",
          "serviceType": "Pay-per-click advertising",
          "description": "Gestione Google Ads (Search, Shopping, Display, YouTube, Performance Max) e Reddit Ads. Conversion tracking, ottimizzazione feed, strategie di bidding avanzate.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-formazione",
          "name": "Formazione professionale",
          "serviceType": "Professional training",
          "description": "Corsi di Technical SEO, Google Ads, Google Search Console e web analytics. Workshop privati o aziendali, dai fondamenti al livello avanzato. In sede o da remoto.",
          "category": ["corsi SEO", "corsi Google Ads", "workshop aziendali", "training in-house", "remote training"],
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
              "name": "In sede",
              "serviceLocation": { "@type": "Place", "name": "Lugano, Svizzera" },
              "availableLanguage": ["Italian", "English"]
            },
            {
              "@type": "ServiceChannel",
              "name": "Remoto",
              "serviceUrl": "https://searcus.ch/it/#servizi",
              "availableLanguage": ["Italian", "English"]
            }
          ]
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-seo-manager",
          "name": "SEO Manager",
          "serviceType": "Fractional SEO management",
          "description": "Orchestrazione strategica della visibilità digitale per aziende. Call mensili, iniziative data-driven, coordinamento con copywriter e sviluppatori interni.",
          "category": ["enterprise SEO", "strategia", "coordinamento", "fractional SEO", "SEO management"],
          "provider": { "@id": "https://searcus.ch/#organization" },
          "areaServed": [
            { "@type": "Country", "name": "Switzerland" },
            { "@type": "Country", "name": "Italy" },
            { "@type": "Place", "name": "Europe" }
          ],
          "audience": { "@type": "BusinessAudience", "audienceType": "Enterprise" },
          "availableChannel": {
            "@type": "ServiceChannel",
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-competitive-intelligence",
          "name": "SEO Competitive Intelligence",
          "serviceType": "Competitive intelligence and SEO gap analysis",
          "description": "Analisi competitor SEO sistematica: mappatura keyword portfolio, crawl comparison, SERP share modelling sui cluster prioritari, backlink gap audit. Output: opportunity matrix azionabile.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-llm-integration",
          "name": "LLM Integration",
          "serviceType": "Custom AI software development — Large Language Model integration",
          "description": "Integrazione di Large Language Model (Claude, GPT, Llama, Gemini) in workflow di prodotto: chat assistant, classificazione, estrazione semantica, content generation con guardrails.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ai-agents",
          "name": "AI Agents",
          "serviceType": "Agentic AI software development",
          "description": "Sviluppo di agenti AI per automatizzare processi business: research agents, classificatori, agenti di analisi SEO, integrazioni multi-tool con MCP, orchestrazione di sub-agent.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-rag-pipelines",
          "name": "RAG Pipelines",
          "serviceType": "Retrieval-Augmented Generation pipelines",
          "description": "Architettura di pipeline RAG: ingestion, chunking, embedding, vector database, retrieval, re-ranking, grounding con citazioni. Casi d'uso: knowledge base, customer support, internal search semantica.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-ai-automation",
          "name": "AI Automation",
          "serviceType": "AI-driven workflow automation",
          "description": "Automazione di processi ripetitivi tramite AI: triage email, classificazione ticket, generazione report SEO, monitoraggio SERP, content briefing. Integrazione con stack esistenti (n8n, Make, Python custom).",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        },
        {
          "@type": "Service",
          "@id": "https://searcus.ch/#service-custom-ai-software",
          "name": "Custom AI Software",
          "serviceType": "Custom AI software development",
          "description": "Sviluppo software AI custom in Python: tool interni, dashboard data-driven, dataset pipelines, fine-tuning, integrazioni API. End-to-end dalla raccolta requisiti al deploy.",
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
            "serviceUrl": "https://searcus.ch/it/#servizi",
            "availableLanguage": ["Italian", "English"]
          }
        }
      ]
    },

    {
      "@type": "ItemList",
      "@id": "https://searcus.ch/#clients",
      "name": "Clienti enterprise Searcus Swiss",
      "description": "Selezione di clienti enterprise serviti da Searcus Swiss SAGL dal 2010: brand internazionali nei settori pharma, banking, fashion, editoriale, hospitality, e-commerce.",
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
      "description": "Sito ufficiale di Searcus Swiss SAGL, agenzia di consulenza Technical SEO, PPC e AI development a Lugano.",
      "inLanguage": ["it", "en"],
      "publisher": { "@id": "https://searcus.ch/#organization" },
      "copyrightHolder": { "@id": "https://searcus.ch/#organization" },
      "copyrightYear": 2010
    },

    {
      "@type": "WebPage",
      "@id": "https://searcus.ch/it/#webpage",
      "url": "https://searcus.ch/it/",
      "name": "Searcus Swiss SAGL — Consulenza Technical SEO, International SEO e PPC, Lugano",
      "description": "Searcus Swiss SAGL: consulenza technical SEO e PPC a Lugano. Crawling, rendering, indexing, log analysis, Core Web Vitals, SEO internazionale, Google Ads e Reddit Ads. Dal 2010. Google Partner.",
      "inLanguage": "it",
      "isPartOf": { "@id": "https://searcus.ch/#website" },
      "about": { "@id": "https://searcus.ch/#organization" },
      "mainEntity": { "@id": "https://searcus.ch/#organization" },
      "primaryImageOfPage": { "@id": "https://searcus.ch/#logo" },
      "significantLink": [
        "https://searcus.ch/it/#servizi",
        "https://searcus.ch/it/#clienti",
        "https://searcus.ch/it/#chi-siamo",
        "https://searcus.ch/it/#contatti"
      ],
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": ["h1", "section#servizi h2", "section#chi-siamo p"]
      }
    }
  ]
}
```

## Mapping HTML → schema (locale al template homepage IT)

| Proprietà schema | Sorgente HTML / sezione | Trasformazione |
|------------------|-------------------------|----------------|
| `Organization.name` | (costante footer) "Searcus Swiss SAGL" | letterale |
| `Organization.alternateName` | navbar `<a>Searcus</a>` | letterale |
| `Organization.legalName` | footer "Searcus Swiss SAGL" | letterale |
| `Organization.slogan` | `<h1>` hero (frammento "Analizziamo come Google vede il tuo sito.") | trim |
| `Organization.description` | section `#chi-siamo` primo `<p>` | sintesi 1–2 frasi |
| `Organization.foundingDate` | hero `<p>// dal 2010 — Lugano, Svizzera` + footer "© 2010–…" | costante 2010-01-01 |
| `Organization.foundingLocation` | footer "© 2010… Searcus Swiss SAGL" + indirizzo | "Lugano, Svizzera" |
| `Organization.address[]` | section `#contatti` blocco "Searcus Swiss SAGL / Via dei Faggi 4V…" + manifest sede operativa Mendrisio | parse riga per riga |
| `Organization.geo` | section `#contatti` "46.0037°N, 8.9511°E" | NB: l'HTML mostra le coordinate del centro Lugano, non di Pazzallo. Nel JSON-LD usate le coordinate effettive di Pazzallo (45.971, 8.9485). Allineare i due valori. |
| `Organization.telephone` | section `#contatti` `<a href="tel:+41798643035">` | strip whitespace |
| `Organization.email` | section `#contatti` `<a href="mailto:giovanni@searcus.ch">` | letterale |
| `Organization.vatID` / `identifier` | section `#contatti` "UID: CHE-180.818.315" + footer | costante CHE-180.818.315 |
| `Organization.contactPoint[]` | tel + email + manifest (telefono IT +39) | merge HTML+manifest |
| `Organization.areaServed[]` | section `#chi-siamo` profilo.json "mercati":["CH","IT","DK","UK","DE","EU"] | mapping ISO → Country/Place |
| `Organization.knowsAbout[]` | section `#servizi` 6 cards + manifest AI sub-services | unione |
| `Organization.knowsLanguage` | navbar lang-toggle IT/EN + manifest | costante |
| `Organization.hasCertification[]` | section credibility bar "Google Partner dal 2012", "SISTRIX Partner dal 2018" | parse |
| `Organization.award[]` | section credibility bar (idem) + "Zero penalizzazioni" | parse |
| `Organization.openingHours` / `openingHoursSpecification` | (manifest, costante operativa) | costante Mo-Fr 09:00-18:00 |
| `Organization.priceRange` | (manifest, costante) | "€€€" |
| `Organization.numberOfEmployees` | section `#chi-siamo` profilo.json "team tecnico":[...] (3 nomi) | count |
| `Organization.sameAs[]` | footer social icons (LinkedIn, GitHub, X, YouTube) + manifest | unione |
| `Person.name` | section `#chi-siamo` "fondata nel 2010 da Giovanni Sacheli" + profilo.json | letterale |
| `Person.alumniOf` | (riuso da evemilano.com — confermare) | costante o omettere se non vuoi inferire |
| `Person.sameAs[]` | footer social + manifest (profili pubblici di Giovanni) | unione |
| `OfferCatalog.itemListElement[].Service.name` | section `#servizi` `<h3>` di ogni card | letterale |
| `Service.description` | section `#servizi` `<p>` di ogni card | letterale |
| `Service.category[]` | section `#servizi` `<span class="pill-tag">` di ogni card | array di Text |
| `Service.serviceType` | (mapping manuale dal `name`) | costante per template |
| `Service.areaServed[]` | manifest `area_served` | costante |
| `Service (AI sub-services)` | (non presenti nell'HTML attuale — da manifest) | da fornire copy nel sito + JSON-LD |
| `ItemList.itemListElement[].Organization.name` | section `#clienti` marquee `<span class="font-display">` | dedup (l'HTML duplica i nomi per il loop infinito) |
| `WebSite.name` | `<title>` brand part | letterale |
| `WebPage.name` | `<title>` completo | letterale |
| `WebPage.description` | `<meta name="description">` | letterale |
| `WebPage.inLanguage` | `<html lang="it">` + manifest (policy: solo `it`) | costante |
| `WebPage.significantLink[]` | navbar `<a href="#…">` | array URL assolute |
