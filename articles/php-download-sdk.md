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
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="0478f-103">Scaricare hello Azure SDK per PHP</span><span class="sxs-lookup"><span data-stu-id="0478f-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="0478f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0478f-104">Overview</span></span>
<span data-ttu-id="0478f-105">Hello Azure SDK per PHP include i componenti che consentono di toodevelop, distribuiscono e gestire le applicazioni PHP per Azure.</span><span class="sxs-lookup"><span data-stu-id="0478f-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="0478f-106">In particolare, hello Azure SDK per PHP include seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0478f-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="0478f-107">**Hello librerie client PHP per Azure**.</span><span class="sxs-lookup"><span data-stu-id="0478f-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="0478f-108">Queste librerie di classi offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio i servizi di gestione dati e i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="0478f-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="0478f-109">**Interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI) Hello**.</span><span class="sxs-lookup"><span data-stu-id="0478f-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="0478f-110">Un insieme di comandi che permette la distribuzione e la gestione di servizi di Azure, come Siti Web e Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0478f-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="0478f-111">Hello lavoro CLI di Azure per qualsiasi piattaforma, tra cui Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="0478f-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="0478f-112">**Azure PowerShell (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="0478f-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="0478f-113">Questo insieme di cmdlet di PowerShell consente la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0478f-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="0478f-114">**Emulatori di Azure (solo Windows) Hello**.</span><span class="sxs-lookup"><span data-stu-id="0478f-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="0478f-115">emulatori di calcolo e archiviazione Hello sono emulatori locali di servizi cloud e servizi di gestione di dati che consentono di tootest locale di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0478f-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="0478f-116">Emulatori di Azure Hello eseguiti solo in Windows.</span><span class="sxs-lookup"><span data-stu-id="0478f-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="0478f-117">Hello nelle sezioni seguenti vengono descrivono come toodownload e installare hello componenti descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0478f-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="0478f-118">Hello istruzioni in questo argomento si presuppone di aver [PHP] [ install-php] installato.</span><span class="sxs-lookup"><span data-stu-id="0478f-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="0478f-119">È necessario disporre PHP 5.5 o le librerie client PHP hello toouse superiore per Azure.</span><span class="sxs-lookup"><span data-stu-id="0478f-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="0478f-120">Librerie client PHP per Azure</span><span class="sxs-lookup"><span data-stu-id="0478f-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="0478f-121">le librerie Client di PHP Hello per Azure forniscono un'interfaccia per l'accesso alle funzionalità di Azure, ad esempio servizi di gestione dati e servizi cloud, da qualsiasi sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0478f-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="0478f-122">Queste librerie possono essere installate tramite hello Composer.</span><span class="sxs-lookup"><span data-stu-id="0478f-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="0478f-123">Per informazioni su come toouse hello librerie Client di PHP per Azure, vedere [come tooUse hello servizio Blob][blob-service], [come tooUse hello del servizio tabelle] [ table-service] e [come tooUse hello servizio di Accodamento][queue-service].</span><span class="sxs-lookup"><span data-stu-id="0478f-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="0478f-124">Installazione tramite Composer</span><span class="sxs-lookup"><span data-stu-id="0478f-124">Install via Composer</span></span>
1. <span data-ttu-id="0478f-125">[Installare Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="0478f-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="0478f-126">In Windows, è necessario anche variabile di ambiente PATH tooadd hello Git tooyour eseguibile.</span><span class="sxs-lookup"><span data-stu-id="0478f-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="0478f-127">Creare un file denominato **composer.json** in hello radice del progetto e aggiungere hello tooit di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0478f-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="0478f-128">Scaricare **[composer.phar][composer-phar]** nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="0478f-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="0478f-129">Aprire un prompt dei comandi ed eseguire quanto segue nella radice del progetto</span><span class="sxs-lookup"><span data-stu-id="0478f-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="0478f-130">Azure PowerShell ed emulatori di Azure</span><span class="sxs-lookup"><span data-stu-id="0478f-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="0478f-131">Azure PowerShell è un insieme di cmdlet di PowerShell per la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0478f-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="0478f-132">Emulatori di Azure Hello sono emulatori di servizi cloud e servizi di gestione di dati che consentono di tootest locale di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0478f-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="0478f-133">Questi componenti sono supportati solo in Windows.</span><span class="sxs-lookup"><span data-stu-id="0478f-133">These components are supported Windows only.</span></span>

<span data-ttu-id="0478f-134">Hello consigliato tooinstall Azure PowerShell e hello emulatori di Azure è hello toouse [installazione guidata piattaforma Web di Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="0478f-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="0478f-135">Si noti che è possibile anche scegliere tooinstall altri componenti di sviluppo, ad esempio PHP, SQL Server, hello Microsoft Drivers for SQL Server per PHP e WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="0478f-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="0478f-136">Per informazioni su come toouse Azure PowerShell, vedere [come tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="0478f-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="0478f-137">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0478f-137">Azure CLI</span></span>
<span data-ttu-id="0478f-138">Hello CLI di Azure è un set di comandi per la distribuzione e gestione dei servizi di Azure, ad esempio siti Web di Azure e macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0478f-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="0478f-139">Per informazioni sull'installazione CLI di Azure, vedere [installazione hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0478f-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0478f-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0478f-140">Next steps</span></span>
<span data-ttu-id="0478f-141">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0478f-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
