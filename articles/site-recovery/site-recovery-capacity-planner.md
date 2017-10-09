---
title: "capacità di replica aaaEstimate in Azure | Documenti Microsoft"
description: "Utilizzare questa capacità tooestimate articolo durante la replica con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Pianificare la capacità per la protezione delle macchine virtuali e dei server fisici in Azure Site Recovery

utilità di pianificazione della capacità di ripristino del sito Azure Hello consente di toofigure out i requisiti di capacità durante la replica delle macchine virtuali Hyper-V, le macchine virtuali VMware e server fisici Windows/Linux, con Azure Site Recovery.

Utilizzare hello tooanalyze di pianificazione della capacità di ripristino del sito, l'ambiente di origine e i carichi di lavoro, stimare le esigenze di larghezza di banda e le risorse del server che è necessario per il percorso di origine hello e hello risorse (macchine virtuali e archiviazione e così via), è necessario nella destinazione hello percorso.

È possibile eseguire lo strumento hello in due modi:

* **Pianificazione rapida**: lo strumento hello in questa modalità le proiezioni di rete e server tooget in base a un numero medio di macchine virtuali, dischi, archiviazione e frequenza di modifica.
* **Modalità di pianificazione**: eseguire lo strumento hello in questa modalità e fornire i dettagli di ogni carico di lavoro a livello di macchina virtuale. Analizzare la compatibilità della macchina virtuale e ottenere le proiezioni di rete e server.

## <a name="before-you-start"></a>Prima di iniziare


1. Raccogliere informazioni sull'ambiente, incluse le macchine virtuali, i dischi per ogni macchina virtuale e l'archiviazione per ogni disco.
2. Identificare la frequenza di modifica giornaliera (varianza) per i dati replicati. toodo questo:

   * Se si esegue la replica di macchine virtuali Hyper-V, quindi scaricare hello [strumento la pianificazione della capacità di Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) frequenza di modifica tooget hello. [Altre informazioni](site-recovery-capacity-planning-for-hyper-v-replication.md) su questo strumento. È consigliabile che eseguire questo strumento su un toocapture settimana medie.
   * Se si esegue la replica di macchine virtuali VMware, usare hello [pianificazione della distribuzione di ripristino del sito Azure](./site-recovery-deployment-planner.md) toofigure out hello varianza del tasso.
   * Se si esegue la replica di server fisici, è necessario tooestimate manualmente.

## <a name="run-hello-quick-planner"></a>Eseguire hello Planner rapido
1. Scaricare e aprire hello [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) strumento. Occorre toorun macro, pertanto selezionare tooenable la modifica e Abilita contenuto quando richiesto.
2. In **selezionare un tipo di pianificazione** selezionare **Planner rapido** dalla casella di riepilogo hello.

   ![introduttiva](./media/site-recovery-capacity-planner/getting-started.png)
3. In hello **Capacity Planner** foglio di lavoro, immettere le informazioni necessarie hello. È necessario inserire in tutti i campi di hello racchiuse in un cerchio rosso nella schermata di hello riportata di seguito.

   * In **selezionare lo scenario**, scegliere **Hyper-V tooAzure** o **tooAzure VMware/fisici**.
   * In **modifica dei dati giornalieri Media frequenza (%)**, inserire le informazioni di hello è raccogliere utilizzando hello [strumento la pianificazione della capacità di Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) o hello [pianificazione della distribuzione di ripristino di Azure sito](./site-recovery-deployment-planner.md).  
   * **Compressione** si applica solo a toocompression visualizzato quando si esegue la replica delle macchine virtuali VMware o tooAzure server fisici. Prevediamo 30% o più, ma è possibile modificare l'impostazione di hello come richiesto. Per la replica delle macchine virtuali Hyper-V tooAzure compressione, è possibile utilizzare uno strumento di terze parti, ad esempio Riverbed.
   * In **Retention Inputs** (Input per conservazione) specificare per quanto tempo devono essere conservate le repliche. Se si esegue la replica VMware o server fisico, specificare il valore di hello in giorni. Se si esegue la replica Hyper-V, specificare il tempo di hello in ore.
   * In **numero di ore in cui la replica iniziale per il batch di hello di macchine virtuali deve essere completata** e **numero di macchine virtuali per ogni batch di replica iniziale**, immesso le impostazioni utilizzate requisiti della replica iniziale toocompute.  Quando viene distribuito il ripristino del sito, è necessario caricare hello intero set di dati iniziale.

   ![Input](./media/site-recovery-capacity-planner/inputs.png)
