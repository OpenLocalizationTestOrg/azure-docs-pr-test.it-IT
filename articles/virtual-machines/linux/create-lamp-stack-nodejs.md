---
title: aaaDeploy LAMP in una macchina virtuale Linux con hello Azure CLI 1.0 | Documenti Microsoft
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Distribuire stack LAMP con hello Azure CLI 1.0
In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in Azure. È necessario un Account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI di Azure](../../cli-install-nodejs.md) ovvero [connesso tooyour account Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0]-il nostro CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Distribuire LAMP in una VM esistente

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Procedura dettagliata per distribuire LAMP in una nuova macchina virtuale
Iniziare creando un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) che conterrà hello nuova macchina virtuale:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate hello macchina virtuale stessa, è possibile utilizzare un modello di gestione risorse di Azure già scritto trovato [qui su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Verrà visualizzata una risposta che chiede alcuni input aggiuntivi:

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

È stata creata una VM Linux con LAMP già installato. Se si desidera, è possibile verificare l'installazione hello passando troppo basso[verificare LAMP installato](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente
Se è necessario informazioni sulla creazione di una VM Linux, è possibile head [toolearn qui come toocreate una VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Successivamente, è necessario tooSSH in hello VM Linux. Per assistenza con la creazione di una chiave SSH, è possibile head [toolearn qui come una chiave SSH in Linux o Mac toocreate](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh exampleUsername@exampleDNS`.

Ora che si lavora all'interno di VM Linux, è possibile scorrere l'installazione di stack LAMP hello in distribuzioni basate su Debian. per altre distribuzioni Linux, potrebbero essere diversi comandi Hello.

#### <a name="installing-on-debianubuntu"></a>Installazione in Debian/Ubuntu
È necessario hello seguenti pacchetti installati: `apache2`, `mysql-server`, `php5`, e `php5-mysql`. È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel. Di seguito sono fornite le istruzioni per entrambi le opzioni.
Prima di installare è necessario toodownload e aggiornare gli elenchi di pacchetto.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Pacchetti singoli
Uso di apt-get:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Uso di Tasksel
In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Dopo aver eseguito una delle opzioni precedenti hello, sarà possibile tooinstall richiesta questi pacchetti e varie altre dipendenze. Premere 'y' e 'Invio' toocontinue e seguire eventuali altri tooset richiede una password amministrativa per MySQL. Consente di installare hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL. 

![][1]

Eseguire hello successivo comando toosee altre estensioni di PHP che sono disponibili come pacchetti:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Creare un documento info.php
Dovrebbe ora essere in grado di toocheck la versione di PHP, MySQL e Apache uso tramite riga di comando hello digitando `apache2 -v`, `mysql -v`, o `php -v`.

Se potrebbe ad esempio tootest, inoltre, è possibile creare un rapido tooview pagina informazioni PHP in un browser. Creare un file con l'editor di testo Nano con questo comando:

    user@ubuntu$ sudo nano /var/www/html/info.php

Nell'editor di testo hello GNU Nano aggiungere hello seguenti righe:

    <?php
    phpinfo();
    ?>

Successivamente, salvare e chiudere l'editor di testo hello.

Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Verificare l'installazione di LAMP
Ora è possibile controllare pagina delle info PHP hello che aprendo un browser e passare toohttp://youruniqueDNS/info.php creato. Dovrebbe essere simile toothis immagine.

![][2]

È possibile controllare l'installazione di Apache visualizzando hello Apache2 Ubuntu predefinito pagina passando tooyou http://youruniqueDNS/. Dovrebbe essere visualizzata una schermata simile a questa immagine.

![][3]

È stato configurato uno stack LAMP nella VM di Azure.

## <a name="next-steps"></a>Passaggi successivi
Estrarre hello documentazione Ubuntu nello stack LAMP hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png