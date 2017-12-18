PELICAN
=======

An implementation of the Pelican 2.0 MAC function, using AES.

Requires a modern Intel or AMD CPU with AES-NI support.

API
===

Pretty straightforward:

```c
#include "pelican.h"

void pelican_init(pelican_state *st,
                  const unsigned char key[pelican_KEYBYTES]);
                  
void pelican(pelican_state *st, unsigned char out[pelican_BYTES],
             const unsigned char *buf, size_t buf_len);
```

Call `pelican_init()` to initialize the state using the key `key`.

Then call `pelican()` to compute a MAC for the message `buf` of length
`buf_len` bytes. The 128-bit MAC is put into `out`.

The `pelican()` function can be called as many times as needed in
order to compute multiple tags with the same key, without having to
re-initialize the state.

Compilation
===========

Do not forget to tell your compiler to enable support for AES opcodes
with the `-maes` flag.

Recommended: `-Ofast -maes -march=native`

Uses AES-256 by default. Define `pelican_KEYBYTES=16` in order to use
AES-128 instead.

References
==========

* [The MAC function Pelican 2.0](https://eprint.iacr.org/2005/088.pdf)
(Joan Daemen, Vincent Rijmen)
