# broken msg: “Mostre seu conhecimento em análise de pacotes e encontre a flag”

> https://shellterlabs.com/en/questions/arahacker-day-2017/broken-msg/

Como de praxe em desafios net, recebemos um pcap:
```shell
$ file net.pcapng
net.pcapng: pcap-ng capture file – version 1.0
```

Abrindo o arquivo com o wireshark e fazendo uma rápida análise, encontro alguns segmentos TCP com dados legíveis que podem ser lidos com a opção ¨tcp follow¨, que nada mais é que uma trollagem. Continuando a análise encontro o que parece ser algo encodado.

Extraio o conteúdo do pcapng usando o tcpflow: 
```shell
$ tcpflow -r net.pcapng
```

Ao exibir o conteúdo dos arquivos encontramos a trollagem, e o que parece ser três pedaços de um hash. Juntando e decodando em base32 obtenho a flag.

```shell
$ cat 192.168.001.19*
tranquilidade
procura aew man kkk
aew blz
e a flag...
NYZXI5ZQ
OJVV6MZU
ON4Q====

$ echo "NYZXI5ZQOJVV6MZUON4Q====" | base32 -d
*******_****
```

Sites:
https://shellterlabs.com
https://www.wireshark.org/
https://github.com/simsong/tcpflow
