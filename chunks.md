# Chunks

* **content-addressed** data structure, address is created from chunk's content's hash

## How do they work?

[Self encryption](self-encryption.md) requires at least 3 chunks. So 1MB of data is split into 3 x 333KB chunks to do the self encryption.

If its just a chunk being stored without self encryption then its one chunks instead of 3 (Assume another form of encryption is done) 

https://safenetforum.org/t/safe-api-registers/39182/59
