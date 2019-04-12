---
layout: post
title: "Publicar ASP.NET Core no CentOS"
date: 2019-04-12 11:37:00 -0300
categories: asp.net core
---

Recentemente precisei publicar um projeto ASP.NET Core em ambiente Linux, especificamente em um CentOS hospedado na Amazon. Foi a primeira vez que coloquei em prova as capacidades multi-plataforma do .NET Core, e tomei algum tempo aprendendo as particularidades para publicação nesse sistema operacional.

Como há diversos detalhes a serem observados quando se faz esse tipo de publicação, criei um passo a passo para facilitar nas próximas vezes. Nesse caso me baseiei no meu cenário especificamente com CentOS e Apache, mas caso precise publicar isso em algum outro _flavor_ do Linux ou com outro servidor como NGIX é relativamente simples adaptar o roteiro.

1. Instalar o Runtime do .NET Core
2. Instalar o Apache (httpd)
3. Copiar a aplicação para o servidor
4. Configurar o Proxy Reverso do Apache
5. Configurar o Serviço para execução do App Web
6. Configurar o Apache para ouvir as portas necessárias
7. Configurar o Firewall para liberar as portas necessárias

Nos próximos posts vou detalhar cada um desses passos.

## Referências
Para formular esse roteiro usei as seguintes referências:

* [Hosting ASP.NET Core in Linux with Apache](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-apache?view=aspnetcore-2.2#configure-a-proxy-server)
* [Kestrel Web Server Configuration in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-2.2)
* [How To Set Up a Firewall Using FirewallD on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)
* [Configure HTTPD to Listen on Multiple Ports](https://www.cyberciti.biz/faq/fedora-rhel-centos-configure-httpd-listen-multipleports/)