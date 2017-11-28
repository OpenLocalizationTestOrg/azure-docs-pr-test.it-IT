---
title: Avvio rapido - aaaAzure creare VM CLI | Documenti Microsoft
description: Consente di capire velocemente toocreate le macchine virtuali con hello CLI di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="0883b-103">Creare una macchina virtuale Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="0883b-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="0883b-104">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="0883b-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="0883b-105">Questa guida descrive l'utilizzo di una macchina virtuale in esecuzione il server Ubuntu hello Azure CLI toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0883b-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="0883b-106">Dopo aver distribuito il server di hello, viene creata una connessione SSH e viene installato un server Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="0883b-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="0883b-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="0883b-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0883b-108">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="0883b-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0883b-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0883b-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0883b-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0883b-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="0883b-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0883b-111">Create a resource group</span></span>

<span data-ttu-id="0883b-112">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0883b-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="0883b-113">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="0883b-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="0883b-114">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="0883b-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="0883b-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0883b-115">Create virtual machine</span></span>

<span data-ttu-id="0883b-116">Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0883b-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="0883b-117">esempio Hello crea una macchina virtuale denominata *myVM* e crea le chiavi SSH se sono già presenti in un percorso chiave predefinito.</span><span class="sxs-lookup"><span data-stu-id="0883b-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="0883b-118">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="0883b-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="0883b-119">Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="0883b-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="0883b-120">Prendere nota di hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="0883b-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="0883b-121">Questo indirizzo è utilizzato tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0883b-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="0883b-122">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="0883b-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="0883b-123">Per impostazione predefinita nelle macchine virtuali Linux distribuite in Azure sono consentite solo le connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="0883b-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="0883b-124">Se questa macchina virtuale verrà toobe un server Web, è necessario tooopen la porta 80 da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="0883b-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="0883b-125">Hello utilizzare [az vm aprire porte](/cli/azure/vm#open-port) comando tooopen hello desiderato porta.</span><span class="sxs-lookup"><span data-stu-id="0883b-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="0883b-126">Usare SSH per connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0883b-126">SSH into your VM</span></span>

<span data-ttu-id="0883b-127">Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0883b-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="0883b-128">Verificare che tooreplace  *<publicIpAddress>*  con hello correggere l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0883b-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="0883b-129">Nell'esempio riportato sopra l'indirizzo IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="0883b-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="0883b-130">Installare NGINX</span><span class="sxs-lookup"><span data-stu-id="0883b-130">Install NGINX</span></span>

<span data-ttu-id="0883b-131">Seguente hello utilizzare origini dei pacchetti tooupdate script bash e installare il pacchetto NGINX più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="0883b-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="0883b-132">Pagina iniziale di visualizzazione hello NGINX</span><span class="sxs-lookup"><span data-stu-id="0883b-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="0883b-133">Con NGINX installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la scelta tooview hello NGINX pagina iniziale predefinita.</span><span class="sxs-lookup"><span data-stu-id="0883b-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="0883b-134">Essere certi hello toouse *publicIpAddress* descritto in precedenza pagina predefinita di toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="0883b-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Sito NGINX predefinito](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="0883b-136">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="0883b-136">Clean up resources</span></span>

<span data-ttu-id="0883b-137">Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="0883b-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="0883b-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0883b-138">Next steps</span></span>

<span data-ttu-id="0883b-139">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="0883b-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="0883b-140">toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="0883b-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="0883b-141">Esercitazioni per le macchine virtuali di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="0883b-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
