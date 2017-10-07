---
title: 'Azure AD Connect: aggiornamento da DirSync | Documentazione Microsoft'
description: Informazioni su come tooupgrade da DirSync tooAzure AD Connect. In questo articolo descrive i passaggi di hello per l'aggiornamento da DirSync tooAzure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: aggiornamento da DirSync
Azure AD Connect è tooDirSync successore hello. Trovare un modo hello che è possibile eseguire l'aggiornamento da DirSync in questo argomento. Questi passaggi non si applicano all'aggiornamento da un'altra versione di Azure AD Connect o da Azure AD Sync.

Prima di iniziare l'installazione di Azure AD Connect, verificare che sia troppo[scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e prerequisito hello completato i passaggi [Azure AD Connect: prerequisiti Hardware e](active-directory-aadconnect-prerequisites.md). In particolare, si desidera tooread sulle seguenti hello, poiché queste aree sono diverse da DirSync:

* versione richiesta di Hello di .net e PowerShell. Le versioni più recenti sono necessari toobe nel server di hello rispetto a quanto necessario DirSync.
* configurazione del server proxy Hello. Se si utilizza un tooreach server proxy internet hello, questa impostazione deve essere configurata prima dell'aggiornamento. DirSync sempre usato come server proxy hello configurata per l'utente hello l'installazione, ma le impostazioni del computer di Azure AD Connect utilizza invece.
* Hello gli URL necessari toobe aperti nel server di proxy hello. Per scenari di base, gli scenari supportati anche da DirSync, i requisiti di hello sono hello stesso. Se si desidera toouse hello nuove funzionalità incluse con Azure AD Connect, alcuni nuovi URL deve essere aperto.

> [!NOTE]
> Dopo aver abilitato la nuova Azure AD Connect server toostart sincronizzazione modifiche tooAzure Active Directory, è necessario non eseguire il rollback toousing DirSync o Azure AD Sync. Downgrade da Azure AD Connect toolegacy client inclusi DirSync e Azure AD Sync non è supportato e può causare tooissues, ad esempio la perdita di dati in Azure AD.

Se non si esegue l'aggiornamento da DirSync, vedere la [documentazione correlata](#related-documentation) per altri scenari.

## <a name="upgrade-from-dirsync"></a>Aggiornamento da DirSync
In base alla distribuzione corrente di DirSync, esistono diverse opzioni per l'aggiornamento di hello. Se hello prevede tempi di aggiornamento sono inferiore a tre ore, indicazione hello è toodo un aggiornamento sul posto. Se hello prevede tempi di aggiornamento sono superiore a tre ore, indicazione hello è toodo una distribuzione in parallelo in un altro server. Si prevede che se si dispone di più di 50.000 oggetti occorre più di tre ore toodo hello aggiornamento.

