# Linux version from zImage

```shell
    ZIMAGE=/boot/kernel.img
    IMG_OFFSET=$(LC_ALL=C grep -abo $'\x1f\x8b\x08\x00' $ZIMAGE | head -n 1 | cut -d ':' -f 1)
    dd if=$ZIMAGE obs=64K ibs=4 skip=$(( IMG_OFFSET / 4)) | zcat | grep -a -m1 "Linux version" | strings | awk '{ print $3; }'
```

# Linux version from kernel headers package

```shell
    dpkg -L raspberrypi-kernel-headers | egrep -m1 "/lib/modules/[^-]+/build" | awk -F'/' '{ print $4; }'
```

# Varible set/non-zero/default

```shell
    # When VAR set return set
    ${VAR+set}
    # When VAR non-set return NONESET
    ${VAR-NONESET}
    # When VAR has a non-zero length return ${VAR}, else return DEF
    ${VAR:-DEF}
    # When VAR has a non-zero length return ALTER, else return ""
    ${VAR:+ALTER}
```

# Find usage

```shell
    # Count files no hidden (not search hidden directory)
    find . ! \( -regex ".*/\..*" -prune \) -type f -printf "%-6s %p\n" | wc -l
    # Count files hidden include all files under hidden directory
    find . \( -regex ".*/\..*" \) -type f -printf "%-6s %p\n" | wc -l

    # Count files hidden,    include the ones under hidden directory
    find ./ \( -name ".*" \) -type f -print | wc -l
    # Count files no hidden, include the ones under hidden directory
    find . ! \( -name ".*" \) -type f -print | wc -l
    # Count files hidden exclude hidden directory
    find . \( -regex ".*/\..*" -prune \) -type f -printf "%-6s %p\n" | wc -l
```
