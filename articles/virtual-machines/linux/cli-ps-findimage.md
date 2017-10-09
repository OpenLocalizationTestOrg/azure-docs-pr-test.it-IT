---
title: le immagini VM Linux di aaaSelect con hello CLI di Azure | Documenti Microsoft
description: Informazioni su come toouse hello toodetermine hello editore CLI di Azure, offerta, SKU e la versione per le immagini VM Marketplace.
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
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="06ea4-103">La modalità di immagini toofind VM Linux in hello Azure Marketplace con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="06ea4-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="06ea4-104">In questo argomento viene descritto come toouse hello immagini di macchina virtuale di Azure 2.0 CLI toofind in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="06ea4-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="06ea4-105">Utilizzare questa toospecify informazioni un'immagine del Marketplace per creare una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="06ea4-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="06ea4-106">Verificare che più recente installato hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e vengono registrati in tooan account Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="06ea4-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="06ea4-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="06ea4-107">Terminology</span></span>

<span data-ttu-id="06ea4-108">Le immagini di Marketplace vengono identificate in hello CLI e altri strumenti di Azure in base tooa gerarchia:</span><span class="sxs-lookup"><span data-stu-id="06ea4-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="06ea4-109">**Server di pubblicazione** -hello organizzazione che ha creato l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="06ea4-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="06ea4-110">Esempio: Canonical</span><span class="sxs-lookup"><span data-stu-id="06ea4-110">Example: Canonical</span></span>
* <span data-ttu-id="06ea4-111">**Offerta**: un gruppo di immagini correlate create da un server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="06ea4-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="06ea4-112">Esempio: server Ubuntu</span><span class="sxs-lookup"><span data-stu-id="06ea4-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="06ea4-113">**SKU**: un'istanza di un'offerta, ad esempio una versione principale di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06ea4-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="06ea4-114">Esempio: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="06ea4-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="06ea4-115">**Versione** -numero di versione di un'immagine SKU hello.</span><span class="sxs-lookup"><span data-stu-id="06ea4-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="06ea4-116">Quando si specifica l'immagine di hello, è possibile sostituire il numero di versione hello con "più recente", che consente di selezionare più recente della distribuzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="06ea4-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="06ea4-117">toospecify un'immagine del Marketplace, è in genere utilizzare hello immagine *URN*.</span><span class="sxs-lookup"><span data-stu-id="06ea4-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="06ea4-118">Hello URN combina tali valori, separati dal carattere due punti (:) hello: *Publisher*:*offrono*:*Sku*:*versione*.</span><span class="sxs-lookup"><span data-stu-id="06ea4-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="06ea4-119">Elencare immagini popolari</span><span class="sxs-lookup"><span data-stu-id="06ea4-119">List popular images</span></span>

