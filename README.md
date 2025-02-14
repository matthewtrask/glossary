# OpenAPI Glossary

To avoid confusion in the creation of educational material, tooling, and other content, having a shared vocabulary is important. A lot of people in the [OpenAPI](https://www.openapis.org) community call a lot of things a lot of different things, so let's take a swing at unification here.

## API

The general definition "Application Program Interface" can mean a lot of things, with different types of interface. OpenAPI is specifically talking about HTTP-based APIs, which in general is anything REST, RESTish, and many generic types of RPC. 

## API-First

When APIs first started getting popular, a lot of companies started flopping them out as a marketing ploy. These APIs were generally not particularly useful, rarely performant, and frustrating to work with.

"API First" is a concept that teams should build the APIs first, and make them something they would want to work with, therefore solving useability issues, performance issues, etc. and supposedly creating a better experience for their customers.

## API Description

Alias include: "API definition", "API contract".

An API Description is meta-data about an API, explaining what endpoints, resources, HTTP methods, headers, query parameters, etc. exist. 

Descriptions are written in a particular "API Description Format" (e.g.: [OpenAPI](http://spec.openapis.org/oas/v3.0.2), [JSON Schema](https://json-schema.org), [RAML](https://raml.org), [WSDL](https://www.w3.org/TR/wsdl/), etc.) and will usually be contained in an "API Description Document" (e.g.: `openapi.yaml`, `schemas/payment.json`) unless the authors decided to use annotations instead.

## API Design

Planning an API specifically using API Descriptions, or a tool which generates / exports API descriptions. When done before coding begins, it is known as API Design First, which is conceptually different to [API First](#API-First) but not mutually exclusive. 

More on [API Design First vs Code First](https://www.apisyouwonthate.com/blog/api-design-first-vs-code-first/).

## API Specification

In the past the term API Specification was one of many terms to describe what most major tooling vendors call an [API Description Document](#API-Description-Document). It was the file that users would write to describe _their_ API.

Ask 100 people and you will get 100 answers, but consensus is forming around API Specifications being an umbrella term for various Specifications involve with API development, and more specific categories exist within the umbrella term.

Message Formats like JSON-API, HAL, Siren, etc. all have a specification.
Data Formats like JSON, YAML, etc all have a specification.

Transfer Protocols like SPDY, HTTP/2, HTTP/3, etc have a specification.

Authentication Strategies like OAuth 2, OpenID, etc all have a specification.

Seeing as there as so many types of API specification floating around, to disambiguate its best to just avoid the term and use one of the more specific categories, or if talking about your own `openapi.yaml` just call it the description document.

## Bundle

Aliases include: "external inlining".

Bundling pulls in external `$refs` from different files, or URLs, and puts them into the `components` object. 

This is done to create a single OpenAPI file, which is easier to share, especially with tooling that does not support resolving external files. If tooling does not support `$ref` at all, then an alternative to bundling is required: [dereferencing](#dereference).

## Callbacks

## Code Generation

## Contract Testing

Confirming that an API is accepting and outputting what it says it is can take many forms. Most commonly, when you hear the term Contract Testing in relation to OpenAPI, people are talking about producer contract testing. This means the API development team (or some test/QA team nearby) have implemented a test suite that will [take an API description and compare it to the actual data](https://apisyouwonthate.com/blog/writing-documentation-via-contract-testing/). 

Conceptually contract testing is the same thing as [data validation](#data-validation), but done for different purposes at different parts of the life-cycle. The same tools could be used under the hood.

There is also client-side contract testing, where you write out the contract in a client test suite then make calls to the API to see if it matches.

## Data Instance

## Data Validation

Often referred to simple as "validation" when there are many types of validation. Data validation is basically taking some real data (maybe an entire HTTP Message with a body, or just the body) and comparing it to the API description.

This is then used to power things like [contract testing](#contract-testing), [gateway validation](#gateway-validation), and [server-side validation](#server-side-validation).

## Dereference

Aliases include: "dereferencing", "internal inlining" or "transclusion".

All `$ref`s and replaced with their values a'la copy & paste. No more `$ref`'s exist in the file/object representation. If you have 10 operations referencing the same model 10 times, you now have 10 different models.

## Description Validation

Aliases include: "schema validation".

A very different type of validation to [data validation](#data-validation). Description validation focuses on making sure the description is correct against the OpenAPI Specification itself.

When a validator moves beyond checking the document is valid, and into custom rules, design opinions, style, etc. the term "linting" is used.

_A list of description validators is available on [OpenAPI.Tools](https://openapi.tools/#description-validation)._

## Documentation

The most common meaning of documentation in OpenAPI-world is [reference documentation](#reference-documentation), but there is a lot more to good API documentation than just that. Guides, tutorials, and other types of how-to content is often combined with reference documentation to provide the best developer experience. This combination along with "sign up for API tokens" type functionality is often referred to as a Developer Portal.

## Gateway Validation

Data Validation leverages in an API Gateway is known as gateway validation, and it will stop invalid requests from wasting application resources. AWS, Tyk, Express Gateway, etc. support some level of OpenAPI or JSON Schema gateway validation.

## Links

## Linting

OpenAPI linter like [Spectral](https://stoplight.io/open-source/spectral) can confirm if API descriptions are valid, but also if they match predetermined rules, like a style guide. Style Guides can be defined by API Governance teams at larger companies, or be shared, like the ones on [openapi-contrib/style-guides](https://github.com/openapi-contrib/style-guides).

## Mocking

A fake server that takes a description document as input, then routes incoming HTTP requests to example responses or dynamically generates examples. 

_A list of mock servers is available on [OpenAPI.Tools](https://openapi.tools/#mock-servers)._

## OAS

This is just shorthand for the OpenAPI Specification, which is just [Markdown files on the internet](https://github.com/OAI/OpenAPI-Specification/tree/master/versions) defining how each version of OpenAPI should work.

## OpenAPI

The new name of the [API Description](#API-Description) Format, which is defined in an [API Specification](#API-Specification). It used to be called [Swagger](#Swagger).

## The OpenAPI Initiative

The [OpenAPI Initiative](https://www.openapis.org) (OAI) are the group in control of the development of the OpenAPI Specification ([OAS](#OAS)).

## Open API

An open API is a public API.

When referring to the [OpenAPI Specification](#OAS), community or the [OpenAPI Initiative](#The-OpenAPI-Initiative), there is no space in "OpenAPI".

## Parameters

Parameters is a general catch-all term for headers, path parameters, query string parameters, and in OpenAPI v2 it also included the request body (like form data).

_More about [Parameters](http://spec.openapis.org/oas/v3.0.2#parameter-object) in the OpenAPI v3.0 specification._

## Reference Documentation

Very similar to the sort of "Classes, Methods, Constants" documentation you're used to seeing for code libraries, modules, packages, explaining the various inputs and outputs. Reference Documentation is a rendering of the API Description in HTML (or maybe a PDF) so slightly less technical people can figure out how to work with the API.

## Reference

A [JSON Reference](https://tools.ietf.org/html/draft-pbryan-zyp-json-ref-03), which can point to a JSON structure in a different location. They may point to objects inside of the current file, but may also refer to other, possibly remote files. They live inside the Reference Object, with the key `$ref`. Here are some examples:

- Reference Object: `{"$ref": "https://example.com/api/openapi.yaml#/components/schemas/Pet"}`
- JSON Reference: `https://example.com/api/openapi.yaml#/components/schemas/Pet`
- [JSON Pointer](https://tools.ietf.org/html/rfc6901) (to the location in the referenced file): `/components/schemas/Pet`

## Resolve

Looking for the value found at the end of a `$ref`, but no changes are made to the file or object being resolved. 

## Schema

Aliases include "data model".

A schema is metadata, which describes the data type, and other properties about the ata like a specific format, and validation rules. JSON Schema is one example of a schema, but OpenAPI has it's own flavour of JSON Schema which it uses for the various locations a `schema` keyword can exist. 

Schema is most commonly associated with describing the body of a HTTP request or response, but it can also describe various [parameters](#parameters) like headers or path parameters.

## SDK

"Software Development Kits" are a generic term in computer-land but in the context of Web APIs and OpenAPI in particular, they usually mean some sort of client library for other developers to interact with an API at a programming language level, and not a HTTP library level. 

_A list of of "SDK Generators" on [OpenAPI.Tools](https://openapi.tools/#sdk)._

## Server-side Validation

Using the concept of [data validation](#data-validation) to 

More on [Server-side Validation](https://www.apisyouwonthate.com/blog/server-side-validation-with-api-descriptions/).

## Swagger

Historically, "Swagger" was the original name of OpenAPI Specification (OAS). It was called Swagger when it was released in 2011, and when SmartBear acquired Swagger Specification they kept the name for a while, and made a bunch of tools with the name Swagger in it. Swagger Editor, Swagger Inspector, SwaggerHub, etc. 

Once the Swagger specification was given to [Open API Initiative](#Open-API-Initiative) in 2016, the name was changed to OpenAPI. 

Now, the word "Swagger" is just part of the SwaggerHub brand of tooling. The specification is "OpenAPI" (not OpenAPI/Swagger).
