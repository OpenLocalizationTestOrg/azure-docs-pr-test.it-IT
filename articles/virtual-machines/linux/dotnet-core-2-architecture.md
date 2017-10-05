---
title: Distribuzione di risorse di calcolo Linux con modelli di Azure Resource Manager | Documentazione Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c3f9f98079e0c89d1231f9c3e62e82c33ad18236
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="b9f28-103">Architettura delle applicazioni con i modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="b9f28-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="b9f28-104">Quando si sviluppa una distribuzione di Azure Resource Manager, i requisiti di calcolo devono essere mappati ai servizi e alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="b9f28-105">Se un'applicazione è costituita da diversi endpoint HTTP, da un database e da un servizio di caching dei dati, le risorse di Azure che ospitano ognuno di questi componenti devono essere razionalizzate.</span><span class="sxs-lookup"><span data-stu-id="b9f28-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="b9f28-106">Nel caso specifico, l'applicazione Music Store di esempio include un'applicazione Web, ospitata in una macchina virtuale, e un database SQL, ospitato in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="b9f28-107">Questo documento descrive in che modo sono configurate le risorse di calcolo dell'applicazione Music Store nel modello di esempio di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9f28-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="b9f28-108">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="b9f28-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="b9f28-109">Per ottenere risultati ottimali, pre-distribuire un'istanza della soluzione alla propria sottoscrizione di Azure ed esercitarsi con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9f28-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="b9f28-110">Il modello completo è disponibile in [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)(Distribuzione di Music Store in Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="b9f28-110">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="b9f28-111">Macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b9f28-111">Virtual Machine</span></span>
<span data-ttu-id="b9f28-112">L'applicazione Music Store include un'applicazione Web in cui i clienti possono cercare e acquistare musica.</span><span class="sxs-lookup"><span data-stu-id="b9f28-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="b9f28-113">Esistono vari servizi di Azure che possono ospitare applicazioni Web. In questo esempio viene usata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="b9f28-114">Con il modello Music Store di esempio, viene distribuita una macchina virtuale, viene installato un server Web e viene installato e configurato il sito Web di Music Store.</span><span class="sxs-lookup"><span data-stu-id="b9f28-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="b9f28-115">Ai fini di questo articolo, viene illustrata solo la distribuzione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="b9f28-116">La configurazione del server Web e dell'applicazione è descritta in un articolo successivo.</span><span class="sxs-lookup"><span data-stu-id="b9f28-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="b9f28-117">È possibile aggiungere una macchina virtuale a un modello usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9f28-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="b9f28-118">Quando si distribuisce una macchina virtuale, sono necessarie anche alcune risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b9f28-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="b9f28-119">Se per creare il modello si usa Visual Studio, queste risorse vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9f28-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="b9f28-120">Se invece si crea il modello manualmente, queste risorse devono essere inserite e configurate.</span><span class="sxs-lookup"><span data-stu-id="b9f28-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="b9f28-121">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Esempio JSON di macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="b9f28-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

<span data-ttu-id="b9f28-122">Dopo la distribuzione, le proprietà della macchina virtuale possono essere visualizzate nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Macchina virtuale](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="b9f28-124">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b9f28-124">Storage Account</span></span>
<span data-ttu-id="b9f28-125">Gli account di archiviazione presentano molte funzionalità e opzioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b9f28-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="b9f28-126">Per il contesto delle macchine virtuali di Azure, un account di archiviazione contiene le unità disco rigido virtuali della macchina virtuale e altri dischi dati.</span><span class="sxs-lookup"><span data-stu-id="b9f28-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="b9f28-127">L'esempio Music Store include un solo account di archiviazione per contenere l'unità disco rigido virtuale di ogni macchina virtuale nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9f28-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="b9f28-128">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Account di archiviazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="b9f28-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="b9f28-129">Un account di archiviazione è associato a una macchina virtuale all'interno della dichiarazione del modello di Resource Manager per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="b9f28-130">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Associazione della macchina virtuale con l'account di archiviazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="b9f28-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="b9f28-131">Dopo la distribuzione, l'account di archiviazione può essere visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Account di archiviazione](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="b9f28-133">Facendo clic sul contenitore BLOB dell'account di archiviazione, è possibile visualizzare il file dell'unità disco rigido virtuale per ogni macchina virtuale distribuita con il modello.</span><span class="sxs-lookup"><span data-stu-id="b9f28-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Unità disco rigido virtuali](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="b9f28-135">Per altre informazioni su Archiviazione di Azure, vedere [Documentazione su Archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="b9f28-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="b9f28-136">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="b9f28-136">Virtual Network</span></span>
<span data-ttu-id="b9f28-137">Se una macchina virtuale richiede una connessione di rete interna, ad esempio per avere la possibilità di comunicare con altre macchine virtuali e risorse di Azure, è necessario configurare una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="b9f28-138">Una rete virtuale non rende accessibile la macchina virtuale attraverso Internet.</span><span class="sxs-lookup"><span data-stu-id="b9f28-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="b9f28-139">La connettività pubblica richiede un indirizzo IP pubblico, come descritto più avanti in questa serie.</span><span class="sxs-lookup"><span data-stu-id="b9f28-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="b9f28-140">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Rete virtuale e subnet](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="b9f28-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="b9f28-141">Nel portale di Azure la rete virtuale ha un aspetto simile all'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="b9f28-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="b9f28-142">Si noti che tutte le macchine virtuali distribuite con il modello sono collegate alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Rete virtuale](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="b9f28-144">Interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b9f28-144">Network Interface</span></span>
 <span data-ttu-id="b9f28-145">Un'interfaccia di rete connette una macchina virtuale a una rete virtuale, in particolare a una subnet definita nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="b9f28-146">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Interfaccia di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="b9f28-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="b9f28-147">Ogni risorsa di macchina virtuale include un profilo di rete,</span><span class="sxs-lookup"><span data-stu-id="b9f28-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="b9f28-148">in cui l'interfaccia di rete è associata alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b9f28-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="b9f28-149">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Profilo di rete della macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="b9f28-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="b9f28-150">Nel portale di Azure l'interfaccia di rete ha un aspetto simile all'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="b9f28-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="b9f28-151">L'associazione dell'indirizzo IP interno con la macchina virtuale è visibile nella risorsa dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b9f28-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Interfaccia di rete](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="b9f28-153">Per altre informazioni sulle reti virtuali di Azure, vedere [Documentazione su Rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="b9f28-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="b9f28-154">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b9f28-154">Azure SQL Database</span></span>
<span data-ttu-id="b9f28-155">Oltre a una macchina virtuale che ospita il sito Web di Music Store, viene distribuito un database SQL di Azure per ospitare il database di Music Store.</span><span class="sxs-lookup"><span data-stu-id="b9f28-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="b9f28-156">L'uso di un database SQL di Azure è vantaggioso perché consente di evitare di usare un secondo set di macchine virtuali, integrando scalabilità e disponibilità nel servizio.</span><span class="sxs-lookup"><span data-stu-id="b9f28-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="b9f28-157">È possibile aggiungere un database SQL di Azure a un modello usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="b9f28-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="b9f28-158">La risorsa di SQL Server include un nome utente e una password a cui sono concessi diritti amministrativi sull'istanza di SQL.</span><span class="sxs-lookup"><span data-stu-id="b9f28-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="b9f28-159">Viene inoltre aggiunta una risorsa di firewall SQL.</span><span class="sxs-lookup"><span data-stu-id="b9f28-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="b9f28-160">Per impostazione predefinita, le applicazioni ospitate in Azure sono in grado di connettersi all'istanza di SQL.</span><span class="sxs-lookup"><span data-stu-id="b9f28-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="b9f28-161">Per consentire a un'applicazione esterna come SQL Server Management Studio di connettersi all'istanza di SQL, il firewall deve essere configurato.</span><span class="sxs-lookup"><span data-stu-id="b9f28-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="b9f28-162">Ai fini della demo di Music Store, è sufficiente accettare la configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b9f28-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="b9f28-163">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Database SQL di Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="b9f28-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="b9f28-164">Di seguito è illustrato il database MusicStore di SQL Server come visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9f28-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="b9f28-166">Per altre informazioni sulla distribuzione del database SQL di Azure, vedere [Documentazione su Database SQL](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="b9f28-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="b9f28-167">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b9f28-167">Next step</span></span>
<hr>

[<span data-ttu-id="b9f28-168">Passaggio 2: Accesso e sicurezza nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b9f28-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

