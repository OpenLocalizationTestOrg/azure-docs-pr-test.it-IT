---
title: 'Azure AD Connect: Eseguire l''aggiornamento da una versione precedente | Documentazione Microsoft'
description: "Illustra hello diversi metodi tooupgrade toohello versione più recente di Azure Active Directory Connect, tra cui un aggiornamento sul posto e una migrazione di attività."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: L'aggiornamento da un precedente toohello versione più recente
Questo argomento descrive i diversi metodi hello che è possibile utilizzare tooupgrade la versione più recente di installazione toohello Connect di Azure Active Directory (Azure AD). È consigliabile mantenere manualmente corrente con le versioni di hello di Azure AD Connect. È inoltre utilizzare i passaggi di hello hello [ruotare migrazione](#swing-migration) sezione quando si esegue una configurazione sostanziale di modifica.

Se si desidera tooupgrade da DirSync, vedere [l'aggiornamento da strumento di sincronizzazione di Azure Active Directory (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) invece.

Sono disponibili alcuni diverse strategie che è possibile utilizzare tooupgrade Azure AD Connect.

| Metodo | Descrizione |
| --- | --- |
| [Aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) |Si tratta hello metodo più semplice per i clienti con un'installazione rapida. |
| [Aggiornamento sul posto](#in-place-upgrade) |Se si dispone di un singolo server, è possibile aggiornare sul posto installazione hello in hello nello stesso server. |
| [Migrazione swing](#swing-migration) |Con due server, è possibile preparare uno dei server hello alla nuova versione di hello o alla configurazione e modificare i server attivo hello quando si è pronti. |

Per informazioni sulle autorizzazioni, vedere hello [delle autorizzazioni necessarie per un aggiornamento](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Dopo aver attivato la nuova Azure AD Connect server toostart sincronizzazione modifiche tooAzure Active Directory, è necessario non eseguire il rollback toousing DirSync o Azure AD Sync. Downgrade da Azure AD Connect toolegacy client, tra cui DirSync e Azure AD Sync, non è supportato e può causare tooissues, ad esempio la perdita di dati in Azure AD.

## <a name="in-place-upgrade"></a>Aggiornamento sul posto
Un aggiornamento sul posto è indicato per il passaggio da Azure AD Sync o Azure AD Connect. Non è possibile usarlo per lo spostamento da DirSync o per una soluzione con Forefront Identity Manager (FIM) e Azure AD Connect.

Questo metodo è preferibile quando sono presenti un singolo server e meno di 100.000 oggetti. Se sono state apportate modifiche regole di sincronizzazione di out-of-box toohello, un'importazione completa e una sincronizzazione completa si verificano dopo l'aggiornamento di hello. Questo metodo garantisce che la nuova configurazione hello oggetti esistenti tooall applicato nel sistema hello. L'esecuzione potrebbe richiedere alcune ore, in base al numero di hello di oggetti che rientrano nell'ambito del motore di sincronizzazione hello. pianificazione di sincronizzazione delta normale Hello (che sincronizza ogni 30 minuti per impostazione predefinita) viene sospeso, ma continua la sincronizzazione delle password. È possibile eseguire l'aggiornamento sul posto di hello durante un fine settimana. Se sono non presenti alcuna configurazione di out-of-box toohello modifiche con versione di hello nuovo Azure AD Connect, quindi un normale importazione/sincronizzazione delta inizia invece.  
![Aggiornamento sul posto](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Se sono state apportate le modifiche delle regole di sincronizzazione di out-of-box toohello, queste regole sono impostare nuovamente configurazione predefinita toohello l'aggiornamento. toomake assicurarsi che la configurazione viene mantenuta tra gli aggiornamenti, assicurarsi che si apportano modifiche come essi è descritto in [procedure consigliate per la modifica della configurazione predefinita di hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Durante l'aggiornamento sul posto, potrebbero esserci modifiche introdotte che richiedono una sincronizzazione specifica le attività (inclusi i passaggi di importazione completa e la sincronizzazione completa) toobe eseguito dopo il completamento dell'aggiornamento. toodefer tali attività, fare riferimento toosection [come toodefer completa la sincronizzazione dopo l'aggiornamento](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Migrazione swing
Se si dispone di una distribuzione complessa o molti oggetti, potrebbe essere poco toodo un aggiornamento sul posto nel sistema in tempo reale hello. Per alcuni clienti questa procedura potrebbe richiedere più giorni, durante i quali non verranno elaborate modifiche differenziali. È inoltre possibile utilizzare questo metodo quando si pianifica toomake modifiche sostanziali tooyour configurazione e si desidera tootry loro out queste sta inviate toohello cloud.

metodo per questi scenari consigliato Hello è toouse una migrazione di attività. Sono necessari almeno due server, uno attivo e uno di staging. ASP Hello (visualizzati con linee blue continue nella seguente immagine hello) è responsabile per il carico di produzione attivo hello. Hello (visualizzata con le linee tratteggiate viola) di server di gestione temporanea è pronti alla nuova versione di hello o alla configurazione. Quando la preparazione è completa, il server viene reso attivo. Hello active server precedente, che ora ha hello configurazione installato o versione precedente, viene eseguita nel server di gestione temporanea hello e viene aggiornato.

due server Hello possono usare versioni diverse. Ad esempio, ASP hello pianificare toodecommission possono usare Azure AD Sync e server di gestione temporanea nuovo hello è possibile utilizzare Azure AD Connect. Se si utilizzano attività migrazione toodevelop una nuova configurazione, è una buona idea toohave hello le stesse versioni in hello due server.  
![server di gestione temporanea](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Alcuni utenti preferiscono toohave tre o quattro server per questo scenario. Quando viene aggiornato hello server di gestione temporanea, non è un server di backup per [il ripristino di emergenza](active-directory-aadconnectsync-operations.md#disaster-recovery). Con tre o quattro server, è possibile preparare un insieme di server primario/in standby con hello nuova versione, che garantisce che sia sempre un server di gestione temporanea che è pronto tootake su.

Questa procedura funziona anche toomove da Azure AD Sync o una soluzione con FIM + Azure Active Directory Connector. Questi passaggi non funzionano per DirSync, ma è hello stesso secondo metodo di migrazione (detto anche distribuzione in parallelo) con i passaggi per DirSync [sincronizzazione aggiornare Azure Active Directory (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Utilizzare un tooupgrade di migrazione di attività
1. Se si utilizza Azure AD Connect nel server e verificare tooonly piano una modifica della configurazione, assicurarsi che il server attivo e il server di gestione temporanea sono entrambi utilizzando hello stessa versione. In questo modo più semplice toocompare differenze in un secondo momento. Se si esegue l'aggiornamento da Azure AD Sync, questi server hanno versioni diverse. Se si esegue l'aggiornamento da una versione precedente di Azure AD Connect, è toostart una buona idea con server hello due utilizzando hello stessa versione, ma non è obbligatorio.
2. Se sono state apportate a una configurazione personalizzata e il server di gestione temporanea non sia utilizzato, effettuare le operazioni di hello in [spostare una configurazione personalizzata dal server di gestione temporanea di hello server attivo toohello](#move-custom-configuration-from-active-to-staging-server).
3. Se si esegue l'aggiornamento da una versione precedente di Azure AD Connect, aggiornare hello versione più recente toohello del server di gestione temporanea. Se si esegue lo spostamento da Azure AD Sync, installare Azure AD Connect nel server di staging.
4. Consentire l'importazione completa di hello sincronizzazione motore di esecuzione e la sincronizzazione completa nel server di gestione temporanea.
5. Verificare che la nuova configurazione hello non causa ulteriori modifiche impreviste attenendosi alla procedura hello in "Verifica" in [configurazione hello verifica di un server](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Se un elemento non è corretto, come previsto, eseguire l'importazione di hello e sincronizzazione e verificare dati hello fino a quando non risulta valida, seguendo i passaggi di hello.
6. Passare hello server attivo hello toobe di server di gestione temporanea. Questo è il passaggio finale hello "Server attivo Switch" [configurazione hello verifica di un server](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Se si esegue l'aggiornamento di Azure AD Connect, aggiornare i server di hello che è a questo punto di gestione temporanea nella versione più recente di modalità toohello. Seguire hello stessi passaggi prima i dati di hello tooget e la configurazione aggiornata. Se si esegue l'aggiornamento da Azure AD Sync, è possibile disattivare e rimuovere le autorizzazioni dal server precedente.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Spostare una configurazione personalizzata dal server di gestione temporanea di hello ASP toohello
Se sono state apportate server attivo toohello modifiche di configurazione, è necessario toomake assicurarsi che hello stesso le modifiche vengono applicata toohello server di gestione temporanea. spostare toohelp con questo oggetto, è possibile utilizzare hello [analizzatore di configurazione di Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

È possibile spostare le regole di sincronizzazione personalizzata hello che è stato creato tramite PowerShell. È necessario applicare altri hello modifiche allo stesso modo in entrambi i sistemi ed è possibile eseguire la migrazione di modifiche hello. Hello [analizzatore configurazione](https://github.com/Microsoft/AADConnectConfigDocumenter) consentono di confrontare due hello sistemi toomake siano identici. strumento Hello inoltre consente di automatizzare i passaggi di hello riportati in questa sezione.

È necessario tooconfigure hello segue operazioni hello stesso modo in entrambi i server:

* Connessione toohello stesso foreste
* Domini e filtri unità organizzativa
* Hello stessa funzionalità facoltative, ad esempio la sincronizzazione delle password e il writeback delle password

**Spostare le regole di sincronizzazione personalizzate**  
regole di sincronizzazione toomove, hello seguenti:

1. Aprire l' **editor delle regole di sincronizzazione** nel server attivo.
2. Selezionare una regola personalizzata. Fare clic su **Esporta**. Viene visualizzata una finestra del Blocco note. Salvare il file temporaneo hello con estensione PS1. In questo modo diventa uno script PowerShell. Copiare toohello di file PS1 hello server di gestione temporanea.  
   ![Esportazione delle regole di sincronizzazione](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hello connettore GUID è diverso nel server di gestione temporanea hello ed è necessario modificarla. avviare tooget hello GUID, **Editor regole di sincronizzazione**, selezionare una delle regole di out-of-box hello hello che rappresentano stesso sistema connesso e fare clic su **esportare**. Sostituisci hello GUID dal server di gestione temporanea hello hello GUID nel file PS1.
4. In un prompt dei comandi di PowerShell, eseguire il file di hello PS1. Questo crea regola di sincronizzazione personalizzata hello hello server di gestione temporanea.
5. Ripetere la procedura per tutte le regole personalizzate.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Come toodefer completa la sincronizzazione dopo l'aggiornamento
Durante l'aggiornamento sul posto, potrebbero esserci modifiche introdotte che richiedono toobe (inclusi i passaggi di importazione completa e la sincronizzazione completa) attività di sincronizzazione specifica eseguita. Ad esempio, le modifiche dello schema connettore richiedono **importazione completa** richiedono modifiche alle regole di sincronizzazione di passaggio e out-of-box **completo sincronizzazione** passaggio toobe eseguita sui connettori interessati. Durante l'aggiornamento, Azure AD Connect determina le attività di sincronizzazione necessarie e le registra come *sostituzioni*. In hello successivo ciclo di sincronizzazione, l'utilità di pianificazione sincronizzazione hello preleva le sostituzioni e li esegue. Dopo essere state eseguite, le sostituzioni vengono rimosse.

Potrebbero verificarsi situazioni in cui non si desidera sul posto tootake tali sostituzioni immediatamente dopo l'aggiornamento. Ad esempio, si dispone di numerosi oggetti sincronizzati e si desidera questi toooccur passaggi di sincronizzazione dopo l'orario lavorativo. tooremove queste sostituzioni:

1. Durante l'aggiornamento, **deselezionare** hello opzione **avviare il processo di sincronizzazione di hello al termine della configurazione**. Ciò disabilita l'utilità di pianificazione sincronizzazione hello e impedisce ciclo di sincronizzazione eseguita automaticamente prima che vengano rimossi hello sostituzioni.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Al termine dell'aggiornamento, eseguire hello toofind cmdlet out sono state aggiunte le sostituzioni seguenti:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > sostituzioni Hello sono specifiche del connettore. In hello riportato, i passaggi di importazione completa e la sincronizzazione completa sono state aggiunte hello tooboth connettore di Active Directory in locale e Azure Active Directory Connector.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Prendere nota delle sostituzioni esistenti hello che sono stati aggiunti.
   
4. esegue l'override hello tooremove per importazione completa e la sincronizzazione completa su un connettore arbitrario, eseguire hello seguente cmdlet:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   sostituzioni hello tooremove su tutti i connettori, eseguire lo script di PowerShell seguente hello:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello dell'utilità di pianificazione, eseguire hello seguente cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Tenere presente i passaggi di sincronizzazione hello necessario tooexecute appena. È possibile manualmente eseguire questi passaggi tramite hello Synchronization Service Manager o aggiungere sostituzioni hello utilizzando il cmdlet Set-ADSyncSchedulerConnectorOverride hello.

esegue l'override hello tooadd per importazione completa e la sincronizzazione completa su un connettore arbitrario, eseguire hello seguente cmdlet:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
