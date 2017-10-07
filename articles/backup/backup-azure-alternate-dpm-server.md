---
title: aaaRecover dati da un Server di Backup di Azure | Documenti Microsoft
description: "Ripristinare i dati di hello è stato protetto da qualsiasi insieme di credenziali di Azure Backup Server registrati toothat insieme di credenziali di servizi di ripristino tooa."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Ripristinare i dati da un server di Backup di Azure
È possibile utilizzare dati di Azure Backup Server hello toorecover che hai eseguito un backup tooa che insieme di credenziali di servizi di ripristino. processo Hello per eseguire queste così è integrata nella console di gestione di Azure Backup Server hello e toohello ripristino flusso di lavoro simile per altri componenti di Azure Backup.

> [!NOTE]
> In questo articolo è applicabile per [System Center Data Protection Manager 2012 R2 con aggiornamento cumulativo 7 o versioni successive] (https://support.microsoft.com/en-us/kb/3065246), combinato con hello [più recenti dell'agente Azure Backup](http://aka.ms/azurebackup_agent).
>
>

toorecover dati da un Server di Backup di Azure:

1. Da hello **ripristino** fare clic sulla scheda della console di gestione di Server di Backup di Azure, hello **'Aggiungi DPM esterno'** (in hello in alto a sinistra della schermata di hello).   
    ![Aggiungi DPM esterno](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Nuovo download **archivio credenziali** dall'insieme di credenziali hello associato hello **Azure Backup Server** in fase di ripristino dati hello, scegliere hello Azure Backup Server dall'elenco di hello del server di Backup di Azure registrato con l'insieme di credenziali di servizi di ripristino hello e fornire hello **passphrase di crittografia** associato hello server i cui dati da ripristinare.

    ![Credenziali DPM esterne](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Solo i server di Backup di Azure associato hello stesso insieme di credenziali di registrazione è possibile ripristinare i dati.
   >
   >

    Una volta hello esterno i Server di Backup di Azure è stato correttamente aggiunto, è possibile esplorare i dati di hello del server esterno hello e hello locale Server di Backup di Azure da hello **ripristino** scheda.
3. Pulsante Sfoglia hello disponibili server di produzione protetti da hello esterno i Server di Backup di Azure e selezionare l'origine dati appropriata hello.

    ![Cercare nel Server DPM esterno](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Selezionare **hello mese e anno** da hello **punti di ripristino** elenco a discesa, seleziona hello necessario **Data ripristino** per quando il punto di ripristino hello è stato creato e seleziona hello **Tempo di recupero**.

    Nel riquadro inferiore hello, che può essere visualizzato e recuperati tooany percorso viene visualizzato un elenco di file e cartelle.

    ![Punti di ripristino del Server DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Fare clic con il pulsante destro elemento appropriato hello e fare clic su **ripristinare**.

    ![Ripristino DPM esterno](./media/backup-azure-alternate-dpm-server/recover.png)
6. Hello revisione **selezione ripristinare**. Verificare i dati hello e tempo hello copia di backup da ripristinare, nonché origine hello da cui è stato creato il backup hello. Se la selezione hello non è corretta, fare clic su **Annulla** un punto di ripristino appropriato tooselect scheda toonavigate toorecovery indietro. Se la selezione hello è corretta, fare clic su **Avanti**.

    ![Riepilogo del ripristino DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Selezionare **recuperare un percorso alternativo tooan**. **Sfoglia** toohello posizione corretta per il ripristino di hello.

    ![Posizione alternativa del ripristino DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Scegliere l'opzione hello correlati troppo**creare copia**, **Skip**, o **sovrascrittura**.

   * **Creare una copia** -crea una copia del file hello se è presente un conflitto di nomi.
   * **Ignora** : se si verifica un conflitto di nome, non viene ripristinato il file hello in modo da lasciare file originale hello.
   * **Sovrascrivere** : se si verifica un conflitto di nome, hello copia esistente del file hello.

     Opzione hello appropriato troppo**Ripristina protezione**. È possibile applicare le impostazioni di sicurezza hello hello computer di destinazione in cui viene ripristinati dati hello o le impostazioni di sicurezza hello che sono stati tooproduct applicabile in fase di hello è stato creato il punto di ripristino hello.

     Identificare se un **notifica** viene inviata, dopo il ripristino di hello è stata completata correttamente.

     ![Notifiche di ripristino DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Hello **riepilogo** dello schermo sono elencate le opzioni di hello scelte finora. Quando si fa clic su **'Ripristina'**, dati hello sono percorso locale appropriato toohello ripristinato.

    ![Riepilogo opzioni di ripristino DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > il processo di ripristino Hello può essere monitorato nel hello **monitoraggio** scheda di hello Azure Backup Server.
   >
   >

    ![Monitoraggio del ripristino](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. È possibile fare clic su **Cancella DPM esterno** su hello **ripristino** scheda della vista hello tooremove del server DPM del server DPM esterno hello hello.

    ![Deselezionare DPM esterno](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Risoluzione dei problemi relativi a messaggi di errore
| di serie | Messaggio di errore | Passaggi per la risoluzione dei problemi |
|:---:|:--- |:--- |
| 1. |Questo server non è registrato toohello insieme di credenziali specificato dall'insieme di credenziali hello. |**Causa:** questo errore viene visualizzato quando il file delle credenziali dell'insieme di credenziali hello selezionato non appartiene toohello insieme di credenziali di servizi di ripristino associati Server di Backup di Azure in cui hello viene eseguito un tentativo di ripristino. <br> **Risoluzione:** file delle credenziali dell'insieme di credenziali hello Download da hello toowhich insieme di credenziali per servizi di ripristino di hello è registrato il Server di Backup di Azure. |
| 2. |I dati ripristinabili hello non sono disponibili o server di hello selezionato non è un server DPM. |**Causa:** non esistono alcun altri server di Backup di Azure toohello registrati servizi di ripristino dell'insieme di credenziali, server hello non sono ancora stati caricati metadati hello o server di hello selezionato non è un Server di Backup di Azure (anche noto come Windows Server o Client Windows). <br> **Risoluzione:** se sono presenti altri insieme di credenziali di Azure Backup server registrati toohello servizi di ripristino, verificare che l'agente Azure Backup più recente hello è installato. <br>Se sono presenti credenziali di servizi di ripristino toohello registrati altri server di Backup di Azure, attendere per un giorno dopo il processo di ripristino di installazione toostart hello. processo notturno Hello caricherà hello metadati per tutti hello protetto backup toocloud. dati Hello saranno disponibili per il ripristino. |
| 3. |Nessun altro server DPM è toothis registrato dell'insieme di credenziali. |**Causa:** non sono presenti altri server di Backup di Azure che sono registrati toohello insieme di credenziali da quale hello è effettuati i tentativi di ripristino.<br>**Risoluzione:** se sono presenti altri insieme di credenziali di Azure Backup server registrati toohello servizi di ripristino, verificare che l'agente Azure Backup più recente hello è installato.<br>Se sono presenti credenziali di servizi di ripristino toohello registrati altri server di Backup di Azure, attendere per un giorno dopo il processo di ripristino di installazione toostart hello. processo notturno Hello carica i metadati di hello per tutti i backup protetti toocloud. dati Hello saranno disponibili per il ripristino. |
| 4. |Hello passphrase di crittografia fornita non corrisponde alla passphrase associata hello server seguenti:**<server name>** |**Causa:** hello passphrase di crittografia fornita non corrisponde a hello passphrase di crittografia utilizzata nel processo di hello di crittografare i dati di hello dai dati del Server di hello Azure Backup da ripristinare. l'agente Hello è dati hello toodecrypt non è possibile. Di conseguenza hello recupero non riesce.<br>**Risoluzione:** fornire hello esatta stessa passphrase di crittografia associata hello Azure Backup Server i cui dati da ripristinare. |

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Perché non è possibile aggiungere un server DPM esterno dopo l'installazione di UR7 e dell'agente Azure Backup più recente?

Per hello i server DPM con origini dati che sono protetti toohello cloud (utilizzando un aggiornamento cumulativo anteriori al primo aggiornamento cumulativo 7), è necessario attendere almeno un giorno dopo l'installazione di hello UR7 e più recenti dell'agente Azure Backup, toostart **server Aggiungi DPM esterno** . Hello un giorno periodo di tempo è necessario tooupload hello metadati di tooAzure di gruppi protezione dati DPM hello. Metadati del gruppo protezione dati viene caricato hello prima volta attraverso un processo notturno.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Qual è la versione minima di hello dell'agente di servizi di ripristino di Microsoft Azure hello necessita?

versione minima di Hello di agente di servizi di ripristino di Microsoft Azure hello o agente di Backup di Azure, tooenable richiesto questa funzionalità è 2.0.8719.0.  versione dell'agente di hello tooview: aprire il pannello di controllo  **>**  gli elementi del Pannello di controllo tutti  **>**  programmi e funzionalità  **>**  Agente di servizi di ripristino di Microsoft Azure. Se la versione hello minore 2.0.8719.0, scaricare e installare hello [più recenti dell'agente Azure Backup](https://go.microsoft.com/fwLink/?LinkID=288905).

![Deselezionare DPM esterno](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Passaggi successivi:
[Domande frequenti su Backup di Azure](backup-azure-backup-faq.md)
