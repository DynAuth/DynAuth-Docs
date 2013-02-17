# GeoAuth Project Proposal
**Project Members:** Jacob Okamoto ``<okam0013@umn.edu>``, Christian Gerrard ``<gerr0041@umn.edu>``, Andrew From ``<fromx010@umn.edu>``, Jason Carter ``<carte660@umn.edu>``

## Overview
This project proposes a service for providing authentication information using real-time location information transmitted from a user's smartphone. The service stores a user's temporal and spatial information as reported by their smartphone, and it uses that data to generate queries which can be used to augment identity verification as part of a multi-factor authentication process.

There are two major benefits this service could potentially provide. The first benefit of such a service is that is uses short-lived dynamic data instead of static data, such as biometric data or traditional passwords. Leaking of this location data, while possibly a short-term privacy issue, is of far less consequence than leaking a fingerprint or password database. The second benefit is that the location data is sufficiently rich and specific to ensure that, assuming a well-thought-out set of challenge queries, a correct answer likely implies proper identity.

## Goals

Produce the following:

* Mobile clients for the three major smartphone platforms: Android, iOS, and Windows Phone
* An API server providing endpoints for the smartphone clients to push data to for storage
* An API server providing endpoints for websites to make use of the system
* A backend for managing API identities (i.e., API user accounts, API tokens, etc.)

## Architecture
There are three main components of this system: the smartphone location client (SLC), the client location API server (CLAS), and the web service API server (WSAS). The SLC clients are responsible for collecting and sending real-time location information to the CLAS server. The CLAS server collects the location information from clients and processes it to permanent storage; it also manages device registration. The WSAS server then uses the data stored by the CLAS server to provide a REST API and authentication portal so that websites can incorporate GeoAuth into their authentication processes. A more detailed explanation of each system follows.

### Smartphone Location Client (SLC)
The smartphone location client is responsible for acquiring the location information that is used by the service to provide authentication challenges. The SLC will interface with a smartphone's native location API to acquire data information, as well as to handle the process of device registration and location tagging. Device registration will associate a device's data with an identity; location tagging will allow for more specific and more useful challenge generation.

### Client Location API Server (CLAS)
The client location API server is responsible for receiving and storing location updates received from SLCs to a relational database for persistent storage. It is also responsible for handling device registration requests and location tags. It may also store additional contextual information from API requests, such as latency, IP address, or device platform.

### Web Service API Server (WSAS)
The web service API server provides the interface that websites will use to request geolocation-based challenges and verify those responses. These challenges will be generated based on the information stored by the CLAS. It will also be responsible for generating the actual challenge forms to allow for collection of relevant contextual information (for instance, is the user connecting from their home IP address, or from a new, previously unseen, location?).

### Backend API Manager
The backend API manager will provide the interface for adding and removing API access to the client and web service APIs. This is an administrative convenience rather than a necessity, since the tasks it will perform can also be performed by loading the GeoAuth system packages and directly manipulating objects there.

## Development Responsibilities
Development work will be divided to cater to each member's skill set and desired learning outcomes. 