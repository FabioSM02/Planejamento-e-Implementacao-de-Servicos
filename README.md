### Hello! :wave:

<div>
    <h4>
        O objetivo deste trabalho é demonstrar a implementação e configuração de um servidor DNS, através do programa de gestão de servidor Webmin.
        Contando com dois clientes Ubuntu 20.04 e dois servers Ubuntu 20.04 (primário e secundário) para este ambiente.
        Segue abaixo a topologia do projeto:
    </h4>
    <br/>
    <p align="center">
        <img src="https://cdn.discordapp.com/attachments/959988615222550528/980911790621868032/d68c3b2f-4d3a-418c-a250-bea7b3028147.jpg" alt="topologia">
    </p>

<br/><br/>

### Server

- Instalando Bind 9

```
$ sudo apt install -y bind9 bind9utils bind9-doc dnsutils
```

- Verificando o status do serviço

```
$ sudo systemctl status bind9
```

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980893721967099934/1bd74da6-a123-4003-a212-a569bcfc9a57.jpg" alt="Status Bind9" />
</p>

## Instalação Webmin

- Instale os pacotes de pré-requisitos:

```
$ sudo apt install wget apt-transport-https software-properties-common
```

### Importar chave do repositório do Webmin

- Anexando chave GPG do Webmin:

```
$ sudo wget http://www.webmin.com/jcameron-key.asc -O-
$ sudo apt-key add -
```

- Adicionando o repositório Webmin ao arquivo da lista de fontes

```
$ sudo add-apt-repository "deb [arch=amd64] http://download.webmin.com/download/repository sarge contrib"
```

- Instalando o Webmin

```
$ sudo apt install webmin
```

- Verificando o status do webmin

```
$ sudo systemctl status webmin
```

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980891539419054120/71319070-cf9d-4dcd-be70-23ba5e2da7cc.jpg" alt="Status Webmin" />
</p>

<br/>

- Configurando o ip fixo acessando o arquivo yaml em /etc/netplan

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980894307378692177/94c3c67c-9464-4ba8-b2c0-cd9d2eacdb87.jpg" alt="Configurando ip" />
</p>

<br/>

- Editando o arquivo 00-installer-config.yaml

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980894476442681384/5b8b51b1-2e6f-4732-819d-473216082831.jpg" alt="Configurando ip" />
</p>

<br/>

- Após a configuração do arquivo e aplicação do ip, iremos salvar utilizando o seguinte comando:

```
$ sudo netplan apply
```
- Para verificar se o ip foi aplicado na placa de rede executamos o seguinte comando:

```
$ ip a
```

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980918905243574272/unknown.png" alt="ip a" >
</p>

<br/>

### Client

