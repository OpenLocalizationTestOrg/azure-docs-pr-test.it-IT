---
title: una distribuzione di Dynamics AX multilivello usando Azure Site Recovery aaaReplicate | Documenti Microsoft
description: Questo articolo viene descritto come tooreplicate e proteggere con Azure Site Recovery di Dynamics AX
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Eseguire la replica di un'applicazione Dynamics AX multilivello usando Azure Site Recovery

## <a name="overview"></a>Panoramica


Microsoft Dynamics AX è una delle soluzioni ERP più diffusi di hello tra processo toostandardized aziende luoghi, gestire le risorse e semplificando la conformità. In considerazione un'applicazione hello è organizzazione tooan critici di business è molto importante toobe assicurarsi che se ripristino di emergenza, applicazione deve essere in esecuzione nel tempo minimo.

Attualmente Microsoft Dynamics AX non include funzionalità di ripristino di emergenza predefinite. Microsoft Dynamics AX è costituito da molti componenti server come applicazione oggetto Server, Active Directory (AD), Server di Database SQL, i SharePoint Server, Reporting e così via Server toomanage hello il ripristino di emergenza di ciascuno di questi componenti è manualmente non solo dispendiosa ma anche soggetto a errori.

Questo articolo descrive dettagliatamente come creare una soluzione di ripristino di emergenza per l'applicazione Dynamics AX usando [Azure Site Recovery](site-recovery-overview.md). Vengono anche descritti i failover pianificati/non pianificati/di test tramite il piano di ripristino con un solo clic, le configurazioni supportate e i prerequisiti.
La soluzione di ripristino di emergenza basata su Azure Site Recovery è completamente testata, certificata e consigliata da Microsoft Dynamics AX.



## <a name="prerequisites"></a>Prerequisiti

L'implementazione di ripristino di emergenza per l'applicazione di Dynamics AX usando Azure Site Recovery richiede hello seguenti prerequisiti completati.

•   Configurare una distribuzione di Dynamics AX locale

•   Creare un insieme di credenziali dei servizi di Azure Site Recovery nella sottoscrizione di Microsoft Azure

• Se Azure è il sito di ripristino, eseguire lo strumento di valutazione della macchina virtuale Azure hello in tooensure macchine virtuali che sono compatibili con le macchine virtuali di Azure e servizi di Azure Site Recovery


## <a name="site-recovery-support"></a>Supporto di Site Recovery

Ai fini di hello della creazione di questo articolo, macchine virtuali VMware con 2012R3 Dynamics AX in Windows Server 2012 R2 Enterprise sono state utilizzate. Replica di ripristino del sito è indipendente dall'applicazione, indicazioni di hello forniti sono toohold previsto negli scenari seguenti.

### <a name="source-and-target"></a>Origine e destinazione

**Scenario** | **sito secondario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sì | Sì
**VMware** | Sì | Sì
**Server fisico** | Sì | Sì

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Abilitare il ripristino di emergenza dell'applicazione Dynamics AX con Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Proteggere l'applicazione Dynamics AX
Ogni componente di hello Dynamics AX esigenze toobe protetti tooenable hello applicazione completa replica e il ripristino. Questa sezione descrive queste operazioni:

**1. Protezione di Active Directory**

**2. Protezione del livello SQL**

**3. Protezione dei livelli app e Web**

**4. Configurazione delle impostazioni di rete**

**5. Piano di ripristino**

### <a name="1-setup-ad-and-dns-replication"></a>1. Configurare la replica di Active Directory e DNS

Active Directory è necessaria nel sito di ripristino di emergenza hello per toofunction applicazione Dynamics AX. Esistono due opzioni consigliate in base hello complessità dell'ambiente locale del cliente hello.

**Opzione 1**

Se il cliente hello dispone di un numero ridotto di applicazioni e un singolo controller di dominio per il suo intero sito locale e verrà essersi verificato un errore sull'intero sito hello insieme, quindi è consigliabile utilizzare la replica di ripristino automatico di sistema tooreplicate hello controller di dominio computer toosecondary sito ( applicabile per sito tooSite e tooAzure sito).

**Opzione 2**

Se hello cliente ha un numero elevato di applicazioni e sia in esecuzione una foresta di Active Directory ed eseguirà il failover alcune applicazioni alla volta, quindi è consigliabile configurare un controller di dominio nel sito di ripristino di emergenza hello (sito secondario o in Azure).

Consultare troppo[guida complementare in rende disponibile un controller di dominio nel sito di ripristino di emergenza](site-recovery-active-directory.md). Nella parte restante di questo documento si presuppone che nel sito di ripristino di emergenza sia disponibile un controller di dominio.

