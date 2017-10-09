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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>La modalità di immagini toofind VM Linux in hello Azure Marketplace con hello CLI di Azure
In questo argomento viene descritto come toouse hello immagini di macchina virtuale di Azure 2.0 CLI toofind in hello Azure Marketplace. Utilizzare questa toospecify informazioni un'immagine del Marketplace per creare una VM Linux.

Verificare che più recente installato hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e vengono registrati in tooan account Azure (`az login`).

## <a name="terminology"></a>Terminologia

Le immagini di Marketplace vengono identificate in hello CLI e altri strumenti di Azure in base tooa gerarchia:

* **Server di pubblicazione** -hello organizzazione che ha creato l'immagine di hello. Esempio: Canonical
* **Offerta**: un gruppo di immagini correlate create da un server di pubblicazione. Esempio: server Ubuntu
* **SKU**: un'istanza di un'offerta, ad esempio una versione principale di una distribuzione. Esempio: 16.04-LTS
* **Versione** -numero di versione di un'immagine SKU hello. Quando si specifica l'immagine di hello, è possibile sostituire il numero di versione hello con "più recente", che consente di selezionare più recente della distribuzione hello hello.

toospecify un'immagine del Marketplace, è in genere utilizzare hello immagine *URN*. Hello URN combina tali valori, separati dal carattere due punti (:) hello: *Publisher*:*offrono*:*Sku*:*versione*. 


## <a name="list-popular-images"></a>Elencare immagini popolari

Eseguire hello [elenco di immagini di macchina virtuale az](/cli/azure/vm/image#list) comando, senza hello `--all` opzione, toosee immagini di un elenco di VM diffusi in hello Azure Marketplace. Ad esempio, eseguire hello successivo comando toodisplay un elenco memorizzati nella cache delle immagini diffusi in formato tabella:

```azurecli
az vm image list --output table
```

output di Hello include hello URN (hello valore hello *Urn* colonna), che si utilizza toospecify hello immagine. Quando si crea una macchina virtuale con una di queste immagini comune di Marketplace, è possibile specificare alias di hello URN, ad esempio *UbuntuLTS*.

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

## <a name="find-specific-images"></a>Trovare immagini specifiche

un'immagine di macchina virtuale specifica nel Marketplace, hello toofind utilizzare hello `az vm image list` con hello `--all` opzione. Questa versione di hello comando accetta alcuni toocomplete tempo e può restituire un output lungo, pertanto è in genere filtrare elenco hello da `--publisher` o un altro parametro. 

Ad esempio, hello comando seguente visualizza tutte le offerte Debian (tenere presente che senza hello `--all` passare, viene cercato solo cache locale di hello delle immagini comune):

```azurecli
az vm image list --offer Debian --all --output table 

```

Output parziale: 
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

Applicare filtri simile con hello `--location`, `--publisher`, e `--sku` opzioni. È anche possibile eseguire le corrispondenze parziali su un filtro, ad esempio la ricerca di `--offer Deb` toofind tutte le immagini Debian.

Se non si specifica una determinata posizione con hello `--location` , hello i valori delle opzioni per `westus` vengono restituiti per impostazione predefinita. Per impostare un percorso predefinito diverso eseguire `az configure --defaults location=<location>`.

Ad esempio, hello comando seguente vengono elencati tutti gli SKU di 8 Debian in `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Output parziale:

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

## <a name="navigate-hello-images"></a>Passare immagini hello 
Un altro modo toofind un'immagine in un percorso è hello toorun [az vm immagine elenco-server di pubblicazione](/cli/azure/vm/image#list-publishers), [az vm immagine elenco-offerte](/cli/azure/vm/image#list-offers), e [Elenca le immagini vm az-SKU](/cli/azure/vm/image#list-skus) comandi in sequenza. Con questi comandi si determinano questi valori:

1. Elenco hello immagine server di pubblicazione.
2. Elencando le offerte di un determinato editore.
3. Elencando le SKU di una determinata offerta.


Ad esempio, hello comando riportato di seguito sono elencati il server di pubblicazione di hello immagine nella posizione di Stati Uniti occidentali hello:

```azurecli
az vm image list-publishers --location westus --output table
```

Output parziale:

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
Utilizzare che questa toofind informazioni sono disponibili da un editore specifico. Ad esempio, se Canonical è un server di pubblicazione di immagine nel percorso di Stati Uniti occidentali hello, trovare le proprie offerte eseguendo `azure vm image list-offers`. Passare il percorso di hello e server di pubblicazione hello come hello di esempio seguente:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Output:

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
Viene visualizzato nell'area Stati Uniti occidentali hello, Canonical pubblica hello **UbuntuServer** offrono in Azure. Ma quali SKU? esecuzione di tali valori, tooget `azure vm image list-skus` e impostare il percorso di hello, server di pubblicazione e offerta che vengono individuati:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Output:

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

Infine, utilizzare hello `az vm image list` toofind comando una specifica versione di hello SKU di cui si desidera, ad esempio, **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Output:

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
## <a name="next-steps"></a>Passaggi successivi
Ora è possibile scegliere l'immagine di hello precisamente toouse si vuole, prendere nota del valore URN hello. Passare questo valore con hello `--image` parametro quando si crea una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando. Tenere presente che è possibile facoltativamente sostituire il numero di versione hello in hello URN "più recente". Questa versione è sempre più recente della distribuzione hello hello. toocreate una macchina virtuale rapidamente usando le informazioni di URN hello, vedere [creare e gestire le macchine virtuali Linux con hello Azure CLI](tutorial-manage-vm.md).
