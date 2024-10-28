# FP-SIG meeting at the RISC-V Summit, October 21st 2024

# Support for small formats (Discussion of Andrew W.'s proposal)

Andrew’s proposal for reduced precision support: https://lists.riscv.org/g/sig-vector/topic/109094169	

## Extended BFloat16 support

* New field `altfmt` in `vtype` [first use, but could be of general interest]
* **Zvfbfa**: https://github.com/aswaterman/riscv-misc/blob/34ac270c6f227d5ed7008810ef8e703e1d06f408/isa/zvfbfa.adoc	
* Answer larger need for computational operations for BF16 (except a few exclusions which are dimmed not necessary)
* Re-used existing opcodes by introducing `vtype.altfmt`

## Support for 8-bit and smaller formats

* Focusing on conversions for smaller / types
* Basic support for OFP8: conversions only (to BF16): **Zvfmx8min**, with four instructions, `vfwcvt.f.e4m3.v`, `vfwcvt.f.e5m2.v`, `vfncvt.e4m3.f.w`, and vfncvt.e5m2.f.w.:
FP4 / Int4: “Zvfmx4min, which adds two instructions, `vfext.vf2` and `vfext.vf4`”
* Putting aside IEEE P3109's binary8 for now (because of no commercial bases for it)
* Binary8 may stay separate from OFP8
* The cheer number of FP8 formats will warrant for adding only conversions and not actual operations
* Conversion to BF16 because of exponent (half/fp16 is too limited when we consider an actual product of OFP8 operands)
* Half precision target could be defined in parallel but in separate extensions

### Micro-scaling

* Scaling not supported as first class citizen (would be done through existing RVV instructions)
* May need performance data
* FP6 format is not part of the proposal

## What is next ?
  
* Andrew expecting technical feedback before RVIA would start working on the specifications themselves (as fast tracks or TGs)

# Discussing AME / IME

Andrew’s proposal: https://lists.riscv.org/g/tech-integrated-matrix-extension/attachment/159/0/zvmm-20241020.pdf	


# Other subjects

## Higher precision:

This subject is regularly mentioned but the conclusion seems to be the same as before.
There are no strong request for ISA support for floating-point precisions larger than double.
It seems some domain (quantum computing, astrophysics) could have a use for it but the SIG has still to hear from those potential users.

* Quad / Octo precision
* John Hauser “it would be nice if Q was used”
* currently in RISV-V `long double` maps to `binary128`
* Could be a good compromise to get the accuracy that double double is often used for
* Andrew and John: Consideration for partial support (double widening multiply to quad and only quad addition)
* KD: Do any of those proposals contain complex ?

## Decimal floating-point

* Not a lot of existing implementations in other ISAs
* Need to wait for actual user request

## Packed SIMD

* Has this ever been requested ? worked on ?
* AW: would need to make the case: why not use vector ?
