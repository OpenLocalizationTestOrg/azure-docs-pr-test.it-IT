---
title: aaaUse hello estensione CustomScript in una VM Linux | Documenti Microsoft
description: Informazioni su come applicazioni di toodeploy estensione CustomScript hello toouse in macchine virtuali Linux in Azure creato tramite il modello di distribuzione classica hello.
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Distribuire un'app di luce usando hello estensione CustomScript Azure per Linux
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sulla distribuzione di uno stack LAMP utilizzando il modello di gestione risorse hello, vedere [qui](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello CustomScript estensioni di Microsoft Azure per Linux fornisce un toocustomize modo le macchine virtuali (VM) tramite l'esecuzione di codice arbitrario, scritto in qualsiasi linguaggio supportato da hello VM (ad esempio, Python e Bash). Ciò fornisce un tooautomate molto flessibile macchine toomultiple di distribuzione dell'applicazione.

È possibile distribuire l'estensione CustomScript hello utilizzando hello hello interfaccia della riga di comando di Azure (Azure CLI), Windows PowerShell o il portale di Azure.

In questo articolo che si userà hello Azure CLI toodeploy un semplice tooan di applicazione LAMP Ubuntu VM creato utilizzando il modello di distribuzione classica hello.

## <a name="prerequisites"></a>Prerequisiti
Per questo esempio, creare innanzitutto due macchine virtuali di Azure che eseguano Ubuntu 14.04 o la versione successiva. Hello macchine virtuali vengono chiamate *script vm* e *lamp vm*. Utilizzare nomi univoci per la creazione di macchine virtuali hello. Uno toorun utilizzati i comandi CLI di hello e uno utilizzato toodeploy hello LAMP app.

È inoltre necessario un account di archiviazione di Azure e una chiave tooaccess it (è possibile ottenere l'URL da hello portale di Azure).

Per ulteriori informazioni sulla creazione di macchine virtuali Linux in Azure riferimento troppo[creare una macchina virtuale che esegue Linux](createportal.md).

comandi di installazione Hello presuppongono Ubuntu, ma è possibile adattare installazione hello per qualsiasi distribuzione Linux è supportata.

Hello script vm VM deve toohave installato CLI di Azure, con un tooAzure di connessione di lavoro. Per informazioni, vedere troppo[installare e configurare l'interfaccia della riga di comando di Azure hello](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Caricamento di uno script
Verrà usata hello estensione CustomScript toorun uno script in uno stack LAMP hello di tooinstall VM remoto e creare una pagina PHP. Nello script di hello tooaccess ordine ovunque si verrà caricato come un blob di Azure.

### <a name="script-overview"></a>Panoramica di script
Nell'esempio di script Hello installa un tooUbuntu stack LAMP (inclusa l'impostazione di un'installazione invisibile all'utente di MySQL), scrive un semplice file PHP e avvia Apache.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Caricamento script
Salva script hello come un file di testo, ad esempio *install_lamp.sh*e quindi caricarla tooAzure archiviazione. È possibile eseguire facilmente questa operazione con l’interfaccia della riga di comando di Azure. Hello esempio carica contenitore dell'archivio tooa file hello denominato "script". Se il contenitore di hello non esiste, è necessario toocreate il primo.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Creare anche un file JSON che descrive la modalità toodownload hello script da archiviazione di Azure. Salva come *public_config.json* (sostituendo la risorsa "mystorage" con il nome di hello dell'account di archiviazione):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Distribuire l'estensione hello
È ora possibile usare hello successivo comando toodeploy hello estensione CustomScript Linux toohello remoto macchina virtuale con hello CLI di Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

comando precedente Hello Scarica ed esegue hello *install_lamp.sh* script nella macchina virtuale denominata hello *lamp vm*.

Poiché l'applicazione hello include un server web, ricordare tooopen HTTP porta in ascolto su hello remoto macchina virtuale con il comando successivo hello.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Monitoraggio e risoluzione dei problemi
È possibile controllare in modalità viene eseguito lo script personalizzato hello esaminando il file di log hello hello remoto macchina virtuale. SSH troppo*lamp vm* e file di log tail hello con il comando successivo hello.

    cd /var/log/azure/customscript
    tail -f handler.log

Dopo aver eseguito hello estensione CustomScript, è possibile esplorare pagina PHP toohello creato per le informazioni. Hello PHP pagina ad esempio hello in questo articolo è *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Risorse aggiuntive
È possibile utilizzare hello stesso toodeploy passaggi di base applicazioni più complesse. In questo esempio, script di installazione hello è stato salvato come un blob pubblico in archiviazione di Azure. Script di installazione hello toostore sarebbe un'opzione più sicura come un blob protetto con un [firma di accesso sicuro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Risorse aggiuntive per l'interfaccia CLI di Azure, Linux e hello estensione CustomScript indicate successivamente.

[Automatizzare le attività di personalizzazione delle macchine virtuali Linux utilizzando l'estensione CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Estensioni per Linux di Azure (GitHub)](https://github.com/Azure/azure-linux-extensions)