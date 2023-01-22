# Flare Specification 1.0.0

## 1. Playlists

### 1.1. Syntax

A Flare playlist MUST be a *valid*, UTF-8 encoded YAML file with the following structure:

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


### 1.2. Semantics

Each stream in SHOULD be independent such that its chunks can be downloaded without reference to any other stream.

Each stream chunk MUST be independent such that it can be downloaded without reference to any other chunk.

Stream headers are arbitrary objects. Their semantics SHOULD be decided by the client.
