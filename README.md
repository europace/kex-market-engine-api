# kex-market-engine-api
API zur Anbindung von Produktanbietern im Ratenkreditgeschäft.

Die Schnittstelle ermöglicht die Annahme von Ratenkredit-Angeboten.

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

# Table of Contents

* [API Version](#api-version)

## API Version

Die Version der API orientiert sich am [Semantic Versioning](https://semver.org/) und hat das Format

`MAJOR.MINOR.PATCH`

und ist in der [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) enthalten (`info.version`).

1. die `MAJOR` Version wird erhöht bei API inkompatiblen Änderungen (z.B. neue Pflichtangaben)
2. die `MINOR` Version wird erhöht bei abwärtskompatiblen API Änderungen (z.B. neue optionale Angaben)
3. die `PATCH` Version wird erhöht, wenn die API gleich bleibt, jedoch die Swagger Definition angepasst wird (z.B. Erweiterung oder Anpassung von Beschreibungen in der API)

Die aktuelle Version der API ist jeweils in den [Releases](https://github.com/europace/kex-market-engine-api/releases) zu finden.

## Response

### Meldungskategorie
| Meldungskategorie  | Beschreibung |
|--------|--------|
| MACHBARKEIT | Der Antrag wird abgelehnt. | 
| VOLLSTAENDIGKEIT | Der Antrag ist unnvollständig und muss zur abschliessenden Prüfung, um fehlende Angaben ergänzt werden. | 
| HINWEIS | Hinweis an den Vermittler. | 
| ANPASSUNG | Information über eine Anpassung des Kundenwunsches, z.B. Rate, Auszahlungsbetrag oder Versicherungswunsch. | 

### Machbarkeitsstatus
| Machbarkeitsstatus  | Beschreibung |
|--------|--------|
| MACHBAR | Dem Antrag kann entsprochen werden. | 
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | Der Antrag konnte nicht abschliessend geprüft werden. | 
| NICHT_MACHBAR | Der Antrag wurde abgelehnt. | 

### Tilgungsplan
in der Regel werden die Zahlungsperioden nur während des ersten (und ggf. des letzten) Jahres monatlich ausgewiesen. Die folgenden Perioden werden auf Jahresebene aggregiert, um den Tilgungsplan kurz zu halten.

## Beispiele

* [Annahme](beispiele/example-annahme.md)

