# KEX Market Engine API

Die API ermöglicht es Produktanbietern im Ratenkreditgeschäft, ihr Kreditangebot über Services mit standardisierten Schnittstellen an die Europace Plattform anzubinden.

> Diese Schnittstelle wird kontinuierlich weiterentwickelt. Daher erwarten wir 
> von allen Nutzern dieser Schnittstelle, dass sie das "[Tolerant Reader Pattern](https://martinfowler.com/bliki/TolerantReader.html)" nutzen, d.h. 
> tolerant gegenüber kompatiblen API-Änderungen beim Lesen und Prozessieren der Daten sind:
>
> 1. unbekannte Felder dürfen keine Fehler verursachen
>
> 2. Strings mit eingeschränktem Wertebereich (Enums) müssen mit neuen, unbekannten Werten umgehen können
>
> 3. sinnvoller Umgang mit HTTP-Statuscodes, die nicht explizit dokumentiert sind  
>

<!-- https://opensource.zalando.com/restful-api-guidelines/#108 -->

# Inhaltsverzeichnis

* [API Version](https://github.com/europace/kex-market-engine-api#api-version)
* [Dokumentation](https://github.com/europace/kex-market-engine-api#dokumentation)
  * [API Spezifikation](https://github.com/europace/kex-market-engine-api#api-spezifikation)
  * [API Referenz](https://github.com/europace/kex-market-engine-api#api-referenz)
    * [Request](https://github.com/europace/kex-market-engine-api#request)
    * [Response](https://github.com/europace/kex-market-engine-api#response)
      * [Umgang mit unvollständigen Anfragen](https://github.com/europace/kex-market-engine-api#umgang-mit-unvollst%C3%A4ndigen-anfragen)
      * [Umgang mit einer Unterdeckung in der Haushaltsrechnung](https://github.com/europace/kex-market-engine-api#umgang-mit-einer-unterdeckung-in-der-haushaltsrechnung)
      * [Meldungskategorie](https://github.com/europace/kex-market-engine-api#meldungskategorie)
      * [Machbarkeitsstatus](https://github.com/europace/kex-market-engine-api#machbarkeitsstatus)
* [Authentifizierung](https://github.com/europace/kex-market-engine-api#authentifizierung)
* [Performance](https://github.com/europace/kex-market-engine-api#performance)
* [Beispiele](https://github.com/europace/kex-market-engine-api#beispiele)
* [Nutzungsbedingungen](https://github.com/europace/kex-market-engine-api#nutzungsbedingungen)

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace/kex-market-engine-api/releases) zu finden.

## Dokumentation

In einem KreditSmart Vorgang werden die Angebote zunächst von Europace ermittelt. Dabei wird die allgemeine Machbarkeit geprüft, 2/3 - Konditionen ermittelt sowie die Vollständigkeit des Vorgangs sichergestellt. 
Wenn alle notwendigen Daten vorhanden sind und die Vorprüfiung erfolgreich war, kann die Annahme über die KEX Market Engine API erfolgen.  

Die Annahme eines Antrags beinhaltet: 
- die Ermittlung der finalen Konditionen (inkl. Tilgungsplan),
- die Ermittlung einzureichender Unterlagen, 
- die Prüfung der Bonität der Antragsteller 
- ein Votum über die Machbarkeit des Antrags (inkl. Berücksichtigung der Scorings externer Anbieter z.B. Schufa) sowie
- die Erstellung der Vertragsdokumente.

Die KEX Market Engine API wird vom Produktanbieter implementiert. Mit Hilfe des KEX Market Engine Service kann Europace das Produktangbeot des Produktanbieters über die API in KreditSmart einbinden.  
 
![](KEX%20Market%20Engine%20API%20Annahme%20Sequenzdiagramm.svg)

### API Spezifikation

Request und Response sind in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) dokumentiert.

### API Referenz

Die implementierte Schnittstelle akzeptiert Daten mit Content-Type **application/json**.  

#### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

Während der Angebotsermittlung wird bereits sichergestellt, dass die Antragsdaten vollständig sind. Dessen ungeachtet muss der Service mit fehlenden Daten umgehen können. Sie dürfen nicht zu einem technischen Fehler führen. 

#### Response

Die Antwort wird als JSON im Body der Repsonse erwartet.

Grundsätzlich wird eine Antwort mit einem vollständigen Angebot und HTTP-Statuscode **200 SUCCESS** erwartet. Wenn das Angebot **MACHBAR** ist, wird mindestens ein Dokument erwartet.
Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. Die Antwort muss kein Angebot enthalten, aber einen Hinweis auf die Fehlerursache als supportMeldung.

##### Umgang mit unvollständigen Anfragen

Es wird ein vollständiges Angebot ohne Dokument(e) erwartet. Der Machbarkeitsstatus ist **NICHT_MACHBAR**. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

##### Umgang mit einer Unterdeckung in der Haushaltsrechnung

Ist der Antrag aufgrund einer Haushaltsunterdeckung nicht machbar, erfolgt im Idealfall eine Verlängerung der Laufzeit. Ist dies nicht möglich, kann ein Downselling des Auszahlungsbetrags erfolgen.

Führt das Downselling zu einem machbaren Angebot, wird dieses als angepasst = true markiert und enthält entsprechende Anpassungsmeldungen, um den Vermittler über die Anpassung zu informieren. 

Ist ein Downselling nicht möglich, wird ein Angebot ohne Dokument(e) mit dem Status **NICHT_MACHBAR** und mindestens einer entsprechenden Machbarkeitsmeldung erwartet. Laufzeit und Kreditbetrag sollten in diesem Fall der ursprünglichen Anfrage entsprechen.

##### Meldungskategorie

| Meldungskategorie  | Beschreibung |
|--------|--------|
| MACHBARKEIT | Der Antrag wird abgelehnt. | 
| VOLLSTAENDIGKEIT | Der Antrag ist unnvollständig und muss zur abschliessenden Prüfung um fehlende Angaben ergänzt werden. | 
| HINWEIS | Hinweis an den Vermittler. | 
| ANPASSUNG | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | 

##### Machbarkeitsstatus

| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. | 
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschliessend geprüft werden. Produktanbieter und Vermittler müssen den Antrag nachverhandeln.| 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. | 

## Authentifizierung

Die Art und Weise der Authentifizierung wird zwischen dem Produktanbieter und Europace abgestimmt. 

## Performance

Wir erwarten die Annahme-Antwort regelmässig innerhalb vonn 30s. Bei einem deutlich höherem Wert, verschlechtert sich die Funktionalität unserer Plattform für andere Partner, z.B. Vertriebe.

## Beispiele

* [Annahme erfolgreich](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-erfolgreich.md)
* [Annahme mit fehlenden Daten](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-fehlenden-daten.md)
* [Annahme mit Unterdeckung](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-unterdeckung.md)
* [Annahme mit Downselling](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-downselling.md)

## Nutzungsbedingungen
Die APIs werden unter folgenden [Nutzungsbedingungen](https://developer.europace.de/terms/) zur Verfügung gestellt
