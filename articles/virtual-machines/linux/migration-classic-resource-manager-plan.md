---
title: aaaPlanning per la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico | Documenti Microsoft
description: Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico
Gestione risorse di Azure offre molte funzionalità straordinarie, ma è critico tooplan out il toomake proprio processo di migrazione cose che avvengano in maniera fluida. Dedicare tempo alla pianificazione garantisce che non si verifichino problemi durante l'esecuzione delle attività di migrazione. 

> [!NOTE] 
> Hello istruzioni disponibili è stata ampiamente contributo tooby hello Azure Customer Advisory team e architetti di soluzioni di Cloud lavorando con clienti migrazione enviornments di grandi dimensioni. Di conseguenza il documento continuerà tooget aggiornato come emerge nuovi modelli di successo, dal tempo tootime toosee verificare se sono presenti eventuali nuove indicazioni.

Esistono quattro fasi generali del proprio processo di migrazione hello:

![Fasi di migrazione](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Pianificare

### <a name="technical-considerations-and-tradeoffs"></a>Considerazioni tecniche e compromessi

A seconda dei dimensioni requisiti tecnici aree geografiche e procedure operative, è possibile tooconsider:

1. Perché si vuole usare Azure Resource Manager per l'organizzazione?  Quali sono i motivi aziendali hello per la migrazione?
2. Quali sono i motivi tecnici hello per Gestione risorse di Azure?  Novità (se presente) servizi di Azure aggiuntivi si sarebbe ad esempio tooleverage?
3. Quale applicazione (o set di macchine virtuali) è incluso nella migrazione hello?
4. Quali scenari sono supportati con la migrazione di hello API?  Hello revisione [non supportate funzionalità e configurazioni](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations).
5. I team operativi supporteranno le applicazioni/macchine virtuali sia nel modello di distribuzione classica che in Azure Resource Manager?
6. Come cambieranno eventualmente i processi di distribuzione, gestione, monitoraggio e report delle VM con Azure Resource Manager?  Gli script di distribuzione necessario toobe aggiornato?
7. Che cos'è comunicazioni hello prevede le parti interessate tooalert (gli utenti finali, i proprietari delle applicazioni e proprietari dell'infrastruttura)?
8. A seconda della complessità hello dell'ambiente di hello, dovrebbe esserci un periodo di manutenzione in cui un'applicazione hello è disponibile tooend utenti e i proprietari di tooapplication?  In questo caso, per quanto tempo?
9. Che cos'è le parti interessate tooensure piano di formazione hello sono esperti ed esperienza nell'utilizzo di gestione risorse di Azure?
10. Che cos'è gestione programma hello o piano di gestione di progetto per la migrazione di hello?
11. Quali sono le sequenze temporali hello per la migrazione di Azure Resource Manager hello e altri relative tecnologie?  Sono allineati in modo ottimale?

### <a name="patterns-of-success"></a>Modelli di successo

I clienti di esito positivo disporre dettagliati piani in hello sopra domande vengono discussi, documentati e governato.  Verificare i piani di migrazione hello siano toosponsors comunicate su vasta scala e le parti interessate.  Acquisire familiarità con le opzioni di migrazione; è consigliabile leggere i documenti sulla migrazione qui di seguito.