4. Dopo aver inserire valori hello per ambiente di origine hello, l'output visualizzato include:

   * **Bandwidth required for delta replication** (Larghezza di banda necessaria per la replica differenziale), in megabit al secondo. Larghezza di banda di rete per la replica differenziale viene calcolata su hello medio giornaliero modifica dei dati.
   * **Bandwidth required for initial replication** (Larghezza di banda necessaria per la replica iniziale), in megabit al secondo. Larghezza di banda di rete per la replica iniziale viene calcolato in valori di replica iniziale hello che si inserisce nella.
   * **Spazio di archiviazione necessario (in GB)** è hello Azure spazio di archiviazione totale richiesto.
   * **Totale di IOPS per gli account di archiviazione standard** viene calcolato in base alle dimensioni dell'unità di IOPS per gli account di archiviazione standard totale hello 8 KB.  Per una pianificazione rapida hello, numero hello è calcolato in base tutti i dischi di macchine virtuali di origine hello e ogni giorno la frequenza di modifica dei dati. Per hello pianificazione dettagliata, il numero di hello è calcolato in base al numero totale di macchine virtuali che vengono mappate toostandard macchine virtuali di Azure e frequenza su tali macchine virtuali di modifica dei dati.
   * **Numero di account di archiviazione standard** fornisce numero totale di hello di archiviazione standard gli account necessari tooprotect macchine virtuali hello. Un account di archiviazione standard può contenere fino a too20000 IOPS tra tutte le macchine virtuali hello in un'archiviazione standard e sono supportati al massimo di 500 operazioni di IOPS per ogni disco.
   * **Numero di dischi blob necessario** offre hello numero di dischi che verranno create in archiviazione di Azure.
   * **Numero di account di archiviazione premium necessari** fornisce hello totale tooprotect Necessito account di archiviazione premium di macchine virtuali hello. Per una VM di origine con numero di operazioni di I/O al secondo elevato (superiore a 20000) è necessario un account di archiviazione premium. Un account di archiviazione premium può contenere fino too80000 IOPS.
   * **Totale di IOPS per archiviazione premium** viene calcolato in base alle dimensioni dell'unità di IOPS sugli account di archiviazione totale premium hello 256 KB.  Per una pianificazione rapida hello, numero hello è calcolato in base tutti i dischi di macchine virtuali di origine hello e ogni giorno la frequenza di modifica dei dati. Per hello Planner dettagliato, hello è hello in base a calcolato il numero complessivo di macchine virtuali che vengono mappate toopremium macchina virtuale di Azure (serie DS e GS) e modifica dei dati hello frequenza su tali macchine virtuali.
   * **Numero di server di configurazione necessari** Mostra il numero di server di configurazione è necessario per la distribuzione di hello.
   * **Numero di server di elaborazione aggiuntive necessarie** Mostra se i server di elaborazione aggiuntive sono necessari, nel server di elaborazione di toohello aggiunta è in esecuzione nel server di configurazione hello per impostazione predefinita.
   * **100% spazio di archiviazione aggiuntivo in origine hello** Mostra se ulteriore spazio di archiviazione è obbligatorio nel percorso di origine hello.

   ![Output](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Esecuzione hello Planner dettagliate

1. Scaricare e aprire hello [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) strumento. Occorre toorun macro, pertanto selezionare tooenable la modifica e Abilita contenuto quando richiesto.
2. In **selezionare un tipo di pianificazione**selezionare **Planner dettagliate** dalla casella di riepilogo hello.

   ![Introduzione](./media/site-recovery-capacity-planner/getting-started-2.png)
3. In hello **qualificazione del carico di lavoro** foglio di lavoro, immettere le informazioni necessarie hello. È necessario compilare hello tutti i campi contrassegnati.

   * In **core del processore**, specificare il numero totale di hello di core in un server di origine.
   * In **allocazione della memoria in MB**, specificare le dimensioni di hello RAM di un server di origine.
   * Hello **numero di schede di rete**, specificare il numero di hello di schede di rete in un server di origine.
   * In **totale di archiviazione (in GB)**, specificare hello dimensione totale di spazio di archiviazione VM hello. Ad esempio, se il server di origine hello contiene 3 dischi con 500 GB, spazio di archiviazione totale è 1500 GB.
   * In **numero di dischi collegati**, specificare il numero totale di hello dei dischi tra un server di origine.
   * In **l'utilizzo della capacità del disco**, specificare l'utilizzo medio hello.
   * In **quotidianamente modificare frequenza (%)**, specificare i dati giornalieri hello frequenza di modifica di un server di origine.
   * In **dimensioni Mapping Azure**, immettere le dimensioni di macchina virtuale di Azure hello che si desidera toomap. Se si desidera toodo manualmente questa operazione, fare clic su **calcolo delle macchine virtuali IaaS**. Se un'impostazione manuale di input e quindi fare clic su macchine virtuali IaaS di calcolo, impostazione manuale hello potrebbe essere sovrascritto perché il processo di calcolo hello identifica automaticamente una corrispondenza migliore di hello sulle dimensioni di macchina virtuale di Azure.

   ![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Se si sceglie **Compute IaaS VMs** , lo strumento esegue queste operazioni:

   * Convalida input obbligatorio hello.
   * Calcola IOPS e vengono suggerite alcune hello migliore macchina virtuale di Azure aize corrispondenza per ogni VM è idoneo per la replica tooAzure. Se non viene trovata una macchina virtuale di Azure della dimensione appropriata viene visualizzato un errore. Ad esempio, se il numero di hello di dischi collegati 65, viene generato un errore perché la dimensione massima hello macchina virtuale di Azure è 64.
   * Suggerisce un account di archiviazione da usare per una macchina virtuale di Azure.
   * Calcola hello il numero totale di account di archiviazione standard e gli account di archiviazione premium necessari per il carico di lavoro di hello. Scorrere verso il basso hello tooview il tipo di archiviazione di Azure e account di archiviazione hello che può essere usato per un server di origine.
   * Completa e Ordina rest hello della tabella hello in base al tipo di archiviazione necessaria (standard o premium) assegnato per una macchina virtuale e il numero di hello di dischi collegati. Per tutte le macchine virtuali che soddisfano i requisiti di hello per Azure hello colonna **VM è qualificato?** Mostra **Sì**. Se una macchina virtuale non è possibile eseguire il backup tooAzure, viene visualizzato un errore.

Colonne AA tooAE sono output e forniscono informazioni per ogni macchina virtuale.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Esempio
Ad esempio, per le macchine virtuali di sei valori hello illustrato nella tabella di hello, strumento hello calcola e assegna hello migliore corrispondenza di macchina virtuale di Azure e i requisiti di archiviazione di Azure hello.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Nell'output di esempio hello, tenere presente i seguenti hello:

  * Hello prima colonna è una colonna di convalida per le macchine virtuali hello, dischi e varianza.
  * Per cinque macchine virtuali sono necessari due account di archiviazione standard e un account di archiviazione premium.
  * La VM3 non è idonea alla protezione perché uno o più dischi sono superiori a 1 TB.
  * VM1 e VM2 possono utilizzare l'account di archiviazione standard prima hello
  * VM4 è possibile utilizzare account di archiviazione standard secondo hello.
  * Per la VM5 e la VM6 è necessario un account di archiviazione premium ed entrambe possono usare un singolo account.

    > [!NOTE]
    > IOPS di archiviazione standard e premium vengono calcolati a hello livello macchina virtuale e non a livello di disco. Una macchina virtuale standard in grado di gestire backup too500 di IOPS per disco. Se le operazioni di I/O al secondo per disco sono superiori a 500, è necessaria l'archiviazione premium. Tuttavia, se IOPS per un disco più di 500, ma IOPS per i dischi di macchina virtuale totali hello sono all'interno di hello standard (dimensioni di macchina virtuale, numero di dischi, numero di memoria di schede di rete, CPU,), i limiti di macchina virtuale di Azure supportano planner hello sceglie una serie standard macchina virtuale e non hello DS o GS. È necessario cella di dimensioni di Azure di mapping di hello aggiornamento toomanually con appropriate serie DS o GS VM.


Dopo che tutti i dettagli di hello siano soddisfatti, fare clic su **dello strumento di pianificazione di inviare dati toohello** tooopen hello **Capacity Planner** carichi di lavoro evidenziato, tooshow se si idonei per la protezione o non.

### <a name="submit-data-in-hello-capacity-planner"></a>Inviare i dati di hello Capacity Planner
1. Quando si apre hello **Capacity Planner** foglio di lavoro viene compilata in base alle impostazioni di hello è stato specificato. Hello word 'carico di lavoro viene visualizzato in hello **origine di input Infra** cella, tooshow che hello input è hello **qualificazione del carico di lavoro** foglio di lavoro.
2. Se si desidera toomake modifiche, è necessario hello toomodify **qualificazione del carico di lavoro** foglio di lavoro e fare clic su **dello strumento di pianificazione di inviare dati toohello** nuovamente.  

   ![Capacity Planner](./media/site-recovery-capacity-planner/capacity-planner.png)
