---
title: Guida introduttiva ad Azure Cloud Shell (anteprima) | Microsoft Docs
description: Guida introduttiva per Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="8f1ed-103">Guida introduttiva all'uso di Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8f1ed-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="8f1ed-104">Questo documento illustra dettagliatamente come usare Azure Cloud Shell nel [portale di Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8f1ed-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="8f1ed-105">Avviare Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8f1ed-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="8f1ed-106">Avviare **Cloud Shell** dalla barra di spostamento in alto nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f1ed-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="8f1ed-107">Selezionare una sottoscrizione per creare un account di archiviazione e una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="8f1ed-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="8f1ed-108">Fare clic su "Create storage" (Crea risorsa di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="8f1ed-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="8f1ed-109">Si viene automaticamente autenticati per l'interfaccia della riga di comando di Azure 2.0 in ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="8f1ed-110">Impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8f1ed-110">Set your subscription</span></span>
1. <span data-ttu-id="8f1ed-111">Elencare le sottoscrizioni a cui si ha accesso:</span><span class="sxs-lookup"><span data-stu-id="8f1ed-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="8f1ed-112">Impostare la sottoscrizione preferita:</span><span class="sxs-lookup"><span data-stu-id="8f1ed-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="8f1ed-113">La sottoscrizione verrà memorizzata per le sessioni future con `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="8f1ed-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8f1ed-114">Create a resource group</span></span>
<span data-ttu-id="8f1ed-115">Creare un nuovo gruppo di risorse negli Stati Uniti occidentali denominato "MyRG":</span><span class="sxs-lookup"><span data-stu-id="8f1ed-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="8f1ed-116">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="8f1ed-116">Create a Linux VM</span></span>
<span data-ttu-id="8f1ed-117">Creare una VM Ubuntu nel nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="8f1ed-118">L'interfaccia della riga di comando di Azure 2.0 creerà chiavi SSH con cui configurerà la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="8f1ed-119">Per impostazione predefinita, le chiavi pubbliche e private usate per autenticare la VM vengono inserite in `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` dall'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="8f1ed-120">La cartella .ssh è persistente nell'immagine da 5 GB della condivisione file di Azure collegata.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="8f1ed-121">Il nome utente in questa VM sarà quello usato in Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="8f1ed-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="8f1ed-122">Usare SSH per connettersi alla VM Linux</span><span class="sxs-lookup"><span data-stu-id="8f1ed-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="8f1ed-123">Cercare il nome della VM nella barra di ricerca del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f1ed-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="8f1ed-124">Fare clic su "Connetti" ed eseguire: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="8f1ed-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="8f1ed-125">Quando viene stabilita la connessione SSH, verrà visualizzato il prompt di benvenuto di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8f1ed-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="8f1ed-126">+ Cleaning up</span><span class="sxs-lookup"><span data-stu-id="8f1ed-126">Cleaning up</span></span> 
<span data-ttu-id="8f1ed-127">Eliminare il gruppo di risorse e tutte le risorse al suo interno:</span><span class="sxs-lookup"><span data-stu-id="8f1ed-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="8f1ed-128">Eseguire `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="8f1ed-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f1ed-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f1ed-129">Next Steps</span></span>
[<span data-ttu-id="8f1ed-130">Informazioni sull'archiviazione permanente su Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8f1ed-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="8f1ed-131">
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="8f1ed-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="8f1ed-132">
[Informazioni sull'archiviazione file di Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8f1ed-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>