![Health SSI Banner](images/banner.png)

# Health SSI Generation 2

Welcome to our Health SSI repository!

# Motivation

We are aiming to showcase healthcare use cases based on Self Sovereign Identity (SSI) principles.

This repository builds on the original idea of [Health SSI](https://github.com/janesp/health-ssi) and the subsequent award-winning [challenge](https://hack.opendata.ch/project/1103) at the [GovTech Hackathon 2024](https://www.bk.admin.ch/bk/en/home/digitale-transformation-ikt-lenkung/bundesarchitektur/api-architektur-bund/govtech-hackathon24.html). Check out the short «making of» [video](https://youtu.be/uNrMFE2wOyQ) with the live demonstration at the final pitch.

A health app proof of concept was built in 2022 with a FHIR server backend ([short video](https://youtu.be/T5bYmy_oXMo)). The Health SSI showcase app shall be implemented with a wallet as data store.

It is our intention to implement a health app with health data verifiable credentials based on the Swiss federal govermnent [public beta](https://www.eid.admin.ch/en/public-beta-e) trust infrastructure.

# Use Cases

To showcase the interaction of several participants of the healthcare system and their wallets, a few simple and easy to comprehend use cases are envisaged for the implementation of the PoC:

* The patient John Miller carries a wallet with information of an international patient summary (allergies, medication, etc.) and a health insurance card in the form of previously issued VCs
* John enters the office of Dr. Charles Brewster and registers through a QR code; this initiaites a proof request for insurance and health information in John's wallet, which is subsequently confirmed by John
* Dr. Brewster issues the findings of his examination as a VC and prescribes some drugs, also in the form of VCs
* After the visit, John orders the drugs through the «Universal Pharmacy» online store by presenting the prescription VCs

See also [Health SSI](https://github.com/janesp/health-ssi).

# Envisaged Implementation

## Architecture

While the hackathon showcase made simplifications for timely implementation, the next proof of concept shall have a state of the art architecture:

* Modular components with APIs to issue and verify healthcare specific verifiable credentials
* Simulations of practitioner and pharmacy «business systems» with appropriate user interfaces
* Wallet for citizen to hold verifiable credetials with health data

![Health SSI Components](images/components.png)

* All participating (healthcare) «business platforms» are based on common health data object definitions, based on openEHR and FHIR standards (technically based on json schemas)
* A verifiable credential framework provides generic VC operations such as wallet functionality, as well as VC issuing and verification ([walt.id](https://walt.id/) for the PoC)
* Healthcare specific VC operations are provided by a «business logic» on top of the generic VC framework (through library and REST API interfaces based on [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html))

## Technology

Currently used for first PoC implementation and planned for next steps.

* Verifiable credentials
  * Simplified JSON payload objects for first feasability validations
  * Payload based on JSON-LD schemas (directly taken from [openEHR](https://specifications.openehr.org/releases/ITS-JSON/latest) and [FHIR](https://www.hl7.org/fhir/fhir.schema.json))
  * SD-JWT signatures
  * Option for BBS+ signatures at a later stage ([Verifiable Credentials Playground](https://vcplayground.org), tbc)
* Verifiable Credential framework with REST and library APIs to manage generic verifiable credentials ([walt.id](https://walt.id/))
* Front end (app, desktop) and business logic based on multiplatform environment [Rect Native](https://reactnative.dev)
* Wallet - [esatus](https://esatus.com/en/digital-identity/), [Lissy](https://www.lissi.id/for-users), ... (during next stage); preferably with APIs for credential manipulation from app

In case you are interested in the code, check out our [development repository](https://github.com/deak-ai/healthwallet).

## Open Source

The prototype is about to be published open source. Check out the GitHub «[HealthWallet](https://github.com/deak-ai/healthwallet-ips)» repository. Stay tuned for more to come.

# Contributors

* [Peter Janes](https://www.linkedin.com/in/peterjanes/) - [DIDAS](https://www.didas.swiss) Health working group lead, GovTech Hackathon challenge owner
* [Oliver Deak](https://www.linkedin.com/in/oliver-deak/) - technology and development specialist

# Past and Envisaged Showcase Events

* DICE 2024, June 2024 - check out our [short video](https://youtu.be/CaEMHeJBKr8), [DICE 2024 Documents](https://drive.google.com/drive/u/1/folders/1z1Ban7MKxz-yanZQrFsAx7H5zHR_Iiag) (DIDAS Health et al) and [DICE 2024 Health session notes](https://docs.google.com/document/d/18KrZ8nvOPWkPkAjAt0Bdu8vWuTFvgFP0donpNUwLPX4/edit)
* DIDAS Health Webinar, 14.02.2025, check out our [teaser video](https://youtu.be/D69uVIVHmsw) and the [full webinar recording](https://youtu.be/hOM_EMtdAl8) for a live demonstration of the current prototype - testimonial of [Adam Eunson](https://www.linkedin.com/in/adameunson/) «I have to say, having been in the space for 5+ years this is one of the best use case and user experience demonstrations of the technology I have ever seen! Amazing job to everyone involved!»
* [DICE 2025](https://diceurope.org), March and September 2025
* ...

# Learnings Log

In the course of our prototyping journey, a number of pivots were made to accomodate for learnings resulting from the process:

* No code platforms [FlutterFlow](https://flutterflow.io/) and [BuildShip](https://buildship.com/) dropped in favor of [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html) for more flexibility regarding functionality as well as VC library and REST API usage
* [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html) dropped for App development in favor of [Rect Native](https://reactnative.dev) due to considerably higher maturity of development environment
* Architecture changed from verifiable credentials as «source of truth» to referenced information to accomodate for other sources of health data (e.g. local Apple [HealthKit](https://developer.apple.com/documentation/healthkit) / Android [Health Connect](https://developer.android.com/health-and-fitness/guides/health-connect), remote EHR)
