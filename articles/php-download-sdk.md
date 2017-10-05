---
title: Download di Azure SDK per PHP
description: Informazioni su come scaricare e installare Azure SDK per PHP.
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
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="e10c7-103">Download di Azure SDK per PHP</span><span class="sxs-lookup"><span data-stu-id="e10c7-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="e10c7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e10c7-104">Overview</span></span>
<span data-ttu-id="e10c7-105">Azure SDK per PHP include componenti che consentono di sviluppare, distribuire e gestire applicazioni PHP per Azure.</span><span class="sxs-lookup"><span data-stu-id="e10c7-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="e10c7-106">In particolare, Azure SDK per PHP include i seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="e10c7-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="e10c7-107">**Librerie client PHP per Azure**.</span><span class="sxs-lookup"><span data-stu-id="e10c7-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="e10c7-108">Queste librerie di classi offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio i servizi di gestione dati e i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="e10c7-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="e10c7-109">**Interfaccia della riga di comando di Azure per Mac, Linux e Windows**</span><span class="sxs-lookup"><span data-stu-id="e10c7-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="e10c7-110">Un insieme di comandi che permette la distribuzione e la gestione di servizi di Azure, come Siti Web e Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e10c7-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="e10c7-111">L’interfaccia della riga di comando di Azure funziona su qualsiasi piattaforma, incluse le piattaforme Mac, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="e10c7-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="e10c7-112">**Azure PowerShell (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="e10c7-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="e10c7-113">Questo insieme di cmdlet di PowerShell consente la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e10c7-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="e10c7-114">**Emulatori di Azure (solo Windows)**.</span><span class="sxs-lookup"><span data-stu-id="e10c7-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="e10c7-115">Gli emulatori di calcolo e archiviazione sono emulatori locali di servizi cloud e di gestione dati che consentono di testare un'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="e10c7-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="e10c7-116">Gli emulatori di Azure funzionano solo su Windows.</span><span class="sxs-lookup"><span data-stu-id="e10c7-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="e10c7-117">Le sezioni seguenti illustrano come eseguire il download e l'installazione dei componenti sopra descritti.</span><span class="sxs-lookup"><span data-stu-id="e10c7-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="e10c7-118">Le istruzioni in questo argomento presuppongono che [PHP][install-php] sia installato.</span><span class="sxs-lookup"><span data-stu-id="e10c7-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="e10c7-119">È necessario avere PHP 5.5 o versione successiva per usare le librerie client PHP per Azure.</span><span class="sxs-lookup"><span data-stu-id="e10c7-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="e10c7-120">Librerie client PHP per Azure</span><span class="sxs-lookup"><span data-stu-id="e10c7-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="e10c7-121">Le librerie client PHP per Azure offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio i servizi di gestione dati e i servizi cloud, da qualsiasi sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e10c7-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="e10c7-122">Queste librerie possono essere installate tramite il programma di creazione.</span><span class="sxs-lookup"><span data-stu-id="e10c7-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="e10c7-123">Per informazioni su come usare le librerie client PHP per Azure, vedere [Come usare il servizio BLOB][blob-service], [Come usare il servizio tabelle][table-service] e [Come usare il servizio di accodamento][queue-service].</span><span class="sxs-lookup"><span data-stu-id="e10c7-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="e10c7-124">Installazione tramite Composer</span><span class="sxs-lookup"><span data-stu-id="e10c7-124">Install via Composer</span></span>
1. <span data-ttu-id="e10c7-125">[Installare Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="e10c7-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="e10c7-126">In Windows sarà inoltre necessario aggiungere l'eseguibile Git alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="e10c7-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="e10c7-127">Creare un file denominato **composer.json** nella radice del progetto, quindi aggiungere nel file il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e10c7-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="e10c7-128">Scaricare **[composer.phar][composer-phar]** nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="e10c7-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="e10c7-129">Aprire un prompt dei comandi ed eseguire quanto segue nella radice del progetto</span><span class="sxs-lookup"><span data-stu-id="e10c7-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="e10c7-130">Azure PowerShell ed emulatori di Azure</span><span class="sxs-lookup"><span data-stu-id="e10c7-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="e10c7-131">Azure PowerShell è un insieme di cmdlet di PowerShell per la distribuzione e la gestione di servizi di Azure, come servizi cloud e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e10c7-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="e10c7-132">Gli emulatori di Azure sono emulatori di servizi cloud e di gestione dati che consentono di verificare un'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="e10c7-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="e10c7-133">Questi componenti sono supportati solo in Windows.</span><span class="sxs-lookup"><span data-stu-id="e10c7-133">These components are supported Windows only.</span></span>

<span data-ttu-id="e10c7-134">È consigliabile installare Azure PowerShell e gli emulatori di Azure tramite l'[Installazione guidata piattaforma Web Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="e10c7-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="e10c7-135">Si noti che è inoltre possibile scegliere di installare altri componenti di sviluppo, come PHP, SQL Server, i driver Microsoft per SQL Server per PHP e WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e10c7-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="e10c7-136">Per informazioni sull'uso di Azure PowerShell, vedere [Come usare Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="e10c7-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="e10c7-137">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e10c7-137">Azure CLI</span></span>
<span data-ttu-id="e10c7-138">Un’interfaccia della riga di comando di Azure è un insieme di comandi per la distribuzione e la gestione di servizi di Azure, come Siti Web e Macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e10c7-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="e10c7-139">Per informazioni sull'installazione di Azure CLI, vedere [Installare Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e10c7-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e10c7-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e10c7-140">Next steps</span></span>
<span data-ttu-id="e10c7-141">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e10c7-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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
