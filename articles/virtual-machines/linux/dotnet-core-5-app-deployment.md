---
title: Automazione della distribuzione di applicazioni con le estensioni delle macchine virtuali | Microsoft Docs
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="7d97d-103">Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="7d97d-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="7d97d-104">Dopo che tutti i requisiti dell'infrastruttura di Azure sono stati identificati e convertiti in un modello di distribuzione, è necessario occuparsi della distribuzione effettiva delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7d97d-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="7d97d-105">Per distribuzione delle applicazioni si intende l'installazione effettiva dei file binari delle applicazioni nelle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d97d-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="7d97d-106">Per l'esempio Music Store, è necessario installare e configurare .NET Core, NGINX e Supervisor in ogni macchina virtuale,</span><span class="sxs-lookup"><span data-stu-id="7d97d-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="7d97d-107">nonché installare i file binari di Music Store nella macchina virtuale e creare il database di Music Store.</span><span class="sxs-lookup"><span data-stu-id="7d97d-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="7d97d-108">Questo documento descrive in che modo le estensioni delle macchine virtuali possono automatizzare la distribuzione e la configurazione di applicazioni nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d97d-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="7d97d-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="7d97d-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="7d97d-110">Per ottenere risultati ottimali, pre-distribuire un'istanza della soluzione alla propria sottoscrizione di Azure ed esercitarsi con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d97d-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="7d97d-111">Il modello completo è disponibile in [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)(Distribuzione di Music Store in Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="7d97d-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="7d97d-112">Script di configurazione</span><span class="sxs-lookup"><span data-stu-id="7d97d-112">Configuration script</span></span>
<span data-ttu-id="7d97d-113">Le estensioni delle macchine virtuali sono programmi specializzati che vengono eseguiti sulle macchine virtuali per automatizzare le attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7d97d-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="7d97d-114">Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker.</span><span class="sxs-lookup"><span data-stu-id="7d97d-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="7d97d-115">Un'estensione script personalizzata può essere usata per eseguire uno script su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d97d-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="7d97d-116">Nel caso dell'esempio Music Store, l'estensione script personalizzata viene usata per configurare le macchine virtuali Ubuntu e installare l'applicazione Music Store.</span><span class="sxs-lookup"><span data-stu-id="7d97d-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="7d97d-117">Prima di vedere in che modo le estensioni delle macchine virtuali sono dichiarate in un modello di Azure Resource Manager, esaminare lo script che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="7d97d-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="7d97d-118">Questo script configura la macchina virtuale Ubuntu in modo da ospitare l'applicazione Music Store.</span><span class="sxs-lookup"><span data-stu-id="7d97d-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="7d97d-119">Durante l'esecuzione, lo script installa tutto il software necessario, installa l'applicazione Music Store dal controllo del codice sorgente e prepara il database.</span><span class="sxs-lookup"><span data-stu-id="7d97d-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="7d97d-120">Per altre informazioni sull'hosting di un'applicazione .NET Core su Linux, vedere [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html)(Pubblicare in un ambiente di produzione Linux).</span><span class="sxs-lookup"><span data-stu-id="7d97d-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="7d97d-121">Questo esempio è fornito a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="7d97d-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="7d97d-122">Estensione script della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7d97d-122">VM Script Extension</span></span>
<span data-ttu-id="7d97d-123">Le estensioni delle macchine virtuali possono essere eseguite su una macchina virtuale in fase di compilazione includendo la risorsa dell'estensione nel modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d97d-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="7d97d-124">È possibile aggiungere l'estensione usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="7d97d-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="7d97d-125">La risorsa dell'estensione script è annidata all'interno della risorsa della macchina virtuale, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7d97d-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="7d97d-126">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Estensione script della macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="7d97d-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="7d97d-127">Nel codice JSON seguente è possibile notare che lo script è archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d97d-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="7d97d-128">Questo script può essere incluso anche nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d97d-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="7d97d-129">Inoltre, i modelli di Azure Resource Manager consentono di creare la stringa di esecuzione dello script in modo che i valori dei parametri del modello siano utilizzabili come parametri per l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="7d97d-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="7d97d-130">In questo caso, i dati vengono forniti quando si distribuiscono i modelli e questi valori possono quindi essere usati durante l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="7d97d-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="7d97d-131">Per altre informazioni sull'estensione script personalizzata, vedere [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(Estensioni script personalizzate con i modelli di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="7d97d-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="7d97d-132">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="7d97d-132">Next Step</span></span>
<hr>

[<span data-ttu-id="7d97d-133">Explore More Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="7d97d-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

