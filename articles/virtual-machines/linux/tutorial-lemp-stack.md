---
title: aaaDeploy LEMP in una macchina virtuale di Linux in Azure | Documenti Microsoft
description: Esercitazione - stack LEMP hello di installazione in una VM Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Installare un server Web LEMP in una macchina virtuale di Azure
In questo articolo illustra come un NGINX toodeploy web server, MySQL e PHP (stack LEMP hello) in una VM Ubuntu in Azure. stack LEMP Hello è un'alternativa toohello diffuso [stack LAMP](tutorial-lamp-stack.md), che è anche possibile installare in Azure. server LEMP toosee hello in azione, è facoltativamente possibile installare e configurare un sito WordPress. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare una VM Ubuntu (Buongiorno "L" nello stack LEMP hello)
> * Aprire la porta 80 per il traffico Web
> * Installare NGINX, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installa WordPress sul server LEMP hello


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Installare NGINX, MySQL e PHP

Eseguire le seguenti origini di comando tooupdate Ubuntu pacchetto hello e installare NGINX, MySQL e PHP. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Sono pacchetti hello tooinstall richiesta e altre dipendenze. Quando richiesto, è possibile impostare una password radice per MySQL e toocontinue [INVIO]. Seguire hello prompt rimanenti. Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL. 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificare l'installazione e la configurazione


### <a name="nginx"></a>NGINX

Controllare la versione di hello di NGINX con hello comando seguente:
```bash
nginx -v
```

Con NGINX installato e la porta 80 aprire tooyour VM, server web hello è ora possibile accedere da hello internet. pagina iniziale NGINX hello tooview, aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale. Utilizzare l'indirizzo IP pubblico hello utilizzato tooSSH toohello VM:

![Pagina NGINX predefinita][3]


### <a name="mysql"></a>MySQL

Controllare la versione di hello di MySQL con hello comando seguente (si noti il capitale hello `V` parametro):

```bash
msql -V
```

Si consiglia di eseguire script toohelp hello sicuro al termine dell'installazione di MySQL hello:

```bash
mysql_secure_installation
```

Immettere la password radice MySQL e configurare le impostazioni di sicurezza hello per l'ambiente.

Se si desidera toocreate un database MySQL, gli utenti di aggiungere o modificare le impostazioni di configurazione, account di accesso tooMySQL:

```bash
mysql -u root -p
```

Al termine, uscire dal prompt dei comandi mysql hello immettendo `\q`.

### <a name="php"></a>PHP

Controllare la versione di hello di PHP con hello comando seguente:

```bash
php -v
```

Configurare hello toouse NGINX gestore di processi FastCGI PHP (PHP FPM). Eseguire i seguenti comandi tooback server NGINX originale hello bloccare il file di configurazione e quindi modificare il file originale di hello in un editor di propria scelta hello:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

Nell'editor di hello, sostituire il contenuto di hello di `/etc/nginx/sites-available/default` con seguenti hello. Vedere i commenti di hello per una descrizione delle impostazioni di hello. Sostituire l'indirizzo IP pubblico hello della macchina virtuale per *yourPublicIPAddress*, lasciando hello rimanenti impostazioni. Quindi salvare il file hello.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Controllare la configurazione di NGINX hello errori di sintassi:

```bash
sudo nginx -t
```

Se la sintassi di hello è corretta, riavviare NGINX con hello comando seguente:

```bash
sudo service nginx restart
```

Se si desidera tootest ulteriormente, creare un rapido tooview pagina informazioni PHP in un browser. Hello comando seguente crea una pagina di informazioni di hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Ora è possibile controllare pagina delle info PHP hello che è stato creato. Aprire un browser e andare troppo`http://yourPublicIPAddress/info.php`. Sostituire l'indirizzo IP pubblico hello della macchina virtuale. Dovrebbe essere simile toothis immagine.

![Pagina di informazioni di PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è distribuito un server LEMP in Azure. Si è appreso come:

> [!div class="checklist"]
> * Creare una VM Ubuntu
> * Aprire la porta 80 per il traffico Web
> * Installare NGINX, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installa WordPress nello stack LEMP hello

Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.

> [!div class="nextstepaction"]
> [Secure web server with SSL (Proteggere il server Web con SSL)](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
