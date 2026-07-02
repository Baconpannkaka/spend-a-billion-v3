# Spend a Billion v3

Ett statiskt fantasishopping-spel byggt med Next.js, React, TypeScript och Tailwind CSS. Användaren väljer ett shoppingläge, en budget och en valuta, fyller en fantasivarukorg och delar ett skrivskyddat resultat.

- **Miljardärsläge:** privatjet, fordon, yachter, klockor, konst, fastigheter, PSA-graderade samlarkort och extrema upplevelser.
- **Vardagsläge:** mobiler, datorer, spel, mat, hem, kläder, barn, fritid, husdjur, resor och andra igenkännbara köp.

Allt körs i webbläsaren. Ingen databas, autentisering eller riktig betalning används.

## Vad som är nytt i v3

- Solida toastmeddelanden som inte försvinner mot produktkorten.
- Kompaktare och stabilare summering i varukorgen.
- Resultatbildsfunktionen är borttagen; länkdelning och Web Share finns kvar.
- Sökfältet är förenklat utan dekorativ sökring.
- Produktnamn skiljer nu på officiella namn och översättbara generiska erbjudanden.
- Standardsorteringen prioriterar verkliga produkter framför kurerade och genererade katalogposter.
- Produktdetaljen visar datatyp, pristyp, granskningsdatum och extern produktkälla när sådan finns.
- 334 verkliga produktnamn/modeller har lagts in med externa källfält och ungefärliga priser.
- Påhittade reservvarumärken har tagits bort. Återstående reservposter är tydligt märkta fantasival.
- Katalograpport och hårdare validering för dubletter, källor, priser och språkmetadata.

## Installera och starta

```bash
npm install
npm run dev
```

Öppna `http://localhost:3000`.

## Kvalitetskontroller

```bash
npm run verify
npm run build
```

`verify` kör katalogvalidering, bildmanifestvalidering, lint, TypeScript och tester.

## GitHub Pages

Projektet använder statisk export och har ett färdigt arbetsflöde i `.github/workflows/pages.yml`.

1. Skapa helst ett nytt, tomt repository för denna stora version.
2. Lägg allt innehåll från projektmappen direkt i repositoryts rot.
3. Kontrollera att `.github`, `package.json`, `package-lock.json`, `src` och `public` syns direkt under **Code**.
4. Gör repositoryt publikt om GitHub-planen kräver det för Pages.
5. Välj **Settings → Pages → GitHub Actions**.
6. Följ körningen under **Actions** tills både `build` och `deploy` är gröna.

## Produktkataloger

Katalogerna byggs med:

```bash
npm run catalog:generate
```

Färdiga filer:

- `public/data/catalog-luxury.json`
- `public/data/catalog-everyday.json`
- `public/data/catalog-report.json`

Varje läge innehåller exakt 10 000 produkter och laddas separat i webbläsaren. Gränssnittet visar 48 produkter åt gången.

Nuvarande kvalitetsfördelning:

- Miljardärsläge: 129 verkliga modeller, 9 kurerade fantasierbjudanden och 9 862 genererade reservposter.
- Vardagsläge: 205 verkliga modeller och 9 795 genererade reservposter.

Läs [DATA-QUALITY.md](DATA-QUALITY.md) för kvalitetsnivåer, språkregler och källor. En prioriterad lista över det som fortfarande återstår finns i [REMAINING-WORK.md](REMAINING-WORK.md).

## Produktnamn och språk

Officiella modellnamn ska inte maskinöversättas. `Audemars Piguet Royal Oak Concept Flying Tourbillon` behålls därför oförändrat, medan generiska namn som `Takvåning i Monaco` kan lokaliseras.

Varje produkt kan ha separata lokaliseringar för:

- namn,
- kort och lång beskrivning,
- fakta,
- kategori,
- underkategori.

Gränssnittet stöder svenska, engelska, spanska, mandarin, hindi och arabiska. Kärnflödet är översatt, medan vissa sekundära informationssidor och delar av den verkliga produktdatan fortfarande använder svensk fallback.

## Priser och källor

Alla priser lagras i SEK och visas i vald valuta. Priserna är ungefärliga underhållningsvärden och har en separat typ:

- ungefärligt list-/konsumentpris,
- uppskattat marknadsvärde,
- fantasipris.

En extern produktkälla bekräftar i första hand att produktnamnet eller modellen är verklig. Den ska inte tolkas som en aktuell offert. Prisdatum och källor måste uppdateras löpande inför en publik lansering.

## Bilder

Produktbilder är separerade från katalogen:

- filer: `public/products/<productId>.webp`
- metadata: `public/data/image-manifest.json`
- granskningskö: `public/data/image-review.json`

Endast bilder med status `approved` visas. Produkter utan godkänd bild använder automatiskt en exklusiv placeholder. Läs `tools/image-importer/README.md` för den framtida Wikimedia-importerarens kontrakt.

## Delning

Resultat serialiseras som validerad, URL-säker data med spelläge, budget, valuta, produkt-id:n och antal. Delade länkar är skrivskyddade. **Utmana en vän** startar ett nytt spel med samma budget men tom varukorg.

## Reklam

Reklamytor är förberedda men avstängda. Inga annons- eller spårningsskript laddas. Läs [AD-INTEGRATION.md](AD-INTEGRATION.md) innan en verklig leverantör kopplas in.

## Viktiga begränsningar

- 334 av 20 000 poster är för närvarande verkliga produktnamn/modeller med externa källfält.
- Resterande katalog behöver successivt ersättas och kvalitetssäkras; reservposterna är avsiktligt tydliga fantasival.
- Priserna är inte en komplett realtidsdatabas och kan vara inaktuella eller variera mellan marknader.
- Automatiserad bildimport, licensgranskning och riktiga produktbilder ingår inte ännu.
- Fullständig översättning av alla 20 000 produkttexter och sekundära sidor återstår.
- Aktiv reklam, CMP/samtycke, analytics och publisher-id är inte aktiverade.

## Juridiskt

Sidan säljer ingenting och är inte ansluten till personerna eller varumärkena som nämns. Produktnamn och varumärken tillhör respektive rättighetsinnehavare. Bildmaterial får bara publiceras när användningsrätt, fotograf och licens är verifierade.
