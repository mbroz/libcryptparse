LibCryptParse
=============
Soon to be a library for parsing linux' `/proc/crypto` file

Now collecting `/proc/crypto` files from the wild to analyze them and search for
common patterns.

Contributing
------------
For now, you can help by running `./collect.sh` on your Linux machine. It should
be run from the project root directory and it will save a copy of your
`/proc/crypto` file into the `samples/` subdirectory. You may run
`cryptsetup benchmark` to load additional common ciphers/modes.

Observations
------------
Below is a table of relationships between cipher type and which fields it may
contain. A ✔ means the field is _always_ present, a ✕ means that field is
_never_ present, a . means the field may or may not be present. It may also
happen that a whole row is just empty, this happens if the supplied crypto file
lacks a cipher of that type.

This table is generated by the `./parse.py` script, which takes paths to crypto
files as command line arguments. So you can run `./parse.py /proc/crypto` to
genarate this table for your system, running `./parse.py samples/*/*` should
yield the table below.

|type/field |async|blocksize|chunksize|digestsize|driver|geniv|internal|ivsize|maxauthsize|max keysize|min keysize|module|name|priority|refcnt|seedsize|selftest|type|walksize|
|-----------|:---:|:-------:|:-------:|:--------:|:----:|:---:|:------:|:----:|:---------:|:---------:|:---------:|:----:|:--:|:------:|:----:|:------:|:------:|:--:|:------:|
|ablkcipher |✔    |✔        |✕        |✕         |✔     |✔    |.       |✔     |✕          |✔          |✔          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|aead       |✔    |✔        |✕        |✕         |✔     |✔    |.       |✔     |✔          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|ahash      |✔    |✔        |✕        |✔         |✔     |✕    |.       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|akcipher   |✕    |✕        |✕        |✕         |✔     |✕    |✔       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|blkcipher  |✕    |✔        |✕        |✕         |✔     |✔    |.       |✔     |✕          |✔          |✔          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|cipher     |✕    |✔        |✕        |✕         |✔     |✕    |.       |✕     |✕          |✔          |✔          |✔     |✔   |✔       |✔     |✕       |.       |✔   |✕       |
|compression|✕    |✕        |✕        |✕         |✔     |✕    |.       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|digest     |✕    |✔        |✕        |✔         |✔     |✕    |✕       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✕       |✔   |✕       |
|givcipher  |✔    |✔        |✕        |✕         |✔     |✔    |✕       |✔     |✕          |✔          |✔          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|kpp        |✕    |✕        |✕        |✕         |✔     |✕    |✔       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|nivaead    |✔    |✔        |✕        |✕         |✔     |✔    |✕       |✔     |✔          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|rng        |✕    |✕        |✕        |✕         |✔     |✕    |.       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✔       |✔       |✔   |✕       |
|scomp      |✕    |✕        |✕        |✕         |✔     |✕    |✔       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|shash      |✕    |✔        |✕        |✔         |✔     |✕    |.       |✕     |✕          |✕          |✕          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✕       |
|skcipher   |✔    |✔        |✔        |✕         |✔     |✕    |✔       |✔     |✕          |✔          |✔          |✔     |✔   |✔       |✔     |✕       |✔       |✔   |✔       |
