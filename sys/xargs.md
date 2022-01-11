# xargs

xargs is a powerfull tool

## multiple process parallel execution demo

````
nheim@vnc:~/config/scripts$ type toto
toto is a function
toto () 
{ 
    echo $@;
    sleep $(( ( RANDOM % 10 )  + 1 ))
}
nheim@vnc:~/config/scripts$ seq 1 20 | xargs -P5 -I# -n1 bash -c 'toto #'
1
2
4
3
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
````

this is in order, that mean that process are launched by 5 at the same time, then xargs wait for all 5 processes to finish, then only spawn a new process