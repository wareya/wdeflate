# WDeflate

Public domain DEFLATE compressor and decompressor written in C99/C++11, using memory safe programming practices (stretchy buffers).

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
        comp.buffer.cur = 2;
        byte_buffer decomp = do_inflate(&comp.buffer, &error);
        printf("%d\n", error);
        printf("%s\n", decomp.data);
```
