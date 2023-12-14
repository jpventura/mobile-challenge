# Android Sample

## TL; DR

The [APK](result/app-debug.apk) is available for download in [results](./results) directory.

## Requirements

  1. Series
     - [x] List of series
     - [x] Search series by name
     - [ ] Series name: **not** added due aesthetic, since the posters already have the series names

  2. Episodes

     - [x] Series details (score, description, poster)
     - [x] Episodes (season, episode number, details, scene)

  3. Optional

     - [x] Tests added only into core modules and data models
     - [x] Cache in memory, allowing to have access to previous data (while app is not killed). The contract allows migrating the cache model to [Apollo Android][apollo-url] or [Room][room-url]

The app contains code of previous projects of mine:

  - [Popular Movies][popular-movies-url]
  - [GitHub for Android][github-url]

## Architecture

Usually I try to organize my projects under clean architecture, deciding to (not) use interactors according the complexity of the project. 

However I keep project modular structure as follows:

| [Android Clean Architecture][aca-img] | [**Single Responsability**][srp-url]  |
|------|------|
| ![Android Clean Architecture][aca-img] | ![SRP][srp-img] |

### Busines logic libraries

This are the libraries implemented on each and every project:

  - [`data`](./data): concrete implementations of repositories defined at `domain` module, controlling cache policy of how remote data should be persisted locally.

  - [`domain`](./domain): use cases and repositories interfaces definitions. This project only required repositories

  - [`app`](./app): view, view-models, dependency injection (kodein) related to screens required as specification.
    - View-Model, Presenter and Controllers can be implemented using use cases. Simpler projects may relay only on repositories

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

[popular-movies-url]: https://github.com/jpventura/popularmovies
[github-url]: https://github.com/jpventura/github

[aca-img]: https://five.agency/wp-content/uploads/2017/06/graf_2_B-1.png
[aca-url]: https://five.agency/android-architecture-part-3-applying-clean-architecture-android/

[apollo-url]: https://www.apollographql.com/docs/kotlin/
[room-url]: https://developer.android.com/jetpack/androidx/releases/room

[srp-img]: https://five.agency/wp-content/uploads/2016/11/Graph-4-1.png
[srp-url]: https://five.agency/android-architecture-part-3-applying-clean-architecture-android/

[anemic-model-url]: https://martinfowler.com/bliki/AnemicDomainModel.html

[domain-model-url]: https://martinfowler.com/eaaCatalog/domainModel.html
