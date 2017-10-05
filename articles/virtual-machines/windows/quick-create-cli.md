---
title: Avvio rapido in Azure - Creare l'interfaccia della riga di comando della VM Windows | Microsoft Docs
description: Informazioni veloci su come creare una macchina virtuale Windows con l'interfaccia della riga di comando di Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="acd05-103">Creare una macchina virtuale Windows con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="acd05-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="acd05-104">L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="acd05-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="acd05-105">Questa guida descrive dettagliatamente come usare l'interfaccia della riga di comando di Azure per distribuire una macchina virtuale che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="acd05-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="acd05-106">Al termine della distribuzione, viene eseguita la connessione al server e viene installato IIS.</span><span class="sxs-lookup"><span data-stu-id="acd05-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="acd05-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="acd05-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="acd05-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="acd05-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="acd05-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="acd05-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="acd05-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="acd05-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="acd05-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="acd05-111">Create a resource group</span></span>

<span data-ttu-id="acd05-112">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="acd05-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="acd05-113">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="acd05-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="acd05-114">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="acd05-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="acd05-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="acd05-115">Create virtual machine</span></span>

<span data-ttu-id="acd05-116">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="acd05-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="acd05-117">L'esempio seguente crea una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="acd05-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="acd05-118">Questo esempio usa *azureuser* come nome utente amministrativo e *myPassword12* come password.</span><span class="sxs-lookup"><span data-stu-id="acd05-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="acd05-119">Aggiornare i valori in modo che siano appropriati all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="acd05-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="acd05-120">Questi valori sono necessari quando si crea una connessione con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="acd05-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="acd05-121">Dopo che la VM è stata creata, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="acd05-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="acd05-122">Prendere nota di `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="acd05-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="acd05-123">Questo indirizzo viene usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="acd05-123">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="acd05-124">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="acd05-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="acd05-125">Per impostazione predefinita nelle macchine virtuali Windows distribuite in Azure sono consentite solo le connessioni RDP.</span><span class="sxs-lookup"><span data-stu-id="acd05-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="acd05-126">Se si intende usare questa macchina virtuale come un server Web, è necessario aprire la porta 80 da Internet.</span><span class="sxs-lookup"><span data-stu-id="acd05-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="acd05-127">Usare il comando [az vm open-port](/cli/azure/vm#open-port) per aprire la porta.</span><span class="sxs-lookup"><span data-stu-id="acd05-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="acd05-128">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="acd05-128">Connect to virtual machine</span></span>

<span data-ttu-id="acd05-129">Usare il comando seguente per creare una sessione desktop remoto con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="acd05-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="acd05-130">Sostituire l'indirizzo IP con l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="acd05-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="acd05-131">Quando richiesto, immettere le credenziali utilizzate durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="acd05-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="acd05-132">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="acd05-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="acd05-133">Dopo avere eseguito l'accesso alla macchina virtuale di Azure, è possibile usare una singola riga di codice di PowerShell per installare IIS e abilitare la regola del firewall locale per consentire il traffico Web.</span><span class="sxs-lookup"><span data-stu-id="acd05-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="acd05-134">Aprire un prompt di PowerShell ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="acd05-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="acd05-135">Visualizzare la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="acd05-135">View the IIS welcome page</span></span>

<span data-ttu-id="acd05-136">Dopo l'installazione di IIS e l'apertura della porta 80 nella macchina virtuale da Internet, è possibile usare il Web browser preferito per visualizzare la pagina iniziale predefinita di IIS.</span><span class="sxs-lookup"><span data-stu-id="acd05-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="acd05-137">Assicurarsi di usare l'indirizzo IP pubblico descritto in precedenza per passare alla pagina predefinita.</span><span class="sxs-lookup"><span data-stu-id="acd05-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="acd05-139">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="acd05-139">Clean up resources</span></span>

<span data-ttu-id="acd05-140">Quando non servono più, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="acd05-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="acd05-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acd05-141">Next steps</span></span>

<span data-ttu-id="acd05-142">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="acd05-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="acd05-143">Per altre informazioni sulle macchine virtuali di Azure, passare all'esercitazione per le VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="acd05-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="acd05-144">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="acd05-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
