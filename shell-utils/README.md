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

    # Find MSYS2 changes
    find / ! \( -regex "/proc.*" -prune -o -regex "/tmp.*" -prune \) -type f -newer /unins000.dat
    # Find MSYS  changes
    find / ! \( -regex "/proc.*" -prune -o -regex "/tmp.*" -prune \) -type f -newer /postinstall
```

# Get uncontinuous icmp_seq numbers

```shell
    logfile=ping-20190911.log
    max_nr=$(wc -l $logfile | awk '{ print $1; }'); (( max_nr -- ))
    nr_list=$(tail -n $(( max_nr )) $logfile | sed -re 's/^[0-9]+ bytes from [^:]+: icmp_seq=([0-9]+) .*$/\1/g')
    uc_nr=$(diff <(seq 1 $max_nr | tr ' ' '\n') <(echo $nr_list | tr ' ' '\n') | awk '$0 ~ /^<.*/{ printf "%s ", $2; }')
    echo $uc_nr
```

# Here document

```shell
    -EOF  - 选项用来标记 here document 的 limit string (<<-LimitString), 
          可以抑制输出时前边的tab(不是空格). 这可以增加一个脚本的可读性.
    "EOF"
    \EOF  当"limit string"被引用或转义那么就禁用了参数替换.
```

# Netcat transfer file
```shell
    # transfer $file_to_send from/to $server_addr port $port
    export file_to_send=u-boot-dtb.imx
    export server_addr=192.168.4.100
    export server_port=9000

    # server to client
    #   server
    tar -c ${file_to_send} | nc -lN ${server_port}
    #   client
    nc ${server_addr} ${server_port} | tar -x

    # client to server
    #   server
    nc -l ${server_port} | tar -x
    #   client
    tar -c ${file_to_send} | nc ${server_addr} ${server_port}
```

# Get git objects contents
```shell
    pushd .git/objects; objects=$(find ./ -type f | sed -e 's,\.,,g;s,/,,g' | sort); popd
    for i in $objects; do echo -ne "=== $i \n";git cat-file -p $i; echo; done
```

# Revert all file mode changes in git repository
```shell
    git diff --summary | while read l; do a=($l); m=${a[@]:2:1}; f=${a[@]:5}; chmod ${m: -3} "$f"; done
```
