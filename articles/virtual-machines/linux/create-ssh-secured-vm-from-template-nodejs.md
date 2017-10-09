---
title: aaaCreate una VM Linux con un modello di Azure 1.0 CLI di Azure | Documenti Microsoft
description: Creare una VM Linux in Azure mediante Azure CLI 1.0 hello e un modello di gestione risorse di Azure.
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
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="47a59-103">Come toocreate una VM Linux utilizzando hello Azure CLI 1.0 un modello di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="47a59-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="47a59-104">Questo articolo illustra come tooquickly distribuire una macchina virtuale di Linux mediante Azure CLI 1.0 hello e un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="47a59-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="47a59-105">articolo Hello richiede:</span><span class="sxs-lookup"><span data-stu-id="47a59-105">hello article requires:</span></span>

* <span data-ttu-id="47a59-106">Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47a59-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="47a59-107">Hello [CLI di Azure 1.0](../../cli-install-nodejs.md) accesso `azure login`.</span><span class="sxs-lookup"><span data-stu-id="47a59-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="47a59-108">Hello Azure CLI *deve essere* modalità Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="47a59-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="47a59-109">È possibile distribuire rapidamente un modello Linux VM utilizzando hello [portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47a59-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="47a59-110">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="47a59-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="47a59-111">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="47a59-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="47a59-112">[Azure CLI 1.0](#quick-command-summary) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="47a59-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="47a59-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="47a59-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="47a59-114">Breve riepilogo del comando</span><span class="sxs-lookup"><span data-stu-id="47a59-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="47a59-115">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="47a59-115">Detailed Walkthrough</span></span>
<span data-ttu-id="47a59-116">I modelli consentono toocreate VM in Azure con le impostazioni che si desidera toocustomize durante l'avvio di hello, impostazioni, ad esempio nomi utente e i nomi host.</span><span class="sxs-lookup"><span data-stu-id="47a59-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="47a59-117">Per questo articolo, verrà avviato un modello di Azure utilizzando una VM Ubuntu con un gruppo di sicurezza di rete (NSG) con la porta 22 aperta per SSH.</span><span class="sxs-lookup"><span data-stu-id="47a59-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="47a59-118">I modelli di Azure Resource Manager sono file JSON che possono essere usati per semplici attività occasionali, ad esempio l'avvio di una VM come in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="47a59-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="47a59-119">Modelli di Azure possono essere anche usato tooconstruct configurazioni complesse di Azure degli ambienti intera come uno stack di distribuzione di test, sviluppo o di produzione.</span><span class="sxs-lookup"><span data-stu-id="47a59-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="47a59-120">Creare hello VM Linux</span><span class="sxs-lookup"><span data-stu-id="47a59-120">Create hello Linux VM</span></span>
<span data-ttu-id="47a59-121">Hello seguente esempio di codice viene illustrato come toocall `azure group create` toocreate una risorsa gruppo e distribuire una VM Linux protetto SSH in hello utilizzando [questo modello di gestione risorse di Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="47a59-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="47a59-122">Tenere presente che nell'esempio sono necessari nomi toouse che si trovano ambiente tooyour univoco.</span><span class="sxs-lookup"><span data-stu-id="47a59-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="47a59-123">Questo esempio viene utilizzato *myResourceGroup* come nome del gruppo di risorse hello, e *myVM* come nome della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="47a59-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="47a59-124">output di Hello dovrebbe essere simile hello dopo il blocco di output:</span><span class="sxs-lookup"><span data-stu-id="47a59-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="47a59-125">Tale esempio distribuita una macchina virtuale tramite hello `--template-uri` parametro.</span><span class="sxs-lookup"><span data-stu-id="47a59-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="47a59-126">È anche possibile scaricare o creare un modello in locale e passare il modello di hello utilizzando hello `--template-file` parametro con un file di modello toohello percorso come argomento.</span><span class="sxs-lookup"><span data-stu-id="47a59-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="47a59-127">Hello CLI di Azure richiede i parametri di hello richiesti dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="47a59-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47a59-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47a59-128">Next steps</span></span>
<span data-ttu-id="47a59-129">Hello ricerca [raccolta di modelli](https://azure.microsoft.com/documentation/templates/) toodiscover quali toodeploy Framework applicazione successivo.</span><span class="sxs-lookup"><span data-stu-id="47a59-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

