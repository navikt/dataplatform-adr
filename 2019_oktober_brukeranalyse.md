# Brukeranalyse verktøy valg:

* Status: Under arbeid
* Deciders: Tobias McVey, Tommy Jocumsen, Christopher Kolstad
* Date: 2019-10-01

Technical Story: [description | ticket/issue URL] <!-- optional -->

## Context and Problem Statement

For at NAV skal kunne lage gode tjenester trenger vi innsikt om hvordan tjenester blir brukt. Hvilke produkter er enkle for brukere, og hvor møter de utfordringer? For å løse dette trenger vi verktøy til å gjøre målinger og innsamling av data enkelt. NAV har også ansvar for å sørge for at data som innsamles er i tråd med lover og regler for offentlige aktører, og må derfor tilpasse innsamling av data deretter.

Bør NAV velge å lage disse verktøyene selv, kjøpe fra leverandør-markedet, eller kombinere? Hvor langt bør NAV gå for å lage en god verktøykasse for egne ansatte, og bør NAV vurdere å lage noe som hele offentlig sektor skal kunne ta i bruk som Open Source Software? 

## Decision Drivers <!-- optional -->

* Manglende målinger: Det er flere tjenester i NAV som ikke har målinger på hvor mange brukere klarer å fullføre sine oppgaver. De trenger data for å forstå dagens bruksmønster, prioritere hvilke deler av tjenesten må forbedres, og lage hypoteser om hvordan produktet skal se ut i fremtiden.
* Smidig utvikling: NAV ønsker å drive smidig utvikling, men dette er vanskelig uten kvantitative data som en kilde til læring i avdelinger som utvikling, design og fagmiljøene.
* … <!-- numbers of drivers can vary -->

## Considered Options

* [Segment.com](https://segment.com)
* [Amplitude](https://amplitude.com)
* Egenutviklet
* [Rudder](https://github.com/rudderlabs/rudder-server)

## Decision Outcome

Chosen option: "[option 1]", because [justification. e.g., only option, which meets k.o. criterion decision driver | which resolves force force | … | comes out best (see below)].

### Positive Consequences <!-- optional -->

* [e.g., improvement of quality attribute satisfaction, follow-up decisions required, …]
* …

### Negative consequences <!-- optional -->

* [e.g., compromising quality attribute, follow-up decisions required, …]
* …

## Pros and Cons of the Options <!-- optional -->

### [option 1]

[Segment](https://segment.com) | Kundedataplattform og dataflyt

* Bra fordi verktøyet lar oss skrive samme SDK i alle applikasjoner uansett hvor data skal sendes. Dette gjør det enklere for utviklere å gjenbruke kode og kunnskap når de bytter produkt-team.
* Bra fordi verktøyet lar behandlingsansvarlig eie dataene sine og overføre de til et utvalg av populære tjenester for webanalyse som f.eks Google Analytics, Amplitude og Hotjar.
* Dårlig fordi verktøyet er dyrt og vil i lengden tilnærme seg kostnadene av et egetutviklet verktøy med samme formål og teknologi.

### [option 2]

[Amplitude](https://amplitude.com) | webanalyse-verktøy for produktutvikling

* Bra fordi verktøyet er hendelses-basert og lar utviklere innsamle og sette opp målinger med enkle spørringer i verktøyet. Verktøyet har en datamodell som er enkel å forholde seg til.
* Bra fordi verktøyet er bygget på moderne teknologier som gjør sammenstilling av data enkelt uansett hvilken teknologi det er laget med, f.eks nettsider, native-applikasjoner og applikasjoner som ikke er laget for internett.
* Dårlig fordi vi må skrive om innsamling av data fra produktene dersom vi bytter ut Amplitude, eller ønsker å bruke mer enn et verktøy. NAV bruker allerede flere verktøy som Google Analytics, Google Tag Manager, Hotjar, App Dynamics og Adrum. Mye av denne koden er i kodebasen til apper. Vi må ha en plan for å støtte flere verktøy, men det må være enkelt å endre koden som brukes til datainnsamling.

### [option 3]

[Rudder](https://github.com/rudderlabs/rudder-server) | åpen kilde verktøy for dataflyt i nettsky hos GCP, AWS og Azure

* Bra fordi et åpen kilde verktøy (Open Source Software) til å samle inn data og eie de i egen nettsky-konto hos f.eks Google lar NAV kontrollere fullstendig hvilke data samles inn i henhold til lovverk og egne behov
* Bra fordi NAV skal støtte åpen kilde 
* Dårlig fordi det vil kreve ressurser internt hos NAV til å drifte miljøet og utvikle det som mangler, f.eks å sende data til Hotjar. Dette er ressurser som NAV kan bruke til andre oppgaver.
* Dårlig fordi det bruker en ny lisens kalt Server Side Public License som kan være juridisk krevende dersom NAV oppfattes som konkurrent

## Links <!-- optional -->

* [Link type] [Link to ADR] <!-- example: Refined by [ADR-0005](0005-example.md) -->
* … <!-- numbers of links can vary -->
