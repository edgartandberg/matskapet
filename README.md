# Matskapet

Prototype av en norsk app for å skanne matvarer, holde oversikt på holdbarhet, og se klimaavtrykket til det du har i skapet. Bygget som en tidlig nettbasert prototype for å teste konseptet før en eventuell native app (React Native / Expo).

## Status

Fungerende prototype, ikke produksjonsklar. Se `index.html` — én selvstendig fil med all HTML, CSS og JavaScript, ingen build-steg.

**Fungerer:**
- Manuell registrering av vare, kategori og holdbarhetsdato (best før / siste forbruksdag)
- Oppslag mot [Open Food Facts](https://world.openfoodfacts.org) sitt gratis API via strekkode
- Kameraskanning av strekkode via nettleserens innebygde `BarcodeDetector`-API (der nettleseren støtter det — faller ellers tilbake til manuell inntasting)
- Oversikt sortert på hva som går ut snarest, med grov CO2-anslag per vare og løpende regnskap for "spart" vs. "kastet" klimaavtrykk
- Kvitteringsskanning (F2): ta/last opp bilde av en kvittering, og appen leser varelinjene med [Tesseract.js](https://tesseract.projectnaomi.com/) (klient-side OCR i nettleseren, ingen server involvert). Gjetter kategori og et standard holdbarhetsanslag per linje — du går alltid gjennom og godkjenner/retter/fjerner linjer før de legges i matskapet
- Handleliste og oppskriftsfoto (F3): egen handleliste du kan legge til varer i manuelt, eller ved å fotografere en ingrediensliste (samme Tesseract.js-motor som F2). Ingredienser som ser ut til å allerede finnes i matskapet ditt er forhåndsavhuket bort — du går alltid gjennom listen før noe legges til
- Kuratert oppskriftsbank (F4): et lite, håndplukket utvalg oppskrifter (ti stk, hardkodet i appen). Hak av det du vil lage denne uken, og ingrediensene fra alle valgte oppskrifter slås sammen til én handleliste — samme kryssjekk mot matskapet og bekreftelsessteg som i F3

**Kjente begrensninger:**
- Klimatallene er grove, internasjonale anslag (ikke de norsktilpassede RISE-tallene fra prosjektskissen)
- Kvitterings- og oppskriftsgjenkjenning er enkle heuristikker (pris-/mengde-mønster + nøkkelord), ikke dedikerte OCR-tjenester — de bommer på butikkforkortelser, oppskriftstitler og uvanlige formater. Bilder sendes aldri til noen server og lagres ikke
- Ingen ekte push-varsler i bakgrunnen — det krever en native app
- Datalagring: bygget for Claude sin Artifact-plattform (en `db`-funksjon knyttet til siden). Kjøres den et annet sted, faller den tilbake til nettleserens `localStorage`, som er per enhet/nettleser

## Kjøre lokalt

Ingen installasjon nødvendig — åpne `index.html` direkte i en nettleser, eller kjør en enkel lokal server, f.eks.:

```
npx serve .
```

## Veien videre

Neste steg er trolig en native app (React Native / Expo) for ekte varsler og App Store-distribusjon, med et engangskjøp i appen for å låse opp full funksjonalitet (gratis nedlasting). Se egen prosjektskisse for detaljer om datakilder, klimadata (RISE) og mulig samarbeid med Framtiden i våre hender.
