# Sydney #

The `check_password` function successively compares the input with four litteral hex values, word by word:

```assembly
cmp	#0x452b, 0x0(r15)
...
cmp	#0x5d21, 0x2(r15)
...
cmp	#0x6035, 0x4(r15)
...
cmp	#0x704e, 0x6(r15)
```

The important information to keep in mind here is the part about memory organization (1.4.5) in the [MSP430 User Guide](https://www.ti.com/lit/ug/slau049f/slau049f.pdf):

> When using word instructions, only even
addresses may be used. **The low byte of a word is always an even address.
The high byte is at the next odd address.** For example, if a data word is located
at address xxx4h, then the low byte of that data word is located at address
xxx4h, and the high byte of that word is located at address xxx5h.

which means that we need to switch the bytes in each word.

For example, for the first comparison above to set the Z status bit, the memory at the address stored in r15 should be `2b45`.

_The CPU completed in 2245 cycles._
