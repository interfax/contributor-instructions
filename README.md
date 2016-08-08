# Library contributors guide

Welcome to the guide for InterFAX library contributors. This document will help you get set up and started on library development, and helps to outline the required output we're looking to achieve.

- [Introduction to InterFAX](#introduction-to-interfax)
	- [Goals](#goals)
- [Getting a Developer Account](#getting-a-developer-account)
	- [Approved inbound number](#approved-inbound-number)
	- [Credits](#credits)
	- [Test fax](#test-fax)
- [Deliverables](#deliverables)
	- [Library](#library)
		- [Example libraries](#example-libraries)
		- [API Coverage](#api-coverage)
		- [DSL](#dsl)
		- [Errors](#errors)
		- [Conventions](#conventions)
		- [Licensing](#licensing)
	- [Publishing](#publishing)
		- [Ownership](#ownership)
			- [Source](#source)
			- [Distribution](#distribution)
			- [Releases](#releases)
	- [Documentation](#documentation)
		- [Title and badges](#title-and-badges)
		- [Installation](#installation)
		- [Getting started](#getting-started)
		- [Reference](#reference)
		- [Contribution](#contribution)
		- [License](#license)
	- [Tests](#tests)
		- [Scope](#scope)
		- [Travis](#travis)
	- [Samples](#samples)


## Introduction to InterFAX

InterFAX provides a simple REST API for sending and receiving faxes. Faxes can be sent in the following ways:


* By uploading a document (PDF, Word Doc, etc) to InterFAX and then pointing to the URI for that document when sending a fax
* By providing the binary data of the document in the body of a POST request
* By providing a URL of a HTML page to be fetched and faxed

Receiving a fax is mostly done asynchronously of this library. The API provides some methods to query new documents, mark them as read, and download the images for further processing.

### Goals

The goal is to make a set of new libraries in various languages that:

- Wrap (most) of the InterFAX REST API
- Allow for sending of a fax in as few lines as is reasonable
- Wrap the erroneous and fragile process of reading binary dating and posting this to the server
- Provide a simple DSL to make the API truly enjoyable to work with

---

## Getting a Developer Account

To be able to send a fax you will need a Developer Account with an approved inbound fax number. Please do not set one up yourself. We will provide you with one.

### Approved inbound number

To prevent abuse every developer account is limited to a single "approved fax number". What this means is that you will only be able to send faxes to this number, which will also function as your own inbound number.

In other words: you can only send faxes to yourself. Sending faxes to anyone else will result in API errors. Please make sure to use your approved inbound number for testing.

### Credits

Your developer account will be set up with some credits to allow you to send and receive faxes. If you run out please contact [Adam](mailto:adam@interfax.net).

### Test fax

Please use [this test fax](test.pdf) in your tests.

---


## Deliverables

### Library

#### Example libraries

We currently have two libraries implemented: [.NET](https://github.com/interfax/interfax-dotnet) and [Ruby](https://github.com/interfax/interfax-ruby). Please use these as references when needed.

#### API Coverage

We are looking to cover most APIs available on the [InterFAX REST API](https://www.interfax.net/en/dev/rest/reference). This includes all options and variations. In other words we want to cover:

- Sending faxes

  - Send fax
  - Get fax list
  - Get completed fax list
  - Get fax record
  - Get fax image
  - Cancel fax
  - Search fax list
  - Resend fax
  - Hide fax
  - Uploading documents (and every sub-call involved)
  - Get outbound credits

- Receiving faxes

  - Get list
  - Get record
  - Get image
  - Get forwarding emails
  - Mark
  - Resend

The only exceptions are **every** API call concerning "Sending batches" (`/outbound/batches`).

#### DSL

We leave with the freedom to decided to build a custom DSL (domain specific language) for the InterFAX library or not. For example, the Ruby library provides direct shortcuts to cancelling a fax from the fax object.

Please keep in mind the "Goals" above and the best practices in your language to fill in your preferred way of building this library.

#### Errors

Where possible if the API returns a non-200 response this error should be passed to the user. (aka it should not be caught)

#### Conventions

##### Client initialization

Ideally your library should follow some of the principles outlined in the  [12-factor](http://12factor.net/config) principle.

* Clients should be instantiable with credentials directly, **OR** by the use of environment variable.
* Multiple clients should be instantiable and should be able to exist at the same time
* When instantiating a client, explicitly provided credentials should override environment variables.

For the environment variables please use: `INTERFAX_USERNAME` and `INTERFAX_PASSWORD`.

##### Naming

* **Library:** ideally we'd use `interfax`, `interfax/interfax` or `InterFAX`, whichever is more idiomatic to the language.
* **Class names:** ideally we'd use `InterFAX` but if this is an issue than `Interfax` will do
* **Lower case:** ideally we'd use `interfax`, not `inter_fax`

##### Files

The following files are required:

- This [LICENSE](LICENSE)
- A `README.md` with documentation
- A `.gitignore` to exclude unwanted build files
- This [CONTRIBUTING.md](CONTRIBUTING.md)
- A `travis.yml` for all relevant language versions to test the library against

Additionally please split your source code into source, test and build folders when needed.

#### Licensing

Please use the [MIT license atached](LICENSE) and reference to this from the documentation and from the source code or packaging files (where applicable).

---

### Publishing

#### Ownership

Please refer to `InterFAX <dev@interfax.net>` as the primary contributor/owner for the library (where applicable). You can refer to yourself and your email address as a secondary contributor (where possible). See the Ruby gem for an example.

##### Source

The source code should be published to github at the following location.

`https://github.com/interfax/interfax-{language}`

Please keep build/distribution files out of Github where possible.

##### Distribution

We'd like your help to publish the libraries to their respective most popular package managers. This would be:

- Java (?) - <http://mvnrepository.com>
- .Net - <https://nuget.org>
- PHP - <https://packagist.org>
- Ruby - <https://rubygems.org>
- Python - <https://pypi.python.org/pypi>
- Node.js - <https://www.npmjs.com>

Any feedback on these choices is more than welcome.

##### Releases

When releasing a new version please:

- Tag the release in github.
- Add release notes to the `CHANGELOG.md` and/or the `RELEASES` tab on Github
- Apply [semver rules](http://semver.org/)

---

### Documentation

Documentation is as important for a useful library as the code itself. We have identified the following core requirements for every library.

#### Title and badges

Please add a clear short title, e.g. "InterFAX {language} library". Additionally please add a badge for the version of your published library and the Travis badge for the build status. For example:

[![Gem Version](https://badge.fury.io/rb/interfax.svg)](https://badge.fury.io/rb/interfax) [![Build Status](https://travis-ci.org/interfax/interfax-ruby.svg?branch=master)](https://travis-ci.org/interfax/interfax-ruby)

#### Description

Please use a short description to highlight the following things:

* The language this library is for
* That it uses the REST API
* That it uses HTTPS
* That this library lets you "send and receive faxes"

#### Requirements

Please highlight language requirements, like the version of the language supported and any other things to consider

#### Installation

Please add clear instruction on how to install the library from the package manager. If it is common to install the library without the package manager then also provide instructions for this.

#### Getting started

Provide with a simple 3-5 line example on how to initialise the library and send your first fax.

#### Reference

After the installation and getting started docs please document every public API method of your library as follows:

* A title of the call
* The method signature
* A short description of the call (you can copy this from the Ruby library)
* A link to the relevant REST reference documentation
* A list of accepted arguments/options/parameters for the method
* A short code sample showing the method being used and a sample response

Please do not document the arguments and response in detail. Instead point to the relevant pages in the [REST reference documentation](https://www.interfax.net/en/dev/rest/reference).

#### Contribution

Please write a short but simple paragraph/list on how to contribute to this project.

#### License

A link to the [LICENSE](LICENSE) is required in the documentation.

---

### Tests

Your code should be well tested. Please apply the following guidelines:

* Test your library, not the API
* Do not make any actual API calls in your tests
  * Use a NET/HTTP mocking framework if needed
* Do not actually write to disk when testing saving files
  * Use a filesystem mocking framework if needed

#### Travis

Additionally prove a `.travis.yml` for your language. We will set your project up on Travis for testing. Please cover the following:

* Every common language version still
  1. In Use
  2. Officially supported
* Additionally if possible set add your language's latest build (e.g. `ruby-head`) but set this one to allow to fail.

For example:

```yml
language: ruby
sudo: false
cache: bundler
rvm:
  - 2.1
  - 2.2
  - 2.3.1
  - ruby-head
matrix:
  allow_failures:
    - rvm: ruby-head
```

----

### Samples

In some languages you can spin up a interactive shell, import the library, and start playing around with it. In others you can't; you either need to set up an entire project first (iOS) or you need to integrate it deeper into a framework (.NET). For these please provide the following 3 samples besides the documentation specified earlier.

These samples should live in a separate project. Ideally this should be named:

`https://github.com/interfax/interfax-{language}-samples`

#### Send a fax

Showcase how to send a fax from a document in a file.

Additionally show:

* How to get the Fax ID for the fax sent
* How to get the current status of the fax
* How to get the image for the fax sent and save it to disk

#### Get fax list

Showcase how to use get a list of sent faxes.

Additionally show:

* How to filter the list
* How to inspect the status of one of the faxes in the list

#### Receive a fax

Showcase how to use get a list of received faxes.

Additionally show:

* How to mark a fax as read
* How to get the image for the fax received and save it to disk
