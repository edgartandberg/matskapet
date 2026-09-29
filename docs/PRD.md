# Matskapet – PRD

Sep 29, 2026 · @Edgar

## Bakgrunn og formål

Denne PRD-en bygger videre på den tidligere prosjektskissen «Matsvinn- og klimaapp», som dekket kjernen i Matskapet: strekkodeskanning, manuell holdbarhetsregistrering, og et klimaavtrykk-regnskap. Denne fasen legger til tre nye funksjoner — kvitteringsskanning, foto av oppskrifter/ingredienslister, og en kuratert oppskriftsbank — som til sammen kobler matskapet tættere på selve matlagingen, ikke bare oversikten over hva som ligger der.

## Mål for denne fasen

- Redusere friksjonen ved registrering — kvitteringsskanning som alternativ til å skanne hver vare enkeltvis
- Koble matskapet direkte til matlaging, ikke bare til oversikt: oppskrifter blir til handlelister, og handlelistene tar hensyn til det du allerede har
- Bygge et gjenkjennelig, kuratert opplevelseslag (oppskriftsbanken) som skiller appen fra rene matsvinn-trackere

## Brukerhistorier

1. Som bruker vil jeg skanne strekkoden på en vare for å legge den raskt i matskapet med riktig holdbarhetstype (videreført fra forrige fase).
2. Som bruker vil jeg ta bilde av kvitteringen etter en handletur, slik at varene automatisk dukker opp i matskapet uten at jeg må registrere hver enkelt manuelt.
3. Som bruker vil jeg ta bilde av en oppskrift — fra en bok, et blad, eller et skjermbilde — og få ingrediensene lagt til i handlelisten.
4. Som bruker vil jeg bla i en kuratert oppskriftsbank, hake av oppskrifter jeg vil lage denne uken, og få én samlet handeliste for alle valgte oppskrifter.
5. Som bruker vil jeg fortsatt få varsel når noe i matskapet snart går ut, og se klimaavtrykket av det jeg bruker opp versus kaster.

## F1 – Matskap-oversikt (videreført)

Kjernen fra forrige fase er uendret i denne omgang: strekkodeskanning eller manuell registrering, holdbarhetstype (best før / siste forbruksdag), oversikt sortert på hastegrad, og et løpende klimaavtrykk-regnskap for brukt opp versus kastet. De tre nye funksjonene under (F2–F4) er nye veier INN til og UT AV det samme matskapet — selve matskap-modellen endres ikke i denne fasen.

## F2 – Kvitteringsskanning

Bruker tar bilde av kvitteringen rett etter en handletur. Appen leser varelinjene med tekstgjenkjenning (OCR) og forsøker å matche hver linje mot en produktkategori og et rimelig holdbarhets-anslag — f.eks. «KYLLFILE» → fjørfe-kategori, standard holdbarhet noen dager fra kjøpsdato.

Viktig forbehold: kvitteringstekst er ofte butikkspesifikke forkortelser, ikke fulle produktnavn — automatisk matching blir aldri 100 % treffsikker. Løsningen bør derfor alltid ha et bekreftelsessteg der bruker raskt kan godkjenne, rette eller fjerne linjer FØR de legges i matskapet, ikke legge dem inn blindt.

Foreslått teknisk tilnærming: bruk en ferdig kvitterings-OCR-tjeneste (f.eks. Tabscanner, Klippa eller Microblink, som alle er spesialisert på nettopp linjevis gjenkjenning av dagligvarekvitteringer) fremfor å bygge egen OCR fra bunnen av. Kvitteringen sier ikke noe om holdbarhet — appen má sette et fornuftig standardanslag per kategori (som allerede finnes i klimadatasettet fra F1) og la bruker justere det.

## F3 – Foto av oppskrift/ingrediensliste → handeliste

Bruker fotograferer en ingrediensliste — fra en kokebok, et blad, eller et skjermbilde av en nettside — og appen leser teksten med OCR og tolker den til en strukturert liste med mengder og ingredienser, som legges til i en samlet handeliste.

Dette er en velprøvd funksjon i etablerte apper som Samsung Food (offisielt tilgjengelig i Norge) og Paprika Recipe Manager — altså ikke en ny idé i seg selv, men en forventet funksjon å tilby når man først har en matlagingsapp. Differensieringen ligger i at handlelisten her kan kryssjekkes mot det man allerede HAR i matskapet (fra F1/F2), slik at appen filtrerer bort det du allerede eier — noe de generelle oppskriftsappene ikke gjør, siden de ikke kjenner innholdet i skapet ditt.

Teknisk: å tolke fritekst-ingredienslinjer («2 dl melk», «3 fedd hvitløk») til strukturerte data (mengde, enhet, ingrediens) er et kjent NLP-problem uten perfekt løsning — forvent at bruker må rydde opp i handelisten iblant, særlig for uvanlige mål og enheter.

## F4 – Kuratert oppskriftsbank