| Scenario |
| --- | --- |
| [Aggiornamento sul posto](#in-place-upgrade) |
| [Distribuzione parallela](#parallel-deployment) |

> [!NOTE]
> Quando si pianifica tooupgrade da DirSync tooAzure AD Connect, non disinstallare DirSync manualmente prima dell'aggiornamento hello. Azure AD Connect di lettura e la migrazione della configurazione hello da DirSync e disinstallazione dopo aver esaminato server hello.

**Aggiornamento sul posto**  
Hello è previsto l'aggiornamento di hello toocomplete ora viene visualizzata dalla procedura guidata hello. Questa stima si basa sul presupposto hello che accetta tre ore toocomplete un aggiornamento per un database con 50.000 oggetti (utenti, contatti e gruppi). Se il numero di hello di oggetti nel database è minore di 50.000, Azure AD Connect consiglia un aggiornamento sul posto. Se si decide di toocontinue, le impostazioni correnti vengono applicate automaticamente durante l'aggiornamento e il server riprende automaticamente una sincronizzazione con active.

Se si desidera toodo una migrazione della configurazione e la distribuzione parallela, è possibile ignorare l'indicazione di aggiornamento sul posto di hello. Ad esempio, si potrebbe richiedere hello opportunità toorefresh hello hardware e sistema operativo. Per ulteriori informazioni, vedere hello [parallela distribuzione](#parallel-deployment) sezione.

**Distribuzione parallela**  
Se sono disponibili più di 50.000 oggetti, è consigliabile eseguire una distribuzione parallela. La distribuzione consente di evitare eventuali ritardi operativi rilevati dagli utenti. Hello Azure AD Connect installazione tenta di tempi di inattività hello tooestimate per l'aggiornamento di hello, ma se è stato eseguito l'aggiornamento di DirSync in hello precedente, l'esperienza è probabilmente toobe Guida di best hello.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Supportato toobe di configurazioni di DirSync aggiornato
Hello dopo le modifiche di configurazione è supportata con DirSync aggiornato:

* Filtro unità organizzativa e dominio
* ID alternativo (UPN)
* Sincronizzazione password e impostazioni ibride di Exchange
* Impostazioni di Azure AD e di foresta/dominio
* Opzioni di filtro basate sugli attributi dell'utente

Impossibile aggiornare Hello successivo alla modifica. Se si dispone di questa configurazione, l'aggiornamento di hello viene bloccato:

* Modifiche di DirSync non supportate, ad esempio attributi rimossi e uso di una DLL di estensione personalizzata

![Aggiornamento bloccato](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

In questi casi, la raccomandazione hello è tooinstall un nuovo server di Azure AD Connect in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode) e verificare hello DirSync vecchia e nuova configurazione di Azure AD Connect. Riapplicare le modifiche usando la configurazione personalizzata, come descritto in [Configurazione personalizzata della sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md).

le password di Hello usate da DirSync per gli account del servizio hello non possono essere recuperate e non vengono migrate. Le password vengono reimpostate durante l'aggiornamento di hello.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Passaggi generali per l'aggiornamento da DirSync tooAzure AD Connect
1. Benvenuti tooAzure Active Directory Connect
2. Analisi della configurazione di DirSync corrente
3. Raccolta della password amministratore globale di Azure AD
4. Raccogliere le credenziali per un account di amministratore dell'organizzazione (solo durante l'installazione di hello di Azure AD Connect)
5. Installazione di Azure AD Connect
   * Disinstallare DirSync o disabilitarlo temporaneamente
   * Installare Azure AD Connect
   * Avviare facoltativamente la sincronizzazione

Nei casi seguenti sono necessari altri passaggi:

* Si usa attualmente una versione completa di SQL Server, locale o remota
* Nell'ambito si trovano più di 50.000 oggetti per la sincronizzazione

## <a name="in-place-upgrade"></a>Aggiornamento sul posto
1. Avviare Installazione guidata di hello Azure AD Connect (con estensione MSI).
2. Rivedere e accettare i termini di toolicense e informativa sulla privacy.  
   ![Benvenuto tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Fare clic su Avanti analysis toobegin dell'installazione esistente di DirSync.  
   ![Analisi dell'installazione della sincronizzazione di directory esistente](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Al termine dell'analisi di hello, visualizzare le raccomandazioni hello sul tooproceed.  
   * Se si utilizza SQL Server Express e si dispone di meno di 50.000 oggetti, verrà visualizzato hello seguente schermata:  
     ![Analisi completata tooupgrade pronti da DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Se si usa una versione completa di SQL Server per DirSync, viene invece visualizzata questa pagina:  
     ![Analisi completata tooupgrade pronti da DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     vengono visualizzate informazioni Hello riguardanti hello Server SQL server di database esistente viene usato da DirSync. Se necessario, apportare le modifiche appropriate. Fare clic su **Avanti** installazione hello toocontinue.
   * Se sono presenti più di 50.000 oggetti, viene invece visualizzata questa pagina:  
     ![Analisi completata tooupgrade pronti da DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed con un aggiornamento sul posto, fare clic su Avanti toothis messaggio di hello casella di controllo: **continua ad aggiornare DirSync in questo computer.**
     toodo un [parallela distribuzione](#parallel-deployment) , invece, si esporta impostazioni di configurazione di DirSync hello e spostare hello configurazione toohello nuovo server.
5. Specificare password hello per account hello che tooconnect tooAzure AD già in uso. Deve trattarsi di account hello attualmente usato da DirSync.  
   ![Immettere le credenziali di Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Se viene visualizzato un errore e si hanno problemi di connettività, vedere [Risolvere i problemi di connettività con Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Fornire un account amministratore dell'organizzazione per Active Directory.  
   ![Immettere le credenziali di ADDS.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. A questo punto si tooconfigure pronto. Quando si fa clic su **Aggiorna**, DirSync viene disinstallato e Azure AD Connect viene configurato e inizia la sincronizzazione.  
   ![Tooconfigure pronto](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Una volta completata l'installazione di hello, disconnettersi e accedere nuovamente tooWindows prima di usare Synchronization Service Manager, Editor regole di sincronizzazione, o provare toomake altre modifiche alla configurazione.

## <a name="parallel-deployment"></a>Distribuzione parallela
### <a name="export-hello-dirsync-configuration"></a>Esportare la configurazione di DirSync hello
**Distribuzione parallela con più di 50.000 oggetti**

Se si hanno più di 50.000 oggetti, hello Azure AD Connect installazione consiglia una distribuzione in parallelo.

Viene visualizzato un seguente toohello simile dello schermo:  
![Analisi completata](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Se si desidera tooproceed con distribuzione in parallelo, è necessario hello tooperform alla procedura seguente:

* Fare clic su hello **esportare impostazioni** pulsante. Quando si installa Azure AD Connect in un server distinto, queste impostazioni vengono migrate dall'installazione corrente di DirSync tooyour nuovo Azure AD Connect.

Una volta che le impostazioni sono state esportate correttamente, è possibile uscire dalla procedura guidata di Azure AD Connect hello nel server DirSync hello. Continuare con il passaggio successivo di hello troppo[installare Azure AD Connect in un server separato](#installation-of-azure-ad-connect-on-separate-server)

**Distribuzione parallela con meno di 50.000 oggetti**

Se si dispone di meno di 50.000 oggetti ma si desidera comunque toodo una distribuzione in parallelo, quindi hello seguenti:

1. Eseguire l'installazione di Azure AD Connect hello (MSI).
2. Quando viene visualizzato hello **tooAzure completamento dell'installazione di Active Directory Connect** schermata Esci hello installazione guidata, fare clic su "X" hello hello angolo superiore destro della finestra hello.
3. Aprire un prompt dei comandi.
4. Da hello installa posizione di Azure AD Connect (predefinita: C:\Program Files\Microsoft Azure Active Directory Connect) eseguire hello comando seguente: `AzureADConnect.exe /ForceExport`.
5. Fare clic su hello **esportare impostazioni** pulsante. Quando si installa Azure AD Connect in un server distinto, queste impostazioni vengono migrate dall'installazione corrente di DirSync tooyour nuovo Azure AD Connect.

![Analisi completata](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Una volta che le impostazioni sono state esportate correttamente, è possibile uscire dalla procedura guidata di Azure AD Connect hello nel server DirSync hello. Continuare con il passaggio successivo di hello troppo[installare Azure AD Connect in un server distinto](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Installare Azure AD Connect in un server separato
Quando si installa Azure AD Connect in un nuovo server, presupponendo hello è che si desidera tooperform un'installazione pulita di Azure AD Connect. Poiché si desidera che la configurazione di DirSync hello toouse, esistono tootake alcuni passaggi aggiuntivi:

1. Eseguire l'installazione di Azure AD Connect hello (MSI).
2. Quando viene visualizzato hello **tooAzure completamento dell'installazione di Active Directory Connect** schermata Esci hello installazione guidata, fare clic su "X" hello hello angolo superiore destro della finestra hello.
3. Aprire un prompt dei comandi.
4. Da hello installa posizione di Azure AD Connect (predefinita: C:\Program Files\Microsoft Azure Active Directory Connect) eseguire hello comando seguente: `AzureADConnect.exe /migrate`.
   installazione guidata di Hello Azure AD Connect verrà avviato e si presenta con hello seguente schermata:  
   ![Immettere le credenziali di Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Selezionare i file di impostazioni di hello esportate dall'installazione DirSync.
6. Configurare tutte le opzioni avanzate, tra cui:
   * Un percorso di installazione personalizzato per Azure AD Connect.
   * Un'istanza esistente di SQL Server (per impostazione predefinita, Azure AD Connect installa SQL Server 2012 Express). Non utilizzare hello stessa istanza di database come server DirSync.
   * Un account del servizio utilizzato tooconnect tooSQL Server (se il database di SQL Server è remoto, questo account deve essere un account di servizio di dominio).
     Queste opzioni possono essere visualizzate in questa schermata:   
     ![Immettere le credenziali di Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Fare clic su **Avanti**.
8. In hello **tooconfigure pronto** , mantenere hello **avviare il processo di sincronizzazione di hello appena viene completata la configurazione hello** selezionata. server Hello è attualmente in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode) affinché le modifiche non vengono esportati tooAzure Active Directory.
9. Fare clic su **Installa**.
10. Una volta completata l'installazione di hello, disconnettersi e accedere nuovamente tooWindows prima di usare Synchronization Service Manager, Editor regole di sincronizzazione, o provare toomake altre modifiche alla configurazione.

> [!NOTE]
> Inizia la sincronizzazione tra Active Directory di Windows Server e Azure Active Directory, ma non sono modifiche tooAzure esportato AD. Le modifiche possono essere esportare attivamente da un solo strumento di sincronizzazione alla volta. Questo stato è detto [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Verificare che la sincronizzazione toobegin pronto Azure AD Connect
tooverify che Azure AD Connect è pronto tootake su da DirSync, è necessario tooopen **Synchronization Service Manager** gruppo hello **Azure AD Connect** dal menu di avvio hello.

In un'applicazione hello, andare toohello **operazioni** scheda. In questa scheda, verificare che hello dopo le operazioni completate:

* L'importazione in hello Active Directory Connector
* L'importazione in hello Azure Active Directory Connector
* Sincronizzazione completa su hello Active Directory Connector
* Sincronizzazione completa su hello Azure Active Directory Connector

![Importazione e sincronizzazione completate](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Esaminare il risultato di hello da queste operazioni e verificare che non siano presenti errori.

Se si desidera toosee e controllare le modifiche di hello su tooAzure toobe esportato Active Directory, quindi leggere come tooverify hello configurazione [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode). Apportare le modifiche di configurazione necessarie fino a quando non si verificano eventi imprevisti.

Si è pronti tooswitch da DirSync tooAzure Active Directory quando si aver completato questi passaggi e risultato hello è corretto.

### <a name="uninstall-dirsync-old-server"></a>Disinstallare DirSync (vecchio server)
* In **Programmi e funzionalità** trovare **Strumento di sincronizzazione di Microsoft Azure Active Directory**
* Disinstallare lo **Strumento di sincronizzazione di Microsoft Azure Active Directory**
* la disinstallazione di Hello può richiedere too15 minuti toocomplete.

Se si preferisce toouninstall DirSync in un secondo momento, è possibile arrestare il server di hello temporaneamente o disabilitare il servizio di hello. Se si verificano problemi, questo metodo consente di abilitare toore è. Tuttavia, non è previsto che il passaggio successivo hello non riuscirà pertanto necessario non è necessario.

Con DirSync disinstallata o disabilitata, non c'è nessun server attivo esportazione tooAzure Active Directory. prima di tutte le modifiche in Active Directory locale continuerà tooAzure toobe sincronizzata Active Directory, è necessario eseguire Hello successivo passaggio tooenable Azure AD Connect.

### <a name="enable-azure-ad-connect-new-server"></a>Abilitare Azure AD Connect (nuovo server)
Dopo l'installazione, la riapertura di Azure AD connect verrà consentono toomake modifiche di configurazione aggiuntive. Avviare **Azure AD Connect** dal menu di avvio hello o dal collegamento hello hello desktop. Assicurarsi che non si toorun hello installazione MSI.

Verrà visualizzato hello segue:  
![Attività aggiuntive](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Selezionare **Configurazione della modalità di gestione temporanea**.
* Disattivare la gestione temporanea da hello deselezionando **modalità di staging abilitato** casella di controllo.

![Immettere le credenziali di Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Fare clic su hello **Avanti** pulsante
* Nella pagina di conferma hello, fare clic su hello **installare** pulsante.

Azure AD Connect è ora il server attivo e non è necessario passare toousing indietro il server DirSync esistente.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere installato di Azure AD Connect è possibile [verificare l'installazione di hello e assegnare licenze](active-directory-aadconnect-whats-next.md).

Altre informazioni su queste nuove funzionalità, che sono state abilitate con installazione hello: [l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md), [impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Altre informazioni su questi argomenti comuni: [dell'utilità di pianificazione e la modalità di sincronizzazione tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
