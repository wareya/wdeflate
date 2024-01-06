# WDeflate

Public domain DEFLATE compressor and decompressor written in C99/C++11, using memory safe programming practices (stretchy buffers).

Has been fuzzed with Jackalope.

Supports zlib and gzip headers, and also raw deflate streams.

zlib header support notes: zlib dictionary directives are not supported.

gzip (.gz) header support notes: If you want to decompress a gzip file with multiple "members" (i.e. what you get when you `cat` multiple gzip files together) you have to do it manually.

The above header support notes don't mean that the deflate implementation itself is incomplete. The deflate implementation is complete.

Example usage:

```c
        const char * test = "When I waked it was broad day, the weather clear, and the storm abated, so that the sea did not rage and swell as before. But that which surprised me most was, that the ship was lifted off in the night from the sand where she lay by the swelling of the tide, and was driven up almost as far as the rock which I at first mentioned, where I had been so bruised by the wave dashing me against it. This being within about a mile from the shore where I was, and the ship seeming to stand upright still, I wished myself on board, that at least I might save some necessary things for my use.";
        
        puts("compressing...");
        bit_buffer comp = do_deflate((const uint8_t *)test, strlen(test) + 1, 12, 1);
        for (size_t i = 0; i < comp.buffer.len; i++)
            printf("%02X ", comp.buffer.data[i]);
        puts("");

        int error = 0;
        puts("decompressing...");
        byte_buffer decomp = do_inflate(&comp.buffer, &error, 1);

        printf("%d\n", error);
        printf("%s\n", decomp.data);
```
