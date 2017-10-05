---
title: Avvio rapido in Azure - Creare l'interfaccia della riga di comando per una VM | Microsoft Docs
description: Informazioni veloci su come creare macchine virtuali con l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="5ac35-103">Creare una macchina virtuale Linux con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5ac35-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="5ac35-104">L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="5ac35-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="5ac35-105">Questa guida illustra in dettaglio l'uso dell'interfaccia della riga di comando di Azure per distribuire una macchina virtuale che esegue Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="5ac35-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="5ac35-106">Dopo aver distribuito il server viene creata una connessione SSH e viene installato un server Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="5ac35-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="5ac35-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="5ac35-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ac35-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ac35-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5ac35-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5ac35-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="5ac35-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ac35-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="5ac35-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5ac35-111">Create a resource group</span></span>

<span data-ttu-id="5ac35-112">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5ac35-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5ac35-113">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="5ac35-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5ac35-114">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="5ac35-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="5ac35-115">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5ac35-115">Create virtual machine</span></span>

<span data-ttu-id="5ac35-116">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5ac35-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="5ac35-117">L'esempio seguente crea una macchina virtuale denominata *myVM* e le chiavi SSH, se non esistono già in un percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="5ac35-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="5ac35-118">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="5ac35-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="5ac35-119">Dopo che la VM è stata creata, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="5ac35-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="5ac35-120">Prendere nota di `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="5ac35-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="5ac35-121">Questo indirizzo viene usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="5ac35-121">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="5ac35-122">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="5ac35-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="5ac35-123">Per impostazione predefinita nelle macchine virtuali Linux distribuite in Azure sono consentite solo le connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="5ac35-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="5ac35-124">Se si intende usare questa macchina virtuale come un server Web, è necessario aprire la porta 80 da Internet.</span><span class="sxs-lookup"><span data-stu-id="5ac35-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="5ac35-125">Usare il comando [az vm open-port](/cli/azure/vm#open-port) per aprire la porta.</span><span class="sxs-lookup"><span data-stu-id="5ac35-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="5ac35-126">Usare SSH per connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5ac35-126">SSH into your VM</span></span>

<span data-ttu-id="5ac35-127">Usare il comando seguente per creare una sessione SSH con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ac35-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="5ac35-128">Sostituire *<publicIpAddress>* con l'indirizzo IP pubblico corretto della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ac35-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="5ac35-129">Nell'esempio riportato sopra l'indirizzo IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="5ac35-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="5ac35-130">Installare NGINX</span><span class="sxs-lookup"><span data-stu-id="5ac35-130">Install NGINX</span></span>

<span data-ttu-id="5ac35-131">Usare lo script bash seguente per aggiornare le origini dei pacchetti e installare il pacchetto NGINX più recente.</span><span class="sxs-lookup"><span data-stu-id="5ac35-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="5ac35-132">Visualizzare la pagina iniziale di NGINX</span><span class="sxs-lookup"><span data-stu-id="5ac35-132">View the NGINX welcome page</span></span>

<span data-ttu-id="5ac35-133">Dopo l'installazione di NGINX e l'apertura della porta 80 nella macchina virtuale da Internet, è possibile usare il Web browser preferito per visualizzare la pagina iniziale predefinita di NGINX.</span><span class="sxs-lookup"><span data-stu-id="5ac35-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="5ac35-134">Assicurarsi di usare l'indirizzo *publicIpAddress* descritto in precedenza per passare alla pagina predefinita.</span><span class="sxs-lookup"><span data-stu-id="5ac35-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Sito NGINX predefinito](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="5ac35-136">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="5ac35-136">Clean up resources</span></span>

<span data-ttu-id="5ac35-137">Quando non servono più, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5ac35-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5ac35-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ac35-138">Next steps</span></span>

<span data-ttu-id="5ac35-139">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="5ac35-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="5ac35-140">Per altre informazioni sulle macchine virtuali di Azure, passare all'esercitazione per le VM di Linux.</span><span class="sxs-lookup"><span data-stu-id="5ac35-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="5ac35-141">Esercitazioni per le macchine virtuali di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="5ac35-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
