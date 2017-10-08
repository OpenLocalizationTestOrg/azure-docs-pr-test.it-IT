---
title: aaaDeploying risorse di calcolo di Linux con modelli di gestione risorse di Azure | Documenti Microsoft
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
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="fcfcb-103">Architettura delle applicazioni con i modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="fcfcb-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="fcfcb-104">Quando si sviluppa una distribuzione di gestione risorse di Azure, i requisiti di calcolo necessario toobe mappato tooAzure risorse e servizi.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="fcfcb-105">Se un'applicazione è costituita da diversi endpoint http, un database e un servizio di memorizzazione di dati, hello risorse di Azure che ospitano ognuno di questi componenti deve toobe ragionato.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="fcfcb-106">Ad esempio, un'applicazione hello esempio negozio include un'applicazione web ospitata in una macchina virtuale e un database SQL, che è ospitato in database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="fcfcb-107">Questo documento vengono indicati come risorse di calcolo negozio hello configurate nel modello di gestione risorse di Azure di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="fcfcb-108">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="fcfcb-109">Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="fcfcb-110">è disponibili qui: modello completa Hello [distribuzione archivio musica in Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="fcfcb-111">Macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fcfcb-111">Virtual Machine</span></span>
<span data-ttu-id="fcfcb-112">applicazione di archiviazione di file musicali Hello include un'applicazione web in cui i clienti possono esplorare e acquistare musica.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="fcfcb-113">Esistono vari servizi di Azure che possono ospitare applicazioni Web. In questo esempio viene usata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="fcfcb-114">Utilizza modello negozio di esempio hello, viene distribuita una macchina virtuale, installare un server web e sito Web di archivio musica hello installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="fcfcb-115">Per i migliori risultati hello di questo articolo, distribuzione della macchina virtuale solo hello è descritta in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="fcfcb-116">configurazione di Hello del server web hello e dell'applicazione hello è descritta in dettaglio in un articolo più avanti.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="fcfcb-117">Una macchina virtuale può essere aggiunti tooa modello utilizzando Visual Studio Aggiungi nuova risorsa o procedura guidata, inserendo JSON valido nel modello di distribuzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="fcfcb-118">Quando si distribuisce una macchina virtuale, sono necessarie anche alcune risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="fcfcb-119">Se usi Visual Studio toocreate hello modello, queste risorse vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="fcfcb-120">Se si crea manualmente il modello di hello, queste risorse devono toobe inserito e configurato.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="fcfcb-121">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [JSON di macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

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

<span data-ttu-id="fcfcb-122">Una volta distribuito, le proprietà della macchina virtuale hello possono essere visualizzate nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Macchina virtuale](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="fcfcb-124">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="fcfcb-124">Storage Account</span></span>
<span data-ttu-id="fcfcb-125">Gli account di archiviazione presentano molte funzionalità e opzioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="fcfcb-126">Per il contesto di hello delle macchine virtuali di Azure, un account di archiviazione contiene hello dischi rigidi virtuali della macchina virtuale hello e per eventuali dischi dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="fcfcb-127">esempio di negozio Hello include uno storage account toohold hello unità disco rigido virtuale di ogni macchina virtuale nella distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="fcfcb-128">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Account di archiviazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

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

<span data-ttu-id="fcfcb-129">Un account di archiviazione è associato a una macchina virtuale all'interno della dichiarazione di modello di gestione risorse di hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="fcfcb-130">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [macchina virtuale e Account di archiviazione associazione](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

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

<span data-ttu-id="fcfcb-131">Dopo la distribuzione, l'account di archiviazione hello possono essere visualizzati nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Account di archiviazione](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="fcfcb-133">Facendo clic in un contenitore blob account di archiviazione hello, possono essere visualizzati i file di disco rigido virtuale hello per ogni macchina virtuale distribuita con il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Unità disco rigido virtuali](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="fcfcb-135">Per altre informazioni su Archiviazione di Azure, vedere [Documentazione su Archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="fcfcb-136">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fcfcb-136">Virtual Network</span></span>
<span data-ttu-id="fcfcb-137">Se una macchina virtuale richiede una rete interna, ad esempio hello possibilità toocommunicate con altre macchine virtuali e le risorse di Azure, è necessario una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="fcfcb-138">Una rete virtuale non rendere hello macchina virtuale accessibili tramite internet hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="fcfcb-139">La connettività pubblica richiede un indirizzo IP pubblico, come descritto più avanti in questa serie.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="fcfcb-140">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [rete virtuale e le subnet](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

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

<span data-ttu-id="fcfcb-141">Dal portale di Azure hello, rete virtuale hello è simile a hello seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="fcfcb-142">Si noti che tutte le macchine virtuali distribuite con il modello di hello toohello collegati di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Rete virtuale](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="fcfcb-144">Interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="fcfcb-144">Network Interface</span></span>
 <span data-ttu-id="fcfcb-145">Un'interfaccia di rete si connette a una rete virtuale della macchina virtuale tooa, in particolare subnet tooa che è stata definita nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="fcfcb-146">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [interfaccia di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

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

<span data-ttu-id="fcfcb-147">Ogni risorsa di macchina virtuale include un profilo di rete,</span><span class="sxs-lookup"><span data-stu-id="fcfcb-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="fcfcb-148">interfaccia di rete Hello è associata a una macchina virtuale hello in questo profilo.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="fcfcb-149">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [il profilo di rete di macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="fcfcb-150">Dal portale di Azure hello, l'interfaccia di rete hello è simile a hello seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="fcfcb-151">indirizzo IP interno Hello e associazione di hello macchina virtuale possono essere visualizzati sulla risorsa di interfaccia di rete hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interfaccia di rete](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="fcfcb-153">Per altre informazioni sulle reti virtuali di Azure, vedere [Documentazione su Rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="fcfcb-154">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="fcfcb-154">Azure SQL Database</span></span>
<span data-ttu-id="fcfcb-155">Macchina virtuale tooa hosting del sito Web di hello Negozio, un Database di SQL Azure è inoltre database dell'archivio di musica hello toohost distribuito.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="fcfcb-156">Hello vantaggio offerto dall'utilizzo del Database SQL di Azure qui è un secondo set di macchine virtuali che non sia obbligatorio, scalabilità e disponibilità è incorporata nel servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="fcfcb-157">È possibile aggiungere un database SQL di Azure utilizzando Visual Studio Aggiungi nuova risorsa o procedura guidata, inserendo un JSON valido in un modello di hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="fcfcb-158">Hello risorsa di SQL Server include un nome utente e una password che vengono concessi i diritti amministrativi sull'istanza di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="fcfcb-159">Viene inoltre aggiunta una risorsa di firewall SQL.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="fcfcb-160">Per impostazione predefinita, le applicazioni ospitate in Azure sono in grado di tooconnect con l'istanza SQL hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="fcfcb-161">applicazione esterna tooallow tali una SQL Server Management studio tooconnect toohello istanza SQL, firewall hello deve toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="fcfcb-162">Per i migliori risultati hello della demo negozio hello, la configurazione predefinita di hello è corretta.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="fcfcb-163">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [database SQL di Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

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

<span data-ttu-id="fcfcb-164">Visualizzazione di hello SQL server e database MusicStore come illustrato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fcfcb-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="fcfcb-166">Per altre informazioni sulla distribuzione del database SQL di Azure, vedere [Documentazione su Database SQL](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="fcfcb-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="fcfcb-167">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="fcfcb-167">Next step</span></span>
<hr>

[<span data-ttu-id="fcfcb-168">Passaggio 2: Accesso e sicurezza nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fcfcb-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

