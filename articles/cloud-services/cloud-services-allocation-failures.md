---
title: Errore di allocazione del servizio Cloud aaaTroubleshooting | Documenti Microsoft
description: Risoluzione dei problemi relativi ad errori di allocazione quando si distribuiscono servizi Cloud in Azure
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Risoluzione dei problemi relativi ad errori di allocazione quando si distribuiscono servizi Cloud in Azure
## <a name="summary"></a>Riepilogo
Quando si distribuisce tooa istanze servizio Cloud o aggiungere istanze del ruolo di lavoro o un nuovo sito web, Microsoft Azure alloca le risorse di calcolo. In alcuni casi, possono verificarsi errori durante l'esecuzione di queste operazioni anche prima di raggiungere i limiti di hello sottoscrizione di Azure. In questo articolo vengono illustrate le cause di alcune delle comuni errori di allocazione hello hello e suggerisce una possibile risoluzione. informazioni di Hello potrebbero essere utile anche quando si pianifica la distribuzione hello dei servizi.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Informazioni preliminari: come funziona l'allocazione
server Hello in Data Center di Azure vengono partizionati in cluster. Una nuova richiesta di allocazione del servizio cloud viene eseguita in più cluster. Quando hello prima istanza è tooa distribuiti servizio cloud (in gestione temporanea o produzione), servizio cloud Ottiene cluster tooa bloccati. Ulteriormente le distribuzioni per il servizio cloud hello avverrà in hello stesso cluster. In questo articolo, si farà riferimento toothis come "aggiunto tooa cluster". Diagramma 1 riportato di seguito viene illustrato il caso di hello di un'allocazione normale che viene eseguito un tentativo di più cluster; Diagramma 2 di viene illustrato il caso di hello di un'allocazione tooCluster bloccati che 2 in quanto in cui è hello CS_1 di servizio Cloud esistente è ospitato.

![Diagramma di allocazione](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Perché si verifica un errore di allocazione
Quando una richiesta di allocazione è bloccata tooa cluster, è una maggiore probabilità di esito positivo toofind liberare le risorse in quanto il pool di risorse disponibili hello è limitato tooa cluster. Inoltre, se la richiesta di allocazione è bloccata tooa cluster, ma il tipo di hello della risorsa richiesta non è supportato da tale cluster, la richiesta avrà esito negativo anche se dispone di cluster hello risorsa gratuita. Diagramma 3 riportato di seguito viene illustrato case hello in cui un'allocazione aggiunta non riesce perché non dispone di liberare le risorse cluster solo candidato hello. Figura 4 viene illustrata case hello in cui un'allocazione aggiunta non riesce perché non supporta i cluster candidato solo hello hello richiesto dimensioni delle macchine Virtuali, anche se sono presenti cluster hello liberare risorse.

![Errore di allocazione bloccata](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Risoluzione di problemi di allocazione non riuscita per i servizi cloud
### <a name="error-message"></a>Messaggio di errore
Si può vedere hello seguente messaggio di errore:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Problemi comuni
Di seguito sono hello allocazione scenari comuni che causano un'allocazione richiesta toobe bloccati tooa singolo cluster.

* La distribuzione tooStaging Slot - se un servizio cloud dispone di una distribuzione in uno slot, quindi hello intero servizio cloud è bloccato tooa specifico cluster.  Ciò significa che se una distribuzione già esiste nello slot di produzione hello, quindi una nuova distribuzione di gestione temporanea può solo essere allocata nella stessa cluster come slot di produzione hello hello. Se il cluster hello è quasi capacità, la richiesta hello potrebbe non riuscire.
* Scalabilità: aggiunta di nuove istanze tooan esistente-servizio cloud deve allocare in hello stesso cluster.  Le piccole richieste di ridimensionamento in genere possono essere allocate, ma non è sempre possibile. Se il cluster hello è quasi capacità, la richiesta hello potrebbe non riuscire.
* Gruppo di affinità - un nuovo servizio cloud vuoto tooan di distribuzione può essere allocato dall'infrastruttura di hello in un cluster in tale area, a meno che il servizio di cloud hello è il gruppo di affinità tooan bloccati. Le distribuzioni toohello verrà ritentato stesso gruppo di affinità hello dello stesso cluster. Se il cluster hello è quasi capacità, la richiesta hello potrebbe non riuscire.
* Gruppo di affinità di rete virtuale - reti virtuali precedenti sono stati collegati tooaffinity gruppi anziché aree e i servizi cloud in queste reti virtuali sarebbe toohello aggiunto gruppo di affinità cluster. Tentativo di tipo toothis le distribuzioni di rete virtuale nel cluster hello bloccato. Se il cluster hello è quasi capacità, la richiesta hello potrebbe non riuscire.

## <a name="solutions"></a>Soluzioni
1. Ridistribuzione tooa nuovo servizio cloud, questa soluzione è probabilmente toobe più efficace in quanto consente di hello piattaforma toochoose di tutti i cluster in tale area.

   * Distribuire il carico di lavoro hello tooa nuovo servizio cloud  
   * Aggiornare hello CNAME o un record toopoint traffico toohello nuovo servizio cloud
   * Una volta zero il traffico verrà toohello vecchio sito, è possibile eliminare il servizio cloud precedente di hello. Questa soluzione non deve causare tempi di inattività.
2. Eliminazione di produzione e gli slot di gestione temporanea: questa soluzione verrà mantenuto il nome DNS esistente, ma verrà applicazione tooyour tempi di inattività.

   * Eliminare la produzione hello e slot di un servizio cloud esistente di gestione temporanea in modo che il servizio di cloud hello è vuoto, quindi
   * Creare una nuova distribuzione nel servizio cloud esistente hello. Si tenterà nuovamente tooallocation in tutti i cluster in area hello. Assicurarsi di servizio cloud hello non è il gruppo di affinità collegati tooan.
3. Indirizzo IP riservato - questa soluzione consentirà di preservare l'IP esistenti indirizzo, ma verrà applicazione tooyour tempi di inattività.  

   * Creare un ReservedIP per la distribuzione esistente utilizzando Powershell

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Seguire #2 di sopra, rendendo toospecify che hello nuovo indirizzo IP riservato in CSCFG del servizio hello.
4. Rimuovere il gruppo di affinità per le nuove distribuzioni: i gruppi di affinità non sono più consigliati. Seguire i passaggi per #1 sopra toodeploy un nuovo servizio cloud. Assicurarsi che il servizio cloud non sia in un gruppo di affinità.
5. Convertire tooa internazionali rete virtuale, vedere la sezione [come toomigrate da gruppi di affinità tooa internazionali rete virtuale (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
