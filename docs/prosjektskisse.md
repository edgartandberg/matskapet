# Matsvinn- og klimaapp – Prosjektskisse

Sep 17, 2026 · @Edgar

## Konsept og visjon

En norsk app der du skanner matvarene dine, legger inn holdbarhetsdato, og får automatisk oversikt og varsel før noe går ut. Differensieringen er klimaavtrykket: appen viser CO2-avtrykket til matvarene du faktisk har i skapet, og hvor mye du sparer klimaet ved å bruke opp mat før den kastes – ikke bare et generelt klimaregnskap koblet til hva du kjøper i én bestemt butikk. På sikt er målet et samarbeid med Framtiden i våre hender, som gir faglig troverdighet og et naturlig publikum av klimabevisste brukere. (Arbeidstittel her er "Matsvinn- og klimaapp" – rent beskrivende; et kortere navn som f.eks. "Holdbar" kan være verdt å vurdere, men det er bare et forslag.)

## Problem og målgruppe

Mye spiselig mat kastes i norske hjem rett og slett fordi det er vanskelig å holde oversikt over hva som ligger i skap, kjøleskap og fryser og når det går ut – man oppdager det for sent. Samtidig øker interessen for å forstå eget klimaavtrykk fra maten man spiser, ikke bare fra reise og forbruk generelt. Målgruppen er klima- og miljøbevisste forbrukere som både vil spare penger på å kaste mindre mat, og forstå den reelle klimapåvirkningen av det de faktisk har hjemme.

## Konkurranselandskap

Throw No More er allerede en etablert norsk matsvinn-aktør (10 000+ nedlastinger) med avtaler med SPAR/EUROSPAR om å selge ned varer nær utløpsdato i butikk – men dette er butikkrettet, ikke en personlig oversikt over holdbarhet hjemme hos deg.

På klimasiden har flere store aktører allerede egne klimaavtrykk-funksjoner: Oda.com viser klimaavtrykk for matvarer og oppskrifter, MENY-appen viser "ditt klimaavtrykk", og fordelsprogrammet Trumf har egen klimaavtrykk-visning på tvers av kjeder. Disse er derimot koblet til hva du KJØPER hos én aktør, ikke til det du faktisk har liggende hjemme og bruker opp eller kaster.

Ingen av aktørene ser ut til å kombinere personlig holdbarhetsoversikt i hjemmet med klimaavtrykk per vare, uavhengig av hvilken butikk maten er kjøpt i – det er trolig her det reelle åpne rommet ligger, fremfor i "matsvinn" eller "klimaavtrykk" hver for seg.

## Kjernefunksjoner

- Skann strekkode for å legge til en matvare (henter produktnavn og bilde automatisk)
- Legg inn holdbarhetsdato manuelt (bildeassistert datoavlesning kan komme senere)
- Oversikt over alt i skap, kjøleskap og fryser, sortert etter hva som går ut snarest
- Push-varsler før holdbarhetsdato nås
- Oppskriftsforslag basert på det som snart går ut
- Klimaavtrykk per vare og for hele "matskapet", pluss hvor mye CO2 du har spart ved å bruke opp mat før den ble kastet

## Klimaavtrykk som differensiator

RISE, et svensk forskningsinstitutt, har en klimatdatabase for matvarer med CO2e-verdier per matkategori – og det finnes en egen norsk versjon av denne. Det er trolig det mest realistiske utgangspunktet for klimaberegninger i appen, fremfor å bygge en egen database fra bunnen av.

Norge har også en bransjeinitiert klimamerking av mat ("Klodemerket", fra Næringssamarbeidet for klimamerking av mat) som etter hvert merkes direkte på enkelte produkter – dette kan på sikt være en ekstra datakilde å hente fra selve pakningen, i tillegg til RISE-tallene.

Appens vinkel bør være å koble klimatall til varer man faktisk HAR hjemme og til matsvinnet man unngår – ikke bare til det man kjøper i én bestemt butikk-app, som er der de eksisterende klimaavtrykk-funksjonene stopper i dag.

## Mulig samarbeid med Framtiden i våre hender

Framtiden i våre hender (FIVH) driver allerede et eget matsvinn-prosjekt, "Fra matsvinn til MatVinn", og har egne tema-sider for både bærekraftig mat og matsvinn. De er derfor en naturlig samarbeidspartner – både for troverdighet og fordi de allerede jobber aktivt med nøyaktig dette problemet.