<span data-ttu-id="06ea4-120">Eseguire hello [elenco di immagini di macchina virtuale az](/cli/azure/vm/image#list) comando, senza hello `--all` opzione, toosee immagini di un elenco di VM diffusi in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="06ea4-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="06ea4-121">Ad esempio, eseguire hello successivo comando toodisplay un elenco memorizzati nella cache delle immagini diffusi in formato tabella:</span><span class="sxs-lookup"><span data-stu-id="06ea4-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="06ea4-122">output di Hello include hello URN (hello valore hello *Urn* colonna), che si utilizza toospecify hello immagine.</span><span class="sxs-lookup"><span data-stu-id="06ea4-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="06ea4-123">Quando si crea una macchina virtuale con una di queste immagini comune di Marketplace, è possibile specificare alias di hello URN, ad esempio *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="06ea4-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="06ea4-124">Trovare immagini specifiche</span><span class="sxs-lookup"><span data-stu-id="06ea4-124">Find specific images</span></span>

<span data-ttu-id="06ea4-125">un'immagine di macchina virtuale specifica nel Marketplace, hello toofind utilizzare hello `az vm image list` con hello `--all` opzione.</span><span class="sxs-lookup"><span data-stu-id="06ea4-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="06ea4-126">Questa versione di hello comando accetta alcuni toocomplete tempo e può restituire un output lungo, pertanto è in genere filtrare elenco hello da `--publisher` o un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="06ea4-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="06ea4-127">Ad esempio, hello comando seguente visualizza tutte le offerte Debian (tenere presente che senza hello `--all` passare, viene cercato solo cache locale di hello delle immagini comune):</span><span class="sxs-lookup"><span data-stu-id="06ea4-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="06ea4-128">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="06ea4-128">Partial output:</span></span> 
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

<span data-ttu-id="06ea4-129">Applicare filtri simile con hello `--location`, `--publisher`, e `--sku` opzioni.</span><span class="sxs-lookup"><span data-stu-id="06ea4-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="06ea4-130">È anche possibile eseguire le corrispondenze parziali su un filtro, ad esempio la ricerca di `--offer Deb` toofind tutte le immagini Debian.</span><span class="sxs-lookup"><span data-stu-id="06ea4-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="06ea4-131">Se non si specifica una determinata posizione con hello `--location` , hello i valori delle opzioni per `westus` vengono restituiti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="06ea4-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="06ea4-132">Per impostare un percorso predefinito diverso eseguire `az configure --defaults location=<location>`.</span><span class="sxs-lookup"><span data-stu-id="06ea4-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="06ea4-133">Ad esempio, hello comando seguente vengono elencati tutti gli SKU di 8 Debian in `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="06ea4-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="06ea4-134">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="06ea4-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="06ea4-135">Passare immagini hello</span><span class="sxs-lookup"><span data-stu-id="06ea4-135">Navigate hello images</span></span> 
<span data-ttu-id="06ea4-136">Un altro modo toofind un'immagine in un percorso è hello toorun [az vm immagine elenco-server di pubblicazione](/cli/azure/vm/image#list-publishers), [az vm immagine elenco-offerte](/cli/azure/vm/image#list-offers), e [Elenca le immagini vm az-SKU](/cli/azure/vm/image#list-skus) comandi in sequenza.</span><span class="sxs-lookup"><span data-stu-id="06ea4-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="06ea4-137">Con questi comandi si determinano questi valori:</span><span class="sxs-lookup"><span data-stu-id="06ea4-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="06ea4-138">Elenco hello immagine server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="06ea4-138">List hello image publishers.</span></span>
2. <span data-ttu-id="06ea4-139">Elencando le offerte di un determinato editore.</span><span class="sxs-lookup"><span data-stu-id="06ea4-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="06ea4-140">Elencando le SKU di una determinata offerta.</span><span class="sxs-lookup"><span data-stu-id="06ea4-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="06ea4-141">Ad esempio, hello comando riportato di seguito sono elencati il server di pubblicazione di hello immagine nella posizione di Stati Uniti occidentali hello:</span><span class="sxs-lookup"><span data-stu-id="06ea4-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="06ea4-142">Output parziale:</span><span class="sxs-lookup"><span data-stu-id="06ea4-142">Partial output:</span></span>

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
<span data-ttu-id="06ea4-143">Utilizzare che questa toofind informazioni sono disponibili da un editore specifico.</span><span class="sxs-lookup"><span data-stu-id="06ea4-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="06ea4-144">Ad esempio, se Canonical è un server di pubblicazione di immagine nel percorso di Stati Uniti occidentali hello, trovare le proprie offerte eseguendo `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="06ea4-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="06ea4-145">Passare il percorso di hello e server di pubblicazione hello come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="06ea4-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="06ea4-146">Output:</span><span class="sxs-lookup"><span data-stu-id="06ea4-146">Output:</span></span>

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
<span data-ttu-id="06ea4-147">Viene visualizzato nell'area Stati Uniti occidentali hello, Canonical pubblica hello **UbuntuServer** offrono in Azure.</span><span class="sxs-lookup"><span data-stu-id="06ea4-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="06ea4-148">Ma quali SKU? esecuzione di tali valori, tooget `azure vm image list-skus` e impostare il percorso di hello, server di pubblicazione e offerta che vengono individuati:</span><span class="sxs-lookup"><span data-stu-id="06ea4-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="06ea4-149">Output:</span><span class="sxs-lookup"><span data-stu-id="06ea4-149">Output:</span></span>

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

<span data-ttu-id="06ea4-150">Infine, utilizzare hello `az vm image list` toofind comando una specifica versione di hello SKU di cui si desidera, ad esempio, **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="06ea4-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="06ea4-151">Output:</span><span class="sxs-lookup"><span data-stu-id="06ea4-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="06ea4-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06ea4-152">Next steps</span></span>
<span data-ttu-id="06ea4-153">Ora è possibile scegliere l'immagine di hello precisamente toouse si vuole, prendere nota del valore URN hello.</span><span class="sxs-lookup"><span data-stu-id="06ea4-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="06ea4-154">Passare questo valore con hello `--image` parametro quando si crea una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="06ea4-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="06ea4-155">Tenere presente che è possibile facoltativamente sostituire il numero di versione hello in hello URN "più recente".</span><span class="sxs-lookup"><span data-stu-id="06ea4-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="06ea4-156">Questa versione è sempre più recente della distribuzione hello hello.</span><span class="sxs-lookup"><span data-stu-id="06ea4-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="06ea4-157">toocreate una macchina virtuale rapidamente usando le informazioni di URN hello, vedere [creare e gestire le macchine virtuali Linux con hello Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="06ea4-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
