Title: NEM Development Resources

## Introduction

As NEMs innovative and solid blockchain solution is growing, the demand and development on top
 starts to grow as-well. But what are good resources to start with, to build a prototype application
 and/or production ready application on top of NEM?
 
In this post I will go through the most common SDK's and resources useful to get started into the NEM blockchain
 development.
 
To get a general idea about what NEM is and what NEM can do, check out the 
 [The Beginner's Guide to NEM](https://blog.nem.io/the-beginners-guide-to-nem/).
 
## Use Cases

The limit of use-case possibilities goes beyond my imagination, I guess. But one of the most common is:

 * Smart Contracts
   * React on transactions
   * Automate payments
   * Analyze and monitor account events
 * Automate other processes (e.g. multisig wallets)
 * Build and extend a frontend for wallets
 * Build a game on top of the blockchain (Item trades etc.)
 * Innovate ([LuxTag](http://luxtag.io/), [Landstead](http://landstead.atraurablockchain.com/), etc...)
 * [2FA](https://www.atraurablockchain.com/project/nem-authenticator/)
 * Everything within your imagination...
 
TIP: There are [bounties for given prototype projects](https://forum.nem.io/t/nem-s-prototype-project-bounty-program/2822), why not give it a try afterwards?

## Resources

### NEM NIS API

The NEM Network Infrastructure Server API.

Reading the [NEM NIS API](https://bob.nem.ninja/docs/) to get started is probably one of the best starting points out 
 there. It also gives a vague overview of what is possible and what not in interaction with the NIS.
 
Don't worry, when using the NEM Core package, it will give you some handsome interfaces of how to interact with NIS.

#### 

#### Existing API Wrappers

 * [nem-api](https://github.com/nikhiljha/nem-api) - A JavaScript API Wrapper for NIS
 * [csharp2nem](https://github.com/NemProject/csharp2nem) - A C# API Wrapper
 * [php2nem](https://github.com/NemProject/php2nem) - A PHP API Wrapper
 * [nis-ruby](https://github.com/44uk/nis-ruby) - A Ruby API Wrapper

PS: A good addition on the API documentation is [rb2nems - developer guide](https://rb2nem.github.io/nem-dev-guide/01-intro/).

### NEM Core

The Java package [nem.core](https://github.com/NemProject/nem.core) is probably one of the most solid SDKs to build
 on top. The reason is simple, NIS and NCC (now deprecated) are also using this and the NEM Team spent a lot of time
 and work in thoroughly testing the code in there.
 
Whereas the code and everything else is well-tested, it definitely lacks in documentation. A good start point to get
 started with nem.core is probably to check out those old but still up to date tutorials:
 
* [NEM Development 101 Episode 1](https://forum.nem.io/t/nem-development-101-episode-01-java-git-maven-nem-core/1656) 
* [NEM Development 101 Episode 2](https://forum.nem.io/t/nem-development-101-episode-02-idea-intellij-nem-core-vanity-gen/1665)

While those Tutorials are a perfect start point to learn a little bit on the build dependencies and building the nem.core
 module itself, they have no example of how to talk to a NIS API. Building around the NIS API is essential for any
 imaginable use case. 

Good resources of how to interact with the API are:

* [NEM Core API](https://bob.nem.ninja/org.nem.core/overview-summary.html)
* [rb2nem - nem programming](https://github.com/rb2nem/nem_programming)

Checking out the [code section](https://github.com/rb2nem/nem_programming/tree/master/code) is a good idea when getting
 stuck. It contains really nice and relevant examples.
 
#### Caveats
 
Specially rb2nems nem programming guide is using Groovy in favor of Java 8. There are some small adaptions to make in 
 order to get his run in Java. Here a few examples of required langauge conversion:

Filtering comparison between Groovy and Java leaning on the example of 
 [chapter 5](https://github.com/rb2nem/nem_programming/blob/master/code/05/groovy-monitoring.groovy#L36):
  
```groovy
// groovy code
// [...]
block.getTransactions().each { t -> 
    if (t.getType()==TransactionTypes.TRANSFER) {
        if (t.getAccounts().collect({it.getAddress()}).any({it.equals(monitored_address)})) {
            println "TRANSFER of ${t.getXemTransferAmount().getNumNem()} XEMs found!"
            println "Tx hash: ${HashUtils.calculateHash(t)}"
        }
    }
}
// [...]
```

```java
// java code
// [...]
block.getTransactions().stream()
    .filter(transaction -> transaction.getType() == TransactionTypes.TRANSFER &&
            transaction.getAccounts().contains(monitoredAccount))
    .forEach(transaction -> {
        if (t.getType() == TransactionTypes.TRANSFER) {
            println "TRANSFER of ${t.getXemTransferAmount().getNumNem()} XEMs found!"
            println "Tx hash: ${HashUtils.calculateHash(t)}"
        }
    });
// [...]
```

#### Example Projects

 * [nem.modules](https://github.com/NemProject/nem.modules) - Collection of communtiy nem modules
 * [NemCommunityClient](https://github.com/NemProject/NemCommunityClient) - The (now deprecated) official client

### NEM-sdk

[NEM-sdk](https://github.com/rb2nem/NEM-sdk) is the NEM Developer Kit for Node.js and the Browser. A pure JavaScript 
 implementation of the NIS REST API. It is well documented and used in a lot of open-source/demo projects within the
 community. It is probably currently the most widely used JavaScript implementation out there.
 
Here is the best starting point probably the
 [README.md](https://github.com/QuantumMechanics/NEM-sdk/blob/master/README.md) of the Github repository, which contains
 the entire documentation.
 
Have a look at the [examples](https://github.com/QuantumMechanics/NEM-sdk/tree/master/examples) if ever you find
 yourself stuck.
 
#### Tutorials

 * [](https://blog.nem.io/node-js-library/)
 
#### Example Projects

 * [NanoWallet](https://github.com/NemProject/NanoWallet) - The official slim wallet solution
 * [PacNEM](https://github.com/evias/pacNEM) - Pacman on top of the NEM blockchain
 * [NEMBot](https://github.com/evias/nem-nodejs-bot) - A bot used to cosign multisig transactions
 * [PayContentJS](https://github.com/aenima86/NEM-PayContentJS) - Content micro payment in NEM
 * [NEMPay](https://github.com/dgarcia360/NEMPay) - Transfer assets in an easy way
 
### NEM Library

The previous solution was the one written in JavaScript. This nice 3rd party library promises to be fully implemented
 in TypeScript. TypeScript brings a lot of nice features such as static code analysis and some ES7 features out of the
 box. This is where [NEM Library](https://nemlibrary.com/) kicks in. For people looking for some sugar: NEM Library
 claims to use a [Reactive](https://en.wikipedia.org/wiki/Reactive_programming) approach.
 
A good starting point here is the [Guide section](https://nemlibrary.com/guide/overview/) in documentation. As the
 NEM-sdk, this library is suited for Node.js and the Browser.
 
Don't forget to check out the [examples](https://github.com/aleixmorgadas/nem-library-examples) when getting stuck.
 
#### Example Projects

 * [Angular Seed Project](https://github.com/guillemsole/nem-library-angular2-seed) - Boilerplate Angular 4 Project
 * [Ionic Seed Project](https://github.com/guillemsole/nem-library-ionic2-seed) - Boilerplate Ionic 2 Project
 
## Last words

And now it's your turn!
If you don't have any idea, don't worry and get inspired by [those ideas](https://forum.nem.io/t/nem-s-prototype-project-bounty-program/2822).

Happy coding!