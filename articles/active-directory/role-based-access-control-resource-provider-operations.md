---
title: Operazioni su Provider di gestione risorse aaaAzure | Documenti Microsoft
description: Dettagli hello operazioni disponibili nel provider di risorse di Microsoft Azure Resource Manager hello
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Operazioni di provider di risorse con Azure Resource Manager

Questo documento elenca le operazioni di hello disponibili per ogni provider di risorse di gestione risorse di Microsoft Azure. Possono essere usati in ruoli personalizzati tooprovide granulare controllo di accesso basato sui ruoli (RBAC) autorizzazioni tooresources in Azure. L’elenco qui fornito non è da ritenersi completo e le operazioni potrebbero essere aggiunte o rimosse man mano che il provider viene aggiornato. Stringhe di operazione seguono il formato di hello delle `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Per un elenco completo e corrente utilizzare `Get-AzureRmProviderOperation` (in PowerShell) o `azure provider operations show` (in Azure CLI) operazioni toolist di provider di risorse di Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Operazione | Descrizione |
|---|---|
|/configuration/action|Aggiorna la configurazione tenant.|
|/services/action|Aggiorna un'istanza del servizio nel tenant di hello.|
|/configuration/write|Crea una configurazione tenant.|
|/configuration/read|Legge hello configurazione del Tenant.|
|/services/write|Crea un'istanza del servizio nel tenant di hello.|
|/services/read|Legge le istanze del servizio nel tenant di hello hello.|
|/services/delete|Elimina un'istanza del servizio nel tenant di hello.|
|/services/servicemembers/action|Crea un'istanza del membro del servizio nel servizio di hello.|
|/services/servicemembers/read|Legge l'istanza del membro hello servizio nel servizio hello.|
|/services/servicemembers/delete|Elimina un'istanza del membro del servizio nel servizio hello.|
|/services/servicemembers/alerts/read|Legge gli avvisi di hello per un membro del servizio.|
|/services/alerts/read|Legge gli avvisi di hello per un servizio.|
|/services/alerts/read|Legge gli avvisi di hello per un servizio.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Operazione | Descrizione |
|---|---|
|/generateRecommendations/action|Genera suggerimenti.|
|/suppressions/action|Crea/aggiorna eliminazioni.|
|/register/action|Registra sottoscrizione hello per hello Microsoft Advisor|
|/generateRecommendations/read|Ottiene lo stato dei suggerimenti generati.|
|/recommendations/read|Legge i suggerimenti.|
|/suppressions/read|Ottiene le eliminazioni.|
|/suppressions/delete|Cancella le eliminazioni.|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Operazione | Descrizione |
|---|---|
|/servers/read|Recupera le informazioni di hello di hello specificato Analysis Server.|
|/servers/write|Crea o aggiorna hello specificato Analysis Server.|
|/servers/delete|Eliminazioni hello Analysis Server.|
|/servers/suspend/action|Sospende hello Analysis Server.|
|/servers/resume/action|Riprende hello Analysis Server.|
|/servers/checkNameAvailability<br>/action|Verifica che il nome dell’Analysis Server specificato sia valido e non in uso.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Operazione | Descrizione |
|---|---|
|/checkNameAvailability/action|Verifica che il nome del servizio sia disponibile.|
|/register/action|Registra la sottoscrizione per il provider di risorse Microsoft.ApiManagement.|
|/unregister/action|Annulla la registrazione della sottoscrizione per il provider di risorse Microsoft.ApiManagement.|
|/service/write|Creare una nuova istanza del servizio Gestione API|
|/service/read|Leggere i metadati per un'istanza del servizio Gestione API|
|/service/delete|Elimina l’istanza del servizio Gestione API.|
|/service/updatehostname/action|Configura, aggiorna o rimuove i nomi di dominio personalizzati per un servizio Gestione API.|
|/service/uploadcertificate/action|Carica il certificato SSL per un servizio Gestione API.|
|/service/backup/action|Servizio gestione API toohello specificato contenitore del backup in un utente fornito l'account di archiviazione|
|/service/restore/action|Ripristinare il servizio Gestione API dal contenitore specificato di hello nell'account di archiviazione dall'utente|
|/service/managedeployments/action|Modifica SKU/unità, aggiunge/rimuove distribuzioni regionali del servizio Gestione API.|
|/service/getssotoken/action|Ottiene il token SSO che può essere utilizzati toologin portale API Gestione servizio Legacy come amministratore|
|/service/applynetworkconfigurationupdates/action|Gli aggiornamenti hello Microsoft.ApiManagement risorse in esecuzione in una rete virtuale toopick aggiornate le impostazioni di rete.|
|/service/operationresults/read|Ottiene lo stato corrente dell'operazione in esecuzione prolungata|
|/service/networkStatus/read|Ottiene lo stato di accesso di rete hello di risorse.|
|/service/loggers/read|Ottiene l'elenco di logger o i dettagli del logger|
|/service/loggers/write|Aggiunge un nuovo logger o aggiorna i dettagli di un logger esistente|
|/service/loggers/delete|Rimuove un logger esistente|
|/service/users/read|Ottiene un elenco di utenti registrati o i dettagli dell’account di un utente|
|/service/users/write|Registra un nuovo utente o aggiorna i dettagli dell’account di un utente esistente|
|/service/users/delete|Rimuove l’account utente|
|/service/users/generateSsoUrl/action|Genera un URL SSO. Hello URL può essere utilizzato tooaccess portale di amministrazione|
|/service/users/subscriptions/read|Ottiene l'elenco di sottoscrizioni utente|
|/service/users/keys/read|Ottiene l'elenco di chiavi utente|
|/service/users/groups/read|Ottiene l'elenco di gruppi utente|
|/service/tenant/operationResults/read|Ottiene l'elenco dei risultati dell'operazione o il risultato di un'operazione specifica|
|/service/tenant/policy/read|Ottenere la configurazione di criteri per il tenant hello|
|/service/tenant/policy/write|Configurazione dei criteri di gruppo per tenant hello|
|/service/tenant/policy/delete|Rimuovere la configurazione dei criteri per il tenant hello|
|/service/tenant/configuration/save/action|Crea commit con configurazione snapshot toohello specificato ramo hello repository|
|/service/tenant/configuration/deploy/action|Esegue un'attività di distribuzione delle modifiche tooapply dalla configurazione di toohello ramo git specificato hello nel database.|
|/service/tenant/configuration/validate/action|Convalida le modifiche dal ramo git specificato hello|
|/service/tenant/configuration/operationResults/read|Ottiene l'elenco dei risultati dell'operazione o il risultato di un'operazione specifica|
|/service/tenant/configuration/syncState/read|Ottiene lo stato dell’ultima sincronizzazione git|
|/service/tenant/access/read|Ottiene i dettagli sulle informazioni di accesso del tenant|
|/service/tenant/access/write|Aggiorna i dettagli sulle informazioni di accesso del tenant|
|/service/tenant/access/regeneratePrimaryKey/action|Rigenera la chiave di accesso primaria|
|/service/tenant/access/regenerateSecondaryKey/action|Rigenera la chiave di accesso secondaria|
|/service/identityProviders/read|Ottiene l’elenco di provider di identità o i dettagli del provider di identità|
|/service/identityProviders/write|Crea un nuovo provider di identità o aggiorna i dettagli di un provider di identità esistente|
|/service/identityProviders/delete|Rimuove un provider di identità esistente|
|/service/subscriptions/read|Ottiene un elenco di sottoscrizioni al prodotto o i dettagli di sottoscrizione a un prodotto|
|/service/subscriptions/write|Sottoscrivere un prodotto esistente tooan utente esistente o aggiornare i dettagli della sottoscrizione esistente. Questa operazione può essere utilizzato toorenew sottoscrizione|
|/service/subscriptions/delete|Elimina una sottoscrizione. Questa operazione può essere utilizzato toodelete sottoscrizione|
|/service/subscriptions/regeneratePrimaryKey/action|Rigenera la chiave primaria di sottoscrizione|
|/service/subscriptions/regenerateSecondaryKey/action|Rigenera la chiave secondaria di sottoscrizione|
|/service/backends/read|Ottiene l’elenco di back-end o i dettagli del back-end|
|/service/backends/write|Aggiunge un nuovo back-end o aggiorna i dettagli di un back-end esistente|
|/service/backends/delete|Rimuove il back-end esistente|
|/service/apis/read|Ottiene l’elenco di tutte le API registrate o i dettagli delle API|
|/service/apis/write|Crea una nuova API o aggiorna i dettagli di una API esistente|
|/service/apis/delete|Rimuove una API esistente|
|/service/apis/policy/read|Ottiene i dettagli di configurazione dei criteri per l’API|
|/service/apis/policy/write|Imposta i dettagli di configurazione dei criteri per l’API|
|/service/apis/policy/delete|Rimuove la configurazione dei criteri dalla API|
|/service/apis/operations/read|Ottiene l’elenco di operazioni API esistenti o i dettagli dell’operazione API|
|/service/apis/operations/write|Crea una nuova operazione API o ne aggiorna una esistente|
|/service/apis/operations/delete|Rimuove un’operazione API esistente|
|/service/apis/operations/policy/read|Ottiene i dettagli di configurazione dei criteri per l’operazione|
|/service/apis/operations/policy/write|Imposta i dettagli di configurazione dei criteri per l’operazione|
|/service/apis/operations/policy/delete|Rimuove la configurazione dei criteri dall’operazione|
|/service/products/read|Ottiene l’elenco dei prodotti o i dettagli di un prodotto|
|/service/products/write|Crea nuovo prodotto o aggiorna i dettagli del prodotto esistente.|
|/service/products/delete|Rimuove il prodotto esistente.|
|/service/products/subscriptions/read|Ottiene l'elenco delle sottoscrizioni di prodotto.|
|/service/products/apis/read|Ottenere un elenco delle API aggiunte tooexisting prodotto|
|/service/products/apis/write|Aggiungi elemento prodotto tooexisting API esistente|
|/service/products/apis/delete|Rimuove le API esistenti dal prodotto esistente.|
|/service/products/policy/read|Ottiene la configurazione dei criteri del prodotto esistente.|
|/service/products/policy/write|Imposta la configurazione dei criteri del prodotto esistente.|
|/service/products/policy/delete|Rimuove la configurazione dei criteri del prodotto esistente.|
|/service/products/groups/read|Ottiene l'elenco di gruppi di sviluppatori associato al prodotto.|
|/service/products/groups/write|Associa il gruppo di sviluppatori esistenti al prodotto esistente.|
|/service/products/groups/delete|Elimina l’associazione del gruppo di sviluppatori esistenti al prodotto esistente.|
|/service/openidConnectProviders/read|Ottiene l'elenco di provider di OpenID Connect o le informazioni dettagliate del Provider di OpenID Connect.|
|/service/openidConnectProviders/write|Crea un nuovo provider OpenID Connect o aggiorna i dettagli di un provider di OpenID Connect esistente.|
|/service/openidConnectProviders/delete|Rimuove il provider di OpenID Connect esistente.|
|/service/certificates/read|Ottiene l'elenco di certificati o i dettagli del certificato.|
|/service/certificates/write|Aggiunge un nuovo certificato.|
|/service/certificates/delete|Elimina un certificato esistente.|
|/service/properties/read|Ottiene l'elenco di tutte le proprietà o i dettagli della proprietà specificata.|
|/service/properties/write|Crea una nuova proprietà o aggiorna il valore per la proprietà specificata.|
|/service/properties/delete|Rimuove la proprietà esistente.|
|/service/groups/read|Ottiene l'elenco dei gruppi o i dettagli di un gruppo.|
|/service/groups/write|Crea un nuovo gruppo o aggiorna i dettagli di un gruppo esistente.|
|/service/groups/delete|Rimuove il gruppo esistente.|
|/service/groups/users/read|Ottiene l'elenco degli utenti del gruppo.|
|/service/groups/users/write|Aggiungere il gruppo tooexisting utenti esistente|
|/service/groups/users/delete|Rimuove l’utente esistente dal gruppo esistente.|
|/service/authorizationServers/read|Ottiene l'elenco dei server di autorizzazione o i dettagli del server di autorizzazione.|
|/service/authorizationServers/write|Crea un nuovo server di autorizzazione o aggiorna i dettagli di un server di autorizzazione esistente.|
|/service/authorizationServers/delete|Rimuove il server di autorizzazione esistente.|
|/service/reports/bySubscription/read|Ottiene un report aggregato in base alla sottoscrizione.|
|/service/reports/byRequest/read|Ottiene i dati dei report sulle richieste|
|/service/reports/byOperation/read|Ottiene un report aggregato per operazioni.|
|/service/reports/byGeo/read|Ottenere il report aggregato per area geografica.|
|/service/reports/byUser/read|Ottiene un report aggregato per sviluppatori.|
|/service/reports/byTime/read|Ottiene un report aggregato per periodi di tempo.|
|/service/reports/byApi/read|Ottiene un report aggregato per API.|
|/service/reports/byProduct/read|Ottiene un report aggregato per prodotti.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Operazione | Descrizione |
|---|---|
|/appidentities/Read|Restituisce hello risorse (sito web) registrata con hello Gateway.|
|/appidentities/Write|Crea una nuova identità app.|
|/appidentities/Delete|Elimina un'identità app esistente.|
|/deploymenttemplates/listMetadata/Action|Elenca i metadati dell'interfaccia utente associata a hello pacchetto App per le API.|
|/deploymenttemplates/generate/Action|Restituisce un tooprovision modello di distribuzione delle istanze di App per le API.|
|/gateways/Read|Istanza del Gateway hello restituisce.|
|/gateways/Write|Crea un nuovo gateway o ne aggiorna uno esistente.|
|/gateways/Delete|Elimina un'istanza di gateway esistente.|
|/gateways/listLoginUris/Action|Popola l'archivio token e restituisce gli URI di accesso OAuth.|
|/gateways/listKeys/Action|Restituisce la chiave privata del gateway.|
|/gateways/tokens/Write|Crea un nuovo Zumo Token con il nome specificato hello.|
|/gateways/registrations/Read|Restituisce hello risorse (sito web) registrata con hello Gateway.|
|/gateways/registrations/Write|Registra una risorsa (sito web) con hello Gateway.|
|/gateways/registrations/Delete|Annulla la registrazione di una risorsa (sito web) da hello Gateway.|
|/apiapps/Read|Restituisce hello istanza App per le API.|
|/apiapps/Write|Crea una nuova app per le API o ne aggiorna una esistente.|
|/apiapps/Delete|Elimina l'istanza di un'app per le API esistente.|
|/apiapps/listStatus/Action|Restituisce lo stato dell'app per le API.|
|/apiapps/listKeys/Action|Restituisce i segreti dell'app per le API.|
|/apiapps/apidefinitions/Read|Restituisce la definizione API dell'app per le API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Operazione | Descrizione |
|---|---|
|/elevateAccess/action|Concede l'accesso di amministratore di accesso utente nell'ambito del tenant hello chiamante di hello|
|/classicAdministrators/read|Legge gli amministratori di hello per sottoscrizione hello.|
|/classicAdministrators/write|Aggiunge o modifica sottoscrizione tooa amministratore.|
|/classicAdministrators/delete|Rimuove hello amministratore dalla sottoscrizione hello.|
|/locks/read|Ottiene i blocchi in hello specificato ambito.|
|/locks/write|Aggiunge i blocchi per hello specificato ambito.|
|/locks/delete|Blocchi di eliminazione a hello specificato ambito.|
|/policyAssignments/read|Ottiene informazioni su un'assegnazione di criteri.|
|/policyAssignments/write|Creare un criterio di assegnazione di hello specificato ambito.|
|/policyAssignments/delete|Elimina un'assegnazione di criterio hello specificato ambito.|
|/permissions/read|Elenca tutte le autorizzazioni di hello hello chiamante abbia un ambito specifico.|
|/roleDefinitions/read|Ottiene informazioni su una definizione di ruolo.|
|/roleDefinitions/write|Crea o aggiorna una definizione del ruolo personalizzata con le autorizzazioni specificate e gli ambiti assegnabili.|
|/roleDefinitions/delete|Eliminare hello specificato definizione di ruolo personalizzata.|
|/providerOperations/read|Ottiene operazioni per tutti i provider di risorse che possono essere usati nelle definizioni del ruolo.|
|/policyDefinitions/read|Ottiene informazioni su una definizione di criteri.|
|/policyDefinitions/write|Crea una definizione di criteri personalizzata.|
|/policyDefinitions/delete|Elimina una definizione criteri.|
|/roleAssignments/read|Ottiene informazioni su un'assegnazione di ruolo.|
|/roleAssignments/write|Creare un ruolo specificato di assegnazione di hello ambito.|
|/roleAssignments/delete|Elimina un'assegnazione di ruolo hello specificato ambito.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Operazione | Descrizione |
|---|---|
|/automationAccounts/read|Ottiene un account di automazione di Azure|
|/automationAccounts/write|Crea o aggiorna un account di automazione di Azure|
|/automationAccounts/delete|Elimina un account di automazione di Azure|
|/automationAccounts/configurations/readContent/action|Ottiene un contenuto di Automation DSC per Azure|
|/automationAccounts/hybridRunbookWorkerGroups/read|Legge le risorse del ruolo di lavoro ibrido per runbook|
|/automationAccounts/hybridRunbookWorkerGroups/delete|Elimina le risorse del ruolo di lavoro ibrido per runbook|
|/automationAccounts/jobSchedules/read|Ottiene una pianificazione del processo di automazione di Azure|
|/automationAccounts/jobSchedules/write|Crea una pianificazione del processo di automazione di Azure|
|/automationAccounts/jobSchedules/delete|Elimina una pianificazione del processo di automazione di Azure|
|/automationAccounts/connectionTypes/read|Ottiene un asset del tipo di connessione di automazione di Azure|
|/automationAccounts/connectionTypes/write|Crea un asset del tipo di connessione di automazione di Azure|
|/automationAccounts/connectionTypes/delete|Elimina un asset del tipo di connessione di automazione di Azure|
|/automationAccounts/modules/read|Ottiene un modulo di automazione di Azure|
|/automationAccounts/modules/write|Crea o aggiorna un modulo di automazione di Azure|
|/automationAccounts/modules/delete|Elimina un modulo di automazione di Azure|
|/automationAccounts/credentials/read|Ottiene un asset delle credenziali di automazione di Azure|
|/automationAccounts/credentials/write|Crea o aggiorna un asset delle credenziali di automazione di Azure|
|/automationAccounts/credentials/delete|Elimina un asset delle credenziali di automazione di Azure|
|/automationAccounts/certificates/read|Ottiene un asset del certificato di automazione di Azure|
|/automationAccounts/certificates/write|Crea o aggiorna un asset del certificato di automazione di Azure|
|/automationAccounts/certificates/delete|Elimina un asset del certificato di automazione di Azure|
|/automationAccounts/schedules/read|Ottiene un asset della pianificazione di automazione di Azure|
|/automationAccounts/schedules/write|Crea o aggiorna un asset della pianificazione di automazione di Azure|
|/automationAccounts/schedules/delete|Elimina un asset della pianificazione di automazione di Azure|
|/automationAccounts/jobs/read|Ottiene un processo di automazione di Azure|
|/automationAccounts/jobs/write|Crea un processo di automazione di Azure|
|/automationAccounts/jobs/stop/action|Arresta un processo di automazione di Azure|
|/automationAccounts/jobs/suspend/action|Sospende un processo di automazione di Azure|
|/automationAccounts/jobs/resume/action|Riprende un processo di automazione di Azure|
|/automationAccounts/jobs/runbookContent/action|Ottiene il contenuto di hello del runbook di automazione di Azure hello in fase di hello hello dell'esecuzione del processo|
|/automationAccounts/jobs/output/action|Ottiene l'output di hello di un processo|
|/automationAccounts/jobs/read|Ottiene un processo di automazione di Azure|
|/automationAccounts/jobs/write|Crea un processo di automazione di Azure|
|/automationAccounts/jobs/stop/action|Arresta un processo di automazione di Azure|
|/automationAccounts/jobs/suspend/action|Sospende un processo di automazione di Azure|
|/automationAccounts/jobs/resume/action|Riprende un processo di automazione di Azure|
|/automationAccounts/jobs/streams/read|Ottiene un flusso del processo di automazione di Azure|
|/automationAccounts/connections/read|Ottiene un asset della connessione di automazione di Azure|
|/automationAccounts/connections/write|Crea o aggiorna un asset della connessione di automazione di Azure|
|/automationAccounts/connections/delete|Elimina un asset della connessione di automazione di Azure|
|/automationAccounts/variables/read|Esegue la lettura di un asset della variabile di automazione di Azure|
|/automationAccounts/variables/write|Crea o aggiorna un asset della variabile di automazione di Azure|
|/automationAccounts/variables/delete|Elimina un asset della variabile di automazione di Azure|
|/automationAccounts/runbooks/readContent/action|Ottiene il contenuto di hello di un runbook di automazione di Azure|
|/automationAccounts/runbooks/read|Ottiene un runbook di automazione di Azure|
|/automationAccounts/runbooks/write|Crea o aggiorna un runbook di automazione di Azure|
|/automationAccounts/runbooks/delete|Elimina un runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/readContent/action|Ottiene il contenuto di hello di una bozza di runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/writeContent/action|Crea contenuto hello di una bozza di runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/read|Ottiene una bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/publish/action|Pubblica una bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/undoEdit/action|Annullare le modifiche bozza del runbook di automazione di Azure tooan|
|/automationAccounts/runbooks/draft/testJob/read|Ottiene un processo di test per la bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/testJob/write|Crea un processo di test per la bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/testJob/stop/action|Interrompe un processo di test per la bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/testJob/suspend/action|Sospende un processo di test per la bozza del runbook di automazione di Azure|
|/automationAccounts/runbooks/draft/testJob/resume/action|Riprende un processo di test per la bozza del runbook di automazione di Azure|
|/automationAccounts/webhooks/read|Esegue la lettura un webhook di automazione di Azure|
|/automationAccounts/webhooks/write|Crea o aggiorna un webhook di automazione di Azure|
|/automationAccounts/webhooks/delete|Elimina un webhook di automazione di Azure |
|/automationAccounts/webhooks/generateUri/action|Genera un URI per un webhook di automazione di Azure|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Questo provider non è un provider ARM completo e non fornisce operazioni ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per Provider di risorse Batch hello e consente la creazione di hello dell'account Batch|
|/batchAccounts/write|Crea un nuovo account Batch o aggiorna un account Batch esistente|
|/batchAccounts/read|Elenca gli account di Batch o ottiene hello proprietà di un account Batch|
|/batchAccounts/delete|Elimina un account Batch|
|/batchAccounts/listkeys/action|Elenca le chiavi di accesso per un account Batch|
|/batchAccounts/regeneratekeys/action|Rigenera le chiavi di accesso per un account Batch|
|/batchAccounts/syncAutoStorageKeys/action|Consente di sincronizzare le chiavi di accesso per account di archiviazione automatica hello configurato per un account Batch|
|/batchAccounts/applications/read|Elenca le applicazioni o ottiene la proprietà hello di un'applicazione|
|/batchAccounts/applications/write|Crea una nuova applicazione o ne aggiorna una esistente|
|/batchAccounts/applications/delete|Elimina un'applicazione|
|/batchAccounts/applications/versions/read|Ottiene la proprietà hello di un pacchetto di applicazione|
|/batchAccounts/applications/versions/write|Crea un nuovo pacchetto dell'applicazione o ne aggiorna uno esistente|
|/batchAccounts/applications/versions/activate/action|Attiva un pacchetto dell'applicazione|
|/batchAccounts/applications/versions/delete|Elimina un pacchetto dell'applicazione|
|/locations/quotas/read|Ottiene le quote di Batch di hello specificato sottoscrizione all'area di Azure specificato hello|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Operazione | Descrizione |
|---|---|
|/invoices/read|Elenca le fatture disponibili|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Operazione | Descrizione |
|---|---|
|/mapApis/Read|Operazione di lettura|
|/mapApis/Write|Operazione di scrittura|
|/mapApis/Delete|Operazione di eliminazione|
|/mapApis/regenerateKey/action|Rigenera chiave hello|
|/mapApis/listSecrets/action|Elenco hello segreti|
|/mapApis/listSingleSignOnToken/action|Hello lettura Single Sign in autorizzazione Token per risorse|
|/Operations/read|Descrizione dell'operazione di hello.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Operazione | Descrizione |
|---|---|
|/checknameavailability/action|Verifica se un nome è disponibile per essere assegnato a nuova cache Redis|
|/register/action|Registra i provider di risorse 'Valori' hello con una sottoscrizione|
|/unregister/action|Annulla la registrazione del provider di risorse 'Valori' hello con una sottoscrizione|
|/redis/write|Modificare le impostazioni e la configurazione nel portale di gestione di hello hello della Cache Redis|
|/redis/read|Visualizzare le impostazioni e configurazione di hello della Cache Redis nel portale di gestione di hello|
|/redis/delete|Delete hello intera Cache Redis|
|/redis/listKeys/action|Valore di hello visualizzazione di chiavi di accesso della Cache Redis nel portale di gestione di hello|
|/redis/regenerateKey/action|Modificare il valore di hello di chiavi di accesso della Cache Redis nel portale di gestione di hello|
|/redis/import/action|Importa i dati di un formato specificato da più BLOB in Redis|
|/redis/export/action|Esportare Redis dati tooprefixed archiviazione BLOB nel formato specificato|
|/redis/forceReboot/action|Forza il riavvio di un'istanza della cache, con possibile perdita di dati.|
|/redis/stop/action|Arresta un'istanza della cache.|
|/redis/start/action|Avvia un'istanza della cache.|
|/redis/metricDefinitions/read|Ottiene la metrica di hello disponibili per una Cache Redis|
|/redis/firewallRules/read|Ottenere le regole firewall di hello IP di una Cache Redis|
|/redis/firewallRules/write|Modificare le regole firewall di hello IP di una Cache Redis|
|/redis/firewallRules/delete|Elimina le regole del firewall per gli indirizzi IP di una cache Redis|
|/redis/listUpgradeNotifications/read|Elenco hello notifiche di aggiornamento più recente per tenant della cache di hello.|
|/redis/linkedservers/read|Ottiene i server collegati associati a una cache Redis.|
|/redis/linkedservers/write|Aggiungere il Server collegato tooa Cache Redis|
|/redis/linkedservers/delete|Elimina un server collegato da una cache Redis|
|/redis/patchSchedules/read|Ottiene hello patch pianificazione di una Cache Redis|
|/redis/patchSchedules/write|Modificare l'applicazione di patch pianificazione di una Cache Redis hello|
|/redis/patchSchedules/delete|Eliminare hello patch pianificazione di una Cache Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Operazione | Descrizione |
|---|---|
|/provisionGlobalAppServicePrincipalInUserTenant/Action|Esegue il provisioning dell'entità servizio per l'entità app del servizio|
|/validateCertificateRegistrationInformation/Action|Convalida l'oggetto acquisto di certificato senza inviarlo|
|/register/action|Registrazione provider di risorse hello Certificates Microsoft per la sottoscrizione di hello|
|/certificateOrders/Write|Aggiunge un nuovo ordine di certificato o ne aggiorna uno esistente|
|/certificateOrders/Delete|Elimina un certificato del servizio app esistente|
|/certificateOrders/Read|Ottenere l'elenco di hello di CertificateOrders|
|/certificateOrders/reissue/Action|Riemette un ordine di certificato esistente|
|/certificateOrders/renew/Action|Rinnova un ordine di certificato esistente|
|/certificateOrders/retrieveCertificateActions/Action|Recuperare l'elenco di hello di azioni di certificato|
|/certificateOrders/retrieveEmailHistory/Action|Recupera la cronologia della posta elettronica di certificato|
|/certificateOrders/resendEmail/Action|Invia di nuovo la posta elettronica di certificato|
|/certificateOrders/verifyDomainOwnership/Action|Verificare la proprietà del dominio|
|/certificateOrders/resendRequestEmails/Action|Inviare di nuovo indirizzo di posta elettronica tooanother messaggi di posta elettronica di richiesta|
|/certificateOrders/resendRequestEmails/Action|Recupera il sealing di sito per un certificato del servizio app emesso|
|/certificateOrders/certificates/Write|Aggiunge un nuovo certificato o ne aggiorna uno esistente|
|/certificateOrders/certificates/Delete|Elimina un certificato esistente|
|/certificateOrders/certificates/Read|Ottenere l'elenco di hello dei certificati|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare tooClassic calcolo|
|/checkDomainNameAvailability/action|Controlla la disponibilità di hello di un nome di dominio specificato.|
|/moveSubscriptionResources/action|Spostare la sottoscrizione diversa tutte le risorse classiche tooa.|
|/validateSubscriptionMoveAvailability/action|Convalidare la disponibilità della sottoscrizione hello per operazione di spostamento classico.|
|/operatingSystemFamilies/read|Elenca hello di famiglie di sistemi operativi guest disponibili in Microsoft Azure e sono elencate le versioni del sistema operativo hello disponibili per ogni f
|/capabilities/read|Vengono illustrate le funzionalità di hello|
|/operatingSystems/read|Elenca le versioni di hello del sistema operativo guest di hello che sono attualmente disponibili in Microsoft Azure.|
|/resourceTypes/skus/read|Ottiene l'elenco di Sku hello per tipi di risorse supportati.|
|/domainNames/read|Restituisce i nomi di dominio hello per le risorse.|
|/domainNames/write|Aggiungere o modificare i nomi di dominio hello per le risorse.|
|/domainNames/delete|Rimuovere i nomi di dominio hello per le risorse.|
|/domainNames/swap/action|Scambia slot di produzione toohello slot di staging hello.|
|/domainNames/serviceCertificates/read|Restituisce hello certificati di servizio usati.|
|/domainNames/serviceCertificates/write|Aggiungere o modificare i certificati di servizio hello usati.|
|/domainNames/serviceCertificates/delete|Eliminare i certificati di servizio hello usati.|
|/domainNames/serviceCertificates/operationStatuses/read|Legge dello stato dell'operazione per i certificati di servizio nomi di dominio di hello hello.|
|/domainNames/capabilities/read|Mostra le funzionalità di nome di dominio hello|
|/domainNames/extensions/read|Restituisce hello le estensioni dei nomi di dominio.|
|/domainNames/extensions/write|Aggiungere le estensioni dei nomi di dominio hello.|
|/domainNames/extensions/delete|Rimuovere le estensioni dei nomi di dominio hello.|
|/domainNames/extensions/operationStatuses/read|Legge dello stato dell'operazione hello per estensioni dei nomi di dominio hello.|
|/domainNames/active/write|Imposta il nome di dominio active hello.|
|/domainNames/slots/read|Mostra gli slot di distribuzione hello.|
|/domainNames/slots/write|Crea o aggiorna una distribuzione di hello.|
|/domainNames/slots/delete|Elimina uno slot di distribuzione specifico.|
|/domainNames/slots/start/action|Avvia uno slot di distribuzione.|
|/domainNames/slots/stop/action|Sospende lo slot di distribuzione hello.|
|/domainNames/slots/operationStatuses/read|Legge dello stato dell'operazione hello per slot dei nomi di dominio hello.|
|/domainNames/slots/roles/read|Ottenere il ruolo di hello di slot di distribuzione hello.|
|/domainNames/slots/roles/extensionReferences/read|Restituisce hello riferimento all'estensione per ruolo dello slot di distribuzione hello.|
|/domainNames/slots/roles/extensionReferences/write|Aggiungere o modificare il riferimento dell'estensione di hello per ruolo dello slot di distribuzione hello.|
|/domainNames/slots/roles/extensionReferences/delete|Rimuovere il riferimento estensione hello per ruolo dello slot di distribuzione hello.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/read|Legge dello stato dell'operazione per i riferimenti all'estensione ruoli slot di hello dominio nomi hello.|
|/domainNames/slots/roles/roleInstances/read|Ottenere l'istanza del ruolo hello.|
|/domainNames/slots/roles/roleInstances/restart/action|Riavvia le istanze del ruolo.|
|/domainNames/slots/roles/roleInstances/reimage/action|Istanza del ruolo reimages hello.|
|/domainNames/slots/roles/roleInstances/operationStatuses/read|Legge dello stato dell'operazione hello per le istanze del ruolo ruoli slot nomi dominio hello.|
|/domainNames/slots/state/start/write|Le modifiche hello toostopped stato dello slot di distribuzione.|
|/domainNames/slots/state/stop/write|Le modifiche hello toostarted stato dello slot di distribuzione.|
|/domainNames/slots/upgradeDomain/write|Vengono illustrati il dominio di aggiornamento hello.|
|/domainNames/internalLoadBalancers/read|Ottiene i servizi di bilanciamento del carico interno hello.|
|/domainNames/internalLoadBalancers/write|Crea un nuovo bilanciamento del carico interno.|
|/domainNames/internalLoadBalancers/delete|Rimuove un nuovo bilanciamento del carico interno.|
|/domainNames/internalLoadBalancers/operationStatuses/read|Legge dello stato dell'operazione hello per servizi di bilanciamento del carico interno dei nomi di dominio hello.|
|/domainNames/loadBalancedEndpointSets/read|Mostra set di endpoint con carico bilanciato hello|
|/domainNames/loadBalancedEndpointSets/operationStatuses/read|Legge dello stato dell'operazione hello per set di endpoint con carico bilanciato dei nomi di dominio hello.|
|/domainNames/availabilitySets/read|Mostra la disponibilità di hello impostare per la risorsa hello.|
|/quotas/read|Ottenere la quota di hello per sottoscrizione hello.|
|/virtualMachines/read|Recupera l'elenco delle macchine virtuali.|
|/virtualMachines/write|Aggiunge o modifica le macchine virtuali.|
|/virtualMachines/delete|Rimuove le macchine virtuali.|
|/virtualMachines/start/action|Avviare la macchina virtuale hello.|
|/virtualMachines/redeploy/action|Ridistribuisce macchina virtuale hello.|
|/virtualMachines/restart/action|Riavvia le macchine virtuali.|
|/virtualMachines/stop/action|Arresta hello macchina virtuale.|
|/virtualMachines/shutdown/action|Spegnere la macchina virtuale hello.|
|/virtualMachines/attachDisk/action|Collega una macchina virtuale tooa di dati su disco.|
|/virtualMachines/detachDisk/action|Scollega un disco dati da una macchina virtuale.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/action|Scarica il file RDP hello per la macchina virtuale.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/read|Ottiene hello gruppo di sicurezza di rete associato hello interfaccia di rete.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/write|Aggiunge un gruppo di sicurezza di rete associato hello interfaccia di rete.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/delete|Elimina gruppo di sicurezza di rete hello associato hello interfaccia di rete.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/operationStatuses/read|Legge dello stato dell'operazione hello per le macchine virtuali hello associate a gruppi di sicurezza di rete.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/read|Ottiene le definizioni di metriche di hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/read|Ottenere le impostazioni di diagnostica hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/write|Aggiunge o modifica le impostazioni di diagnostica.|
|/virtualMachines/metrics/read|Ottiene la metrica di hello.|
|/virtualMachines/operationStatuses/read|Legge dello stato dell'operazione hello per le macchine virtuali hello.|
|/virtualMachines/extensions/read|Ottiene l'estensione della macchina virtuale hello.|
|/virtualMachines/extensions/write|Inserisce l'estensione della macchina virtuale hello.|
|/virtualMachines/extensions/operationStatuses/read|Legge dello stato dell'operazione hello per le estensioni di macchine virtuali hello.|
|/virtualMachines/asyncOperations/read|Ottiene le operazioni asincrone possibili hello|
|/virtualMachines/disks/read|Recupera l'elenco dei dischi dati|
|/virtualMachines/associatedNetworkSecurityGroups/read|Ottiene hello gruppo di sicurezza di rete associata a una macchina virtuale hello.|
|/virtualMachines/associatedNetworkSecurityGroups/write|Aggiunge un gruppo di sicurezza di rete associato a una macchina virtuale hello.|
|/virtualMachines/associatedNetworkSecurityGroups/delete|Elimina gruppo di sicurezza di rete hello associata a una macchina virtuale hello.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/read|Legge dello stato dell'operazione hello per le macchine virtuali hello associate a gruppi di sicurezza di rete.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare tooClassic rete|
|/gatewaySupportedDevices/read|Recupera l'elenco di hello dei dispositivi supportati.|
|/reservedIps/read|Ottiene hello IP riservati|
|/reservedIps/write|Aggiunge un nuovo IP riservato|
|/reservedIps/delete|Elimina un IP riservato.|
|/reservedIps/link/action|Collega un IP riservato|
|/reservedIps/join/action|Unisce un IP riservato|
|/reservedIps/operationStatuses/read|Legge dello stato dell'operazione per gli indirizzi IP riservato hello hello.|
|/virtualNetworks/read|Ottenere la rete virtuale hello.|
|/virtualNetworks/write|Aggiunge una nuova rete virtuale.|
|/virtualNetworks/delete|Consente di eliminare la rete virtuale hello.|
|/virtualNetworks/peer/action|Associa una rete virtuale a un'altra rete virtuale.|
|/virtualNetworks/join/action|Crea un join tra la rete virtuale hello.|
|/virtualNetworks/checkIPAddressAvailability/action|Controlla la disponibilità di hello di un determinato indirizzo IP in una rete virtuale.|
|/virtualNetworks/capabilities/read|Vengono illustrate le funzionalità di hello|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/read|Ottiene hello gruppo di sicurezza di rete associato alla subnet hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/write|Aggiunge un gruppo di sicurezza di rete associato alla subnet hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/delete|Elimina gruppo di sicurezza di rete hello associato hello subnet.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/operationStatuses/read|Legge dello stato dell'operazione hello per gruppo di sicurezza di rete associato subnet di rete virtuale hello.|
|/virtualNetworks/operationStatuses/read|Legge dello stato dell'operazione hello per le reti virtuali hello.|
|/virtualNetworks/gateways/read|Ottiene il gateway di rete virtuale hello.|
|/virtualNetworks/gateways/write|Aggiunge un gateway di rete virtuale.|
|/virtualNetworks/gateways/delete|Elimina il gateway di rete virtuale hello.|
|/virtualNetworks/gateways/startDiagnostics/action|Avvia la diagnostica per il gateway di rete virtuale hello.|
|/virtualNetworks/gateways/stopDiagnostics/action|Arresta hello diagnostica per il gateway di rete virtuale hello.|
|/virtualNetworks/gateways/downloadDiagnostics/action|Download di diagnostica del gateway hello.|
|/virtualNetworks/gateways/listCircuitServiceKey/action|Recupera una chiave del servizio hello circuito.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/action|Scarica script di configurazione del dispositivo hello.|
|/virtualNetworks/gateways/listPackage/action|Elenca i pacchetti di gateway di rete virtuale hello.|
|/virtualNetworks/gateways/operationStatuses/read|Legge dello stato dell'operazione per i gateway delle reti virtuali hello hello.|
|/virtualNetworks/gateways/packages/read|Ottiene il pacchetto di gateway di hello rete virtuale.|
|/virtualNetworks/gateways/connections/read|Recupera l'elenco di hello delle connessioni.|
|/virtualNetworks/gateways/connections/connect/action|Si connette una connessione gateway da sito toosite.|
|/virtualNetworks/gateways/connections/disconnect/action|Disconnette una connessione gateway da sito toosite.|
|/virtualNetworks/gateways/connections/test/action|Verifica di una connessione gateway da sito toosite.|
|/virtualNetworks/gateways/clientRevokedCertificates/read|Hello lettura revoca i certificati client.|
|/virtualNetworks/gateways/clientRevokedCertificates/write|Revoca un certificato client.|
|/virtualNetworks/gateways/clientRevokedCertificates/delete|Annulla la revoca di un certificato client.|
|/virtualNetworks/gateways/clientRootCertificates/read|Trovare hello certificati radice client.|
|/virtualNetworks/gateways/clientRootCertificates/write|Carica un nuovo certificato radice client.|
|/virtualNetworks/gateways/clientRootCertificates/delete|Elimina certificato client gateway di rete virtuale hello.|
|/virtualNetworks/gateways/clientRootCertificates/download/action|Scarica il certificato in base all'identificazione personale.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/action|Pacchetto certificato gateway di rete virtuale hello di elenchi.|
|/networkSecurityGroups/read|Ottiene il gruppo di sicurezza rete hello.|
|/networkSecurityGroups/write|Aggiunge un nuovo gruppo di sicurezza di rete.|
|/networkSecurityGroups/delete|Elimina gruppo di sicurezza di rete hello.|
|/networkSecurityGroups/operationStatuses/read|Legge dello stato dell'operazione hello per gruppo di sicurezza di rete hello.|
|/networkSecurityGroups/securityRules/read|Ottiene la regola di sicurezza hello.|
|/networkSecurityGroups/securityRules/write|Aggiunge o aggiorna una regola di sicurezza.|
|/networkSecurityGroups/securityRules/delete|Elimina regola di sicurezza hello.|
|/networkSecurityGroups/securityRules/operationStatuses/read|Legge dello stato dell'operazione hello per regole di sicurezza di gruppo di sicurezza di rete di hello.|
|/quotas/read|Ottenere la quota di hello per sottoscrizione hello.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare tooClassic archiviazione|
|/checkStorageAccountAvailability/action|Verifica disponibilità hello di un account di archiviazione.|
|/capabilities/read|Vengono illustrate le funzionalità di hello|
|/publicImages/read|Ottiene l'immagine di macchina virtuale pubblico hello.|
|/images/read|Immagine di hello restituisce.|
|/storageAccounts/read|Restituisce l'account di archiviazione hello con hello dato account.|
|/storageAccounts/write|Aggiunge un nuovo account di archiviazione.|
|/storageAccounts/delete|Eliminare l'account di archiviazione hello.|
|/storageAccounts/listKeys/action|Elenca le chiavi di accesso hello per gli account di archiviazione hello.|
|/storageAccounts/regenerateKey/action|Rigenera chiavi di accesso per account di archiviazione hello esistenti hello.|
|/storageAccounts/operationStatuses/read|Legge dello stato dell'operazione per la risorsa hello hello.|
|/storageAccounts/images/read|Restituisce hello immagine dell'account di archiviazione.|
|/storageAccounts/images/delete|Elimina una data immagine dell'account di archiviazione.|
|/storageAccounts/disks/read|Restituisce hello disco account di archiviazione.|
|/storageAccounts/disks/write|Aggiunge un disco dell'account di archiviazione.|
|/storageAccounts/disks/delete|Elimina un disco specifico dell'account di archiviazione.|
|/storageAccounts/disks/operationStatuses/read|Legge dello stato dell'operazione per la risorsa hello hello.|
|/storageAccounts/osImages/read|Restituisce hello immagine del sistema operativo dell'account di archiviazione.|
|/storageAccounts/osImages/delete|Elimina un'immagine specifica del sistema operativo dell'account di archiviazione.|
|/storageAccounts/services/read|Ottenere servizi disponibili hello.|
|/storageAccounts/services/metricDefinitions/read|Ottiene le definizioni di metriche di hello.|
|/storageAccounts/services/metrics/read|Ottiene la metrica di hello.|
|/storageAccounts/services/diagnosticSettings/read|Ottenere le impostazioni di diagnostica hello.|
|/storageAccounts/services/diagnosticSettings/write|Consente di aggiungere o modificare le impostazioni di diagnostica.|
|/disks/read|Restituisce hello disco account di archiviazione.|
|/osImages/read|Immagine del sistema operativo restituisce hello.|
|/quotas/read|Ottenere la quota di hello per sottoscrizione hello.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Operazione | Descrizione |
|---|---|
|/accounts/read|Legge gli account delle API.|
|/accounts/write|Scrive gli account delle API.|
|/accounts/delete|Elimina gli account delle API|
|/accounts/listKeys/action|Elenco delle chiavi|
|/accounts/regenerateKey/action|Rigenerazione della chiave|
|/accounts/skus/read|Legge gli SKU disponibili per una risorsa esistente.|
|/accounts/usages/read|Ottenere l'utilizzo della quota di hello per una risorsa esistente.|
|/Operations/read|Descrizione dell'operazione di hello.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Operazione | Descrizione |
|---|---|
|/RateCard/read|Restituisce offrono dati, metadati o misuratore risorse e tariffe per hello sottoscrizione specificata.|
|/UsageAggregates/read|Recupera il consumo di Microsoft Azure da una sottoscrizione. il risultato di Hello contiene funzioni di aggregazione dati di utilizzo, sottoscrizione e della risorsa informazioni correlate, in un intervallo di tempo specifico.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Operazione | Descrizione |
|---|---|
|/register/action|Registra la sottoscrizione con il provider di risorse Microsoft.Compute|
|/restorePointCollections/read|Ottenere le proprietà di hello di un insieme di punti di ripristino|
|/restorePointCollections/write|Crea un nuovo insieme di punti di ripristino o aggiorna un insieme esistente|
|/restorePointCollections/delete|Eliminazioni hello insieme di punti di ripristino e i punti di ripristino di contenuto|
|/restorePointCollections/restorePoints/read|Ottenere le proprietà di hello di un punto di ripristino|
|/restorePointCollections/restorePoints/write|Crea un nuovo punto di ripristino|
|/restorePointCollections/restorePoints/delete|Elimina il punto di ripristino hello|
|/restorePointCollections/restorePoints/retrieveSasUris/action|Ottenere le proprietà di hello di un punto di ripristino con blob URI SAS|
|/virtualMachineScaleSets/read|Ottenere le proprietà di hello di un set di scalabilità della macchina virtuale|
|/virtualMachineScaleSets/write|Crea un nuovo set di scalabilità di macchine virtuali o ne aggiorna uno esistente|
|/virtualMachineScaleSets/delete|Elimina set di scalabilità della macchina virtuale hello|
|/virtualMachineScaleSets/start/action|Avvia hello le istanze di set di scalabilità della macchina virtuale hello|
|/virtualMachineScaleSets/powerOff/action|Arresta le istanze di hello di set di scalabilità della macchina virtuale hello|
|/virtualMachineScaleSets/restart/action|Riavvia istanze di hello del set di scalabilità della macchina virtuale hello|
|/virtualMachineScaleSets/deallocate/action|Arresta e rilascia le risorse di calcolo di hello per le istanze di hello di set di scalabilità della macchina virtuale hello |
|/virtualMachineScaleSets/manualUpgrade/action|Aggiorna manualmente il modello di toolatest le istanze del set di scalabilità della macchina virtuale hello|
|/virtualMachineScaleSets/scale/action|Scala verticalmente/orizzontalmente il numero di istanze di un set di scalabilità di macchine virtuali|
|/virtualMachineScaleSets/instanceView/read|Ottiene una visualizzazione dell'istanza del set di scalabilità della macchina virtuale hello hello|
|/virtualMachineScaleSets/skus/read|Gli elenchi di hello SKU valide per un set di scalabilità macchina virtuale esistente|
|/virtualMachineScaleSets/virtualMachines/read|Recupera le proprietà di hello di una macchina virtuale in un Set di scalabilità della macchina virtuale|
|/virtualMachineScaleSets/virtualMachines/delete|Elimina una specifica macchina virtuale in un set di scalabilità VM.|
|/virtualMachineScaleSets/virtualMachines/start/action|Avvia un'istanza di macchina virtuale in un set di scalabilità VM.|
|/virtualMachineScaleSets/virtualMachines/powerOff/action|Disabilita un'istanza di macchina virtuale in un set di scalabilità VM.|
|/virtualMachineScaleSets/virtualMachines/restart/action|Riavvia un'istanza di macchina virtuale in un set di scalabilità VM.|
|/virtualMachineScaleSets/virtualMachines/deallocate/action|Arresta e rilascia le risorse di calcolo di hello per una macchina virtuale in un Set di scalabilità della macchina virtuale.|
|/virtualMachineScaleSets/virtualMachines/instanceView/read|Recupera visualizzazione hello dell'istanza di una macchina virtuale in un Set di scalabilità della macchina virtuale.|
|/images/read|Ottenere le proprietà di hello di hello immagine|
|/images/write|Crea una nuova immagine o ne aggiorna una esistente|
|/images/delete|Elimina immagine hello|
|/operations/read|Elenca le operazioni disponibili sul provider di risorse Microsoft.Compute|
|/disks/read|Ottenere le proprietà di hello di un disco|
|/disks/write|Crea un nuovo disco o ne aggiorna uno esistente|
|/disks/delete|Eliminazioni hello disco|
|/disks/beginGetAccess/action|Ottenere hello URI SAS di hello disco per l'accesso di blob|
|/disks/endGetAccess/action|Revocare hello URI SAS di hello disco|
|/snapshots/read|Ottenere le proprietà di hello di uno Snapshot|
|/snapshots/write|Crea una nuova snapshot o ne aggiorna una esistente|
|/snapshots/delete|Elimina una snapshot|
|/availabilitySets/read|Ottenere le proprietà di hello un set di disponibilità|
|/availabilitySets/write|Crea un nuovo set di disponibilità o ne aggiorna uno esistente|
|/availabilitySets/delete|Elimina il set di disponibilità hello|
|/availabilitySets/vmSizes/read|Elenca le dimensioni disponibili per la creazione o l'aggiornamento di una macchina virtuale nel set di disponibilità hello|
|/virtualMachines/read|Ottenere le proprietà di hello di una macchina virtuale|
|/virtualMachines/write|Crea una nuova macchina virtuale o ne aggiorna una esistente|
|/virtualMachines/delete|Elimina macchina virtuale hello|
|/virtualMachines/start/action|Avvia la macchina virtuale hello|
|/virtualMachines/powerOff/action|Arresta macchina virtuale hello. Si noti che la macchina virtuale hello continuerà toobe fatturato.|
|/virtualMachines/redeploy/action|Ridistribuisce la macchina virtuale|
|/virtualMachines/restart/action|Riavvia una macchina virtuale hello|
|/virtualMachines/deallocate/action|Arresta macchina virtuale hello e hello rilascia le risorse di calcolo|
|/virtualMachines/generalize/action|Imposta tooGeneralized stato macchina virtuale di hello e prepara una macchina virtuale hello per l'acquisizione|
|/virtualMachines/capture/action|Acquisisce una macchina virtuale hello copiando i dischi rigidi virtuali e genera un modello che può essere utilizzato toocreate le macchine virtuali simili|
|/virtualMachines/convertToManagedDisks/action|Converte i dischi di blob in base hello di dischi di toomanaged hello macchina virtuale|
|/virtualMachines/vmSizes/read|Elenca le dimensioni disponibili macchina virtuale hello può essere aggiornato a|
|/virtualMachines/instanceView/read|Ottiene hello lo stato di runtime dettagliato della macchina virtuale hello e le relative risorse|
|/virtualMachines/extensions/read|Ottenere le proprietà di hello di un'estensione della macchina virtuale|
|/virtualMachines/extensions/write|Crea una nuova estensione macchina virtuale o ne aggiorna una esistente|
|/virtualMachines/extensions/delete|Elimina l'estensione della macchina virtuale hello|
|/locations/vmSizes/read|Elenca le dimensioni delle macchine virtuali disponibili in una posizione|
|/locations/usages/read|Ottiene i limiti dei servizi e quantità di utilizzo correnti per le risorse di calcolo della sottoscrizione hello in una posizione|
|/locations/operations/read|Ottiene lo stato di hello di un'operazione asincrona|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse di hello contenitore del Registro di sistema e consente la creazione di hello di registri di contenitore.|
|/checknameavailability/read|Controlla che il nome del registro sia valido e che non sia in uso.|
|/registries/read|Restituisce l'elenco di registri di contenitore di hello o ottiene hello le proprietà del Registro di sistema di hello contenitore specificato.|
|/registries/write|Crea un registro di sistema contenitore hello parametri specificati o aggiornare le proprietà di hello o tag per registro di sistema di hello contenitore specificato.|
|/registries/delete|Elimina un registro contenitori esistente.|
|/registries/listCredentials/action|Elenca le credenziali di accesso hello del Registro di sistema di hello contenitore specificato.|
|/registries/regenerateCredential/action|Rigenera le credenziali di accesso hello del Registro di sistema di hello contenitore specificato.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Operazione | Descrizione |
|---|---|
|/containerServices/subscriptions/read|Get hello servizi contenitore specificati in base a una sottoscrizione|
|/containerServices/resourceGroups/read|Get hello servizi contenitore specificati in base a gruppo di risorse|
|/containerServices/resourceGroups/ContainerServiceName/read|Ottiene hello specificato servizio contenitore|
|/containerServices/resourceGroups/ContainerServiceName/write|Inserisce o hello aggiornamenti specificato servizio contenitore|
|/containerServices/resourceGroups/ContainerServiceName/delete|Eliminazioni hello specificato servizio contenitore|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Operazione | Descrizione |
|---|---|
|/updateCommunicationPreference/action|Aggiorna le preferenze di comunicazione|
|/listCommunicationPreference/action|Elenca le preferenze di comunicazione|
|/applications/read|Operazione di lettura|
|/applications/write|Operazione di scrittura|
|/applications/write|Operazione di scrittura|
|/applications/delete|Operazione di eliminazione|
|/applications/listSecrets/action|Elenca i segreti|
|/applications/listSingleSignOnToken/action|Esegue la lettura di token Single Sign-On|
|/operations/read|operazioni di lettura|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Operazione | Descrizione |
|---|---|
|/hubs/read|Esegue la lettura di qualsiasi hub di Azure Customer Insights|
|/hubs/write|Crea o aggiorna qualsiasi hub di Azure Customer Insights|
|/hubs/delete|Elimina qualsiasi hub di Azure Customer Insights|
|/hubs/providers/Microsoft.Insights/metricDefinitions/read|Ottiene la metrica di hello disponibili per la risorsa|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/read|Ottiene l'impostazione di diagnostica hello per risorse hello|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/write|Crea o aggiorna l'impostazione di diagnostica di hello per risorsa hello|
|/hubs/providers/Microsoft.Insights/logDefinitions/read|Ottiene i log disponibili hello per risorsa|
|/hubs/authorizationPolicies/read|Esegue la lettura di qualsiasi criterio di firma di accesso condiviso di Azure Customer Insights|
|/hubs/authorizationPolicies/write|Crea o aggiorna qualsiasi criterio di firma di accesso condiviso di Azure Customer Insights|
|/hubs/authorizationPolicies/delete|Elimina qualsiasi criterio di firma di accesso condiviso di Azure Customer Insights|
|/hubs/authorizationPolicies/regeneratePrimaryKey/action|Rigenera la chiave primaria dei criteri di firma di accesso condiviso di Azure Customer Insights|
|/hubs/authorizationPolicies/regenerateSecondaryKey/action|Rigenera la chiave secondaria dei criteri di firma di accesso condiviso di Azure Customer Insights|
|/hubs/profiles/read|Esegue la lettura di qualsiasi profilo di Azure Customer Insights|
|/hubs/profiles/write|Esegue la scrittura di qualsiasi profilo di Azure Customer Insights|
|/hubs/kpi/read|Esegue la lettura di qualsiasi indicatore di prestazioni chiave di Azure Customer Insights|
|/hubs/kpi/write|Crea o aggiorna qualsiasi indicatore di prestazioni chiave Azure Customer Insights|
|/hubs/kpi/delete|Elimina qualsiasi indicatore di prestazioni chiave Azure Customer Insights|
|/hubs/views/read|Esegue la lettura di qualsiasi visualizzazione app di Azure Customer Insights|
|/hubs/views/write|Crea o aggiorna qualsiasi visualizzazione app di Azure Customer Insights|
|/hubs/views/delete|Elimina qualsiasi visualizzazione app di Azure Customer Insights|
|/hubs/interactions/read|Esegue la lettura di qualsiasi interazione di Azure Customer Insights|
|/hubs/interactions/write|Crea o aggiorna qualsiasi interazione di Azure Customer Insights|
|/hubs/roleAssignments/read|Esegue la lettura di qualsiasi assegnazione di controllo degli accessi in base al ruolo di Azure Customer Insights|
|/hubs/roleAssignments/write|Crea o aggiorna qualsiasi assegnazione di controllo degli accessi in base al ruolo di Azure Customer Insights|
|/hubs/roleAssignments/delete|Elimina qualsiasi assegnazione di controllo degli accessi in base al ruolo di Azure Customer Insights|
|/hubs/connectors/read|Esegue la lettura di qualsiasi connettore Azure Customer Insights|
|/hubs/connectors/write|Crea o aggiorna qualsiasi connettore Azure Customer Insights|
|/hubs/connectors/delete|Elimina qualsiasi connettore Azure Customer Insights|
|/hubs/connectors/mappings/read|Esegue la lettura di qualsiasi mapping di connettori Azure Customer Insights|
|/hubs/connectors/mappings/write|Crea o aggiorna qualsiasi mapping di connettori Azure Customer Insights|
|/hubs/connectors/mappings/delete|Elimina qualsiasi mapping di connettori Azure Customer Insights|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Operazione | Descrizione |
|---|---|
|/checkNameAvailability/action|Controlla la disponibilità del nome di catalogo per il tenant.|
|/catalogs/read|Ottiene le proprietà del catalogo o dei cataloghi nella sottoscrizione o nel gruppo di risorse.|
|/catalogs/write|Crea tag hello catalogo o gli aggiornamenti e le proprietà per il catalogo di hello.|
|/catalogs/delete|Elimina catalogo hello.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Operazione | Descrizione |
|---|---|
|/datafactories/read|Esegue la lettura del data factory.|
|/datafactories/write|Crea o aggiorna il data factory|
|/datafactories/delete|Elimina il data factory.|
|/datafactories/datapipelines/read|Esegue la lettura della pipeline.|
|/datafactories/datapipelines/delete|Elimina la pipeline.|
|/datafactories/datapipelines/pause/action|Sospende la pipeline.|
|/datafactories/datapipelines/resume/action|Riavvia la pipeline.|
|/datafactories/datapipelines/update/action|Aggiorna la pipeline.|
|/datafactories/datapipelines/write|Crea o aggiorna la pipeline|
|/datafactories/linkedServices/read|Esegue la lettura del servizio collegato.|
|/datafactories/linkedServices/delete|Elimina il servizio collegato.|
|/datafactories/linkedServices/write|Crea o aggiorna il servizio collegato|
|/datafactories/tables/read|Esegue la lettura di una tabella.|
|/datafactories/tables/delete|Elimina una tabella.|
|/datafactories/tables/write|Crea o aggiorna una tabella|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Operazione | Descrizione |
|---|---|
|/accounts/read|Ottenere informazioni sull'account DataLakeAnalytics hello.|
|/accounts/write|Crea o Aggiorna account DataLakeAnalytics hello.|
|/accounts/delete|Eliminare l'account DataLakeAnalytics hello.|
|/accounts/firewallRules/read|Ottiene informazioni su una regola del firewall.|
|/accounts/firewallRules/write|Crea o aggiorna una regola del firewall.|
|/accounts/firewallRules/delete|Elimina una regola del firewall.|
|/accounts/storageAccounts/read|Ottenere l'account di archiviazione collegato per hello DataLakeAnalytics account.|
|/accounts/storageAccounts/write|Collegare un toohello di account di archiviazione DataLakeAnalytics account.|
|/accounts/storageAccounts/delete|Scollegare un account di archiviazione da hello DataLakeAnalytics account.|
|/accounts/storageAccounts/Containers/read|Ottenere i contenitori in hello account di archiviazione|
|/accounts/storageAccounts/Containers/listSasTokens/action|Elenco di token SAS hello contenitore di archiviazione|
|/accounts/dataLakeStoreAccounts/read|Ottenere l'account DataLakeStore collegato per hello DataLakeAnalytics account.|
|/accounts/dataLakeStoreAccounts/write|Collegare un toohello account DataLakeStore DataLakeAnalytics account.|
|/accounts/dataLakeStoreAccounts/delete|Scollegare un conto DataLakeStore da hello DataLakeAnalytics account.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Operazione | Descrizione |
|---|---|
|/accounts/read|Ottiene informazioni su un account DataLakeStore esistente.|
|/accounts/write|Crea un nuovo account DataLakeStore o aggiorna un account DataLakeStore esistente.|
|/accounts/delete|Elimina un account DataLakeStore esistente.|
|/accounts/firewallRules/read|Ottiene informazioni su una regola del firewall.|
|/accounts/firewallRules/write|Crea o aggiorna una regola del firewall.|
|/accounts/firewallRules/delete|Elimina una regola del firewall.|
|/accounts/trustedIdProviders/read|Ottiene informazioni su un provider di identità attendibile.|
|/accounts/trustedIdProviders/write|Crea o aggiorna un provider di identità attendibile.|
|/accounts/trustedIdProviders/delete|Elimina un provider di identità attendibile.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare la sottoscrizione di hello per hello hub IOT resource provider Abilita hello la creazione e di risorse hub IOT|
|/checkNameAvailability/Action|Controlla se il nome IotHub è disponibile|
|/usages/Read|Ottiene dettagli sull'utilizzo della sottoscrizione per questo provider.|
|/operations/Read|Ottiene tutte le operazioni ResourceProvider|
|/iotHubs/Read|Ottiene le risorse di hello hub IOT|
|/iotHubs/Write|Crea o aggiorna una risorsa IotHub|
|/iotHubs/Delete|Elimina una risorsa IotHub|
|/iotHubs/listkeys/Action|Ottiene tutte le chiavi IotHub|
|/iotHubs/exportDevices/Action|Esporta dispositivi|
|/iotHubs/importDevices/Action|Importa dispositivi|
|/IotHubs/metricDefinitions/read|Ottiene le metriche disponibili hello per hello servizio hub IOT|
|/iotHubs/iotHubKeys/listkeys/Action|Ottenere IotHub Key il nome specificato hello|
|/iotHubs/iotHubStats/Read|Ottiene le statistiche IotHub|
|/iotHubs/quotaMetrics/Read|Ottiene la metrica di quota|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Crea un gruppo di consumer EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Ottiene il gruppo o i gruppi di consumer EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Delete|Elimina un gruppo di consumer EventHub|
|/iotHubs/routing/routes/$testall/Action|Effettua il test di un messaggio con tutte le route esistenti|
|/iotHubs/routing/routes/$testnew/Action|Effettua il test di un messaggio con la route di test fornita|
|/IotHubs/diagnosticSettings/read|Ottiene l'impostazione di diagnostica hello per risorse hello|
|/IotHubs/diagnosticSettings/write|Crea o aggiorna l'impostazione di diagnostica di hello per risorsa hello|
|/iotHubs/skus/Read|Ottiene gli SKU IotHub validi|
|/iotHubs/jobs/Read|Ottiene i dettagli del processo o dei processi inviati per un servizio IotHub specifico|
|/iotHubs/routingEndpointsHealth/Read|Ottiene l'integrità di hello di tutti gli endpoint di routing per un hub IOT|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Operazione | Descrizione |
|---|---|
|/Subscription/register/action|Registra sottoscrizione hello|
|/labs/delete|Elimina lab.|
|/labs/read|Esegue la lettura di lab.|
|/labs/write|Aggiunge o modifica lab.|
|/labs/ListVhds/action|Elenca le immagini di un disco disponibili per la creazione di immagini personalizzate.|
|/labs/GenerateUploadUri/action|Generare un URI per il caricamento personalizzato disco immagini tooa Lab.|
|/labs/CreateEnvironment/action|Crea macchine virtuali in un lab.|
|/labs/ClaimAnyVm/action|Richiedere una macchina virtuale claimable casuale nell'ambiente lab hello.|
|/labs/ExportResourceUsage/action|Esportazioni hello dell'utilizzo delle risorse lab in un account di archiviazione|
|/labs/users/delete|Elimina profili utente.|
|/labs/users/read|Esegue la lettura di profili utente.|
|/labs/users/write|Aggiunge o modifica profili utente.|
|/labs/users/secrets/delete|Elimina segreti.|
|/labs/users/secrets/read|Esegue la lettura di segreti.|
|/labs/users/secrets/write|Aggiunge o modifica segreti.|
|/labs/users/environments/delete|Elimina ambienti.|
|/labs/users/environments/read|Esegue la lettura di ambienti.|
|/labs/users/environments/write|Aggiunge o modifica ambienti.|
|/labs/users/disks/delete|Elimina dischi.|
|/labs/users/disks/read|Esegue la lettura di dischi.|
|/labs/users/disks/write|Aggiunge o modifica dischi.|
|/labs/users/disks/Attach/action|Collegare e creare lease hello della macchina virtuale di hello disco toohello.|
|/labs/users/disks/Detach/action|Scollegare e lease hello interruzione del disco hello collegato macchina virtuale toohello.|
|/labs/customImages/delete|Elimina immagini personalizzate.|
|/labs/customImages/read|Esegue la lettura di immagini personalizzate.|
|/labs/customImages/write|Aggiunge o modifica immagini personalizzate.|
|/labs/serviceRunners/delete|Elimina strumenti di esecuzione servizio.|
|/labs/serviceRunners/read|Esegue la lettura di strumenti di esecuzione servizio.|
|/labs/serviceRunners/write|Aggiunge o modifica strumenti di esecuzione servizio.|
|/labs/artifactSources/delete|Elimina origini elemento.|
|/labs/artifactSources/read|Esegue la lettura di origini elemento.|
|/labs/artifactSources/write|Aggiunge o modifica origini elemento.|
|/labs/artifactSources/artifacts/read|Esegue la lettura di elementi.|
|/labs/artifactSources/artifacts/GenerateArmTemplate/action|Genera un modello ARM per hello dato elemento, carica l'account di archiviazione tooa hello necessario file e convalida artefatto hello generato.|
|/labs/artifactSources/armTemplates/read|Esegue la lettura di modelli di Azure Resource Manager.|
|/labs/costs/read|Esegue la lettura di costi.|
|/labs/costs/write|Aggiunge o modifica costi.|
|/labs/virtualNetworks/delete|Elimina reti virtuali.|
|/labs/virtualNetworks/read|Esegue la lettura di reti virtuali.|
|/labs/virtualNetworks/write|Aggiunge o modifica reti virtuali.|
|/labs/formulas/delete|Elimina le formule.|
|/labs/formulas/read|Esegue la lettura di formule.|
|/labs/formulas/write|Aggiunge o modifica le formule.|
|/labs/schedules/delete|Elimina le pianificazioni.|
|/labs/schedules/read|Esegue la lettura delle pianificazioni.|
|/labs/schedules/write|Aggiunge o modifica pianificazioni.|
|/labs/schedules/Execute/action|Esegue una pianificazione.|
|/labs/schedules/ListApplicable/action|Elenca tutte le pianificazioni applicabili|
|/labs/galleryImages/read|Esegue la lettura delle immagini della raccolta.|
|/labs/policySets/EvaluatePolicies/action|Valuta i criteri del lab.|
|/labs/policySets/policies/delete|Elimina i criteri.|
|/labs/policySets/policies/read|Esegue la lettura di criteri.|
|/labs/policySets/policies/write|Aggiunge o modifica i criteri.|
|/labs/virtualMachines/delete|Elimina macchine virtuali.|
|/labs/virtualMachines/read|Esegue la lettura di macchine virtuali.|
|/labs/virtualMachines/write|Aggiunge o modifica macchine virtuali.|
|/labs/virtualMachines/Start/action|Avvia una macchina virtuale.|
|/labs/virtualMachines/Stop/action|Arrestare una macchina virtuale|
|/labs/virtualMachines/ApplyArtifacts/action|Applicare macchina toovirtual elementi.|
|/labs/virtualMachines/AddDataDisk/action|Collegare una macchina di toovirtual disco dati nuovi o esistenti.|
|/labs/virtualMachines/DetachDataDisk/action|Scollegare il disco specificato di hello dalla macchina virtuale hello.|
|/labs/virtualMachines/Claim/action|Consente di assumere la proprietà di una macchina virtuale esistente|
|/labs/virtualMachines/ListApplicableSchedules/action|Elenca tutte le pianificazioni applicabili|
|/labs/virtualMachines/schedules/delete|Elimina le pianificazioni.|
|/labs/virtualMachines/schedules/read|Esegue la lettura delle pianificazioni.|
|/labs/virtualMachines/schedules/write|Aggiunge o modifica pianificazioni.|
|/labs/virtualMachines/schedules/Execute/action|Esegue una pianificazione.|
|/labs/notificationChannels/delete|Elimina canali di notifica.|
|/labs/notificationChannels/read|Esegue la lettura di canali di notifica.|
|/labs/notificationChannels/write|Aggiunge o modifica canali di notifica.|
|/labs/notificationChannels/Notify/action|Canale di notifica tooprovided di trasmissione.|
|/schedules/delete|Elimina le pianificazioni.|
|/schedules/read|Esegue la lettura delle pianificazioni.|
|/schedules/write|Aggiunge o modifica pianificazioni.|
|/schedules/Execute/action|Esegue una pianificazione.|
|/schedules/Retarget/action|Aggiorna l'ID risorsa di destinazione di una pianificazione.|
|/locations/operations/read|Esegue la lettura delle operazioni.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Operazione | Descrizione |
|---|---|
|/databaseAccountNames/read|Controlla la disponibilità del nome.|
|/databaseAccounts/read|Esegue la lettura di un account di database.|
|/databaseAccounts/write|Aggiorna un account di database.|
|/databaseAccounts/listKeys/action|Elenca le chiavi di un account di database|
|/databaseAccounts/regenerateKey/action|Ruota le chiavi di un account di database|
|/databaseAccounts/listConnectionStrings/action|Ottenere le stringhe di connessione hello per un account di database|
|/databaseAccounts/changeResourceGroup/action|Modifica il gruppo di risorse di un account di database|
|/databaseAccounts/failoverPriorityChange/action|Modifica le priorità di failover di aree di un account di database. Operazione di failover manuale tooperform utilizzato|
|/databaseAccounts/delete|Elimina l'account di database hello.|
|/databaseAccounts/metricDefinitions/read|Legge l'account del database hello le definizioni di metrica.|
|/databaseAccounts/metrics/read|Legge le metriche di account database hello.|
|/databaseAccounts/usages/read|Legge gli utilizzi di account database hello.|
|/databaseAccounts/databases/collections/metricDefinitions/read|Legge le definizioni delle metriche di raccolta hello.|
|/databaseAccounts/databases/collections/metrics/read|Legge le metriche di hello insieme.|
|/databaseAccounts/databases/collections/usages/read|Legge gli utilizzi di hello insieme.|
|/databaseAccounts/databases/metricDefinitions/read|Legge le definizioni delle metriche di hello database|
|/databaseAccounts/databases/metrics/read|Legge le metriche database hello.|
|/databaseAccounts/databases/usages/read|Legge gli utilizzi database hello.|
|/databaseAccounts/readonlykeys/read|Legge l'account del database hello le chiavi di sola lettura.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Operazione | Descrizione |
|---|---|
|/generateSsoRequest/Action|Genera una richiesta per l'accesso al centro di controllo del dominio.|
|/validateDomainRegistrationInformation/Action|Convalida l'oggetto acquisto di dominio senza inviarlo|
|/checkDomainAvailability/Action|Controlla se un dominio è disponibile per l'acquisto|
|/listDomainRecommendations/Action|Recuperare le indicazioni di dominio elenco hello in base alle parole chiave|
|/register/action|Registrazione provider di risorse hello Domains Microsoft per la sottoscrizione di hello|
|/domains/Read|Ottenere l'elenco di hello dei domini|
|/domains/Write|Aggiunge un nuovo dominio o ne aggiorna uno esistente|
|/domains/Delete|Elimina un dominio esistente.|
|/domains/operationresults/Read|Ottiene un'operazione di dominio|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Operazione | Descrizione |
|---|---|
|/lcsprojects/read|Visualizzare i progetti di servizi di Microsoft Dynamics del ciclo di vita appartenenti tooa utente|
|/lcsprojects/write|Creare e aggiornare i progetti di servizi di Microsoft Dynamics del ciclo di vita toohello utente appartengano. È possibile aggiornare solo le proprietà di nome e una descrizione di hello. Impossibile aggiornare sottoscrizione Hello e il percorso associato hello progetto dopo la creazione|
|/lcsprojects/delete|Eliminare i progetti di servizi di Microsoft Dynamics del ciclo di vita appartenenti toohello utente|
|/lcsprojects/clouddeployments/read|Visualizzare le distribuzioni di Microsoft Dynamics AX 2012 R3 Evaluation in un progetto di servizi di Microsoft Dynamics del ciclo di vita appartenenti tooa utente|
|/lcsprojects/clouddeployments/write|Creare la distribuzione di Microsoft Dynamics AX 2012 R3 Evaluation in un progetto di servizi di Microsoft Dynamics del ciclo di vita appartenenti tooa utente. Le distribuzioni possono essere gestite dal portale di gestione di Azure|
|/lcsprojects/connectors/read|Lettura di connettori che appartengono a progetto di servizi del ciclo di vita di Microsoft Dynamics tooa|
|/lcsprojects/connectors/write|Creare e aggiornare i connettori appartenenti al progetto di servizi del ciclo di vita di Microsoft Dynamics tooa|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Operazione | Descrizione |
|---|---|
|/checkNameAvailability/action|Verifica la disponibilità dello spazio dei nomi nella sottoscrizione specificata.|
|/register/action|Registra sottoscrizione hello per provider di risorse hub eventi hello e consente la creazione di hello di risorse hub eventi.|
|/namespaces/write|Crea una risorsa spazio dei nomi e ne aggiorna le proprietà. Tag e lo stato di hello Namespace sono proprietà hello che può essere aggiornata.|
|/namespaces/read|Ottenere l'elenco di hello della descrizione della risorsa Namespace|
|/namespaces/Delete|Elimina una risorsa spazio dei nomi|
|/namespaces/metricDefinitions/read|Ottiene l'elenco di descrizioni delle risorse metrica dello spazio dei nomi|
|/namespaces/authorizationRules/read|Ottenere l'elenco di hello della descrizione delle regole di autorizzazione di spazi dei nomi.|
|/namespaces/authorizationRules/write|Crea regole di autorizzazione a livello dello spazio dei nomi e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/authorizationRules/delete|Elimina regola di autorizzazione dello spazio dei nomi. Impossibile eliminare Hello regola di autorizzazione Namespace predefinita. |
|/namespaces/authorizationRules/listkeys/action|Ottenere una stringa di connessione di hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Rigenerare hello primario o secondario chiave toohello risorse|
|/namespaces/eventhubs/write|Crea o aggiorna le proprietà dell'hub eventi.|
|/namespaces/eventhubs/read|Ottiene l'elenco delle descrizioni delle risorse dell'hub eventi|
|/namespaces/eventhubs/Delete|Operazione toodelete risorse hub eventi|
|/namespaces/eventHubs/consumergroups/write|Crea o aggiorna le proprietà del gruppo consumer.|
|/namespaces/eventHubs/consumergroups/read|Ottiene l'elenco delle descrizioni delle risorse gruppo consumer|
|/namespaces/eventHubs/consumergroups/Delete|Operazione toodelete risorsa gruppo di consumer per|
|/namespaces/eventhubs/authorizationRules/read| Ottenere l'elenco di hello EventHub delle regole di autorizzazione|
|/namespaces/eventhubs/authorizationRules/write|Crea regole di autorizzazione dell'hub eventi e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/eventhubs/authorizationRules/delete|Operazione toodelete EventHub le regole di autorizzazione|
|/namespaces/eventhubs/authorizationRules/listkeys/action|Ottenere hello tooEventHub di stringa di connessione|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/action|Rigenerare hello primario o secondario chiave toohello risorse|
|/namespaces/diagnosticSettings/read|Ottiene l'elenco di descrizioni delle risorse impostazioni di diagnostica dello spazio dei nomi|
|/namespaces/diagnosticSettings/write|Ottiene l'elenco di descrizioni delle risorse impostazioni di diagnostica dello spazio dei nomi|
|/namespaces/logDefinitions/read|Ottiene l'elenco di descrizioni delle risorse log dello spazio dei nomi|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Operazione | Descrizione |
|---|---|
|/providers/features/read|Ottiene la funzionalità hello di una sottoscrizione in un provider di risorse specificato.|
|/providers/features/register/action|Funzionalità di hello registri per una sottoscrizione in un provider di risorse specificato.|
|/features/read|Ottiene le funzionalità di hello di una sottoscrizione.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Operazione | Descrizione |
|---|---|
|/clusters/write|Crea o aggiorna un cluster HDInsight|
|/clusters/read|Ottiene informazioni sul cluster HDInsight|
|/clusters/delete|Elimina un cluster HDInsight|
|/clusters/changerdpsetting/action|Modifica l'impostazione RDP per il cluster HDInsight|
|/clusters/configurations/action|Aggiorna la configurazione del cluster HDInsight|
|/clusters/configurations/read|Ottiene le configurazioni del cluster HDInsight|
|/clusters/roles/resize/action|Ridimensiona un cluster HDInsight|
|/locations/capabilities/read|Ottiene le funzionalità di sottoscrizione|
|/locations/checkNameAvailability/read|Controlla la disponibilità del nome|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse di importazione/esportazione hello e consente la creazione di hello dei processi di importazione/esportazione.|
|/jobs/write|Crea un processo con hello parametri specificati o aggiornare le proprietà di hello o tag per il processo specificato hello.|
|/jobs/read|Ottiene le proprietà di hello per processo specificato hello o restituisce hello elenco di processi.|
|/jobs/listBitLockerKeys/action|Ottiene le chiavi BitLocker hello per processo specificato hello.|
|/jobs/delete|Elimina il processo esistente.|
|/locations/read|Ottiene la proprietà hello hello percorso o restituisce hello elenco specificato di posizioni.|

## <a name="microsoftinsights"></a>Microsoft.Insights

| Operazione | Descrizione |
|---|---|
|/Register/Action|Registrare il provider di informazioni di microsoft hello|
|/AlertRules/Write|Creazione della configurazione tooan regola di avviso|
|/AlertRules/Delete|Eliminazione di una configurazione di regola di avviso|
|/AlertRules/Read|Lettura di una configurazione di regola di avviso|
|/AlertRules/Activated/Action|Regola di avviso attivata|
|/AlertRules/Resolved/Action|Regola di avviso risolta|
|/AlertRules/Throttled/Action|La regola di avviso è limitata|
|/AlertRules/Incidents/Read|Lettura di una configurazione di eventi imprevisti associati alla regola di avviso|
|/MetricDefinitions/Read|Consente di leggere le definizioni della metrica|
|/eventtypes/values/Read|Consente di leggere i valori dei tipi di evento di gestione|
|/eventtypes/digestevents/Read|Consente di leggere il digest dei tipi di evento di gestione|
|/Metrics/Read|Esegue la lettura delle metriche|
|/LogProfiles/Write|Scrittura della configurazione profilo tooa log|
|/LogProfiles/Delete|Elimina configurazione dei profili di log|
|/LogProfiles/Read|Lettura profili di log|
|/AutoscaleSettings/Write|Scrittura di configurazione delle impostazioni di scalabilità automatica tooan|
|/AutoscaleSettings/Delete|Eliminazione di una configurazione di impostazione di scalabilità automatica|
|/AutoscaleSettings/Read|Lettura di una configurazione di impostazione di scalabilità automatica|
|/AutoscaleSettings/Scaleup/Action|Scalabilità automatica: operazione di aumento|
|/AutoscaleSettings/Scaledown/Action|Scalabilità automatica: operazione di riduzione|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Consente di leggere le definizioni della metrica|
|/ActivityLogAlerts/Activated/Action|Trigger hello attività registro avvisi|
|/DiagnosticSettings/Write|Configurazione delle impostazioni di scrittura toodiagnostic|
|/DiagnosticSettings/Delete|È in corso l'eliminazione di una configurazione di impostazioni di diagnostica|
|/DiagnosticSettings/Read|È in corso la lettura di una configurazione di impostazioni di diagnostica|
|/LogDefinitions/Read|Consente di leggere le definizioni del log|
|/ExtendedDiagnosticSettings/Write|Configurazione di impostazioni di diagnostica tooextended scrittura|
|/ExtendedDiagnosticSettings/Delete|È in corso l'eliminazione di una configurazione di impostazioni di diagnostica estese|
|/ExtendedDiagnosticSettings/Read|È in corso la lettura di una configurazione di impostazioni di diagnostica estese|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Operazione | Descrizione |
|---|---|
|/register/action|Registra una sottoscrizione|
|/checkNameAvailability/read|Controlla che il nome dell'insieme di credenziali delle chiavi sia valido e che non sia in uso|
|/vaults/read|Hello di visualizzare le proprietà di un insieme di credenziali chiave|
|/vaults/write|Creare un nuovo hello di insieme di credenziali o aggiornamento chiave le proprietà di un insieme di credenziali chiave esistente|
|/vaults/delete|Elimina un insieme di credenziali delle chiavi|
|/vaults/deploy/action|Abilita toosecrets in un insieme di credenziali chiave di accesso durante la distribuzione di risorse di Azure|
|/vaults/secrets/read|Hello di visualizzare le proprietà di un segreto, ma non il relativo valore.|
|/vaults/secrets/write|Creare un nuovo valore di hello segreto o aggiornamento di un segreto esistente|
|/vaults/accessPolicies/write|Aggiornare un criterio di accesso esistente mediante l'unione o la sostituzione oppure aggiungere un nuovo archivio tooa criteri di accesso.|
|/deletedVaults/read|Visualizzare le proprietà di hello di soft eliminare gli insiemi di credenziali chiave|
|/locations/operationResults/read|Controllo hello risultato di un'operazione a esecuzione prolungata|
|/locations/deletedVaults/read|Visualizzare le proprietà di hello di temporanea eliminato insieme di credenziali chiave|
|/locations/deletedVaults/purge/action|Ripulisce un Key Vault eliminato temporaneamente|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Operazione | Descrizione |
|---|---|
|/workflows/read|Legge flussi di lavoro hello.|
|/workflows/write|Crea o Aggiorna del flusso di lavoro di hello.|
|/workflows/delete|Elimina flusso di lavoro hello.|
|/workflows/run/action|Avvia un'esecuzione del flusso di lavoro hello.|
|/workflows/disable/action|Disabilita il flusso di lavoro hello.|
|/workflows/enable/action|Consente di flusso di lavoro hello.|
|/workflows/validate/action|Convalida del flusso di lavoro di hello.|
|/workflows/move/action|Sposta del flusso di lavoro dal relativo esistente id sottoscrizione, gruppo di risorse e/o id di sottoscrizione diverso tooa nome, gruppo di risorse e/o nome.|
|/workflows/listSwagger/action|Ottiene swagger definizioni di flusso di lavoro hello.|
|/workflows/regenerateAccessKey/action|Rigenera chiave segreti di hello accesso.|
|/workflows/listCallbackUrl/action|Ottiene l'URL callback hello per flusso di lavoro.|
|/workflows/versions/read|Legge una versione di hello del flusso di lavoro.|
|/workflows/versions/triggers/listCallbackUrl/action|Ottiene l'URL callback hello per trigger.|
|/workflows/runs/read|Legge flussi di lavoro hello eseguire.|
|/workflows/runs/cancel/action|Annulla esecuzione hello del flusso di lavoro.|
|/workflows/runs/actions/read|Legge flussi di lavoro hello eseguire l'azione.|
|/workflows/runs/operations/read|Legge flussi di lavoro hello eseguire dello stato dell'operazione.|
|/workflows/triggers/read|Legge il trigger di hello.|
|/workflows/triggers/run/action|Esegue i trigger di hello.|
|/workflows/triggers/listCallbackUrl/action|Ottiene l'URL callback hello per trigger.|
|/workflows/triggers/histories/read|Legge le cronologie trigger hello.|
|/workflows/triggers/histories/resubmit/action|Invia nuovamente il trigger del flusso di lavoro hello.|
|/workflows/accessKeys/read|Legge la chiave di accesso hello.|
|/workflows/accessKeys/write|Crea o aggiorna la chiave di accesso hello.|
|/workflows/accessKeys/delete|Elimina la chiave di accesso hello.|
|/workflows/accessKeys/list/action|Elenca i segreti chiave di accesso hello.|
|/workflows/accessKeys/regenerate/action|Rigenera chiave segreti di hello accesso.|
|/locations/workflows/validate/action|Convalida del flusso di lavoro di hello.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse del servizio web di apprendimento automatico hello e consente la creazione di hello dei servizi web.|
|/webServices/action|Creare proprietà del servizio Web regionali per le aree supportate|
|/commitmentPlans/read|Esegue la lettura di qualsiasi piano di impegno di Machine Learning|
|/commitmentPlans/write|Crea o aggiorna un qualsiasi piano di impegno di Machine Learning|
|/commitmentPlans/delete|Elimina un qualsiasi piano di impegno di Machine Learning|
|/commitmentPlans/join/action|Consente di partecipare a qualsiasi piano di impegno di Machine Learning|
|/commitmentPlans/commitmentAssociations/read|Esegue la lettura di qualsiasi associazione a un piano di impegno di Machine Learning|
|/commitmentPlans/commitmentAssociations/move/action|Sposta qualsiasi associazione a un piano di impegno di Machine Learning|
|/Workspaces/read|Esegue la lettura di una qualsiasi area di lavoro di Machine Learning|
|/Workspaces/write|Crea o aggiorna una qualsiasi area di lavoro di Machine Learning|
|/Workspaces/delete|Elimina una qualsiasi area di lavoro di Machine Learning|
|/Workspaces/listworkspacekeys/action|Elenca le chiavi per un'area di lavoro di Machine Learning|
|/Workspaces/resyncstoragekeys/action|Risincronizza le chiavi dell'account di archiviazione configurato per un'area di lavoro di Machine Learning|
|/webServices/read|Legge qualsiasi servizio Web di Machine Learning.|
|/webServices/write|Crea o aggiorna qualsiasi servizio Web di Machine Learning.|
|/webServices/delete|Elimina qualsiasi servizio Web di Machine Learning.|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Operazione | Descrizione |
|---|---|
|/agreements/offers/plans/read|Restituisce un contratto per uno specifico elemento del marketplace.|
|/agreements/offers/plans/sign/action|Firma un contratto per uno specifico elemento del marketplace.|
|/agreements/offers/plans/cancel/action|Elimina un contratto per uno specifico elemento del marketplace.|

## <a name="microsoftmedia"></a>Microsoft.Media

| Operazione | Descrizione |
|---|---|
|/mediaservices/read||
|/mediaservices/write||
|/mediaservices/delete||
|/mediaservices/regenerateKey/action||
|/mediaservices/listKeys/action||
|/mediaservices/syncStorageKeys/action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello|
|/unregister/action|Annulla la registrazione di sottoscrizione hello|
|/checkTrafficManagerNameAvailability/action|Controlla la disponibilità di hello del nome DNS di Traffic Manager relativo.|
|/dnszones/read|Ottenere una zona DNS hello, in formato JSON. proprietà Hello della zona includono tag, etag, numero e set. Si noti che questo comando non recupera il set di record hello contenuti all'interno di zona hello.|
|/dnszones/write|Crea o aggiorna una zona DNS in un gruppo di risorse.  Tag di hello tooupdate utilizzato in una risorsa di zona DNS. Si noti che questo comando non può essere utilizzato toocreate o aggiornamento set di record nella zona hello.|
|/dnszones/delete|Eliminare la zona DNS hello, in formato JSON. proprietà Hello della zona includono tag, etag, numero e set.|
|/dnszones/MX/read|Ottiene il set di record hello di tipo 'MX', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/MX/write|Crea o aggiorna un set di record di tipo "MX" all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/MX/delete|Rimuove i set di record di un determinato nome hello e di tipo 'MX' da una zona DNS.|
|/dnszones/NS/read|Ottiene i set di record DNS di tipo NS.|
|/dnszones/NS/write|Crea o aggiorna i set di record DNS di tipo NS.|
|/dnszones/NS/delete|Elimina set di record DNS hello di tipo NS|
|/dnszones/AAAA/read|Ottiene il set di record hello di tipo 'AAAA', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/AAAA/write|Crea o aggiorna un set di record di tipo "AAAA" all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/AAAA/delete|Rimuove i set di record di un determinato nome hello e di tipo 'AAAA' da una zona DNS.|
|/dnszones/CNAME/read|Ottiene il set di record hello di tipo 'CNAME', nel formato JSON. set di record Hello contiene hello TTL, tag ed etag.|
|/dnszones/CNAME/write|Crea o aggiorna un set di record di tipo "CNAME" all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/CNAME/delete|Rimuovere i set di record hello di un nome e tipo 'CNAME' da una zona DNS.|
|/dnszones/SOA/read|Ottiene i set di record DNS di tipo SOA.|
|/dnszones/SOA/write|Crea o aggiorna i set di record DNS di tipo SOA.|
|/dnszones/SRV/read|Ottiene il set di record hello di tipo 'SRV', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/SRV/write|Crea o aggiorna il set di record di tipo SRV.|
|/dnszones/SRV/delete|Rimuove i set di record di un determinato nome hello e di tipo 'SRV' da una zona DNS.|
|/dnszones/PTR/read|Ottiene il set di record hello di tipo 'PTR', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/PTR/write|Crea o aggiorna un set di record di tipo "PTR" all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/PTR/delete|Rimuove i set di record di un determinato nome hello e di tipo 'PTR' da una zona DNS.|
|/dnszones/A/read|Ottiene il set di record hello di tipo 'A', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/A/write|Crea o aggiorna un set di record di tipo "A" all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/A/delete|Rimuove i set di record di un determinato nome hello e di tipo 'A' da una zona DNS.|
|/dnszones/TXT/read|Ottiene il set di record hello di tipo 'TXT', nel formato JSON. set di record Hello contiene un elenco di record, nonché hello TTL, tag ed etag.|
|/dnszones/TXT/write|Crea o aggiorna un set di record di tipo ‘TXT’ all'interno di una zona DNS. record Hello specificati correnti verranno sostituiti hello hello set di record.|
|/dnszones/TXT/delete|Rimuove i set di record di un determinato nome hello e di tipo 'TXT' da una zona DNS.|
|/dnszones/recordsets/read|Ottiene i set di record DNS tra i tipi|
|/networkInterfaces/read|Ottiene una definizione dell’interfaccia di rete. |
|/networkInterfaces/write|Crea un'interfaccia di rete o ne aggiorna una esistente. |
|/networkInterfaces/join/action|Unisce un'interfaccia di rete di macchina virtuale tooa|
|/networkInterfaces/delete|Elimina un'interfaccia di rete|
|/networkInterfaces/effectiveRouteTable/action|Ottenere la tabella di Route configurato nell'interfaccia di rete di hello Vm|
|/networkInterfaces/effectiveNetworkSecurityGroups/action|Ottenere hello nella rete dell'interfaccia di configurati gruppi di sicurezza di rete Vm|
|/networkInterfaces/loadBalancers/read|Ottiene tutti i bilanciamenti del carico di hello che hello interfaccia di rete fa parte di|
|/networkInterfaces/ipconfigurations/read|Ottiene la definizione della configurazione IP dell’interfaccia di rete. |
|/publicIPAddresses/read|Ottiene una definizione dell’indirizzo IP pubblico.|
|/publicIPAddresses/write|Crea un indirizzo IP pubblico o ne aggiorna uno esistente. |
|/publicIPAddresses/delete|Elimina un indirizzo IP pubblico.|
|/publicIPAddresses/join/action|Aggiunge un indirizzo IP pubblico|
|/routeFilters/read|Ottiene una definizione del filtro di instradamento|
|/routeFilters/join/action|Aggiunge un filtro di instradamento|
|/routeFilters/delete|Elimina una definizione del filtro di instradamento|
|/routeFilters/write|Crea un filtro di instradamento o ne aggiorna uno esistente|
|/routeFilters/rules/read|Ottiene una definizione della regola del filtro di instradamento|
|/routeFilters/rules/write|Crea una regola del filtro di instradamento o ne aggiorna una esistente|
|/routeFilters/rules/delete|Elimina una definizione della regola del filtro di instradamento|
|/networkWatchers/read|Ottenere una definizione di controllo rete hello|
|/networkWatchers/write|Crea un Network Watcher o ne aggiorna uno esistente|
|/networkWatchers/delete|Elimina un Network Watcher|
|/networkWatchers/configureFlowLog/action|Configura la registrazione del flusso per una risorsa di destinazione.|
|/networkWatchers/ipFlowVerify/action|Restituisce se i pacchetti hello sono consentito o negato tooor da una determinata destinazione.|
|/networkWatchers/nextHop/action|Per una destinazione specificata e l'indirizzo IP di destinazione, restituire il tipo dell'hop successivo di hello e successivamente sperare che l'indirizzo IP.|
|/networkWatchers/queryFlowLogStatus/action|Ottiene lo stato di hello del flusso di registrazione su una risorsa.|
|/networkWatchers/queryTroubleshootResult/action|Ottiene hello risultato hello in precedenza eseguito o attualmente in esecuzione operazione di risoluzione dei problemi di risoluzione dei problemi.|
|/networkWatchers/securityGroupView/action|Consente di visualizzare hello configurato e regole di gruppo di sicurezza di rete effettiva applicate in una macchina virtuale.|
|/networkWatchers/topology/action|Ottiene una vista a livello di rete delle risorse e le relative relazioni in un gruppo di risorse.|
|/networkWatchers/troubleshoot/action|Avvia la risoluzione dei problemi su una risorsa di rete in Azure.|
|/networkWatchers/packetCaptures/queryStatus/action|Ottiene informazioni sulle proprietà e sullo stato di una risorsa di acquisizione dei pacchetti.|
|/networkWatchers/packetCaptures/stop/action|Arrestare hello che esegue la sessione di acquisizione di pacchetti.|
|/networkWatchers/packetCaptures/read|Prelevare la definizione di acquisizione di pacchetti hello|
|/networkWatchers/packetCaptures/write|Crea un'acquisizione di pacchetti|
|/networkWatchers/packetCaptures/delete|Elimina un'acquisizione di pacchetti|
|/loadBalancers/read|Ottiene una definizione del servizio di bilanciamento del carico|
|/loadBalancers/write|Crea un servizio di bilanciamento del carico o ne aggiorna uno esistente|
|/loadBalancers/delete|Elimina un servizio di bilanciamento del carico|
|/loadBalancers/networkInterfaces/read|Ottiene i riferimenti interfacce di rete tooall hello in un bilanciamento del carico|
|/loadBalancers/loadBalancingRules/read|Ottiene una definizione di regola di bilanciamento del carico per il servizio di bilanciamento del carico|
|/loadBalancers/backendAddressPools/read|Ottiene una definizione del pool di indirizzi di back-end del servizio di bilanciamento del carico|
|/loadBalancers/backendAddressPools/join/action|Aggiunge un pool di indirizzi di back-end del servizio di bilanciamento del carico|
|/loadBalancers/inboundNatPools/read|Ottiene una definizione del pool NAT in entrata del servizio di bilanciamento del carico|
|/loadBalancers/inboundNatPools/join/action|Aggiunge un pool NAT in entrata del servizio di bilanciamento del carico|
|/loadBalancers/inboundNatRules/read|Ottiene una definizione di regola NAT in entrata del servizio di bilanciamento del carico|
|/loadBalancers/inboundNatRules/write|Crea una regola NAT in entrata del servizio di bilanciamento del carico o aggiorna una regola NAT in entrata di bilanciamento del carico esistente|
|/loadBalancers/inboundNatRules/delete|Elimina una regola NAT in entrata del servizio di bilanciamento del carico|
|/loadBalancers/inboundNatRules/join/action|Aggiunge una regola NAT in entrata del servizio di bilanciamento del carico|
|/loadBalancers/outboundNatRules/read|Ottiene una definizione della regola NAT in uscita del servizio di bilanciamento del carico|
|/loadBalancers/probes/read|Ottiene un probe del servizio di bilanciamento del carico|
|/loadBalancers/virtualMachines/read|Ottiene i riferimenti tooall hello le macchine virtuali in un bilanciamento del carico|
|/loadBalancers/frontendIPConfigurations/read|Ottiene una definizione della configurazione IP del front-end del servizio di bilanciamento del carico|
|/trafficManagerGeographicHierarchies/read|Ottiene hello Traffic Manager geografico gerarchia che contiene aree che possono essere utilizzate con metodo di routing del traffico geografica hello|
|/bgpServiceCommunities/read|Ottiene le community del servizio BGP|
|/applicationGatewayAvailableWafRuleSets/read|Ottiene i set di regole WAF disponibili sul gateway applicazione|
|/virtualNetworks/read|Ottenere una definizione di rete virtuale hello|
|/virtualNetworks/write|Crea una rete virtuale o ne aggiorna una esistente|
|/virtualNetworks/delete|Elimina una rete virtuale|
|/virtualNetworks/peer/action|Associa una rete virtuale a un'altra rete virtuale|
|/virtualNetworks/virtualNetworkPeerings/read|Ottiene una definizione di peering della rete virtuale|
|/virtualNetworks/virtualNetworkPeerings/write|Crea un peering della rete virtuale o ne aggiorna uno esistente|
|/virtualNetworks/virtualNetworkPeerings/delete|Elimina un peering della rete virtuale|
|/virtualNetworks/subnets/read|Ottiene una definizione di subnet della rete virtuale|
|/virtualNetworks/subnets/write|Crea una subnet della rete virtuale o ne aggiorna una esistente|
|/virtualNetworks/subnets/delete|Elimina una subnet della rete virtuale|
|/virtualNetworks/subnets/join/action|Aggiunge una rete virtuale|
|/virtualNetworks/subnets/joinViaServiceTunnel/action|Crea un join tra risorse, ad esempio account di archiviazione o SQL database tooa servizio Tunneling abilitato subnet.|
|/virtualNetworks/subnets/virtualMachines/read|Ottiene i riferimenti tooall hello le macchine virtuali in una subnet di rete virtuale|
|/virtualNetworks/checkIpAddressAvailability/read|Controllare se l'indirizzo Ip è disponibile in rete virtuale specificata hello|
|/virtualNetworks/virtualMachines/read|Ottiene i riferimenti tooall hello le macchine virtuali in una rete virtuale|
|/expressRouteServiceProviders/read|Ottiene i provider del servizio Express Route|
|/dnsoperationresults/read|Ottiene i risultati di un'operazione DNS|
|/localnetworkgateways/read|Ottiene il LocalNetworkGateway|
|/localnetworkgateways/write|Crea un LocalNetworkGateway o ne aggiorna uno esistente|
|/localnetworkgateways/delete|Elimina il LocalNetworkGateway|
|/trafficManagerProfiles/read|Ottenere la configurazione del profilo di Traffic Manager hello. Ciò include le impostazioni DNS, impostazioni di routing del traffico, le impostazioni di monitoraggio di endpoint ed elenco hello degli endpoint indirizzato da questo profilo di Traffic Manager.|
|/trafficManagerProfiles/write|Creare un profilo di gestione traffico oppure modificare la configurazione di un profilo di gestione traffico esistente hello. Questo include l’abilitazione o la disabilitazione di un profilo e la modifica delle impostazioni di DNS, di instradamento del traffico o di monitoraggio dell’endpoint. Gli endpoint di cui il profilo di gestione traffico hello possono essere aggiunti, rimossi, abilitati o disabilitati.|
|/trafficManagerProfiles/delete|Eliminare il profilo di gestione traffico hello. Tutte le impostazioni associate hello profilo di gestione traffico andranno perse e profilo di hello non può più essere utilizzato tooroute traffico.|
|/dnsoperationstatuses/read|Ottiene lo stato di un’operazione DNS |
|/operations/read|Ottiene le operazioni disponibili|
|/expressRouteCircuits/read|Ottiene un ExpressRouteCircuit|
|/expressRouteCircuits/write|Crea un ExpressRouteCircuit o ne aggiorna uno esistente|
|/expressRouteCircuits/delete|Elimina un ExpressRouteCircuit|
|/expressRouteCircuits/stats/read|Ottiene uno Stat di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/read|Ottiene il peering di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/write|Crea il peering di ExpressRouteCircuit o ne aggiorna uno esistente|
|/expressRouteCircuits/peerings/delete|Elimina il peering di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/arpTables/action|Ottiene una ArpTable di peering di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/routeTables/action|Ottiene una RouteTable di peering di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/<br>routeTablesSummary/action|Ottiene il riepilogo di una RouteTable di peering di ExpressRouteCircuit|
|/expressRouteCircuits/peerings/stats/read|Ottiene lo Stat di peering di ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/read|Ottiene un’autorizzazione di ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/write|Crea un'autorizzazione di circuito Express Route o ne aggiorna una esistente|
|/expressRouteCircuits/authorizations/delete|Elimina un’autorizzazione di circuito Express Route|
|/connections/read|Ottiene una connessione di gateway di rete virtuale|
|/connections/write|Crea una connessione del gateway di rete virtuale o ne aggiorna una esistente|
|/connections/delete|Elimina una connessione di gateway di rete virtuale|
|/connections/sharedKey/read|Ottiene una connessione di gateway di rete virtuale SharedKey|
|/connections/sharedKey/write|Crea una connessione del gateway di rete virtuale SharedKey o ne aggiorna una esistente|
|/networkSecurityGroups/read|Ottiene una definizione del gruppo di sicurezza di rete|
|/networkSecurityGroups/write|Crea un gruppo di sicurezza di rete o ne aggiorna uno esistente|
|/networkSecurityGroups/delete|Elimina un gruppo di sicurezza di rete|
|/networkSecurityGroups/join/action|Aggiunge un gruppo di sicurezza di rete|
|/networkSecurityGroups/defaultSecurityRules/read|Ottiene una definizione delle regole di sicurezza predefinita|
|/networkSecurityGroups/securityRules/read|Ottiene una definizione delle regole di sicurezza|
|/networkSecurityGroups/securityRules/write|Crea una regola di sicurezza o ne aggiorna una esistente|
|/networkSecurityGroups/securityRules/delete|Elimina una regola di sicurezza|
|/applicationGateways/read|Ottiene un gateway applicazione|
|/applicationGateways/write|Crea un gateway applicazione o ne aggiorna uno esistente|
|/applicationGateways/delete|Elimina un gateway applicazione|
|/applicationGateways/backendhealth/action|Ottiene l'integrità back-end del gateway applicazione|
|/applicationGateways/start/action|Avvia un gateway applicazione|
|/applicationGateways/stop/action|Arresta un gateway applicazione|
|/applicationGateways/backendAddressPools/join/action|Aggiunge un pool di indirizzi back-end del gateway applicazione|
|/routeTables/read|Ottiene una definizione della tabella di route|
|/routeTables/write|Crea una tabella di route o ne aggiorna una esistente|
|/routeTables/delete|Elimina una definizione della tabella di route|
|/routeTables/join/action|Aggiunge una tabella di route|
|/routeTables/routes/read|Ottiene una definizione di route|
|/routeTables/routes/write|Crea una route o ne aggiorna una esistente|
|/routeTables/routes/delete|Elimina una definizione di route|
|/locations/operationResults/read|Ottiene il risultato di un'operazione POST o DELETE asincrona|
|/locations/checkDnsNameAvailability/read|Controlla se l'etichetta dns è disponibile all'indirizzo hello percorso specificato|
|/locations/usages/read|Ottiene la metrica di utilizzo risorse hello|
|/locations/operations/read|Ottiene una risorsa per l'operazione che rappresenta lo stato di un'operazione asincrona|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse hub di notifica hello e consente la creazione di hello di spazi dei nomi e hub di notifica|
|/CheckNamespaceAvailability/action|Controlla se un determinato nome di risorsa Namespace è disponibile all'interno di hello servizio hub di notifica.|
|/Namespaces/write|Crea una risorsa spazio dei nomi e ne aggiorna le proprietà. Tag e lo stato di hello Namespace sono proprietà hello che può essere aggiornata.|
|/Namespaces/read|Ottenere l'elenco di hello della descrizione della risorsa Namespace|
|/Namespaces/Delete|Elimina la risorsa spazio dei nomi|
|/Namespaces/authorizationRules/action|Ottenere l'elenco di hello della descrizione delle regole di autorizzazione di spazi dei nomi.|
|/Namespaces/CheckNotificationHubAvailability/action|Controlla se un determinato nome di hub di notifica è disponibile all'interno di uno spazio dei nomi.|
|/Namespaces/authorizationRules/write|Crea regole di autorizzazione a livello dello spazio dei nomi e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/Namespaces/authorizationRules/read|Ottenere l'elenco di hello della descrizione delle regole di autorizzazione di spazi dei nomi.|
|/Namespaces/authorizationRules/delete|Elimina regola di autorizzazione dello spazio dei nomi. Impossibile eliminare Hello regola di autorizzazione Namespace predefinita. |
|/Namespaces/authorizationRules/listkeys/action|Ottenere una stringa di connessione di hello toohello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/action|Namespace autorizzazione regola Rigenera primaria/chiave secondaria, specificare hello chiave è toobe rigenerata|
|/Namespaces/NotificationHubs/write|Crea un hub di notifica e ne aggiorna le proprietà. Le proprietà includono principalmente credenziali PNS, regole di autorizzazione e TTL|
|/Namespaces/NotificationHubs/read|Ottiene l’elenco di descrizioni dell’hub di notifica|
|/Namespaces/NotificationHubs/Delete|Elimina la risorsa nell’hub di notifica|
|/Namespaces/NotificationHubs/authorizationRules/action|Ottenere l'elenco di hello delle regole di autorizzazione Hub di notifica|
|/Namespaces/NotificationHubs/pnsCredentials/action|Ottiene tutte le credenziali PNS dell’hub di notifica. Queste includono le credenziali WNS, MPNS, APNS, GCM e Baidu|
|/Namespaces/NotificationHubs/debugSend/action|Invia una notifica push di prova.|
|/Namespaces/NotificationHubs/metricDefinitions/read|Ottiene l'elenco di descrizioni delle risorse di metrica dello spazio dei nomi|
|/Namespaces/NotificationHubs/<br>authorizationRules/write|Crea regole di autorizzazione dell'inoltro dell’hub di notifica e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/Namespaces/NotificationHubs/<br>authorizationRules/read|Ottenere l'elenco di hello delle regole di autorizzazione Hub di notifica|
|/Namespaces/NotificationHubs/<br>authorizationRules/delete|Elimina le regole di autorizzazione dell’hub di notifica|
|/Namespaces/NotificationHubs/<br>authorizationRules/listkeys/action|Ottenere hello toohello di stringa di connessione Hub di notifica|
|/Namespaces/NotificationHubs/<br>authorizationRules/regenerateKeys/action|Notifica Hub autorizzazione regola Rigenera primaria/chiave secondaria, specificare hello chiave è toobe rigenerata|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare un provider di risorse tooa di sottoscrizione.|
|/linkTargets/read|Elenca gli account esistenti non associati a una sottoscrizione di Azure. toolink questa area di lavoro tooa sottoscrizione di Azure, utilizzare un id cliente restituito da questa operazione nella proprietà id cliente di hello di hello operazione Crea area di lavoro.|
|/workspaces/write|Crea una nuova area di lavoro o i collegamenti tooan esistente fornendo l'id cliente hello dall'area di lavoro esistente hello.|
|/workspaces/read|Ottiene un'area di lavoro esistente|
|/workspaces/delete|Elimina un'area di lavoro. Se è stato collegato l'area di lavoro hello tooan area di lavoro esistente al momento della creazione quindi hello dell'area di lavoro è stato collegato toois non è stato eliminato.|
|/workspaces/generateregistrationcertificate/action|Genera l'errore di registrazione certificati per l'area di lavoro hello. Questo certificato è l'area di lavoro toohello tooconnect usato Microsoft System Center Operation Manager.|
|/workspaces/sharedKeys/action|Recupera le chiavi di hello condiviso per l'area di lavoro hello. Queste chiavi sono utilizzati tooconnect informazioni operative di Microsoft agenti toohello area.|
|/workspaces/search/action|Esegue una query di ricerca|
|/workspaces/datasources/read|Ottiene le origini dati in un'area di lavoro.|
|/workspaces/datasources/write|Crea/Aggiorna le origini dati in un'area di lavoro.|
|/workspaces/datasources/delete|Elimina le origini dati in un'area di lavoro.|
|/workspaces/managementGroups/read|Ottiene i nomi di hello e metadati per l'area di lavoro di System Center Operations Manager Gestione gruppi toothis connesso.|
|/workspaces/schema/read|Ottiene dello schema di ricerca hello per area di lavoro hello.  Schema di ricerca include campi hello esposto e i relativi tipi.|
|/workspaces/usages/read|Ottiene i dati di utilizzo per un'area di lavoro tra cui hello quantità dei dati letti dall'area di lavoro hello.|
|/workspaces/intelligencepacks/read|Elenca tutti intelligence Pack che sono visibili per una determinata area di lavoro e vengono elencati anche se pack hello è abilitato o disabilitato per l'area di lavoro.|
|/workspaces/intelligencepacks/enable/action|Abilita un Intelligence Pack per una specifica area di lavoro.|
|/workspaces/intelligencepacks/disable/action|Disabilita un Intelligence Pack per una specifica area di lavoro.|
|/workspaces/sharedKeys/read|Recupera le chiavi di hello condiviso per l'area di lavoro hello. Queste chiavi sono utilizzati tooconnect informazioni operative di Microsoft agenti toohello area.|
|/workspaces/savedSearches/read|Ottiene una query di ricerca salvata|
|/workspaces/savedSearches/write|Crea una query di ricerca salvata|
|/workspaces/savedSearches/delete|Elimina una query di ricerca salvata|
|/workspaces/storageinsightconfigs/write|Crea una nuova configurazione di archiviazione. Queste configurazioni sono dati toopull utilizzato da un percorso di un account di archiviazione esistente.|
|/workspaces/storageinsightconfigs/read|Ottiene una configurazione di archiviazione.|
|/workspaces/storageinsightconfigs/delete|Elimina una configurazione di archiviazione. Informazioni operative di Microsoft di leggere i dati dall'account di archiviazione hello verrà interrotta.|
|/workspaces/configurationScopes/read|Ottiene l'ambito di configurazione|
|/workspaces/configurationScopes/write|Imposta l'ambito di configurazione|
|/workspaces/configurationScopes/delete|Elimina l'ambito di configurazione|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Operazione | Descrizione |
|---|---|
|/register/action|Registrare un provider di risorse tooa di sottoscrizione.|
|/solutions/write|Crea una nuova soluzione OMS|
|/solutions/read|Ottiene soluzione OMS esistente|
|/solutions/delete|Elimina soluzione OMS esistente|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Operazione | Descrizione |
|---|---|
|/Vaults/backupJobsExport/action|Esporta processi|
|/Vaults/write|L'operazione Crea insieme di credenziali crea una risorsa di Azure di tipo 'vault'|
|/Vaults/read|Hello operazione Ottieni insieme di credenziali Ottiene un oggetto che rappresenta le risorse di Azure di tipo 'vault' hello|
|/Vaults/delete|Hello Elimina insieme di credenziali operazione eliminazioni hello specificato risorsa di Azure di tipo 'vault'|
|/Vaults/refreshContainers/read|Aggiorna l'elenco di contenitori hello|
|/Vaults/backupJobsExport/operationResults/read|Hello restituisce risultati dell'operazione del processo esportare.|
|/Vaults/backupOperationResults/read|Restituisce il risultato dell'operazione di backup di un insieme di credenziali di Servizi di ripristino.|
|/Vaults/monitoringAlerts/read|Ottiene gli avvisi di hello per l'insieme di credenziali di hello Recovery services.|
|/Vaults/monitoringAlerts/{uniqueAlertId}/read|Ottiene i dettagli di hello di avviso hello.|
|/Vaults/backupSecurityPIN/read|Restituisce le informazioni sul PIN di sicurezza dell'insieme di credenziali di Servizi di ripristino.|
|/vaults/replicationEvents/read|Legge tutti gli eventi|
|/Vaults/backupProtectableItems/read|Restituisce l'elenco di tutti gli elementi da proteggere.|
|/vaults/replicationFabrics/read|Legge tutte le infrastrutture|
|/vaults/replicationFabrics/write|Crea o aggiorna tutte le infrastrutture|
|/vaults/replicationFabrics/remove/action|Rimuove l'infrastruttura|
|/vaults/replicationFabrics/checkConsistency/action|Controlli di coerenza di hello dell'infrastruttura|
|/vaults/replicationFabrics/delete|Elimina tutte le infrastrutture|
|/vaults/replicationFabrics/renewcertificate/action||
|/vaults/replicationFabrics/deployProcessServerImage/action|Distribuisce immagine del server di elaborazione|
|/vaults/replicationFabrics/reassociateGateway/action|Riassocia gateway|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>read|Legge tutti i provider dei servizi di ripristino|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>remove/action|Rimuove tutti i provider dei servizi di ripristino|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>delete|Elimina tutti i provider dei servizi di ripristino|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>refreshProvider/action|Aggiorna i provider|
|/vaults/replicationFabrics/replicationStorageClassifications/read|Legge tutte le classificazioni di archiviazione|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/read|Legge tutti i mapping di classificazioni di archiviazione|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/write|Crea o aggiorna tutti i mapping di classificazioni di archiviazione|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/delete|Elimina tutti i mapping di classificazioni di archiviazione|
|/vaults/replicationFabrics/replicationvCenters/read|Legge tutti i processi|
|/vaults/replicationFabrics/replicationvCenters/write|Crea o aggiorna tutti i processi|
|/vaults/replicationFabrics/replicationvCenters/delete|Elimina tutti i processi|
|/vaults/replicationFabrics/replicationNetworks/read|Legge tutte le reti|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/read|Legge tutti i mapping di rete|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/write|Crea o aggiorna tutti i mapping di rete|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/delete|Elimina tutti i mapping di rete|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>read|Legge tutti i contenitori di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>discoverProtectableItem/action|Individua elemento da proteggere|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>write|Crea o aggiorna i contenitori di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>remove/action|Rimuove il contenitore di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>switchprotection/action|Cambia il contenitore di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectableItems/read|Legge gli elementi da proteggere|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/read|Legge i mapping dei contenitori di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/write|Crea o aggiorna i mapping dei contenitori di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/remove/action|Rimuove il mapping di contenitore di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/delete|Elimina i mapping dei contenitori di protezione|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/read|Legge tutti gli elementi protetti|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/write|Crea o aggiorna gli elementi protetti|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/delete|Elimina tutti gli elementi protetti|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/remove/action|Rimuove l'elemento protetto|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/plannedFailover/action|Failover pianificato|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/unplannedFailover/action|Failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailover/action|Failover di test|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailoverCleanup/action|Pulizia del failover di test|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/failoverCommit/action|Commit del failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/reProtect/action|Riprotegge l'elemento protetto|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/updateMobilityService/action|Aggiorna servizio Mobility|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/repairReplication/action|Ripristina replica|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/applyRecoveryPoint/action|Applica punto di ripristino|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/recoveryPoints/read|Legge i punti di ripristino di replica|
|/vaults/replicationPolicies/read|Legge tutti i criteri|
|/vaults/replicationPolicies/write|Crea o aggiorna i criteri|
|/vaults/replicationPolicies/delete|Elimina i criteri|
|/vaults/replicationRecoveryPlans/read|Legge i piani di ripristino|
|/vaults/replicationRecoveryPlans/write|Crea o aggiorna i piani di ripristino|
|/vaults/replicationRecoveryPlans/delete|Elimina i piani di ripristino|
|/vaults/replicationRecoveryPlans/plannedFailover/action|Piano di ripristino del failover pianificato|
|/vaults/replicationRecoveryPlans/unplannedFailover/action|Piano di ripristino del failover|
|/vaults/replicationRecoveryPlans/testFailover/action|Piano di ripristino del failover di test|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/action|Piano di ripristino della pulizia del failover di test|
|/vaults/replicationRecoveryPlans/failoverCommit/action|Piano di ripristino del commit del failover|
|/vaults/replicationRecoveryPlans/reProtect/action|Piano di ripristino di riprotezione|
|/Vaults/extendedInformation/read|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/Vaults/extendedInformation/write|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/Vaults/extendedInformation/delete|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/Vaults/backupManagementMetaData/read|Restituisce i metadati di gestione di backup di un insieme di credenziali di Servizi di ripristino.|
|/Vaults/backupProtectionContainers/read|Restituisce tutti i contenitori appartenenti toohello sottoscrizione|
|/Vaults/backupFabrics/operationResults/read|Restituisce lo stato dell'operazione hello|
|/Vaults/backupFabrics/protectionContainers/read|Restituisce tutti i contenitori registrati|
|/Vaults/backupFabrics/protectionContainers/<br>operationResults/read|Ottiene il risultato dell'operazione eseguita sul contenitore di protezione.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/read|Restituisce i dettagli dell'elemento protetto hello di oggetto|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/write|Crea un elemento protetto di backup|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/delete|Elimina l'elemento protetto|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/backup/action|Esegue il backup dell'elemento protetto.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationResults/read|Ottiene il risultato dell'operazione eseguita sugli elementi protetti.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationStatus/read|Restituisce lo stato di hello di operazione eseguita su elementi protetti.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/read|Ottiene i punti di ripristino degli elementi protetti.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>restore/action|Ripristina i punti di ripristino degli elementi protetti.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>provisionInstantItemRecovery/action|Effettua il provisioning del ripristino elementi immediato per l'elemento protetto|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>revokeInstantItemRecovery/action|Revoca il ripristino elementi immediato per l'elemento protetto|
|/Vaults/usages/read|Restituisce i dettagli di utilizzo di un insieme di credenziali di Servizi di ripristino.|
|/vaults/usages/read|Legge tutti gli utilizzi dell'insieme di credenziali|
|/Vaults/certificates/write|operazione di certificato risorsa Aggiorna Hello Aggiorna certificato della credenziale dell'insieme di credenziali/risorsa hello.|
|/Vaults/tokenInfo/read|Restituisce le informazioni sul token dell'insieme di credenziali di Servizi di ripristino.|
|/vaults/replicationAlertSettings/read|Legge tutte le impostazioni degli avvisi|
|/vaults/replicationAlertSettings/write|Crea o aggiorna le impostazioni degli avvisi|
|/Vaults/backupOperations/read|Restituisce lo stato dell'operazione di backup dell'insieme di credenziali di Servizi di ripristino.|
|/Vaults/storageConfig/read|Restituisce la configurazione di archiviazione dell'insieme di credenziali di Servizi di ripristino.|
|/Vaults/storageConfig/write|Aggiorna la configurazione di archiviazione dell'insieme di credenziali di Servizi di ripristino.|
|/Vaults/backupUsageSummaries/read|Restituisce i riepiloghi per gli elementi protetti e i server protetti di un'istanza di Servizi di ripristino.|
|/Vaults/backupProtectedItems/read|Restituisce hello elenco di tutti gli elementi protetti.|
|/Vaults/backupconfig/vaultconfig/read|Restituisce la configurazione dell'insieme di credenziali di Servizi di ripristino.|
|/Vaults/backupconfig/vaultconfig/write|Aggiorna la configurazione dell'insieme di credenziali di Servizi di ripristino.|
|/Vaults/registeredIdentities/write|Hello operazione registra contenitore di servizi può essere utilizzato tooregister un contenitore con il servizio di ripristino.|
|/Vaults/registeredIdentities/read|Hello Ottieni contenitori può essere utilizzata l'operazione get contenitori hello registrati per una risorsa.|
|/Vaults/registeredIdentities/delete|Hello operazione Annulla registrazione contenitore può essere utilizzato toounregister un contenitore.|
|/Vaults/registeredIdentities/operationResults/read|invio di Hello operazione ottieni risultati dell'operazione può essere usata per ottenere hello dello stato dell'operazione e generano in modo asincrono per hello operazione|
|/vaults/replicationJobs/read|Legge tutti i processi|
|/vaults/replicationJobs/cancel/action|Annulla processo|
|/vaults/replicationJobs/restart/action|Riavvia processo|
|/vaults/replicationJobs/resume/action|Riprende il processo|
|/Vaults/backupPolicies/read|Restituisce tutti i criteri di protezione|
|/Vaults/backupPolicies/write|Crea i criteri di protezione|
|/Vaults/backupPolicies/delete|Elimina i criteri di protezione|
|/Vaults/backupPolicies/operationResults/read|Ottiene i risultati dell'operazione sui criteri.|
|/Vaults/backupPolicies/operationStatus/read|Ottiene lo stato dell'operazione sui criteri.|
|/Vaults/vaultTokens/read|Hello operazione Token dell'insieme di credenziali può essere utilizzato tooget Token dell'insieme di credenziali per le operazioni di back-end di livello di insieme di credenziali.|
|/Vaults/monitoringConfigurations/notificationConfiguration/read|Ottiene la configurazione notifica hello Recovery services insieme di credenziali.|
|/Vaults/backupJobs/read|Restituisce tutti gli oggetti processo|
|/Vaults/backupJobs/cancel/action|Hello Annulla processo|
|/Vaults/backupJobs/operationResults/read|Hello restituisce risultati dell'operazione del processo.|
|/locations/allocateStamp/action|AllocateStamp è un'operazione interna usata dal servizio|
|/locations/allocatedStamp/read|GetAllocatedStamp è un'operazione interna usata dal servizio|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Operazione | Descrizione |
|---|---|
|/checkNamespaceAvailability/action|Verifica la disponibilità dello spazio dei nomi nella sottoscrizione specificata.|
|/register/action|Registra sottoscrizione hello per provider di risorse di inoltro hello e consente la creazione di hello delle risorse di inoltro|
|/namespaces/write|Crea una risorsa spazio dei nomi e ne aggiorna le proprietà. Tag e lo stato di hello Namespace sono proprietà hello che può essere aggiornata.|
|/namespaces/read|Ottenere l'elenco di hello della descrizione della risorsa Namespace|
|/namespaces/Delete|Elimina la risorsa spazio dei nomi|
|/namespaces/authorizationRules/write|Crea regole di autorizzazione a livello dello spazio dei nomi e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/authorizationRules/delete|Elimina regola di autorizzazione dello spazio dei nomi. Impossibile eliminare Hello regola di autorizzazione Namespace predefinita. |
|/namespaces/authorizationRules/listkeys/action|Ottenere una stringa di connessione di hello toohello Namespace|
|/namespaces/HybridConnections/write|Crea o aggiorna proprietà della connessione ibrida.|
|/namespaces/HybridConnections/read|Ottiene l'elenco delle descrizioni delle risorse della connessione ibrida|
|/namespaces/HybridConnections/Delete|Operazione toodelete HybridConnection risorse|
|/namespaces/HybridConnections/authorizationRules/write|Crea regole di autorizzazione della connessione ibrida e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/HybridConnections/authorizationRules/delete|Operazione toodelete HybridConnection le regole di autorizzazione|
|/namespaces/HybridConnections/authorizationRules/listkeys/action|Ottenere hello tooHybridConnection di stringa di connessione|
|/namespaces/WcfRelays/write|Crea o aggiorna proprietà inoltro WCF.|
|/namespaces/WcfRelays/read|Ottiene l'elenco delle descrizioni delle risorse dell'inoltro WCF|
|/namespaces/WcfRelays/Delete|Operazione toodelete WcfRelay risorse|
|/namespaces/WcfRelays/authorizationRules/write|Crea regole di autorizzazione dell'inoltro WCF e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/WcfRelays/authorizationRules/delete|Operazione toodelete WcfRelay le regole di autorizzazione|
|/namespaces/WcfRelays/authorizationRules/listkeys/action|Ottenere hello tooWcfRelay di stringa di connessione|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Operazione | Descrizione |
|---|---|
|/AvailabilityStatuses/read|Ottiene gli stati di disponibilità hello per tutte le risorse in hello specificato ambito|
|/AvailabilityStatuses/current/read|Ottiene lo stato di disponibilità hello per hello risorsa specificata.|

## <a name="microsoftresources"></a>Microsoft.Resources

| Operazione | Descrizione |
|---|---|
|/checkResourceName/action|Controllare il nome di risorsa hello la validità.|
|/providers/read|Ottenere l'elenco di hello di provider.|
|/subscriptions/read|Ottiene l'elenco di sottoscrizioni hello.|
|/subscriptions/operationresults/read|Ottenere i risultati delle operazioni di sottoscrizione hello.|
|/subscriptions/providers/read|Ottiene o elenca i provider di risorse.|
|/subscriptions/tagNames/read|Ottiene o elenca le categorie della sottoscrizione.|
|/subscriptions/tagNames/write|Aggiunge una categoria della sottoscrizione.|
|/subscriptions/tagNames/delete|Elimina una categoria della sottoscrizione.|
|/subscriptions/tagNames/tagValues/read|Ottiene o elenca i valori delle categorie della sottoscrizione.|
|/subscriptions/tagNames/tagValues/write|Aggiunge un valore di categoria della sottoscrizione.|
|/subscriptions/tagNames/tagValues/delete|Elimina un valore di categoria della sottoscrizione.|
|/subscriptions/resources/read|Ottiene le risorse di una sottoscrizione.|
|/subscriptions/resourceGroups/read|Ottiene o elenca i gruppi di risorse.|
|/subscriptions/resourceGroups/write|Crea o aggiorna un gruppo di risorse.|
|/subscriptions/resourceGroups/delete|Elimina un gruppo di risorse e tutte le risorse in esso contenute.|
|/subscriptions/resourceGroups/moveResources/action|Sposta le risorse da una risorsa gruppo tooanother.|
|/subscriptions/resourceGroups/validateMoveResources/action|Convalida lo spostamento di risorse da una risorsa gruppo tooanother.|
|/subscriptions/resourcegroups/resources/read|Ottiene le risorse di hello per il gruppo di risorse hello.|
|/subscriptions/resourcegroups/deployments/read|Ottiene o elenca le distribuzioni.|
|/subscriptions/resourcegroups/deployments/write|Crea o aggiorna una distribuzione.|
|/subscriptions/resourcegroups/deployments/operationstatuses/read|Ottiene o elenca gli stati dell'operazione di distribuzione.|
|/subscriptions/resourcegroups/deployments/operations/read|Ottiene o elenca le operazioni di distribuzione.|
|/subscriptions/locations/read|Ottiene l'elenco di hello delle località supportate.|
|/links/read|Ottiene o elenca i collegamenti a una risorsa.|
|/links/write|Crea o aggiorna un collegamento a una risorsa.|
|/links/delete|Elimina un collegamento a una risorsa.|
|/tenants/read|Ottiene l'elenco di hello di tenant.|
|/resources/read|Ottenere l'elenco di hello delle risorse in base a filtri.|
|/deployments/read|Ottiene o elenca le distribuzioni.|
|/deployments/write|Crea o aggiorna una distribuzione.|
|/deployments/delete|Elimina una distribuzione.|
|/deployments/cancel/action|Annulla una distribuzione.|
|/deployments/validate/action|Convalida una distribuzione.|
|/deployments/operations/read|Ottiene o elenca le operazioni di distribuzione.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Operazione | Descrizione |
|---|---|
|/jobcollections/read|Ottiene la raccolta processi|
|/jobcollections/write|Crea o aggiorna la raccolta processi.|
|/jobcollections/delete|Elimina la raccolta processi.|
|/jobcollections/enable/action|Abilita la raccolta processi.|
|/jobcollections/disable/action|Disabilita la raccolta processi.|
|/jobcollections/jobs/read|Ottiene il processo.|
|/jobcollections/jobs/write|Crea o aggiorna il processo.|
|/jobcollections/jobs/delete|Elimina il processo.|
|/jobcollections/jobs/run/action|Esegue il processo.|
|/jobcollections/jobs/generateLogicAppDefinition/action|Genera la definizione dell'app per la logica in base a un processo dell'Utilità di pianificazione.|
|/jobcollections/jobs/jobhistories/read|Ottiene la cronologia processi.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse ricerca hello e consente la creazione di hello di servizi di ricerca.|
|/checkNameAvailability/action|Controlla la disponibilità del nome del servizio hello.|
|/searchServices/write|Crea o aggiorna il servizio di ricerca di hello.|
|/searchServices/read|Legge il servizio di ricerca di hello.|
|/searchServices/delete|Elimina il servizio di ricerca di hello.|
|/searchServices/start/action|Avvia il servizio di ricerca hello.|
|/searchServices/stop/action|Arresta il servizio di ricerca hello.|
|/searchServices/listAdminKeys/action|Legge le chiavi amministratore hello.|
|/searchServices/regenerateAdminKey/action|Rigenera chiave di amministrazione di hello.|
|/searchServices/createQueryKey/action|Crea una chiave di query hello.|
|/searchServices/queryKey/read|Legge le chiavi di query hello.|
|/searchServices/queryKey/delete|Elimina la chiave di query hello.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Operazione | Descrizione |
|---|---|
|/jitNetworkAccessPolicies/read|Ottiene i criteri di accesso di rete-in-time hello|
|/jitNetworkAccessPolicies/write|Crea un nuovo criterio di accesso alla rete JIT o ne aggiorna uno esistente|
|/jitNetworkAccessPolicies/initiate/action|Avvia un criterio di accesso alla rete JIT|
|/securitySolutionsReferenceData/read|Ottiene i dati di riferimento di soluzioni per la sicurezza hello|
|/securityStatuses/read|Ottiene gli stati di integrità di protezione hello per le risorse di Azure|
|/webApplicationFirewalls/read|Ottiene i firewall applicazione web di hello|
|/webApplicationFirewalls/write|Crea un nuovo firewall dell'applicazione Web o ne aggiorna uno esistente|
|/webApplicationFirewalls/delete|Elimina un firewall dell'applicazione Web|
|/securitySolutions/read|Ottiene le soluzioni di sicurezza hello|
|/securitySolutions/write|Crea una nuova soluzione di sicurezza o ne aggiorna una esistente|
|/securitySolutions/delete|Elimina una soluzione di sicurezza|
|/tasks/read|Ottiene tutti i consigli per la sicurezza disponibili|
|/tasks/dismiss/action|Ignora un consiglio per la sicurezza|
|/tasks/activate/action|Attiva un consiglio per la sicurezza|
|/policies/read|Ottiene i criteri di sicurezza hello|
|/policies/write|Gli aggiornamenti hello criteri di sicurezza|
|/applicationWhitelistings/read|Ottiene whitelistings applicazione hello|
|/applicationWhitelistings/write|Crea un nuovo elenco elementi consentiti per l'applicazione o ne aggiorna uno esistente|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Operazione | Descrizione |
|---|---|
|/subscriptions/write|Crea o aggiorna una sottoscrizione|
|/gateways/write|Crea o aggiorna un gateway|
|/gateways/delete|Elimina un gateway|
|/gateways/read|Ottiene un gateway|
|/gateways/regenerateprofile/action|Rigenera profilo gateway hello|
|/gateways/upgradetolatest/action|Versione più recente di aggiornamenti hello gateway toohello|
|/nodes/write|Crea o aggiorna un nodo|
|/nodes/delete|Elimina un nodo|
|/nodes/read|Ottiene un nodo|
|/sessions/write|Crea o aggiorna una sessione|
|/sessions/read|Ottiene una sessione|
|/sessions/delete|Elimina una sessione|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Operazione | Descrizione |
|---|---|
|/checkNameAvailability/action|Verifica la disponibilità dello spazio dei nomi nella sottoscrizione specificata.|
|/register/action|Registra sottoscrizione hello per provider di risorse bus di servizio hello e consente la creazione di hello di risorse bus di servizio|
|/namespaces/write|Crea una risorsa spazio dei nomi e ne aggiorna le proprietà. Tag e lo stato di hello Namespace sono proprietà hello che può essere aggiornata.|
|/namespaces/read|Ottenere l'elenco di hello della descrizione della risorsa Namespace|
|/namespaces/Delete|Elimina una risorsa spazio dei nomi|
|/namespaces/metricDefinitions/read|Ottiene l'elenco di descrizioni delle risorse metrica dello spazio dei nomi|
|/namespaces/authorizationRules/write|Crea regole di autorizzazione a livello dello spazio dei nomi e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/authorizationRules/read|Ottenere l'elenco di hello della descrizione delle regole di autorizzazione di spazi dei nomi.|
|/namespaces/authorizationRules/delete|Elimina regola di autorizzazione dello spazio dei nomi. Impossibile eliminare Hello regola di autorizzazione Namespace predefinita. |
|/namespaces/authorizationRules/listkeys/action|Ottenere una stringa di connessione di hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Rigenerare hello primario o secondario chiave toohello risorse|
|/namespaces/diagnosticSettings/read|Ottiene l'elenco di descrizioni delle risorse impostazioni di diagnostica dello spazio dei nomi|
|/namespaces/diagnosticSettings/write|Ottiene l'elenco di descrizioni delle risorse impostazioni di diagnostica dello spazio dei nomi|
|/namespaces/queues/write|Crea o aggiorna proprietà di coda.|
|/namespaces/queues/read|Ottiene l'elenco delle descrizioni delle risorse coda|
|/namespaces/queues/Delete|Operazione toodelete risorsa coda|
|/namespaces/queues/authorizationRules/write|Crea regole di autorizzazione delle code e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/queues/authorizationRules/read| Ottenere l'elenco di hello coda delle regole di autorizzazione|
|/namespaces/queues/authorizationRules/delete|Operazione toodelete le regole di autorizzazione della coda|
|/namespaces/queues/authorizationRules/listkeys/action|Ottenere hello tooQueue di stringa di connessione|
|/namespaces/queues/authorizationRules/regenerateKeys/action|Rigenerare hello primario o secondario chiave toohello risorse|
|/namespaces/logDefinitions/read|Ottiene l'elenco di descrizioni delle risorse log dello spazio dei nomi|
|/namespaces/topics/write|Crea o aggiorna le proprietà degli argomenti.|
|/namespaces/topics/read|Ottiene l'elenco delle descrizioni delle risorse argomento|
|/namespaces/topics/Delete|Operazione toodelete argomento risorsa|
|/namespaces/topics/authorizationRules/write|Crea regole di autorizzazione dell’argomento e ne aggiorna le proprietà. Diritti di accesso di regole di autorizzazione Hello, hello primario e secondario chiavi possono essere aggiornate.|
|/namespaces/topics/authorizationRules/read| Ottenere l'elenco di hello argomento delle regole di autorizzazione|
|/namespaces/topics/authorizationRules/delete|Operazione toodelete le regole di autorizzazione di argomento|
|/namespaces/topics/authorizationRules/listkeys/action|Ottenere hello tooTopic di stringa di connessione|
|/namespaces/topics/authorizationRules/regenerateKeys/action|Rigenerare hello primario o secondario chiave toohello risorse|
|/namespaces/topics/subscriptions/write|Crea o aggiorna le proprietà TopicSubscription.|
|/namespaces/topics/subscriptions/read|Ottiene l'elenco delle descrizioni delle risorse TopicSubscription|
|/namespaces/topics/subscriptions/Delete|Operazione toodelete TopicSubscription risorse|
|/namespaces/topics/subscriptions/rules/write|Crea o aggiorna le proprietà di una regola.|
|/namespaces/topics/subscriptions/rules/read|Ottiene l'elenco delle descrizioni delle risorse di una regola|
|/namespaces/topics/subscriptions/rules/Delete|Operazione toodelete risorsa regola|

## <a name="microsoftsql"></a>Microsoft.Sql

| Operazione | Descrizione |
|---|---|
|/servers/read|Restituisce un elenco di server in un gruppo di risorse per una sottoscrizione|
|/servers/write|Crea un nuovo server o modifica le proprietà di un server esistente in un gruppo di risorse per una sottoscrizione|
|/servers/delete|Elimina un server e tutti i database e i pool elastici contenuti|
|/servers/import/action|Creare un nuovo database nel server di hello e distribuire lo schema e dati da un pacchetto con estensione DacPac|
|/servers/upgrade/action|Abilitare nuove funzionalità disponibili nella versione più recente di hello del server e specificare una mappa di conversione di database edition|
|/servers/VulnerabilityAssessmentScans/action|Esegue la scansione del server per la valutazione della vulnerabilità|
|/servers/operationResults/read|Viene utilizzata l'operazione tootrack lo stato di avanzamento dell'aggiornamento del server da toohigher versione inferiore|
|/servers/operationResults/delete|Interrompe l’aggiornamento di versione del server in corso|
|/servers/securityAlertPolicies/read|Recuperare i dettagli di criteri di rilevamento delle minacce di hello server configurato in un determinato server|
|/servers/securityAlertPolicies/write|Modifica di rilevamento minacce hello server per un determinato server|
|/servers/securityAlertPolicies/operationResults/read|Recuperare i risultati di server hello operazione di impostazione dei criteri di rilevamento minacce|
|/servers/administrators/read|Recupera i dettagli dell’amministratore del server|
|/servers/administrators/write|Crea o aggiorna l’amministratore del server|
|/servers/administrators/delete|Eliminare l'amministratore del server da server hello|
|/servers/recoverableDatabases/read|Questa operazione viene utilizzata per il ripristino di emergenza del database attivo toorestore database noti toolast buon punto di backup. Restituisce informazioni sul backup precedente hello ma in realtà non ripristina i database di hello.|
|/servers/serviceObjectives/read|Recupera l'elenco degli obiettivi del livello di servizio (anche noti come livelli di prestazioni) disponibili in un determinato server|
|/servers/firewallRules/read|Recupera i dettagli della regola del firewall del server|
|/servers/firewallRules/write|Crea o Aggiorna regola firewall del server che controlla l'intervallo di indirizzi IP consentito tooconnect toohello server|
|/servers/firewallRules/delete|Eliminare una regola del firewall dal server hello|
|/servers/administratorOperationResults/read|Recupera i risultati dell’operazione dell’amministratore del server|
|/servers/recommendedElasticPools/read|Recuperare l'indicazione di database elastico pool tooreduce costo o migliorare le prestazioni in base all'utilizzo delle risorse historica|
|/servers/recommendedElasticPools/metrics/read|Recupera le metriche per i pool di database elastici consigliati per un determinato server|
|/servers/recommendedElasticPools/databases/read|Recupera i database da aggiungere nei pool di database elastici consigliati per un determinato server|
|/servers/elasticPools/read|Recupera i dettagli per il pool di database elastico per un determinato server|
|/servers/elasticPools/write|Crea nuove proprietà o elimina quelle esistenti di un pool di database elastico|
|/servers/elasticPools/delete|Elimina un pool di database elastico esistente|
|/servers/elasticPools/operationResults/read|Recupera i dettagli su un’operazione di un pool di database elastico specifico|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/read|Restituisce i tipi di metriche disponibili per i pool di database elastici|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/read|Ottiene l'impostazione di diagnostica hello per risorse hello|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crea o aggiorna l'impostazione di diagnostica di hello per risorsa hello|
|/servers/elasticPools/metrics/read|Restituisce la metrica di utilizzo delle risorse di un pool di database elastico|
|/servers/elasticPools/elasticPoolDatabaseActivity/read|Recupera attività e dettagli su uno specifico database che fa parte del pool di database elastico|
|/servers/elasticPools/advisors/read|Restituisce l'elenco di Advisor è disponibile per il pool elastico hello|
|/servers/elasticPools/advisors/write|Aggiorna lo stato di esecuzione automatica di un advisor a livello di pool elastico.|
|/servers/elasticPools/advisors/recommendedActions/read|Restituisce l'elenco di azioni consigliate di preparazione specificato per il pool elastico hello|
|/servers/elasticPools/advisors/recommendedActions/write|Applicare l'azione nel pool elastico hello consigliata hello|
|/servers/elasticPools/elasticPoolActivity/read|Recupera attività e dettagli su un pool di database elastico|
|/servers/elasticPools/databases/read|Recupera elenco e dettagli dei database che fanno parte di un pool di database elastico su un server specifico|
|/servers/auditingPolicies/read|Recuperare i dettagli della tabella di server predefinito hello criteri configurati in un determinato server di controllo|
|/servers/auditingPolicies/write|Tabella di server hello predefinito per un determinato server di controllo delle modifiche|
|/servers/disasterRecoveryConfiguration/operationResults/read|Ottiene i risultati dell’operazione di configurazione di ripristino di emergenza|
|/servers/advisors/read|Restituisce l'elenco di Advisor è disponibile per il server hello|
|/servers/advisors/write|Aggiorna lo stato di esecuzione automatica di un advisor a livello di server.|
|/servers/advisors/recommendedActions/read|Restituisce l'elenco di azioni consigliate di preparazione specificato per il server hello|
|/servers/advisors/recommendedActions/write|Applicare l'azione sul server hello consigliata hello|
|/servers/usages/read|Quota DTU del server restituito e consuption DTU corrente da tutti i database all'interno di server hello|
|/servers/elasticPoolEstimates/read|Restituisce l’elenco di stime del pool elastico già create per questo server|
|/servers/elasticPoolEstimates/write|Crea una nuova stima del pool elastico per l'elenco dei database fornito|
|/servers/auditingSettings/read|Recuperare i dettagli del blob server hello criteri configurati in un determinato server di controllo|
|/servers/auditingSettings/write|Controllo delle modifiche hello server blob per un determinato server|
|/servers/auditingSettings/operationResults/read|Recuperare i risultati del blob server hello operazione di impostazione di criteri di controllo|
|/servers/backupLongTermRetentionVaults/read|Questa operazione è tooget usato un insieme di credenziali di conservazione dei backup a lungo termine. Restituisce informazioni sul server registrato toothis di hello insieme di credenziali.|
|/servers/backupLongTermRetentionVaults/write|Registra un insieme di credenziali di conservazione a lungo termine del backup|
|/servers/restorableDroppedDatabases/read|Recupera un elenco di database eliminati su uno specifico server che rientrano ancora nei criteri di conservazione. Questa operazione restituisce un elenco di database e metadati associati, come ad esempio la data di eliminazione.|
|/servers/databases/read|Restituisce un elenco di server in un gruppo di risorse per una sottoscrizione|
|/servers/databases/write|Crea un nuovo server o modifica le proprietà di un server esistente in un gruppo di risorse per una sottoscrizione|
|/servers/databases/delete|Elimina un server e tutti i database e i pool elastici contenuti|
|/servers/databases/export/action|Creare un nuovo database nel server di hello e distribuire lo schema e dati da un pacchetto con estensione DacPac|
|/servers/databases/VulnerabilityAssessmentScans/action|Esegue la scansione del database per la valutazione della vulnerabilità.|
|/servers/databases/pause/action|Sospende un database versione DataWarehouse|
|/servers/databases/resume/action|Riprende un database versione DataWarehouse|
|/servers/databases/operationResults/read|Viene utilizzata l'operazione tootrack lo stato di avanzamento dell'operazione di database a esecuzione prolungata, ad esempio scala.|
|/servers/databases/replicationLinks/read|Restituisce i dettagli sui collegamenti di replica stabiliti per uno specifico database|
|/servers/databases/replicationLinks/delete|È possibile terminare la relazione di replica hello in modo forzato e con potenziale perdita di dati|
|/servers/databases/replicationLinks/unlink/action|Terminare la relazione di replica hello in modo forzato o dopo la sincronizzazione con partner hello|
|/servers/databases/replicationLinks/failover/action|Failover dopo la sincronizzazione di tutte le modifiche da hello primario, creazione di questo database primario di remoto hello primari, rendendo della relazione di replica hello in un database secondario|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/action|Failover immediatamente con potenziale perdita di dati, rendendo il database in remoto hello primari, rendendo della relazione di replica hello primario in un database secondario|
|/servers/databases/replicationLinks/updateReplicationMode/action|Aggiornare la modalità di replica per collegamento toosynchronous o in modalità asincrona|
|/servers/databases/replicationLinks/operationResults/read|Ottiene lo stato di operazioni prolungate sui collegamenti di replica del database|
|/servers/databases/dataMaskingPolicies/read|Recuperare i dettagli del criterio configurato su un determinato database di maschera dati hello|
|/servers/databases/dataMaskingPolicies/write|Modifica i criteri di mascheramento dati per uno specifico database|
|/servers/databases/dataMaskingPolicies/rules/read|Recuperare i dettagli della regola dei criteri configurata su un determinato database di maschera dati hello|
|/servers/databases/dataMaskingPolicies/rules/write|Modifica la regola per i criteri di mascheramento dati per uno specifico database|
|/servers/databases/securityAlertPolicies/read|Recuperare i dettagli dei criteri di rilevamento minacce hello configurato su un determinato database|
|/servers/databases/securityAlertPolicies/write|Modificare i criteri di rilevamento minacce hello per un determinato database|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions/read|Restituisce i tipi di metriche disponibili per i database|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/read|Ottiene l'impostazione di diagnostica hello per risorse hello|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crea o aggiorna l'impostazione di diagnostica di hello per risorsa hello|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions/read|Ottiene i log disponibili hello per i database|
|/servers/databases/topQueries/read|Restituisce le statistiche aggregate a runtime per la query selezionata nel periodo di tempo selezionato|
|/servers/databases/topQueries/queryText/read|Restituisce il testo di hello Transact-SQL per l'ID query selezionata|
|/servers/databases/topQueries/statistics/read|Restituisce le statistiche aggregate a runtime per la query selezionata nel periodo di tempo selezionato|
|/servers/databases/connectionPolicies/read|Recuperare i dettagli dei criteri di connessione hello configurato su un determinato database|
|/servers/databases/connectionPolicies/write|Modifica i criteri di connessione per uno specifico database|
|/servers/databases/metrics/read|Restituisce le metriche di utilizzo delle risorse del database|
|/servers/databases/auditRecords/read|Recuperare i record di controllo di hello database blob|
|/servers/databases/transparentDataEncryption/read|Recupera lo stato e i dettagli della funzionalità di sicurezza di Transparent Data Encryption per uno specifico database|
|/servers/databases/transparentDataEncryption/write|Abilita o disabilita la Transparent Data Encryption per uno specifico database|
|/servers/databases/transparentDataEncryption/operationResults/read|Recupera lo stato e i dettagli della funzionalità di sicurezza di Transparent Data Encryption per uno specifico database|
|/servers/databases/auditingPolicies/read|Recuperare i dettagli del criterio di tabella hello configurato su un determinato database|
|/servers/databases/auditingPolicies/write|Modificare i criteri di controllo tabella hello per un determinato database|
|/servers/databases/dataWarehouseQueries/read|Restituisce informazioni query distribuzione hello data warehouse per l'ID query selezionata|
|/servers/databases/dataWarehouseQueries/<br>dataWarehouseQuerySteps/read|Distributed di hello restituisce informazioni sui passaggi di query per l'ID di passaggio selezionato di query di data warehouse|
|/servers/databases/serviceTierAdvisors/read|Restituire suggerimento sulla scalabilità del database verso l'alto o verso il basso in base alle prestazioni tooimprove statistiche di esecuzione query o ridurre i costi|
|/servers/databases/advisors/read|Restituisce l'elenco di Advisor è disponibile per il database hello|
|/servers/databases/advisors/write|Aggiorna lo stato di esecuzione automatica di un advisor a livello di database.|
|/servers/databases/advisors/recommendedActions/read|Restituisce l'elenco di azioni consigliate di preparazione specificato per il database hello|
|/servers/databases/advisors/recommendedActions/write|Applicare l'azione sul database hello consigliata hello|
|/servers/databases/usages/read|Restituisce la dimensione massima raggiungibile dal database e la dimensione attualmente occupata dai dati|
|/servers/databases/queryStore/read|Restituisce i valori correnti delle impostazioni di archivio Query per database hello|
|/servers/databases/queryStore/write|Aggiorna l'impostazione di archivio Query per il database hello|
|/servers/databases/auditingSettings/read|Recuperare i dettagli del criterio di controllo blob hello configurato su un determinato database|
|/servers/databases/auditingSettings/write|Modificare i criteri di controllo hello blob per un determinato database|
|/servers/databases/schemas/tables/recommendedIndexes/read|Recupera l’elenco di raccomandazioni sull’indice su un database|
|/servers/databases/schemas/tables/recommendedIndexes/write|Applica la raccomandazione sull’indice|
|/servers/databases/schemas/tables/columns/read|Recupera l'elenco delle colonne di una tabella|
|/servers/databases/missingindexes/read|Restituire suggerimenti toocreate gli indici di database, modificare o eliminare ordine tooimprove prestazioni di query|
|/servers/databases/missingindexes/write|Usa la raccomandazione sull’indice di database in uno specifico database|
|/servers/databases/importExportOperationResults/read|Restituisce i dettagli sulle operazioni di importazione o esportazione del database dal DacPac situato sull’account di archiviazione|
|/servers/importExportOperationResults/read|Restituire l'elenco di hello con i dettagli per le operazioni di importazione di database da account di archiviazione in un determinato server|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Operazione | Descrizione |
|---|---|
|/register/action|Registra sottoscrizione hello per provider di risorse di archiviazione hello e consente la creazione di hello di account di archiviazione.|
|/checknameavailability/read|Controlla che il nome dell’account sia valido e non in uso.|
|/storageAccounts/write|Crea un account di archiviazione con hello specificato parametri o aggiornamento hello proprietà o i tag oppure aggiunge personalizzato dominio per hello specificato l'account di archiviazione.|
|/storageAccounts/delete|Elimina un account di archiviazione esistente.|
|/storageAccounts/listkeys/action|Restituisce le chiavi di accesso hello per hello specificato l'account di archiviazione.|
|/storageAccounts/regeneratekey/action|Rigenerare le chiavi di accesso hello per hello specificato l'account di archiviazione.|
|/storageAccounts/read|Restituisce l'elenco di account di archiviazione di hello o ottiene le proprietà di hello per hello specificavano l'account di archiviazione.|
|/storageAccounts/listAccountSas/action|Restituisce il token di firma di accesso condiviso di hello per hello specificato l'account di archiviazione.|
|/storageAccounts/listServiceSas/action|Token SAS del servizio di archiviazione|
|/storageAccounts/services/diagnosticSettings/write|Crea/Aggiorna le impostazioni di diagnostica dell’account di archiviazione.|
|/skus/read|Elenca gli SKU supportati da Microsoft.Storage hello.|
|/usages/read|Restituisce hello limite e conteggio di utilizzo corrente di hello per le risorse di hello sottoscrizione specificata|
|/operations/read|Stato di hello viene eseguito il polling di un'operazione asincrona.|
|/locations/deleteVirtualNetworkOrSubnets/action|Avvisa Microsoft.Storage che la rete virtuale o la subnet è in fase di eliminazione|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Operazione | Descrizione |
|---|---|
|/managers/clearAlerts/action|Deselezionare tutti gli avvisi di hello associati al gestore di dispositivi hello.|
|/managers/getActivationKey/action|Ottieni chiave di attivazione per la gestione di dispositivi hello.|
|/managers/regenerateActivationKey/action|Rigenerare la chiave di attivazione per la gestione di dispositivi hello.|
|/managers/regenarateRegistationCertificate/action|Rigenerare il certificato di registrazione per i responsabili di dispositivo hello.|
|/managers/getEncryptionKey/action|Ottenere la chiave di crittografia per la gestione di dispositivi hello.|
|/managers/read|Elenca o ottiene hello Device Manager|
|/managers/delete|Elimina Manager dispositivi hello|
|/managers/write|Crea o aggiorna hello Device Manager|
|/managers/configureDevice/action|Configura un dispositivo|
|/managers/listActivationKey/action|Ottiene la chiave di attivazione hello di hello dispositivo StorSimple Manager.|
|/managers/listPublicEncryptionKey/action|Elenca le chiavi di crittografia pubbliche di uno strumento Gestione dispositivi StorSimple.|
|/managers/listPrivateEncryptionKey/action|Ottiene la chiave di crittografia privata per uno strumento Gestione dispositivi StorSimple.|
|/managers/provisionCloudAppliance/action|Crea una nuova appliance cloud.|
|/Managers/write|L'operazione Crea insieme di credenziali crea una risorsa di Azure di tipo 'vault'|
|/Managers/read|Hello operazione Ottieni insieme di credenziali Ottiene un oggetto che rappresenta le risorse di Azure di tipo 'vault' hello|
|/Managers/delete|Hello Elimina insieme di credenziali operazione eliminazioni hello specificato risorsa di Azure di tipo 'vault'|
|/managers/storageAccountCredentials/write|Creare o aggiornare le credenziali dell'Account di archiviazione hello|
|/managers/storageAccountCredentials/read|Elenca o ottiene le credenziali dell'Account di archiviazione hello|
|/managers/storageAccountCredentials/delete|Elimina le credenziali dell'Account di archiviazione hello|
|/managers/storageAccountCredentials/listAccessKey/action|Elenca le chiavi di accesso delle credenziali dell'account di archiviazione|
|/managers/accessControlRecords/read|Elenca o ottiene hello record di controllo di accesso|
|/managers/accessControlRecords/write|Creare o aggiornare i record di controllo di accesso hello|
|/managers/accessControlRecords/delete|Elimina record di controllo di accesso hello|
|/managers/metrics/read|Elenca o ottiene hello metriche|
|/managers/bandwidthSettings/read|L'elenco delle impostazioni della larghezza di banda hello (solo serie 8000)|
|/managers/bandwidthSettings/write|Crea una nuova impostazione o aggiorna le impostazioni di larghezza di banda esistenti (solo serie 8000)|
|/managers/bandwidthSettings/delete|Elimina impostazioni di larghezza di banda esistenti (solo serie 8000)|
|/Managers/extendedInformation/read|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/Managers/extendedInformation/write|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/Managers/extendedInformation/delete|Hello operazione Ottieni informazioni estese Ottiene informazioni estese di un oggetto che rappresenta le risorse di Azure di tipo hello? insieme di credenziali?|
|/managers/alerts/read|Elenca o ottiene hello avvisi|
|/managers/storageDomains/read|Elenca o ottiene hello archiviazione domini|
|/managers/storageDomains/write|Creare o aggiornare i domini di archiviazione hello|
|/managers/storageDomains/delete|Elimina hello archiviazione domini|
|/managers/devices/scanForUpdates/action|Verifica la disponibilità di aggiornamenti per un dispositivo.|
|/managers/devices/download/action|Scarica aggiornamenti per un dispositivo.|
|/managers/devices/install/action|Installa aggiornamenti in un dispositivo.|
|/managers/devices/read|Elenca o ottiene hello dispositivi|
|/managers/devices/write|Creare o aggiornare i dispositivi hello|
|/managers/devices/delete|Elimina i dispositivi hello|
|/managers/devices/deactivate/action|Disattiva un dispositivo.|
|/managers/devices/publishSupportPackage/action|Pubblica il pacchetto per il supporto di un dispositivo per la risoluzione dei problemi da parte del supporto tecnico Microsoft.|
|/managers/devices/failover/action|Failover del dispositivo hello.|
|/managers/devices/sendTestAlertEmail/action|Invia messaggio di avviso di test tooconfigured destinatari di posta elettronica.|
|/managers/devices/installUpdates/action|Installa gli aggiornamenti nei dispositivi hello|
|/managers/devices/listFailoverSets/action|Elenco hello failover imposta per un dispositivo esistente.|
|/managers/devices/listFailoverTargets/action|Elenco di destinazioni di failover di dispositivi hello|
|/managers/devices/publicEncryptionKey/action|Chiave di crittografia pubblica elenco di gestione di dispositivi hello|
|/managers/devices/hardwareComponentGroups/<br>read|Hello elenco gruppi di componenti Hardware|
|/managers/devices/hardwareComponentGroups/<br>changeControllerPowerState/action|Modifica lo stato di alimentazione del controller dei gruppi di componenti hardware|
|/managers/devices/metrics/read|Elenca o ottiene hello metriche|
|/managers/devices/chapSettings/write|Creare o aggiornare le impostazioni Chap hello|
|/managers/devices/chapSettings/read|Elenca o ottiene le impostazioni Chap hello|
|/managers/devices/chapSettings/delete|Elimina le impostazioni Chap hello|
|/managers/devices/backupScheduleGroups/read|Elenchi o gruppi di pianificazione di Backup hello Ottiene|
|/managers/devices/backupScheduleGroups/write|Crea o aggiorna i gruppi di pianificazione di Backup hello|
|/managers/devices/backupScheduleGroups/delete|Elimina gruppi di pianificazione di Backup hello|
|/managers/devices/updateSummary/read|Elenca o ottiene hello riepilogo aggiornamento|
|/managers/devices/migrationSourceConfigurations/<br>import/action|Importa le configurazioni di origine per la migrazione|
|/managers/devices/migrationSourceConfigurations/<br>startMigrationEstimate/action|Avviare un processo tooestimate hello durante hello processo di migrazione.|
|/managers/devices/migrationSourceConfigurations/<br>startMigration/action|Avvia la migrazione usando le configurazioni di origine|
|/managers/devices/migrationSourceConfigurations/<br>confirmMigration/action|Conferma una migrazione completata correttamente e ne esegue il commit.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationEstimate/action|Recuperare lo stato di hello per processo di stima della migrazione hello.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationStatus/action|Recuperare lo stato di hello per la migrazione di hello.|
|/managers/devices/migrationSourceConfigurations/<br>fetchConfirmMigrationStatus/action|Recupero hello conferma lo stato della migrazione.|
|/managers/devices/alertSettings/read|Elenca o ottiene le impostazioni degli avvisi di hello|
|/managers/devices/alertSettings/write|Creare o aggiornare le impostazioni degli avvisi di hello|
|/managers/devices/networkSettings/read|Elenca o ottiene le impostazioni di rete hello|
|/managers/devices/networkSettings/write|Crea nuove impostazioni di rete o aggiorna quelle esistenti|
|/managers/devices/jobs/read|Elenca o ottiene i processi di hello|
|/managers/devices/jobs/cancel/action|Annulla un processo in esecuzione|
|/managers/devices/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/devices/volumeContainers/write|Crea nuovi contenitori del volume o aggiorna quelli esistenti (solo serie 8000)|
|/managers/devices/volumeContainers/read|Elenco di contenitori di volumi hello (solo serie 8000)|
|/managers/devices/volumeContainers/delete|Elenca un contenitore del volume esistente (solo serie 8000)|
|/managers/devices/volumeContainers/listEncryptionKeys/action|Elenca le chiavi di crittografia dei contenitori del volume|
|/managers/devices/volumeContainers/rolloverEncryptionKey/action|Sostituisce le chiavi di crittografia dei contenitori del volume|
|/managers/devices/volumeContainers/metrics/read|Elenco hello metriche|
|/managers/devices/volumeContainers/volumes/read|Elenco volumi hello|
|/managers/devices/volumeContainers/volumes/write|Crea nuovi volumi o aggiorna quelli esistenti|
|/managers/devices/volumeContainers/volumes/delete|Elimina i volumi esistenti|
|/managers/devices/volumeContainers/volumes/metrics/read|Elenco hello metriche|
|/managers/devices/volumeContainers/volumes/metricsDefinitions/read|Elenco di definizioni di metriche hello|
|/managers/devices/volumeContainers/metricsDefinitions/read|Elenco di definizioni di metriche hello|
|/managers/devices/iscsiservers/read|Elenca o ottiene iSCSI hello server|
|/managers/devices/iscsiservers/write|Crea o aggiorna iSCSI hello server|
|/managers/devices/iscsiservers/delete|Elimina iSCSI hello server|
|/managers/devices/iscsiservers/backup/action|Esegue il backup di un server iSCSI.|
|/managers/devices/iscsiservers/metrics/read|Elenca o ottiene hello metriche|
|/managers/devices/iscsiservers/disks/read|Elenca o ottiene hello dischi|
|/managers/devices/iscsiservers/disks/write|Creare o aggiornare i dischi hello|
|/managers/devices/iscsiservers/disks/delete|Elimina dischi hello|
|/managers/devices/iscsiservers/disks/metrics/read|Elenca o ottiene hello metriche|
|/managers/devices/iscsiservers/disks/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/devices/iscsiservers/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/devices/backups/read|Elenca o ottiene hello del Set di Backup|
|/managers/devices/backups/delete|Eliminazioni hello del Set di Backup|
|/managers/devices/backups/restore/action|Ripristinare tutti i volumi di hello da un set di backup.|
|/managers/devices/backups/elements/clone/action|Clona una condivisione o volume usando un elemento di backup.|
|/managers/devices/backupPolicies/write|Crea nuovi criteri di backup o aggiorna quelli esistenti (solo serie 8000)|
|/managers/devices/backupPolicies/read|Hello elenco Criteri di Backup (solo serie 8000)|
|/managers/devices/backupPolicies/delete|Elimina criteri di backup esistenti (solo serie 8000)|
|/managers/devices/backupPolicies/backup/action|Eseguire il backup di tutti i volumi di hello protetti dai criteri hello un toocreate backup manuale un su richiesta.|
|/managers/devices/backupPolicies/schedules/write|Crea pianificazioni o aggiorna pianificazioni esistenti|
|/managers/devices/backupPolicies/schedules/read|Elenco hello pianificazioni|
|/managers/devices/backupPolicies/schedules/delete|Elimina le pianificazioni esistenti|
|/managers/devices/securitySettings/update/action|Aggiornare le impostazioni di sicurezza hello.|
|/managers/devices/securitySettings/read|Elenco di impostazioni di sicurezza hello|
|/managers/devices/securitySettings/<br>syncRemoteManagementCertificate/action|Sincronizzare il certificato di gestione remota hello per un dispositivo.|
|/managers/devices/securitySettings/write|Crea nuove impostazioni di protezione o aggiorna quelle esistenti|
|/managers/devices/fileservers/read|Elenca o ottiene hello File server|
|/managers/devices/fileservers/write|Crea o aggiorna hello File server|
|/managers/devices/fileservers/delete|Elimina hello File server|
|/managers/devices/fileservers/backup/action|Esegue il backup di un file server.|
|/managers/devices/fileservers/metrics/read|Elenca o ottiene hello metriche|
|/managers/devices/fileservers/shares/write|Creare o aggiornare le condivisioni hello|
|/managers/devices/fileservers/shares/read|Elenca o ottiene hello condivisioni|
|/managers/devices/fileservers/shares/delete|Elimina hello condivisioni|
|/managers/devices/fileservers/shares/metrics/read|Elenca o ottiene hello metriche|
|/managers/devices/fileservers/shares/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/devices/fileservers/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/devices/timeSettings/read|Elenca o ottiene le impostazioni dell'ora hello|
|/managers/devices/timeSettings/write|Crea nuove impostazioni ora o aggiorna quelle esistenti|
|/Managers/certificates/write|operazione di certificato risorsa Aggiorna Hello Aggiorna certificato della credenziale dell'insieme di credenziali/risorsa hello.|
|/managers/cloudApplianceConfigurations/read|Elenco di configurazioni supportate di Cloud accessorio hello|
|/managers/metricsDefinitions/read|Elenca o ottiene le definizioni di metriche di hello|
|/managers/encryptionSettings/read|Elenca o ottiene le impostazioni di crittografia hello|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Operazione | Descrizione |
|---|---|
|/streamingjobs/Start/action|Avvia un processo di Analisi di flusso|
|/streamingjobs/Stop/action|Arresta un processo di Analisi di flusso|
|/streamingjobs/Read|Legge un processo di Analisi di flusso|
|/streamingjobs/Write|Scrive un processo di Analisi di flusso|
|/streamingjobs/Delete|Elimina un processo di Analisi di flusso|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/read|Ottiene le metriche disponibili hello per streamingjobs|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/read|Legge un'impostazione di diagnostica.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/write|Scrive un'impostazione di diagnostica.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/read|Ottiene i log disponibili hello per streamingjobs|
|/streamingjobs/transformations/Read|Crea una trasformazione processo di Analisi di flusso|
|/streamingjobs/transformations/Write|Scrive una trasformazione processo di Analisi di flusso|
|/streamingjobs/transformations/Delete|Elimina una trasformazione processo di Analisi di flusso|
|/streamingjobs/inputs/Read|Legge un input processo di Analisi di flusso|
|/streamingjobs/inputs/Write|Scrive un input processo di Analisi di flusso|
|/streamingjobs/inputs/Delete|Elimina un input processo di Analisi di flusso|
|/streamingjobs/outputs/Read|Legge un output processo di Analisi di flusso|
|/streamingjobs/outputs/Write|Scrive un output processo di Analisi di flusso|
|/streamingjobs/outputs/Delete|Elimina un output processo di Analisi di flusso|

## <a name="microsoftsupport"></a>Microsoft.Support

| Operazione | Descrizione |
|---|---|
|/register/action|Registra i Provider di risorse tooSupport|
|/supportTickets/read|Ottiene i dettagli di Ticket di supporto (incluso lo stato, gravità, i dettagli di contatto e le comunicazioni) o ottiene l'elenco di hello di ticket di supporto per le sottoscrizioni.|
|/supportTickets/write|Crea o aggiorna un ticket di supporto. È possibile creare un ticket di supporto per problemi associati ai settori Tecnico, Fatturazione, Quote o Gestione della sottoscrizione. È possibile aggiornare la gravità, i dettagli di contatto e le comunicazioni dei ticket di supporto esistenti.|

## <a name="microsoftweb"></a>Microsoft.Web

| Operazione | Descrizione |
|---|---|
|/unregister/action|Annullare la registrazione del provider di risorse di Microsoft per la sottoscrizione di hello.|
|/validate/action|Convalida il provider di risorse Microsoft.Web per la sottoscrizione.|
|/register/action|Registrare il provider di risorse Microsoft per la sottoscrizione di hello.|
|/hostingEnvironments/Read|Ottenere le proprietà di hello dell'ambiente del servizio App|
|/hostingEnvironments/Write|Crea un nuovo ambiente del servizio app o ne aggiorna uno esistente|
|/hostingEnvironments/Delete|Elimina un ambiente del servizio app|
|/hostingEnvironments/reboot/Action|Riavvia tutti i computer in un ambiente del servizio app|
|/hostingenvironments/resume/action|Ripristina l'esecuzione degli ambienti di hosting.|
|/hostingenvironments/suspend/action|Sospende l'esecuzione degli ambienti di hosting.|
|/hostingenvironments/metricdefinitions/read|Ottiene le definizioni metrica degli ambienti di hosting.|
|/hostingEnvironments/workerPools/Read|Ottenere le proprietà di hello di un Pool di lavoro in un ambiente del servizio App|
|/hostingEnvironments/workerPools/Write|Crea un nuovo pool di lavoro in un ambiente del servizio app o ne aggiorna uno esistente|
|/hostingenvironments/workerpools/metricdefinitions/read|Ottiene le definizioni metrica dei pool di lavoro degli ambienti di hosting.|
|/hostingenvironments/workerpools/metrics/read|Ottiene la metrica dei pool di lavoro degli ambienti di hosting.|
|/hostingenvironments/workerpools/skus/read|Ottiene gli SKU dei pool di lavoro degli ambienti di hosting.|
|/hostingenvironments/workerpools/usages/read|Ottiene gli utilizzi dei pool di lavoro degli ambienti di hosting.|
|/hostingenvironments/sites/read|Ottiene le app Web degli ambienti di hosting.|
|/hostingenvironments/serverfarms/read|Ottiene i piani di servizio app degli ambienti di hosting.|
|/hostingenvironments/usages/read|Ottiene gli utilizzi degli ambienti di hosting.|
|/hostingenvironments/capacities/read|Ottiene le capacità degli ambienti di hosting.|
|/hostingenvironments/operations/read|Ottiene le operazioni degli ambienti di hosting.|
|/hostingEnvironments/multiRolePools/Read|Ottenere le proprietà di hello di un Pool di server front-end in un ambiente del servizio App|
|/hostingEnvironments/multiRolePools/Write|Crea un nuovo pool front-end o ne aggiorna uno esistente in un ambiente del servizio app|
|/hostingenvironments/multirolepools/metricdefinitions/read|Ottiene le definizioni metrica dei pool multiruolo degli ambienti di hosting.|
|/hostingenvironments/multirolepools/metrics/read|Ottiene la metrica dei pool multiruolo degli ambienti di hosting.|
|/hostingenvironments/multirolepools/skus/read|Ottiene gli SKU dei pool multiruolo degli ambienti di hosting.|
|/hostingenvironments/multirolepools/usages/read|Ottiene gli utilizzi dei pool multiruolo degli ambienti di hosting.|
|/hostingenvironments/diagnostics/read|Ottiene la diagnostica degli ambienti di hosting.|
|/publishingusers/read|Ottiene gli utenti di pubblicazione.|
|/publishingusers/write|Aggiorna gli utenti di pubblicazione.|
|/checknameavailability/read|Verifica se il nome della risorsa è disponibile.|
|/geoRegions/Read|Ottenere l'elenco di hello delle aree geografiche.|
|/sites/Read|Ottenere le proprietà di hello di un'App Web|
|/sites/Write|Crea una nuova app Web o ne aggiorna una esistente|
|/sites/Delete|Eliminare un'app Web esistente|
|/sites/backup/Action|Crea il backup di una nuova app Web|
|/sites/publishxml/Action|Ottiene l'XML del profilo di pubblicazione di un'app Web|
|/sites/publish/Action|Pubblica un'app Web|
|/sites/restart/Action|Riavvia un'app Web|
|/sites/start/Action|Avvia un'app Web|
|/sites/stop/Action|Arresta un'app Web|
|/sites/slotsswap/Action|Scambia gli slot di distribuzione di un'app Web|
|/sites/slotsdiffs/Action|Ottiene le differenze di configurazione tra l'app Web e gli slot|
|/sites/applySlotConfig/Action|Applicare la configurazione dello slot di app web da un'app web corrente di destinazione slot toohello|
|/sites/resetSlotConfig/Action|Ripristina la configurazione dell'app Web|
|/sites/functions/action|Funzioni delle app Web.|
|/sites/listsyncfunctiontriggerstatus/action|Elenca le app Web di stato dei trigger delle funzioni.|
|/sites/networktrace/action|App Web di traccia della rete.|
|/sites/newpassword/action|Consente di creare una nuova password per app Web.|
|/sites/sync/action|App Web di sincronizzazione.|
|/sites/operationresults/read|Ottiene i risultati delle operazioni delle app Web.|
|/sites/webjobs/read|Ottiene i processi Web delle app Web.|
|/sites/backup/read|Ottiene il backup delle app Web.|
|/sites/backup/write|Aggiorna il backup delle app Web.|
|/sites/metricdefinitions/read|Ottiene le definizioni di metrica per le app Web.|
|/sites/metrics/read|Ottiene la metrica di app Web.|
|/sites/continuouswebjobs/delete|Elimina i processi Web continui delle app Web.|
|/sites/continuouswebjobs/read|Ottiene i processi Web continui delle app Web.|
|/sites/continuouswebjobs/start/action|Avvia i processi Web continui delle app Web.|
|/sites/continuouswebjobs/stop/action|Interrompe i processi Web continui delle app Web.|
|/sites/domainownershipidentifiers/read|Ottiene gli identificatori di proprietà del dominio delle app Web.|
|/sites/domainownershipidentifiers/write|Aggiorna gli identificatori di proprietà del dominio delle app Web.|
|/sites/premieraddons/delete|Elimina i componenti aggiuntivi Premier delle app Web.|
|/sites/premieraddons/read|Ottiene i componenti aggiuntivi Premier delle app Web.|
|/sites/premieraddons/write|Aggiorna i componenti aggiuntivi Premier delle app Web.|
|/sites/triggeredwebjobs/delete|Elimina i processi Web attivati delle app Web.|
|/sites/triggeredwebjobs/read|Ottiene i processi Web attivati delle app Web.|
|/sites/triggeredwebjobs/run/action|Esegue i processi Web attivati delle app Web.|
|/sites/hostnamebindings/delete|Elimina i binding nome host delle app Web.|
|/sites/hostnamebindings/read|Ottiene i binding nome host delle app Web.|
|/sites/hostnamebindings/write|Aggiorna i binding nome host delle app Web.|
|/sites/virtualnetworkconnections/delete|Elimina le connessioni di rete virtuale delle app Web.|
|/sites/virtualnetworkconnections/read|Ottiene le connessioni di rete virtuale delle app Web.|
|/sites/virtualnetworkconnections/write|Aggiorna le connessioni di rete virtuale delle app Web.|
|/sites/virtualnetworkconnections/gateways/read|Ottiene i gateway delle connessioni di rete virtuale delle app Web.|
|/sites/virtualnetworkconnections/gateways/write|Aggiorna i gateway delle connessioni di rete virtuale delle app Web.|
|/sites/publishxml/read|Ottiene l'XML di pubblicazione delle app Web.|
|/sites/hybridconnectionrelays/read|Ottiene i relay di connessione ibrida delle app Web.|
|/sites/perfcounters/read|Ottiene i contatori delle prestazioni delle app Web.|
|/sites/usages/read|Ottiene gli utilizzi delle app Web.|
|/sites/slots/Write|Crea un nuovo slot di app Web o ne aggiorna uno esistente|
|/sites/slots/Delete|Elimina uno slot di app Web esistente|
|/sites/slots/backup/Action|Crea un nuovo backup di slot di app Web.|
|/sites/slots/publishxml/Action|Ottiene l'XML del profilo di pubblicazione per uno slot di app Web|
|/sites/slots/publish/Action|Pubblica uno slot di app Web|
|/sites/slots/restart/Action|Riavvia uno slot di app Web|
|/sites/slots/start/Action|Avvia uno slot di app Web|
|/sites/slots/stop/Action|Arresta uno slot di app Web|
|/sites/slots/slotsswap/Action|Scambia gli slot di distribuzione di un'app Web|
|/sites/slots/slotsdiffs/Action|Ottiene le differenze di configurazione tra l'app Web e gli slot|
|/sites/slots/applySlotConfig/Action|Applicare la configurazione dello slot di app web da uno slot di destinazione slot toohello corrente.|
|/sites/slots/resetSlotConfig/Action|Ripristina la configurazione dello slot di app Web|
|/sites/slots/Read|Ottenere le proprietà di hello di uno slot di distribuzione di App Web|
|/sites/slots/newpassword/action|Consente di creare una nuova password per slot di app Web.|
|/sites/slots/sync/action|Sincronizza gli slot di app Web.|
|/sites/slots/operationresults/read|Ottiene i risultati delle operazioni degli slot di app Web.|
|/sites/slots/webjobs/read|Ottiene i processi Web degli slot per le app Web.|
|/sites/slots/backup/write|Aggiorna il backup degli slot per le app Web.|
|/sites/slots/metricdefinitions/read|Ottiene le definizioni metrica degli slot per le app Web.|
|/sites/slots/metrics/read|Ottiene la metrica degli slot per le app Web.|
|/sites/slots/continuouswebjobs/delete|Elimina i processi Web continui degli slot per le app Web.|
|/sites/slots/continuouswebjobs/read|Ottiene i processi Web continui degli slot per le app Web.|
|/sites/slots/continuouswebjobs/start/action|Avvia i processi Web continui degli slot per le app Web.|
|/sites/slots/continuouswebjobs/stop/action|Arresta i processi Web continui degli slot per le app Web.|
|/sites/slots/premieraddons/delete|Elimina i componenti aggiuntivi Premier degli slot per le app Web.|
|/sites/slots/premieraddons/read|Ottiene i componenti aggiuntivi Premier degli slot per le app Web.|
|/sites/slots/premieraddons/write|Aggiorna i componenti aggiuntivi Premier degli slot per le app Web.|
|/sites/slots/triggeredwebjobs/delete|Elimina i processi Web attivati degli slot per le app Web.|
|/sites/slots/triggeredwebjobs/read|Ottiene i processi Web attivati degli slot per le app Web.|
|/sites/slots/triggeredwebjobs/run/action|Esegue i processi Web attivati degli slot per le app Web.|
|/sites/slots/hostnamebindings/delete|Elimina le associazioni nome host degli slot per le app Web.|
|/sites/slots/hostnamebindings/read|Ottiene le associazioni nome host degli slot per le app Web.|
|/sites/slots/hostnamebindings/write|Aggiorna le associazioni nome host degli slot per le app Web.|
|/sites/slots/phplogging/read|Ottiene la registrazione PHP degli slot per le app Web.|
|/sites/slots/virtualnetworkconnections/delete|Elimina le connessioni rete virtuale degli slot per le app Web.|
|/sites/slots/virtualnetworkconnections/read|Ottiene le connessioni rete virtuale degli slot per le app Web.|
|/sites/slots/virtualnetworkconnections/write|Aggiorna le connessioni rete virtuale degli slot per le app Web.|
|/sites/slots/virtualnetworkconnections/gateways/write|Aggiorna i gateway delle connessioni rete virtuale degli slot per le app Web.|
|/sites/slots/usages/read|Ottiene gli utilizzi degli slot per le app Web.|
|/sites/slots/hybridconnection/delete|Elimina la connessione ibrida degli slot per le app Web.|
|/sites/slots/hybridconnection/read|Ottiene la connessione ibrida degli slot per le app Web.|
|/sites/slots/hybridconnection/write|Aggiorna la connessione ibrida degli slot per le app Web.|
|/sites/slots/config/Read|Ottiene le impostazioni di configurazione degli slot per le app Web|
|/sites/slots/config/list/Action|Elenca le impostazioni importanti per la sicurezza degli slot per le app Web, quali le credenziali di pubblicazione, le impostazioni delle app e le stringhe di connessione|
|/sites/slots/config/Write|Aggiorna le impostazioni di configurazione degli slot per le app Web|
|/sites/slots/config/delete|Elimina la configurazione degli slot per le app Web.|
|/sites/slots/instances/read|Ottiene le istanze degli slot per le app Web.|
|/sites/slots/instances/processes/read|Ottiene i processi delle istanze degli slot per le app Web.|
|/sites/slots/instances/deployments/read|Ottiene le distribuzioni delle istanze degli slot per le app Web.|
|/sites/slots/sourcecontrols/Read|Ottiene le impostazioni di configurazione del controllo codice sorgente degli slot per le app Web|
|/sites/slots/sourcecontrols/Write|Aggiorna le impostazioni di configurazione del controllo codice sorgente degli slot per le app Web|
|/sites/slots/sourcecontrols/Delete|Elimina le impostazioni di configurazione del controllo codice sorgente degli slot per le app Web|
|/sites/slots/restore/read|Ottiene il ripristino degli slot per le app Web.|
|/sites/slots/analyzecustomhostname/read|Ottiene l'analisi nome host personalizzato degli slot per le app Web.|
|/sites/slots/backups/Read|Ottenere le proprietà di hello del backup degli slot dell'app web|
|/sites/slots/backups/list/action|Elenca i backup degli slot per le app Web.|
|/sites/slots/backups/restore/action|Ripristina i backup degli slot per le app Web.|
|/sites/slots/deployments/delete|Elimina le distribuzioni degli slot per le app Web.|
|/sites/slots/deployments/read|Ottiene le distribuzioni degli slot per le app Web.|
|/sites/slots/deployments/write|Aggiorna le distribuzioni degli slot per le app Web.|
|/sites/slots/deployments/log/read|Ottiene il registro delle distribuzioni degli slot per le app Web.|
|/sites/hybridconnection/delete|Elimina la connessione ibrida delle app Web.|
|/sites/hybridconnection/read|Ottiene la connessione ibrida delle app Web.|
|/sites/hybridconnection/write|Aggiorna la connessione ibrida delle app Web.|
|/sites/recommendationhistory/read|Ottiene la cronologia consigli delle app Web.|
|/sites/recommendations/Read|Ottenere l'elenco di hello di indicazioni per l'app web.|
|/sites/recommendations/disable/action|Disattiva i consigli delle app Web.|
|/sites/config/Read|Ottiene le impostazioni di configurazione delle app Web|
|/sites/config/list/Action|Elenca le impostazioni dell'app Web sensibili alla sicurezza, ad esempio le credenziali di pubblicazione, le impostazioni dell'app e le stringhe di connessione|
|/sites/config/Write|Aggiorna le impostazioni di configurazione dell'app Web|
|/sites/config/delete|Elimina la configurazione delle app Web.|
|/sites/instances/read|Ottiene le istanze delle app Web.|
|/sites/instances/processes/delete|Elimina i processi delle istanze delle app Web.|
|/sites/instances/processes/read|Ottiene i processi delle istanze delle app Web.|
|/sites/instances/deployments/read|Ottiene le distribuzioni delle istanze delle app Web.|
|/sites/sourcecontrols/Read|Ottiene le impostazioni di configurazione del controllo codice sorgente dell'app Web|
|/sites/sourcecontrols/Write|Aggiorna le impostazioni di configurazione del controllo codice sorgente dell'app Web|
|/sites/sourcecontrols/Delete|Elimina le impostazioni di configurazione del controllo codice sorgente dell'app Web|
|/sites/restore/read|Ottiene il ripristino delle app Web.|
|/sites/analyzecustomhostname/read|Analizza il nome host personalizzato.|
|/sites/backups/Read|Ottenere le proprietà di hello del backup dell'app web|
|/sites/backups/list/action|Elenca i backup delle app Web.|
|/sites/backups/restore/action|Ripristina i backup delle app Web.|
|/sites/snapshots/read|Ottiene snapshot delle app Web.|
|/sites/functions/delete|Elimina funzioni delle app Web.|
|/sites/functions/listsecrets/action|Elenca i segreti delle funzioni delle app Web.|
|/sites/functions/read|Ottiene le funzioni delle app Web.|
|/sites/functions/write|Aggiorna le funzioni delle app Web.|
|/sites/deployments/delete|Elimina le distribuzioni delle app Web.|
|/sites/deployments/read|Ottiene le distribuzioni delle app Web.|
|/sites/deployments/write|Aggiorna le distribuzioni delle app Web.|
|/sites/deployments/log/read|Ottiene il registro delle distribuzioni delle app Web.|
|/sites/diagnostics/read|Ottiene la diagnostica delle app Web.|
|/sites/diagnostics/workerprocessrecycle/read|Ottiene il riciclo del processo di lavoro di diagnostica delle app Web.|
|/sites/diagnostics/workeravailability/read|Ottiene la disponibilità del processo di lavoro di diagnostica delle app Web.|
|/sites/diagnostics/runtimeavailability/read|Ottiene la disponibilità del runtime di diagnostica delle app Web.|
|/sites/diagnostics/cpuanalysis/read|Ottiene l'analisi CPU della diagnostica delle app Web.|
|/sites/diagnostics/servicehealth/read|Ottiene l'integrità di servizio della diagnostica delle app Web.|
|/sites/diagnostics/frebanalysis/read|Ottiene l'analisi FREB della diagnostica delle app Web.|
|/availablestacks/read|Ottiene gli stack disponibili.|
|/isusernameavailable/read|Verifica se il nome utente è disponibile.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Read|Ottenere l'elenco di hello delle API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Write|Aggiunge una nuova API o ne aggiorna una esistente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Delete|Elimina un'API esistente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Read|Ottenere l'elenco di hello delle connessioni.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Write|Salva una nuova connessione o ne aggiorna una esistente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Delete|Elimina una connessione esistente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Read|Legge gli ACL della connessione|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Write|Aggiunge o aggiorna un ACL della connessione|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Delete|Elimina un ACL della connessione|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connectionAcls/Read|Legge gli ACL della connessione per l'API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Read|Legge gli ACL della connessione|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Write|Crea o aggiorna gli ACL dell'API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Delete|Elimina gli ACL dell'API|
|/serverfarms/Read|Ottenere le proprietà di hello in un piano di servizio App|
|/serverfarms/Write|Crea un nuovo piano di servizio app o ne aggiorna uno esistente|
|/serverfarms/Delete|Eliminare un piano di servizio app esistente|
|/serverfarms/restartSites/Action|Riavvia tutte le app Web in un piano di servizio app|
|/serverfarms/operationresults/read|Ottiene i risultati dell'operazione per i piani di servizio app.|
|/serverfarms/capabilities/read|Ottiene le capacità dei piani di servizio app.|
|/serverfarms/metricdefinitions/read|Ottiene le definizioni metrica dei piani di servizio app.|
|/serverfarms/metrics/read|Ottiene la metrica dei piani di servizio app.|
|/serverfarms/hybridconnectionplanlimits/read|Ottiene i limiti del piano di connessione ibrida per i piani di servizio app.|
|/serverfarms/virtualnetworkconnections/read|Ottiene le connessioni rete virtuale dei piani di servizio app.|
|/serverfarms/virtualnetworkconnections/routes/delete|Elimina i percorsi delle connessioni rete virtuale dei piani di servizio app.|
|/serverfarms/virtualnetworkconnections/routes/read|Ottiene i percorsi delle connessioni rete virtuale dei piani di servizio app.|
|/serverfarms/virtualnetworkconnections/routes/write|Aggiorna i percorsi delle connessioni rete virtuale dei piani di servizio app.|
|/serverfarms/virtualnetworkconnections/gateways/write|Aggiorna i gateway delle connessioni rete virtuale dei piani di servizio app.|
|/serverfarms/firstpartyapps/settings/delete|Elimina le impostazioni delle app proprietarie dei piani di servizio app.|
|/serverfarms/firstpartyapps/settings/read|Ottiene le impostazioni delle app proprietarie dei piani di servizio app.|
|/serverfarms/firstpartyapps/settings/write|Aggiorna le impostazioni delle app proprietarie dei piani di servizio app.|
|/serverfarms/sites/read|Ottiene le app Web dei piani di servizio app.|
|/serverfarms/workers/reboot/action|Riavvia i ruoli di lavoro dei piani di servizio app.|
|/serverfarms/hybridconnectionrelays/read|Ottiene gli inoltri connessione ibrida dei piani di servizio app.|
|/serverfarms/skus/read|Ottiene gli SKU dei piani di servizio app.|
|/serverfarms/usages/read|Ottiene gli utilizzi dei piani di servizio app.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/read|Ottiene le app Web degli inoltri spazio dei nomi connessione ibrida dei piani di servizio app.|
|/ishostnameavailable/read|Verifica se il nome host è disponibile.|
|/connectionGateways/Read|Ottenere l'elenco di hello di gateway di connessione.|
|/connectionGateways/Write|Crea o aggiorna un gateway di connessione.|
|/connectionGateways/Delete|Elimina un gateway di connessione.|
|/connectionGateways/Join/Action|Unisce un gateway di connessione.|
|/classicmobileservices/read|Ottiene servizi mobili classici.|
|/skus/read|Ottiene SKU.|
|/certificates/Read|Ottenere l'elenco di hello dei certificati.|
|/certificates/Write|Aggiunge un nuovo certificato o ne aggiorna uno esistente.|
|/certificates/Delete|Elimina un certificato esistente.|
|/operations/read|Ottiene operazioni.|
|/recommendations/Read|Ottenere l'elenco di hello di indicazioni per le sottoscrizioni.|
|/ishostingenvironmentnameavailable/read|Definisce se il nome dell'ambiente di hosting è disponibile.|
|/apiManagementAccounts/Read|Ottenere l'elenco di hello di ApiManagementAccounts.|
|/apiManagementAccounts/Write|Aggiunge un nuovo account di Gestione API o ne aggiorna uno esistente|
|/apiManagementAccounts/Delete|Elimina un account di Gestione API esistente|
|/apiManagementAccounts/connectionAcls/Read|Ottenere l'elenco di hello degli elenchi ACL di connessione.|
|/apiManagementAccounts/apiAcls/Read|Legge gli ACL della connessione|
|/connections/Read|Ottenere l'elenco di hello delle connessioni.|
|/connections/Write|Crea o aggiorna una connessione.|
|/connections/Delete|Elimina una connessione.|
|/connections/Join/Action|Unisce una connessione.|
|/connections/confirmconsentcode/action|Conferma il codice di consenso delle connessioni.|
|/connections/listconsentlinks/action|Elenca i collegamenti di consenso per le connessioni.|
|/deploymentlocations/read|Ottiene i percorsi di distribuzione.|
|/sourcecontrols/read|Ottiene i controlli del codice sorgente.|
|/sourcecontrols/write|Aggiorna i controlli del codice sorgente.|
|/managedhostingenvironments/read|Ottiene gli ambienti di hosting gestiti.|
|/managedhostingenvironments/sites/read|Ottiene le app Web degli ambienti di hosting gestiti.|
|/managedhostingenvironments/serverfarms/read|Ottiene i piani di servizio app degli ambienti di hosting gestiti.|
|/locations/managedapis/read|Ottiene le API gestite dei percorsi.|
|/locations/apioperations/read|Ottiene le operazioni delle API dei percorsi.|
|/locations/connectiongatewayinstallations/read|Ottiene le installazioni dei gateway di connessione dei percorsi.|
|/listSitesAssignedToHostName/Read|Ottenere i nomi di siti assegnati toohostname.|

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[creare un ruolo personalizzato](role-based-access-control-custom-roles.md).

- Hello revisione [compilato nei ruoli RBAC](role-based-access-built-in-roles.md).

- Informazioni su come accedere a assegnazioni toomanage [utente](role-based-access-control-manage-assignments.md) o [dalla risorsa](role-based-access-control-configure.md) 
