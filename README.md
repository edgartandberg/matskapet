# Matskapet

Prototype av en norsk app for å skanne matvarer, holde oversikt på holdbarhet, og se klimaavtrykket til det du har i skapet. Bygget som en tidlig nettbasert prototype for å teste konseptet før en eventuell native app (React Native / Expo).

## Status

Fungerende prototype, ikke produksjonsklar. Se `index.html` — én selvstendig fil med all HTML, CSS og JavaScript, ingen build-steg.

**Fungerer:**
- Manuell registrering av vare, kategori og holdbarhetsdato (best før / siste forbruksdag)
- Oppslag mot [Open Food Facts](https://world.openfoodfacts.org) sitt gratis API via strekkode
- Kameraskanning av strekkode via nettleserens innebygde `BarcodeDetector`-API (der nettleseren støtter det — faller ellers tilbake til manuell inntasting)
- Oversikt sortert på hva som går ut snarest, med grov CO2-anslag per vare og løpende regnskap for "spart" vs. "kastet" klimaavtrykk

**Kjente begrensninger:**
- Klimatallene er grove, internasjonale anslag (ikke de norsktilpassede RISE-tallene fra prosjektskissen)
- Ingen ekte push-varsler i bakgrunnen — det krever en native app
- Datalagring: bygget for Claude sin Artifact-plattform (en `db`-funksjon knyttet til siden). Kjøres den et annet sted, faller den tilbake til nettleserens `localStorage`, som er per enhet/nettleser

## Kjøre lokalt

Ingen installasjon nødvendig — åpne `index.html` direkte i en nettleser, eller kjør en enkel lokal server, f.eks.:

```
npx serve .
```

## Veien videre

Neste steg er trolig en native app (React Native / Expo) for ekte varsler og App Store-distribusjon, med et engangskjøp i appen for å låse opp full funksjonalitet (gratis nedlasting). Se egen prosjektskisse for detaljer om datakilder, klimadata (RISE) og mulig samarbeid med Framtiden i våre hender.
