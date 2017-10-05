---
title: Distribuire LAMP in una macchina virtuale Linux in Azure | Microsoft Docs
description: 'Esercitazione: installare lo stack LAMP in una macchina virtuale Linux in Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Installare un server Web LAMP in una macchina virtuale di Azure
Questo articolo illustra come distribuire un server Web Apache, MySQL e PHP (lo stack LAMP) in una VM Ubuntu in Azure. Se si preferisce il server Web NGINX, vedere l'esercitazione [LEMP stack](tutorial-lemp-stack.md) (Stack LEMP). Per verificare il funzionamento del server LAMP, è facoltativamente possibile installare e configurare un sito WordPress. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare una VM Ubuntu ("L" nello stack LAMP)
> * Aprire la porta 80 per il traffico Web
> * Installare Apache, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installare WordPress nel server LAMP


Per altre informazioni sullo stack LAMP, incluse le raccomandazioni per un ambiente di produzione, vedere la [documentazione di Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva. Eseguire `az --version` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Installare Apache, MySQL e PHP

Usare il comando seguente per aggiornare le origini dei pacchetti Ubuntu e installare Apache, MySQL e PHP. Si noti l'accento circonflesso (^) alla fine del comando.


```bash
sudo apt update && sudo apt install lamp-server^
```



Viene chiesto di installare i pacchetti e le altre dipendenze. Quando viene richiesto, impostare una password radice per MySQL e quindi premere [INVIO] per continuare. Seguire i prompt rimanenti. In questo modo vengono installate le estensioni PHP minime richieste per l'uso di PHP con MySQL. 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificare l'installazione e la configurazione


### <a name="apache"></a>Apache

Controllare la versione di Apache con il comando seguente:
```bash
apache2 -v
```

Con Apache installato e la porta 80 aperta per la macchina virtuale, è ora possibile accedere al server Web da Internet. Per visualizzare Apache2 Ubuntu Default Page (Pagina predefinita Apache2 Ubuntu), aprire un Web browser e immettere l'indirizzo IP pubblico della VM. Usare l'indirizzo IP pubblico usato per stabilire la connessione SSH alla VM:

![Pagina predefinita di Apache][3]


### <a name="mysql"></a>MySQL

Controllare la versione di MySQL con il comando seguente. Si noti il parametro `V` in maiuscolo:

```bash
msql -V
```

È consigliabile eseguire lo script seguente per proteggere l'installazione di MySQL:

```bash
mysql_secure_installation
```

Immettere la password radice per MySQL e configurare le impostazioni di sicurezza per l'ambiente.

Per creare un database MySQL, aggiungere utenti o modificare le impostazioni di configurazione, accedere a MySQL:

```bash
mysql -u root -p
```

Al termine, chiudere il prompt mysql digitando `\q`.

### <a name="php"></a>PHP

Controllare la versione di PHP con il comando seguente:

```bash
php -v
```

Per eseguire altri test, creare rapidamente una pagina di informazioni PHP da visualizzare in un browser. Il comando seguente crea la pagina di informazioni di PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Ora è possibile controllare la pagina di informazioni di PHP creata. Aprire un browser e passare a `http://yourPublicIPAddress/info.php`. Sostituire l'indirizzo IP pubblico della VM. Dovrebbe avere un aspetto simile a questa immagine.

![Pagina di informazioni di PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è distribuito un server LAMP in Azure. Si è appreso come:

> [!div class="checklist"]
> * Creare una VM Ubuntu
> * Aprire la porta 80 per il traffico Web
> * Installare Apache, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installare WordPress nel server LAMP

Passare all'esercitazione successiva per apprendere come proteggere i server Web con i certificati SSL.

> [!div class="nextstepaction"]
> [Secure web server with SSL (Proteggere il server Web con SSL)](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png