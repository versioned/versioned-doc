# Versioned Documentation

## Introduction

Versioned is a headless CMS (i.e. content backend) that is available both
as [a managed service](https://www.versioned.io) and as [open source software on Github](https://github.com/versioned-cms). Versioned consists of a REST API and an admin UI and is built on the tech stack [Node.js](https://nodejs.org), [MongoDB](https://www.mongodb.com), and [Vue.js](https://vuejs.org).

The value proposition of a content backend like Versioned is that it provides a cost- and time-efficient way to manage content in a single repository and to publish it via an API to your websites and applications (and any other clients or systems that need it). Building such a system from scratch takes months of developer time but with Versioned you can be up and running in hours.

The two main building blocks of Versioned are:

* A web UI where content editors can manage content
* A REST API that delivers published content to clients (websites, apps etc.)

Feature highlights:

* *Dynamic Content Types* - the ability for content editors to set up any custom content types without having to involve software developers
* *Data Validation* - each content type field has a data type and can have additional validation rules to ensure the integrity of the data
* *Relationships* - you can have `one-way` or `two-way` relationships between two content types and the type of relationship can be either `one-to-one`, `one-to-many`, or `many-to-many`.
* *Publishing and Versioning* - work on content in a draft state and publish it to clients when it's ready. Content is versioned and there is a publish history.
* *Changelog* - there is a log of all changes made to data so that editors can keep track of what has been changed, when, and by whom
* *Webhooks* - have another system receive an HTTP call whenever content has been changed so that you can make sure your clients always have the latest published content (i.e. you may need to rebuild a [static website](https://jamstack.org))
* *Translations* - have your texts translated into multiple languages and deliver the relevant language to your users

## Core Concepts

At a conceptual level Versioned is made up of the following core building blocks:

* *Models* (i.e. database tables). Models are the content types that define the structure (schema) of your data, i.e. what fields you can store, the validation rules, and the relationships between different types of data. You for example have an `Author` model with the fields `name` and `biography` and an `Article` model with the fields `title` and `body`. The `Author` and `Article` models can then have a relationship so that an author `has many` articles and each article `belongs to` an author.
* *Data* (i.e. database rows). Data is the content entered into each model and once it's published it gets delivered as JSON to your clients.
* *Spaces* (i.e. database namespaces). Spaces are used to group models and their data and typically represent different projects in your organization.

## The REST API

The [REST API](http://api.versioned.io) services has two main purposes:

* Managing content. i.e. defining models (content types) and creating data
* Delivering content to clients

## The Admin UI

TODO

Everything that can be done in the admin UI can also be done via the REST API.

## Content Delivery to Clients

Content delivery to clients is done with the REST API via a CDN and makes use of an `apiKey`.

## Relationships

TODO

## Publishing

TODO
