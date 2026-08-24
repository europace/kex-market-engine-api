## Example: Annahme mit Kommunikationsangaben

Es handelt sich um ein Beispiel zum besseren Verständnis der API.

In diesem Beispiel werden die Kommunikationsangaben gemäß Verbraucherkreditrichtlinie 2 (VKRL2 / CCD2)
übermittelt. Sie werden je Antragsteller separat erfasst und können sich zwischen den Antragstellern
unterscheiden - hier wählt Antragstellerin 1 überwiegend den digitalen Weg, Antragsteller 2 überwiegend
den Weg in Papierform.

Der Wert `DIGITAL_PAPIER` ist ausschließlich für `bereitstellungswegSecci` zulässig. Er bedeutet, dass die
Bank-VVI (SECCI) in Papierform **und zusätzlich** digital bereitgestellt werden muss. Für alle anderen
Kommunikationswege stehen nur `DIGITAL` und `PAPIER` zur Verfügung.

Zusätzlich enthält das Beispiel die `registrierungsnummer34k` des Kundenbetreuers.

## Table of Contents

* [Request](#request)
* [Response](#response)

### Request

```json
{
  "traceId": "ks-7fq2m814",
  "vorgangsnummer": "GE0203",
  "antragsnummer": "GE0203/1/1",
  "angebotsvariantentyp": "eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6IlJBVEVOS1JFRElUIiwicHJvZHV6ZW50IjoiU1BJVFpFTkJBTksifX0=",
  "antragsteller": [
    {
      "id": "eb51059a-ab2d-4253-9a7b-61864ae17123",
      "haushaltspartnerId": "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477",
      "persoenlicheAngaben": {
        "geschlecht": "WEIBLICH",
        "vorname": "Antonia",
        "nachname": "Meise",
        "geburtsdatum": "1980-03-02",
        "geburtsort": "Berlin",
        "geburtsland": "DE",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET",
        "anzahlPersonenImHaushalt": 2
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "ANGESTELLT",
        "beschaeftigungsbeginn": "2020-04-15",
        "beruf": "Angestellte",
        "arbeitgeber": {
          "name": "Topjob AG",
          "anschrift": {
            "strasse": "Heidestraße",
            "hausnummer": "8",
            "postleitzahl": "10557",
            "ort": "Berlin",
            "land": "DE"
          }
        },
        "branche": "DIENSTLEISTUNGEN"
      },
      "derzeitigeWohnsituation": {
        "wohnart": "ZUR_MIETE",
        "wohnhaftSeit": "2020-03-01",
        "anschrift": {
          "strasse": "Kurfürstendamm",
          "hausnummer": "1",
          "postleitzahl": "10115",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "+49305293909",
        "email": "toni.m@fiktivedomain.de"
      },
      "legitimation": {
        "ausweisart": "PERSONALAUSWEIS",
        "ausweisnummer": "ZJ86XCJNBX7CBB",
        "ausstellendeBehoerde": "Bezirksamt Mitte",
        "ausstellungsdatum": "2018-07-19",
        "ausstellungsort": "Berlin"
      },
      "bonitaetsangaben": {
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 1989.84
          }
        },
        "monatlicheAusgaben": {
          "eigenmieteInklusiveNebenkosten": 1081.51
        }
      },
      "kommunikationsangaben": {
        "bereitstellungswegSecci": "DIGITAL_PAPIER",
        "kommunikationswegNachVertragsschluss": "DIGITAL",
        "kommunikationswegHinweisWiderrufsfrist": "DIGITAL",
        "widerrufsweg": "DIGITAL"
      }
    },
    {
      "id": "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477",
      "haushaltspartnerId": "eb51059a-ab2d-4253-9a7b-61864ae17123",
      "persoenlicheAngaben": {
        "geschlecht": "MAENNLICH",
        "vorname": "Bernd",
        "nachname": "Meise",
        "geburtsdatum": "1977-11-19",
        "geburtsort": "Potsdam",
        "geburtsland": "DE",
        "staatsangehoerigkeit": "DE",
        "familienstand": "VERHEIRATET",
        "anzahlPersonenImHaushalt": 2
      },
      "derzeitigeBeschaeftigung": {
        "beschaeftigungsverhaeltnis": "BEAMTER",
        "beschaeftigungsbeginn": "2011-09-01",
        "beruf": "Lehrer",
        "arbeitgeber": {
          "name": "Land Berlin",
          "anschrift": {
            "strasse": "Bernhard-Weiß-Straße",
            "hausnummer": "6",
            "postleitzahl": "10178",
            "ort": "Berlin",
            "land": "DE"
          }
        },
        "branche": "ERZIEHUNG_UNTERRICHT"
      },
      "derzeitigeWohnsituation": {
        "wohnart": "ZUR_MIETE",
        "wohnhaftSeit": "2020-03-01",
        "anschrift": {
          "strasse": "Kurfürstendamm",
          "hausnummer": "1",
          "postleitzahl": "10115",
          "ort": "Berlin",
          "land": "DE"
        }
      },
      "kontakt": {
        "telefonPrivat": "+49305293909",
        "email": "bernd.m@fiktivedomain.de"
      },
      "legitimation": {
        "ausweisart": "PERSONALAUSWEIS",
        "ausweisnummer": "TK41QWNMZP2XAA",
        "ausstellendeBehoerde": "Bezirksamt Mitte",
        "ausstellungsdatum": "2019-02-04",
        "ausstellungsort": "Berlin"
      },
      "bonitaetsangaben": {
        "einnahmen": {
          "monatlicheEinnahmen": {
            "regelmaessigesUnselbstaendigesEinkommen": 2450.00
          }
        }
      },
      "kommunikationsangaben": {
        "bereitstellungswegSecci": "PAPIER",
        "kommunikationswegNachVertragsschluss": "PAPIER",
        "kommunikationswegHinweisWiderrufsfrist": "DIGITAL",
        "widerrufsweg": "PAPIER"
      }
    }
  ],
  "gemeinsameAntragstellerangaben": {
    "bonitaetsangaben": {}
  },
  "finanzierungswunsch": {
    "kreditwunsch": {
      "finanzierungszweck": "MODERNISIERUNG_UND_WOHNEN",
      "verwendung": "Neue Küche",
      "auszahlungsbetrag": 15000,
      "ratenzahlungstermin": "MONATSENDE",
      "laufzeitInMonaten": 60
    },
    "versicherungswunsch": [
      {
        "antragstellerId": "eb51059a-ab2d-4253-9a7b-61864ae17123",
        "tod": true,
        "arbeitsunfaehigkeit": true,
        "arbeitslosigkeit": false
      },
      {
        "antragstellerId": "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477",
        "tod": true,
        "arbeitsunfaehigkeit": false,
        "arbeitslosigkeit": false
      }
    ]
  },
  "konto": {
    "kreditinstitut": "Musterbank",
    "kontoinhaberIds": [
      "eb51059a-ab2d-4253-9a7b-61864ae17123",
      "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477"
    ],
    "iban": "DE72100500005985478128",
    "bic": "BELADEBEXXX"
  },
  "kundenbetreuer": {
    "partnerId": "EZ556",
    "vertriebsorganisationsId": "POOL",
    "firma": "Vermittler oHG",
    "vorname": "Manfred",
    "nachname": "Talent",
    "anschrift": {
      "strasse": "Am Platz",
      "hausnummer": "42",
      "postleitzahl": "10247",
      "ort": "Berlin"
    },
    "telefon": "030-6598714",
    "email": "manfred.talent@vermittlerohg.de",
    "anrede": "HERR",
    "registrierungsnummer34k": "D-W-34K-1A2B3-45"
  },
  "vertriebskanal": "B2B",
  "bearbeiter": {
    "vorname": "Susanne",
    "nachname": "Korrekt"
  },
  "handelsbeziehung": {
    "produktanbieter": "BEISPIEL_BANK",
    "kreditprovisionswunsch": 0.0123,
    "vertriebsgruppe": "Beispielgruppe"
  },
  "beratungsart": "FERN_ABSATZ_GESCHAEFT"
}
```

### Response

Die Kommunikationsangaben wirken sich nicht auf die Struktur der Antwort aus. Die Antwort ist hier
gekürzt dargestellt - Bonitätscheck und Tilgungsplan sind ausgelassen.

```json
{
  "angebot": {
    "produktanbieter": "MUSTERBANK",
    "referenznummerProduktanbieter": "XVG456",
    "referenznummerDienstleister": null,
    "produktbezeichnung": "Top Ratenkredit Modernisierung",
    "produktart": "MODERNISIERUNGSKREDIT",
    "angebotsvariantentyp": "eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6IlJBVEVOS1JFRElUIiwicHJvZHV6ZW50IjoiU1BJVFpFTkJBTksifX0=",
    "kredit": {
      "vertragsbeginn": "2026-10-01",
      "effektivzinssatz": 0.0641,
      "sollzinssatz": 0.0623,
      "gesamtbetrag": 17520.6,
      "nettokreditbetrag": 15000,
      "auszahlungsbetrag": 15000,
      "laufzeitInMonaten": 60,
      "rateProMonat": 292.01,
      "letzteRate": 291.99,
      "provisionsbetrag": 184.5,
      "vorlaufzinsenProTag": 2.56
    },
    "status": {
      "machbarkeitsstatus": "MACHBAR",
      "angepasst": false
    },
    "meldungen": [
      {
        "kategorie": "HINWEIS",
        "text": "Die Bank-VVI wird für Antragstellerin 1 zusätzlich digital bereitgestellt.",
        "code": "bank.hinweis.secci.zusaetzlich.digital"
      }
    ],
    "unterlagen": [
      {
        "code": "bank.unterlage.gehaltsnachweis",
        "text": "Bitte legen Sie die Gehaltsnachweise der letzten 3 Monate vor.",
        "referenz": {
          "id": "eb51059a-ab2d-4253-9a7b-61864ae17123",
          "art": "ANTRAGSTELLER"
        }
      },
      {
        "code": "bank.unterlage.gehaltsnachweis",
        "text": "Bitte legen Sie die Gehaltsnachweise der letzten 3 Monate vor.",
        "referenz": {
          "id": "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477",
          "art": "ANTRAGSTELLER"
        }
      }
    ],
    "maximalerAuszahlungsbetrag": 18000
  },
  "dokumente": [
    {
      "dateiname": "Europaeische_Standardinformationen.pdf",
      "base64pdf": "foobar8765436765765454565675",
      "sichtbarkeit": {
        "sichtbarFuerVertrieb": true,
        "sichtbarFuerProduktanbieter": true
      }
    },
    {
      "dateiname": "Darlehensvertrag.pdf",
      "base64pdf": "foobar8765436765765454565675",
      "sichtbarkeit": {
        "sichtbarFuerVertrieb": true,
        "sichtbarFuerProduktanbieter": true
      }
    }
  ],
  "identifikation": [
    {
      "antragstellerId": "eb51059a-ab2d-4253-9a7b-61864ae17123",
      "videolegitimationUrl": "http://videolegi-provider.de/34567876543567",
      "qesUrl": "http://qes-provider.de/34567876543567"
    },
    {
      "antragstellerId": "c7a4410d-93f1-4a8e-8d21-5f0b2c9e4477",
      "videolegitimationUrl": "http://videolegi-provider.de/98765432109876",
      "qesUrl": "http://qes-provider.de/98765432109876"
    }
  ]
}
```