---
title: Guida introduttiva di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Avvio rapido per hello Shell di Cloud di Azure
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
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="49d3c-103">Guida introduttiva per l'utilizzo di hello Shell di Cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="49d3c-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="49d3c-104">Questo documento illustra in dettaglio come toouse hello Azure Cloud Shell in hello [portale di Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="49d3c-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="49d3c-105">Avviare Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="49d3c-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="49d3c-106">Avviare **Shell Cloud** dal riquadro di spostamento superiore hello di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="49d3c-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="49d3c-107">Selezionare una sottoscrizione toocreate un account di archiviazione e condivisione di file di Azure</span><span class="sxs-lookup"><span data-stu-id="49d3c-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="49d3c-108">Fare clic su "Create storage" (Crea risorsa di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="49d3c-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="49d3c-109">Si viene automaticamente autenticati per l'interfaccia della riga di comando di Azure 2.0 in ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="49d3c-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="49d3c-110">Impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="49d3c-110">Set your subscription</span></span>
1. <span data-ttu-id="49d3c-111">Elencare le sottoscrizioni a cui si ha accesso:</span><span class="sxs-lookup"><span data-stu-id="49d3c-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="49d3c-112">Impostare la sottoscrizione preferita:</span><span class="sxs-lookup"><span data-stu-id="49d3c-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="49d3c-113">La sottoscrizione verrà memorizzata per le sessioni future con `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="49d3c-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="49d3c-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="49d3c-114">Create a resource group</span></span>
<span data-ttu-id="49d3c-115">Creare un nuovo gruppo di risorse negli Stati Uniti occidentali denominato "MyRG":</span><span class="sxs-lookup"><span data-stu-id="49d3c-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="49d3c-116">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="49d3c-116">Create a Linux VM</span></span>
<span data-ttu-id="49d3c-117">Creare una VM Ubuntu nel nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="49d3c-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="49d3c-118">Hello Azure CLI 2.0 verrà create le chiavi SSH e hello installazione VM con essi.</span><span class="sxs-lookup"><span data-stu-id="49d3c-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="49d3c-119">Hello tooauthenticate chiavi pubbliche e private usate la macchina virtuale vengono inseriti in `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` dall'interfaccia CLI di Azure 2.0 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="49d3c-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="49d3c-120">La cartella .ssh è persistente nell'immagine da 5 GB della condivisione file di Azure collegata.</span><span class="sxs-lookup"><span data-stu-id="49d3c-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="49d3c-121">Il nome utente in questa VM sarà quello usato in Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="49d3c-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="49d3c-122">Usare SSH per connettersi alla VM Linux</span><span class="sxs-lookup"><span data-stu-id="49d3c-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="49d3c-123">Cercare il nome della macchina virtuale nella barra di ricerca del portale Azure hello</span><span class="sxs-lookup"><span data-stu-id="49d3c-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="49d3c-124">Fare clic su "Connetti" ed eseguire: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="49d3c-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="49d3c-125">Al momento di stabilire una connessione SSH hello, dovrebbe essere prompt di hello Ubuntu iniziale.</span><span class="sxs-lookup"><span data-stu-id="49d3c-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="49d3c-126">+ Cleaning up</span><span class="sxs-lookup"><span data-stu-id="49d3c-126">Cleaning up</span></span> 
<span data-ttu-id="49d3c-127">Eliminare il gruppo di risorse e tutte le risorse al suo interno:</span><span class="sxs-lookup"><span data-stu-id="49d3c-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="49d3c-128">Eseguire `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="49d3c-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="49d3c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49d3c-129">Next Steps</span></span>
[<span data-ttu-id="49d3c-130">Informazioni sull'archiviazione permanente su Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="49d3c-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="49d3c-131">
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="49d3c-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="49d3c-132">
[Informazioni sull'archiviazione file di Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="49d3c-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>