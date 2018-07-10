# node-cure-outreach

In section 7 of our [paper](http://people.cs.vt.edu/~davisjam/downloads/publications/DavisWilliamsonLee-SenseOfTime-USENIXSecurity18.pdf) we described our efforts at outreach to the Node.js community.

Here are links to those efforts.

1. We wrote a [guide](https://nodejs.org/en/docs/guides/dont-block-the-event-loop/) for nodejs.org. Our guide describes how to avoid Event Handler Poisoning attacks in Node.js. Our [pull request](https://github.com/nodejs/nodejs.org/pull/1478) benefited from helpful feedback from community members.
2. We partitioned the implementation of `fs.readFile` in the core `fs` module. Before our change, `fs.readFile` would `stat` the file and then submit a single `read` spanning the entire file. If the file were large, this would block the Worker Pool. Our [pull request](https://github.com/nodejs/node/pull/17054) partitions the read into chunks, with the same overall memory cost but improved sharing of the Worker Pool. The pull request was accepted after a months-long discussion on the performance-security tradeoff involved.
3. We documented several "Vulnerable APIs", potential DoS vectors among the core APIs. These include [fs.readFile](https://github.com/nodejs/node/pull/17154) (before our patch), [crypto.randomBytes and crypto.randomFill](https://github.com/nodejs/node/pull/17250), and [child_process.spawn](https://github.com/nodejs/node/pull/21234).
