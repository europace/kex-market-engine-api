## Annahme-Request

Es handelt sich um ein Beispiel zum besseren Verständnis der API. 

## Table of Contents

* [Request](#request)
* [Response](#response)

### Request

```json
{
    "traceId": "ks-95i5t397",
    "vorgangsnummer": "GE0203",
    "antragsnummer": "GE0203/1/1",
    "angebotsvariantentyp": "eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6IlBST0RVS1RfSUQiLCJwcm9kdXplbnQiOiJTUElUWkVOQkFOSyJ9fQ==",
    "antragsteller": [
        {
            "id": "eb51059a-ab2d-4253-9a7b-61864ae17123",
            "persoenlicheAngaben": {
                "geschlecht": "WEIBLICH",
                "vorname": "Antonia",
                "nachname": "Meise",
                "geburtsdatum": "1980-03-02",
                "geburtsort": "Berlin",
                "geburtsland": "DE",
                "staatsangehoerigkeit": "DE",
                "familienstand": "LEDIG",
                "anzahlPersonenImHaushalt": 3
            },
            "derzeitigeBeschaeftigung": {
                "beschaeftigungsverhaeltnis": "ANGESTELLT",
                "befristet": "BEFRISTET",
                "beschaeftigungsbeginn": "2020-04-15",
                "befristetBis": "2020-12-31",
                "beruf": "Angestellter",
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
            "vorherigeBeschaeftigung": {
                "beschaeftigungsbeginn": "2016-01-01",
                "beschaeftigungsende": "2020-01-30",
                "arbeitgeber": {
                    "name": "EXJOB GmbH",
                    "anschrift": {
                        "strasse": "Klosterstraße",
                        "hausnummer": "71",
                        "postleitzahl": "10179",
                        "ort": "Berlin",
                        "land": "DE"
                    }
                }
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
            "vorherigeWohnsituation": {
                "wohnhaftSeit": "1980-03-02",
                "anschrift": {
                    "strasse": "Dunckerstraße",
                    "hausnummer": "21",
                    "postleitzahl": "10437",
                    "ort": "Berlin",
                    "land": "DE"
                }
            },
            "kontakt": {
                "telefonPrivat": "+49305293909",
                "telefonGeschaeftlich": "0171 659824",
                "email": "toni.m@fiktivedomain.de"
            },
            "aufenthaltsstatus": {
                "aufenthaltstitel": {}
            },
            "kinder": [
                {
                    "id": "uw54322a-ba1r-8770-7b7a-61864no65982",
                    "kindergeldBerechtigt": true
                },
                {
                    "id": "pl66546a-bu1z-3331-99j0-khg85xnol494",
                    "kindergeldBerechtigt": false
                }
            ],
            "anzahlPkw": "1",
            "rentenversicherung": {
                "anschrift": {}
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
                        "regelmaessigesUnselbstaendigesEinkommen": 1989.84,
                        "kindesunterhalt": 395.12,
                        "kindergeld": 408,
                        "nebentaetigkeiten": [
                            {
                                "betrag": 400,
                                "beginn": "2017-02-01"
                            }
                        ],
                        "mietUndPachteinnahmen": {}
                    },
                    "jaehrlicheEinnahmen": {
                        "einkommenAusSelbstaendigkeit": {
                            "zuVersteuerndesEinkommen": {},
                            "einkommenssteuer": {},
                            "abschreibungen": {}
                        }
                    }
                },
                "monatlicheAusgaben": {
                    "eigenmieteInklusiveNebenkosten": 1081.51,
                    "sonstigeAusgaben": 65
                },
                "vermoegen": {
                    "rueckkaufswertLebensversicherung": 741.51,
                    "immobilien": []
                },
                "verbindlichkeiten": {
                    "ratenkredite": [
                        {
                            "id": "lkmjhuyg7-9876-gy6z-09ik-jihyf5anbhv65v",
                            "monatlicheRate": 175.95,
                            "letzteRate": 150.66,
                            "datumLetzteRate": "2027-03-31",
                            "restschuld": 5007.61,
                            "glaeubiger": "MUSTER SPARKASSE"
                        }
                    ],
                    "sonstigeVerbindlichkeiten": [],
                    "leasings": [],
                    "kreditkarten": [],
                    "dispositionskredite": [
                        {
                            "id": "bii9876ghj-ab2d-6595-ok08-61864ae87654f",
                            "verfuegungsrahmen": 8000,
                            "beanspruchterBetrag": 8120.69,
                            "zinssatz": 0.1369,
                            "glaeubiger": "MUSTERBANK"
                        }
                    ],
                    "immobiliendarlehen": [],
                    "geschaeftskredite": [],
                    "kontokorrentkredite": []
                }
            }
        }
    ],
    "gemeinsameAntragstellerangaben": {
        "bonitaetsangaben": {}
    },
    "finanzierungswunsch": {
        "kreditwunsch": {
            "finanzierungszweck": "SONSTIGES",
            "verwendung": "Autoreparatur, Schulranzen und Urlaub",
            "auszahlungsbetrag": 10000,
            "ratenzahlungstermin": "MONATSENDE",
            "laufzeitInMonaten": 72
        },
        "versicherungswunsch": [
            {
                "antragstellerId": "eb51059a-ab2d-4253-9a7b-61864ae17123",
                "tod": true,
                "arbeitsunfaehigkeit": true,
                "arbeitslosigkeit": false
            }
        ],
        "abzuloesendeVerbindlichkeiten": {
            "ratenkredite": [],
            "sonstigeVerbindlichkeiten": [],
            "kreditkarten": [],
            "dispositionskredite": [],
            "geschaeftskredite": []
        },
        "fahrzeug": {}
    },
    "konto": {
        "kreditinstitut": "Musterbank",
        "kontoinhaberIds": [
            "eb51059a-ab2d-4253-9a7b-61864ae17123"
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
        "fax": "030-65987141",
        "email": "manfred.talent@vermittlerohg.de",
        "iban": "DE752012070031009854090",
        "anrede": "HERR"
    },
    "featureToggles": [
        {
            "id": "BANKANBINDUNG",
            "aktiv": "true"
        }
    ],
    "bearbeiter": {
        "vorname": "Susanne",
        "nachname": "Korrekt"
    },
    "handelsbeziehung": {
        "produktanbieter": "BEISPIEL_BANK",
        "kreditprovisionswunsch": 0.0123,
        "vertriebsgruppe": "Beispielgruppe"
    },
    "beratungsart": "AUSSER_GESCHAEFTSRAUM_VERTRAG"
}
```

### Response

Der Tilgungsplan ist teilweise gekürzt dargestellt.   

```json
{
    "angebot": {
        "produktanbieter": "MUSTERBANK",
        "referenznummerProduktanbieter": "XVG456",
        "referenznummerDienstleister": null,
        "produktbezeichnung": "Top Ratenkredit",
        "produktart": "RATENKREDIT",
        "angebotsvariantentyp": "eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6eyJhbmdlYm90c1ZhcmlhbnRlblR5cCI6IlBST0RVS1RfSUQiLCJwcm9kdXplbnQiOiJTUElUWkVOQkFOSyJ9fQ==",
        "kredit": {
            "vertragsbeginn": "2020-05-01",
            "effektivzinssatz": 0.0082,
            "sollzinssatz": 0.0079,
            "gesamtbetrag": 9500,
            "nettokreditbetrag": 7500,
            "auszahlungsbetrag": 7000,
            "laufzeitInMonaten": 84,
            "rateProMonat": 110.01,
            "letzteRate": 108.87,
            "provisionsbetrag": 210,
            "basisbetragFuerDieProvisionsermittlung": 10500,
            "vorlaufzinsenProTag": 1.37,
            "versicherung": {
                "basisFuerDieProvisionsermittlung": "VERSICHERUNGS_PRAEMIE_NETTO",
                "provisionsbetrag": 50,
                "praemieBrutto": 500,
                "praemieNetto": 500,
                "risiken": [
                    {
                        "antragstellerId": "eb51059a-ab2d-4253-9a7b-61864ae17123",
                        "tod": true,
                        "arbeitsunfaehigkeit": true,
                        "arbeitslosigkeit": false
                    }
                ],
                "versicherer": "VERSICHERUNGS_AG"
            }
        },
        "status": {
            "machbarkeitsstatus": "NICHT_MACHBAR",
            "angepasst": false
        },
        "meldungen": [
            {
                "kategorie": "ANPASSUNG",
                "text": "Der Provisionswunsch wurde angepasst.",
                "code": "bank.anpassung.provision"
            },
            {
                "kategorie": "MACHBARKEIT",
                "text": "Der Bonitätscheck weist einen zu geringen Betrag aus.",
                "code": "bank.machbarkeit.bonitaet.unterdeckung"
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
                "code": "bank.unterlage.selbstauskunft",
                "text": "Bitte legen Sie die Selbstauskunft vor.",
                "referenz": null
            }
        ],
        "bonitaetscheck": {
            "name": "Haushaltsrechnung",
            "ueberschrift": "Musterbank",
            "ueberschuss": 10,
            "bloecke": [
                {
                    "zeilen": [
                        {
                            "hervorgehoben": false,
                            "label": "Unselbständiges Nettoeinkommen",
                            "wert": 1969.84
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Einkünfte aus Nebentätigkeit",
                            "wert": 400
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Kindesunterhalt",
                            "wert": 395.12
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Kindergeld",
                            "wert": 408
                        }
                    ],
                    "titel": "Einnahmen",
                    "innerBlock": {
                        "zeilen": [
                            {
                                "hervorgehoben": true,
                                "label": "Summe Einnahmen",
                                "wert": 3192.96
                            }
                        ],
                        "hervorgehoben": true
                    }
                },
                {
                    "zeilen": [
                        {
                            "hervorgehoben": false,
                            "label": "Lebenshaltungskosten",
                            "wert": 1750.49
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Mietausgaben",
                            "wert": 1081.51
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Kreditraten",
                            "wert": 175.95
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Sonstige Ausgaben",
                            "wert": 65
                        },
                        {
                            "hervorgehoben": false,
                            "label": "Rate der Finanzierung",
                            "wert": 110.01
                        }
                    ],
                    "titel": "Ausgaben",
                    "innerBlock": {
                        "zeilen": [
                            {
                                "hervorgehoben": true,
                                "label": "Summe Ausgaben",
                                "wert": 3182.96
                            }
                        ],
                        "hervorgehoben": true
                    }
                },
                {
                    "zeilen": null,
                    "titel": "Überschuss / Fehlbetrag",
                    "innerBlock": {
                        "zeilen": [
                            {
                                "hervorgehoben": true,
                                "label": "Fehlbetrag",
                                "wert": -10
                            }
                        ],
                        "hervorgehoben": true
                    }
                }
            ]
        },
        "tilgungsplan": {
            "eintraege": [
                {
                    "jahr": 2020,
                    "monat": 5,
                    "tag": 1,
                    "zahlung": -7000,
                    "zinsen": 0,
                    "tilgung": 0,
                    "saldo": -7000
                },
                {
                    "jahr": 2020,
                    "monat": 6,
                    "tag": 1,
                    "zahlung": 110.01,
                    "zinsen": 46.2,
                    "tilgung": 63.81,
                    "saldo": -6939.19
                },
                {
                    "jahr": 2020,
                    "monat": 7,
                    "tag": 1,
                    "zahlung": 110.01,
                    "zinsen": 45.78,
                    "tilgung": 64.23,
                    "saldo": -6874.96
                },
//                ...
                {
                    "jahr": 2021,
                    "monat": null,
                    "tag": null,
                    "zahlung": 1320.12,
                    "zinsen": 543.12,
                    "tilgung": 777,
                    "saldo": -6097.96
                }
//                ...
            ],
            "schlusswerte": {
                "zahlung": 9240.84,
                "zinsen": 2240.84,
                "tilgung": 7000,
                "saldo": 0
            }
        },
        "maximalerAuszahlungsbetrag": 7100
    }
}
  ```
