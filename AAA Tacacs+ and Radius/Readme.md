## Tacacs+ server

#### On router: 

```
username Admin2 secret admin2pa55

tacacs-server host 192.168.2.2

tacacs-server key tacacspa55
```

#### configuring the AAA

```
aaa new-model

aaa authentication login default group tacacs+ local

line console 0 

login authentication default
```

#### Verifying:

```
end

write

exit
```





