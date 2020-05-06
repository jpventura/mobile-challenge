# Android Sample

## Requirements

TODO

## Architecture

Usually I try to organize my projects under clean architecture, deciding to (not) use interactors according the complexity of the project. 

However I keep project modular structure as follows:

| [Android Clean Architecture][aca-img] | [**Single Responsability**][srp-url]  |
|------|------|
| ![Android Clean Architecture][aca-img] | ![SRP][srp-img] |

### Busines logic libraries

This are the libraries implemented on each and every project:

  - [`data`](./data): TODO

  - [`domain`](./domain): TODO

  - [`app`](./app): TODO

### Core Libraries

You shall notice the following modules in my projects

  - [`core-domain`](./core-domain): provides all _domain_ contracts (i.e. _interface_) that shall be used by any module providing:

    - **Use cases:** also know as interactors. Instead of using command-pattern, they were created as callable Kotlin objects.
    - **Bean:** [anemic models][anemic-model-url] interfaces that rules how data transfer objects should be implemented by the devs.
    - **Model:** in the correct sense (domain models), in order to wrap any data persistence behavior (shared preferences, network, SQLite, memory)

  - [`core-data`](./core-data):
      - Uses [`core-domain`](./core-domain), it provides abstract classes for creating
        - Memory models
        - Cache first repositories

This libraries shall be provide as independend packages in Maven, allowing faster creation of _clean arch apps_.

## Reference

  - [Clean Arch Modules | Five Agency][srp-url]
  - [Hands on Clean Arch | Five Agency][aca-url]
  - [Domain Model, by Martin Fowler][domain-model-url]
  - [Anemic Model, by Martin Fowler][anemic-model-url]

[aca-img]: https://five.agency/wp-content/uploads/2017/06/graf_2_B-1.png
[aca-url]: https://five.agency/android-architecture-part-3-applying-clean-architecture-android/

[srp-img]: https://five.agency/wp-content/uploads/2016/11/Graph-4-1.png
[srp-url]: https://five.agency/android-architecture-part-3-applying-clean-architecture-android/

[anemic-model-url]: https://martinfowler.com/bliki/AnemicDomainModel.html

[domain-model-url]: https://martinfowler.com/eaaCatalog/domainModel.html
