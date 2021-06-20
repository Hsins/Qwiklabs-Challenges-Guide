# GSP294 —— Introduction to APIs in Google

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [APIs and Cloud APIs](#apis-and-cloud-apis)
- [API Library and API Dashboard](#api-library-and-api-dashboard)
- [API Architecture](#api-architecture)
- [HTTP Protocol and Request Methods](#http-protocol-and-request-methods)
- [RESTful APIs](#restful-apis)
- [References](#references)

</details>

## Overview

APIs (Application Programming Interfaces) are software programs that give developers access to computing resources and data. Companies from many different fields offer publicly available APIs so that developers can integrate specialized tools, services, or libraries with their own applications and codebase.

This lab will teach you about the architecture and basic functioning of APIs. This will be supplemented with hands-on practice, where you will configure and run [Cloud Storage API](https://cloud.google.com/storage/docs/json_api/) methods in Google Cloud Shell. After taking this lab you will understand key principles of API communication, architecture, and authentication. You will also gain practical experience with APIs, which you can apply to future labs or projects.

## APIs and Cloud APIs

- An **API (Application Programming Interface)** is a software program that gives developers access to computing resources and data.
- APIs adhere to specific rules and methods to clearly communicate requests and responses.
- Google offers APIs that can be applied to many different fields and sectors.
- The tool [APIs Explorer](https://developers.google.com/apis-explorer/) allows us to explore various Google APIs interactively.

## API Library and API Dashboard

- The **API library** offers quick access, documentation, and configuration options for 200+ Google APIs.
  - Click **Navigation Menu** > **APIs & Services** > **Library**.
- The **API Dashboard** details our project's usage of specific APIs, including traffic levels, error rates, and even latencies, which helps us quickly triage problems with applications that use Google services.
  - Click **Navigation Menu** > **APIs & Services** > **Dashboard**.

## API Architecture

The internet is the standard communication channel that APIs use to transmit requests and responses between programs. The **Client-Server Model** is the underlying architecture that web-based APIs use for exchanging information.

<div align="center">
  <img src="https://i.imgur.com/pgEZfWo.png" alt="Client-Server Model">
</div>

- **Client**: a computing device (e.g. a smartphone, laptop, etc.) that makes a request for some computing resource or data. The client's request needs to be formatted in the agreed upon protocol.
- **Server**: has data and/or computing resources stored on it. Its job is to interpret and fulfill a client's request.

## HTTP Protocol and Request Methods

Many of APIs adhere to the [HTTP protocol](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview), which specifies rules and methods for data exchange between clients and servers over the internet.

APIs that utilize the HTTP protocol use HTTP request methods (also known as "HTTP verbs") for transmitting client requests to servers. The most commonly used HTTP request methods are `GET`, `POST`, `PUT`, and `DELETE`.

- `GET` is used by a client to fetch data from a server. If the requested resource is found on the server, it will then be sent back to the client.
- `PUT` method replaces existing data or creates data if it does not exist. If you use PUT many times, it will have no effect — there will only be one copy of the dataset on the server.
- `POST` is used primarily to create new resources. Using POST many times will add data in multiple places on the server. It is recommended to use PUT to update resources and POST to create new resources.
- `DELETE` will remove data or resources specified by the client on a server.

## RESTful APIs

APIs that utilize the HTTP protocol, request methods, and endpoints are referred to as **RESTful APIs**. REST (Representational State Transfer) is an architectural style that prescribes standards for web-based communication. RESTful APIs are modelled as:

- Collections of individually-addressable resources.
- The resource-oriented design is a key principle
- The resources and methods are known as **nouns** and **verbs** of APIs.
  - Resource names naturally map to URLs.
  - Methods naturally map to HTTP methods.

These terms should sound familiar since you examined these building blocks in the previous sections. REST is the most widely used framework for APIs. In 2010, about 74% of public network APIs were HTTP REST APIs.

Besides query strings, RESTful APIs can also use the following fields in their requests:

- **Headers**: parameters that detail the HTTP request itself.
- **Body**: data that a client wants to send to a server.

The body is written in the JSON or XML data formatting language. Check more description of RESTful APIs from Google: [What is a REST API?](https://cloud.google.com/apis/design/resources#what_is_a_rest_api) and [About RESTful APIs
](https://developers.google.com/photos/library/guides/about-restful-apis).

## References

- [REST API Tutorial](https://restfulapi.net/)
- [HTTP | MDN Web Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP)