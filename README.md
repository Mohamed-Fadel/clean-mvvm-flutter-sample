# Flutter app architecture

<p align="center">
  <img src="https://uploads.toptal.io/blog/image/127608/toptal-blog-image-1543413671794-80993a19fea97477524763c908b50a7a.png" />
</p>

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

- **Domain** contains UseCases, Domain Objects/Models, and Repository Interfaces

- **Application** contains UI, View Objects, Widgets, etc. Can be split into separate modules itself if needed. For example, we could have a module called Device handling things like camera, location, etc.

# Repository
- Bridge between Data layer and Domain layer
- Connects to data sources and returns mapped data
- Data sources include DB and Api

# UseCase
- Responsible for connecting to repository to retrieve necessary data. returns a Stream that will emit each update.
- This is where the business logic takes place.
- Returns data downstream.
- Single use.
- Lives in Domain (No Platform dependencies. Very testable).

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
