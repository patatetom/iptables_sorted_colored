# iptables -S | sorted | colored

Sort and color the output of `iptables --list-rules`

![Sorted and colored output](iptables_sorted_colored.png)



## implementation

### iptsort

- download [iptsort](iptsort) bash script in `/usr/local/bin/`
- after verification, make it executable with `chmod +x /usr/local/bin/iptsort`
- try it with `iptables -S | iptsort`
