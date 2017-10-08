---
title: insieme di credenziali di servizi di ripristino di Azure tooan aaaUpgrade un insieme di credenziali di Site Recovery
description: Informazioni su come un insieme di credenziali di Azure Site Recovery tooupgrade tooa servizi di ripristino dell'insieme di credenziali
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>L'aggiornamento di un archivio di servizi di ripristino basate su Gestione risorse di Azure Site Recovery tooan insieme di credenziali

In questo articolo viene descritto come tooupgrade Azure Site Recovery insiemi di credenziali di insiemi di credenziali del servizio di ripristino basate su Gestione risorse tooAzure senza alcun impatto sulla replica in corso. Per altre informazioni sulle funzionalità e sui vantaggi di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Introduzione
Un insieme di credenziali di servizi di ripristino è una risorsa di gestione risorse di Azure per la gestione dei backup e ripristino di emergenza in modo nativo nel cloud hello. È un insieme di credenziali unificata che è possibile utilizzare in hello nuovo portale di Azure e sostituisce backup classico hello e insiemi di credenziali di Site Recovery.

Gli insiemi di credenziali di Servizi di ripristino offrono una nuova gamma di funzionalità, elencate di seguito:

* Supporto di Azure Resource Manager: è possibile proteggere ed eseguire il failover delle macchine virtuali e dei computer fisici in uno stack di Azure Resource Manager.

* Escludere il disco: se si dispone di file temporanei o elevata varianza dei dati che non si desidera toouse tutta la larghezza di banda per, è possibile escludere i volumi di replica. Questa funzionalità è stata abilitata in *VMware tooAzure* e *tooAzure Hyper-V* e viene estesa anche scenari tooother.

* Supporto per premium e l'archiviazione con ridondanza locale: È ora possibile proteggere i server nel servizio di archiviazione premium gli account che consentono agli utenti di applicazioni tooprotect con versioni successive operazioni di input/output al secondo (IOPS). Questa funzionalità è attualmente abilitata *tooAzure VMware*.

* Guida introduttiva esperienza semplificata: hello avanzata esperienza di Guida introduttiva è stata progettata l'installazione di ripristino di emergenza toomake semplice.

* Backup e gestione di ripristino del sito da hello stesso insieme di credenziali: È ora possibile proteggere i server per il ripristino di emergenza o eseguire il backup da hello stesso insieme di credenziali, che può ridurre il sovraccarico in modo significativo la gestione.

Per ulteriori informazioni sull'esperienza hello aggiornato e le funzionalità, vedere hello [blog di archiviazione, Backup e ripristino](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Funzionalità principali

* Nessun impatto sulla replica in corso: le repliche in corso continuano senza interruzioni durante e dopo l'aggiornamento.

* Nessun costo aggiuntivo: è possibile ottenere un intero set di funzionalità aggiornate senza costi aggiuntivi.

* Senza perdita di dati: poiché questo processo è un aggiornamento e non una migrazione, punti di ripristino esistenti di replica e le impostazioni rimangono invariate durante e dopo l'aggiornamento di hello.


## <a name="what-happens-during-hello-vault-upgrade"></a>Cosa accade durante l'aggiornamento dell'insieme di credenziali hello?

Durante l'aggiornamento di hello, è possibile eseguire operazioni quali la registrazione di un nuovo server o l'abilitazione della replica per una macchina virtuale (VM). Le operazioni che coinvolgono la lettura o di scrittura dati toohello insieme di credenziali, ad esempio la replica in corso dell'insieme di credenziali toohello gli elementi protetti, senza interruzioni.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Tooautomation modifiche e gli strumenti dopo l'aggiornamento di hello
Come si aggiorna il tipo di insieme di credenziali hello dal modello di distribuzione di gestione delle risorse modello toohello hello distribuzione classica, aggiornare automazione esistente hello o tooensure gli strumenti che continui toowork dopo l'aggiornamento di hello.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Preparare l'ambiente per l'aggiornamento di hello