Et samarbeid kunne for eksempel innebære at appens klimatall og matsvinn-tips er faglig forankret hos FIVH, at de anbefaler appen til sine medlemmer, eller at data om spart matsvinn kan inngå i deres påvirkningsarbeid overfor bransjen og myndighetene. Dette er satt på vent i denne omgang – ikke noe man bygger inn en avhengighet av eller planlegger kontakt om ennå.

## Teknisk arkitektur og datakilder

- **Mobilapp:** cross-platform (React Native eller Flutter) for raskest vei til App Store
- **Strekkodeskanning:** mot Open Food Facts som gratis utgangspunkt for produktdata; vurder GS1 sin GEPIR-lisens ved skalering hvis dekningen ikke er god nok
- **Holdbarhetsdato:** manuell registrering i første versjon — bildeassistert avlesning (OCR) av påtrykt dato er en egen, vesentlig tyngre utviklingsfase som bør komme senere
- **Klimadata-lag:** koblet til RISE sin klimatdatabase (norsk versjon) per produktkategori
- **Varsler:** lokale påminnelser på telefonen dekker holdbarhetsvarsler uten behov for egen server; en lett backend er først nødvendig hvis oppskriftsforslag skal hente fra en ekstern tjeneste
- **Lagring:** enkel lokal lagring av brukerens "matskap" kan være nok i en første versjon, uten å bygge full serverløsning før man vet konseptet fungerer

## Regulatoriske hensyn og personvern

Mattilsynet skiller mellom "best før" (kvalitet, ofte trygt å spise etter) og "siste forbruksdag" (sikkerhet, kritisk på ferskvarer som kjøtt, fisk og meieri) — appens varslingslogikk bør reflektere dette skillet tydelig, både for å unngå å gi utrygge råd og for å unngå å få folk til å kaste mat unødvendig, som ville undergravd hele poenget med appen.

Klimatall bør presenteres som anslag basert på kategorigjennomsnitt fra RISE, ikke som eksakte tall for akkurat den ene varen – vær tydelig på dette i appen for å unngå å fremstå villedende.

Data om husholdningens matskap er ikke særlig sensitiv persondata, men vanlig personvernhygiene – dataminimering og en tydelig personvernerklæring – gjelder likevel.

## MVP-omfang og veikart

1. Én kjernefunksjon først: skann, manuell holdbarhetsdato og varsel – uten klimaavtrykk i første versjon. Få selve matsvinn-nytten til å funke og test om folk faktisk bruker den daglig
2. Legg til klimaavtrykk per vare (koblet mot RISE-data) som differensierende funksjon i versjon 2, med enkel visualisering av "spart klimaavtrykk" over tid
3. Oppskriftsforslag basert på det som snart går ut
4. Samarbeid med Framtiden i våre hender er satt på vent inntil videre – ikke en del av nær-tidsplanen

## Forretningsmodell og åpne spørsmål

Siden dette er et hobbyprosjekt, er planen en engangssum ved kjøp av appen, uten abonnement eller løpende kostnad for brukeren etterpå. Arkitekturen bør støtte opp under dette: lokale påminnelser i stedet for serverbasert varsling, et klimadatasett som bunter med appen og oppdateres via app-oppdateringer, og oppslag direkte mot Open Food Facts sitt gratis API – da blir engangssummen også reelt kostnadsfri å drifte for deg, ikke bare gratis for brukeren etter kjøp.

Verdt å være obs på: en betalt nedlasting (du må betale før du har prøvd appen) gir typisk vesentlig færre nedlastinger og anmeldelser enn en gratis app, uavhengig av selve prisen – det demper synlighet og totalinntekt mer enn prismodellen i seg selv gjør. Et mellomalternativ som ofte fungerer bedre uten å gi slipp på "ingen løpende kostnad"-prinsippet: gratis nedlasting, med ett engangskjøp i appen for å låse opp full funksjonalitet.

Åpne spørsmål: hvor mye manuell registrering brukere er villige til å gjøre før appen føles som en byrde i stedet for en hjelp; og om Open Food Facts sin norske produktdekning er god nok til å starte uten en betalt GS1-lisens, som ville gitt en løpende kostnad denne modellen ellers unngår.