- Acessando o webmin pelo cliente, através do ip do server na porta 10000 (https://172.16.1.10.10000/)

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980895807882530826/9a86328b-9c60-4452-8e22-c2848161a085.jpg" alt="Acessando o Webmin no navegador" />
</p>

<br/>

- Configurando Bind9: Servers > BIND DNS Server > create master zone

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980901743237955634/e2327dcd-99b5-421b-8379-e0b292cec49d.jpg" alt="Configurando Bind 9" />
</p>

<br/>

- Criando uma master zone

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980904091175772190/d44abc09-6224-42f9-9696-abf3de1de426.jpg" alt="Criação da master zone" />
</p>

<br/>

- Editando a Master Zone

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980904536988344400/2dddf99d-66e0-4879-a23d-8e5a46e660b6.jpg" alt="Edição master zone" />
</p>

<br/>

- Configurando os IPs dos hosts: Edit master zone > Addresses

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980904798842937344/ceed319f-caf1-40bd-9866-3d37c9c014b8.jpg" alt="Configurando Ips dos hosts" />
</p>

<br/>

- Atribuindo os nomes aos IPs dos hosts

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980904864626389093/5157878f-c0ed-4be6-89e2-c64b146243f3.jpg" alt="Atribuindo os nomes aos Ips dos hosts" />
</p>

<br/>

- Criando zona reversa: Create master zone > opçao: reverse (addresses to names)

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980904920909754428/7db4cf0e-a6e4-4912-b63c-e4f48a8fab24.jpg" alt="Ctiando zona reversa" />
</p>

<br/>

- Editando a zona reversa criada

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980905015185133608/da2f28d2-c258-4205-b100-a0ff7c461e2c.jpg" alt="Editando Zona Reversa" />
</p>

<br/>

- Dentro de reverse address records da zona reversa: Atribuindo os ips das máquinas com seus nomes de host

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980905768259833916/156001fd-1e38-4fcf-9395-6d948a2d5c7c.jpg" alt="Atribuindo ips das máquinas com nomes de host" />
</p>

<br/>

- Dentro de DNS Keys

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980905830641704960/f2e439ee-38f3-4c03-9df3-32b22f73eecc.jpg" alt="DNS Keys" />
</p>

<br/>

- Atribuir uma chave DNS

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980905902276231229/aa92d02d-719a-4558-b153-cf5ddcd9d2b3.jpg" alt="Atribuindo chave DNS" />
</p>

<br/>

- Reiniciando o BIND DNS Server pelo Webmin (parando o serviço e iniciando novamente)

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980906319986982962/fafee66b-969c-4cad-a024-ed28c3871340.jpg" alt="Reiniciando Bind DNS" />
</p>

<br/>

- Reiniciando Bind9 pelo prompt do Server

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980906956699082762/26b2d580-508f-4610-8889-f5c10f8b6547.jpg" alt="Reiniciando Bind 9" />
</p>

<br/>

- Configurando o server secundário no primário

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980907135401607198/5cb3cac7-ed1c-4188-9d24-c207134ddc5e.jpg" alt="Configuração server secundário a partir do primário" />
</p>

<br/>

- Configurando o server secundário pelo Webmin

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980908317100634142/20.jpg" alt="Configuração server secundário pelo webmin" />
</p>

<br/>

- Criando a slave zone (Webmin do Server secundário)

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980908317322936420/21.jpg" alt="Criação da Slave Zone" />
</p>

<br/>

- Configurando a transferência de zona no Server secundário

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980917732159651880/unknown.png" alt="Transferência de zona" />
</p>

<br/>

- Alteração do arquivo resolv.conf em /etc (em todas as máquinas)

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980908317805264916/23.jpg" alt="resolv.conf" />
</p>

<br/>

- Configurando no host para testar os Servers DNS criados

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980908318031765514/24.jpg" alt="Teste de server DNS" />
</p>

<br/>

- Testando via nslookup ou dig

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980909484446715994/unknown.png" alt="Testes" />
</p>

<br/>

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980910888339009596/unknown.png" alt="Testes" />
</p>

<br/>

<p align="center">
  <img src="https://cdn.discordapp.com/attachments/959988615222550528/980915084664635422/unknown.png" alt="Testes" />
</p>

<br/>

## </> Tecnologias utilizadas no projeto

- <a href="https://www.isc.org/bind/" target="_blank">Bind 9</a>
- <a href="https://www.webmin.com/" target="_blank">Webmin</a>
- <a href="https://www.samba.org/" target="_blank">Samba4</a>
- <a href="https://www.apache.org/" target="_blank">Apache 2</a>
- <a href="https://www.postfix.org/" target="_blank">Postfix</a>
- <a href="https://www.dovecot.org/" target="_blank">Dovecot</a>
    ## :page_with_curl: Licença

    <h4>Esse projeto está sob a licença MIT. Veja o arquivo <a href="https://github.com/FabioSM02/Planejamento-e-Implementacao-de-Servicos/blob/day01/LICENSE" target="_blank">License</a> para mais detalhes</h4>

    <h4 align="center">SEGMA 04 grupo 01 - 2022 - 1º semestre</h4>
</div>
