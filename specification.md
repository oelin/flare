# Flare Specification Version 1.0.0


## Introduction

Flare is a simple file format for streaming large datasets over HTTP(s). It resembles M3U and PLS formats, whereby a lightweight playlist file is downloaded in order to obtain URLs pointing to several stream chunks. The client downloads said chunks as needed.


## Syntax

A Flare file MUST be a *valid*, UTF-8 encoded YAML file with the following structure:

```yaml
<Stream 0 Name>:
    headers:
        ...
    content:
        - <Chunk 0 URL>
        - <Chunk 1 URL>
        - ...

<Stream 1 Name>:
    headers:
        ...
    content:
        - <Chunk 0 URL>
        - <Chunk 1 URL>
        - ...
```

where:

* Stream names MUST be unique.
* Chunk URLs SHOULD be unique.
* Chunk URLs SHOULD use the HTTP(s) scheme.
* `headers` MUST be an object.  
* `content` MUST be an array of URLs, as descrbed in [RFC-1738](https://www.rfc-editor.org/rfc/rfc1738).


## Semantics

Each stream in a Flare file SHOULD be independent of all other streams. This means its chunks can be downloaded without information provided by any other streams.
