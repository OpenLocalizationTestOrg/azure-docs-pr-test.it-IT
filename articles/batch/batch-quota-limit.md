---
title: aaaService quote e limiti per il Batch di Azure | Documenti Microsoft
description: Informazioni sulle quote di Azure Batch predefinito, i limiti e i vincoli e come aumentare il livello toorequest quota
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Quote e limiti del servizio Batch

Come con altri servizi di Azure, vi sono limiti di determinate risorse associate hello servizio Batch. Molti di questi limiti sono le quote predefinite applicate da Azure a livello di account o sottoscrizione hello. Questo articolo illustra i valori predefiniti e come è possibile richiedere aumenti di quota.

Tenere presenti queste quote quando si progettano i carichi di lavoro di Batch e se ne aumentano le prestazioni. Ad esempio, se il pool non è raggiunto il numero di destinazione hello dei nodi di calcolo che è stato specificato, potrebbe aver raggiunto limite di quota di core hello per l'account Batch o una quota di core VM internazionale per la sottoscrizione.

È possibile eseguire i carichi di lavoro di più Batch in un singolo account di Batch o distribuire i carichi di lavoro tra gli account Batch in hello stessa sottoscrizione, ma in diverse aree di Azure.

Se si prevede di toorun i carichi di lavoro in Batch, si potrebbe essere necessario tooincrease uno o più quote hello sopra predefinito hello. Se si desidera tooraise una quota, è possibile aprire in linea [richiesta di supporto clienti](#increase-a-quota) senza alcun costo.

> [!NOTE]
> Una quota è un limite di credito, non una garanzia di capacità. Se si hanno esigenze di capacità su larga scala, contattare il supporto di Azure.
> 
> 

## <a name="resource-quotas"></a>Quote di risorse
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Quote in modalità di sottoscrizione utente

Per un account Batch in modalità di allocazione del pool di troppo**sottoscrizione utente**, Batch macchine virtuali e altre risorse, quali gli account di archiviazione, vengono creati direttamente nella sottoscrizione quando viene creato un pool. quota di core Hello Azure Batch non è applicabile tooan account creato in questa modalità. Al contrario, vengono applicate le quote di hello nella sottoscrizione per core di calcolo locali e altre risorse. Per altre informazioni su tali quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).

Quando si pianifica l'utilizzo delle risorse per un account creato in modalità di sottoscrizione utente, sono necessarie per ogni 40 le macchine virtuali Linux, o 20 macchine virtuali di Windows hello nota seguente risorse Batch (in core toocompute aggiunta):

| Risorsa | Quota | Provider |
| --- | ---| --- |
| Un account di archiviazione | Account di archiviazione | Microsoft.Storage |
| Un indirizzo IP pubblico | Indirizzi IP pubblici | Microsoft.Network | 
| Una rete virtuale | Reti virtuali | Microsoft.Network | 
| Un gruppo di sicurezza di rete | Gruppi di sicurezza di rete | Microsoft.Network | 
| Un set di scalabilità di macchine virtuali | Set di scalabilità di macchine virtuali | Microsoft.Compute | 
| Un bilanciamento del carico | Servizi di bilanciamento del carico | Microsoft.Network | 

quota di core Hello livello regionale o per ogni famiglia di macchina virtuale deve essere set in base toohello dimensioni delle macchine Virtuali necessarie per il pool di Batch o il pool:

| Quota | Provider |
| --- | ---- |
| Totale core regionali | Microsoft.Compute |
| … Core a livello di famiglia | Microsoft.Compute |



## <a name="other-limits"></a>Altri limiti
| **Risorsa** | **Limite massimo** |
| --- | --- |
| [Attività simultanee](batch-parallel-node-tasks.md) per nodo di calcolo |4 x numero di core del nodo |
| [Applicazioni](batch-application-packages.md) per account Batch |20 |
| Pacchetti dell'applicazione per applicazione |40 |
| Dimensioni del pacchetto dell'applicazione (ciascuno) |Circa 195 GB<sup>1</sup> |
| Dimensione massima dell'attività di avvio | 32768 caratteri<sup>2</sup> |

<sup>1</sup> Limite di archiviazione di Azure per le dimensioni massime del BLOB in blocchi<br />
<sup>2</sup> include i file di risorse e le variabili di ambiente

## <a name="view-batch-quotas"></a>Visualizzare le quote Batch
Visualizzare le quote di account di Batch in hello [portale di Azure][portal].

1. Selezionare **Batch account** nel portale di hello, quindi selezionare account di Batch hello si è interessati.
2. Selezionare **proprietà** nel Pannello di menu dell'account Batch hello.
3. Pannello proprietà Hello Visualizza hello **quote** attualmente applicato account Batch toohello
   
    ![Quote di account Batch][account_quotas]

Per un account Batch è stato creato in modalità di sottoscrizione utente, hello Vista correlate le quote della sottoscrizione nel portale di Azure hello.

1. Selezionare **sottoscrizioni**e selezionare hello sottoscrizione in uso per hello account Batch.

2. In hello **sottoscrizione** pannello seleziona **utilizzo + quote**.



## <a name="increase-a-quota"></a>Aumentare una quota
Seguire questi toorequest passaggi aumentare di una quota per l'account Batch o la sottoscrizione utilizzando hello [portale di Azure][portal]. tipo di Hello di aumento della quota dipende dalla modalità di allocazione del pool di hello dell'account di Batch.

### <a name="increase-a-batch-cores-quota"></a>Aumentare una quota di core Batch 

Se l'account Batch è stato creato **Batch servizio** modalità, seguire questi toorequest passaggi un aumento della quota core Batch:

1. Seleziona hello **Guida e supporto** riquadro nel dashboard del portale o hello punto interrogativo (**?**) nell'angolo superiore destro di hello del portale hello.
2. Selezionare **Nuova richiesta di supporto** > **Informazioni di base**.
3. In hello **nozioni di base** pannello:
   
    a. **Tipo di problema** > **Quota**
   
    b. Selezionare la propria sottoscrizione.
   
    c. **Tipo di quota** > **Batch**
   
    d. **Piano di supporto** > **Supporto per la quota - Incluso**
   
    Fare clic su **Avanti**.
4. In hello **problema** pannello:
   
    a. Selezionare un **gravità** in base tooyour [impatto aziendale][support_sev].
   
    b. In **dettagli**, specificare ogni quota si desidera toochange, nome dell'account Batch hello e hello nuovo limite.
   
    Fare clic su **Avanti**.
5. In hello **le informazioni di contatto** pannello:
   
    a. Selezionare il **metodo di contatto preferito**.
   
    b. Verificare e immettere i dettagli di contatto hello necessario.
   
    Fare clic su **crea** toosubmit hello richiesta di supporto.

Dopo aver inviato la richiesta di supporto, si verrà contattati dal supporto tecnico di Azure. Nota: completamento hello richiesta può richiedere giorni lavorativi too2.

### <a name="increase-a-subscription-cores-quota"></a>Aumentare la quota di core della sottoscrizione

Se l'account Batch è stato creato in modalità di **sottoscrizione utente** ed è necessario disporre di core regionali o a livello di famiglia, richiedere un aumento di quote per la sottoscrizione. Per istruzioni, vedere [Richieste di aumento della quota di core per Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Argomenti correlati
* [Creare un account Azure Batch utilizzando hello portale di Azure](batch-account-create-portal.md)
* [Cenni preliminari sulla funzionalità Azure Batch](batch-api-basics.md)
* [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
