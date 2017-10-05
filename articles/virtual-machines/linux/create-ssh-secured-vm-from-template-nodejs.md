---
title: Creare una VM Linux usando un modello di Azure con l'interfaccia della riga di comando 1.0 di Azure| Microsoft Docs
description: Creare una VM Linux in Azure con un'interfaccia della riga di comando 1.0 di Azure e un modello di Azure Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="788ed-103">Procedura per creare una VM Linux in Azure con un'interfaccia della riga di comando 1.0 di Azure e un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="788ed-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="788ed-104">Questo articolo illustra come distribuire rapidamente una macchina virtuale Linux usando un'interfaccia della riga di comando 1.0 di Azure e un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="788ed-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="788ed-105">L'articolo richiede:</span><span class="sxs-lookup"><span data-stu-id="788ed-105">The article requires:</span></span>

* <span data-ttu-id="788ed-106">Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="788ed-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="788ed-107">Accesso tramite `azure login` per l'[interfaccia della riga di comando 1.0 di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="788ed-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="788ed-108">L'interfaccia della riga di comando di Azure *deve essere impostata obbligatoriamente* sulla modalità Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="788ed-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="788ed-109">È anche possibile distribuire rapidamente un modello di VM Linux usando il [portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="788ed-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="788ed-110">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="788ed-110">CLI versions to complete the task</span></span>
<span data-ttu-id="788ed-111">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="788ed-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="788ed-112">[Interfaccia della riga di comando di Azure 1.0](#quick-command-summary): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="788ed-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="788ed-113">[Interfaccia della riga di comando di Azure 2.0](create-ssh-secured-vm-from-template.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="788ed-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="788ed-114">Breve riepilogo del comando</span><span class="sxs-lookup"><span data-stu-id="788ed-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="788ed-115">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="788ed-115">Detailed Walkthrough</span></span>
<span data-ttu-id="788ed-116">I modelli consentono di creare VM in Azure con le impostazioni da personalizzare durante l'avvio, ad esempio i nomi utente e i nomi host.</span><span class="sxs-lookup"><span data-stu-id="788ed-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="788ed-117">Per questo articolo, verrà avviato un modello di Azure utilizzando una VM Ubuntu con un gruppo di sicurezza di rete (NSG) con la porta 22 aperta per SSH.</span><span class="sxs-lookup"><span data-stu-id="788ed-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="788ed-118">I modelli di Azure Resource Manager sono file JSON che possono essere usati per semplici attività occasionali, ad esempio l'avvio di una VM come in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="788ed-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="788ed-119">I modelli di Azure possono essere usati anche per costruire configurazioni di Azure complesse di interi ambienti, ad esempio uno stack di distribuzione di test, di sviluppo o di produzione.</span><span class="sxs-lookup"><span data-stu-id="788ed-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="788ed-120">Creare la VM Linux</span><span class="sxs-lookup"><span data-stu-id="788ed-120">Create the Linux VM</span></span>
<span data-ttu-id="788ed-121">L'esempio di codice seguente illustra come chiamare `azure group create` per creare un gruppo di risorse e distribuire una VM Linux protetta con SSH, usando contemporaneamente [questo modello di Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="788ed-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="788ed-122">Tenere presente che nell'esempio è necessario usare nomi univoci per l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="788ed-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="788ed-123">In questo esempio il nome del gruppo di risorse è *myResourceGroup* e il nome della VM è *myVM*.</span><span class="sxs-lookup"><span data-stu-id="788ed-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="788ed-124">L'output dovrebbe essere simile al blocco di output seguente:</span><span class="sxs-lookup"><span data-stu-id="788ed-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="788ed-125">L'esempio ha distribuito una VM usando il parametro `--template-uri` .</span><span class="sxs-lookup"><span data-stu-id="788ed-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="788ed-126">È anche possibile scaricare o creare un modello in locale e passarlo usando il parametro `--template-file` con un percorso del file modello come argomento.</span><span class="sxs-lookup"><span data-stu-id="788ed-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="788ed-127">L'interfaccia della riga di comando di Azure richiede i parametri necessari per il modello.</span><span class="sxs-lookup"><span data-stu-id="788ed-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="788ed-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="788ed-128">Next steps</span></span>
<span data-ttu-id="788ed-129">Eseguire una ricerca nella [raccolta di modelli](https://azure.microsoft.com/documentation/templates/) per scoprire quali framework per app si possono distribuire successivamente.</span><span class="sxs-lookup"><span data-stu-id="788ed-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

