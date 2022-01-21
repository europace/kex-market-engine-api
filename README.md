# KEX Market Engine API

> ⚠️ You'll find German domain-specific terms in the documentation, for translations and further explanations please refer to our [glossary](https://docs.api.europace.de/common/glossary/)

This API enables Produktanbieter within consumer loans to connect their loan offering to the Europace platform via services with standardized interfaces.

> ⚠️ This API is continuously developed. Therefore we expect
> all users to align with the "[Tolerant Reader Pattern](https://martinfowler.com/bliki/TolerantReader.html)", which requires clients to be
> tolerant towards compatible API changes when reading and processing the data. This means:
>
> 1. unknown properties must not result in errors
>
> 2. Strings with a restricted set of values (Enums) must support new unknown values
>
> 3. sensible usage of HTTP status codes, even if they are not explicitly documented
>

<!-- https://opensource.zalando.com/restful-api-guidelines/#108 -->

## API version

The version of the API is based on [Semantic Versioning](https://semver.org/) and has the format

`MAJOR.MINOR.PATCH`

and is part of the [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml) (`info.version`).

1. The `MAJOR` version is incremented in case of API incompatible changes (e.g. new mandatory data)
2. The `MINOR` version is incremented for backward compatible API changes (e.g. new optional specifications)
3. The `PATCH` version is incremented if the API remains the same, but the Swagger definition is adapted (e.g. extension or adaptation of descriptions in the API)

You will find the current version of the API within the [Releases](https://github.com/europace/kex-market-engine-api/releases).

## API specifikation

Request and response are defined in the [Swagger Definition](https://github.com/europace/kex-market-engine-api/blob/master/swagger.yml).

## Documentation

### Annahme

In a KreditSmart Vorgang, offers are first calculated by Europace. In the process, the general feasibility is pre-checked, adjustments to the request are made if necessary, 2/3 - conditions are calculated and the completeness of the process is ensured.

If all the necessary data is available and the preliminary check was successful, the acceptance can take place via the KEX Market Engine API. In this process, the <b>customer's request</b>, i.e. the <b>recorded (but unadjusted)</b> data of the Finanzierungswunsch by the broker, as well as the applicant data are transmitted to the Produktanbieter.

The Produktanbieter shall then in turn carry out all steps necessary for the acceptance of the offer:

#### Adaptation of the customer's request

- If it is not possible to issue an offer on the desired financing criteria, an adjustment should be made to generate a feasible offer
- The following specifications can be adjusted
    - Duration specification
    - Monthly payment specification
    - Loan amount specification
    - Insurance combinations
    - Commission
- An adjustment message must be generated for each adjustment to inform the broker of the adjustment.
- See fields <code>status.angepasst</code> and <code>meldungen</code>

#### Credit assessment of the Antragssteller

- Including an overview of the accounted income and expenses and the calculated surplus/shortfall
- See field <code>bonitaetscheck</code>

#### Calculation of final conditions

- Including redemption schedule
- See fields <code>kredit</code> and <code>tilgungsplan</code>

#### Vote on the feasibility of the application

- Including consideration of the scores of external providers e.g. Schufa
- In case of rejection, generating a message with reason for rejection
- See fields <code>status</code> and <code>meldungen</code>

#### Identification of documents to be submitted
- See field <code>unterlagen</code>

#### Creation of the contract documents
- See field <code>dokumente</code>

#### Providing links for the digital identification of the Antragsteller

- Video legitimation
- QES
- See field <code>identifikation</code>

### Integration of the KEX Market Engine API in Europace

The KEX Market Engine API will be implemented by the Produktanbieter. With support of the KEX Market Engine service Europace can integrate the products of the Produktanbieter via API into KreditSmart.

![](KEX%20Market%20Engine%20API%20Annahme%20Sequenzdiagramm.svg)

### API reference

The implemented interface accepts data with content-type **application/json**.

#### Request

Services that implement the API expect a POST-request with a JSON-document as request-body.

During the offer calculation, it is already ensured that the application data is complete. Notwithstanding this, the service must be able to deal with missing data. This should not lead to a technical error.

#### Response

The response will be expected as JSON within the response body. 

In general a response with a complete offer and HTTP status code **200 SUCCESS** is expected. If the offer is **MACHBAR**, at least one document is expected.

In case of a technical error a response with HTTP status code **500** is expected. The response must not contain an offer, but should give an indication of the cause of the error as <code>supportMeldung</code>.

##### Handling incomplete requests

A complete offer without document(s) is expected. The Machbarkeitsstatus is **NICHT_MACHBAR**. Vollständigkeitsmeldungen must be available, that point out the missing data.

##### Handling shortfall in the Haushaltsrechnung

If the Antrag is not feasible due to a shortfall in the Haushaltsrechnung, in best case the duration will be extended. If this is not possible, a downselling of the loan amount can take place.

If a downselling results in a feasible offer, this is marked as <code>"angepasst": true</code> and contains appropriate adjustment messages to inform the broker of the adjustment.


If a downselling is not possible, an offer without document(s) with the status **NICHT_MACHBAR** and at least one corresponding feasibility message is expected. Duration and loan amount should in this case correspond to the original request.

##### Messages

Messages are generated to provide guidance to the broker on the excecution and feasibility of the application. The following categories are distinguished.

| Message category  | Description | <code>machbarkeitsstatus</code>| <code>angepasst</code> |
|--------|--------|--------|--------|
| <code>MACHBARKEIT</code> | The Antrag will be rejected. | NICHT_MACHBAR| <i>no influence<i> |
| <code>VOLLSTAENDIGKEIT</code> | The Antrag is incomplete and must be completed with missing data. | NICHT_MACHBAR| <i>no influence<i> | 
| <code>HINWEIS</code> | Note to the broker. | <i>no influence<i> | <i>no influence<i>|
| <code>ANPASSUNG</code> | Not to adjustments of the customer's request, e.g. monthly payment, loan amount oder insurance. | MACHBAR | true | 

##### Status

| Machbarkeitsstatus  | Description |
|--------|--------|
| MACHBAR | The Antrag is accepted. |
| MACHBAR_UNTER_VORBEHALT_PRODUKTANBIETER | The Antrag could not be finally examined. Produktanbieter and broker need to renegotiate.| 
| NICHT_MACHBAR | The Antrag is rejected. |

## Authentication

The method of authentication is agreed between the Produktanbieter and Europace.

## Performance

We expect the Annahme-response on average within 30s. If the response time is significantly higher, the functionality of our platform deteriorates for other partners, e.g. brokers.

## Example

* [Successful Annahme](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-erfolgreich.md)
* [Annahme with missing data](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-fehlenden-daten.md)
* [Annahme with shortfall](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-unterdeckung.md)
* [Annahme with downselling](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-annahme-mit-downselling.md)
* [Annahme with technical error](https://github.com/europace/kex-market-engine-api/blob/master/beispiele/example-technischer-fehler-antwort-annahme.md)

## Terms of use
    
The APIs are made available under the following [Terms of Use](https://docs.api.europace.de/terms/).
