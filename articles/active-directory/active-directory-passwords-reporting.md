---
title: 'Creazione di rapporti: reimpostazione password self-service di Azure AD | Documentazione Microsoft'
description: Creazione di rapporti in reimpostazione self-service della password di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Opzioni di creazione di rapporti per la gestione delle password di Azure AD

Dopo la distribuzione, molte organizzazioni interessate tooknow come o se SSPR è effettivamente in uso. Azure AD fornisce funzionalità di reporting che consentono di domande tooanswer usando predefinito report e se la licenza in modo appropriato, consentono di query personalizzate toocreate.

Hello seguenti possono rispondere a domande da report esistenti in hello [portale] (https://portal.azure.com/).

> [!NOTE]
> È necessario essere [un amministratore globale](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) e deve acconsentire esplicitamente per questa toobe dati raccolti per conto dell'organizzazione, visita hello reporting tab o controllo registrati per almeno una volta. Fino a quel momento, i dati per l'organizzazione non verranno raccolti

* Quante persone si sono registrate per la reimpostazione delle password?
* Chi ha eseguito la registrazione per la reimpostazione delle password?
* Quali dati vengono registrati?
* Quante persone hanno reimpostato la password in hello negli ultimi sette giorni?
* Quali sono gli utenti metodi più comuni di hello o gli amministratori utilizzano tooreset le proprie password?
* Che cosa sono i comuni problemi faccia utenti o amministratori durante il tentativo di reimpostazione della password toouse?
* Con quale frequenza gli amministratori reimpostano le proprie password?
* Sono state rilevate eventuali attività sospette nell'ambito della reimpostazione delle password?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Come i report di gestione delle password tooview in hello portale di Azure

In hello esperienza del portale di Azure, è disponibile un modo migliore tooview reimpostazione e la password registrazione attività di reimpostazione password.  Seguire i passaggi di hello sotto toofind hello password reset e la password registrazione eventi di reimpostazione:

1. Passare troppo[**portal.azure.com**](https://portal.azure.com)
2. Fare clic su hello **più servizi** menu hello principale Azure portale navigazione a sinistra
3. Cercare **Azure Active Directory** in hello l'elenco dei servizi e selezionarlo
4. Fare clic su **utenti e gruppi** dal menu di navigazione di hello Azure Active Directory
5. Fare clic su hello **i log di controllo** elemento di navigazione hello utenti e gruppi di menu di navigazione. Verrà visualizzata tutti gli eventi di controllo hello effettuate verso tutti gli utenti di hello nella directory. È possibile filtrare questa toosee vista tutti hello password eventi correlati, nonché.
6. toofilter questa visualizzazione tooonly hello reimpostazione della password eventi correlati, fare clic su hello **filtro** pulsante nella parte superiore di hello del pannello hello.
7. Da hello **filtro** menu, seleziona hello **categoria** elenco a discesa e modificarlo toohello **la gestione delle Password Self-Service** tipo di categoria.
8. Elenco di hello facoltativamente ulteriore filtro scegliendo hello specifiche **attività** si è interessati

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>La modalità di hello tooretrieve gli eventi di gestione delle password da report di Azure AD API e gli eventi

i report di Hello Azure AD API e gli eventi supporta il recupero di tutte le informazioni incluse in password reset e la password reset registrazione report hello. Tramite questa API, è possibile scaricare la reimpostazione della password singoli e gli eventi di registrazione per l'integrazione di reimpostazione della password con hello reporting tecnologia di propria scelta.

### <a name="how-tooget-started-with-hello-reporting-api"></a>La modalità di avvio tooget con hello reporting API

tooaccess questi dati, è necessario toowrite un'app di piccole dimensioni o script tooretrieve dal server. [Informazioni su come iniziare tooget con hello API Azure AD Reporting](active-directory-reporting-api-getting-started.md).

Dopo aver creato uno script di lavoro, quindi è opportuno tooexamine hello password reimpostazione e registrazione degli eventi che è possibile recuperare toomeet gli scenari.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): Elenca le colonne di hello disponibili per gli eventi di reimpostazione della password
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): Elenca le colonne di hello disponibili per gli eventi di registrazione di reimpostazione della password

### <a name="reporting-api-data-retrieval-limitations"></a>Segnalazione dei limiti di recupero dati API

