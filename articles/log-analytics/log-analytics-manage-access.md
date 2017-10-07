---
title: aree di lavoro aaaManage nel portale OMS Analitica di Log di Azure e hello | Documenti Microsoft
description: "È possibile gestire le aree di lavoro nel portale OMS Analitica di Log di Azure e hello utilizzando un'ampia gamma di attività amministrative su utenti, account, aree di lavoro e gli account di Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Gestire le aree di lavoro

toomanage accesso tooLog Analitica, eseguire tooworkspaces correlati di varie attività amministrative. Questo articolo fornisce consigliata workspace toomanage suggerimenti e procedure. Un'area di lavoro è sostanzialmente un contenitore che include informazioni sull'account e semplici informazioni di configurazione per l'account di hello. Altri membri dell'organizzazione è potrebbero usare più aree di lavoro toomanage diversi set di dati raccolti da tutte o alcune parti dell'infrastruttura IT.

toocreate un'area di lavoro, è necessario:

1. Disporre di una sottoscrizione di Azure
2. Scegliere un nome per l'area di lavoro
3. Associare l'area di lavoro hello con la sottoscrizione.
4. Scegliere una località geografica

## <a name="determine-hello-number-of-workspaces-you-need"></a>Determinare il numero di hello di aree di lavoro che necessarie
Un'area di lavoro è una risorsa di Azure ed è un contenitore in cui data è raccolti, aggregato, analizzato e presentato nel portale di Azure hello.

È possibile avere più aree di lavoro per ogni sottoscrizione di Azure ed è possibile disporre di accesso toomore rispetto a un'area di lavoro. La riduzione a icona hello numero di aree di lavoro consente tooquery e correlazione hello la maggior parte dei dati, perché non è possibile tooquery tra più aree di lavoro. In questa sezione viene descritto quando può essere utile toocreate più di un'area di lavoro.

Oggi, un'area di lavoro fornisce:

* Una posizione geografica per archiviare i dati
* Granularità per la fatturazione
* Isolamento dei dati
* Ambito per la configurazione

In base a hello precedente caratteristiche, è consigliabile toocreate più aree di lavoro:

* Si opera in un'azienda globale ed è necessario che i dati siano archiviati in aree specifiche per motivi di sovranità o conformità.
* Si usa Azure e si desidera che il trasferimento di dati in uscita tooavoid spese dalla presenza di un'area di lavoro in hello stessa area come hello gestisce le risorse di Azure.
* Si desidera reparti di toodifferent tooallocate costi o i gruppi aziendali in base all'utilizzo. Quando si crea un'area di lavoro per ogni reparto o gruppo aziendale, l'istruzione di fattura e dell'utilizzo Azure Mostra separatamente gli addebiti di hello per ogni area di lavoro.
* È un provider di servizi gestiti ed necessari tookeep hello log analitica dati relativi a ogni cliente che si gestiscono isolato da altri dati cliente.
* Per gestire più clienti e si desidera che ogni cliente / reparto / business gruppo toosee i propri dati, ma non i dati di hello per altri utenti.

Quando si utilizzano dati toocollect agenti, è possibile [configurare ogni tooone tooreport agent o altre aree di lavoro](log-analytics-windows-agents.md).

Se si usa System Center Operations Manager, ogni gruppo di gestione di Operations Manager può essere connesso con una sola area di lavoro. È possibile installare Microsoft Monitoring Agent hello nei computer gestiti da Operations Manager e hello agente report tooboth Operations Manager e un'area di lavoro Analitica Log diverso.

### <a name="workspace-information"></a>Informazioni sull'area di lavoro

È possibile visualizzare i dettagli sull'area di lavoro nel portale di Azure hello. È inoltre possibile visualizzare i dettagli nel portale OMS hello.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Visualizzare le informazioni dell'area di lavoro nel portale di Azure hello

1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com) tramite la sottoscrizione di Azure.
2. In hello **Hub** menu, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **Analitica Log**. Si inizia a digitare, hello filtri di elenco in base all'input. Fare clic su **Log Analytics**.  
    ![Hub di Azure](./media/log-analytics-manage-access/hub.png)  
