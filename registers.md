# Registers

* their **address does not change**
* can contain any data, like addresses of [chunks](chunks.md)
* each change to the data is stored in **history**

## Development

Registers are currently stored in a `Record` just like the other data types on the Network (Chunks and Spends). Those `Record`s have a fixed size limit that is configurable but it affects all other data types as well. This limit is currently 5mb.

Also we need to keep in mind that each *Register* entry (one entry = one version) comes along with its CRDT data and signatures so that’s an extra constant weight for each entry (roughly 500 bytes).

https://safenetforum.org/t/safe-api-registers/39182/85

* local first storage means [local first software](https://www.inkandswitch.com/local-first/)
* synchronising over Safe Network with multiple replicas using underlying MerkleReg CRDT from the rust [crdts](https://crates.io/crates/crdts) crate. There are a lot more data types in there too.
* a history of all previous states of the Register and its entries

you need to understand how to write entries and how to access entries in a way that makes sense for your application. None of that is straightforward because it is unfamiliar and not well documented yet.

Writing Entries though is easy! Getting the particular data back in a form useful in your app is not so easy. For example, you don’t have an array, or even a map of variable names to values. What you have is a set of one or more current values and access to the full history, or to any particular point in the history if you know the hash of the Node you want. 

For applications that just want the latest value (e.g. of a file or document) you could use one Register per document and track its history though the sequence of entries.

https://safenetforum.org/t/safe-api-registers/39182/77

`pub fn write(&mut self, entry: &[u8]) -> Result<()>`

https://safenetforum.org/t/safe-api-registers/39182/74
