---
layout: default
title: Keepers
subtitle: incentive-following bots
description: Compete for profit opportunities created by the Maker system
---

### Introduction

The Maker system provides various opportunities for profit which help to
maintain market equilibrium. Strategies to arbitrage these opportunities can be
codified as keepers - automated bots which can detect and trade inefficiencies
across Dai Core, OasisDEX and various other exchanges.

It is expected that developers and operators will evolve their own keepers over
time. Below you will find a list of our reference keepers. Bear in mind that this
page is just a brief summary and you can find out more by reading individual keepers
READMEs present in their GitHub repositories, or even by reading their source code
which is usually quite well documented.


### bite-keeper

CDPs that fall below the safe collateralization ratio can be liquidated by any
external agent via an operation known as [bite]({{ "dai/1/api/bite" |
relative_url }}).

The **[bite-keeper](https://github.com/makerdao/bite-keeper)** constantly monitors
the `Tub` contract looking for unsafe cups and bites them the moment they
become unsafe. In future versions, it will take into account the profit it can
make by processing the liquidated collateral via [bust]({{ "dai/1/api/bust" |
relative_url }}) and only waste gas on bite if it can make it up by subsequent
arbitrage. For now, it's just a dumb keeper that bites any cups that become
unsafe.


### arbitrage-keeper

The **[arbitrage-keeper](https://github.com/makerdao/arbitrage-keeper)** performs
arbitrage on OasisDEX, `join`, `exit`, `boom` and `bust` actions. It constantly
scans for profitable arbitrage opportunities and executes them the moment they
become available. Although a bit dated, it provides valuable source of information
where to look for arbitrage opportunities in the Dai system and how to exploit them.
It also supports atomic risk-free arbitrage via the [tx-manager](https://github.com/makerdao/tx-manager)
contract.


### market-maker-keeper

The **[market-maker-keeper](https://github.com/makerdao/market-maker-keeper)** is actually
a set of keepers that facilitate market making on multiple exchanges. They all follow
the same configuration principles, and almost all of them are capable of covering
any DAI market provided an appropriate price feed is present.

As of today, the following exchanges are supported:
* OasisDEX,
* EtherDelta,
* RadarRelay and ERCdEX (via [Standard Relayer API](https://github.com/0xProject/standard-relayer-api)),
* Paradex,
* DDEX,
* Ethfinex,
* GoPax,
* HitBTC,
* IDEX,
* Bibox,
* OKEX,
* gate.io.


### cdp-keeper

The **[cdp-keeper](https://github.com/makerdao/cdp-keeper)** is responsible for
actively monitoring and managing open CDPs. In early versions it was only capable
only of topping up CDPs at risk of falling below the liquidation level, but
more functionality started being added to allow:

- automatically wiping debt when approaching the liquidatio ratio
- managing the dai volume to keep it within specific range

This keeper is still under development.
