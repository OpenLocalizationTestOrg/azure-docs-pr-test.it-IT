---
title: il riavvio di manutenzione per le macchine virtuali Linux in Azure aaaVM | Documenti Microsoft
description: Riavvio per manutenzione delle macchine virtuali Linux.
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a>Riavvio per manutenzione delle macchine virtuali

Vi sono alcuni casi in cui le macchine virtuali vengono riavviate a causa di tooplanned toohello di manutenzione dell'infrastruttura sottostante. Essendo toothe ripercussioni sulle disponibilità delle macchine virtuali ospitate in Azure, seguente hello sono ora disponibili per toouse è:

-   Notifica inviata almeno 30 giorni prima dell'impatto di hello.

-   Visibilità toohello le finestre di manutenzione per ogni macchina virtuale.

-   Flessibilità e controllo nell'impostazione hello ora esatta per la manutenzione delle macchine virtuali abbiano un impatto.

Le operazioni di manutenzione in Microsoft Azure sono pianificate secondo iterazioni. Le iterazioni iniziali hanno un ambito più ridotto in ordine tooreduce hello rischio nell'implementazione della funzionalità e nuove correzioni. Le iterazioni successive possono estendersi su più aree (non da hello stessa coppia di area). Una macchina virtuale è inclusa in una singola iterazione di manutenzione. Se un'iterazione viene interrotta, le macchine virtuali rimanenti verranno incluse in un'altra interazione successiva.

manutenzione pianificata iterazione Hello ha due fasi: la finestra di manutenzione Pre-emptive e una finestra di manutenzione pianificata.

Hello **finestra di manutenzione Pre-emptive** fornisce hello flessibilità tooinitiate hello la manutenzione delle macchine virtuali. In questo modo, è possibile determinare quando le macchine virtuali sono influenzate, hello sequenza di aggiornamento hello e hello tempo tra ogni macchina virtuale viene mantenuta. È possibile richiedere toosee ogni macchina virtuale se è prevista per la manutenzione e verificare il risultato di hello dell'ultima richiesta di manutenzione avviata.

Hello **finestra di manutenzione pianificata** è al momento le macchine virtuali per la manutenzione hello Azure. Durante questo intervallo di tempo che segue la finestra di manutenzione preventiva, è possibile comunque una query per la finestra di manutenzione hello, ma non essere più in grado di tooorchestrate manutenzione di hello.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerazioni sulla disponibilità durante la manutenzione pianificata 

### <a name="paired-regions"></a>Aree abbinate

