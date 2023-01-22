# Flare Specification Version 1.0.0


## Introduction

Flare is a simple file format for streaming large datasets over HTTP(s). It resembles M3U and PLS, whereby a lightweight playlist file is downloaded to learn the locations of stream chunks.


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
* Chunk URLs SHOULD conform to [RFC-1738](https://www.rfc-editor.org/rfc/rfc1738).
* Chunk URLs SHOULD use the HTTP(s) scheme.


## Semantics

Each stream in SHOULD be independent such that its chunks can be downloaded without reference to any other stream.

Each stream chunk MUST be independent such that it can be downloaded without reference to any other chunk.

Stream headers are arbitrary objects. Their semantics SHOULD be decided by the client.
