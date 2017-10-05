---
title: Usare l'estensione CustomScript in una macchina virtuale Linux | Microsoft Docs
description: Informazioni su come utilizzare l'estensione CustomScript per distribuire le applicazioni in macchine virtuali Linux in Azure create utilizzando il modello di distribuzione classica.
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="8f766-103">Distribuire un'applicazione LAMP utilizzando l'estensione CustomScript di Azure per Linux</span><span class="sxs-lookup"><span data-stu-id="8f766-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8f766-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8f766-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8f766-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="8f766-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8f766-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="8f766-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8f766-107">Per informazioni sulla distribuzione di uno stack LAMP con il modello di Resource Manager, vedere [qui](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f766-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8f766-108">L'estensione CustomScript di Microsoft Azure per Linux fornisce un modo per personalizzare le macchine virtuali (VM) tramite l'esecuzione di codice arbitrario scritto in un linguaggio supportato dalla macchina virtuale (ad esempio, Python e Bash).</span><span class="sxs-lookup"><span data-stu-id="8f766-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="8f766-109">In tal modo è possibile automatizzare la distribuzione di applicazioni a più computer in un modo molto flessibile.</span><span class="sxs-lookup"><span data-stu-id="8f766-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="8f766-110">È possibile distribuire l'estensione CustomScript tramite il portale di Azure, Windows PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="8f766-111">In questo articolo utilizzeremo la CLI di Azure per distribuire una semplice applicazione LAMP a una macchina virtuale di Ubuntu creata utilizzando il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="8f766-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f766-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f766-112">Prerequisites</span></span>
<span data-ttu-id="8f766-113">Per questo esempio, creare innanzitutto due macchine virtuali di Azure che eseguano Ubuntu 14.04 o la versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8f766-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="8f766-114">Le macchine virtuali vengono chiamate *script-vm* e *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="8f766-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="8f766-115">Quando si creano macchine virtuali, utilizzare sempre nomi univoci.</span><span class="sxs-lookup"><span data-stu-id="8f766-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="8f766-116">Uno viene utilizzato per eseguire i comandi dell’interfaccia della riga di comando e uno viene utilizzato per distribuire l'applicazione LAMP.</span><span class="sxs-lookup"><span data-stu-id="8f766-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="8f766-117">Sono necessari anche un account di archiviazione di Azure e una chiave di accesso, che è possibile ottenere nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="8f766-118">Per informazioni sulla creazione delle macchine virtuali Linux in Azure, fare riferimento a [Creare una macchina virtuale che esegue Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="8f766-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="8f766-119">I comandi di installazione presuppongono Ubuntu, ma è possibile adattare l'installazione per qualsiasi distro Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="8f766-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="8f766-120">La macchina virtuale script-vm richiede l'interfaccia della riga di comando di Azure installata e una connessione ad Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="8f766-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="8f766-121">Per informazioni, fare riferimento a [Installare e configurare l'interfaccia della riga di comando multipiattaforma di Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8f766-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="8f766-122">Caricamento di uno script</span><span class="sxs-lookup"><span data-stu-id="8f766-122">Upload a script</span></span>
<span data-ttu-id="8f766-123">Si utilizzerà l'estensione CustomScript per eseguire uno script in una macchina virtuale remota per installare lo stack LAMP e creare una pagina PHP.</span><span class="sxs-lookup"><span data-stu-id="8f766-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="8f766-124">Per accedere ovunque ci si trovi, lo script viene caricato come blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="8f766-125">Panoramica di script</span><span class="sxs-lookup"><span data-stu-id="8f766-125">Script overview</span></span>
<span data-ttu-id="8f766-126">Lo script consente di installare uno stack LAMP in Ubuntu (inclusa l'impostazione di un'installazione invisibile all'utente di MySQL), di scrivere un semplice file PHP e di avviare Apache:</span><span class="sxs-lookup"><span data-stu-id="8f766-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="8f766-127">Caricamento script</span><span class="sxs-lookup"><span data-stu-id="8f766-127">Upload script</span></span>
<span data-ttu-id="8f766-128">Salvare lo script come file di testo, ad esempio *install_lamp.sh* e caricarlo nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="8f766-129">È possibile eseguire facilmente questa operazione con l’interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="8f766-130">Nell'esempio seguente il file viene caricato in un contenitore di archiviazione denominato "scripts".</span><span class="sxs-lookup"><span data-stu-id="8f766-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="8f766-131">se il contenitore non esiste, è necessario prima crearlo.</span><span class="sxs-lookup"><span data-stu-id="8f766-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="8f766-132">Creare inoltre un file JSON che descrive la procedura di download dello script dall'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="8f766-133">Salvare il file come *public_config.json* (sostituendo "mystorage" con il nome dell'account di archiviazione in uso):</span><span class="sxs-lookup"><span data-stu-id="8f766-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="8f766-134">Distribuzione dell'estensione</span><span class="sxs-lookup"><span data-stu-id="8f766-134">Deploy the extension</span></span>
<span data-ttu-id="8f766-135">A questo punto, è possibile utilizzare il seguente comando per distribuire l'estensione CustomScript di Linux alla macchina virtuale remota utilizzando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="8f766-136">In tal modo verrà scaricato ed eseguito lo script *install_lamp.sh* in una macchina virtuale denominata *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="8f766-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="8f766-137">Poiché l'applicazione include un server Web, ricordarsi di aprire una porta di ascolto HTTP nella macchina virtuale remota con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="8f766-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="8f766-138">Monitoraggio e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="8f766-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="8f766-139">È possibile controllare l'avanzamento dell'esecuzione dello script personalizzato esaminando il file di log nella macchina virtuale remota.</span><span class="sxs-lookup"><span data-stu-id="8f766-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="8f766-140">SSH per *lamp-vm* e tail per il file di log con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="8f766-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="8f766-141">Dopo aver eseguito l'estensione CustomScript, è possibile esplorare la pagina PHP creata per le informazioni.</span><span class="sxs-lookup"><span data-stu-id="8f766-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="8f766-142">La pagina PHP per l'esempio in questo articolo è *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="8f766-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f766-143">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8f766-143">Additional resources</span></span>
<span data-ttu-id="8f766-144">È possibile utilizzare gli stessi passaggi di base per distribuire applicazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="8f766-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="8f766-145">In questo esempio lo script di installazione è stato salvato come blob pubblico in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f766-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="8f766-146">Un'opzione più sicura sarebbe archiviare lo script di installazione come blob protetto con una [firma di accesso protetto](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="8f766-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="8f766-147">Di seguito sono riportate alcune risorse aggiuntive per l’interfaccia della riga di comando di Azure, Linux e l'estensione CustomScript:</span><span class="sxs-lookup"><span data-stu-id="8f766-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="8f766-148">Automatizzare le attività di personalizzazione delle macchine virtuali Linux utilizzando l'estensione CustomScript</span><span class="sxs-lookup"><span data-stu-id="8f766-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="8f766-149">Estensioni per Linux di Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="8f766-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)