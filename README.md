# Versioned Documentation

## Introduction

Versioned is a headless CMS (or content backend) that is available both
as [a managed service](https://www.versioned.io) and as [open source software on Github](https://github.com/versioned-cms). Versioned consists of a REST API and an admin UI and is built on the tech stack [Node.js](https://nodejs.org), [MongoDB](https://www.mongodb.com), and [Vue.js](https://vuejs.org).

The value proposition of a content backend like Versioned is that it provides a cost- and time-efficient way to manage database content in a single repository and to deliver it via an API to your websites and applications (and any other clients or systems that need it). Building such a system from scratch takes months of developer time but with Versioned you can be up and running in hours.

## Core Concepts

At a conceptual level Versioned is made up of the following core building blocks:

* *Models* (i.e. database tables). Models are the content types that define the structure (schema) of your data, i.e. what fields you can store, the validation rules, and the relationships between different types of data. You for example have an `Author` model with the fields `name` and `biography` and an `Article` model with the fields `title` and `body`. The `Author` and `Article` models can then have a relationship so that an author `has many` articles and each article `belongs to` an author.
* *Data* (i.e. database rows). Data is the content entered into each model and once it's published it gets delivered as JSON to your clients.
* *Spaces* (i.e. database namespaces). Spaces are used to group models and their data and typically represent different projects in your organization.

## The REST API

The [REST API](http://api.versioned.io) services has two main purposes:

* Managing content. i.e. defining models and creating their data
* Delivering content to clients

## The Admin UI

Everything that can be done in the admin UI can also be done via the REST API.

## Content Delivery to Clients

Content delivery to clients is done with the REST API via a CDN and makes use of an `apiKey`.

## Relationships

TODO

## Publishing

TODO
