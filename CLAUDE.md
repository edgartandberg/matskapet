# Matskapet – kontekst for Claude Code

Dette er en norsk app-prototype for å redusere matsvinn: skanne matvarer, holde oversikt på holdbarhet, og vise klimaavtrykket til det man har i skapet.

## Status nå

`index.html` er en fungerende, selvstendig web-prototype (ingen build-steg — ren HTML/CSS/JS). Den dekker:

- Manuell registrering av vare, kategori og holdbarhetsdato (best før / siste forbruksdag)
- Strekkode-oppslag mot Open Food Facts sitt gratis API
- Kameraskanning via nettleserens `BarcodeDetector`-API, med fallback til manuell inntasting
- Oversikt sortert på hva som går ut snarest, med grovt CO2-anslag per vare og løpende regnskap for "spart" vs. "kastet" klimaavtrykk
- Datalagring bygget for Claude sin Artifact-plattform (`db`-capability), med fallback til `localStorage`

Se `README.md` for kjente begrensninger og hvordan man kjører den lokalt.

## Hva som skal bygges videre

Full kravspesifikasjon ligger i `docs/PRD.md` — les den først. Den beskriver tre nye funksjoner, i denne rekkefølgen (se PRD-ens "Foreslått rekkefølge / faseplan"):

1. **F2 – Kvitteringsskanning**: fotografer en kvittering, og appen registrerer varene automatisk i "skapet".
2. **F3 – Foto av oppskrift/ingrediensliste → handleliste**: fotografer en oppskrift eller ingrediensliste, og appen bygger en handleliste av det.
3. **F4 – Kuratert oppskriftsbank**: en samling oppskrifter (inspirert av den britiske appen MOB), der man kan hake av flere oppskrifter og få én samlet handleliste.

`docs/prosjektskisse.md` er det opprinnelige, bredere produktnotatet (visjon, målgruppe, konkurranselandskap, klimadata, forretningsmodell — engangskjøp med gratis nedlasting, ikke abonnement). Bruk den for kontekst om *hvorfor*, PRD-en for *hva* som skal bygges nå.

## Rammer å jobbe innenfor

- **Ingen backend med mindre det er nødvendig.** Målet er et hobbyprosjekt uten løpende kostnader. Lokale varsler og `db`-capability/`localStorage` dekker det meste. Hvis en funksjon (f.eks. kvitterings-OCR) krever en ekte tjeneste, flagg det tydelig og fortell hvorfor, i stedet for å bygge det inn stille.
- **Foto → strukturert data (kvittering, oppskrift) er den vanskeligste delen.** PRD-en peker på tredjeparts OCR-tjenester (Tabscanner, Klippa, Microblink) som et alternativ til å bygge egen bildeanalyse — vurder dette opp mot en enklere/billigere løsning før du går i gang, og spør hvis det er uklart.
- **Klimatall er grove anslag**, ikke offisielle RISE-tall. Ikke fremstill dem som mer presise enn de er.
- Hold appen som **én selvstendig fil (eller et lite sett filer uten build-steg)** så langt det er praktisk, i tråd med hvordan `index.html` er bygget i dag — med mindre kompleksiteten i de nye funksjonene gjør det uhensiktsmessig. Si fra hvis du mener det er på tide å bryte den mønsteret.

## Foreslått måte å starte på

Begynn med F2 (kvitteringsskanning) alene, foreslå en teknisk tilnærming (inkl. om det trengs en ekstern OCR-tjeneste), og vent på godkjenning før du går videre til F3 og F4.
