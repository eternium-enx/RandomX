# RnX-keccak
RnX-keccak is a variant of the RandomX proof-of-work (PoW) algorithm that is optimized for general-purpose CPUs. RnXkeccak and RandomX use random code execution (hence the name) together with several memory-hard techniques to minimize the efficiency advantage of specialized hardware. RnXkeccak differs from RandomX by performing a sha3-512 hash of the final outputs of the executed programs instead of Blake2b. Additionally, a variable scratchpad is introduced which scales with Moore's Law.

## Overview

RnX-keccak utilizes a virtual machine that executes programs in a special instruction set that consists of integer math, floating point math and branches. These programs can be translated into the CPU's native machine code on the fly (example: [program.asm](doc/program.asm)). At the end, the outputs of the executed programs are consolidated into a 256-bit result using a cryptographic hashing function ([Sha3-512](https://keccak.team/files/Keccak-implementation-3.2.pdf)).

RnX-keccak can operate in two main modes with different memory requirements:

* **Fast mode** - requires 2080 MiB of shared memory.
* **Light mode** - requires only 256 MiB of shared memory, but runs significantly slower

Both modes are interchangeable as they give the same results. The fast mode is suitable for "mining", while the light mode is expected to be used only for proof verification.

## Documentation

Full specification is available in [specs.md](doc/specs.md).

Design description and analysis is available in [design.md](doc/design.md).

## Audits

Between May and August 2019, RandomX was audited by 4 independent security research teams:

* [Trail of Bits](https://www.trailofbits.com/) (28 000 USD)
* [X41 D-SEC](https://www.x41-dsec.de/) (42 000 EUR)
* [Kudelski Security](https://www.kudelskisecurity.com/) (18 250 CHF)
* [QuarksLab](https://quarkslab.com/en/) (52 800 USD)

The first audit was generously funded by [Arweave](https://www.arweave.org/), one of the early adopters of RandomX. The remaining three audits were funded by donations from the [Monero community](https://ccs.getmonero.org/proposals/RandomX-audit.html). All four audits were coordinated by [OSTIF](https://ostif.org/).

Final reports from all four audits are available in the [audits](audits/) directory. None of the audits found any critical vulnerabilities, but several changes in the algorithm and the code were made as a direct result of the audits. More details can be found in the [final report by OSTIF](https://ostif.org/four-audits-of-randomx-for-monero-and-arweave-have-been-completed-results/).

## Acknowledgements
* [RandomX](https://github.com/tevador/RandomX) - RandomX
* [tevador](https://github.com/tevador) - RandomX author
* [SChernykh](https://github.com/SChernykh) - contributed significantly to the design of RandomX
* [hyc](https://github.com/hyc) - original idea of using random code execution for PoW
* [Other contributors](https://github.com/tevador/RandomX/graphs/contributors)

RnXkeccak uses some source code from the following 3rd party repositories:
* Argon2d hashing function: https://github.com/P-H-C/phc-winner-argon2
