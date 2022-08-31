## Local Span

#### Example:

1. Access the Sniffer and click GUI.

2. Verify Service is set to On.

3. Click Edit Filters and select ICMP.

4. Leave the Sniffer window open.


#### Configuring SPAN on Switch or router:

```
monitor session 1 source interface f0/5         > Interface de exemplo

monitor session 1 destination interface f0/6    > Interface de exemplo

show monitor session 1
```

> Para verificar o trafego, entre no sniffer por exemplo
