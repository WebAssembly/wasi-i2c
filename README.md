# WASI I2C

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

wasi-i2c is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg)

### Champions

- Friedrich Vandenberghe
- Merlijn Sebrechts
- Maximilian Seidler

### Portability Criteria

WASI-I2C must have at least an independent implementation for the following platforms: 
- Linux (ARM)
- Linux (RISC-V)
- RTOS (Zephyr or FreeRTOS)
- Microcontroller implementation (Cortex M4 as a lowerbound)

### Introduction

The WASI-I2C proposal defines an API for the I2C protocol. The API of [embedded_hal](https://github.com/rust-embedded/embedded-hal) is closely followed.

Reference implementations can be found in [i2c-wasm-components](https://github.com/Zelzahn/i2c-wasm-components). Furthermore, there is also a [wasi-embedded-hal](https://crates.io/crates/wasi-embedded-hal) crate that implements the `embedded-hal` traits for the generated bindings.

### Goals

The primary goal is to provide an interface that WASI programs can use to read and write data over an I2C connection.

### Non-goals

Although I2C is in some aspects not that different from SPI, the purpose of this proposal is to solely focus on I2C.

### API walk-through

The full API documentation can be found [here](wasi-proposal-template.md).

[Walk through of how someone would use this API.]

#### [Use case 1]

[Provide example code snippets and diagrams explaining how the API would be used to solve the given problem]

#### [Use case 2]

[etc.]

### Detailed design discussion

#### Should this be combined with SPI, GPIO and PWM into 1 embedded proposal?

Although `embedded_hal` takes this approach, I would keep them separated for now. At least until each proposal is at least in Phase 2.

#### Why are there no constructors for the i2c interface? How does one obtain an i2c handle?

I2c resources will be constructed in many different ways on different devices, so worlds that include the i2c interface should also include a way to obtain i2c handles. Typically this will either be by having i2c handles passed into exported functions as parameters, or by having i2c handles returned from imported functions.

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- Merlijn Sebrechts
- Dan Gohman for the `hello-embedded` repository
- Everyone else in SIG Embedded
