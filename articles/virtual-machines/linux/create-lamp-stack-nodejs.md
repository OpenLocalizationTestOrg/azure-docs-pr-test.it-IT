---
title: Distribuire LAMP in una macchina virtuale Linux con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come installare lo stack LAMP in una VM Linux in Azure
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
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a><span data-ttu-id="9f854-103">Distribuire lo stack LAMP con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9f854-103">Deploy LAMP stack with the Azure CLI 1.0</span></span>
<span data-ttu-id="9f854-104">Questo articolo illustra come distribuire un server Web Apache, MySQL e PHP (lo stack LAMP) in Azure.</span><span class="sxs-lookup"><span data-stu-id="9f854-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="9f854-105">Sono necessari un account Azure ([richiedere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e l'[interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) [connessa all'account Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9f854-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI](../../cli-install-nodejs.md) that is [connected to your Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9f854-106">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="9f854-106">CLI versions to complete the task</span></span>
<span data-ttu-id="9f854-107">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="9f854-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9f854-108">[Interfaccia della riga di comando di Azure 1.0]: interfaccia della riga di comando per i modelli di distribuzione classica e di Gestione risorsa (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="9f854-108">[Azure CLI 1.0] – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9f854-109">[Interfaccia della riga di comando di Azure 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="9f854-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="9f854-110">Distribuire LAMP in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="9f854-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="9f854-111">Procedura dettagliata per distribuire LAMP in una nuova VM</span><span class="sxs-lookup"><span data-stu-id="9f854-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="9f854-112">È possibile iniziare creando un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) che conterrà la nuova VM:</span><span class="sxs-lookup"><span data-stu-id="9f854-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain the new VM:</span></span>

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

<span data-ttu-id="9f854-113">Per creare la VM, è possibile usare un modello di Azure Resource Manager già pronto disponibile [qui in GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="9f854-113">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="9f854-114">Verrà visualizzata una risposta che chiede alcuni input aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="9f854-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
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

<span data-ttu-id="9f854-115">È stata creata una VM Linux con LAMP già installato.</span><span class="sxs-lookup"><span data-stu-id="9f854-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="9f854-116">Se si desidera verificare l'installazione, si può passare direttamente a [Verificare l'installazione di LAMP](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="9f854-116">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="9f854-117">Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="9f854-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="9f854-118">Per assistenza nella creazione di una macchina virtuale Linux, [qui sono disponibili informazioni su come creare una macchina virtuale Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f854-118">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9f854-119">È quindi necessario connettersi tramite SSH alla macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="9f854-119">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="9f854-120">Per assistenza nella creazione di una chiave SSH, [qui sono disponibili informazioni su come creare una chiave SSH in Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f854-120">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="9f854-121">Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="9f854-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="9f854-122">Ora che la macchina virtuale Linux è disponibile, viene illustrata l'installazione dello stack LAMP nelle distribuzioni basate su Debian.</span><span class="sxs-lookup"><span data-stu-id="9f854-122">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="9f854-123">I comandi possono essere leggermente diversi per le altre distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="9f854-123">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="9f854-124">Installazione in Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9f854-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="9f854-125">È necessario che siano installati i pacchetti seguenti: `apache2`, `mysql-server`, `php5` e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="9f854-125">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="9f854-126">È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel.</span><span class="sxs-lookup"><span data-stu-id="9f854-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="9f854-127">Di seguito sono fornite le istruzioni per entrambi le opzioni.</span><span class="sxs-lookup"><span data-stu-id="9f854-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="9f854-128">Prima dell'installazione, è necessario scaricare e aggiornare gli elenchi di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9f854-128">Before installing you need to download and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="9f854-129">Pacchetti singoli</span><span class="sxs-lookup"><span data-stu-id="9f854-129">Individual packages</span></span>
<span data-ttu-id="9f854-130">Uso di apt-get:</span><span class="sxs-lookup"><span data-stu-id="9f854-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="9f854-131">Uso di Tasksel</span><span class="sxs-lookup"><span data-stu-id="9f854-131">Using tasksel</span></span>
<span data-ttu-id="9f854-132">In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.</span><span class="sxs-lookup"><span data-stu-id="9f854-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="9f854-133">Dopo l'esecuzione di una delle due opzioni precedenti, verrà richiesto di installare questi pacchetti e altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9f854-133">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="9f854-134">Premere y e quindi INVIO per continuare e seguire eventuali altri comandi per impostare una password amministrativa per MySQL.</span><span class="sxs-lookup"><span data-stu-id="9f854-134">Press 'y' and then 'Enter' to continue, and follow any other prompts to set an administrative password for MySQL.</span></span> <span data-ttu-id="9f854-135">In questo modo vengono installate le estensioni PHP minime obbligatorie per l'uso di PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="9f854-135">This installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="9f854-136">Eseguire il comando seguente per visualizzare altre estensioni PHP disponibili come pacchetti:</span><span class="sxs-lookup"><span data-stu-id="9f854-136">Run the following command to see other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="9f854-137">Creare un documento info.php</span><span class="sxs-lookup"><span data-stu-id="9f854-137">Create info.php document</span></span>
<span data-ttu-id="9f854-138">Ora sarà possibile controllare la versione di Apache, MySQL e PHP disponibile digitando `apache2 -v`, `mysql -v` o `php -v` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="9f854-138">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="9f854-139">Per eseguire altri test, è possibile creare rapidamente una pagina di informazioni PHP da visualizzare in un browser.</span><span class="sxs-lookup"><span data-stu-id="9f854-139">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="9f854-140">Creare un file con l'editor di testo Nano con questo comando:</span><span class="sxs-lookup"><span data-stu-id="9f854-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="9f854-141">Nell'editor di testo GNU Nano aggiungere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="9f854-141">Within the GNU Nano text editor, add the following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="9f854-142">Quindi salvare e chiudere l'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="9f854-142">Then save and exit the text editor.</span></span>

<span data-ttu-id="9f854-143">Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.</span><span class="sxs-lookup"><span data-stu-id="9f854-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="9f854-144">Verificare l'installazione di LAMP</span><span class="sxs-lookup"><span data-stu-id="9f854-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="9f854-145">A questo punto è possibile aprire un browser e accedere a http://youruniqueDNS/info.php per controllare la pagina di informazioni PHP creata.</span><span class="sxs-lookup"><span data-stu-id="9f854-145">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="9f854-146">Dovrebbe avere un aspetto simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="9f854-146">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="9f854-147">È possibile controllare l'installazione di Apache visualizzando la pagina predefinita di Apache2 Ubuntu andando su http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="9f854-147">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="9f854-148">Dovrebbe essere visualizzata una schermata simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="9f854-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="9f854-149">È stato configurato uno stack LAMP nella VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f854-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f854-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f854-150">Next steps</span></span>
<span data-ttu-id="9f854-151">Vedere la documentazione di Ubuntu sullo stack LAMP:</span><span class="sxs-lookup"><span data-stu-id="9f854-151">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="9f854-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="9f854-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png