Ogni area di Azure è associato a un'altra area all'interno di hello stesso geografia, rendendo insieme una coppia internazionale. Quando si esegue la manutenzione, Azure aggiornerà solo le istanze di macchine virtuali hello in una singola area della coppia. Ad esempio, quando si aggiorna hello macchine virtuali in North Central US, Azure non aggiornerà tutte le macchine virtuali nel centro-meridionali in hello contemporaneamente. Questa operazione viene pianificata in un secondo momento, consentendo il failover o il bilanciamento del carico tra le aree. Tuttavia, le altre aree, ad esempio Europa settentrionale può essere in fase di manutenzione in hello stesso tempo come Stati Uniti orientali.
Leggere altre informazioni sulle [coppie di aree di Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Macchine virtuali a istanza singola e set di disponibilità o set di scalabilità di una macchina virtuale

Quando si distribuisce un carico di lavoro di macchine virtuali in Azure, è possibile creare hello macchine virtuali all'interno di un set di disponibilità in applicazione tooyour tooprovide la disponibilità elevata. Questa configurazione assicura che in caso di interruzione o di eventi di manutenzione sia disponibile almeno una macchina virtuale.

All'interno di un set di disponibilità, singole macchine virtuali vengono distribuite tra i domini di aggiornamento too20. Durante la manutenzione pianificata, l'impatto prodotto interessa un solo dominio di aggiornamento in un dato momento ordine di Hello di domini di aggiornamento influenzate non possono essere eseguite in sequenza durante la manutenzione pianificata. Per una singola istanza macchine virtuali (non fa parte del gruppo di disponibilità), non è disponibile alcun toopredict modo o determinare quali e quante macchine virtuali sono interessate insieme.

Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure che consente di toodeploy e gestire un set di macchine virtuali identiche come una singola risorsa.
set di scalabilità Hello fornisce garanzie simili tooan set di disponibilità in forma di domini di aggiornamento. 

Per ulteriori informazioni sulla configurazione delle macchine virtuali per la disponibilità elevata, vedere [ *gestione hello disponibilità delle macchine virtuali Windows*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Eventi pianificati

Azure Metadata Service consente toodiscover informazioni della macchina virtuale ospitata in Azure. Gli eventi, una delle categorie di hello esposto, informazioni di aree relative a eventi pianificati (ad esempio, riavviare il computer) in modo che l'applicazione può preparare la transizione e limitare le interruzioni.

Per ulteriori informazioni sugli eventi pianificati, fare riferimento troppo[servizio metadati di Azure - eventi pianificati](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Individuazione degli interventi di manutenzione e notifiche

Pianificazione di manutenzione è toocustomers visibile a livello di hello di singole macchine virtuali. È possibile utilizzare Azure portal, tooquery CLI, PowerShell o API per le finestre di manutenzione preventiva e pianificato. Inoltre, prevede di ricevere una notifica (posta elettronica) in caso di hello in cui uno o più di macchine virtuali sono interessati durante il processo di hello.

Entrambe le fasi di manutenzione, preventiva e pianificata, iniziano con una notifica. Prevedere tooreceive una singola notifica per ogni sottoscrizione di Azure. notifica Hello viene inviata toohello della sottoscrizione e co-amministratore per impostazione predefinita. È inoltre possibile configurare destinatari hello per la notifica di manutenzione.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Finestra di manutenzione hello visualizzazione nel portale di hello 

È possibile utilizzare hello portale di Azure e cercare le macchine virtuali pianificate per la manutenzione.

1.  Accedi toohello portale di Azure.

2.  Fare clic e aprire hello **macchine virtuali** blade.

3.  Fare clic su hello **colonne** pulsante tooopen hello elenco colonne disponibili toochoose da

4.  Selezionare e aggiungere hello **finestra di manutenzione** colonne. Le macchine virtuali che sono pianificate per la manutenzione sono rese disponibili le finestre di manutenzione hello. Quando la manutenzione viene completata o interrotta, la finestra di manutenzione non è più visibile.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Dettagli di manutenzione della query utilizzando hello API di Azure

Hello utilizzare [ottenere le informazioni di VM API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) e cercare hello istanza toodiscover hello manutenzione dettagli su una macchina virtuale di singoli. risposta Hello include hello seguenti elementi:

  - isCustomerInitiatedMaintenanceAllowed: indica se preventiva ridistribuzione in hello VM ora è possibile avviare.

  - preMaintenanceWindowStartTime: hello ora di inizio della finestra di manutenzione preventiva hello.

  - preMaintenanceWindowEndTime: hello ora di fine della finestra di manutenzione preventiva hello. Trascorso questo periodo, non sarà non è più in grado di tooinitiate manutenzione in questa macchina virtuale.
    
  - maintenanceWindowStartTime: hello ora di inizio della finestra di manutenzione pianificata di hello quando la macchina virtuale sono interessati.

  - maintenanceWindowEndTime: hello ora di fine della finestra di manutenzione pianificata hello.
  
  - lastOperationResultCode: hello risultato dell'ultima operazione ridistribuzione di manutenzione.
 
  - lastOperationMessage: messaggio che descrive i risultati di hello dell'ultima operazione di ridistribuzione di manutenzione.


## <a name="pre-emptive-redeploy"></a>Ridistribuzione preventiva

Azione preventiva Ridistribuisci fornisce hello flessibilità toocontrol hello ora manutenzione tooyour applicato macchine virtuali in Azure. Manutenzione pianificata inizia con una finestra di manutenzione preventiva in cui è possibile ora esatta di hello per ognuna delle toobe macchine virtuali riavviato. Di seguito sono indicati i casi di uso in cui tale funzionalità è utile:

-   Manutenzione necessità toobe coordinato con utenti finali di hello.

-   finestra di manutenzione pianificata Hello offerto da Azure non è sufficiente.
    È possibile che la finestra hello accade toobe puntualmente più movimentato hello, della settimana o è troppo lungo.

-   Per multi-istanza o le applicazioni a più livelli, è necessario un tempo sufficiente tra due macchine virtuali o di un determinato toofollow sequenza.

Quando si chiama per ridistribuire preventiva in una macchina virtuale, sposta hello VM tooan già aggiornato nodo e quindi viene acceso, nuovo, mantenendo tutte le opzioni di configurazione e le risorse associate. Durante questa operazione, disco temporaneo hello viene perso e gli indirizzi IP dinamici associati vengono aggiornati l'interfaccia di rete virtuale.

La ridistribuzione preventiva viene abilitata una sola volta per ogni macchina virtuale. Se si verifica un errore durante il processo di hello, hello operazione viene interrotta, hello VM non è compromessa e viene escluso dall'iterazione manutenzione hello pianificato. Si verrà contattati in un secondo momento con una nuova pianificazione e disponibile un nuova opportunità tooschedule e sequenza hello impatto sulle macchine virtuali.
