---
title: infrastruttura aaaAzure convenzioni di denominazione - Linux | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la denominazione dei servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure per macchine virtuali Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

In questo articolo si incentra sulla comprensione di come impostare le convenzioni di denominazione tooapproach per tutti i toobuild risorse di Azure diversi logico e facilmente identificabile delle risorse nel proprio ambiente.

## <a name="implementation-guidelines-for-naming-conventions"></a>Linee guida di implementazione per le convenzioni di denominazione
Decisioni:

* Quali sono le convenzioni di denominazione per le risorse di Azure?

Attività:

* Definire hello affissi toouse tra la coerenza toomaintain risorse.
* Definire l'account di archiviazione sono stati specificati nomi hello requisito relativa toobe univoco globale.
* Distribuire tooall parti coinvolte tooensure coerenza tra distribuzioni hello documento toobe convenzione di denominazione utilizzata.

## <a name="naming-conventions"></a>Convenzioni di denominazione
Prima di creare qualsiasi elemento in Azure, è necessaria una buona convenzione di denominazione Una convenzione di denominazione garantisce che tutte le risorse di hello abbiano un nome stimabile, che aiuta a basso carico amministrativo di hello associato alla gestione di tali risorse.

È possibile scegliere toofollow un set specifico di convenzioni di denominazione definite per l'intera organizzazione o per una specifica sottoscrizione di Azure o l'account. Anche se è facile per utenti singoli all'interno delle regole di organizzazioni tooestablish implicita quando si utilizzano le risorse di Azure, è necessario tooscale in grado di toobe per i team collaborano in Azure.

Concordare in anticipo il set di convenzioni di denominazione. Alcune considerazioni relative alle convenzioni di denominazione trascendono questi set di regole.

## <a name="affixes"></a>Affissi
Osservando toodefine una convenzione di denominazione, una decisione è se affisso hello in:

* inizio Hello del nome hello (prefisso)
* fine di Hello del nome di hello (suffisso)

Ecco ad esempio, due nomi possibili per un gruppo di risorse utilizzando hello `rg` appone:

* Rg-WebApp (prefisso)
* WebApp-Rg (suffisso)

Affissi possono fare riferimento a aspetti toodifferent che descrivono le risorse particolare hello. Hello nella tabella seguente vengono illustrati alcuni esempi utilizzati in genere.

| Aspetto | esempi | Note |
|:--- |:--- |:--- |
| Environment |dev, stg, prod |In base a scopo di hello e il nome di ogni ambiente. |
| Percorso |usw (Stati Uniti occidentali), use (Stati Uniti orientali 2) |A seconda area hello del Data Center hello o hello nell'area dell'organizzazione hello. |
| Componente di Azure, servizio o prodotto |Rg per gruppo di risorse, VNet per rete virtuale |A seconda del prodotto hello fornisce il supporto per i quali hello risorse. |
| Ruolo |db, app, web |In base al ruolo hello della macchina virtuale hello. |
| Istanza |01, 02 e 03 e così via. |Per le risorse con più di un'istanza. Ad esempio, i server Web con carico bilanciato in un servizio cloud. |

Quando si stabiliscono le convenzioni di denominazione, assicurarsi che è chiaramente indicato che appone toouse per ogni tipo di risorsa e in quale posizione (suffisso vs prefisso).

## <a name="dates"></a>Date
È spesso data hello toodetermine importante della creazione dal nome hello di una risorsa. Si consiglia di formato di data hello aaaammgg. Questo formato garantisce che non solo è hello completo data verrà registrata, ma anche che due risorse i cui nomi si differenziano solo per data hello vengono ordinati in ordine alfabetico e in ordine cronologico.

## <a name="naming-resources"></a>Nomi delle risorse
Definire ogni tipo di risorsa nella convenzione di denominazione hello, che dovrebbero essere presenti regole che definiscono come tooassign nomi tooeach risorsa che viene creato. Queste regole, applicare tooall tipi di risorse, ad esempio:

* Sottoscrizioni
* Account
* Account di archiviazione
* Reti virtuali
* Subnet
* Set di disponibilità
* Gruppi di risorse
* Macchine virtuali
* Endpoint
* Gruppi di sicurezza di rete
* Ruoli

tooensure che hello nome fornisce risorse di toowhich toodetermine sufficienti informazioni che fa riferimento, è necessario utilizzare nomi descrittivi.

## <a name="computer-names"></a>Nomi dei computer
Quando si crea una macchina virtuale (VM), Azure richiede un nome della macchina virtuale di backup too64 caratteri che viene utilizzato per il nome di risorsa hello. Azure Usa hello stesso nome del sistema operativo hello installato nella macchina virtuale hello. Tuttavia, questi nomi potrebbero non sempre essere hello stesso.

Se una macchina virtuale viene creata da un file di immagine con estensione vhd che contiene già un sistema operativo, nome della macchina virtuale hello in Azure può differire da hello Nome computer del sistema operativo della macchina virtuale. Questa situazione è possibile aggiungere un livello di gestione di tooVM difficoltà, che pertanto non è consigliabile. Assegnare hello hello risorsa macchina virtuale di Azure stesso nome come nome di computer hello assegnare toohello di sistema operativo della macchina virtuale.

Si consiglia di tale nome di macchina virtuale di Azure hello è hello come hello Nome computer del sistema operativo sottostante.

## <a name="storage-account-names"></a>Nomi account di archiviazione
In questa sezione non si applica troppo[dischi gestiti di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), come si crea un account di archiviazione separata. Per i dischi non gestiti, gli account di archiviazione hanno regole speciali che ne controllano i nomi. È possibile usare solo lettere minuscole e numeri. Per altre informazioni, vedere [Creare un account di archiviazione](../../storage/storage-create-storage-account.md#create-a-storage-account). Inoltre, nome account di archiviazione hello, con core.windows.net, deve essere un nome DNS univoco globale valido. Ad esempio, se l'account di archiviazione hello viene chiamato mystorageaccount, hello seguenti nomi DNS risultanti devono essere univoci:

* mystorageaccount.blob.core.windows.net
* mystorageaccount.table.core.windows.net
* mystorageaccount.queue.core.windows.net

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

