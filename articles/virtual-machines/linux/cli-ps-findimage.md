---
title: Selezionare immagini di macchine virtuali Linux con l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Informazioni su come usare l'interfaccia della riga di comando di Azure per determinare il server di pubblicazione, l'offerta, la SKU e la versione delle immagini di macchine virtuali del Marketplace.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="3ad38-103">Come trovare immagini di macchine virtuali Linux in Azure Marketplace con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3ad38-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="3ad38-104">Questo argomento descrive come usare l'interfaccia della riga di comando di Azure 2.0 per trovare immagini di VM (Virtual Machine, macchina virtuale) in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3ad38-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="3ad38-105">Usare queste informazioni per specificare un'immagine del Marketplace quando si crea una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="3ad38-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="3ad38-106">Assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di avere effettuato l'accesso a un account di Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="3ad38-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="3ad38-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="3ad38-107">Terminology</span></span>

<span data-ttu-id="3ad38-108">Le immagini in Marketplace vengono identificate nell'interfaccia della riga di comando e altri strumenti di Azure in base a una gerarchia:</span><span class="sxs-lookup"><span data-stu-id="3ad38-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="3ad38-109">**Server di pubblicazione**: un'organizzazione che ha creato l'immagine.</span><span class="sxs-lookup"><span data-stu-id="3ad38-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="3ad38-110">Esempio: Canonical</span><span class="sxs-lookup"><span data-stu-id="3ad38-110">Example: Canonical</span></span>
* <span data-ttu-id="3ad38-111">**Offerta**: un gruppo di immagini correlate create da un server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="3ad38-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="3ad38-112">Esempio: server Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3ad38-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="3ad38-113">**SKU**: un'istanza di un'offerta, ad esempio una versione principale di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ad38-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="3ad38-114">Esempio: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="3ad38-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="3ad38-115">**Versione**: il numero di versione di un'immagine SKU.</span><span class="sxs-lookup"><span data-stu-id="3ad38-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="3ad38-116">Quando si specifica l'immagine, è possibile sostituire il numero di versione con "latest", che seleziona la versione più recente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ad38-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="3ad38-117">Per specificare un'immagine in Marketplace, si usa in genere l'immagine *URN*.</span><span class="sxs-lookup"><span data-stu-id="3ad38-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="3ad38-118">L'URN combina tali valori, separati dal carattere due punti (:): *Server di pubblicazione*:*Offerta*:*SKU*:*Versione*.</span><span class="sxs-lookup"><span data-stu-id="3ad38-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="3ad38-119">Elencare immagini popolari</span><span class="sxs-lookup"><span data-stu-id="3ad38-119">List popular images</span></span>

