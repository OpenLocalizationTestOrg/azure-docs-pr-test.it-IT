---
title: Distribuire LAMP in una macchina virtuale Linux in Azure | Microsoft Docs
description: Informazioni su come installare lo stack LAMP in una macchina virtuale Linux in Azure
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
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="a9605-103">Distribuire lo stack LAMP in Azure</span><span class="sxs-lookup"><span data-stu-id="a9605-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="a9605-104">Questo articolo illustra come distribuire un server Web Apache, MySQL e PHP (lo stack LAMP) in Azure.</span><span class="sxs-lookup"><span data-stu-id="a9605-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="a9605-105">Sono necessari un account Azure ([richiedere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a9605-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="a9605-106">È possibile eseguire questi passaggi anche tramite l'[interfaccia della riga di comando di Azure 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9605-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="a9605-107">Breve riepilogo dei comandi</span><span class="sxs-lookup"><span data-stu-id="a9605-107">Quick command summary</span></span>

1. <span data-ttu-id="a9605-108">Salvare e modificare il [file azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) nel punto desiderato sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="a9605-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="a9605-109">Eseguire i due comandi seguenti per creare un gruppo di risorse e quindi distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="a9605-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="a9605-110">Distribuire LAMP in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="a9605-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="a9605-111">I comandi seguenti aggiornano i pacchetti e poi installano Apache, MySQL e PHP:</span><span class="sxs-lookup"><span data-stu-id="a9605-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="a9605-112">Procedura dettagliata per distribuire LAMP in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a9605-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="a9605-113">Creare un gruppo di risorse con [az group create](/cli/azure/group#create) per contenere la nuova macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="a9605-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="a9605-114">Per creare la VM, è possibile usare un modello di Azure Resource Manager già pronto disponibile [qui in GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="a9605-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="a9605-115">Salvare il [file azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a9605-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="a9605-116">Modificare il file **azuredeploy.parameters.json** secondo le proprie preferenze di input.</span><span class="sxs-lookup"><span data-stu-id="a9605-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="a9605-117">Distribuire il modello con [az group deployment create] che fa riferimento al file json scaricato:</span><span class="sxs-lookup"><span data-stu-id="a9605-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="a9605-118">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a9605-118">The output is similar to the following example:</span></span>

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

<span data-ttu-id="a9605-119">È stata creata una VM Linux con LAMP già installato.</span><span class="sxs-lookup"><span data-stu-id="a9605-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="a9605-120">Se si desidera verificare l'installazione, si può passare direttamente a [Verificare l'installazione di LAMP](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="a9605-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="a9605-121">Procedura dettagliata per distribuire LAMP in una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="a9605-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="a9605-122">Per assistenza nella creazione di una macchina virtuale Linux, [qui sono disponibili informazioni su come creare una macchina virtuale Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="a9605-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="a9605-123">È quindi necessario connettersi tramite SSH alla macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="a9605-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="a9605-124">Per assistenza nella creazione di una chiave SSH, [qui sono disponibili informazioni su come creare una chiave SSH in Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9605-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="a9605-125">Se si dispone già di una chiave SSH, continuare connettendosi tramite SSH dalla riga di comando alla macchina virtuale Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a9605-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="a9605-126">Ora che la macchina virtuale Linux è disponibile, viene illustrata l'installazione dello stack LAMP nelle distribuzioni basate su Debian.</span><span class="sxs-lookup"><span data-stu-id="a9605-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="a9605-127">I comandi possono essere leggermente diversi per le altre distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="a9605-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="a9605-128">Installazione in Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a9605-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="a9605-129">È necessario che siano installati i pacchetti seguenti: `apache2`, `mysql-server`, `php5` e `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="a9605-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="a9605-130">È possibile installare questi pacchetti catturandoli direttamente o usando Tasksel.</span><span class="sxs-lookup"><span data-stu-id="a9605-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="a9605-131">Prima dell'installazione, è necessario scaricare e aggiornare gli elenchi di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a9605-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="a9605-132">Pacchetti singoli</span><span class="sxs-lookup"><span data-stu-id="a9605-132">Individual packages</span></span>
<span data-ttu-id="a9605-133">Uso di apt-get:</span><span class="sxs-lookup"><span data-stu-id="a9605-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="a9605-134">Uso di Tasksel</span><span class="sxs-lookup"><span data-stu-id="a9605-134">Using tasksel</span></span>
<span data-ttu-id="a9605-135">In alternativa è possibile scaricare Tasksel, uno strumento Debian/Ubuntu che installa più pacchetti correlati come "attività" coordinata nel sistema.</span><span class="sxs-lookup"><span data-stu-id="a9605-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="a9605-136">Dopo l'esecuzione di una delle due opzioni precedenti, verrà richiesto di installare questi pacchetti e altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a9605-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="a9605-137">Per impostare una password amministrativa per MySQL, premere 'y' e poi 'INVIO' per continuare e seguire eventuali altri prompt.</span><span class="sxs-lookup"><span data-stu-id="a9605-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="a9605-138">In questo modo vengono installate le estensioni PHP minime richieste per l'uso di PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9605-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="a9605-139">Eseguire il comando seguente per visualizzare altre estensioni PHP disponibili come pacchetti:</span><span class="sxs-lookup"><span data-stu-id="a9605-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="a9605-140">Creare un documento info.php</span><span class="sxs-lookup"><span data-stu-id="a9605-140">Create info.php document</span></span>
<span data-ttu-id="a9605-141">Ora sarà possibile controllare la versione di Apache, MySQL e PHP disponibile digitando `apache2 -v`, `mysql -v` o `php -v` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a9605-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="a9605-142">Per eseguire altri test, è possibile creare rapidamente una pagina di informazioni PHP da visualizzare in un browser.</span><span class="sxs-lookup"><span data-stu-id="a9605-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="a9605-143">Creare un file con l'editor di testo Nano con questo comando:</span><span class="sxs-lookup"><span data-stu-id="a9605-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="a9605-144">Nell'editor di testo GNU Nano aggiungere le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9605-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="a9605-145">Quindi salvare e chiudere l'editor di testo.</span><span class="sxs-lookup"><span data-stu-id="a9605-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="a9605-146">Riavviare Apache con questo comando, in modo che tutte le nuove installazioni vengano applicate.</span><span class="sxs-lookup"><span data-stu-id="a9605-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="a9605-147">Verificare l'installazione di LAMP</span><span class="sxs-lookup"><span data-stu-id="a9605-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="a9605-148">A questo punto è possibile aprire un browser e accedere a http://youruniqueDNS/info.php per controllare la pagina di informazioni PHP creata.</span><span class="sxs-lookup"><span data-stu-id="a9605-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="a9605-149">Dovrebbe avere un aspetto simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="a9605-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="a9605-150">È possibile controllare l'installazione di Apache visualizzando la pagina predefinita di Apache2 Ubuntu andando su http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="a9605-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="a9605-151">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a9605-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="a9605-152">È stato configurato uno stack LAMP nella VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9605-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9605-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9605-153">Next steps</span></span>
<span data-ttu-id="a9605-154">Vedere la documentazione di Ubuntu sullo stack LAMP:</span><span class="sxs-lookup"><span data-stu-id="a9605-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="a9605-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="a9605-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
