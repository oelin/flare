<div align='center'>
	<img src='./images/flare.svg' width='30%'>
</div>


# Flare: Flexible, streamed access to big datasets 🔥

Flare provides streamed access to big datasets by partitioning them into bite-sized chunks that can be read asynchronously. The locations of individual chunks are stored in lightweight YAML files called *playlists*. Given a playlist, any portion of a dataset can be read without loading the whole file into memory.


## Overview

Flare takes inspiration from multimedia streaming formats such as [M3U](https://en.wikipedia.org/wiki/M3U) and [PLS](https://en.wikipedia.org/wiki/PLS_(file_format)) to simplify access to vast amounts of data on limited devices. The chunk abstraction allows applications to download only those portions of a dataset which they require *at runtime* and minimize unneccessary memory usage. The [Python reference implementation](https://github.com/oelin/flare-python) further makes use of layered LRU caching to minimize latency when reading chunks and allow prevent exhaustion of storage space.


### Playlists

At the core of Flare, are *playlists*. These are lightweight YAML files which store the locations of individual chunks. Playlists have the following structure:

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

A playlist is an array of streams. Streams are typically used to store distinct objects within a dataset, such as inputs or labels. Each stream has a name, headers and content. The stream headers are intended to communicate metadata about the stream such as encoding options. There are no standards about what must be specified here and they may be empty. The content of a stream is an array of chunk URLs. Each URL should typically use HTTPs, however some specific applications may use alterantive schemes.