3. Nel Pannello di sottoscrizioni hello Analitica di Log, selezionare un'area di lavoro.
4. Pannello area di lavoro Hello Visualizza i dettagli sull'area di lavoro hello e collegamenti per ulteriori informazioni.  
    ![Dettagli dell'area di lavoro](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Gestire utenti e account
Ogni area di lavoro può avere più account associati e ogni account (account Microsoft o account aziendale) può disporre di accesso toomultiple aree di lavoro.

Per impostazione predefinita, hello account di Microsoft o aziendale che crea area di lavoro hello diventa l'amministratore dell'area di lavoro hello hello.

Sono disponibili due modelli di autorizzazione che controllano l'area di lavoro di access tooa Analitica Log:

1. Ruoli utente di Log Analytics legacy
2. [Accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md)

Hello nella tabella seguente vengono riepilogate accesso hello che può essere impostato con ogni modello di autorizzazione:

|                          | Portale di Log Analytics | Portale di Azure | API (incluso PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Ruoli utente di Log Analytics | Sì                  | No           | No                         |
| Accessi in base al ruolo di Azure  | Sì                  | Sì          | Sì                        |

> [!NOTE]
> Log Analitica è lo spostamento toouse accesso basato sui ruoli di Azure come modello di autorizzazioni hello, sostituendo i ruoli utente di Log Analitica hello.
>
>

Hello legacy ruoli utente di Log Analitica controllano solo accesso tooactivities eseguite in hello [portale Analitica Log](https://mms.microsoft.com).

Hello seguenti anche attività richiede autorizzazioni di Azure:

| Azione                                                          | Autorizzazioni di Azure necessarie | Note |
|-----------------------------------------------------------------|--------------------------|-------|
| Aggiunta e rimozione di soluzioni di gestione                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Modifica livello di prezzo hello                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Visualizzazione dei dati in hello *Backup* e *Site Recovery* riquadri delle soluzioni | Amministratore/Coamministratore | Risorse di accessi distribuiti tramite il modello di distribuzione classica hello |
| Creazione di un'area di lavoro in hello portale di Azure                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Gestione di accesso tooLog Analitica con autorizzazioni di Azure
toogrant accesso toohello Log Analitica dell'area di lavoro con autorizzazioni di Azure, seguire i passaggi hello [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md).

Azure offre due ruoli utente predefiniti per Log Analytics:
- Lettore di Log Analytics
- Collaboratore di Log Analytics

I membri di hello *agente di lettura Log Analitica* ruolo può:
- Visualizzare e cercare tutti i dati di monitoraggio 
- Consente di visualizzare le impostazioni di monitoraggio, tra cui la visualizzazione configurazione hello di diagnostica Azure in tutte le risorse di Azure.

| Tipo    | Autorizzazione | Descrizione |
| ------- | ---------- | ----------- |
| Azione | `*/read`   | Capacità tooview tutte le risorse e configurazione di risorsa. Include la visualizzazione di: <br> Stato dell'estensione macchina virtuale <br> Configurazione della diagnostica di Azure nelle risorse <br> Tutte le proprietà e le impostazioni di tutte le risorse |
| Azione | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Query di ricerca nei Log v2 tooperform possibilità |
| Azione | `Microsoft.OperationalInsights/workspaces/search/action` | Query di ricerca nei Log v1 tooperform possibilità |
| Azione | `Microsoft.Support/*` | Casi di supporto tooopen possibilità |
|Non azione | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Impedisce la lettura di area di lavoro toouse obbligatorio chiave hello dati raccolta API e tooinstall degli agenti |


I membri di hello *Log Analitica collaboratore* ruolo può:
- Leggere tutti i dati di monitoraggio 
- Creare e configurare account di automazione
- Aggiungere e rimuovere soluzioni di gestione
- Leggere le chiavi degli account di archiviazione 
- Configurare la raccolta di log da Archiviazione di Azure
- Modificare le impostazioni di monitoraggio per le risorse di Azure, tra cui
  - Aggiunta di hello VM estensione tooVMs
  - Configurazione della diagnostica di Azure in tutte le risorse di Azure

> [!NOTE] 
> È possibile utilizzare hello possibilità tooadd un macchina virtuale estensione tooa macchina virtuale toogain controllo completo su una macchina virtuale.

| Autorizzazione | Descrizione |
| ---------- | ----------- |
| `*/read`     | Capacità tooview tutte le risorse e configurazione di risorsa. Include la visualizzazione di: <br> Stato dell'estensione macchina virtuale <br> Configurazione della diagnostica di Azure nelle risorse <br> Tutte le proprietà e le impostazioni di tutte le risorse |
| `Microsoft.Automation/automationAccounts/*` | Toocreate possibilità e configurare gli account di automazione di Azure, inclusa l'aggiunta e modifica di runbook |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Aggiungere, aggiornare e rimuovere le estensioni di macchina virtuale, incluse l'estensione Microsoft Monitoring Agent hello e hello agente OMS per estensione Linux |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Chiave account di archiviazione hello di visualizzazione. Richiesto tooconfigure Log Analitica tooread registri gli account di archiviazione di Azure |
| `Microsoft.Insights/alertRules/*` | Consente di aggiungere, aggiornare e rimuovere regole di avviso |
| `Microsoft.Insights/diagnosticSettings/*` | Consente di aggiungere, aggiornare e rimuovere impostazioni di diagnostica dalle risorse di Azure |
| `Microsoft.OperationalInsights/*` | Consente di aggiungere, aggiornare e rimuovere configurazioni per le aree di lavoro di Log Analytics |
| `Microsoft.OperationsManagement/*` | Consente di aggiungere e rimuovere soluzioni di gestione |
| `Microsoft.Resources/deployments/*` | Consente di creare ed eliminare distribuzioni, è necessaria per aggiungere e rimuovere soluzioni, aree di lavoro e account di automazione |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Consente di creare ed eliminare distribuzioni, è necessaria per aggiungere e rimuovere soluzioni, aree di lavoro e account di automazione |

tooadd e rimuovere utenti tooa ruolo utente, è necessario toohave `Microsoft.Authorization/*/Delete` e `Microsoft.Authorization/*/Write` autorizzazione.

Utilizzare tali utenti l'accesso toogive ruoli in ambiti diversi:
- Sottoscrizione di aree di lavoro di accesso tooall dalla sottoscrizione hello-
- Gruppo di risorse - lavoro tooall di accesso nel gruppo di risorse hello
- Risorse - hello tooonly di accesso specificato dell'area di lavoro

Utilizzare [ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md) toocreate ruoli con hello informazioni sulle autorizzazioni necessarie.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Ruoli utente di Azure e ruoli utente del portale di Log Analytics
Se si dispone di Azure almeno dell'autorizzazione in lettura dell'area di lavoro di hello Analitica di Log, è possibile aprire portale Log Analitica hello facendo hello **portale OMS** attività durante la visualizzazione dell'area di lavoro di hello Analitica di Log.

All'apertura del portale Log Analitica hello, si passa toousing hello legacy Analitica Log i ruoli utente. Se non si dispone un'assegnazione di ruolo nel portale di hello Log Analitica, hello servizio [controlli hello Azure autorizzazioni disponibili nell'area di lavoro hello](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
Assegnazione di ruolo nel portale di Log Analitica hello viene determinato in base a come indicato di seguito:

| Condizioni                                                   | Ruolo utente di Log Analytics assegnato | Note |
|--------------------------------------------------------------|----------------------------------|-------|
| L'account appartiene tooa legacy ruolo utente di Log Analitica     | Hello specificato il ruolo di utente Log Analitica | |
| L'account non appartiene tooa legacy ruolo utente di Log Analitica <br> Area di lavoro di Azure completo autorizzazioni toohello (`*` autorizzazione <sup>1</sup>) | Amministratore ||
| L'account non appartiene tooa legacy ruolo utente di Log Analitica <br> Area di lavoro di Azure completo autorizzazioni toohello (`*` autorizzazione <sup>1</sup>) <br> *non azioni*`Microsoft.Authorization/*/Delete` e `Microsoft.Authorization/*/Write` | Collaboratore ||
| L'account non appartiene tooa legacy ruolo utente di Log Analitica <br> Autorizzazione di lettura di Azure | Sola lettura ||
| L'account non appartiene tooa legacy ruolo utente di Log Analitica <br> Le autorizzazioni di Azure non vengono riconosciute | Sola lettura ||
| Per le sottoscrizioni gestite da un Cloud Solution Provider (CSP) <br> account di Hello firmato in con è nell'area di lavoro toohello hello Azure Active Directory collegata | Amministratore | In genere i clienti di hello di un provider CSP |
| Per le sottoscrizioni gestite da un Cloud Solution Provider (CSP) <br> account di Hello firmato in con non è presente nell'area di lavoro toohello hello Azure Active Directory collegata | Collaboratore | In genere hello CSP |

<sup>1</sup> vedere troppo[autorizzazioni Azure](../active-directory/role-based-access-control-custom-roles.md) per ulteriori informazioni sulle definizioni di ruolo. Durante la valutazione di ruoli, un'azione di `*` non equivale troppo`Microsoft.OperationalInsights/workspaces/*`.

Tookeep alcuni punti presente su hello portale di Azure:

* Quando si accede nel portale OMS toohello utilizzando http://mms.microsoft.com, vedrai hello **selezionare un'area di lavoro** elenco. Questo elenco contiene solo le aree di lavoro in cui si ha un ruolo utente di Log Analytics. aree di lavoro di hello toosee si dispone di accesso toowith Azure sottoscrizioni, è necessario un tenant toospecify come parte dell'URL hello. Ad esempio: `mms.microsoft.com/?tenant=contoso.com`. Identificatore del tenant Hello è spesso quest'ultima parte dell'indirizzo di posta elettronica hello utilizzati toosign in.
* Se si desidera toonavigate direttamente portale tooa che è necessario accedere toousing Azure autorizzazioni, sarà necessario risorse hello toospecify come parte dell'URL hello. È possibile tooget questo URL mediante PowerShell.

  ad esempio `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  URL di Hello è simile:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Gestione degli utenti nel portale OMS hello
Gestire utenti e gruppi in hello **Gestisci utenti** scheda hello **account** scheda nella pagina Impostazioni hello.   

![gestione utenti](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Aggiungere un'area di lavoro dell'utente tooan esistente
Utilizzare hello seguendo i passaggi tooadd un'area di lavoro tooa utente o gruppo.

1. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro.
2. Fare clic su hello **account** scheda e quindi fare clic su hello **Gestisci utenti** scheda.
3. In hello **Gestisci utenti** , scegliere hello account tipo tooadd: **Account aziendale**, **Account Microsoft**, **supporto Microsoft**.

   * Se si sceglie Microsoft Account, digitare l'indirizzo di posta elettronica hello dell'utente di hello associato hello Account Microsoft.
   * Se si sceglie l'Account aziendale, immettere parte dell'utente hello / alias di posta elettronica o nome del gruppo e un elenco di utenti e gruppi corrispondenti, viene visualizzato nella casella a discesa. Selezionare un utente o gruppo.
   * Utilizzare un tecnico del supporto Microsoft o altri toohelp dell'area di lavoro di Microsoft dipendente accesso temporaneo tooyour toogive di supporto Microsoft la risoluzione dei problemi.

     > [!NOTE]
     > Per prestazioni ottimali hello, limitare il numero di hello di gruppi di Active Directory associati a un singolo toothree account OMS, ovvero uno per gli amministratori, uno per i collaboratori e uno per gli utenti di sola lettura. Uso di più gruppi può influire sulle prestazioni di hello del Log Analitica.
     >
     >
4. Scegliere il tipo di hello di utente o gruppo tooadd: **amministratore**, **collaboratore**, o **utente ReadOnly**.  
5. Fare clic su **Aggiungi**.

   Se si aggiunge un account Microsoft, un'area di lavoro di invito toojoin hello viene inviato tramite posta elettronica toohello fornito. Dopo che l'utente hello segue istruzioni hello hello invito toojoin OMS, hello consente l'accesso dell'area di lavoro di hello.
   Se si aggiunge un account aziendale, hello consente l'accesso Analitica Log immediatamente.  

#### <a name="edit-an-existing-user-type"></a>Modificare un tipo utente esistente
È possibile modificare il ruolo account hello per un utente associato all'account OMS. È necessario hello ruolo le opzioni seguenti:

* *Administrator*: può gestire gli utenti, visualizzare ed eseguire operazioni su tutti gli avvisi e aggiungere e rimuovere i server
* *Collaboratore*: può visualizzare ed eseguire operazioni su tutti gli avvisi e aggiungere e rimuovere i server
* *Utente di sola lettura*: gli utenti contrassegnati come di sola lettura non possono:

  1. Aggiungere o rimuovere soluzioni. raccolta di soluzioni Hello è nascosto.
  2. Aggiungere, modificare o rimuovere riquadri nel **Dashboard**.
  3. Hello vista **impostazioni** pagine. pagine Hello sono nascosti.
  4. Nella visualizzazione ricerca hello, configurazione di Power BI, ricerche salvate e avvisi le attività sono nascoste.

#### <a name="tooedit-an-account"></a>tooedit un account
1. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro.
2. Fare clic su hello **account** scheda e quindi fare clic su hello **Gestisci utenti** scheda.
3. Selezionare il ruolo di hello per utente hello che si desidera toochange.
4. Nella finestra di dialogo Conferma hello, fare clic su **Sì**.

### <a name="remove-a-user-from-a-workspace"></a>Rimuovere un utente da un'area di lavoro
Utilizzare hello seguendo i passaggi tooremove un utente da un'area di lavoro. Utente hello rimozione non comporta la chiusura dell'area di lavoro di hello. Ma rimuove l'associazione di hello tra tale utente e l'area di lavoro hello. Se un utente è associato a più aree di lavoro, tale utente può comunque accedere tooOMS e visualizzare le altre aree di lavoro.

1. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro.
2. Fare clic su hello **account** scheda e quindi fare clic su hello **Gestisci utenti** scheda.
3. Fare clic su **rimuovere** che si desidera tooremove un nome di utente toohello successivo.
4. Nella finestra di dialogo Conferma hello, fare clic su **Sì**.

### <a name="add-a-group-tooan-existing-workspace"></a>Aggiungere un gruppo tooan esistente dell'area di lavoro
1. Nella precedente sezione "tooadd un'area di lavoro dell'utente tooan esistente" di hello, seguire i passaggi 1-4.
2. In **Scegliere l'utente/gruppo** selezionare **Gruppo**.  
   ![aggiungere un gruppo tooan esistente dell'area di lavoro](./media/log-analytics-manage-access/add-group.png)
3. Immettere l'indirizzo di posta elettronica o nome visualizzato hello per gruppo hello quali tooadd.
4. Selezionare il gruppo di hello nei risultati elenco hello e quindi fare clic su **Aggiungi**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Collegare un tooan dell'area di lavoro esistente, sottoscrizione di Azure
Tutte le aree di lavoro creati dopo il 26 settembre 2016, deve essere collegato tooan sottoscrizione di Azure al momento della creazione. Aree di lavoro create prima di tale data deve essere collegato tooa dell'area di lavoro quando si accede. Quando si crea l'area di lavoro hello da hello portale di Azure o quando si collega il tooan dell'area di lavoro sottoscrizione di Azure, Azure Active Directory è collegato con l'account aziendale.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink tooan un'area di lavoro sottoscrizione di Azure nel portale OMS hello

- Quando si accede al portale OMS hello, verrà richiesta tooselect una sottoscrizione di Azure. Selezionare hello sottoscrizione che desidera toolink tooyour area di lavoro e quindi fare clic su **collegamento**.  
    ![Collegare la sottoscrizione di Azure](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink un'area di lavoro, l'account di Azure abbia già accesso toohello area di lavoro desideri toolink.  In altre parole, hello l'account utilizzato tooaccess hello portale di Azure deve essere **hello stesso** come account hello è utilizzare l'area di lavoro tooaccess hello. In caso contrario, vedere [aggiungere un'area di lavoro dell'utente tooan esistente](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink tooan un'area di lavoro sottoscrizione di Azure nel portale di Azure hello
1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Cercare e selezionare **Log Analytics**.
3. Viene visualizzato un elenco delle aree di lavoro esistenti. Fare clic su **Aggiungi**.  
   ![Elenco di aree di lavoro](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. In **Area di lavoro di OMS** fare clic su **Collega esistente**.  
   ![Collegare un'area di lavoro esistente](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Fare clic su **Configura le impostazioni necessarie**.  
   ![configure required settings](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Viene visualizzato l'elenco di hello di aree di lavoro che non sono ancora collegato tooyour account Azure. Selezionare un'area di lavoro.  
   ![Selezionare le aree di lavoro](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Se necessario, è possibile modificare i valori per hello seguenti elementi:
   * Sottoscrizione
   * Gruppo di risorse
   * Percorso
   * Piano tariffario   
     ![Modificare i valori](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Fare clic su **OK**. area di lavoro Hello è ora collegato tooyour account Azure.

> [!NOTE]
> Se non viene visualizzata l'area di lavoro hello toolink desiderato, quindi la sottoscrizione di Azure non dispone di accesso toohello area di lavoro creato tramite il portale di OMS hello.  account di toothis toogrant accesso dal portale OMS hello, vedere [aggiungere un'area di lavoro dell'utente tooan esistente](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Aggiornare un tooa dell'area di lavoro piano di pagamento
In OMS sono disponibili tre tipi di piani per l'area di lavoro: **Gratuito**, **Standalone** e **OMS**.  Se si utilizza hello *libero* piano, è previsto un limite di 500 MB di dati al giorno inviato tooLog Analitica.  Se si supera questo periodo, è necessario toochange tooavoid di piano tooa a pagamento l'area di lavoro non raccoglie i dati oltre questo limite. Il tipo di piano può essere cambiato in qualsiasi momento.  Per altre informazioni sui prezzi di OMS, vedere i [dettagli sui prezzi](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Uso dei diritti derivanti da una sottoscrizione di OMS
i diritti di hello toouse che provengono da acquistare OMS E1, OMS E2 OMS o un componente aggiuntivo OMS per System Center, scegliere hello *OMS* piano di OMS Log Analitica.

Quando si acquista una sottoscrizione di OMS, i diritti di hello vengono aggiunti tooyour contratto Enterprise Agreement. Tutte le sottoscrizioni Azure viene creata in questo contratto è possono usare i diritti di hello. Tutte le aree di lavoro in queste sottoscrizioni utilizzare diritti OMS hello.

tooensure che l'utilizzo di un'area di lavoro sia tooyour applicati i diritti da hello sottoscrizione OMS, è necessario:

1. Creare l'area di lavoro in una sottoscrizione di Azure che fa parte del contratto Enterprise Agreement che include sottoscrizione OMS hello hello
2. Seleziona hello *OMS* piano per l'area di lavoro hello

> [!NOTE]
> Se l'area di lavoro è stato creato prima il 26 settembre 2016 e Analitica del Log prezzi piano *Premium*, quindi l'area di lavoro utilizza dei diritti dal componente aggiuntivo OMS hello per System Center. È anche possibile usare i diritti modificando toohello *OMS* piano tariffario.
>
>

diritti di sottoscrizione OMS Hello non sono visibili in hello Azure o il portale di OMS. È possibile visualizzare i diritti e l'utilizzo in hello Enterprise Portal.  

Se è necessario toochange hello sottoscrizione Azure in cui è collegata l'area di lavoro, è possibile utilizzare hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Uso dell'impegno di Azure da un contratto Enterprise
Se non si dispone di una sottoscrizione di OMS, pagamento per ogni componente di OMS avverrà separatamente e l'utilizzo di hello appare nella fattura di Azure.

Se si dispone di un impegno monetario Azure su hello enterprise registrazione toowhich sono collegate le sottoscrizioni di Azure, utilizzo del Log Analitica verrà automaticamente addebitato contro hello rimanenti monetario commit.

Se è necessario toochange hello sottoscrizione di Azure che hello dell'area di lavoro collegato, è possibile usare Azure PowerShell hello [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Modificare un tooa dell'area di lavoro a pagamento piano tariffario in hello portale di Azure
1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Cercare e selezionare **Log Analytics**.
3. Viene visualizzato un elenco delle aree di lavoro esistenti. Selezionare un'area di lavoro.  
4. Nel pannello dell'area di lavoro hello in **generale**, fare clic su **tariffario**.  
5. In **Piano tariffario** selezionare un piano tariffario e quindi fare clic su **Seleziona**.  
    ![selezione piano](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Quando si aggiorna la visualizzazione nel portale di Azure hello, vedere **tariffario** aggiornato per il livello di hello selezionato.  
    ![piano aggiornato](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Se l'area di lavoro è collegato tooan account di automazione, prima selezionare hello *autonomo (Per GB)* tariffario è necessario eliminare qualsiasi **automazione e controllo** soluzioni e scollegare hello automazione account. Nel pannello dell'area di lavoro hello in **generale**, fare clic su **soluzioni** soluzioni toosee e delete. hello toounlink account di automazione, di fare clic sul nome di account di automazione in hello hello hello **tariffario** blade.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Modificare un tooa dell'area di lavoro a pagamento a livello di prezzo nel portale OMS hello

toochange hello tramite il portale di OMS hello piano tariffario, è necessario disporre di una sottoscrizione di Azure.

1. Nel portale OMS hello, fare clic su hello **impostazioni** riquadro.
2. Fare clic su hello **account** scheda e quindi fare clic su hello **sottoscrizione di Azure & piano dati** scheda.
3. Fare clic su hello desiderato toouse piano tariffario.
4. Fare clic su **Salva**.  
   ![Sottoscrizione e piani dati](./media/log-analytics-manage-access/subscription-tab.png)

Il nuovo piano di dati viene visualizzato nella barra multifunzione del portale di OMS nella parte superiore di hello della pagina web hello.

![Barra multifunzione di OMS](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Modificare la durata dell'archiviazione dei dati di Log Analytics

Livello di prezzo gratuito di hello, Analitica Log consente di creare hello disponibile negli ultimi sette giorni di dati.
In hello piano tariffario Standard, Log Analitica rende disponibile hello ultimi 30 giorni di dati.
Nel livello di prezzo Premium hello, Log Analitica rende disponibile hello ultimi 365 giorni di dati.
Hello autonomo e OMS, i livelli di prezzo per impostazione predefinita, Log Analitica rende disponibile hello ultimi 31 giorni di dati.

Quando si utilizza hello autonomo e livelli di prezzi di OMS, è possibile utilizzare too2 anni di dati (730 giorni). Dati archiviati da più tempo rispetto al valore predefinito di hello di 31 giorni comporta un costo di conservazione dei dati. Per altre informazioni sui prezzi, vedere i [prezzi per eccedenze](https://azure.microsoft.com/pricing/details/log-analytics/).

durata di hello toochange di conservazione dei dati:

1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Cercare e selezionare **Log Analytics**.
3. Viene visualizzato un elenco delle aree di lavoro esistenti. Selezionare un'area di lavoro.  
4. Nel pannello dell'area di lavoro hello in **generale**, fare clic su **conservazione**.  
5. Utilizzare hello dispositivo di scorrimento tooincrease o diminuire hello numero di giorni di conservazione e quindi fare clic su **salvare**.  
    ![Modificare la conservazione](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Modificare un'organizzazione di Azure Active Directory in un'area di lavoro

È possibile modificare un'organizzazione di Azure Active Directory in un'area di lavoro. Modifica hello organizzazione di Azure Active Directory consente di tooadd utenti e gruppi da tale area di lavoro toohello directory.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>toochange hello organizzazione di Azure Active Directory per un'area di lavoro

1. Nella pagina Impostazioni di hello nel portale OMS hello, fare clic su **account** e quindi fare clic su hello **Gestisci utenti** scheda.  
2. Esaminare le informazioni sugli account aziendali hello e quindi fare clic su **Modifica organizzazione**.  
    ![Modificare l'organizzazione](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Immettere le informazioni di identità hello per messaggio per l'amministratore di dominio di Azure Active Directory. Verrà visualizzato un messaggio di riconoscimento che informa che l'area di lavoro è collegato tooyour dominio di Azure Active Directory.  
    ![Acknowledgment dell'area di lavoro collegata](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Eliminare un'area di lavoro di Log Analytics
Quando si elimina un'area di lavoro Log Analitica, tutti i dati relativi a tooyour dell'area di lavoro viene eliminato dal servizio OMS hello entro 30 giorni.

Se si è amministratore e vi sono più utenti associati hello area di lavoro, l'associazione di hello tra gli utenti e l'area di lavoro hello viene interrotta. Se gli utenti di hello sono associati ad altre aree di lavoro, quindi potranno continuare a usare OMS con tali aree di lavoro. Tuttavia, se non associate ad altre aree di lavoro è necessario toocreate toouse un'area di lavoro OMS.

### <a name="toodelete-a-workspace"></a>toodelete un'area di lavoro
1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Cercare e selezionare **Log Analytics**.
3. Viene visualizzato un elenco delle aree di lavoro esistenti. Selezionare l'area di lavoro hello che si desidera toodelete.
4. Nel pannello dell'area di lavoro hello, fare clic su **eliminare**.  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. Nella finestra di conferma di hello Elimina area di lavoro, fare clic su **Sì**.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md) tooadd agenti e raccogliere i dati.
* [Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.
* [Configurare le impostazioni proxy e firewall nel Log Analitica](log-analytics-proxy-firewall.md) se l'organizzazione utilizza un server proxy o firewall in modo che gli agenti possono comunicare con hello servizio Analitica di Log.
