---
title: Distribuzione dell'applicazione con estensioni di macchine virtuali aaaAutomating | Documenti Microsoft
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
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="0298a-103">Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="0298a-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="0298a-104">Una volta tutti i requisiti infrastrutturali Azure sono stati identificati e convertiti in un modello di distribuzione, distribuzione di applicazione reale hello deve toobe risolti.</span><span class="sxs-lookup"><span data-stu-id="0298a-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="0298a-105">Distribuzione dell'applicazione qui fa riferimento a file binari dell'applicazione effettivo hello tooinstalling su risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0298a-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="0298a-106">Per esempio negozio hello, .net Core e NGINX Supervisore necessario toobe installato e configurato in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0298a-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="0298a-107">Hello negozio file binari necessari toobe installato nella macchina virtuale hello e database dell'archivio di musica hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0298a-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="0298a-108">Questo documento illustra in dettaglio come estensioni di macchine virtuali consente di automatizzare la distribuzione e configurazione tooAzure macchine virtuali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0298a-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="0298a-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="0298a-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="0298a-110">Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="0298a-111">è disponibili qui: modello completa Hello [distribuzione archivio musica in Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="0298a-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="0298a-112">Script di configurazione</span><span class="sxs-lookup"><span data-stu-id="0298a-112">Configuration script</span></span>
<span data-ttu-id="0298a-113">Estensioni di macchine virtuali sono programmi specializzati eseguite sui automazione configurazione tooprovide di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0298a-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="0298a-114">Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker.</span><span class="sxs-lookup"><span data-stu-id="0298a-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="0298a-115">Un'estensione script personalizzato può essere utilizzato toorun qualsiasi a fronte di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0298a-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="0298a-116">Con l'esempio hello Negozio, è backup di macchine virtuali toohello script personalizzato estensione tooconfigure hello Ubuntu e installare un'applicazione hello Negozio.</span><span class="sxs-lookup"><span data-stu-id="0298a-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="0298a-117">Prima che riporta in dettaglio come estensioni di macchine virtuali vengono dichiarate in un modello di gestione risorse di Azure, esaminare script hello che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="0298a-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="0298a-118">Questo script configura hello toohost di macchina virtuale Ubuntu hello applicazione Negozio.</span><span class="sxs-lookup"><span data-stu-id="0298a-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="0298a-119">Durante l'esecuzione, script hello installa il software necessario tutte, installare un'applicazione hello musica archivio dal controllo del codice sorgente e preparare i database di hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="0298a-120">applicazione di base toolearn più sull'hosting di .net su Linux, vedere [ambiente di produzione Linux tooa pubblica](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="0298a-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="0298a-121">Questo esempio è fornito a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="0298a-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="0298a-122">Estensione script della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0298a-122">VM Script Extension</span></span>
<span data-ttu-id="0298a-123">Le estensioni VM possibile eseguire in una macchina virtuale in fase di compilazione con l'inclusione di risorse di estensione hello nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="0298a-124">Hello estensione può essere aggiunta con hello Visual Studio Aggiunta guidata risorsa o tramite l'inserimento di un oggetto JSON valido nel modello hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="0298a-125">risorse di estensione dello Script Hello è annidata all'interno di hello risorsa macchina virtuale. può essere visto nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="0298a-126">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [estensione della macchina virtuale Script](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="0298a-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="0298a-127">Si noti che in hello seguito JSON che hello script viene archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0298a-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="0298a-128">Questo script può essere incluso anche nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0298a-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="0298a-129">Inoltre, i modelli di gestione risorse di Azure consentono hello script esecuzione stringa tooconstructed in modo che i valori di parametri di modello possono essere usati come parametri per l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="0298a-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="0298a-130">In questo caso i dati vengono forniti durante la distribuzione di modelli di hello e questi valori possono quindi essere utilizzati durante l'esecuzione di script hello.</span><span class="sxs-lookup"><span data-stu-id="0298a-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="0298a-131">Per ulteriori informazioni sull'uso delle estensioni hello script personalizzato, vedere [le estensioni degli script personalizzati con modelli di gestione risorse](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0298a-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="0298a-132">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="0298a-132">Next Step</span></span>
<hr>

[<span data-ttu-id="0298a-133">Explore More Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="0298a-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

