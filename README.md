# Urban Planning in the Paraverse with ink!

## Table of Contents
- [Introduction](#introduction)
- [Hybrid Chains](#hybrid-chains)
- [Smart Contract Advantages](#smart-contract-advantages)
    - [Ease of Development](#ease-of-development)
    - [Scalable Deployments](#scalable-deployments)
    - [Simple Maintenance](#simple-maintenance)
- [Smart Contracts and Hybrid Chains](#smart-contracts-and-hybrid-chains)
    - [Mixed-Use Development](#mixed-use-development)
- [ink! For Urban Planning](#ink-for-urban-planning)
    - [Chain-Extensions](#chain-extensions)
    - [Rust Integration](#rust-integration)
- [Conclusion](#conclusion)

## Intro

The current trend in the blockchain space is one in which application specific
blockchains (app-chains) are becoming more and more common. 

The idea that specilizaton is the be-all-end-all for the future of blockchain is overblown.

We seem to have forgotten that smart contracts will play a crutial role in this app-chain
world.

Their ease of development, deployment and flexibility creates developer velocity and
economic value in a way that app-chains cannot achieve on their own.

Smart contracts promote economic activity on app-chains in the same way restaurants and
shops do in a mixed-used neighbourhood.

Without smart contracts app-chains will turn into suburban nightmares.

## Hybrid Chains

Rob H. has a good post on the concept of hybrid chains. You should go read that in it's
entirety when you have a change. We'll summarize the concept here.
    - https://www.rob.tech/blog/hybrid-chains/

A hybrid chain is one which contains both application specific logic, as well as
smart contracts.

From the ink! side, we've historically referred to this as the concept of "smart
contracts as second class citizens". The idea that they exist on a blockchain whose
_raison d'etre_ isn't to just simply run smart contracts.

Rob argues that hybrid chains increase the efficiency of blockspace utilization and
economic value creation.

Rob doesn't really go into why ink! and smart contracts more generally are well suited,
so we'll do that here.

TODO: Re-read article and summarize properly

## Smart Contract Advantages

People often think that app-chains are the next evolution of smart contracts. However,
this is far from the case.

Smart contracts should instead be considered a standalone primitive for writing
applications. They come with their own advantages and trade-offs.

What are some of the reasons why we might want to use smart contracts instead of running
our own blockchain?

Smart contracts are typically:
- Simpler to develop
- More scalable to deploy
- Less complicated to maintain once deployed

Let's dig into each of these points a bit.

TODO: Something something blockchain aquisition

### Ease of Development

To make this a slightly more fair comparison, we'll assume that you're using Substrate, a
blockchain development framework, to build your app-chain. If you're writing your own
blockchain from scratch you've got a whole bunch of other problems ahead of you - good
luck!

Writing smart contracts, especially ink! ones, is relatively simple compared to building
writing pallets (i.e blockchain logic legos) to build a Substrate runtime. The main
reason being that smart contracts trade off performance and flexibility for ease of
development.

With smart contracts, you aren't able to customize core blockchain components like the
consensus engine or the transaction pool. However, by not being able to tune these
components you have less to worry about as a developer.

Smart contracts are run in a sandboxed environment. This limits the scope of their
contagion if a bad upgrade is applied. However, if you apply an erroneous runtime upgrade
you can end up bricking your blockchain and all the applications that live(d) on top of
it.

Smart contracts are also gas metered, whereas with a Substrate pallet you need to
manually perform benchmarking for all your public functions (dispatchables). If you get
this wrong you open your chain up to denial-of-service (DoS) attacks!

### Scalable Deployments

There are three things that make deploying smart contracts scalable:
1. Permisionless deployments
1. Small code sizes
1. Default to a dormant state

It is a combination of these three factors that a chain like Ethereum is able to support
nearly eight million smart contracts deployed on it in just 2022!
- https://www.alchemy.com/blog/web3-developer-report-q4-2022


For (1), typically as long as you have enough funds to cover the cost of putting the code
on-chain nobody can stop you from deploying code. 

For (2), smart contracts are typically quite small in size (on the order of kilobytes).
With consumer hardware it is possible to store millions of smart contracts and not worry
about disk space.

For (3), a smart contract typically doesn't run every block. Instead smart contracts are
mostly dormant creatures and they only wake when an off-chain actor pokes them. Millions
of contracts can lie dormant while a few hundred or thousand are actually running.

In their current state, app-specific chains don't have this kind of reach in terms of
deployments. In a world with thousands of app-chains, there may end up being billions of
smart contracts.

### Simple Maintenance

As we mentioned in the last section, once a smart contract is deployed on-chain they can
lie dormant as long as their underlying chain is still running. As a developer you don't
need to contantly worry about whether or not your code will disappear.

When you've deployed your own app-chain, you do need to worry about this.

Typically the way you'd keep your app running is by convincing block producers (e.g
validators or miners) to run infrastructure for your blockchain. This is often done
through the issuance of a token...which means you now have to worry about things like
token game theoretics, exchange listings, regulatory compliance, etc.

This sounds like quite a bit of work, when all you really wanted to do was deploy an
application and gets users playing with it, no?

## Smart Contracts and Hybrid Chains

Now that we understand some of the fundamental advantages of smart contracts, how can we
leverage these in the context of hybrid chains?

It all starts with the idea of _synchronous composability_. This is the idea that
applications can talk to each other in the _same block_.

We can contrast this with _asynchronous composability_, in which applications interact
with each other across a _variable number of blocks_.

Smart contracts are in a position to synchronously compose with the unique capabilies of
their underlying app-chain as well as other smart contracts which exist on the same
chain.


Okay cool, so what can we do with this?

For one, developers are able to leverage hybrid chains and synchronous composability to
increase their development velocity.

Let's consider a team building a parachain. In order to upgrade their chain's core
functionality they have to issue runtime upgrades. This typically involves a lot of work,
for example, making sure that new features have been benchmarked correctly or that any
necessary storage migrations have been applied.

The enactment of the runtime upgrade may also involve social coordination, for example in
the case where the parachain has a decentralized on-chain governance body approving
upgrades.

What if these same parachain authors were able to develop new features as smart contracts
instead? They could deploy them on to their chain much more quickly, they could get users
to play with the features sooner, and then once they were confident with the feature they
could translate that over into a runtime logic and _only then_ go through the whole song and
dance of a runtime upgrade.


We can also use hybrid chains and synchronous composability to improve the application
density of a given blockchain. Developers are not only able to interact with the
app-chain itself, but also with many different smart contracts in a fast and efficient
manner.

As long as we have the enough blockspace to support our workloads, a higher application
density will create more economic value.

A good example of this is the DeFi lego ecosystem in Ethereum. DeFi smart contracts build
off of each other to create increasing more sophisticated applications. Now imagine if we
could pull out all the common DeFi primitives into the core logic of the blockchain! This
is what hybrid chains will enable.


### Mixed-Use Development

We did tease an urban planning analogy at the beginning, so let's circle back to that.

We can think of app-chains as suburban developers or business districts. These types of
neighbourhoods are overly specialized towards one kind of use-case (living and work,
respectively). As soon as you want to do anything else you need to leave the
neighbourhood.

App-chains have the same problem. As soon as you want to do anything other than what the
app-chain exposes you need to leave the app-chain (either via bridges, or XCM in the
Paraverse).

This means extra overhead for running whatever errand you need to run. The more
specialized your app-chain is, the more often you'll need to pay for this.

Hybrid-chains are akin to mixed-use neighbourhoods. The magic in these types of
neighbourhoods stems from the facts that residents can easily live, work, and play all in
the same place.

Allowing smart contracts on app-chains we can create mixed-used neighbourhoods. Ones in
which different bits of logic are able to not only leverage the underlying chain's unique
selling point (e.g a nice beachfront location) but also work together with other
smart contracts (e.g a nice cafe by the water) to create economic value.

The higher the density of businesses, the more economic value that can be created.


Even in mixed-use neighbourhoods we'll still run into times that we need to run errands
elsewhere. The nice thing about deploying your contract on a Polkadot parachain is that
you get access to all the other neighbourhoods in the paraverse out of the box thanks to
XCM! Sure, running this errands wil take a bit more time and cost a bit more, but you can
do it.

## ink! for Urban Planning

In mixed-use neighbourhoods, why is is ink! uniquely suited to thrive? Two main reasons:
chain-extensions, and native Rust integrations.

### Chain-Extensions

One nice feature that ink! has is called _chain extensions_. This allows ink! contracts
to natively tap into the core functionality exposed by the app-chain the ink! contract is
running on.

There is also the flexible `CallBuidler`, which allows you to not only call other ink!
contracts but also Solidity contracts compiled using Solang.

This in combination of chain-extensions with the flexible `CallBuilder` gives contract
authors a lot of ways to integrate other applications in their own smart contracts.


### Rust Integration

If you've spent any time in the Polkadot ecosystem, it comes as no surprise that at the
moment it is very heavily biased towards Rust. The Polkadot reference implementation,
Substrate framework, and ink! are all written in Rust.

This gives ink! contracts a bit of an unfair advantage when adding new Polkadot or
Substrate features.

For example, the implementation of the SCALE codec used by ink! is the reference
implementation used by Polkadot and Substrate. From the ink! side there was nothing for
us to do but import the `parity-scale-codec` crate.

Similarly, when libraries for things like cross-chain messaging get split out from the
Polkadot and Substrate repositories ink! will be able to use them directly. No need to
reimplement all this tricky code correctly!

Our cross-chain errands will be no match for this level of integration!

## Conclusion

TODO: Write

## How do we go forward?
- Is it too radical to introduce the idea of pure-ink! chains in this post?
    - I feel like this could maybe be its own short post with a technical speicfication
- Same with the whole story around "The Merge"
- These two things could be their own blog post
    - Maybe something along the lines of "ink! as the gateway to Polkadot"
