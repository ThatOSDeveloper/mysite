# KARM programming style

## General style

All code in KARM and any sister projects must be written in as simple format as possible.

Examples of what is not allowed:

```c
#include <log.h>

int function(void)
{
    uint64_t x = 1;
    return x;
}
```

A correct version of this code would read

```c
uint64_t function(void) {
    return 1;
}
```

It looks far more clean, and is more readable, has no unneeded inclusion, and looks better in general. Also this allows a more universal format, please fix formatting where needed.

## On the topic of inline ASM and architecture specific code being used in the rest of the kernel.

Both should be avoided, but it is permitted when needed.

### Inline Assembly

If Inline Assembly is needed for whatever reason that may be, unless 100% needed or its better off as just some small helper in an `#ifdef __arch__` auto or static function, it should be in its own file, under the arch, and exposed via a standard HAL.

### Calling arch specific functions

This is a major issue everywhere in the kernel, I have attempted to keep the two seperated but in many parts (especially the API or ACPI) I call upon specific x86_64 code such as the VMM. Any contribution to fix this would be greatly appreciated.