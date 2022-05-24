### Hello! :wave:

<div>
    <h4>
        Texto de boas vindas e explicação do projeto.
    </h4>
    <p 
        align="center" 
        style="max-width: 100%;"
    >
        <img src="" style=""/>
    </p>

    - Instalando Bind 9

```
$ sudo apt install -y bind9 bind9utils bind9-doc dnsutils
```

- Verificando o status do serviço

```
$ sudo systemctl status bind9
```

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

## </> Tecnologias utilizadas no projeto

- <a href="https://www.isc.org/bind/" target="_blank">Bind 9</a>
- <a href="https://www.webmin.com/" target="_blank">Webmin</a>
- <a href="https://www.samba.org/" target="_blank">Samba4</a>
- <a href="https://www.apache.org/" target="_blank">Apache 2</a>
- <a href="https://www.postfix.org/" target="_blank">Postfix</a>
    ## :page_with_curl: Licença

    <h4>Esse projeto está sob a licença MIT. Veja o arquivo License* para mais detalhes</h4>

    <h4 align="center">SEGMA 04 - 2022</h4>
</div>