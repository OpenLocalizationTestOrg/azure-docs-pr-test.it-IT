---
title: aaaDeploy LAMP in una macchina virtuale di Linux in Azure | Documenti Microsoft
description: Informazioni su come tooinstall hello luce dello stack in una VM Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Distribuire lo stack LAMP in Azure
In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in Azure. È necessario un account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Breve riepilogo dei comandi

1. Salva e modifica hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) preferenza tooyour sul computer locale.
2. Eseguire i seguenti due comandi toocreate hello un gruppo di risorse e quindi distribuire il modello:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Distribuire LAMP in una VM esistente
esempio Hello comandi pacchetti di aggiornamenti, quindi installa Apache, MySQL e PHP:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Procedura dettagliata per distribuire LAMP in una nuova macchina virtuale

1. Creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create) toocontain hello nuova macchina virtuale:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate hello macchina virtuale stessa, è possibile utilizzare un modello di gestione risorse di Azure già scritto trovato [qui su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Salvare hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour di computer locale.
3. Modifica hello **azuredeploy.parameters.json** tooyour file preferito di input.
4. Distribuire il modello di hello con [distribuzione gruppo az crea] riferimento hello scaricato i file json:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Hello l'output è simile toohello seguente esempio:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

È stata creata una VM Linux con LAMP già installato. Se si desidera, è possibile verificare l'installazione hello passando troppo basso[verificare LAMP installato](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente
Se è necessario informazioni sulla creazione di una VM Linux, è possibile head [toolearn qui come toocreate una VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Successivamente, è necessario tooSSH in hello VM Linux. Per assistenza con la creazione di una chiave SSH, è possibile head [toolearn qui come una chiave SSH in Linux o Mac toocreate](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Ora che si lavora all'interno di VM Linux, è possibile scorrere l'installazione di stack LAMP hello in distribuzioni basate su Debian. per altre distribuzioni Linux, potrebbero essere diversi comandi Hello.

#### <a name="installing-on-debianubuntu"></a>Installazione in Debian/Ubuntu
È necessario hello seguenti pacchetti installati: `apache2`, `mysql-server`, `php5`, e `php5-mysql`. È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel.
Prima di installare è necessario toodownload e aggiornare gli elenchi di pacchetto.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Pacchetti singoli
Uso di apt-get:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Uso di Tasksel
In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Dopo aver eseguito una delle opzioni precedenti hello, sarà possibile tooinstall richiesta questi pacchetti e varie altre dipendenze. tooset una password amministrativa per MySQL, premere 'y' e 'Invio' toocontinue e seguire eventuali altre istruzioni. Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL. 

![][1]

Eseguire hello successivo comando toosee altre estensioni di PHP che sono disponibili come pacchetti:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Creare un documento info.php
Dovrebbe ora essere in grado di toocheck la versione di PHP, MySQL e Apache uso tramite riga di comando hello digitando `apache2 -v`, `mysql -v`, o `php -v`.

Se potrebbe ad esempio tootest, inoltre, è possibile creare un rapido tooview pagina informazioni PHP in un browser. Creare un file con l'editor di testo Nano con questo comando:

```bash
sudo nano /var/www/html/info.php
```

Nell'editor di testo hello GNU Nano aggiungere hello seguenti righe:

```php
<?php
phpinfo();
?>
```

Successivamente, salvare e chiudere l'editor di testo hello.

Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Verificare l'installazione di LAMP
Ora è possibile controllare pagina delle info PHP hello che aprendo un browser e passare toohttp://youruniqueDNS/info.php creato. Dovrebbe essere simile toothis immagine.

![][2]

È possibile controllare l'installazione di Apache visualizzando hello Apache2 Ubuntu predefinito pagina passando tooyou http://youruniqueDNS/. Hello l'output è simile toohello seguente esempio:

![][3]

È stato configurato uno stack LAMP nella VM di Azure.

## <a name="next-steps"></a>Passaggi successivi
Estrarre hello documentazione Ubuntu nello stack LAMP hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
