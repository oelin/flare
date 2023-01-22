<div align='center'>
	<img src='./images/flare.svg' width='30%'>
</div>


# Flare: Progressive streaming of large datasets

Flare is a tiny protocol for streaming large datasets over HTTPS. It works by partitioning datasets into small chunks which can be downloaded asynchronously. The locations of individual chunks are held in lightweight YAML files called *playlists*. Given a playlist, any portion of a dataset can then be read without loading the whole file into memory 🥳👌.


## Introduction

Flare takes inspiration from multimedia streaming formats such as [M3U](https://en.wikipedia.org/wiki/M3U) and [PLS](https://en.wikipedia.org/wiki/PLS_(file_format)), in which a single stream is divided into several chunks. This allows applications to download only those pieces of data which they require *at runtime* and minimize unneccessary memory usage. It also allows streams to be hosted on multiple servers for improved load balancing and locale-aware distribution.

Flare essentially brings these ideas to the data science domain.


## Playlists

At the core of Flare, are *playlists*. These are lightweight YAML files which store the locations of stream chunks and other metadata. Playlists have the following structure:

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
...
```

     
### Streams

A playlist consists of one or more *streams*. Streams are typically used to encompas a single *variable* or *object* within a dataset - for example in a supervised learning dataset, one stream may be used for inputs while another is used for labels. Streams have a name, headers and content, which are described below.


#### Headers

Stream headers are used to communicate metadata about a stream towards client applications. For example, they may indicate how stream chunks have been encoded or provide a natural language description of the stream. While these headers can be completely arbitrary, we recommend following the conventions described [here](https://github.com/oelin/flare-guidelines#stream-headers).


#### Content

Streams also contain an array of chunk URLs which denote where each chunk can be downloaded from.


## Conclusion

Flare is a simple, flexible format for streaming big datasets to limited devices. Our hope is that it positively contributes to the democratization of big data.


## Resources

* [Flare Python](https://github.com/oelin/flare-python) - A reference Flare client written in Python.
* [Tundra](https://github.com/oelin/tundra) - PyTorch APIs over Flare.
