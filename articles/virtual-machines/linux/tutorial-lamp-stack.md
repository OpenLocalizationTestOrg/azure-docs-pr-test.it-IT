---
title: aaaDeploy LAMP in una macchina virtuale di Linux in Azure | Documenti Microsoft
description: Esercitazione - stack LAMP hello di installazione in una VM Linux in Azure
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
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Installare un server Web LAMP in una macchina virtuale di Azure
In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in una VM Ubuntu in Azure. Se si preferisce server web NGINX di hello, vedere hello [stack LEMP](tutorial-lemp-stack.md) esercitazione. server di luce toosee hello in azione, è facoltativamente possibile installare e configurare un sito WordPress. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare una VM Ubuntu (Buongiorno "L" nello stack LAMP hello)
> * Aprire la porta 80 per il traffico Web
> * Installare Apache, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installa WordPress nel server di luce hello


Per ulteriori informazioni su stack LAMP hello, incluse le raccomandazioni per un ambiente di produzione, vedere hello [Ubuntu documentazione](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Installare Apache, MySQL e PHP

Eseguire le seguenti origini di comando tooupdate Ubuntu pacchetto hello e installare Apache, MySQL e PHP. Si noti hello punto di inserimento (^) alla fine di hello del comando hello.


```bash
sudo apt update && sudo apt install lamp-server^
```



Sono pacchetti hello tooinstall richiesta e altre dipendenze. Quando richiesto, è possibile impostare una password radice per MySQL e toocontinue [INVIO]. Seguire hello prompt rimanenti. Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL. 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificare l'installazione e la configurazione


### <a name="apache"></a>Apache

Controllare la versione di hello di Apache con hello comando seguente:
```bash
apache2 -v
```

In quest'ultimo installato e la porta 80 aprire tooyour VM, server web hello è ora possibile accedere da hello internet. Ciao tooview Apache2 Ubuntu predefinito pagina, aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale. Utilizzare l'indirizzo IP pubblico hello utilizzato tooSSH toohello VM:

![Pagina predefinita di Apache][3]


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

Se si desidera tootest ulteriormente, creare un rapido tooview pagina informazioni PHP in un browser. Hello comando seguente crea una pagina di informazioni di hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Ora è possibile controllare pagina delle info PHP hello che è stato creato. Aprire un browser e andare troppo`http://yourPublicIPAddress/info.php`. Sostituire l'indirizzo IP pubblico hello della macchina virtuale. Dovrebbe essere simile toothis immagine.

![Pagina di informazioni di PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è distribuito un server LAMP in Azure. Si è appreso come:

> [!div class="checklist"]
> * Creare una VM Ubuntu
> * Aprire la porta 80 per il traffico Web
> * Installare Apache, MySQL e PHP
> * Verificare l'installazione e la configurazione
> * Installa WordPress nel server di luce hello

Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.

> [!div class="nextstepaction"]
> [Secure web server with SSL (Proteggere il server Web con SSL)](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png