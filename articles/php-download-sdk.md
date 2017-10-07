---
title: hello aaaDownload Azure SDK per PHP
description: Informazioni su come toodownload e installare hello Azure SDK per PHP.
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>Scaricare hello Azure SDK per PHP
## <a name="overview"></a>Panoramica
Hello Azure SDK per PHP include i componenti che consentono di toodevelop, distribuiscono e gestire le applicazioni PHP per Azure. In particolare, hello Azure SDK per PHP include seguente hello:

* **Hello librerie client PHP per Azure**. Queste librerie di classi offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio i servizi di gestione dati e i servizi cloud.  
* **Interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI) Hello**. Un insieme di comandi che permette la distribuzione e la gestione di servizi di Azure, come Siti Web e Macchine virtuali di Azure. Hello lavoro CLI di Azure per qualsiasi piattaforma, tra cui Windows, Mac e Linux.
* **Azure PowerShell (solo Windows)**. Questo insieme di cmdlet di PowerShell consente la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali.
* **Emulatori di Azure (solo Windows) Hello**. emulatori di calcolo e archiviazione Hello sono emulatori locali di servizi cloud e servizi di gestione di dati che consentono di tootest locale di un'applicazione. Emulatori di Azure Hello eseguiti solo in Windows.

Hello nelle sezioni seguenti vengono descrivono come toodownload e installare hello componenti descritti in precedenza.

Hello istruzioni in questo argomento si presuppone di aver [PHP] [ install-php] installato.

> [!NOTE]
> È necessario disporre PHP 5.5 o le librerie client PHP hello toouse superiore per Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Librerie client PHP per Azure
le librerie Client di PHP Hello per Azure forniscono un'interfaccia per l'accesso alle funzionalità di Azure, ad esempio servizi di gestione dati e servizi cloud, da qualsiasi sistema operativo. Queste librerie possono essere installate tramite hello Composer.

Per informazioni su come toouse hello librerie Client di PHP per Azure, vedere [come tooUse hello servizio Blob][blob-service], [come tooUse hello del servizio tabelle] [ table-service] e [come tooUse hello servizio di Accodamento][queue-service].

### <a name="install-via-composer"></a>Installazione tramite Composer
1. [Installare Git][install-git].

    > [AZURE.NOTE] In Windows, è necessario anche variabile di ambiente PATH tooadd hello Git tooyour eseguibile.

1. Creare un file denominato **composer.json** in hello radice del progetto e aggiungere hello tooit di codice seguente:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Scaricare **[composer.phar][composer-phar]** nella radice del progetto.
3. Aprire un prompt dei comandi ed eseguire quanto segue nella radice del progetto
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell ed emulatori di Azure
Azure PowerShell è un insieme di cmdlet di PowerShell per la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali. Emulatori di Azure Hello sono emulatori di servizi cloud e servizi di gestione di dati che consentono di tootest locale di un'applicazione. Questi componenti sono supportati solo in Windows.

Hello consigliato tooinstall Azure PowerShell e hello emulatori di Azure è hello toouse [installazione guidata piattaforma Web di Microsoft][download-wpi]. Si noti che è possibile anche scegliere tooinstall altri componenti di sviluppo, ad esempio PHP, SQL Server, hello Microsoft Drivers for SQL Server per PHP e WebMatrix.

Per informazioni su come toouse Azure PowerShell, vedere [come tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
Hello CLI di Azure è un set di comandi per la distribuzione e gestione dei servizi di Azure, ad esempio siti Web di Azure e macchine virtuali di Azure. Per informazioni sull'installazione CLI di Azure, vedere [installazione hello Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