<span data-ttu-id="3ad38-120">Eseguire il comando [az vm image list](/cli/azure/vm/image#list), senza l'opzione `--all`, per visualizzare un elenco di immagini di VM popolari in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3ad38-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="3ad38-121">Ad esempio, eseguire il comando seguente per visualizzare un elenco memorizzato nella cache di immagini popolari in formato tabella:</span><span class="sxs-lookup"><span data-stu-id="3ad38-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="3ad38-122">L'output include l'URN (il valore nella colonna *Urn*), che consente di specificare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="3ad38-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="3ad38-123">Se si vuole creare una VM con tali immagini popolari in Marketplace, è possibile specificare in alternativa l'alias URN, ad esempio *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="3ad38-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="3ad38-124">Trovare immagini specifiche</span><span class="sxs-lookup"><span data-stu-id="3ad38-124">Find specific images</span></span>

<span data-ttu-id="3ad38-125">Per trovare un'immagine di VM specifica in Marketplace, usare il comando `az vm image list` con l'opzione `--all`.</span><span class="sxs-lookup"><span data-stu-id="3ad38-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="3ad38-126">Questa versione del comando richiede del tempo per essere completata e può restituire un output lungo, pertanto l'elenco si filtra in genere in base a `--publisher` o a un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="3ad38-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="3ad38-127">Ad esempio, il comando che segue visualizza tutte le offerte Debian. Tenere presente che senza l'opzione `--all`, la ricerca viene eseguita solo nella cache locale delle immagini comuni:</span><span class="sxs-lookup"><span data-stu-id="3ad38-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="3ad38-128">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="3ad38-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="3ad38-129">Applicare filtri simili con le opzioni `--location`, `--publisher` e `--sku`.</span><span class="sxs-lookup"><span data-stu-id="3ad38-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="3ad38-130">È anche possibile cercare corrispondenze parziali in base a un filtro, ad esempio cercare `--offer Deb` per trovare tutte le immagini Debian.</span><span class="sxs-lookup"><span data-stu-id="3ad38-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="3ad38-131">Se non si indica una posizione specifica con l'opzione `--location`, per impostazione predefinita vengono restituiti i valori relativi a `westus`.</span><span class="sxs-lookup"><span data-stu-id="3ad38-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="3ad38-132">Per impostare un percorso predefinito diverso eseguire `az configure --defaults location=<location>`.</span><span class="sxs-lookup"><span data-stu-id="3ad38-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="3ad38-133">Ad esempio, il comando seguente elenca elencati tutti gli SKU di Debian 8 in `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="3ad38-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="3ad38-134">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="3ad38-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-the-images"></a><span data-ttu-id="3ad38-135">Esplorare le immagini</span><span class="sxs-lookup"><span data-stu-id="3ad38-135">Navigate the images</span></span> 
<span data-ttu-id="3ad38-136">Un altro modo per trovare un'immagine in una posizione è l'esecuzione in sequenza dei comandi [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers) e [az vm image list-skus](/cli/azure/vm/image#list-skus) .</span><span class="sxs-lookup"><span data-stu-id="3ad38-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="3ad38-137">Con questi comandi si determinano questi valori:</span><span class="sxs-lookup"><span data-stu-id="3ad38-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="3ad38-138">Elencando gli editori di immagini.</span><span class="sxs-lookup"><span data-stu-id="3ad38-138">List the image publishers.</span></span>
2. <span data-ttu-id="3ad38-139">Elencando le offerte di un determinato editore.</span><span class="sxs-lookup"><span data-stu-id="3ad38-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="3ad38-140">Elencando le SKU di una determinata offerta.</span><span class="sxs-lookup"><span data-stu-id="3ad38-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="3ad38-141">Ad esempio, il comando seguente elenca i server di pubblicazione di immagini nella posizione Stati Uniti occidentali (westus):</span><span class="sxs-lookup"><span data-stu-id="3ad38-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="3ad38-142">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="3ad38-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="3ad38-143">Usare queste informazioni per individuare le offerte di un server di pubblicazione specifico.</span><span class="sxs-lookup"><span data-stu-id="3ad38-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="3ad38-144">Ad esempio, se Canonical è un server di pubblicazione di immagini nella posizione Stati Uniti occidentali, è possibile trovare le relative offerte eseguendo `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="3ad38-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="3ad38-145">Passare la posizione e il server di pubblicazione come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3ad38-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="3ad38-146">Output:</span><span class="sxs-lookup"><span data-stu-id="3ad38-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="3ad38-147">Come si può vedere, nell'area degli Stati Uniti occidentali Canonical pubblica l'offerta **UbuntuServer** in Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad38-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="3ad38-148">Ma quali sono le SKU?</span><span class="sxs-lookup"><span data-stu-id="3ad38-148">But what SKUs?</span></span> <span data-ttu-id="3ad38-149">Per ottenere questi valori, eseguire `azure vm image list-skus` e impostare il percorso, il server di pubblicazione e l'offerta individuati:</span><span class="sxs-lookup"><span data-stu-id="3ad38-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="3ad38-150">Output:</span><span class="sxs-lookup"><span data-stu-id="3ad38-150">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="3ad38-151">Usare infine il comando `az vm image list` per trovare una versione specifica della SKU voluta, ad esempio, **16.04-LTS**:</span><span class="sxs-lookup"><span data-stu-id="3ad38-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="3ad38-152">Output:</span><span class="sxs-lookup"><span data-stu-id="3ad38-152">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="3ad38-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ad38-153">Next steps</span></span>
<span data-ttu-id="3ad38-154">A questo punto è possibile scegliere con precisione l'immagine da usare prendendo nota del valore URN.</span><span class="sxs-lookup"><span data-stu-id="3ad38-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="3ad38-155">Passare questo valore con il parametro `--image` quando si crea una macchina virtuale con il [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3ad38-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="3ad38-156">Facoltativamente, è possibile sostituire il numero di versione nell'URN con "latest",</span><span class="sxs-lookup"><span data-stu-id="3ad38-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="3ad38-157">che rappresenta sempre la versione più recente della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ad38-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="3ad38-158">Per creare rapidamente una macchina virtuale usando le informazioni relative all'URN, vedere [Creare e gestire VM Linux con l'interfaccia della riga di comando di Azure](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3ad38-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
