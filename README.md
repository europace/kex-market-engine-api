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

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace/kex-market-engine-api/releases) zu finden.

## API Spezifikation

Request und Response sind in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) dokumentiert.

## Dokumentation

### Annahme

In einem KreditSmart Vorgang werden die Angebote zunächst von Europace ermittelt. Dabei wird die allgemeine Machbarkeit vorgeprüft, gegebenenfalls Anpassungen am Wunsch vorgenommen, 2/3 - Konditionen
ermittelt sowie die Vollständigkeit des Vorgangs sichergestellt.

Wenn alle notwendigen Daten vorhanden sind und die Vorprüfung erfolgreich war, kann die Annahme über die KEX Market Engine API erfolgen. Dabei wird <b>der Kundenwunsch</b>, also die vom Vermittler 
<b>erfassten (nicht angepassten)</b> Daten zum Finanzierungswunsch sowie die Antragstellerdaten an den Produktanbieter übermittelt.

Der Produktanbieter führt dann seinerseits alle für die Annahme des Angebots notwendigen Schritte durch:

#### Anpassung des Kundenwunsches

- Ist die Herausgabe eines Angebots zu den gewünschten Finanzierungskriterien nicht möglich, sollte eine Anpassung erfolgen, um ein machbares Angebot zu erzeugen
- Folgende Vorgaben können angepasst werden
    - Laufzeitvorgabe
    - Ratenvorgabe
    - Kreditbeträge
    - Versicherungskombinationen
    - Provisionen
- Zu jeder Anpassung muss eine Anpassungsmeldung generiert werden, um den Vermittler über die Anpassung zu informieren.
- siehe Felder <code>status.angepasst</code> und <code>meldungen</code>

#### Bonitätsprüfung der Antragsteller

- inklusive Übersicht der angerechneten Einnahmen sowie Ausgaben und des ermittelten Überschusses/Unterdeckung
- siehe Feld <code>bonitaetscheck</code>

#### Ermittlung der finalen Konditionen

- inklusive Tilgungsplan
- siehe Felder <code>kredit</code> und <code>tilgungsplan</code>

#### Votum über die Machbarkeit des Antrags

- inklusive Berücksichtigung der Scorings externer Anbieter z.B. Schufa
- Im Falle der Ablehnung, generierung einer Meldung mit Ablehnungsgrund
- siehe Felder <code>status</code> und <code>meldungen</code>

#### Ermittlung einzureichender Unterlagen
- siehe Feld <code>unterlagen</code>

#### Erstellung der Vertragsdokumente
- siehe Feld <code>dokumente</code>

#### Bereitstellung von Links zur digitialen Identifikation der Antragsteller

- Videolegitimation
- QES
- siehe Feld <code>identifikation</code>

### Integration der KEX Market Engine API in Europace

Die KEX Market Engine API wird vom Produktanbieter implementiert. Mit Hilfe des KEX Market Engine Service kann Europace das Produktangebot des Produktanbieters über die API in KreditSmart einbinden.

![](KEX%20Market%20Engine%20API%20Annahme%20Sequenzdiagramm.svg)

### API Referenz

Die implementierte Schnittstelle akzeptiert Daten mit Content-Type **application/json**.

#### Request

Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

Während der Angebotsermittlung wird bereits sichergestellt, dass die Antragsdaten vollständig sind. Dessen ungeachtet muss der Service mit fehlenden Daten umgehen können. Sie dürfen nicht zu einem
technischen Fehler führen.

#### Response

Die Antwort wird als JSON im Body der Repsonse erwartet.

Grundsätzlich wird eine Antwort mit einem vollständigen Angebot und HTTP-Statuscode **200 SUCCESS** erwartet. Wenn das Angebot **MACHBAR** ist, wird mindestens ein Dokument erwartet.

Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode **500** erwartet. Die Antwort darf kein Angebot enthalten, sollte aber einen Hinweis auf die Fehlerursache als <code>
supportMeldung</code> liefern.

##### Umgang mit unvollständigen Anfragen

Es wird ein vollständiges Angebot ohne Dokument(e) erwartet. Der Machbarkeitsstatus ist **NICHT_MACHBAR**. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

##### Umgang mit einer Unterdeckung in der Haushaltsrechnung

Ist der Antrag aufgrund einer Haushaltsunterdeckung nicht machbar, erfolgt im Idealfall eine Verlängerung der Laufzeit. Ist dies nicht möglich, kann ein Downselling des Auszahlungsbetrags erfolgen.

Führt das Downselling zu einem machbaren Angebot, wird dieses als <code>"angepasst": true</code> markiert und enthält entsprechende Anpassungsmeldungen, um den Vermittler über die Anpassung zu
informieren.

Ist ein Downselling nicht möglich, wird ein Angebot ohne Dokument(e) mit dem Status **NICHT_MACHBAR** und mindestens einer entsprechenden Machbarkeitsmeldung erwartet. Laufzeit und Kreditbetrag
sollten in diesem Fall der ursprünglichen Anfrage entsprechen.

##### Meldungen

Meldungen werden erzeugt, um den Vermittler Hinweise zur Durchführung und Machbarkeit des Antrags zu geben. Es werden folgende Kategorien unterschieden.

| Meldungskategorie  | Beschreibung | <code>machbarkeitsstatus</code>| <code>angepasst</code> |
|--------|--------|--------|--------|
| <code>MACHBARKEIT</code> | Der Antrag wird abgelehnt. | NICHT_MACHBAR| <i>kein Einfluß<i> |
| <code>VOLLSTAENDIGKEIT</code> | Der Antrag ist unvollständig und muss zur abschließenden Prüfung um fehlende Angaben ergänzt werden. | NICHT_MACHBAR| <i>kein Einfluß<i> | 
| <code>HINWEIS</code> | Hinweis an den Vermittler. | <i>kein Einfluß<i> | <i>kein Einfluß<i>|
| <code>ANPASSUNG</code> | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | MACHBAR | true | 

##### Status

| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. |
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschließend geprüft werden. Produktanbieter und Vermittler müssen den Antrag nachverhandeln.| 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. |

## Authentifizierung

Die Art und Weise der Authentifizierung wird zwischen dem Produktanbieter und Europace abgestimmt.

## Performance

Wir erwarten die Annahme-Antwort regelmäßig innerhalb von 30s. Bei einem deutlich höherem Wert, verschlechtert sich die Funktionalität unserer Plattform für andere Partner, z.B. Vertriebe.

## Beispiele

* [Erfolgreiche Annahme](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-erfolgreich.md)
* [Annahme mit fehlenden Daten](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-fehlenden-daten.md)
* [Annahme mit Unterdeckung](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-unterdeckung.md)
* [Annahme mit Downselling](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-downselling.md)
* [Annahme mit technischem Fehler](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-technischer-fehler-antwort-annahme.md)

## Nutzungsbedingungen

Die APIs werden unter folgenden [Nutzungsbedingungen](https://docs.api.europace.de/nutzungsbedingungen/) zur Verfügung gestellt
