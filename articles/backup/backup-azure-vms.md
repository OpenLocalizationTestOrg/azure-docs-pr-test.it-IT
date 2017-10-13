---
title: Eseguire il backup di macchine virtuali di Azure distribuite con il modello di distribuzione classica in un insieme di credenziali per il backup | Documentazione Microsoft
description: Individuare, registrare ed eseguire il backup delle macchine virtuali usando queste procedure per il backup di macchine virtuali di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup della macchina virtuale; eseguire il backup della macchina virtuale; backup e ripristino di emergenza; backup di vm
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Eseguire il backup di macchine virtuali di Azure (portale classico)
> [!div class="op_single_selector"]
> * [Eseguire il backup di macchine virtuali in un insieme di credenziali di Servizi di ripristino](backup-azure-arm-vms.md)
> * [Eseguire il backup di macchine virtuali in un insieme di credenziali per il backup](backup-azure-vms.md)
>
>

Questo articolo include le procedure per eseguire il backup di una macchina virtuale di Azure distribuita con il modello di distribuzione classica in un insieme di credenziali per il backup. Prima di poter eseguire il backup di una macchina virtuale di Azure, è necessario occuparsi di alcune attività. Se non è già stato fatto, completare i [prerequisiti](backup-azure-vms-prepare.md) per preparare l'ambiente per il backup delle macchine virtuali.

