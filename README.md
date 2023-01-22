<div align='center'>
	<img src='./images/flare.svg' width='30%'>
</div>


# Flare: Progressive streaming of large datasets

Flare is a simple protocol for streaming large datasets over HTTPS. It revolves around splitting a dataset into small chunks and storing the chunk URLs within a playlist file. The playlist can then be used read any part of the dataset without loading the whole file into memory 🥳👌.


## Introduction

Flare takes inspiration from multimedia streaming formats such as [M3U](https://en.wikipedia.org/wiki/M3U) and [PLS](https://en.wikipedia.org/wiki/PLS_(file_format)), which split a single stream into several chunks; allowing applications to download only the parts they need. Chunking also allows streams to be hosted on multiple servers for greater redundancy, storage capacity, and download rates (i.e. CDNs). 

Flare aims to bring these benifits to the data science domain.


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

Flare is a simple protocol for streaming large datasets over HTTPS. We hope that it allows big data to be shared more easily between ordinary internet users.


## Resources

* [Flare Python](https://github.com/oelin/flare-python) - A reference Flare client written in Python.
* [Tundra](https://github.com/oelin/tundra) - PyTorch + Flare.
