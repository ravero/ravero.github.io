---
layout: post
title: "Usando o SQL Server no macOS"
date: 2019-11-01 11:24:00 -0300
tags: sqlserver docker macos
---

O SQL Server foi durante muito tempo um produto exclusivo do Windows. Isso felizmente mudou com o lançamento da versão 2014 do produto, que passou a disponibilizar o serviço _Database Engine_ para instalação no Linux. Isso abriou novas possibilidades como disponibiliza-lo via Docker, e com isso podemos começar a ter o recurso dentro do macOS.

As imagens de Docker do SQL Server foram disponibilizadas pela própria Microsoft dentro do [**Docker Hub**](https://hub.docker.com/_/microsoft-mssql-server). Tendo o Docker instalado e em execução basta usar o comando:

```bash
sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
``` 

Isso irá baixar a imagem da última versão estável do SQL Server 2017 Database Engine disponível. Para subir criar uma nova instância use o seguinte comando:

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Senha" \
   -p 1433:1433 \
   --name sql1 \
   -d mcr.microsoft.com/mssql/server:2017-latest
```

Com isso será configurada uma nova instância que pode ser acessada diretamente por `localhost` e usando a porta padrão do SQL Server. Na prática é como se você tivesse um servidor local nos mesmos moldes do Windows. Para conferir se a instalação aconteceu corretamente, execute no terminal:

```
docker ps -a
```

Esse comando lista os processos ativos no Docker, o output deve ser semelhante ao abaixo:

![](/assets/images/docker-sql01.png)

Para acessar e administrar o servidor há diversas ferramentas disponíveis no macOS:

* [Azure Data Studio](https://docs.microsoft.com/en-us/sql/azure-data-studio/download?view=sql-server-ver15): Esse é um IDE multiplataforma da Microsoft para conectar-se e administrar servidores SQL Server. Ao longo do tempo deverá substituir o Management Studio quando incorporar mais de suas capacidades.
* [Plugin para VS Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql): Com esse plugin é possível acessar instâncias do SQL Server diretamente através do VS Code. Muito prático e conveniente.
* [mssql-cli](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15): Ferramentas de linha de comando multiplataforma para acessar instâncias do SQL Server. Bastante rica em recursos e prática para ações rápidas.

```bash
sudo docker start sql1
```


## Referências

* [Docker Hub](https://hub.docker.com/_/microsoft-mssql-server)
* [Quickstart: Run SQL Server container images with Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-2017&pivots=cs1-bash)
* [Setting up SQL server on Docker in Mac OS](https://getadigital.com/blog/setting-up-sql-server-on-docker-in-mac-os/)