* [Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utilizzare le risorse IaaS toomigrate PowerShell da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utilizzare le risorse IaaS toomigrate CLI da Gestione risorse di tooAzure classico](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rivedere gli errori di migrazione più comuni](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Risoluzione dei problemi tooavoid

- Errore tooplan.  passaggi per la tecnologia Hello questa migrazione sono rivelati e risultato hello è prevedibile.
- Presupponendo che hello API migrazione piattaforma supportata verrà tenuto in considerazione tutti gli scenari. Hello lettura [non supportate funzionalità e configurazioni](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand gli scenari supportati.
- Nessuna pianificazione di potenziali interruzioni delle applicazioni per gli utenti finali.  Pianificare i buffer insufficiente tooadequately avvisa gli utenti finali del tempo applicazione potenzialmente non disponibile.


## <a name="lab-test"></a>Test di laboratorio 

**Replicare l'ambiente ed eseguire una migrazione di test**
  > [!NOTE]
  > La replica esatta dell'ambiente esistente viene eseguita tramite uno strumento creato dalla community che non è ufficialmente supportato dal supporto tecnico Microsoft. È pertanto un **facoltativo** passaggio ma è toofind modo migliore di hello problemi senza modificare gli ambienti di produzione. Se uno strumento con il contributo della community non è un'opzione, quindi informazioni su come hello esecuzione Prepare/convalida/interruzione indicazione riportata di seguito.
  >
  
  Esecuzione di un lab di testing del proprio scenario esatto (calcolo, rete e archiviazione) è hello migliore modo tooensure una facile migrazione. In modo da garantire:

  - Un laboratorio interamente separato o un tootest ambiente non di produzione esistente. È consigliabile un laboratorio totalmente separato che possa essere migrato ripetutamente e modificato in modo distruttivo.  Script toocollect/idrato metadati dalle sottoscrizioni reale hello sono elencati di seguito.
  - Si tratta di un lab di hello buona toocreate in una sottoscrizione separata. Hello motivo è che lab hello verrà eliminata ripetutamente verso il basso e di un oggetto separato, sottoscrizione di tipo isolato ridurrà il possibilità hello che qualcosa reale otterranno accidentalmente eliminato.

  Questo può essere eseguito tramite lo strumento AsmMetadataParser hello. [Per altre informazioni su questo strumento vedere qui](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Modelli di successo

esempio Hello è i problemi individuati in molte delle migrazioni maggiore hello. Si tratta di un elenco completo e si deve fare riferimento toohello [non supportate funzionalità e configurazioni](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) per ulteriori dettagli. Questi problemi tecnici potrebbero anche non verificarsi, ma se vengono risolti prima della migrazione, questa sarà più semplice.

- **Eseguire una convalida/preparazione/Abort esecuzione** -questo è probabilmente hello più importante passaggio tooensure classica tooAzure Gestione risorse corretta esecuzione della migrazione. migrazione di Hello API dispone di tre passaggi principali: convalidare, preparazione e Commit. La convalida verrà leggere hello lo stato dell'ambiente classico e restituiscono un risultato di tutti i problemi. Tuttavia, poiché alcuni problemi possono esistere nello stack di Azure Resource Manager hello, convalida non rileverà tutti gli elementi. Hello passaggio successivo nel processo di migrazione preparazione consente di esporre tali problemi. Preparare verrà spostare hello i metadati da classica tooAzure Gestione risorse, ma verrà non commit hello spostamento e non rimuovere o modificare qualsiasi elemento sul lato classica hello. Hello consiste nel preparare la migrazione di hello, quindi l'interruzione (**non eseguire il commit**) preparare la migrazione di hello. obiettivo di Hello di esecuzione convalidare/preparare/abort è toosee tutti i metadati di hello nello stack di gestione risorse di Azure hello, esaminarlo (*a livello di codice o nel portale*), verificare che tutto ciò che viene eseguita la migrazione correttamente e di lavoro tramite problemi tecnici.  Inoltre si avrà un'idea della durata della migrazione in modo che sia possibile pianificare di conseguenza i tempi di inattività.  Convalida/preparare/interruzione di una non provoca alcun tempo di inattività utente; Pertanto, è l'uso di tooapplication non comportano interruzioni del servizio.
  - elementi Hello seguenti saranno necessario risolvere prima esecuzione hello toobe, ma un test di esecuzione eliminerà anche in modo sicuro i questi passaggi di preparazione se essi vengono persi. Durante la migrazione dell'organizzazione, è stata trovata la preparazione della migrazione tooensure un metodo estremamente utile e sicuro hello toobe di esecuzione.
  - Preparare quando è in esecuzione, il controllo hello piano (operazioni di gestione di Azure) verrà bloccato per la rete virtuale intero hello, pertanto non è possibile apportare modifiche tooVM metadati durante la convalida/preparare/abort.  A parte questo, tutte le funzioni delle applicazioni, ad esempio l'uso del desktop remoto, le macchine virtuali e così via, non saranno interessate.  Gli utenti delle macchine virtuali di hello non riconoscerà che esecuzione hello è in esecuzione.

- **Circuiti ExpressRoute e VPN**. I gateway ExpressRoute con collegamenti di autorizzazione attualmente non possono essere migrati senza tempi di inattività. Per risolvere il problema hello, vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Le estensioni VM** -estensioni delle macchine virtuali sono potenzialmente uno dei toomigrating gli ostacoli principali hello macchine virtuali in esecuzione. Pianificare tenendo conto che la correzione delle estensioni VM potrebbe richiedere fino a 1-2 giorni.  Un agente di Azure di lavoro stato necessari tooreport indietro estensione della macchina virtuale di macchine virtuali in esecuzione. Se lo stato di hello vengono restituiti come non valido per una macchina virtuale in esecuzione, questo verrà interrotto la migrazione. agente Hello stesso non necessario toobe nella migrazione tooenable funzioni correttamente, ma se esistono estensioni su hello macchina virtuale, quindi entrambe un agente di lavoro e la connettività internet in uscita (con DNS) necessarie per la migrazione toomove in avanti.
  - Se il server DNS di connettività tooa viene persa durante la migrazione, tutte le estensioni VM tranne BGInfo v1. \* necessario toofirst rimossa ogni macchina virtuale prima di preparare la migrazione e successivamente riaggiunto toohello indietro VM dopo la migrazione di gestione risorse di Azure.  **Questo vale solo per le VM in esecuzione.**  Se le macchine virtuali hello viene arrestato deallocata, estensioni di macchina virtuale non è necessario toobe rimosso. **Nota:** molte estensioni come la diagnostica Azure e il monitoraggio del centro sicurezza si reinstalleranno automaticamente dopo la migrazione, per cui la loro rimozione non è un problema.
  - Assicurarsi inoltre che non ci siano Gruppi di sicurezza di rete che limitano l'accesso Internet in uscita. Questa situazione può verificarsi con alcune configurazioni di Gruppi di sicurezza di rete. Accesso a internet in uscita (e DNS) è necessaria per le estensioni VM toobe migrati tooAzure Gestione risorse. 
  - Sono disponibili due versioni dell'estensione BGInfo hello: v1 e v2.  Se hello VM è stato creato tramite portale classico hello o PowerShell, hello VM probabilmente avrà estensione v1 hello su di esso. Questa estensione non è necessario toobe rimosso e verrà ignorata (non migrati) dalla migrazione hello API. Tuttavia, se hello Classic VM è stato creato con nuovo portale di Azure hello, probabilmente avrà versione hello v2 basata su JSON di BGInfo, che può essere migrato tooAzure Gestione risorse fornite agente hello funzioni e ha accesso a internet in uscita (e DNS). 
  - **Opzione di correzione 1**. Se si conoscono che le macchine virtuali non avrà internet in uscita, accedere, un servizio DNS funzionante e utilizzano gli agenti di Azure nelle macchine virtuali di hello, quindi disinstallare tutte le estensioni di macchina virtuale come parte della migrazione hello prima di preparare, quindi reinstallare le estensioni VM hello dopo la migrazione. 
  - **Opzione di correzione 2**. Se le estensioni VM sono troppo grandi di un ostacolo, un'altra opzione è tooshutdown/deallocare tutte le macchine virtuali prima della migrazione. Eseguire la migrazione di hello deallocato macchine virtuali, quindi riavviarli su hello lato Azure Resource Manager. Hello vantaggio consiste nel fatto che le estensioni VM verranno eseguita la migrazione. Hello svantaggio è che gli indirizzi IP virtuali pubblici di tutti i andranno persi (potrebbe essere un non-starter,) e ovviamente hello macchine virtuali verrà arrestato causando un molto maggiore impatto sulle applicazioni di lavoro.

    > [!NOTE] 
    > Se viene configurato un criterio di Centro sicurezza di Azure in esecuzione macchine virtuali viene eseguita la migrazione di hello, i criteri di sicurezza hello devono toobe arrestato prima di rimuovere le estensioni, in caso contrario sicurezza hello estensione monitoraggio verrà reinstallato automaticamente in hello VM dopo la rimozione.

- **Set di disponibilità** : per una rete virtuale (vNet) di toobe tooAzure Gestione risorse di migrazione, hello Classic macchine virtuali di distribuzione (ad esempio il servizio cloud) contenuta deve essere tutti in un set di disponibilità o le macchine virtuali hello tutti non deve essere in qualsiasi set di disponibilità. Presenza di più di un set di disponibilità in servizio cloud hello non è compatibile con Gestione risorse di Azure e verrà interrotta la migrazione.  Non ci possono essere inoltre alcune macchine virtuali in un set di disponibilità e alcune macchine virtuali non in un set di disponibilità. tooresolve, si sarà necessario tooremediate o riassegnare il servizio cloud.  Pianificare di conseguenza, in quanto questa operazione potrebbe richiedere molto tempo. 

- **Le distribuzioni di ruoli Web/di lavoro** -servizi Cloud che contiene i ruoli web e di lavoro non è possibile eseguire la migrazione tooAzure Gestione risorse. i ruoli web/di lavoro di Hello, è necessario rimuovere dalla rete virtuale hello prima di poter avviare la migrazione.  Una tipica soluzione è toojust spostamento web/di lavoro ruolo istanze tooa separato classica rete virtuale che è anche un circuito ExpressRoute tooan collegato o toomigrate hello codice toonewer App Services PaaS (questa discussione esula dall'ambito di hello di questo documento). Nel primo hello ridistribuire case, creare una nuova rete virtuale classica, spostamento o ridistribuire hello web/di lavoro ruoli toothat nuova rete virtuale, quindi eliminare le distribuzioni di hello dalla rete virtuale di hello viene spostato. Non è necessaria alcuna modifica nel codice. nuovo Hello [Peering di rete virtuale](../../virtual-network/virtual-network-peering-overview.md) funzionalità può essere utilizzato toopeer hello insieme classico rete virtuale che contiene i ruoli web/di lavoro hello e altre reti virtuali in hello stessa area di Azure, ad esempio da rete virtuale hello eseguire la migrazione (**dopo la migrazione della rete virtuale è completata, poiché il peering reti virtuali non possono essere migrate**), fornendo funzionalità stesso hello con senza perdita di prestazioni e non sanzioni/latenza della larghezza di banda. Data aggiunta hello di [Peering di rete virtuale](../../virtual-network/virtual-network-peering-overview.md), le distribuzioni di ruoli web/di lavoro ora può facilmente essere ridotti e non bloccati hello migrazione tooAzure Gestione risorse.

- **Le quote di Azure Resource Manager** - Le aree di Azure hanno di quote/limiti separati per il modello di distribuzione classica e per Azure Resource Manager. Anche se in uno scenario di migrazione non è utilizzata nuovo hardware *(ci stiamo swapping macchine virtuali esistenti da classica tooAzure Gestione risorse)*, le quote di gestione risorse di Azure è comunque necessario toobe sul posto con una capacità sufficiente prima di Avvia la migrazione. Di seguito sono elencati i limiti di hello principali che abbiamo visto causano problemi.  Aprire un hello di tooraise ticket di supporto quota limita. 

    > [!NOTE]
    > Questi limiti necessario toobe generato in hello stessa area, come la migrazione del toobe ambiente corrente.
    >

    - Interfacce di rete
    - Servizi di bilanciamento del carico
    - Indirizzi IP pubblici
    - Indirizzi IP pubblici statici
    - Core
    - Gruppi di sicurezza di rete
    - Tabelle di route

    È possibile controllare le quote di gestione risorse di Azure corrente utilizzando hello seguendo i comandi con hello versione 2.0 di CLI di Azure.

    **Calcolo** *(memoria centrale, set di disponibilità)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **Rete***(reti virtuali, indirizzi IP statici, indirizzi IP pubblici, gruppi di sicurezza di rete, interfacce di rete, bilanciamenti del carico, tabelle route)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **Risorsa di archiviazione** *(account di archiviazione)*
    
    ```bash
    az storage account show-usage
    ```

- **Limitazioni dell'API di Azure Resource Manager** - In presenza di un ambiente sufficientemente grande, ad esempio, > 400 macchine virtuali in una rete virtuale), si potrebbe raggiunge hello predefinito API limitazioni per operazioni di scrittura (attualmente **1200 operazioni di scrittura/ora**) in Gestione risorse di Azure. Prima di iniziare la migrazione, è necessario generare un tooincrease di ticket di supporto per questo limite per la sottoscrizione.

- **Provisioning timeout Out stato della macchina virtuale** - se qualsiasi macchina virtuale ha lo stato hello **timeout del provisioning**, questo deve toobe risolto pre-migrazione. Hello unico modo toodo equivale con tempi di inattività per deprovisioning o la riconfigurazione hello VM (delete, conservare il disco hello e ricreare hello VM). 

- **Stato della macchina virtuale RoleStateUnknown** - se la migrazione si arresta a causa tooa **stato del ruolo sconosciuto** errore del messaggio, esaminare hello VM tramite il portale di hello e assicurarsi che sia in esecuzione. Questo errore in genere scompare da solo (nessuna correzione necessaria) dopo alcuni minuti, è spesso temporaneo e si verifica durante un'operazione di **avvio**, **arresto** o **riavvio** di una macchina virtuale. **Procedura consigliata:** ritentare nuovamente la migrazione dopo alcuni minuti. 

- **Cluster di infrastruttura inesistente**: in alcuni casi, alcune VM non possono essere migrate per vari motivi. Uno di questi casi noti è se hello VM è stato creato di recente (all'interno di hello ultima settimana o meno) e si sono verificate tooland un cluster di Azure che non è ancora per carichi di lavoro di gestione risorse di Azure.  Si riceverà un messaggio di errore **dell'infrastruttura cluster non esiste** e hello VM non è possibile eseguire la migrazione. In attesa di un paio di giorni verrà risolto in genere questo particolare problema come cluster hello non appena verrà visualizzato Gestione risorse di Azure abilitata. Tuttavia, una soluzione immediata è troppo`stop-deallocate` hello VM, quindi continuare in avanti con la migrazione e avviare hello VM eseguire il backup in Azure Resource Manager dopo la migrazione.

### <a name="pitfalls-tooavoid"></a>Risoluzione dei problemi tooavoid

- Non richiedere i tasti di scelta rapida e omettere le migrazioni di hello esecuzione convalidare/preparare/abort.
- Più, se non tutti, dei problemi potenziali esporrà durante i passaggi di convalida/preparare/abort hello.

## <a name="migration"></a>Migrazione

### <a name="technical-considerations-and-tradeoffs"></a>Considerazioni tecniche e compromessi

Si è pronti a questo punto perché ha esaminato hello problemi noti con l'ambiente.

Per le migrazioni di reale hello, potrebbe essere tooconsider:

1. Pianificazione e la pianificazione di rete virtuale hello (più piccola unità di migrazione) con l'aumento di priorità.  Hello innanzitutto semplice reti virtuali e lo stato di avanzamento hello più complicato reti virtuali.
2. La maggior parte dei clienti avrà ambienti non di produzione e di produzione.  Pianificare per ultimo l'ambiente di produzione.
3. **(FACOLTATIVO)**  Pianificare un tempo di inattività di manutenzione con molto buffer nel caso in cui si verifichino problemi imprevisti.
4. Comunicare e allinearsi con i team di supporto nel caso in cui si verifichino problemi.

### <a name="patterns-of-success"></a>Modelli di successo

informazioni tecniche sulla Hello da hello sezione Test Lab deve essere considerato e risolti migrazione reale tooa precedente.  Grazie a testing adeguate, la migrazione di hello è effettivamente un esterne.  Per gli ambienti di produzione, potrebbe essere utile toohave ulteriore supporto, ad esempio un partner Microsoft attendibile o servizi Microsoft Premier.

### <a name="pitfalls-tooavoid"></a>Risoluzione dei problemi tooavoid

Test non completamente potrebbe causare problemi e ritardo nella migrazione hello.  

## <a name="beyond-migration"></a>Oltre la migrazione

### <a name="technical-considerations-and-tradeoffs"></a>Considerazioni tecniche e compromessi

Ora che si è in Gestione risorse di Azure, ottimizzare la piattaforma di hello.  Hello lettura [Panoramica di gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md) toofind out sui vantaggi aggiuntivi.

Tooconsider operazioni:

- Creazione di bundle migrazione hello con altre attività.  La maggior parte dei clienti opta per una finestra di manutenzione dell'applicazione.  Se in tal caso, potrebbe essere necessario toouse tooenable il tempo di inattività altre funzionalità di gestione risorse di Azure, ad esempio la crittografia e la migrazione tooManaged dischi.
- Accedere nuovamente hello tecnica e motivi aziendali per Gestione risorse di Azure. abilitare hello servizi aggiuntivi disponibili solo in Gestione risorse di Azure che si applicano tooyour ambiente.
- Aggiornare l'ambiente con servizi PaaS.

### <a name="patterns-of-success"></a>Modelli di successo

Essere intenzionale su quali servizi ora si desidera tooenable in Gestione risorse di Azure.  Molti clienti trovare hello seguito interessanti per gli ambienti Azure:

- [controllo degli accessi in base al ruolo](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Modelli di Azure Resource Manager per una distribuzione più semplice e controllata](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Tag](../../azure-resource-manager/resource-group-using-tags.md).
- [Controllo di attività](../../azure-resource-manager/resource-group-audit.md)
- [Criteri delle risorse](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Risoluzione dei problemi tooavoid

Tenere presente perché è stato avviato questo percorso di migrazione classica tooAzure Gestione risorse.  Quali sono state motivi aziendali originale hello? Si sono raggiunti motivazioni hello?


## <a name="next-steps"></a>Passaggi successivi

* [Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utilizzare le risorse IaaS toomigrate PowerShell da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rivedere gli errori di migrazione più comuni](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
