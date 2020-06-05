# kex-market-engine-api
Die API ermöglicht es Produktanbietern im Ratenkreditgeschäft, ihr Kreditangebot über Services mit standardisierten Schnittstellen an die Europace Plattform anzubinden.
Services, die die API implementieren, erwarten einen POST-Request mit einem JSON-Dokument als Request-Body.

![](KEX%20Market%20Engine%20API%20Annahme%20Sequenzdiagramm.svg)

> :warning: Diese Schnittstelle wird kontinuierlich weiterentwickelt. Daher erwarten wir 
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

* [API Version](#api-version)
* [Annahme](#Annahme)
* [Beispiele](#Beispiele)

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/), hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace/kex-market-engine-api/releases) zu finden.

## Annahme

Die Annahme eines Antrags beinhaltet: 
- die Ermittlung der Konditionen (inkl. Tilgungsplan),
- die Ermittlung einzureichender Unterlagen, 
- die Prüfung der Bonität der Antragsteller 
- ein Votum über die Machbarkeit des Antrags (inkl. Berücksichtigung der Scorings externer Anbieter z.B. Schufa) sowie
- die Erstellung der Vertragsdokumente.

### Performance

Wir erwarten die Antwort regelmässig innerhalb vonn 30s. Bei einem deutlich höherem Wert, verschlechtert sich die Funktionalität unserer Plattform für andere Partner, z.B. Vertriebe.

### Request

Während der Angebotsermittlung wird bereits sichergestellt, dass die Antragsdaten vollständig sind. Dessen ungeachtet muss der Service mit fehlenden Daten umgehen können. Sie dürfen nicht zu einem technischen Fehler führen. 

### Response

Grundsätzlich wird eine Antwort mit einem vollständigen Angebot und HTTP-Statuscode 200 erwartet. Wenn das Angebot MACHBAR ist, wird mindestens ein Dokument erwartet.
Im Falle eines technischen Fehlers wird eine Antwort mit HTTP-Statuscode 500 erwartet. Die Antwort muss kein Angebot enthalten, aber einen Hinweis auf die Fehlerursache als supportMeldung.

#### Umgang mit unvollständigen Anfragen

Es wird ein vollständiges Angebot ohne Dokument(e) erwartet. Der Machbarkeitsstatus ist NICHT_MACHBAR. Es sind Vollständigkeitsmeldungen vorhanden, die auf die fehlenden Angaben hinweisen.

#### Umgang mit einer Unterdeckung in der Haushaltsrechnung

Ist der Antrag aufgrund einer Haushaltsunterdeckung nicht machbar, erfolgt im Idealfall eine Verlängerung der Laufzeit. Ist dies nicht möglich, kann ein Downselling des Auszahlungsbetrags erfolgen.

Führt das Downselling zu einem machbaren Angebot, wird dieses als angepasst = true markiert und enthält entsprechende Anpassungsmeldungen, um den Vermittler über die Anpassung zu informieren. 

Ist ein Downselling nicht möglich, wird ein Angebot ohne Dokument(e) mit dem Status NICHT_MACHBAR und mindestens einer entsprechenden Machbarkeitsmeldung erwartet. Laufzeit und Kreditbetrag sollten in diesem Fall der ursprünglichen Anfrage entsprechen.

#### Meldungskategorie

| Meldungskategorie  | Beschreibung |
|--------|--------|
| MACHBARKEIT | Der Antrag wird abgelehnt. | 
| VOLLSTAENDIGKEIT | Der Antrag ist unnvollständig und muss zur abschliessenden Prüfung um fehlende Angaben ergänzt werden. | 
| HINWEIS | Hinweis an den Vermittler. | 
| ANPASSUNG | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | 

#### Machbarkeitsstatus

| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. | 
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschliessend geprüft werden. Produktanbieter und Vermittler müssen den Antrag nachverhandeln.| 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. | 

## Beispiele

* [Annahme erfolgreich](beispiele/example-annahme-erfolgreich.md)
* [Annahme mit fehlenden Daten](beispiele/example-annahme-mit-fehlenden-daten.md)
* [Annahme mit Unterdeckung](beispiele/example-annahme-mit-unterdeckung.md)
* [Annahme mit Downselling](beispiele/example-annahme-mit-downselling.md)
