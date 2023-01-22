<div align='center'>
	<img src='./images/flare.svg' width='30%'>
</div>


# Flare: A flexible file format for random access to big data

Flare provides efficient access to big datasets by only downloading chunks of data *when required* by an applicaiton. The locations of individual chunks are specified with URLs inside a lightweight playlist file. This is the only item of data neccessary for an application to subsequently access the complete dataset.


## Overview

Flare takes inspiration from multimedia streaming formats such as [M3U](https://en.wikipedia.org/wiki/M3U) and [PLS](https://en.wikipedia.org/wiki/PLS_(file_format)) to support arbitrary read access to unlimited quantities of data. Chunks can be downloaded in any order and be encoded in any format to accomodate for a broad range of applications. 


### Index Files

At the core of Flare, are *index files*. These are lightweight YAML files which specify the location of each chunk within dataset. An index file MUST have the following structure:

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

