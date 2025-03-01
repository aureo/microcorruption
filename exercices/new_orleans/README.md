# New Orleans #

We start slowly with a rather straight-forward exercice.

The `create_password` crudely writes the password starting at address 0x2400, byte by byte:

```assembly
mov     #0x2400, r15
mov.b   #0x7c, 0x0(r15)
mov.b   #0x78, 0x1(r15)
```

The `check_password` then compares the input with that password, byte by byte:

```assembly
cmp.b   @r13, 0x2400(r14)
```

and stops after 8 characters:

```assembly
cmp	#0x8, r14
```

To solve this exercice, either directly enter the hex values and check the box for hex encoded input, or convert those hex values to ascii and enter the resulting string.

_The CPU completed in 2392 cycles._