# Brukeranalyse verktøy valg:

* Status: Under arbeid
* Deciders: Tobias McVey, Tommy Jocumsen, Christopher Kolstad
* Date: 2019-10-01

Technical Story: [description | ticket/issue URL] <!-- optional -->

## Context and Problem Statement


For at NAV skal kunne lage gode tjenester trenger vi innsikt om hvordan tjenester blir brukt. Hvilke produkter er enkle for brukere, og hvor møter de utfordringer? For å løse dette trenger vi verktøy til å gjøre målinger og innsamling av data enkelt. NAV har også ansvar for å sørge for at data som innsamles er i tråd med lover og regler for offentlige aktører, og må derfor tilpasse innsamling av data deretter. For eksempel må vi regne med at vi har flere vurderinger i fremtiden om planer for tjenesteutvikling i forhold til krav om personvern. Derfor er ikke alle spørsmål om dette temaet avklart på forhånd før vi inngår en avtale med leverandør.

Bør NAV velge å lage disse verktøyene selv, kjøpe fra leverandør-markedet, eller kombinere? Hvor langt bør NAV gå for å lage en god verktøykasse for egne ansatte, og bør NAV vurdere å lage noe som hele offentlig sektor kan ta i bruk som Open Source Software? 

Programvaren bør gjøre det enkelt å se hvordan brukere navigerer i en NAV-tjeneste og på tvers av tjenester. Typisk funksjonalitet for slike tjenester inkluderer å aggregere hvilke sider brukere har besøkt, å kunne sammenstille et hendelsesløp med flere steg i traktanalyser og måle endringer over tid. Det kan også være nyttig å eksportere rådata fra verktøyet for analyser, spesielt dersom NAV ønsker å sammenstille disse dataene med data fra andre kilder. 

## Decision Drivers <!-- optional -->

* Manglende målinger: Det er flere tjenester i NAV som ikke har målinger på hvor mange brukere klarer å fullføre sine oppgaver. De trenger data for å forstå dagens bruksmønster, prioritere hvilke deler av tjenesten må forbedres, og lage hypoteser om hvordan produktet skal se ut i fremtiden.
* Smidig utvikling: NAV ønsker å drive smidig utvikling, men dette er vanskelig uten kvantitative data som en kilde til læring i avdelinger som utvikling, design og fagmiljøene.
* … <!-- numbers of drivers can vary -->

## Considered Options

