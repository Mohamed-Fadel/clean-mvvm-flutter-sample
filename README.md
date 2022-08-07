# Flutter app architecture

Guide to design Flutter app architecture using Stacked plugin.
Here is the detailed guide on Medium
https://medium.com/codex/a-complete-guide-to-architect-your-flutter-application-a5a4da662549

## Introduction

This sample demonstrates how one can

- Setup base architecture of Flutter app using Stacked plugin
- Use dependency injection for layers separation
- Code generator to generate boilerplate code for DI, routes and JSON parsing
- Make api calls using Retrofit plugin (mostly Android developers might be familier with it).

Apart from the basic architecture setup, this sample also demonstrates

- Project folder structure
- Navigation using ViewModel (without context)
- Easy data sharing between the screens
- And few more...

# Module Structure
There are 3 main modules to help separate the code. They are Data, Domain, and Application.

- **Data** contains Local Storage, APIs, Data objects (Request/Response object, DB objects), and the repository implementation.

- **Domain** contains UseCases, Domain Objects/Models (Pojos/Kotlin Data Classes), and Repository Interfaces

- **Application** contains UI, View Objects, Android components, etc. Can be split into separate modules itself if needed. For example, we could have a module called Device handling things like camera, location, etc.

# Repository
- Bridge between Data layer and Domain layer
- Connects to data sources and returns mapped data
- Data sources include DB, Api, and RxCache (Cache of data that is constantly emitting updates to subscribers. More on this in another post).
- Always store mapped data. E.g. Store the domain objects in the RxCache.
# UseCase
- Responsible for connecting to repository to retrieve necessary data. Can either return a Flowable that will emit each update (from RxCache), or a Single/Completable that finishes after result is retrieved.
- This is where the business logic takes place.
- Returns data downstream.
- Single use.
- Lives in Domain (No Android dependencies. Very testable).
# ViewModel
- Organizes data and holds View state.
- Talks to use cases.
- Does not know about the View.
# View
- Updates UI
- Knows about the ViewModel
- Observes changes to ViewModel.
# Router
- I leave this open ended to suit each projects needs. The main point here is that it is important to consolidate navigation logic to one place. This helps with maintenance and unit testing.

## Setup

One can download the code in zip format or take checkout from the git repository.

### Note
You need to run build_runner command for code generation everytime when you make changes in your original file.
