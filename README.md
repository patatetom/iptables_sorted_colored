# iptables -S | sorted | colored

Sort and color the output of `iptables --list-rules`

![Sorted and colored output](iptables_sorted_colored.png)



## implementation

### iptsort

- download the [bash script](iptsort) in `/usr/local/bin/`
- after verification, make it executable with `chmod +x /usr/local/bin/iptsort`
- try it with `iptables -S | iptsort`.


### bat

- install (or download it in `/usr/local/bin/` if not available for your distribution) the excellent [bat](https://github.com/sharkdp/bat)
- build the necessary tree structure with `mkdir -p ~/.cache/bat/ ~/.config/bat/syntaxes/`
- download the [lexer](iptables.sublime-syntax) in `~/.config/bat/syntaxes/`
- rebuild the bat cache with `bat cache --build`
- try it with `iptables -S | bat`.

**that's all !**

you can now orchestrate the whole thing with `iptables -S | iptsort | bat`.



## trick

 you can add this helper in your `~/.bashrc` script :
 
```bash
function iptables {
  org=$( which iptables ) || return;
  if [ "${1}" ]
  then
    "${org}" $@
  else
    "${org}" -S | iptsort | bat -p
  fi
}
```

this following helper can also be very useful :

```bash
function ss {
  org=$( which ss ) || return;
  if [ "${1}" ]
  then
    "${org}" $@
  else
    "${org}" -plntu | sed -e 1d -e 's/users:(//g' -e 's/)$//g' | awk '{print $1, $5, $7}' | column -t | bat -pl c
  fi
}
```


---

the lexer was partially written using [Iro](https://eeyo.io/iro/).
