---
title: aaaBack di Windows server o workstation tooAzure (modello classico) | Documenti Microsoft
description: Eseguire il backup di Windows Server o client tooa insieme di credenziali backup in Azure. Scorrere nozioni di base per la protezione dei file e cartelle tooa insieme di credenziali di Backup tramite hello Azure Backup agent.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: insieme di credenziali di backup; backup di un server Windows; backup di Windows;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Eseguire il backup di un tooAzure di Windows server o workstation tramite il portale classico di hello
> [!div class="op_single_selector"]
> * [Portale classico](backup-configure-vault-classic.md)
> * [Portale di Azure](backup-configure-vault.md)
>
>

In questo articolo vengono descritte le procedure di hello, che è necessario toofollow tooprepare ambiente ed eseguire il backup un tooAzure di Windows server (o una workstation). Contiene anche considerazioni sulla distribuzione della soluzione di backup. Se si è interessati durante il Backup di Azure per hello prima volta, in questo articolo rapidamente illustra hello processo.

Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Resource Manager e distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="before-you-start"></a>Prima di iniziare
tooback backup di un server o client tooAzure, è necessario un account di Azure. Se non si ha un account, è possibile crearne uno [gratuito](https://azure.microsoft.com/free/) in pochi minuti.

## <a name="create-a-backup-vault"></a>Creare un insieme di credenziali per il backup
tooback backup di file e cartelle da un server o client, è necessario un insieme di credenziali di backup in cui si desidera toostore hello dati area geografica di hello toocreate.

> [!IMPORTANT]
> A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
>
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> **15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell. <br/> **A partire dal 1° novembre 2017**:
>- Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>


## <a name="download-hello-vault-credential-file"></a>Scaricare file delle credenziali dell'insieme di credenziali hello
è necessario toobe autenticato con un insieme di credenziali di backup prima di è possibile eseguire il backup dei dati tooAzure Hello nel computer locale. l'autenticazione di Hello viene ottenuta tramite *archivio credenziali*. file delle credenziali dell'insieme di credenziali Hello viene scaricato tramite un canale protetto dal portale classico hello. chiave privata del certificato Hello non viene mantenuto nel portale di hello o servizio hello.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello archivio credenziali file tooa locale
1. Nel riquadro di spostamento a sinistra di hello, fare clic su **servizi di ripristino**, quindi selezionare hello insieme di credenziali backup creato.

    ![Completamento infrarossi](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Nella pagina introduttiva hello, fare clic su **Scarica credenziali**.

   portale classico Hello genera un insieme di credenziali utilizzando una combinazione di nome insieme di credenziali hello e hello data corrente. file delle credenziali dell'insieme di credenziali Hello viene utilizzato solo durante il flusso di lavoro di hello registrazione e scade dopo 48 ore.

   file delle credenziali dell'insieme di credenziali Hello può essere scaricato dal portale hello.
3. Fare clic su **salvare** toodownload hello archivio credenziali file toohello cartella download dell'account locale hello. È inoltre possibile selezionare **Salva con nome** da hello **salvare** menu toospecify un percorso per i file delle credenziali dell'insieme di credenziali hello.

   > [!NOTE]
   > Assicurarsi che i file delle credenziali dell'insieme di credenziali hello viene salvato in una posizione accessibile dal computer. Se è stata archiviata in un blocco di messaggio server o condivisione file, assicurarsi di disporre tooaccess autorizzazioni hello è.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Scaricare, installare e registrare l'agente di Backup hello
Dopo aver creato l'insieme di credenziali backup hello e file delle credenziali dell'insieme di credenziali hello download, è necessario installare un agente in ogni computer Windows.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, installare e registrare agente hello
1. Fare clic su **servizi di ripristino**, quindi selezionare hello insieme di credenziali backup che si desidera tooregister con un server.
2. Nella pagina introduttiva hello, fare clic su agente hello **agente per Windows Server o client di System Center Data Protection Manager o Windows**. Fare quindi clic su **Salva**.

    ![Salva agente](./media/backup-configure-vault-classic/agent.png)
3. Dopo aver scaricato il file di MARSagentinstaller.exe hello, fare clic su **eseguire** (o fare doppio clic su **MARSAgentInstaller.exe** dal percorso hello salvato).
4. Scegliere la cartella di installazione hello e la cartella della cache che sono necessari per l'agente di hello e quindi fare clic su **Avanti**. percorso della cache di Hello specificato deve disporre di spazio uguale tooat almeno il 5% dei dati di backup hello.
5. È possibile continuare tooconnect toohello Internet tramite le impostazioni di proxy predefinito hello.             Se si usa un toohello tooconnect di server proxy Internet, nella pagina di configurazione del Proxy hello, selezionare hello **Usa impostazioni proxy personalizzate** casella di controllo e quindi immettere i dettagli del server proxy hello. Se si utilizza un proxy autenticato, immettere i dettagli di nome e una password utente hello e quindi fare clic su **Avanti**.
6. Fare clic su **installare** toobegin installazione dell'agente hello. l'agente di Backup Hello installa .NET Framework 4.5 e Windows PowerShell (se non è già installato) installazione hello toocomplete.
7. Dopo aver installato l'agente di hello, fare clic su **procedere tooRegistration** toocontinue con flusso di lavoro hello.
8. Nella pagina di identificazione dell'insieme di credenziali hello, Sfoglia tooand hello selezionare archivio credenziali scaricato in precedenza.

    file delle credenziali dell'insieme di credenziali Hello è valido solo 48 ore dopo che è stato scaricato dal portale hello. Se si verifica un errore in questa pagina (ad esempio, "insieme di credenziali file specificato è scaduto"), accedi toohello portal e scaricare di nuovo il file delle credenziali dell'insieme di credenziali hello.

    Verificare che il file di credenziali dell'insieme di credenziali hello è disponibile in una posizione a cui è possibile accedere da un'applicazione hello il programma di installazione. Se si verificano errori di accesso, copiare hello archivio credenziali file tooa percorso temporaneo hello stesso computer e ripetere l'operazione di hello.

    Se si verifica un errore relativo alle credenziali dell'insieme di credenziali, ad esempio "non valido dell'insieme di credenziali le credenziali fornite", il file hello è danneggiato o non avere hello credenziali più recenti associate al servizio di ripristino hello. Ripetere l'operazione di hello dopo il download di un nuovo file delle credenziali dell'insieme di credenziali dal portale hello. Questo errore può verificarsi anche se un utente fa clic hello **Download insieme di credenziali** opzione più volte in rapida successione. In questo caso, solo hello ultimo insieme di credenziali file delle credenziali è valido.
9. Nella pagina impostazione crittografia hello, è possibile generare una passphrase o fornire una passphrase (con un minimo di 16 caratteri). Tenere presente che toosave hello passphrase in un luogo sicuro.
10. Fare clic su **Finish**. Hello registrazione guidata Server Registra server hello con Backup.

    > [!WARNING]
    > Se si perde o dimentica passphrase hello, Microsoft non consente di ripristinare i dati di backup hello. Si è proprietari hello passphrase di crittografia e Microsoft non abbiano visibilità sul passphrase hello in uso. Salvare il file di hello in un luogo sicuro perché sarà necessaria durante un'operazione di ripristino.
    >
    >

11. Dopo aver impostata la chiave di crittografia hello, lasciare hello **avviare Microsoft Azure Recovery Services Agent** casella selezionata e quindi fare clic su **Chiudi**.

## <a name="complete-hello-initial-backup"></a>Backup iniziale hello completo
backup iniziale Hello include due attività principali:

* Creazione pianificazione backup hello
* Il backup dei file e cartelle per hello prima volta

Al termine di backup iniziale hello, criteri di backup hello crea punti di backup che è possibile utilizzare se sono necessari dati hello toorecover. criteri di backup Hello avviene in base a una pianificazione hello definita.

### <a name="tooschedule-hello-backup"></a>backup di hello tooschedule
1. Aprire l'agente di Backup di Microsoft Azure hello. (Verrà aperto automaticamente se sono stati lasciati hello **avviare Microsoft Azure Recovery Services Agent** casella di controllo selezionata quando si è chiuso hello registrazione guidata Server.) È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.

    ![Avviare l'agente Azure Backup hello](./media/backup-configure-vault-classic/snap-in-search.png)
2. Nell'agente di Backup hello, fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Pagina di pianificazione guidata Backup hello introduzione su hello, fare clic su **Avanti**.
4. Nella pagina di tooBackup selezionare elementi hello, fare clic su **Aggiungi elementi**.
5. Selezionare le cartelle che si desidera tooback e quindi fare clic su file hello **OK**.
6. Fare clic su **Avanti**.
7. In hello **specificare pianificazione Backup** specificare hello **pianificazione del backup** e fare clic su **Avanti**.

    È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.

    ![Elementi per il backup di Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Per ulteriori informazioni su come toospecify hello pianificazione del backup, vedere l'articolo hello [tooreplace utilizzare Azure Backup infrastruttura nastro](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. In hello **selezionare criteri di conservazione** pagina, seleziona hello **criteri di conservazione** hello copia di backup.

    criteri di conservazione Hello specificano durata hello per cui verrà archiviato il backup di hello. Anziché specificare solo un criterio"semplice" per tutti i punti di backup, è possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello. È possibile modificare toomeet criteri di conservazione giornaliero, settimanale, mensile e annuale hello le proprie esigenze.
9. Nella pagina tipo di Backup iniziale scegliere hello, scegliere il tipo di backup iniziale di hello. Lasciare l'opzione hello **automaticamente tramite rete hello** selezionata e quindi fare clic su **Avanti**.

    È possibile eseguire il backup automaticamente tramite rete hello oppure è possibile eseguire il backup non in linea. resto Hello di questo articolo descrive il processo di hello per il backup automaticamente. Se si preferisce toodo un backup offline, vedere l'articolo di hello [Offline backup flusso di lavoro in Backup di Azure](backup-azure-backup-import-export.md) per ulteriori informazioni.
10. Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.
11. Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.

### <a name="enable-network-throttling-optional"></a>Abilitare la limitazione della larghezza di banda (facoltativo)
l'agente di Backup Hello fornisce la limitazione delle richieste di rete. La limitazione controlla l'uso della larghezza di banda della rete durante il trasferimento dati. Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico Internet. La limitazione si applica tooback backup e ripristino.

**la limitazione delle richieste di rete tooenable**

1. Nell'agente di Backup hello, fare clic su **Modifica proprietà**.

    ![Modifica proprietà](./media/backup-configure-vault-classic/change-properties.png)
2. In hello **limitazione** scheda, seleziona hello **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet** casella di controllo.

    ![Limitazione della larghezza di banda della rete](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Dopo avere abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.

    i valori di larghezza di banda Hello iniziano 512 kilobit al secondo (Kbps) e possono aumentare fino a too1, 023 megabyte al secondo (MBps). È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello sono considerate giorni. Gli orari al di fuori delle ore lavorative definite vengono considerati ore non lavorative.
4. Fare clic su **OK**.

### <a name="tooback-up-now"></a>tooback backup adesso
1. Nell'agente di Backup hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.

    ![Eseguire ora il backup di Windows Server](./media/backup-configure-vault-classic/backup-now.png)
2. Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello. Fare clic su **Backup**.
3. Fare clic su **Chiudi** guidata hello tooclose. Se si esegue questa operazione prima al termine del processo di backup hello, toorun guidata hello continua in background hello.

Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.

![Completamento infrarossi](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Passaggi successivi
* Sottoscrivere un [account Azure gratuito](https://azure.microsoft.com/free/).

Per altre informazioni sul backup di macchine virtuali o altri carichi di lavoro, vedere:

* [Eseguire il backup di macchine virtuali IaaS](backup-azure-vms-prepare.md)
* [Eseguire il backup dei carichi di lavoro tooAzure con il Server di Backup di Microsoft Azure](backup-azure-microsoft-azure-backup.md)
* [Eseguire il backup dei carichi di lavoro tooAzure con Data Protection Manager](backup-azure-dpm-introduction.md)
