# Contributor instructions

## Content to create

### 1. Wrapper library 

#### Method coverage

The following methods, available on the [InterFAX REST interface](https://www.interfax.net/en/dev/rest/reference) should be covered:

* A
* B
* C

#### Tests

#### Publishing destination

The library source code should be published Github at the following location: 

```
//interfax/interfax-{lang}
```

for example:

````
https://github.com/interfax/interfax-php
````

Where applicable, a compiled library will be published to one or both of the following destinations:

1. To the language-appropriate public package repository.
2. To the Github repository's 'releases'.

#### Documentation

##### 'Getting started' documentation

README.md file in the library's root folder. The file will include the following sections (see [reference for .Net](https://github.com/interfax/interfax-dotnet)):

* Introduction with link to developer registration (see reference link above)
* Table of contents
* Installation
    * Through the language-appropriate public package repository
    * Directly from the latest Github release
* Usage
* Examples - link to samples repo
* Documentation - link to further documentation on the public website as at the reference link above
* Support - boilerplate text available at the reference link above
* Contributing - boilerplate text available at the reference link above
* License - MIT license as at the reference link above
 
##### Library methods 

will be documented in ...

### 3. Usage samples

#### Coverage

##### 1. SendFax - Submitting a fax for transmission

* Send a single fax from a document in a file

##### 2. GetFaxStatus - Checking the status of a previously-submitted fax

* Retrieve list of completed faxes
* Retrieve status and metadata of newly-completed fax

##### 3. ReceiveFax - Polling for new faxes and retrieving them

* Retrieve list of unread incoming faxes
* Retrieve fax image for all unread faxes
* Mark retrieved faxes as read

#### Documentation

The samples will be documented on the public website under a language-specific "Getting Started" document (e.g.[Getting started faxing from C#](https://www.interfax.net/en/dev/getting-started/csharp). The contributor needs to provide any language-specific instructions.

#### Publishing destination

On Github: 
```
//interfax/interfax-{lang}-samples
```

## Uploading code to public package repositories

* ? Java - http://mvnrepository.com
* .Net - https://nuget.org
* PHP - Composer @ https://packagist.org / PEAR?
* Ruby - https://rubygems.org
* Python - https://pypi.python.org/pypi
* Perl - http://www.cpan.org
* Node.js - https://www.npmjs.com

### Naming

### Ownership