Attualmente, hello report di Azure AD e API eventi recupera backup troppo**75.000 singoli eventi** di hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) e [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) tipi , che si estende su hello **ultimi 30 giorni**.

Se è necessario tooretrieve o memorizzare dati oltre a questa finestra, è consigliabile salvarli in modo permanente in un database esterno e l'utilizzo delta di hello tooquery hello API risultanti. Il Consiglio è toobegin recupero dei dati, quando si inizia a usare SSPR nell'organizzazione, archiviarlo esternamente e proseguire delta hello tootrack da questo punto.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Reimpostazione della password di toodownload come eventi di registrazione rapidamente con PowerShell

Inoltre toousing hello report di Azure AD API e gli eventi direttamente, è inoltre possibile utilizzare hello di sotto di eventi di registrazione toorecent script PowerShell nella directory. Questo è utile nel caso in cui si desidera toosee che ha registrato recente o desidera che la password reimpostata implementazione tooensure avviene nel modo previsto.

* [Script di PowerShell per le attività di registrazione della reimpostazione della password self-service di Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Descrizione delle colonne del rapporto nel Portale di Azure

Hello elenco seguente viene spiegata ciascuna delle colonne del report hello in dettaglio:

* **Utente** : operazione di registrazione di reimpostazione utente hello che hanno tentato di una password.
* **Ruolo** : ruolo di hello di hello utente nella directory hello.
* **Data e ora** : hello data e ora del tentativo di hello.
* **Dati registrati** : registrazione di reimpostazione della quale utente hello dati di autenticazione fornito durante la password.

### <a name="description-of-report-values-in-azure-portal"></a>Descrizione dei valori del rapporto nel Portale di Azure

Hello nella tabella seguente vengono descritti hello diversi valori consentiti per ogni colonna:

| Colonna | Valori consentiti e relativi significati |
| --- | --- |
| Dati registrati |**Messaggio di posta elettronica alternativo** – tooauthenticate posta elettronica tramite posta elettronica o l'autenticazione alternativo utente<p><p>**Telefono ufficio**: office phone tooauthenticate utilizzato dall'utente<p>**Cellulare** -tooauthenticate telefono cellulare o di autenticazione utilizzato dall'utente<p>**Domande di sicurezza** – domande di sicurezza dell'utente utilizzato tooauthenticate<p>**Qualsiasi combinazione di hello sopra (ad esempio, posta elettronica alternativo + telefono cellulare)** : si verifica quando un criterio di 2 controllo viene specificato e Mostra i due metodi hello tooauthentication utente richiesta di reimpostazione della password. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Attività nel portale classico hello reimpostazione della password di visualizzazione

Questo report illustra tutti i tentativi di reimpostazione delle password che si sono verificati nell'organizzazione.

* **Intervallo di tempo massimo**: 30 giorni
* **Numero massimo di righe**: 75.000
* **Scaricabile**: Sì, tramite file CSV

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Descrizione delle colonne del rapporto nel Portale di Azure classico

Hello elenco seguente viene spiegata ciascuna delle colonne del report hello in dettaglio:

1. **Utente** : operazione (basato su campo di ID utente hello specificato quando l'utente hello proviene tooreset una password) per la reimpostazione utente hello che hanno tentato di una password.
2. **Ruolo** : ruolo di hello di hello utente nella directory hello.
3. **Data e ora** : hello data e ora del tentativo di hello.
4. **Metodi utilizzato** : i metodi di autenticazione hello utente utilizzato per questa operazione di reimpostazione.
5. **Risultato** : operazione di reimpostazione della password hello di risultato hello.
6. **Dettagli** : hello dettagli del motivo per cui la reimpostazione della password hello comportato valore hello.  Include anche eventuali passaggi che è possibile eseguire tooresolve un errore imprevisto.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Descrizione dei valori del rapporto nel Portale di Azure classico

Hello nella tabella seguente vengono descritti hello diversi valori consentiti per ogni colonna:

| Colonna | Valori consentiti e relativi significati |
| --- | --- |
| Metodi usati |**Messaggio di posta elettronica alternativo** – tooauthenticate posta elettronica tramite posta elettronica o l'autenticazione alternativo utente<p>**Telefono ufficio** : office phone tooauthenticate utilizzato dall'utente<p>**Cellulare** – tooauthenticate telefono cellulare o di autenticazione utilizzato dall'utente<p>**Domande di sicurezza** – domande di sicurezza dell'utente utilizzato tooauthenticate<p>**Qualsiasi combinazione di hello sopra (ad esempio, posta elettronica alternativo + telefono cellulare)** : si verifica quando un criterio di 2 controllo viene specificato e Mostra i due metodi hello tooauthentication utente richiesta di reimpostazione della password. |
| Risultato |**Operazione abbandonata**: l'utente ha iniziato l'operazione di reimpostazione delle password, ma l'ha interrotta senza completarla<p>**Bloccato** : l'account dell'utente è stato toouse ha impedito la reimpostazione a causa di pagina di reimpostazione password hello toouse tooattempting della password o una sola password reimpostazione gate troppe volte in un periodo di 24 ore<p>**Annullato** – utente avviata la reimpostazione della password, ma si è scelto di hello Annulla pulsante toocancel hello della sessione in <p>**Contattare l'amministratore** – utente presenta un problema durante la sessione che ha non è stato possibile risolvere, in modo utente hello fa clic sul collegamento "Contattare l'amministratore" hello anziché terminare un flusso di reimpostazione della password hello<p>**Non è stato possibile** : utente non è stato in grado di tooreset una password, probabilmente perché hello utente non è stato configurato toouse hello funzionalità (ad esempio, alcuna licenza, informazioni di autenticazione mancante, password gestita in locale, ma il writeback off).<p>**Operazione riuscita** – la reimpostazione della password è stata eseguita correttamente. |
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
| L'utente ha annullato prima di passare i metodi di autenticazione richiesto hello |Canceled |
| L'utente ha annullato prima di inviare una nuova password |Canceled |
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

## <a name="self-service-password-management-activity-types"></a>Tipi di attività di gestione delle password self-service

Hello seguenti tipi di attività vengono visualizzati in hello **la gestione delle Password Self-Service** categoria di eventi di controllo.  Segue una descrizione per ogni tipo.

* [**Impedito la reimpostazione della password self-service** ](#activity-type-blocked-from-self-service-password-reset) -indica un utente ha tentato tooreset una password, utilizzare un controllo specifico oppure convalidare un numero di telefono più di 5 volte totale nelle 24 ore.
* [**Modificare la password (Self-Service)** ](#activity-type-change-password-self-service) -indica un utente eseguita volontario o forzato (scadenza tooexpiry) la modifica della password.
* [**Reimpostazione della password (dall'amministratore)** ](#activity-type-reset-password-by-admin) -indica che un amministratore che ha eseguito una reimpostazione per conto dell'utente dal portale di Azure hello password.
* [**Reimpostazione della password (Self-Service)** ](#activity-type-reset-password-self-service) -indica che un utente è stata reimpostata la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com).
* [**Lo stato di avanzamento di flusso attività di reimpostazione della password self-service** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indica ogni passaggio specifico segua un utente (ad esempio, passando una password specifica, reimposta il controllo dell'autenticazione) come parte della password hello processo di reimpostazione.
* [**Sbloccare l'account utente (Self-Service)** ](#activity-type-unlock-user-account-self-service) -indica che un utente sbloccato il proprio account di Active Directory senza reimpostare la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com) utilizzando account di Active Directory Hello sbloccare senza funzionalità di reimpostazione.
* [**L'utente ha registrato per la reimpostazione della password self-service** ](#activity-type-user-registered-for-self-service-password-reset) -indica che un utente ha registrato tutti hello necessarie informazioni toobe tooreset in grado delle password in conformità hello attualmente specificati criteri di reimpostazione password del tenant.

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
* **Attività attore** -utente hello che ha modificato la password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello che ha modificato la password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Success_ (Operazione riuscita): indica che un utente ha modificato correttamente la propria password.
  * _Errore_ -indica che un utente non è stato possibile toochange la propria password. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Activity Status Failure Reason** - (Motivo dell'errore sullo stato dell'attività) 
  * _FuzzyPolicyViolationInvalidPassword_ -hello utente ha selezionato una password, che è stato escluso automaticamente a causa di funzionalità escluse rilevamento Password della tooMicrosoft ricerca toobe troppo comune o particolarmente vulnerabili.

### <a name="activity-type-reset-password-by-admin"></a>Tipo di attività: Reimpostare la password (amministratore)

Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un amministratore che ha eseguito una reimpostazione per conto dell'utente dal portale di Azure hello password.
* **Attività attore** -messaggio per l'amministratore che ha eseguito la reimpostazione per conto di un altro utente o amministratore della password hello. Deve essere un amministratore globale, un amministratore di password, un amministratore utenti o un amministratore supporto tecnico.
* **Destinazione attività** -utente hello la cui password è stata reimpostata. Può essere un utente finale o un altro amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Success_ (Operazione riuscita): indica che un amministratore ha reimpostato correttamente la password dell'utente.
  * _Errore_ -indica che un amministratore non è riuscito toochange password di un utente. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.

### <a name="activity-type-reset-password-self-service"></a>Tipo di attività: Reimpostare la password (self-service)

Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente è stata reimpostata la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com).
* **Attività attore** -utente hello Reimposta la password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello Reimposta la password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Success_ (Operazione riuscita): indica che un utente ha reimpostato correttamente la propria password.
  * _Errore_ -indica che un utente non è stato possibile tooreset la propria password. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Activity Status Failure Reason** - (Motivo dell'errore sullo stato dell'attività)
  * _FuzzyPolicyViolationInvalidPassword_ -salve selezionato di una password, che è stato escluso automaticamente a causa di funzionalità escluse rilevamento Password della tooMicrosoft ricerca toobe troppo comune o particolarmente vulnerabili.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Tipo di attività: Stato di avanzamento dell'attività di reimpostazione della password self-service

Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica di ogni passaggio specifico di un utente passa (ad esempio, passando una password specifica, reimposta il controllo dell'autenticazione) come parte della password hello processo di reimpostazione.
* **Attività attore** -flusso di reimpostazione utente hello che ha eseguito una parte della password hello. Può essere un utente finale o un amministratore.
* **Destinazione attività** -flusso di reimpostazione utente hello che ha eseguito una parte della password hello. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Esito positivo_ -indica un passaggio specifico del flusso di reimpostazione della password hello completata su un utente.
  * _Errore_ -indica un passaggio specifico di password hello reimpostato flusso non è riuscito. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.
* **Allowed Activity Status Reasons** (Motivi degli stati attività consentite)
  * Vedere la tabella seguente per [tutti i motivi degli stati relativi alle attività di reimpostazione consentite](#allowed-values-for-details-column).

### <a name="activity-type-unlock-user-account-self-service"></a>Tipo di attività: Sbloccare l'account utente (self-service)

Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente sbloccato il proprio account di Active Directory senza reimpostare la password da hello [portale di reimpostazione della Password di Azure AD](https://passwordreset.microsoftonline.com) utilizzando hello AD account sbloccare senza reimpostazione funzionalità.
* **Attività attore** -utente hello sbloccato il proprio account senza reimpostare la password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utente hello sbloccato il proprio account senza reimpostare la password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Success_ (Operazione riuscita): indica che un utente ha sbloccato correttamente il proprio account.
  * _Errore_ -indica che un utente non è stato possibile toounlock il proprio account. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Tipo di attività: Utente registrato per la reimpostazione della password self-service

Hello seguente elenco descrive questa attività in modo dettagliato:

* **Descrizione attività** : indica che un utente ha registrato tutti hello necessarie informazioni toobe tooreset in grado delle password in conformità hello attualmente specificati criteri di reimpostazione password del tenant. 
* **Attività attore** -utenti hello registrati per la reimpostazione della password. Può essere un utente finale o un amministratore.
* **Destinazione attività** -utenti hello registrati per la reimpostazione della password. Può essere un utente finale o un amministratore.
* **Allowed Activity Statuses** (Stati attività consentite)
  * _Esito positivo_ -indica un utente registrato per la reimpostazione in base ai criteri correnti hello della password. 
  * _Errore_ -indica un tooregister utente non è riuscita per la reimpostazione della password. Facendo clic su riga hello consente hello toosee **motivo dello stato attività** toolearn categoria informazioni sul motivo per cui si è verificato un errore di hello. Nota: questo non significa un utente è Impossibile tooreset la propria password, solo che non ha completato il processo di registrazione hello. Se sono presenti dati non verificati il proprio account corretto (ad esempio un numero di telefono non viene convalidato), anche se essi non verificato il numero di telefono, è comunque possibile utilizzarla tooreset la propria password. Per altre informazioni, vedere [Cosa accade quando un utente si registra?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [Log di controllo di gestione di scelta rapida toouser](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - andare direttamente i log di controllo di gestione di utenti del tenant tooyour
* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
