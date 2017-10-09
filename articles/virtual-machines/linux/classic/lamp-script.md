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
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="94a0d-103">Distribuire un'app di luce usando hello estensione CustomScript Azure per Linux</span><span class="sxs-lookup"><span data-stu-id="94a0d-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="94a0d-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="94a0d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="94a0d-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="94a0d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="94a0d-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="94a0d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="94a0d-107">Per informazioni sulla distribuzione di uno stack LAMP utilizzando il modello di gestione risorse hello, vedere [qui](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="94a0d-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="94a0d-108">Hello CustomScript estensioni di Microsoft Azure per Linux fornisce un toocustomize modo le macchine virtuali (VM) tramite l'esecuzione di codice arbitrario, scritto in qualsiasi linguaggio supportato da hello VM (ad esempio, Python e Bash).</span><span class="sxs-lookup"><span data-stu-id="94a0d-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="94a0d-109">Ciò fornisce un tooautomate molto flessibile macchine toomultiple di distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94a0d-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="94a0d-110">È possibile distribuire l'estensione CustomScript hello utilizzando hello hello interfaccia della riga di comando di Azure (Azure CLI), Windows PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="94a0d-111">In questo articolo che si userà hello Azure CLI toodeploy un semplice tooan di applicazione LAMP Ubuntu VM creato utilizzando il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="94a0d-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94a0d-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94a0d-112">Prerequisites</span></span>
<span data-ttu-id="94a0d-113">Per questo esempio, creare innanzitutto due macchine virtuali di Azure che eseguano Ubuntu 14.04 o la versione successiva.</span><span class="sxs-lookup"><span data-stu-id="94a0d-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="94a0d-114">Hello macchine virtuali vengono chiamate *script vm* e *lamp vm*.</span><span class="sxs-lookup"><span data-stu-id="94a0d-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="94a0d-115">Utilizzare nomi univoci per la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="94a0d-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="94a0d-116">Uno toorun utilizzati i comandi CLI di hello e uno utilizzato toodeploy hello LAMP app.</span><span class="sxs-lookup"><span data-stu-id="94a0d-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="94a0d-117">È inoltre necessario un account di archiviazione di Azure e una chiave tooaccess it (è possibile ottenere l'URL da hello portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="94a0d-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="94a0d-118">Per ulteriori informazioni sulla creazione di macchine virtuali Linux in Azure riferimento troppo[creare una macchina virtuale che esegue Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="94a0d-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="94a0d-119">comandi di installazione Hello presuppongono Ubuntu, ma è possibile adattare installazione hello per qualsiasi distribuzione Linux è supportata.</span><span class="sxs-lookup"><span data-stu-id="94a0d-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="94a0d-120">Hello script vm VM deve toohave installato CLI di Azure, con un tooAzure di connessione di lavoro.</span><span class="sxs-lookup"><span data-stu-id="94a0d-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="94a0d-121">Per informazioni, vedere troppo[installare e configurare l'interfaccia della riga di comando di Azure hello](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="94a0d-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="94a0d-122">Caricamento di uno script</span><span class="sxs-lookup"><span data-stu-id="94a0d-122">Upload a script</span></span>
<span data-ttu-id="94a0d-123">Verrà usata hello estensione CustomScript toorun uno script in uno stack LAMP hello di tooinstall VM remoto e creare una pagina PHP.</span><span class="sxs-lookup"><span data-stu-id="94a0d-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="94a0d-124">Nello script di hello tooaccess ordine ovunque si verrà caricato come un blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="94a0d-125">Panoramica di script</span><span class="sxs-lookup"><span data-stu-id="94a0d-125">Script overview</span></span>
<span data-ttu-id="94a0d-126">Nell'esempio di script Hello installa un tooUbuntu stack LAMP (inclusa l'impostazione di un'installazione invisibile all'utente di MySQL), scrive un semplice file PHP e avvia Apache.</span><span class="sxs-lookup"><span data-stu-id="94a0d-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

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

### <a name="upload-script"></a><span data-ttu-id="94a0d-127">Caricamento script</span><span class="sxs-lookup"><span data-stu-id="94a0d-127">Upload script</span></span>
<span data-ttu-id="94a0d-128">Salva script hello come un file di testo, ad esempio *install_lamp.sh*e quindi caricarla tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94a0d-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="94a0d-129">È possibile eseguire facilmente questa operazione con l’interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="94a0d-130">Hello esempio carica contenitore dell'archivio tooa file hello denominato "script".</span><span class="sxs-lookup"><span data-stu-id="94a0d-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="94a0d-131">Se il contenitore di hello non esiste, è necessario toocreate il primo.</span><span class="sxs-lookup"><span data-stu-id="94a0d-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="94a0d-132">Creare anche un file JSON che descrive la modalità toodownload hello script da archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="94a0d-133">Salva come *public_config.json* (sostituendo la risorsa "mystorage" con il nome di hello dell'account di archiviazione):</span><span class="sxs-lookup"><span data-stu-id="94a0d-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="94a0d-134">Distribuire l'estensione hello</span><span class="sxs-lookup"><span data-stu-id="94a0d-134">Deploy hello extension</span></span>
<span data-ttu-id="94a0d-135">È ora possibile usare hello successivo comando toodeploy hello estensione CustomScript Linux toohello remoto macchina virtuale con hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="94a0d-136">comando precedente Hello Scarica ed esegue hello *install_lamp.sh* script nella macchina virtuale denominata hello *lamp vm*.</span><span class="sxs-lookup"><span data-stu-id="94a0d-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="94a0d-137">Poiché l'applicazione hello include un server web, ricordare tooopen HTTP porta in ascolto su hello remoto macchina virtuale con il comando successivo hello.</span><span class="sxs-lookup"><span data-stu-id="94a0d-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="94a0d-138">Monitoraggio e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="94a0d-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="94a0d-139">È possibile controllare in modalità viene eseguito lo script personalizzato hello esaminando il file di log hello hello remoto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="94a0d-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="94a0d-140">SSH troppo*lamp vm* e file di log tail hello con il comando successivo hello.</span><span class="sxs-lookup"><span data-stu-id="94a0d-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="94a0d-141">Dopo aver eseguito hello estensione CustomScript, è possibile esplorare pagina PHP toohello creato per le informazioni.</span><span class="sxs-lookup"><span data-stu-id="94a0d-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="94a0d-142">Hello PHP pagina ad esempio hello in questo articolo è *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="94a0d-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94a0d-143">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="94a0d-143">Additional resources</span></span>
<span data-ttu-id="94a0d-144">È possibile utilizzare hello stesso toodeploy passaggi di base applicazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="94a0d-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="94a0d-145">In questo esempio, script di installazione hello è stato salvato come un blob pubblico in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94a0d-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="94a0d-146">Script di installazione hello toostore sarebbe un'opzione più sicura come un blob protetto con un [firma di accesso sicuro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="94a0d-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="94a0d-147">Risorse aggiuntive per l'interfaccia CLI di Azure, Linux e hello estensione CustomScript indicate successivamente.</span><span class="sxs-lookup"><span data-stu-id="94a0d-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="94a0d-148">Automatizzare le attività di personalizzazione delle macchine virtuali Linux utilizzando l'estensione CustomScript</span><span class="sxs-lookup"><span data-stu-id="94a0d-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="94a0d-149">Estensioni per Linux di Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="94a0d-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)