Per altre informazioni, vedere gli articoli [Pianificare l'infrastruttura di backup delle macchine virtuali in Azure](backup-azure-vms-introduction.md) e [Macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Un insieme di credenziali per il backup consente di proteggere solo macchine virtuali distribuite con il modello di distribuzione classica. Non è possibile proteggere le macchine virtuali distribuite con il modello di distribuzione Resource Manager usando un insieme di credenziali per il backup. Per informazioni dettagliate sull'utilizzo di insiemi di credenziali di Servizi di ripristino, vedere [Eseguire il backup di macchine virtuali in un insieme di credenziali di Servizi di ripristino](backup-azure-arm-vms.md) .
>
>

L'esecuzione del backup di macchine virtuali di Azure prevede tre passaggi principali:

![Tre passaggi per eseguire il backup di una macchina virtuale IaaS di Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Il backup di macchine virtuali è un processo locale. Non è possibile eseguire il backup di macchine virtuali di un'area in un insieme di credenziali per il backup in un'altra area. È quindi necessario creare un insieme di credenziali per il backup in ogni area di Azure dove sono presenti VM di cui sarà seguito il backup.
>
> [!IMPORTANT]
> A partire da marzo 2017, non è più possibile usare il portale classico per creare insiemi di credenziali di backup.
> È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino. Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.<br/> Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup. **Entro il 1° novembre 2017**:
>- Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.
>- e non sarà più possibile accedere ai dati di backup nel portale classico. Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Passaggio 1: Individuare le macchine virtuali di Azure
Per assicurarsi che prima della registrazione vengano identificate le eventuali nuove macchine virtuali (VM) aggiunte alla sottoscrizione, eseguire il processo di individuazione. Il processo esegue una query su Azure per ottenere l'elenco delle macchine virtuali disponibili nella sottoscrizione, insieme ad altre informazioni come il nome del servizio cloud e l'area.

1. Accedere al [portale classico](http://manage.windowsazure.com/)
2. Nell'elenco di servizi di Azure, fare clic su **Servizi di ripristino** per aprire l'elenco degli insiemi di credenziali per il backup e Site Recovery.
    ![Elenco dell'insieme di credenziali](./media/backup-azure-vms/choose-vault-list.png)
3. Nell'elenco degli insiemi di credenziali di Backup, selezionare l'insieme di credenziali per eseguire il backup di una macchina virtuale.

    Se si tratta di un nuovo insieme di credenziali, nel portale verrà aperta la pagina **Avvio rapido** .

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-quick-start.png)

    Se in precedenza è stato configurato l'insieme di credenziali, il portale apre il menu usato più di recente.
4. Nel menu dell'insieme di credenziali nella parte superiore della pagina fare clic su **Elementi registrati**.

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-menu.png)
5. Scegliere **Macchina virtuale di Azure** dal menu **Tipo**.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. Fare clic su **INDIVIDUA** nella parte inferiore della pagina.
    ![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)

    Il processo di individuazione può richiedere alcuni minuti mentre le macchine virtuali vengono elencate in formato tabulare. Nella parte inferiore della schermata è presente una notifica che indica che il processo è in esecuzione.

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    Al termine del processo, la notifica cambia. Se il processo di individuazione non riesce a trovare le macchine virtuali, verificare innanzitutto che le macchine virtuali esistano. Se le macchine virtuali esistono, verificare che si trovino nella stessa area dell'insieme di credenziali di backup. Se le macchine virtuali esistono e si trovano nella stessa area, verificare che non sono già registrate in un insieme di credenziali di backup. Se una macchina virtuale viene assegnata a un insieme di credenziali di backup, non è possibile assegnarla ad altri insiemi di credenziali di backup.

    ![Individuazione completata](./media/backup-azure-vms/discovery-complete.png)

    Dopo aver individuato i nuovi elementi, andare al passaggio 2 e registrare le macchine virtuali.

## <a name="step-2---register-azure-virtual-machines"></a>Passaggio 2: Registrare le macchine virtuali di Azure
Si registra una macchina virtuale di Azure per associarla al servizio Backup di Azure. Questa attività viene in genere eseguita una sola volta.

1. Passare all'insieme di credenziali per il backup disponibile in **Servizi di ripristino** nel portale di Azure, quindi fare clic su **Elementi registrati**.
2. Selezionare **Macchina virtuale di Azure** dal menu a discesa.

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
3. Fare clic su **REGISTRA** nella parte inferiore della pagina.
    ![Pulsante Registra](./media/backup-azure-vms/register-button-only.png)
4. Nel menu di scelta rapida **Registra elementi** selezionare le macchine virtuali da registrare. Se sono presenti due o più macchine virtuali con lo stesso nome, usare il servizio cloud per distinguerle.

   > [!TIP]
   > È possibile registrare più macchine virtuali contemporaneamente.
   >
   >

    Viene creato un processo per ogni macchina virtuale selezionata.
5. Fare clic su **Visualizza processo** nella notifica per passare alla pagina **Processi**.

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    La macchina virtuale viene visualizzata anche nell'elenco di elementi registrati insieme allo stato dell'operazione di registrazione.

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    Al termine dell'operazione, lo stato diventerà *Registrazione completata* per riflettere la modifica.

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Passaggio 3: Proteggere le macchine virtuali di Azure
Ora è possibile configurare i criteri di backup e conservazione per la macchina virtuale. È possibile proteggere più macchine virtuali usando una singola operazione.

Gli insiemi di credenziali di Backup di Azure creati dopo maggio 2015 includono criteri predefiniti. Questi criteri predefiniti prevedono un periodo di conservazione predefinito di 30 giorni e una pianificazione per il backup una volta al giorno.

1. Passare all'insieme di credenziali per il backup disponibile in **Servizi di ripristino** nel portale di Azure, quindi fare clic su **Elementi registrati**.
2. Selezionare **Macchina virtuale di Azure** dal menu a discesa.

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. Fare clic su **PROTEGGI** nella parte inferiore della pagina.

    Verrà visualizzata la procedura guidata **Proteggi elementi** . La procedura guidata elenca solo le macchine virtuali registrate e non protette. Selezionare le macchine virtuali da proteggere.

    Se sono presenti due o più macchine virtuali con lo stesso nome, usare il servizio cloud per distinguere tra le macchine virtuali.

   > [!TIP]
   > È possibile proteggere più macchine virtuali contemporaneamente.
   >
   >

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)

4. Scegliere una **pianificazione per il backup** per eseguire il backup delle macchine virtuali selezionate. È possibile scegliere da un set di criteri esistenti o definirne di nuovi.

    Ai singoli criteri di backup possono essere associate più macchine virtuali. Una macchina virtuale può tuttavia essere associata a un solo criterio in un dato momento.

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > I criteri di backup includono uno schema di conservazione per i backup pianificati. Se si selezionano criteri di backup esistenti, non si potranno modificare le opzioni di conservazione nel passaggio successivo.
   >
   >

5. Scegliere un **intervallo di conservazione** da associare ai backup.

    ![Proteggere con criteri di conservazione flessibili](./media/backup-azure-vms/policy-retention.png)

    I criteri di conservazione specificano il periodo di tempo per l'archiviazione di una copia di backup. È possibile specificare criteri di conservazione diversi in base alla momento in cui viene eseguito il backup. Ad esempio, un punto di backup eseguito quotidianamente, che funge da punto di ripristino operativo, può essere conservato per 90 giorni. Diversamente, è possibile che un punto di backup eseguito alla fine di ogni trimestre, a scopo di controllo, debba essere conservato per molti mesi o anni.

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    In questa immagine di esempio:

   * **Criteri di conservazione giornaliera**: i backup eseguiti ogni giorno vengono archiviati per 30 giorni.
   * **Criteri di conservazione settimanale**: i backup eseguiti ogni domenica vengono conservati per 104 settimane.
   * **Criteri di conservazione mensile**: i backup eseguiti l'ultima domenica di ogni mese vengono conservati per 120 mesi.
   * **Criteri di conservazione annuale**: i backup eseguiti la prima domenica di gennaio di ogni anno vengono conservati per 99 anni.

     Viene creato un processo per configurare i criteri di protezione e associare ogni macchina virtuale selezionata a questi criteri.
6. Per visualizzare l'elenco di processi di **Configura protezione**, fare clic su **Processi** dal menu degli insiemi di credenziali e selezionare **Configura protezione** nel filtro **Operazione**.

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Backup iniziale
Dopo avere applicato i criteri di protezione alla macchina virtuale, questa verrà visualizzata nella scheda **Elementi protetti** e avrà lo stato *Protetto (backup iniziale in sospeso)*. Per impostazione predefinita, il primo backup pianificato è il *backup iniziale*.

Per attivare il backup iniziale immediatamente dopo la configurazione della protezione:

1. Nella parte inferiore della pagina **Elementi protetti** fare clic su **Backup Now** (Esegui backup ora).

    Il servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale.
2. Fare clic sulla scheda **Processi** per visualizzare l'elenco dei processi.

    ![Backup in progress](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Come parte dell'operazione di backup, il servizio Backup di Azure invia un comando all'estensione per il backup in ogni macchina virtuale, per scaricare tutti processi di scrittura e acquisire uno snapshot coerente.
>
>

Al termine del backup iniziale, lo stato della macchina virtuale nella scheda **Elementi protetti** sarà *Protetto*.

![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Visualizzazione dello stato di backup e dei relativi dettagli
Dopo la protezione, il numero di macchine virtuali aumenta anche nella pagina di riepilogo **Dashboard** . Anche la pagina **Dashboard** mostra il numero di processi *completati*, *non riusciti* e *in corso* nell'arco delle ultime 24 ore. Nella pagina **Processi** usare i menu **Stato**, **Operazione** o **Da** e **A** per filtrare i processi.

![Status of backup in Dashboard page](./media/backup-azure-vms/dashboard-protectedvms.png)

I valori nel dashboard vengono aggiornati ogni 24 ore.

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi
In caso di problemi durante il backup della macchina virtuale, vedere l'articolo [Risolvere i problemi relativi al backup delle macchine virtuali di Azure](backup-azure-vms-troubleshoot.md) per assistenza.

## <a name="next-steps"></a>Passaggi successivi
* [Gestire e monitorare il backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
* [Ripristino di macchine virtuali](backup-azure-restore-vms.md)
