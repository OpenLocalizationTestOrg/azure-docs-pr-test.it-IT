---
title: Come ottenere informazioni dettagliate con i report di gestione delle password di Azure AD | Documentazione Microsoft
description: In questo articolo viene descritto come toouse segnala tooget approfondite sulle operazioni di gestione delle password nell'organizzazione.
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Come i report tooget operational insights con la gestione delle password
> [!IMPORTANT]
> **Se si sta visualizzando questa pagina perché si riscontrano problemi nell'accesso,** [seguire questa procedura per cambiare e reimpostare la password](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

In questa sezione viene descritto come usare Azure Active Directory la gestione delle password segnala tooview come gli utenti utilizzano la reimpostazione della password e modificare all'interno dell'organizzazione.

* [**Panoramica dei report di gestione delle password**](#overview-of-password-management-reports)
* [**Come la gestione delle password tooview report nel nuovo portale di Azure hello**](#how-to-view-password-management-reports)
 * [Ruoli della directory consentiti tooread report](#directory-roles-allowed-to-read-reports)
* [**Tipi di attività Gestione della Password self-servizi in hello nuovo portale di Azure**](#self-service-password-management-activity-types)
 * [Bloccato dalla reimpostazione self-service delle password](#activity-type-blocked-from-self-service-password-reset)
 * [Modificare la password (self-service)](#activity-type-change-password-self-service)
 * [Reimpostare la password (amministratore)](#activity-type-reset-password-by-admin)
 * [Reimpostare la password (self-service)](#activity-type-reset-password-self-service)
 * [Stato di avanzamento dell'attività di reimpostazione della password self-service](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Sbloccare l'account utente (self-service)](#activity-type-unlock-user-account-self-service)
 * [Utente registrato per la reimpostazione della password self-service](#activity-type-user-registered-for-self-service-password-reset)
* [**La modalità di hello tooretrieve gli eventi di gestione delle password da report di Azure AD API e gli eventi**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Segnalazione dei limiti di recupero dati API](#reporting-api-data-retrieval-limitations)
* [**Reimpostazione della password di toodownload come eventi di registrazione rapidamente con PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Come la gestione delle password tooview report nel portale classico hello**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Attività di registrazione all'interno dell'organizzazione nel portale classico hello di reimpostazione della password di visualizzazione**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Attività all'interno dell'organizzazione nel portale classico hello reimpostazione della password di visualizzazione**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Informazioni generali sui report di gestione delle password
Dopo aver distribuito la reimpostazione della password, uno dei passaggi successivi più comuni di hello è toosee come perché è in uso nell'organizzazione.  Ad esempio, si consiglia una visione tooget in modalità di registrazione di utenti per la reimpostazione della password o il numero di password Reimposta eseguite negli ultimi giorni hello.  Ecco alcune delle domande frequenti hello che sarà in grado di tooanswer con report di gestione di password hello che esistono in hello [il portale di gestione di Azure](https://manage.windowsazure.com) oggi:

* Quante persone si sono registrate per la reimpostazione delle password?
* Chi ha eseguito la registrazione per la reimpostazione delle password?
* Quali dati vengono registrati?
* Quante persone hanno reimpostato la password in hello ultimi 7 giorni?
* Quali sono gli utenti metodi più comuni di hello o gli amministratori utilizzano tooreset le proprie password?
* Che cosa sono i comuni problemi faccia utenti o amministratori durante il tentativo di reimpostazione della password toouse?
* Con quale frequenza gli amministratori reimpostano le proprie password?
* Sono state rilevate eventuali attività sospette nell'ambito della reimpostazione delle password?

## <a name="how-tooview-password-management-reports"></a>Come report di gestione delle Password tooview
Nella nuova hello [portale di Azure](https://portal.azure.com) verifica, è necessario un modo migliore tooview reimpostazione e la password registrazione attività di reimpostazione password.  Seguire la procedura seguente hello sotto toofind hello la reimpostazione della password e la password reimpostare gli eventi di registrazione nel nuovo hello [portale Azure](https://portal.azure.com):

1. Passare troppo[**portal.azure.com**](https://portal.azure.com)
2. Fare clic su hello **più servizi** menu di navigazione di sinistra hello principale portale di Azure
3. Cercare **Azure Active Directory** in hello l'elenco dei servizi e selezionarlo
4. Fare clic su **utenti e gruppi** dal menu di navigazione di hello Azure Active Directory
5. Fare clic su hello **i log di controllo** elemento di navigazione hello utenti e gruppi di menu di navigazione. In questo verrà visualizzati tutti che si verificano gli eventi di controllo hello su tutti gli utenti di hello nella directory. È possibile filtrare questa toosee vista tutti hello password eventi correlati, nonché.
6. toofilter relative alla gestione di password questa vista tooonly hello eventi, fare clic su hello **filtro** pulsante nella parte superiore di hello del pannello hello.
7. Da hello **filtro** menu, seleziona hello **categoria** elenco a discesa e modificarlo toohello **la gestione delle Password Self-Service** tipo di categoria.
8. Elenco di hello facoltativamente ulteriore filtro scegliendo hello specifiche **attività** si è interessati
### <a name="direct-link-toouser-audit-blade"></a>Pannello di controllo tooUser collegamento diretto
Se si accede nel portale tooyour, ecco un pannello di controllo utente toohello collegamento diretto in cui è possibile visualizzare questi eventi:

* [Passare a gestione toouser direttamente visualizzazione controlli](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>I ruoli della directory consentito tooread report
Attualmente, hello seguenti ruoli di directory possono leggere i report di gestione delle Password di Azure Active Directory nel portale di Azure classico hello:

* Amministratore globale

Prima di essere in grado di tooread questi report, un amministratore globale nella società hello deve avere scelto aggiuntivo per questo toobe dati recuperata per conto dell'organizzazione hello visitando hello reporting scheda o audit log almeno una volta. Fino a quel momento, i dati per l'organizzazione non verranno raccolti.

ulteriori informazioni sui ruoli della directory e sono disponibili, vedere tooread [l'assegnazione di ruoli di amministratore in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Tipi di attività di gestione delle password self-service
Hello seguenti tipi di attività vengono visualizzati in hello **la gestione delle Password Self-Service** categoria di eventi di controllo.  Segue una descrizione per ogni tipo.

* [**Impedito la reimpostazione della password self-service** ](#activity-type-blocked-from-self-service-password-reset) -indica un utente ha tentato tooreset una password, utilizzare un controllo specifico oppure convalidare un numero di telefono più di 5 volte totale nelle 24 ore.
* [**Modificare la password (Self-Service)** ](#activity-type-change-password-self-service) -indica un utente eseguita volontario o forzato (scadenza tooexpiry) la modifica della password.
* [**Reimpostazione della password (dall'amministratore)** ](#activity-type-reset-password-by-admin) -indica che un amministratore che ha eseguito una reimpostazione per conto dell'utente dal portale di Azure hello password.
* [**Reimpostazione della password (Self-Service)** ](#activity-type-reset-password-self-service) -indica che un utente è stata reimpostata la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com).
* [**Lo stato di avanzamento di flusso attività di reimpostazione della password Self-Service** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indica ogni passaggio specifico segua un utente (ad esempio, passando una password specifica, reimposta il controllo dell'autenticazione) come parte della password hello processo di reimpostazione.
* [**Sbloccare l'account utente (Self-Service)** ](#activity-type-unlock-user-account-self-service) -indica che un utente sbloccato al proprio account di Active Directory senza reimpostare la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com) utilizzo di hello [sblocco dell'account di Active Directory senza reimpostazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funzionalità.
* [**L'utente ha registrato per la reimpostazione della password self-service** ](#activity-type-user-registered-for-self-service-password-reset) -indica un utente ha registrato tutti hello necessarie informazioni toobe in grado di tooreset la propria password in base ai criteri di reimpostazione password hello tenant attualmente specificato.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Tipo di attività: Bloccato dalla reimpostazione self-service delle password
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica un utente ha tentato tooreset una password, utilizzare un controllo specifico o convalidare un numero di telefono più di 5 volte totale nelle 24 ore.
* **Attività attore** -utente hello che è stata limitata dall'esecuzione di ulteriori operazioni di reimpostazione. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello che è stata limitata dall'esecuzione di ulteriori operazioni di reimpostazione. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Esito positivo_ -indica che un utente è stato limitato dall'esecuzione di qualsiasi Reimposta aggiuntive, tentare di eventuali altri metodi di autenticazione o convalidare eventuali altri numeri di telefono per hello 24 ore successive.
* **Activity Status Failure Reason** (Motivo dell'errore sullo stato dell'attività): non applicabile

### <a name="activity-type-change-password-self-service"></a>Tipo di attività: Modificare la password (self-service)
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica un utente eseguita volontario o forzato (scadenza tooexpiry) la modifica della password.
* **Attività attore** -utente hello che ha modificato la propria password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello che ha modificato la propria password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Success_ (Operazione riuscita): indica che un utente ha modificato correttamente la propria password.
 * _Errore_ -indica che un utente non è stato possibile toochange la propria password. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Activity Status Failure Reason** - (Motivo dell'errore sullo stato dell'attività)
 * _FuzzyPolicyViolationInvalidPassword_ -hello utente ha selezionato una password che è stato escluso automaticamente a causa di funzionalità escluse rilevamento Password della tooMicrosoft ricerca toobe troppo comune o particolarmente vulnerabili.

### <a name="activity-type-reset-password-by-admin"></a>Tipo di attività: Reimpostare la password (amministratore)
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un amministratore che ha eseguito una reimpostazione per conto dell'utente dal portale di Azure hello password.
* **Attività attore** -messaggio per l'amministratore che ha eseguito la reimpostazione per conto di un altro utente finale o un amministratore della password hello. Deve essere un amministratore globale, un amministratore di password, un amministratore utenti o un amministratore supporto tecnico.
* **Destinazione attività** -utente hello la cui password è stata reimpostata. Può essere un utente finale o un altro amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Success_ (Operazione riuscita): indica che un amministratore ha reimpostato correttamente la password dell'utente.
 * _Errore_ -indica che un amministratore non è riuscito toochange password di un utente. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.

### <a name="activity-type-reset-password-self-service"></a>Tipo di attività: Reimpostare la password (self-service)
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente è stata reimpostata la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com).
* **Attività attore** -utente hello Reimposta la propria password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello Reimposta la propria password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Success_ (Operazione riuscita): indica che un utente ha reimpostato correttamente la propria password.
 * _Errore_ -indica che un utente non è stato possibile tooreset la propria password. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Activity Status Failure Reason** - (Motivo dell'errore sullo stato dell'attività)
 * _FuzzyPolicyViolationInvalidPassword_ -salve ha selezionato una password che è stato escluso automaticamente a causa di funzionalità escluse rilevamento Password della tooMicrosoft ricerca toobe troppo comune o particolarmente vulnerabili.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Tipo di attività: Stato di avanzamento dell'attività di reimpostazione della password self-service
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica di ogni passaggio specifico di un utente passa (ad esempio, passando una password specifica, reimposta il controllo dell'autenticazione) come parte della password hello processo di reimpostazione.
* **Attività attore** -flusso di reimpostazione utente hello che ha eseguito una parte della password hello. Può essere un utente finale o un amministratore.
* **Destinazione attività** -flusso di reimpostazione utente hello che ha eseguito una parte della password hello. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Esito positivo_ -indica un passaggio specifico del flusso di reimpostazione della password hello completata su un utente.
 * _Errore_ -indica un passaggio specifico di password hello reimpostato flusso non è riuscito. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Allowed Activity Status Reasons** (Motivi degli stati attività consentite)
 * Vedere la tabella seguente per [tutti i motivi degli stati relativi alle attività di reimpostazione consentite](#allowed-values-for-details-column).

### <a name="activity-type-unlock-user-account-self-service"></a>Tipo di attività: Sbloccare l'account utente (self-service)
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente sbloccato al proprio account di Active Directory senza reimpostare la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com) utilizzando hello [AD sblocco dell'account senza reimpostazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) funzionalità.
* **Attività attore** -utente hello sbloccato il proprio account senza reimpostare la password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello sbloccato il proprio account senza reimpostare la password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Success_ (Operazione riuscita): indica che un utente ha sbloccato correttamente il proprio account.
 * _Errore_ -indica un utente non è riuscito toounlock al proprio account. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Tipo di attività: Utente registrato per la reimpostazione della password self-service
Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente ha registrato tutti hello necessarie informazioni toobe tooreset in grado della propria password in base ai criteri di reimpostazione password hello tenant attualmente specificato.
* **Attività attore** -utenti hello registrati per la reimpostazione della password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utenti hello registrati per la reimpostazione della password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
 * _Esito positivo_ -indica un utente registrato per la reimpostazione in base ai criteri correnti hello della password.
 * _Errore_ -indica un tooregister utente non è riuscita per la reimpostazione della password. Fare clic sulla riga hello consentirà hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello. Nota: questo non significa un utente è tooreset non è possibile la propria password, solo che egli non ha completato il processo di registrazione hello. Se sono presenti dati non verificati il proprio account corretto (ad esempio un numero di telefono non viene convalidato), anche se essi non verificato il numero di telefono, è comunque possibile utilizzarla tooreset la propria password. Per altre informazioni, vedere [Cosa accade quando un utente si registra?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>La modalità di hello tooretrieve gli eventi di gestione delle password da report di Azure AD API e gli eventi
A partire da agosto 2015, report hello Azure AD API e gli eventi supporta il recupero di informazioni hello incluse in hello password reset e la password reset segnalazioni con registrazione tutti. Tramite questa API, è possibile scaricare la reimpostazione della password singoli e gli eventi di registrazione per l'integrazione con la tecnologia del choce di reporting hello reimpostazione della password.

### <a name="how-tooget-started-with-hello-reporting-api"></a>La modalità di avvio tooget con hello reporting API
tooaccess questi dati, si devono toowrite un'app di piccole dimensioni oppure script tooretrieve dal server. [Informazioni su come iniziare tooget con hello API Azure AD Reporting](active-directory-reporting-api-getting-started.md).

Dopo aver creato uno script di lavoro, quindi è opportuno tooexamine hello password reimpostazione e registrazione degli eventi che è possibile recuperare toomeet gli scenari.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Elenca le colonne di hello disponibili per gli eventi di reimpostazione della password
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Elenca le colonne di hello disponibili per gli eventi di registrazione di reimpostazione della password

### <a name="reporting-api-data-retrieval-limitations"></a>Segnalazione dei limiti di recupero dati API
Attualmente, hello report di Azure AD e API eventi recupera backup troppo**75.000 singoli eventi** di hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) e [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) tipi , che si estende su hello **ultimi 30 giorni**.

Se è necessario tooretrieve o memorizzare dati oltre a questa finestra, è consigliabile salvarli in modo permanente in un database esterno e l'utilizzo delta di hello tooquery hello API risultanti. Una procedura consigliata è toobegin recupero dei dati, quando si avvia la password il processo di registrazione all'interno dell'organizzazione di reimpostare archiviarlo esternamente e proseguire delta hello tootrack da questo punto.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Reimpostazione della password di toodownload come eventi di registrazione rapidamente con PowerShell
Inoltre toousing hello report di Azure AD API e gli eventi direttamente, è inoltre possibile utilizzare hello di sotto di eventi di registrazione toorecent script PowerShell nella directory. Questo è utile nel caso in cui si desidera toosee che ha registrato recente o desidera che la password reimpostata implementazione tooensure avviene nel modo previsto.

* [Script di PowerShell per le attività di registrazione della reimpostazione della password self-service di Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Come la gestione delle password tooview report nel portale classico hello
report di gestione password hello toofind, procedura hello riportata di seguito:

1. Fare clic su hello **Active Directory** estensione hello [portale di Azure classico](https://manage.windowsazure.com).
2. Selezionare la directory dall'elenco di hello visualizzata nel portale di hello.
3. Fare clic su hello **report** scheda.
4. Cercare in hello **log attività** sezione.
5. Selezionare entrambi hello **attività di reimpostazione Password** report o hello **attività di registrazione reimpostazione Password** report.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Attività di registrazione nel portale classico hello di reimpostazione della password di visualizzazione
report attività di registrazione reimpostazione password Hello illustra che reimpostazione della password tutte le registrazioni che si sono verificati nell'organizzazione.  Una registrazione di reimpostazione della password viene visualizzata in questo report per qualsiasi utente che hanno registrato correttamente le informazioni di autenticazione password hello Reimposta portale di registrazione ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Intervallo di tempo massimo**: 30 giorni
* **Numero massimo di righe**: 75.000
* **Scaricabile**: Sì, tramite file CSV

### <a name="description-of-report-columns"></a>Descrizione delle colonne del report
Hello elenco seguente viene spiegata ciascuna delle colonne del report hello in dettaglio:

* **Utente** : operazione di registrazione di reimpostazione utente hello che hanno tentato di una password.
* **Ruolo** : ruolo di hello di hello utente nella directory hello.
* **Data e ora** : hello data e ora del tentativo di hello.
* **Dati registrati** : registrazione di reimpostazione della quale utente hello dati di autenticazione fornito durante la password.

### <a name="description-of-report-values"></a>Descrizione dei valori del report
Hello nella tabella seguente vengono descritti hello diversi valori consentiti per ogni colonna:

| Colonna | Valori consentiti e relativi significati |
| --- | --- |
| Dati registrati |**Messaggio di posta elettronica alternativo** – tooauthenticate posta elettronica tramite posta elettronica o l'autenticazione alternativo utente<p><p>**Telefono ufficio**: office phone tooauthenticate utilizzato dall'utente<p>**Cellulare** -tooauthenticate telefono cellulare o di autenticazione utilizzato dall'utente<p>**Domande di sicurezza** – domande di sicurezza dell'utente utilizzato tooauthenticate<p>**Qualsiasi combinazione di hello sopra (ad esempio posta elettronica alternativo + telefono cellulare)** : si verifica quando un criterio di 2 controllo viene specificato e Mostra i due metodi hello tooauthentication utente richiesta di reimpostazione della password. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Attività nel portale classico hello reimpostazione della password di visualizzazione
Questo report illustra tutti i tentativi di reimpostazione delle password che si sono verificati nell'organizzazione.

* **Intervallo di tempo massimo**: 30 giorni
* **Numero massimo di righe**: 75.000
* **Scaricabile**: Sì, tramite file CSV

### <a name="description-of-report-columns"></a>Descrizione delle colonne del report
Hello elenco seguente viene spiegata ciascuna delle colonne del report hello in dettaglio:

1. **Utente** : operazione (basato su campo di ID utente hello specificato quando l'utente hello proviene tooreset una password) per la reimpostazione utente hello che hanno tentato di una password.
2. **Ruolo** : ruolo di hello di hello utente nella directory hello.
3. **Data e ora** : hello data e ora del tentativo di hello.
4. **Uno o più metodi utilizzati** : i metodi di autenticazione hello utente utilizzato per questa operazione di reimpostazione.
5. **Risultato** : operazione di reimpostazione della password hello risultato finale hello.
6. **Dettagli** : hello dettagli del motivo per cui la reimpostazione della password hello comportato valore hello.  Include anche eventuali passaggi che è possibile eseguire tooresolve un errore imprevisto.

### <a name="description-of-report-values"></a>Descrizione dei valori del report
Hello nella tabella seguente vengono descritti hello diversi valori consentiti per ogni colonna:

| Colonna | Valori consentiti e relativi significati |
| --- | --- |
| Metodi usati |**Messaggio di posta elettronica alternativo** – tooauthenticate posta elettronica tramite posta elettronica o l'autenticazione alternativo utente<p>**Telefono ufficio** : office phone tooauthenticate utilizzato dall'utente<p>**Cellulare** – tooauthenticate telefono cellulare o di autenticazione utilizzato dall'utente<p>**Domande di sicurezza** – domande di sicurezza dell'utente utilizzato tooauthenticate<p>**Qualsiasi combinazione di hello sopra (ad esempio posta elettronica alternativo + telefono cellulare)** : si verifica quando un criterio di 2 controllo viene specificato e Mostra i due metodi hello tooauthentication utente richiesta di reimpostazione della password. |
| Risultato |**Operazione abbandonata**: l'utente ha iniziato l'operazione di reimpostazione delle password, ma l'ha interrotta senza completarla<p>**Bloccato** : l'account dell'utente è stato toouse ha impedito la reimpostazione a causa di pagina di reimpostazione password hello toouse tooattempting della password o una sola password reimpostazione gate troppe volte in un periodo di 24 ore<p>**Annullato** – utente avviata la reimpostazione della password, ma si è scelto di hello Annulla pulsante toocancel hello della sessione in <p>**Contattare l'amministratore** – utente presenta un problema durante la sessione che ha non è stato possibile risolvere, in modo utente hello fa clic sul collegamento "Contattare l'amministratore" hello anziché terminare un flusso di reimpostazione della password hello<p>**Non è stato possibile** : utente non è stato in grado di tooreset una password, probabilmente perché non è utente hello funzionalità hello toouse configurato (ad esempio, alcuna licenza, mancano informazioni di autenticazione, password è gestita in locale, ma il writeback non è disattivato).<p>**Operazione riuscita** – la reimpostazione della password è stata eseguita correttamente. |
| Dettagli |Vedere la tabella seguente |

### <a name="allowed-values-for-details-column"></a>Valori consentiti per la colonna dettagli
Di seguito è elenco hello di tipi di risultati che sarà probabilmente quando tramite password hello attività di reimpostazione:

| Dettagli | Tipo di risultato |
| --- | --- |
| Utente ha abbandonato dopo avere completato l'opzione di verifica tramite posta elettronica hello |Abbandonato |
| Utente ha abbandonato dopo avere completato l'opzione di verifica SMS cellulare hello |Abbandonato |
| Utente ha abbandonato dopo avere completato l'opzione di verifica tramite chiamata vocale mobili hello |Abbandonato |
| Utente ha abbandonato dopo avere completato l'opzione di verifica tramite chiamata vocale office hello |Abbandonato |
| Utente ha abbandonato dopo avere completato l'opzione di domande di sicurezza hello |Abbandonato |
| L'utente ha abbandonato dopo avere immesso il proprio ID utente. |Abbandonato |
| Utente ha abbandonato dopo avere avviato l'opzione di verifica tramite posta elettronica hello |Abbandonato |
| Utente ha abbandonato dopo avere avviato l'opzione di verifica SMS cellulare hello |Abbandonato |
| Utente ha abbandonato dopo avere avviato l'opzione di verifica tramite chiamata vocale mobili hello |Abbandonato |
| Utente ha abbandonato dopo avere avviato l'opzione di verifica tramite chiamata vocale office hello |Abbandonato |
| Utente ha abbandonato dopo avere avviato l'opzione di domande di sicurezza hello |Abbandonato |
| L'utente ha abbandonato prima di selezionare una nuova password. |Operazione abbandonata |
| L'utente ha abbandonato durante la selezione di una nuova password. |Operazione abbandonata |
| L'utente ha immesso troppi codici di verifica SMS non validi a e rimarrà bloccato per 24 ore. |Bloccato |
| L'utente ha superato il numero di tentativi consentiti per la verifica tramite chiamata vocale al telefono cellulare e rimarrà bloccato per 24 ore. |Bloccato |
| L'utente ha superato il numero di tentativi consentiti per la verifica tramite chiamata vocale al telefono dell'ufficio e rimarrà bloccato per 24 ore. |Bloccato |
| Utente ha tentato di troppe volte tooanswer domande di sicurezza e rimarrà bloccato per 24 ore |Bloccato |
| Utente ha tentato di troppe volte tooverify un numero di telefono e rimarrà bloccato per 24 ore |Bloccato |
| L'utente ha annullato prima di passare i metodi di autenticazione richiesto hello |Operazione annullata |
| L'utente ha annullato prima di inviare una nuova password. |Operazione annullata |
| L'utente ha contattato un amministratore dopo aver tentato l'opzione di verifica tramite posta elettronica hello |Amministratore contattato |
| L'utente ha contattato un amministratore dopo aver tentato l'opzione di verifica SMS cellulare hello |Amministratore contattato |
| L'utente ha contattato un amministratore dopo aver tentato l'opzione di verifica tramite chiamata vocale mobili hello |Amministratore contattato |
| L'utente ha contattato un amministratore dopo aver tentato l'opzione di verifica tramite chiamata vocale office hello |Amministratore contattato |
| L'utente ha contattato un amministratore dopo aver tentato l'opzione di verifica della domanda di sicurezza hello |Amministratore contattato |
| La reimpostazione della password non è abilitata per questo utente. Scheda tooresolve configurare questa impostazione abilita la reimpostazione in hello della password |Operazione non riuscita |
| All'utente non sono assegnate licenze. È possibile aggiungere questo un tooresolve utente toohello di licenza |Operazione non riuscita |
| L'utente ha tentato tooreset da un dispositivo senza i cookie abilitati |Operazione non riuscita |
| Il numero di metodi di autenticazione definito per l'account dell'utente non è sufficiente. Aggiungere questo elemento tooresolve informazioni di autenticazione |Operazione non riuscita |
| La password dell'utente è gestita in locale. È possibile abilitare questa tooresolve di writeback delle Password |Operazione non riuscita |
| Non è stato possibile raggiungere il servizio di reimpostazione della password locale. Verificare il log eventi del computer di sincronizzazione. |Operazione non riuscita |
| Si è verificato un problema durante la reimpostazione delle password locale dell'utente hello. Verificare il log eventi del computer di sincronizzazione. |Operazione non riuscita |
| Questo utente non è un membro del gruppo utenti di reimpostazione della password hello. Aggiungere questo tooresolve di gruppo toothat questo utente. |Operazione non riuscita |
| La reimpostazione della password è stata completamente disabilitata per questo tenant. Vedere [qui](http://aka.ms/ssprtroubleshoot) tooresolve questo. |Operazione non riuscita |
| La reimpostazione della password dell'utente è riuscita. |Operazione completata |

## <a name="next-steps"></a>Passaggi successivi
Di seguito sono collegamenti tooall di hello pagine della documentazione di reimpostazione della Password di Azure AD:

* **Se si sta visualizzando questa pagina perché si riscontrano problemi nell'accesso,** [seguire questa procedura per cambiare e reimpostare la password](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Come funziona** ](active-directory-passwords-how-it-works.md) -apprendere hello sei diversi componenti di servizio hello e ciò che ognuno di essi
* [**Guida introduttiva** ](active-directory-passwords-getting-started.md) -informazioni su come tooallow utenti tooreset e modificare le proprie password cloud o locale
* [**Personalizzare** ](active-directory-passwords-customize.md) - apprendere aspetto toocustomize hello e aspetto e il comportamento di hello tooyour esigenze del servizio
* [**Procedure consigliate** ](active-directory-passwords-best-practices.md) -informazioni su come tooquickly distribuire e gestire in modo efficace le password nell'organizzazione
* [**Domande frequenti su** ](active-directory-passwords-faq.md) -risposte toofrequently domande frequenti
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooquickly risolvere i problemi con il servizio hello
* [**Altre informazioni** ](active-directory-passwords-learn-more.md) : passare approfondita i dettagli tecnici di hello del funzionamento del servizio hello
