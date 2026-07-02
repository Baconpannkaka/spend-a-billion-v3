# AGENTS.md

## Produktregler

- Sidan är alltid ett fantasishopping-spel. Ingen riktig betalning eller beställning får införas.
- Budgeten får aldrig överskridas.
- Delade resultat är skrivskyddade.
- En utmaning återanvänder spelläge, valuta och budget men inte originalets varukorg.
- Alla priser lagras i SEK och visas i användarens valda valuta.
- Lyx- och vardagskatalogen ska vardera innehålla exakt 10 000 produkter.
- Produkt-id:n får aldrig återanvändas för en annan publicerad produkt.
- Endast bilder med status `approved` får visas.
- Officiella varumärkes- och modellnamn ska inte översättas. Generiska erbjudanden ska använda lokaliseringsfält.
- En extern produktkälla verifierar produktens existens, inte automatiskt det angivna priset.
- Genererade reservposter får inte använda påhittade varumärken eller framstå som verifierade produkter.
- Reklam ska vara avstängd tills publisher-id, juridik och samtyckeslösning är klara.

## Produktkvalitet

- `verified`: verkligt produktnamn/modell med extern källa.
- `curated`: manuellt kurerat fantasierbjudande.
- `generated`: tydligt märkt reservpost.
- `official-retail`: ungefärligt list-/konsumentpris.
- `market-estimate`: uppskattat marknads- eller samlarvärde.
- `fantasy-estimate`: underhållningsvärde.

Standardsorteringen ska prioritera `verified`, därefter `curated`, därefter `generated`.

## Struktur

- `src/app`: statiska routes för GitHub Pages.
- `src/components`: återanvändbara UI- och flödeskomponenter.
- `src/context`: global spelstatus, språk och toast.
- `src/catalog`: asynkron katalog- och bildmanifestladdning.
- `src/lib`: budget, varukorg, sökning, format, delning, produkttext och achievements.
- `src/data`: små handskrivna referensdata som valuta och förmögenhetsprofiler.
- `src/config/ads.ts`: avstängd reklamkonfiguration.
- `scripts/real-product-seeds.mjs`: kurerade verkliga produktnamn, priser och källor.
- `scripts/generate-catalogs.mjs`: genererar 20 000 produkter och kvalitetsrapport.
- `public/data`: färdiga kataloger, rapport och bildmanifest.
- `public/products`: framtida produktbilder döpta efter produkt-id.
- `schemas`: JSON-kontrakt för katalog och bildmanifest.
- `tools/image-importer`: krav för framtida importerare.
- `DATA-QUALITY.md`: kvalitets- och språkmodell.
- `AD-INTEGRATION.md`: regler för framtida reklam.

## Kodprinciper

- TypeScript strict, inga `any`.
- Stora kataloger importeras inte i React-bundlen; de hämtas som JSON per spelläge.
- Lägg inte in 20 000 dynamiska routes. Produktsidan använder query-parametrar.
- Håll shoppingflödet kompakt och överskådligt; stora redaktionella rubriker hör främst hemma på landningssidor.
- All klientlagring ska valideras innan den används.
- All delningsdata ska valideras och budgetbegränsas.
- Nya verkliga produkter ska ha källa, pristyp och granskningsdatum.
- Synliga kvalitetsmarkörer ska vara sakliga och inte påstå att ett uppskattat pris är verifierat.
- Annonskomponenter får inte efterlikna produktkort eller orsaka layoutskiften.

## Kommandon

```bash
npm run catalog:generate
npm run catalog:validate
npm run images:validate
npm run lint
npm run typecheck
npm test
npm run verify
npm run build
```
