# Technical Analysis for Rust (ta)

[![Build Binaries](https://github.com/Sarsoo/ta-rs/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/Sarsoo/ta-rs/actions/workflows/build.yml)
[![Crates.io](https://img.shields.io/crates/v/ta)](https://crates.io/crates/finlib_ta)
[![Docs.rs](https://docs.rs/ta/badge.svg)](https://docs.rs/finlib_ta)
[![License](https://img.shields.io/crates/l/ta)](https://raw.githubusercontent.com/sarsoo/ta-rs/master/LICENSE)

[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua/)

Technical analysis library for Rust.

* [Getting started](#getting-started)
* [Basic ideas](#basic-ideas)
* [List of indicators](#list-of-indicators)
* [Running benchmarks](#running-benchmarks)
* [Donations](#donations)
* [License](#license)
* [Contributors](#contributors)

## Getting started

Add to you `Cargo.toml`:

```
[dependencies]
finlib-ta = "0.6.0"
```

Example:

```rust
use finlib_ta::indicators::ExponentialMovingAverage;
use finlib_ta::Next;

// it can return an error, when an invalid length is passed (e.g. 0)
let mut ema = ExponentialMovingAverage::new(3).unwrap();

assert_eq!(ema.next(2.0), 2.0);
assert_eq!(ema.next(5.0), 3.5);
assert_eq!(ema.next(1.0), 2.25);
assert_eq!(ema.next(6.25), 4.25);
```

See more in the examples [here](https://github.com/greyblake/ta-rs/tree/master/examples).
Check also the [documentation](https://docs.rs/ta).

## Basic ideas

A data item which represent a stock quote may implement the following traits:

* `Open`
* `High`
* `Low`
* `Close`
* `Volume`

It's not necessary to implement all of them, but it must be enough to fulfill requirements for a particular indicator.
You probably should prefer using `DataItem` unless you have reasons to implement your own structure.

Indicators typically implement the following traits:

* `Next<T>` (often `Next<f64>` and `Next<&DataItem>`) - to feed and get the next value
* `Reset` - to reset an indicator
* `Debug`
* `Display`
* `Default`
* `Clone`

## List of indicators

So far there are the following indicators available.

* Trend
    * Exponential Moving Average (EMA)
    * Hull Moving Average (HMA)
    * Weighted Moving Average (WMA)
    * Simple Moving Average (SMA)
* Oscillators
    * Relative Strength Index (RSI)
    * Fast Stochastic
    * Slow Stochastic
    * Moving Average Convergence Divergence (MACD)
    * Percentage Price Oscillator (PPO)
    * Commodity Channel Index (CCI)
    * Money Flow Index (MFI)
* Other
    * Minimum
    * Maximum
    * True Range
    * Standard Deviation (SD)
    * Mean Absolute Deviation (MAD)
    * Average True Range (AR)
    * Efficiency Ratio (ER)
    * Bollinger Bands (BB)
    * Chandelier Exit (CE)
    * Keltner Channel (KC)
    * Rate of Change (ROC)
    * On Balance Volume (OBV)

## Features

* `serde` - allows to serialize and deserialize indicators. NOTE: the backward compatibility of serialized
  data with the future versions of ta is not guaranteed because internal implementation of the indicators is a subject
  to change.

## Running benchmarks

```
cargo bench
```

## Donations

You can support the project by donating [NEAR tokens](https://near.org).

Our NEAR wallet address is `ta-rs.near`

## License

[MIT](https://github.com/sarsoo/ta-rs/blob/master/LICENSE) © [Sergey Potapov](http://greyblake.com/)

## Contributors

- [greyblake](https://github.com/greyblake) Potapov Sergey - creator, maintainer.
- [Bartoshko](https://github.com/Bartoshko) - BollingerBands
- [shreyasdeotare](https://github.com/shreyasdeotare) Shreyas Deotare - MoneyFlowIndex, OnBalanceVolume
- [edwardycl](https://github.com/edwardycl) - StandardDeviation Implementation & More Efficient BollingerBands
- [rideron89](https://github.com/rideron89) Ron Rider - Keltner Channel
- [tirz](https://github.com/tirz) - CCI, CE, MAD, PPO, refactorings
- [Devin Gunay](https://github.com/dgunay) - serde support
- [Youngchan Lee](https://github.com/edwardycl) - bugfix
- [tommady](https://github.com/tommady) - get rid of error-chain dependency
- [menkaru](https://github.com/menkaru) - WMA, HMA
