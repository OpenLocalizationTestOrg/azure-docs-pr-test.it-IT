---
title: Avvio rapido - aaaAzure creare CLI VM di Windows | Documenti Microsoft
description: Informazioni toocreate rapidamente una macchina virtuale di Windows con hello CLI di Azure.
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
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="fdbb4-103">Creare una macchina virtuale Windows con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="fdbb4-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="fdbb4-104">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="fdbb4-105">Questa guida descrive l'utilizzo di una macchina virtuale in esecuzione Windows Server 2016 hello Azure CLI toodeploy.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="fdbb4-106">Una volta completata la distribuzione, è connettersi toohello server e installare IIS.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="fdbb4-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fdbb4-108">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fdbb4-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fdbb4-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fdbb4-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="fdbb4-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="fdbb4-111">Create a resource group</span></span>

<span data-ttu-id="fdbb4-112">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fdbb4-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fdbb4-113">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fdbb4-114">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="fdbb4-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fdbb4-115">Create virtual machine</span></span>

<span data-ttu-id="fdbb4-116">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fdbb4-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="fdbb4-117">esempio Hello crea una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="fdbb4-118">Questo esempio viene utilizzato *azureuser* per un nome utente amministrativo e *myPassword12* come password hello.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="fdbb4-119">Aggiornare questi ambiente appropriato tooyour toosomething di valori.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="fdbb4-120">Questi valori sono necessari quando si crea una connessione con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="fdbb4-121">Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="fdbb4-122">Prendere nota di hello `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="fdbb4-123">Questo indirizzo è utilizzato tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-123">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="fdbb4-124">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="fdbb4-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="fdbb4-125">Per impostazione predefinita sono consentite solo le connessioni RDP in tooWindows le macchine virtuali distribuite in Azure.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="fdbb4-126">Se questa macchina virtuale verrà toobe un server Web, è necessario tooopen la porta 80 da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="fdbb4-127">Hello utilizzare [az vm aprire porte](/cli/azure/vm#open-port) comando tooopen hello desiderato porta.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="fdbb4-128">Connettere la macchina toovirtual</span><span class="sxs-lookup"><span data-stu-id="fdbb4-128">Connect toovirtual machine</span></span>

<span data-ttu-id="fdbb4-129">Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="fdbb4-130">Sostituire l'indirizzo IP hello con indirizzo IP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="fdbb4-131">Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="fdbb4-132">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdbb4-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="fdbb4-133">Ora che è stato effettuato in toohello macchina virtuale di Azure, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="fdbb4-134">Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fdbb4-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="fdbb4-135">Hello Visualizza la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="fdbb4-135">View hello IIS welcome page</span></span>

<span data-ttu-id="fdbb4-136">Con IIS installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la pagina iniziale tooview scelte hello predefinita IIS.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="fdbb4-137">Impossibile verificare toouse hello indirizzo IP pubblico che descritto in precedenza pagina predefinita di toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="fdbb4-139">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="fdbb4-139">Clean up resources</span></span>

<span data-ttu-id="fdbb4-140">Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="fdbb4-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdbb4-141">Next steps</span></span>

<span data-ttu-id="fdbb4-142">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="fdbb4-143">toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="fdbb4-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdbb4-144">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="fdbb4-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
