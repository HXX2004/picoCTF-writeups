### 題目:
Do you know how to move between directories and read files in the shell? Start the container, ssh to it, and then ls once connected to begin.
### 提示:
1.Finding a cheatsheet for bash would be really helpful!
### 解法:
首先利用ssh去連線

`ssh ctf-player@xebec.cylabacademy.net -p 15068`

再輸入題目給的密碼進入
進入後先用ls看

```
ctf-player@academy-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@academy-chall$ cat 1of3.flag.txt
academy{xxsh_
ctf-player@academy-chall$ cat instructions-to-2of3.txt
Next, go to the root of all things, more succinctly `/`
```
順著提示繼續做下去
```
ctf-player@academy-chall$ cd /
ctf-player@academy-chall$ ls
2of3.flag.txt  boot       dev  home                      lib                lib64  mnt  proc  run   srv  tmp  var
bin            challenge  etc  instructions-to-3of3.txt  lib.usr-is-merged  media  opt  root  sbin  sys  usr
ctf-player@academy-chall$ cat 2of3.flag.txt
0ut_0f_//4t3r_
ctf-player@academy-chall$ cat instructions-to-3of3.txt
Lastly, ctf-player, go home... more succinctly `~`
```
接著下去，去取得第三部分的旗子
```
ctf-player@academy-chall$ cd ~
ctf-player@academy-chall$ ls
3of3.flag.txt  drop-in
ctf-player@academy-chall$ cat 3of3.flag.txt
47c47679}
```
最後再將旗子拼湊在一起
### 旗子:
academy{xxsh_0ut_0f_//4t3r_47c47679}