En kuratert samling oppskrifter — redaksjonelt utvalgt, ikke skrapet fra hele internett — inspirert av den britiske appen Mob, som nå har sin egen app med kuraterte oppskrifter, måltidsplaner og et premium-abonnement, i tillegg til nettsiden. Bruker blar i oppskriftsbanken, haker av oppskrifter for uken, og appen slår sammen ingredienslistene fra alle valgte oppskrifter til én handleliste — med samme mulighet som i F3 til å filtrere bort det man allerede har i matskapet.

Dette krever et redaksjonelt arbeid i seg selv — noen må velge og strukturere oppskriftene — som er en helt annen type arbeid enn resten av appen. Dette bør trolig starte smått, med et titalls oppskrifter lagt inn manuelt, fremfor å bygges som en skalerbar redaksjonspipeline fra dag én.

## Konkurranselandskap for de nye funksjonene

Samsung Food og Paprika Recipe Manager dekker allerede oppskrift-skanning og handlelistegenerering godt, og Samsung Food er offisielt tilgjengelig i Norge. Mob har sin egen app med kuraterte oppskrifter og måltidsplaner. På kvitteringssiden finnes det flere etablerte OCR-tjenester spesialisert på nettopp dagligvarekvitteringer (Tabscanner, Klippa, Microblink).

Ingen av disse kombinerer dette med et faktisk matskap med holdbarhet og klimaavtrykk, koblet til kvitteringsskanning — det er fortsatt her helheten skiller seg fra hver enkeltdel. Men det betyr også at hver enkeltfunksjon i denne PRD-en isolert sett konkurrerer med etablerte, godt finansierte apper. Verdien må komme fra helheten, ikke fra én enkelt funksjon alene.

## Ikke-mål og avgrensning

- Ikke bygge egen OCR-motor fra bunnen — bruk tredjeparts API-er
- Ikke forsøk på 100 % automatisk, feilfri gjenkjenning fra kvittering eller oppskriftsfoto — et bekreftelses-/rettesteg er en forutsetning, ikke en snarvei å fjerne senere
- Ikke en åpen, brukergenerert oppskriftsplattform i denne fasen — oppskriftsbanken er kuratert og liten til å begynne med
- Ikke «hva kan jeg lage av det jeg har»-motoren (omvendt matching fra matskap til oppskrift) i denne fasen, selv om det er en naturlig fremtidig utvidelse

## Tekniske betraktninger på tvers

- **Datamodell:** en handeliste må kunne hente rader fra flere kilder (F2 kvittering → matskap direkte, F3 oppskriftsfoto → handeliste, F4 oppskriftsbank → handeliste). Disse bør normaliseres til samme ingrediens-/kategoristruktur som allerede finnes i klimadatasettet fra F1, slik at et element fra en hvilken som helst kilde kan vises med riktig holdbarhetsanslag og klimatall.
- **OCR-leverandør:** vurder én leverandør for begge bruksområder (kvittering og oppskrift-tekst) fremfor to ulike integrasjoner, hvis én dekker begge godt nok.
- **Matching-laget** (tekst → kategori/produkt) er i praksis det vanskeligste og mest verdifulle tekniske stykket i hele denne fasen — vurder å bygge og teste dette isolert før resten av UI-et.
- **Personvern:** bilder av kvitteringer kan inneholde mer enn varelinjer (butikknavn, betalingsinfo, tidspunkt). Vurder å beskjære eller ignorere alt annet enn varelinjene før noe lagres, og vær tydelig i personvernerklæringen på at kvitteringsbilder behandles for gjenkjenning, ikke lagres rå med mindre bruker ber om det.

## Avhengigheter, risiko og åpne spørsmål

De fleste kvitterings- og oppskrift-OCR-API-er tar betalt per skann — noe som er i direkte spenning med «ingen løpende kostnad»-prinsippet fra forrige fase. Dette bør avklares før F2/F3 bygges, ikke etterpå.

Åpne spørsmål: hvem kuraterer oppskriftsbanken, og hvor mye tid er realistisk å bruke på dette som hobbyprosjekt? Skal kvitteringsskanning støtte flere kjeder (Rema, Kiwi, Coop, Meny) med ulike kvitteringsformat, eller starte med én?

Risiko: for mange inntaksmåter (strekkode, kvittering, oppskriftsfoto, oppskriftsbank) kan gjøre appen kompleks å bruke. Vurder å teste én ny funksjon om gangen med ekte bruk, fremfor — bygge alle fire samtidig.

## Foreslått rekkefølge / faseplan

&#91;embedded content: faseplan · 3 steg + 1 fremtidig fase\]

Kvitteringsskanning (F2) bør komme først siden den bygger direkte på matskap-modellen fra forrige fase. Oppskriftsfoto (F3) gjenbruker samme OCR- og matching-lag. Oppskriftsbanken (F4) kan bygges uavhengig av OCR-arbeidet, men kryssjekk mot matskapet bør vente til F1–F2 er solide. Den omvendte krysningen — hva du kan lage av det du har — er en egen, senere fase.
