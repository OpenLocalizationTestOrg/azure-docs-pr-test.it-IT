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
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="aa430-103">Distribuire stack LAMP con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa430-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="aa430-104">In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in Azure.</span><span class="sxs-lookup"><span data-stu-id="aa430-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="aa430-105">È necessario un Account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI di Azure](../../cli-install-nodejs.md) ovvero [connesso tooyour account Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="aa430-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="aa430-106">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="aa430-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="aa430-107">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="aa430-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="aa430-108">[Azure CLI 1.0]-il nostro CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="aa430-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="aa430-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="aa430-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="aa430-110">Distribuire LAMP in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="aa430-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="aa430-111">Procedura dettagliata per distribuire LAMP in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="aa430-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="aa430-112">Iniziare creando un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) che conterrà hello nuova macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="aa430-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

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

<span data-ttu-id="aa430-113">toocreate hello macchina virtuale stessa, è possibile utilizzare un modello di gestione risorse di Azure già scritto trovato [qui su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="aa430-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="aa430-114">Verrà visualizzata una risposta che chiede alcuni input aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="aa430-114">You should see a response prompting some more inputs:</span></span>

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

<span data-ttu-id="aa430-115">È stata creata una VM Linux con LAMP già installato.</span><span class="sxs-lookup"><span data-stu-id="aa430-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="aa430-116">Se si desidera, è possibile verificare l'installazione hello passando troppo basso[verificare LAMP installato](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="aa430-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="aa430-117">Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="aa430-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="aa430-118">Se è necessario informazioni sulla creazione di una VM Linux, è possibile head [toolearn qui come toocreate una VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa430-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="aa430-119">Successivamente, è necessario tooSSH in hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="aa430-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="aa430-120">Per assistenza con la creazione di una chiave SSH, è possibile head [toolearn qui come una chiave SSH in Linux o Mac toocreate](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa430-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="aa430-121">Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="aa430-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="aa430-122">Ora che si lavora all'interno di VM Linux, è possibile scorrere l'installazione di stack LAMP hello in distribuzioni basate su Debian.</span><span class="sxs-lookup"><span data-stu-id="aa430-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="aa430-123">per altre distribuzioni Linux, potrebbero essere diversi comandi Hello.</span><span class="sxs-lookup"><span data-stu-id="aa430-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="aa430-124">Installazione in Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="aa430-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="aa430-125">È necessario hello seguenti pacchetti installati: `apache2`, `mysql-server`, `php5`, e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="aa430-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="aa430-126">È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel.</span><span class="sxs-lookup"><span data-stu-id="aa430-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="aa430-127">Di seguito sono fornite le istruzioni per entrambi le opzioni.</span><span class="sxs-lookup"><span data-stu-id="aa430-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="aa430-128">Prima di installare è necessario toodownload e aggiornare gli elenchi di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="aa430-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="aa430-129">Pacchetti singoli</span><span class="sxs-lookup"><span data-stu-id="aa430-129">Individual packages</span></span>
<span data-ttu-id="aa430-130">Uso di apt-get:</span><span class="sxs-lookup"><span data-stu-id="aa430-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="aa430-131">Uso di Tasksel</span><span class="sxs-lookup"><span data-stu-id="aa430-131">Using tasksel</span></span>
<span data-ttu-id="aa430-132">In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.</span><span class="sxs-lookup"><span data-stu-id="aa430-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="aa430-133">Dopo aver eseguito una delle opzioni precedenti hello, sarà possibile tooinstall richiesta questi pacchetti e varie altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="aa430-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="aa430-134">Premere 'y' e 'Invio' toocontinue e seguire eventuali altri tooset richiede una password amministrativa per MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa430-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="aa430-135">Consente di installare hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa430-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="aa430-136">Eseguire hello successivo comando toosee altre estensioni di PHP che sono disponibili come pacchetti:</span><span class="sxs-lookup"><span data-stu-id="aa430-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="aa430-137">Creare un documento info.php</span><span class="sxs-lookup"><span data-stu-id="aa430-137">Create info.php document</span></span>
<span data-ttu-id="aa430-138">Dovrebbe ora essere in grado di toocheck la versione di PHP, MySQL e Apache uso tramite riga di comando hello digitando `apache2 -v`, `mysql -v`, o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="aa430-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="aa430-139">Se potrebbe ad esempio tootest, inoltre, è possibile creare un rapido tooview pagina informazioni PHP in un browser.</span><span class="sxs-lookup"><span data-stu-id="aa430-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="aa430-140">Creare un file con l'editor di testo Nano con questo comando:</span><span class="sxs-lookup"><span data-stu-id="aa430-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="aa430-141">Nell'editor di testo hello GNU Nano aggiungere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="aa430-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="aa430-142">Successivamente, salvare e chiudere l'editor di testo hello.</span><span class="sxs-lookup"><span data-stu-id="aa430-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="aa430-143">Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.</span><span class="sxs-lookup"><span data-stu-id="aa430-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="aa430-144">Verificare l'installazione di LAMP</span><span class="sxs-lookup"><span data-stu-id="aa430-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="aa430-145">Ora è possibile controllare pagina delle info PHP hello che aprendo un browser e passare toohttp://youruniqueDNS/info.php creato.</span><span class="sxs-lookup"><span data-stu-id="aa430-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="aa430-146">Dovrebbe essere simile toothis immagine.</span><span class="sxs-lookup"><span data-stu-id="aa430-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="aa430-147">È possibile controllare l'installazione di Apache visualizzando hello Apache2 Ubuntu predefinito pagina passando tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="aa430-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="aa430-148">Dovrebbe essere visualizzata una schermata simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="aa430-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="aa430-149">È stato configurato uno stack LAMP nella VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa430-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa430-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa430-150">Next steps</span></span>
<span data-ttu-id="aa430-151">Estrarre hello documentazione Ubuntu nello stack LAMP hello:</span><span class="sxs-lookup"><span data-stu-id="aa430-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="aa430-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="aa430-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png