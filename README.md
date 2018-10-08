# Versioned Documentation

## Introduction

Versioned is a headless CMS (or content backend) that is available both as [a managed service](https://www.versioned.io) and as [open source software on Github](https://github.com/versioned).

The main building blocks are:

* A web UI where content editors can manage content
* A REST API that delivers published content/data to clients (i.e. websites and apps)

## Value Proposition

Versioned provides a cost- and time-effective way to manage content via a web UI and to publish it through an API to your websites and applications (and any other clients or systems that need it). Building such a system from scratch takes months of developer time. With Versioned you can be up and running in hours and you don't and you also avoid the maintenance burden of writing software.

## Feature Highlights

* *Dynamic Content Types* - a flexible way for content editors to set up the content types they need without having to do any software development
* *Data Validation* - content types are a collection of fields and each field has a data type and optionally validation rules to ensure the integrity of the data
* *Relationships* - the field of a content type can represent a `one-way` or `two-way` relationship (i.e. link or reference) to another content type and the type of the relationship can be either `one-to-one`, `one-to-many`, or `many-to-many`
* *Publishing and Versioning* - work on new content in a draft state, preview it, and then publish it to clients when it's ready. Content is versioned and you can see what has happened in a publish history.
* *Changelog* - Versioned maintains a log of changes made to all data so that editors can keep track of exactly what has been changed, when, and by whom
* *Webhooks* - you can configure another system to receive an HTTP call whenever content is changed so that your clients always have the latest published content (you may for example need to rebuild a [static website](https://jamstack.org) when content changes)
* *Translations* - select which languages to translate your texts into and deliver only the relevant language to your users

## Tech Stack

Versioned is built on these technologies:

* [Node.js](https://nodejs.org)
* [MongoDB](https://www.mongodb.com)
* [Vue.js](https://vuejs.org)

## Core Concepts

* *Models* (i.e. database tables). Models are content types that define the structure (or schema) of your data, i.e. which fields you can store, validation rules, and relationships to other models. You may for example have an `Author` model with the fields `name` and `biography` and an `Article` model with the fields `title` and `body`. The `Author` and `Article` can have a relationship so that an author `has many` articles and each article `belongs to` an author.
* *Data* (i.e. database rows or documents). Data is the content entered into each model and once it's published it gets delivered as JSON to your clients. Data is stored as documents in a MongoDB database.
* *Spaces* (i.e. database namespaces). Spaces are isolated collections of models and data and typically represent projects in your organization. A space can be configured to use its own dedicated database.

## The REST API

The [REST API](http://api.versioned.io) has two main purposes:

* Allowing `models` and `data` to be managed (primarily via the web UI). The API also handles `accounts`, `users`, and `spaces`.
* Delivering published `data` to clients. Through the use of a secret API key clients can fetch one or more published documents. Clients have fine grained control over what should be fetched - the number of documents, sorting, filtering, fields, and relationships.

The REST API has detailed API documentation (built on Swagger) available
and it's linked from the [Admin UI](http://app.versioned.io).

## The Admin UI

The [Admin UI](http://app.versioned.io) is where content creators manage
`models` and `data` and make sure `data` gets published to clients. The main features are:

* Registration of `users` and `accounts`
* Defining `models` (data types) which are collections of fields and each field has a data type, validation rules (optional), and can represent a relationship to another model
* Managing (creating, updating, deleting) `data` for each model. Data can be versioned and you control when new data (changes) should be published to clients
* Organizing `models` and `data` into `spaces` (or projects) and configuring those spaces. It is highly recommended that you use a dedicated MongoDB database (i.e. with a service like [mLab](https://mlab.com) or [Compose](https://www.compose.com/databases/mongodb)) and [Algolia search service](https://www.algolia.com) for your spaces especially if you have large amounts of data. Via [Heroku Add-Ons](https://elements.heroku.com/addons) you can get access to free MongoDB and Algolia services.
* Managing `assets`, i.e. uploaded files such as images, videos, PDFs etc. This feature requires that you sign up for a [Cloudinary](https://cloudinary.com) account.

Note that since the web UI is based on the REST API, everything that can be done with the admin UI can also be done directly with the REST API.

## Content Delivery to Clients

Content delivery to clients is done with the REST API via a CDN (Content Delivery Network) and makes use of an API key. Versioned doesn't come with
a built-in CDN and you need to sign up for a service like [Fastly](https://www.fastly.com), [Cloudflare](https://www.cloudflare.com), [CloudFront](https://aws.amazon.com/cloudfront) and use it as a layer between your clients and the CDN for performance and scalability. Setting up such a CDN is straightforward and relatively cheap (i.e. [Fastly](https://elements.heroku.com/addons/fastly) offers</a> 10 million requests per month at 25 USD/month). If you are not using a CDN you can expect the Versioned REST API to be rate limited at around 5 requests per second.

In the [Admin UI](http://app.versioned.io) you will find links to detailed API documentation and example API calls that illustrate how you fetch published data from your clients. Here is an example API call (with [httpie](https://httpie.org)) that lists published blog posts:

```bash
export BASE_URL=https://api.versioned.io/v1
export SPACE_ID=5ba205c2aefdde0013596636
export MODEL=blog_posts
export API_KEY=kf924ed960b74556
http GET "$BASE_URL/data/$SPACE_ID/$MODEL?apiKey=$API_KEY&published=1"
```

For more fine grained control over which data to fetch to your clients you
can use the query parameters `limit`, `skip`, `sort`, and `filter`. To configure which relationships to fetch (if there are any) use the query parameter `relationshipLevels` and optionally one of `relationships` and `graph`. The `graph` parameter is more powerful than the `relationships` parameter as it controls all fields and not just relationship fields. Please consult the API documentation for more details.

## Relationships

TODO

## Publishing

TODO

## Assets

TODO
