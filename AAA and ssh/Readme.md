## AAA and SSH

#### Configuring Local AAA Authentication for Console Access:

```
username the_name secret the_password
```

#### Enabling AAA on Router and configuring AAA authentication for the console login to use the local database:

```
aaa new-model

aaa authentication login default local
```

#### Verifying the AAA authentication method:

```
end

exit
```

## With SSH:

```
ip domain-name the_name

crypto generate rsa general-keys modulus 1024
```

#### Configuring a named list called SSH-LOGIN to authenticate logins using local AAA:

```
aaa authentication login SSH-LOGIN local
```

#### Configuring the vty lines to use the named AAA method and only allow SSH for remote access:

```
line vtu 0 4 

login authentication SSH-LOGIN   #the same name of list created lately   

transport input ssh

end  
```
