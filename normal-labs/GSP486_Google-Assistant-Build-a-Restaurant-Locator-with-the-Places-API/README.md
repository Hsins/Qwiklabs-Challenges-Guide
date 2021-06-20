# GSP486 —— Google Assistant: Build a Restaurant Locator with the Places API

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [References](#references)

</details>

## Overview

[Google Assistant](https://assistant.google.com/#?modal_active=none) is a personal voice assistant that offers a host of actions and integrations. From sending texts and setting reminders, to ordering coffee and playing music, the 1 million+ actions available suit a wide range of voice command needs.

[Cloud Functions](https://cloud.google.com/functions/docs/) is a lightweight compute solution for developers to create single-purpose, stand-alone functions that respond to Cloud events without the need to manage a server or runtime environment.

The [Places API](https://developers.google.com/maps/documentation/places/web-service/overview) is a service that returns information about points of interest by using HTTP requests. More specifically, you will take advantage of the [Place Details](https://developers.google.com/maps/documentation/places/web-service/details) and [Place Photos](https://developers.google.com/maps/documentation/places/web-service/photos) services to receive detailed information and photos of establishments.

By utilizing Cloud Functions and the Places API, you will build an Assistant application that takes in a user's current location and restaurant preferences to generate the ideal restaurant for them to visit, complete with names, addresses, and photos.

## References

- [Google Assistant](https://assistant.google.com/#?modal_active=none)
- [Cloud Functions](https://cloud.google.com/functions/docs/)
- [Places API](https://developers.google.com/maps/documentation/places/web-service/overview)
- [Place Details](https://developers.google.com/maps/documentation/places/web-service/details)
- [Place Photos](https://developers.google.com/maps/documentation/places/web-service/photos)