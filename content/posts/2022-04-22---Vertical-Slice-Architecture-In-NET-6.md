---
template: post
title: Vertical Slice Architecture in .NET 6
slug: /posts/vetical-slice-architecture-dotnet/
draft: false
date: 2022-04-22T19:23:38.477Z
description: Vertical Slice Architecture approach with project sample in .NET 6.
category: Software Architecture
tags:
  - Architecture
  - .NET
---

## Traditional Layered Architecture

The first approach is the traditional layered architecture. This is a very common way to organize code and has been a standard for decades. I’m sure you have seen and used this on many projects before. A traditional layered/onion architecture approach organizes code around technical concerns in layers. In this approach, different layers are defined based on their responsibilities in the system. The layers then depend on each other so that they can collaborate and achieve their responsibilities. The dependency flow is guaranteed by forcing each layer to only depend on the ones below them (e.g., the presentation layer can only call code in the business logic layer).

For example, in a web application, we might define these four layers:

- Presentation Layer (controllers)
- Business Logic Layer (services)
- Data Access Layer (repositories)
- Infrastructure Layer (database)

## The Problem with traditional layered architecture

The most significant drawback of a layered architecture is that each layer is highly coupled to the layers it depends on. This coupling makes a layered architecture rigid and difficult to maintain.

Tight coupling also makes it more difficult for developers working on different parts of the application to make changes in parallel, because one developer's work might cause problems with another developer's work. Having tight coupling between the layers, when changes are made to a feature, all the layers must be changed.

Typically if I need to change a feature in a layered application, I end up touching different layers of the application and navigating through piles of projects, folders and files. For example for a simple change in a given feature you could be editing more than 5 files in all the layers:

- Domain/TodoItem.cs
- Repositories/TodoItemsRepository.cs
- Services/TodoItemsService.cs
- ViewModels/TodoItemsViewModel.cs
- Controllers/TodoItemsController.cs

Layered architecture is great for some things, but it does have major drawbacks:

- Tight coupling between layers. You can't easily swap out a layer without rewriting code in other layers. This means that if you want to make a change to one feature, you might have to touch several different layers.
- Each layer is aware of the next layer down (and sometimes even a few more). This makes it very difficult to understand the "big picture" at any given time and can lead to unexpected side effects when we make changes in one part of our application.
- It's often unclear where some components belong; should they be placed in Business Logic or Data Access? Do they go in both? Or maybe in Presentation as well? These are questions that we need answers to before writing any code or else we will end up with big messes of tightly coupled spaghetti code.

Instead of separating based on technical concerns, Vertical Slices are about focusing on features.

## Vertical Slice Architecture

Implementing a vertical slice architecture is a good step in designing a robust software system. It's important to be familiar with it, because it provides the foundation for how to structure your codebase and establish the roles and responsibilities of each part of your application.

First, let's clarify what vertical slice architecture means. Vertical slice is an architectural pattern which organizes your code by feature instead of organizing by technical concerns. For example, you can have different features for creating an admin user account versus a normal user account. Or you could have different features for checking if something has been created versus an existing item. This method helps keep track of exactly what your application does for a particular use case within the application.

It's about the idea of grouping code according to the business functionality and putting all the relevant code close together. It improves maintenance, testability, clean separation of concerns and is easier to adapt to changes.

Vertical Slice architecture approach is a good starting point that can be evolved later when an application becomes more sophisticated:
> We can start simple (Transaction Script) and simply refactor to the patterns that emerge from code smells we see in the business logic.
>
> - Jimmy Bogard.

## Sample API solution in .NET

Most applications start simple but they tend to change and evolve. Because of this, I wanted to create a simpler project template that showcases Vertical Slice Architecture approach.

The goal is to stop thinking about horizontal layers and start thinking about vertical slices and organize code by Features. When the code is organized by feature you get the benefits of not having to jump around projects, folders and files. Things related to given features are placed close together.

When moving towards the vertical slices we stop thinking about layers and abstractions. The reason is the vertical slice doesn't necessarily need shared layer abstractions like repositories, services and controllers. We are more focused on concrete Feature implementation and what is the best solution to implement. With this approach, every Feature (vertical slice) is in most cases self-contained and not coupled with other slices. The features relate and share the same domain model in most cases.

![vertical-slices.png](/media/vertical-slices.png)

## The change

This project repository is created based on the Clean Architecture solution template by Jason Taylor, and it uses technology choices and application business logic from this template, like:

- ASP.NET API with .NET 6
- CQRS with MediatR
- FluentValidations
- EF Core 6
- NUnit, FluentAssertions, Moq

I used the Clean Architecture template, because it uses the CQRS pattern with the MediatR library and vertical slices naturally fit into the commands and queries.

Another approach I took (taken from Derek Comartin) about organizing code, is to put all code related to a given feature in a single file in most cases. With this approach we are having self-explanatory file names ExportTodos.cs and all related code close together: Api controller action methods, MediatR requests, MediatR handlers, validations, DTOs. This is what it looks like:

![example-feature.png](/media/example-feature.png)

## Benefits of Vertical Slice Architecture

By building the system around vertical slices, you can avoid making compromises between cohesion and coupling. This is achieved by keeping a low coupling between vertical slices and high cohesion within the slice.

Systems are developed and structured around Features and are use-case driven.

Also, most abstractions aren't needed, and we usually don't need shared abstractions like services, repositories.

When developing and working on feature there are fewer side effects and less paralysis surrounding the change.

When following the principle of keeping things related to each other close, the structure and navigation within the codebase becomes more clear and saves time.

## The source code

Check out the [source code](https://github.com/nadirbad/VerticalSliceArchitecture) for more info. If you like this pls star the repository :).

## Inspired by

- [Clean Architecture solution template by Jason Taylor](https://github.com/jasontaylordev/CleanArchitecture)
- [Vertical slice architecture by Jimmy Bogard](https://jimmybogard.com/vertical-slice-architecture/)
- [Organize code by Feature using Vertical Slices by Derek Comartin](https://codeopinion.com/organizing-code-by-feature-using-vertical-slices/)