### <a name="2-setup-sql-server-replication"></a>2. Configurare la replica di SQL Server
Per indicazioni tecniche dettagliate su hello consigliata l'opzione per la protezione, consultare Guida toocompanion [livello SQL](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Abilitare la protezione per le VM AOS e client Dynamics AX
Eseguire la configurazione di Azure Site Recovery pertinente in base alle macchine virtuali hello se distribuite in [Hyper-V](site-recovery-hyper-v-site-to-azure.md) oppure [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Tooconfigure di frequenza coerente con l'arresto anomalo del sistema consigliata è di 15 minuti.
>

Hello seguito snapshot Mostra lo stato di protezione hello di macchine virtuali componente Dynamics in uno scenario di protezione 'TooAzure sito VMware'.
![Elementi protetti ](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Configurare le impostazioni di rete
Configurare le impostazioni di calcolo e di rete delle VM

Per i client AX hello e le macchine virtuali AOS configurare le impostazioni di rete in Azure Site Recovery in modo che le reti VM hello ottenere toohello collegato corretto ripristino di emergenza rete dopo il failover. Verificare che sia di rete di ripristino di emergenza hello per questi livelli livello SQL toohello instradabile.

È possibile selezionare Ciao VM hello replicate le impostazioni di rete hello tooconfigure elementi come illustrato nello snapshot hello riportato di seguito.

* Per i server AOS selezionare il set di disponibilità corretto hello.

* Se si utilizza un indirizzo IP statico, specificare hello IP che si desidera hello tootake macchina virtuale in hello **indirizzo IP di destinazione** campo ![le impostazioni di rete](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Creazione di un piano di ripristino

È possibile creare un piano di ripristino nel processo di failover di Azure Site Recovery tooautomate hello. Aggiungere il livello di applicazione e web in hello il piano di ripristino. Ordinarli in diversi gruppi in modo che hello front-end arresto prima di livello applicazione.

1)  Selezionare l'insieme di credenziali di Azure Site Recovery hello nella sottoscrizione e fare clic sul riquadro 'Piani di ripristino'.

2)  Fare clic su "Crea piano di ripristino" e specificare un nome.

3)  Selezionare hello 'Source' e 'Target'. destinazione Hello può essere il sito secondario o di Azure. Nel caso in cui si sceglie di Azure, è necessario specificare il modello di distribuzione hello

![Crea piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Selezionare hello AOS e piano di ripristino toohello macchine virtuali di client e fare clic su ✓.
![Crea piano di ripristino](./media/site-recovery-dynamics-ax/selectvms.png)


![Piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplan.png)

È possibile personalizzare il piano di ripristino hello per l'applicazione di Dynamics AX aggiungendo i vari passaggi come indicato di seguito. Hello sopra snapshot viene illustrato il piano di ripristino completo hello dopo l'aggiunta di tutti i passaggi di hello.

*Passaggi:*

*1. Passaggi di failover di SQL Server*

Fare riferimento troppo['Soluzione di ripristino di emergenza di SQL Server'](site-recovery-sql.md) guida complementare per informazioni sul server tooSQL specifici passaggi di ripristino.

*2. Failover gruppo 1: Eseguire il failover le macchine virtuali AOS hello*

Assicurarsi che il punto di ripristino hello selezionato sia il più vicino possibile toohello database PIT ma non-ahead.

*3. Script: Servizio di bilanciamento del carico Aggiungi (solo A E)* aggiungere uno script (tramite l'automazione di Azure) dopo il gruppo di VM AOS arriva tooadd un tooit di bilanciamento del carico. È possibile utilizzare un toodo script questa attività. Vedere l'articolo [come tooadd bilanciamento del carico per applicazioni multilivello ripristino di emergenza](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Failover gruppo 2: Eseguire il failover client AX hello macchine virtuali.*
Il livello di web hello macchine virtuali come parte del piano di ripristino hello il failover.


### <a name="doing-a-test-failover"></a>Esecuzione di un failover di test

Fare riferimento too'AD Solution ' e 'Soluzione di ripristino di emergenza di SQL Server' le guide complementari per considerazioni specifiche tooAD e SQL server rispettivamente durante il Failover di Test.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.
2.  Fare clic sul piano di ripristino hello creato per Dynamics AX.
3.  Fare clic su "Failover di test".
4.  Selezionare hello rete virtuale toostart hello il failover, il processo di test.
5.  Una volta ambiente secondario hello è attivo, è possibile eseguire le convalide.
6.  Dopo aver complete le convalide hello, è possibile selezionare 'Convalide completare' e ambiente di failover di test hello verrà pulita.

Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.

### <a name="doing-a-failover"></a>Esecuzione di un failover

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.
2.  Fare clic sul piano di ripristino hello creato per Dynamics AX.
3.  Fare clic su "Failover" e selezionare "Failover".
4.  Selezionare la rete di destinazione hello e fare clic su processo di failover ✓ toostart hello.

Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.

### <a name="perform-a-failback"></a>Eseguire un failback

Fare riferimento too'SQL soluzione di ripristino di emergenza Server "nella Guida complementare per server tooSQL specifiche considerazioni durante il Failback.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.
2.  Fare clic sul piano di ripristino hello creato per Dynamics AX.
3.  Fare clic su "Failover" e selezionare il failover.
4.  Fare clic su "Cambia direzione".
5.  Selezionare le opzioni appropriate di hello - sincronizzazione dei dati e le opzioni di creazione di VM
6.  Fare clic su ✓ toostart hello 'Failback' processo.


Seguire [queste linee guida](site-recovery-failback-azure-to-vmware.md) quando si esegue un failback.

##<a name="summary"></a>Riepilogo
Con Azure Site Recovery è possibile creare un piano di ripristino di emergenza completamente automatico per l'applicazione Dynamics AX. È possibile avviare il failover hello entro pochi secondi da qualsiasi posizione in hello evento di interruzione e ottenere un'applicazione hello attivo e in esecuzione in minuti.

## <a name="next-steps"></a>Passaggi successivi
Lettura [i carichi di lavoro è possibile proteggere?](site-recovery-workload.md) toolearn ulteriori informazioni sulla protezione di carichi di lavoro aziendali con Azure Site Recovery.