* SAAS [Segment.com](https://segment.com)
* SAAS [Amplitude](https://amplitude.com)
* SAAS [Google 360](https://marketingplatform.google.com/home)
* Egenutviklet
* OSS [Rudder](https://github.com/rudderlabs/rudder-server)
* OSS [Event Layer](https://github.com/kidGodzilla/event-layer)

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
* Dårlig fordi NAV bør først utføre en datavask før data sendes til Segment, og dette krever utvikling og drift av en proxy-løsning
* Dårlig fordi verktøyet er dyrt og vil i lengden tilnærme seg kostnadene av et egetutviklet verktøy med samme formål og teknologi.
* Dårlig fordi verktøyet ikke har innebygd måling av økter (sessions). Må kanskje utvikles hos NAV eller bruke en SDK i tillegg som f.eks Amplitude.

### [option 2]

[Amplitude](https://amplitude.com) | webanalyse-verktøy for produktutvikling

* Bra fordi verktøyet er hendelses-basert og lar utviklere innsamle og sette opp målinger med enkle spørringer i verktøyet. Verktøyet har en datamodell som er enkel å forholde seg til.
* Bra fordi verktøyet er bygget på moderne teknologier som gjør sammenstilling av data enkelt uansett hvilken teknologi det er laget med, f.eks nettsider, native-applikasjoner og applikasjoner som ikke er laget for internett. Støtter både web, native og har [HTTP API](https://help.amplitude.com/hc/en-us/articles/360032842391-HTTP-API-V2).
* Dårlig fordi NAV bør først utføre en datavask før data sendes til Amplitude, og dette krever utvikling og drift av en proxy-løsning
* Dårlig fordi vi må skrive om innsamling av data fra produktene dersom vi bytter ut Amplitude, eller ønsker å bruke mer enn et verktøy. NAV bruker allerede flere verktøy som Google Analytics, Google Tag Manager, Hotjar, App Dynamics og Adrum. Mye av denne koden er i kodebasen til apper. Vi bør ha en plan for å støtte flere verktøy, og det bør være enkelt å endre koden som brukes til datainnsamling.

### [option 3]

[Rudder](https://github.com/rudderlabs/rudder-server) | åpen kilde verktøy for dataflyt i nettsky hos GCP, AWS og Azure

* Bra fordi et åpen kilde verktøy (Open Source Software) som styres av NAV i sin egen konto hos f.eks Google Cloud lar NAV kontrollere fullstendig hvilke data samles inn i henhold til lovverk og egne behov
* Bra fordi verktøyet er et åpen kilde alternativ til Segment og  NAV skal støtte åpen kilde som prinsipp
* Dårlig fordi det vil kreve ressurser internt hos NAV til å drifte miljøet og utvikle det som mangler i forhold til produkter på markedet, f.eks å sende data til Hotjar. Dette er ressurser som NAV kan bruke til andre oppgaver. Man bør regne på om dette er billigere enn å betale for Segment når man tar driftskostnader og lønn til ansatte i betraktning.
* Dårlig fordi det bruker en ny lisens kalt Server Side Public License som kan være juridisk krevende dersom NAV oppfattes som konkurrent. Det pågår en [juridisk diskusjon](https://opensource.stackexchange.com/questions/7522/sspl-and-the-open-source-definition) om denne lisensen påfører brukere obligasjoner de ellers ikke ville hatt med lisenser som GPL og MIT. Så lenge NAV ikke oppfattes som konkurrent så skal denne lisensen være tilsvarende de fleste OSS lisenser, dvs. at de kan bruke lisensen fritt men med forventning om at de bidrar tilbake til prosjektet Rudder-server.

### [option 4]

[Event Layer](https://github.com/kidGodzilla/event-layer) | åpen kilde fork av Segment

* Bra fordi det er et enkelt åpenkilde bibliotek for å samle inn data fra nettsider til flere datakilder som Google Analytics og Amplitude
* Bra fordi det kan skreddersys til egne behov hos NAV.
* Dårlig fordi det kun støtte innsamling av data fra nettleser. Om det skal støtte fagsystemer og applikasjoner som ikke er laget for internett så må NAV utvikle et HTTP API for å sende data til Event Layer.
* Dårlig fordi det ikke støtter å sende data til leverandører som Hotjar. Hvis NAV bruker Event Layer så må vi utvikle dette selv.

### [option 5]

[Google 360](https://marketingplatform.google.com/home) | betalt versjon av Google Analytics

* Bra fordi det er et verktøy vi har mye erfaring med og som vil være enkelt å ta i bruk, og vi får flere verktøy inkludert som Google Optimize for AB-testing
* Bra fordi det støtter mange plattformer. Det kan brukes til å spore tradisjonelle og moderne web-applikasjoner og native-applikasjoner, og har et [HTTP API - measurement protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide)
* Dårlig fordi NAV bør først utføre en datavask før data sendes til Google Analytics, og dette krever utvikling og drift av en proxy-løsning
* Dårlig fordi vi må skrive om innsamling av data fra produktene dersom vi bytter ut Amplitude, eller ønsker å bruke mer enn et verktøy. NAV bruker allerede flere verktøy som Google Analytics, Google Tag Manager, Hotjar, App Dynamics og Adrum. Mye av denne koden er i kodebasen til apper. Vi bør ha en plan for å støtte flere verktøy, og det bør være enkelt å endre koden som brukes til datainnsamling.

## Links <!-- optional -->

* [Link type] [Link to ADR] <!-- example: Refined by [ADR-0005](0005-example.md) -->
* … <!-- numbers of links can vary -->