* [Installare PowerShell o l'aggiornamento tooversion 5 o versione successiva](https://www.microsoft.com/download/details.aspx?id=50395)
* [Installare hello la versione più recente di Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases)
* [Scaricare script di aggiornamento dell'insieme di credenziali di servizi di ripristino hello](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Prerequisiti
gli insiemi di credenziali del servizio di ripristino basate su Gestione risorse tooAzure insiemi di credenziali di tooupgrade da Site Recovery, è necessario soddisfare i seguenti requisiti hello:

* Versione minima dell'agente: versione di hello del Provider di Azure Site Recovery installato nel server deve essere 5.1.1700.0 o versione successiva.

* Configurazione supportata: non è possibile configurare l'insieme di credenziali con la rete di archiviazione (SAN) o i gruppi di disponibilità AlwaysOn di SQL Server. Sono supportate tutte le altre configurazioni.

    >[!NOTE]
    >Dopo l'aggiornamento di hello, è possibile gestire i mapping di archiviazione solo tramite PowerShell.

* Scenario di distribuzione supportati: l'insieme di credenziali non devono essere hello *tooAzure VMware* modello di distribuzione legacy. Prima di procedere, spostare innanzitutto il modello di distribuzione avanzata di toohello.

* Nessun processo attivo avviata dall'utente che coinvolgono gestione piano operations: perché il piano di gestione toohello di accesso è limitato durante l'aggiornamento, completare tutte le azioni del piano di gestione prima attivare l'aggiornamento di hello. Questo processo non include la replica in corso.

## <a name="frequently-asked-questions"></a>Domande frequenti

**L'aggiornamento influisce sulla replica in corso?**

No. La replica in corso continua senza interruzioni durante e dopo l'aggiornamento di hello.

**Cosa accade toonetwork impostazioni, ad esempio le impostazioni IP e VPN da sito a sito?**

aggiornamento di Hello non influenza le impostazioni di rete hello. Tutte le connessioni da Azure a locale rimangono inalterate.

**Gli insiemi di credenziali toomy cosa accade se non è previsto tooupgrade in hello prossimo futuro?**

Supporto per l'insieme di credenziali di Site Recovery nel portale di Azure precedente hello verrà deprecato a partire settembre 2017. È consigliabile utilizzare hello funzionalità di aggiornamento toomove toohello nuovo portale.

**Qual è l'impatto di questo piano di migrazione per gli strumenti esistenti?**  

L'aggiornamento del modello di distribuzione di gestione delle risorse toohello strumenti è una delle modifiche più importanti hello che è necessario tener conto nei piani di aggiornamento. gli insiemi di credenziali di Hello servizi di ripristino sono basati sul modello di distribuzione di gestione risorse hello. 

**Il tempo hello tempi di inattività gestione piano ultimo?**

aggiornamento di Hello richiede in genere circa 15 minuti too30 e potrebbero richiedere tooa massima di un'ora.

**È possibile eseguire il ripristino dello stato precedente dopo l'aggiornamento?**

No. Eseguire il rollback non è supportato dopo risorse hello sono state aggiornate.

**È possibile convalidare la sottoscrizione o risorse toosee se possono essere aggiornate?**

Sì. In hello piattaforma supportata l'opzione di aggiornamento, hello innanzitutto l'aggiornamento di hello è toovalidate che le risorse di hello siano in grado di un aggiornamento. Se la convalida di hello non riesce, si riceverà i messaggi di errore appropriato o avvisi.

**Come è possibile segnalare un problema con l'aggiornamento di hello?**

Se si verificano eventuali errori durante l'aggiornamento di hello, notare l'ID operazione hello elencato in errore hello. Supporto Microsoft funzionerà in modo proattivo sulla risoluzione problema hello. È anche possibile contattare il team di supporto hello con l'ID sottoscrizione, nome insieme di credenziali e l'ID dell'operazione. Supporto funzionerà problema hello tooresolve più rapidamente possibile. Non ripetere l'operazione di hello a meno che non si è toodo in modo esplicito istruzioni riportata in questo caso da Microsoft.

## <a name="run-hello-script"></a>Eseguire script hello

In PowerShell eseguire hello comando seguente:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* SubscriptionID: hello ID sottoscrizione associato a credenziali hello che si esegue l'aggiornamento.

* VaultName: nome di hello dell'insieme di credenziali hello che si esegue l'aggiornamento.

* : Hello posizione dell'insieme di credenziali hello che si esegue l'aggiornamento.

* ResourceType: HyperVRecoveryManagerVault per gli insiemi di credenziali di Site Recovery.

* TargetResourceGroupName: gruppo di risorse hello in cui si desidera hello aggiornato toobe insieme di credenziali inserito. TargetResourceGroupName può essere un gruppo di risorse esistente in Azure Resource Manager o uno nuovo. Se hello TargetResourceGroupName fornito non esiste, viene creato come parte dell'aggiornamento hello in hello stessa località dell'insieme di credenziali hello. Per ulteriori informazioni, vedere sezione "Gruppi di risorse" hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Denominazione di gruppo di risorse è vincoli toocertain soggetto. insieme di credenziali tooprevent aggiornare errore, essere attentamente che hello tooobserve convenzione di denominazione.
    >
    >ad esempio:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc

In alternativa, è possibile eseguire lo script seguente hello. Per i parametri di hello richiesto, immettere i valori di hello.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Hello script di PowerShell richiesto è tooenter le credenziali. Immetterli due volte, una volta per conto del modello di distribuzione classica hello e una volta per hello account di gestione risorse di Azure.

2. Dopo aver immesso le credenziali, script hello viene eseguito un toodetermine di controllo se il hello soddisfa il programma di installazione di infrastruttura indicato in precedenza requisiti.

3. Dopo prerequisiti hello sono stati verificati e confermati, si è tooproceed richiesta con l'aggiornamento dell'insieme di credenziali hello. processo di aggiornamento Hello avvia l'insieme di credenziali di aggiornamento. intero aggiornamento Hello può richiedere 15 too30 minuti toocomplete.

4. Dopo l'aggiornamento di hello è stata completata, è possibile accedere hello aggiornato dell'insieme di credenziali nel portale di Azure nuova hello.

## <a name="post-upgrade-vault-management"></a>Gestione dell'insieme di credenziali successiva all'aggiornamento

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>La replica tramite Azure Site Recovery in hello che insieme di credenziali di servizi di ripristino

* È ora possibile proteggere le macchine virtuali di Azure da un'area tooanother. Per altre informazioni, vedere [Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery](site-recovery-azure-to-azure.md).

* Per ulteriori informazioni sulla replica tooAzure le macchine virtuali VMware, vedere [tooAzure di replicare le macchine virtuali VMware con il ripristino del sito](vmware-walkthrough-overview.md).

* Per ulteriori informazioni sulla replica tooAzure macchine virtuali Hyper-V (senza VMM), vedere [replica Hyper-V le macchine virtuali (senza VMM) tooAzure](hyper-v-site-walkthrough-overview.md).

* Per ulteriori informazioni sulla replica tooAzure macchine virtuali Hyper-V (con VMM), vedere [hello di macchine virtuali di replica Hyper-V in VMM cloud tooAzure usando Site Recovery nel portale di Azure](vmm-to-azure-walkthrough-overview.md).

* Per ulteriori informazioni sulla replica sito secondario tooa di Hyper-macchine virtuali (con VMM), vedere [hello di macchine virtuali di replica Hyper-V in VMM cloud tooa secondario VMM del sito utilizzando il portale di Azure](site-recovery-vmm-to-vmm.md).

* Per ulteriori informazioni sulla replica sito secondario di tooa le macchine virtuali VMware, vedere [replica locale macchine virtuali VMware o un sito secondario di server fisici tooa nel portale di Azure classico hello](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Visualizzare gli elementi replicati

Hello immagine seguente mostra la pagina hello servizi di ripristino dell'insieme di credenziali dashboard che consente di visualizzare le entità di chiave per l'insieme di credenziali hello. Selezionare un elenco di entità protetti nell'insieme di credenziali hello tooview **Site Recovery** > **gli elementi replicati**.


![Elementi replicati](./media/upgrade-site-recovery-vaults/replicateditems.png)

Hello immagine seguente viene illustrato del flusso di lavoro hello per la visualizzazione delle elementi replicati e hello **Failover** comando per avviare un failover.

![Elementi replicati](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Visualizzare le impostazioni di replica

Nell'insieme di credenziali Site Recovery hello ogni gruppo protezione dati è configurato con la frequenza di copia, conservazione del punto di ripristino, frequenza di snapshot coerenti dell'applicazione e altre impostazioni di replica. Nell'insieme di credenziali di hello servizi di ripristino, queste impostazioni sono configurate come un criterio di replica. nome di Hello del criterio di hello è il nome di hello del gruppo protezione dati hello o hello *primarycloud_Policy*.

Per ulteriori informazioni sui criteri di replica, vedere [gestire criteri di replica per VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).
