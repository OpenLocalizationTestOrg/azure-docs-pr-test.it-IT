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
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="ee0f9-103">Distribuire lo stack LAMP in Azure</span><span class="sxs-lookup"><span data-stu-id="ee0f9-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="ee0f9-104">In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="ee0f9-105">È necessario un account di Azure ([ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="ee0f9-106">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="ee0f9-107">Breve riepilogo dei comandi</span><span class="sxs-lookup"><span data-stu-id="ee0f9-107">Quick command summary</span></span>

1. <span data-ttu-id="ee0f9-108">Salva e modifica hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) preferenza tooyour sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="ee0f9-109">Eseguire i seguenti due comandi toocreate hello un gruppo di risorse e quindi distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="ee0f9-110">Distribuire LAMP in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="ee0f9-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="ee0f9-111">esempio Hello comandi pacchetti di aggiornamenti, quindi installa Apache, MySQL e PHP:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="ee0f9-112">Procedura dettagliata per distribuire LAMP in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ee0f9-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="ee0f9-113">Creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create) toocontain hello nuova macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="ee0f9-114">toocreate hello macchina virtuale stessa, è possibile utilizzare un modello di gestione risorse di Azure già scritto trovato [qui su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="ee0f9-115">Salvare hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour di computer locale.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="ee0f9-116">Modifica hello **azuredeploy.parameters.json** tooyour file preferito di input.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="ee0f9-117">Distribuire il modello di hello con [distribuzione gruppo az crea] riferimento hello scaricato i file json:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="ee0f9-118">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-118">hello output is similar toohello following example:</span></span>

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

<span data-ttu-id="ee0f9-119">È stata creata una VM Linux con LAMP già installato.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="ee0f9-120">Se si desidera, è possibile verificare l'installazione hello passando troppo basso[verificare LAMP installato](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="ee0f9-121">Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="ee0f9-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="ee0f9-122">Se è necessario informazioni sulla creazione di una VM Linux, è possibile head [toolearn qui come toocreate una VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="ee0f9-123">Successivamente, è necessario tooSSH in hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="ee0f9-124">Per assistenza con la creazione di una chiave SSH, è possibile head [toolearn qui come una chiave SSH in Linux o Mac toocreate](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee0f9-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="ee0f9-125">Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ee0f9-126">Ora che si lavora all'interno di VM Linux, è possibile scorrere l'installazione di stack LAMP hello in distribuzioni basate su Debian.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="ee0f9-127">per altre distribuzioni Linux, potrebbero essere diversi comandi Hello.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="ee0f9-128">Installazione in Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ee0f9-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="ee0f9-129">È necessario hello seguenti pacchetti installati: `apache2`, `mysql-server`, `php5`, e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="ee0f9-130">È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="ee0f9-131">Prima di installare è necessario toodownload e aggiornare gli elenchi di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="ee0f9-132">Pacchetti singoli</span><span class="sxs-lookup"><span data-stu-id="ee0f9-132">Individual packages</span></span>
<span data-ttu-id="ee0f9-133">Uso di apt-get:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="ee0f9-134">Uso di Tasksel</span><span class="sxs-lookup"><span data-stu-id="ee0f9-134">Using tasksel</span></span>
<span data-ttu-id="ee0f9-135">In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="ee0f9-136">Dopo aver eseguito una delle opzioni precedenti hello, sarà possibile tooinstall richiesta questi pacchetti e varie altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="ee0f9-137">tooset una password amministrativa per MySQL, premere 'y' e 'Invio' toocontinue e seguire eventuali altre istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="ee0f9-138">Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="ee0f9-139">Eseguire hello successivo comando toosee altre estensioni di PHP che sono disponibili come pacchetti:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="ee0f9-140">Creare un documento info.php</span><span class="sxs-lookup"><span data-stu-id="ee0f9-140">Create info.php document</span></span>
<span data-ttu-id="ee0f9-141">Dovrebbe ora essere in grado di toocheck la versione di PHP, MySQL e Apache uso tramite riga di comando hello digitando `apache2 -v`, `mysql -v`, o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="ee0f9-142">Se potrebbe ad esempio tootest, inoltre, è possibile creare un rapido tooview pagina informazioni PHP in un browser.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="ee0f9-143">Creare un file con l'editor di testo Nano con questo comando:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="ee0f9-144">Nell'editor di testo hello GNU Nano aggiungere hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="ee0f9-145">Successivamente, salvare e chiudere l'editor di testo hello.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="ee0f9-146">Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="ee0f9-147">Verificare l'installazione di LAMP</span><span class="sxs-lookup"><span data-stu-id="ee0f9-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="ee0f9-148">Ora è possibile controllare pagina delle info PHP hello che aprendo un browser e passare toohttp://youruniqueDNS/info.php creato.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="ee0f9-149">Dovrebbe essere simile toothis immagine.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="ee0f9-150">È possibile controllare l'installazione di Apache visualizzando hello Apache2 Ubuntu predefinito pagina passando tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="ee0f9-151">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="ee0f9-152">È stato configurato uno stack LAMP nella VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0f9-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee0f9-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee0f9-153">Next steps</span></span>
<span data-ttu-id="ee0f9-154">Estrarre hello documentazione Ubuntu nello stack LAMP hello:</span><span class="sxs-lookup"><span data-stu-id="ee0f9-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="ee0f9-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="ee0f9-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
