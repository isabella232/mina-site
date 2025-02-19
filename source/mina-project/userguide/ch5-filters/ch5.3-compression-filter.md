---
type: mina
title: 5.3 - Compression Filter
navPrev: ch5.2-buffered-write-filter.html
navPrevText: 5.2 - Buffered Write Filter
navUp: ch5-filters.html
navUpText: Chapter 5 - Filters
navNext: ch5.4-connection-throttle-filter.html
navNextText: 5.4 - Connection Throttle Filter
---

# 5.3 - Compression Filter

The _CompressionFilter_ class is used to compress data before it gets sent and decompress it when it's received. It uses the [JZLIB library](http://www.jcraft.com/jzlib/).

It only handles two events :

* _messageReceived_: The received message will be decompressed, if it's contained in a _IoBuffer_.
* _filterWrite_: The message to write will be compressed, assuming it's stored in a _IoBuffer_ (otherwise an exception will be generated).

## Configuration

It's possible to configure the _CompressionFilter_, with the listed parameters :

* _compressInbound_: if set to _true_, the incoming data will be decompressed, otherwise they will be left intact.
* _compressOutbound_: if set to _true_, the outgoing data will be compressed, otherwise they will be ignored.
* _compressionLevel_: one of _COMPRESSION_DEFAULT_ (-1), _COMPRESSION_MAX_ (9), _COMPRESSION_MIN_ (1), _COMPRESSION_NONE_ (0). Sets the level, of desired compression.

There is one more parameter that can be used, injected into the session's attributes, the _DISABLE_COMPRESSION_ONCE_ flag. If present in the session's attributes, the first compression will be ignored (this is probably useful for application that needs to send a message that the flowing messages are going to be compressed).

## Initialization

When the filter is added to the chain, instances of the deflater and inflater are created and injected into the session's attributes. This could change, as each session has its own instance of the filter in its chain, so there is no reason not to store those instances in the filter itself.


## Side notes

The way this filter works does not make it very efficient. It requires that the received data to be decompressed are fully read - and there are no control that it's the case of not -, and it also requires that the data to be compressed be fully compressed in one pass, which is quite inefficient from the memory perspective, as we may compress data by blocks, and send them immediately, waiting for the block to be really sent to compress the next one.

One more thing: there is no way this filter can be used to compress something like a file or anything that is not contained in a _IoFilter_. This is a pretty strong limitation.

All in all, it's a brittle filter, you'd better not use it as it is!

## Future improvements

So we need a compression filter that does not eat all the memory, possibly a stateless one - why should we have to create as many instances as we have sessions ? -, that is fast, AL 2.0 compatible, and that can flush data pieces by pieces.

### Stateless compression/decompression

The idea is to have a function that can be called statically, with a context. It's not necessarily complex  we just need to keep track of a context.

It should be possible top compress a block of data, send it, and process the next block when the first block has been processed. Same thing with received data: it should be possible to process a buffer, decompress it and wait for the remaining bytes until a block of data has been fully decompressed.