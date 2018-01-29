---
title: Risoluzione dei problemi relativi alla reimpostazione della password self-service - Azure Active Directory
description: Risolvere i problemi di reimpostazione della password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2018
ms.author: joflore
ms.custom: it-pro;seohack1
ms.openlocfilehash: c038a9ec682a5971a5f79b9fe36e667493702cbd
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="troubleshoot-self-service-password-reset"></a>Risolvere i problemi di reimpostazione della password self-service

In caso di problemi di reimpostazione della password self-service in Azure Active Directory (Azure AD), le informazioni seguenti possono aiutare a ripristinare il corretto funzionamento.

## <a name="troubleshoot-self-service-password-reset-errors-that-a-user-might-see"></a>Risolvere i problemi di reimpostazione della password self-service visualizzati dall'utente

| Tipi di errore | Dettagli | Dettagli tecnici |
| --- | --- | --- |
| TenantSSPRFlagDisabled = 9 | Non è possibile reimpostare la password in questo momento perché l'amministratore ha disabilitato la reimpostazione delle password per l'organizzazione. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e chiedere di abilitare questa funzionalità. Per altre informazioni, vedere [Password di Azure AD dimenticata](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password#common-problems-and-their-solutions). | SSPR_0009: è stato rilevato che la reimpostazione della password non è stata abilitata dall'amministratore. Contattare l'amministratore e richiedere l'abilitazione della reimpostazione delle password per l'organizzazione. |
| WritebackNotEnabled = 10 |Non è possibile reimpostare la password in questo momento perché l'amministratore non ha abilitato un servizio necessario per l'organizzazione. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e chiedere di controllare la configurazione dell'organizzazione. Per altre informazioni su questo servizio necessario, vedere [Configurare il writeback delle password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-writeback#configure-password-writeback). | SSPR_0010: è stato rilevato che il writeback delle password non è abilitato. Contattare l'amministratore e richiedere l'abilitazione del writeback delle password. |
| SsprNotEnabledInUserPolicy = 11 | Non è possibile reimpostare la password in questo momento perché l'amministratore non ha configurato la reimpostazione delle password per l'organizzazione. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e richiedere la configurazione della reimpostazione della password. Per altre informazioni sulla configurazione della reimpostazione della password, vedere [Guida introduttiva: Reimpostazione della password self-service di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started). | SSPR_0011: L'organizzazione non ha definito criteri di reimpostazione della password. Contattare l'amministratore e chiedere di definire i criteri di reimpostazione della password. |
| UserNotLicensed = 12 | Non è possibile reimpostare la password in questo momento perché alcune licenze necessarie non sono presenti nell'organizzazione. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e richiedere una verifica delle assegnazioni delle licenze. Per altre informazioni sulle licenze, vedere [Requisiti di licenza per la reimpostazione password self-service di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-licensing). | SSPR_0012: L'organizzazione non ha le licenze necessarie per la reimpostazione della password. Contattare l'amministratore e richiedere una verifica delle assegnazioni delle licenze. |
| UserNotMemberOfScopedAccessGroup = 13 | Non è possibile reimpostare la password in questo momento perché l'amministratore non ha configurato l'account per l'uso della reimpostazione della password. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e chiedere di configurare l'account per la reimpostazione della password. Per altre informazioni sulla configurazione dell'account per la reimpostazione della password, vedere [Implementare la reimpostazione della password per gli utenti](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-best-practices). | SSPR_0012: Non si è membri di un gruppo abilitato per la reimpostazione della password. Contattare l'amministratore e richiedere di essere aggiunti al gruppo. |
| UserNotProperlyConfigured = 14 | Non è possibile reimpostare la password in questo momento perché l'account non include alcune informazioni necessarie. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e chiedergli di reimpostare la password. Dopo avere recuperato l'accesso all'account, è necessario registrare le informazioni necessarie. Per registrare le informazioni, seguire i passaggi nell'articolo [Eseguire la registrazione per la reimpostazione password self-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-reset-register). | SSPR_0014: Per reimpostare la password sono necessarie informazioni di sicurezza aggiuntive. Per procedere, contattare l'amministratore e chiedergli di reimpostare la password. Dopo avere recuperato l'accesso all'account, è possibile registrare informazioni di sicurezza aggiuntive all'indirizzo https://aka.ms/ssprsetup. L'amministratore può aggiungere altre informazioni di sicurezza all'account seguendo la procedura illustrata in [Impostare e leggere i dati di autenticazione per la reimpostazione della password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-data#set-and-read-authentication-data-using-powershell). |
| OnPremisesAdminActionRequired = 29 | Non è possibile reimpostare la password in questo momento a causa di un problema con la configurazione della reimpostazione delle password dell'organizzazione. Non c'è alcuna azione aggiuntiva da eseguire per risolvere questa situazione. Contattare l'amministratore e chiedere di esaminare la situazione. Per altre informazioni sul problema potenziale, vedere [Risolvere i problemi relativi al writeback delle password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback). | SSPR_0029: Non è possibile reimpostare la password a causa di un errore nella configurazione locale. Contattare l'amministratore e chiedere di esaminare la situazione. |
| OnPremisesConnectivityError = 30 | Non è possibile reimpostare la password in questo momento a causa di problemi di connettività con l'organizzazione. Non è necessario eseguire alcuna azione in questo momento, ma è possibile che il problema risulti risolto se si prova più tardi. Se il problema persiste, contattare l'amministratore e chiedere di esaminare la situazione. Per altre informazioni sui problemi di connettività, vedere [Risolvere i problemi relativi alla connettività di writeback della password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback-connectivity). | SSPR_0030: non è possibile reimpostare la password a causa di una connessione di qualità scadente con l'ambiente locale. Contattare l'amministratore e richiedere una verifica.|


## <a name="troubleshoot-the-password-reset-configuration-in-the-azure-portal"></a>Risolvere problemi relativi alla configurazione della funzione di reimpostazione della password nel portale di Azure

| Tipi di errore | Soluzione |
| --- | --- |
| Non viene visualizzata la sezione **Reimpostazione password** in Azure AD nel portale di Azure. | Questo problema può verificarsi se all'amministratore che esegue l'operazione non è stata assegnata una licenza di Azure AD Premium o Basic. <br> <br> Assegnare una licenza all'account amministratore in questione. È possibile seguire i passaggi illustrati nell'articolo [Assegnare e verificare le licenze e risolvere i relativi problemi](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses).|
| Non è possibile visualizzare un'opzione di configurazione specifica. | Molti elementi dell'interfaccia utente rimangono nascosti finché non sono necessari. Provare ad abilitare tutte le opzioni che si desidera visualizzare. |
| Non possibile visualizzare la scheda **Integrazione locale**. | Questa opzione è visibile solo se è stato scaricato Azure AD Connect ed è stata eseguita la configurazione del writeback delle password. Per altre informazioni, vedere [Introduzione alle impostazioni rapide per Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md). |

## <a name="troubleshoot-password-reset-reporting"></a>Risolvere i problemi di segnalazione relativi alla reimpostazione della password

| Tipi di errore | Soluzione |
| --- | --- |
| Nella categoria degli eventi di controllo **Self-Service Password Management** (Gestione delle password self-service) non viene visualizzato alcun tipo di attività di gestione della password. | Questo problema può verificarsi se all'amministratore che esegue l'operazione non è stata assegnata una licenza di Azure AD Premium o Basic. <br> <br> Per risolvere il problema, assegnare una licenza all'account amministratore in questione. Seguire i passaggi illustrati nell'articolo [Assegnare e verificare le licenze e risolvere i relativi problemi](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses). |
| Le registrazioni utente vengono visualizzate più volte. | Attualmente, quando un utente effettua la registrazione, ogni singolo dato inserito viene registrato come un evento distinto. <br> <br> Per aggregare i dati e avere più flessibilità nelle modalità di visualizzazione, è possibile scaricare il report e aprire i dati come tabella pivot in Excel.

## <a name="troubleshoot-the-password-reset-registration-portal"></a>Risolvere i problemi relativi al portale di registrazione per la reimpostazione della password

| Tipi di errore | Soluzione |
| --- | --- |
| La directory non è abilitata per la reimpostazione della password. **L'amministratore non ha abilitato l'utente all'uso di questa funzionalità.** | Impostare il flag **Reimpostazione password self-service abilitata** su **Selezionato** o **Tutto** e quindi fare clic su **Salva**. |
| All'utente non è stata assegnata una licenza di Azure AD Premium o Basic. **L'amministratore non ha abilitato l'utente all'uso di questa funzionalità.** | Questo problema può verificarsi se all'amministratore che esegue l'operazione non è stata assegnata una licenza di Azure AD Premium o Basic. <br> <br> Per risolvere il problema, assegnare una licenza all'account amministratore in questione. Seguire i passaggi illustrati nell'articolo [Assegnare e verificare le licenze e risolvere i relativi problemi](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses).|
| Si è verificato un errore durante l'elaborazione della richiesta. | Questo errore può essere causato da molti problemi, ma in genere è dovuto a un'interruzione del servizio o a un problema di configurazione. Se l'errore si verifica e ha un impatto sull'attività aziendale, contattare il supporto tecnico Microsoft per assistenza. |

## <a name="troubleshoot-the-password-reset-portal"></a>Risolvere i problemi relativi al portale di reimpostazione della password

| Tipi di errore | Soluzione |
| --- | --- |
| La directory non è abilitata per la reimpostazione della password. | Impostare il flag **Reimpostazione password self-service abilitata** su **Selezionato** o **Tutto** e quindi fare clic su **Salva**. |
| All'utente non è stata assegnata una licenza di Azure AD Premium o Basic. | Questo problema può verificarsi se all'amministratore che esegue l'operazione non è stata assegnata una licenza di Azure AD Premium o Basic. <br> <br> Per risolvere il problema, assegnare una licenza all'account amministratore in questione. Seguire i passaggi illustrati nell'articolo [Assegnare e verificare le licenze e risolvere i relativi problemi](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses). |
| La directory è abilitata per la reimpostazione della password, ma le informazioni di autenticazione dell'utente sono mancanti o errate. | Prima di procedere, verificare che i dati di contatto dell'utente archiviati nella directory siano corretti. Per altre informazioni, vedere l'articolo relativo ai [dati usati per la reimpostazione password self-service di Azure AD](active-directory-passwords-data.md). |
| La directory è abilitata per la reimpostazione della password, ma per l'utente è archiviato un solo metodo di contatto mentre i criteri sono impostati in modo da richiedere due metodi di verifica. | Prima di procedere, verificare che per l'utente siano configurati correttamente almeno due metodi di contatto. Sono ad esempio necessari un numero di telefono cellulare *e* un numero di telefono dell'ufficio. |
| La directory è abilitata per la reimpostazione della password, ma non è possibile contattare l'utente anche se questo è configurato correttamente. | Questo errore può essere causato da un problema temporaneo del servizio o da dati di contatto errati che non sono stati rilevati correttamente. <br> <br> Se l'utente attende 10 secondi, vengono visualizzati i collegamenti per riprovare o per contattare l'amministratore. Se l'utente sceglie di riprovare, viene eseguito un nuovo tentativo di chiamata. Se l'utente sceglie di contattare l'amministratore, viene inviato un modulo di posta elettronica agli amministratori in cui viene richiesto di eseguire la reimpostazione della password per l'account utente. |
| L'utente non riceve mai un SMS o una telefonata per la reimpostazione della password. | Questo errore può essere causato da un numero di telefono non corretto nella directory. Verificare che il numero di telefono sia nel formato "+ccc xxxyyyzzzzXeeee". <br> <br> La reimpostazione della password non supporta gli interni, anche se vengono specificati nella directory. Gli interni vengono rimossi prima dell'invio della chiamata. Usare un numero senza interno o integrare l'interno nel numero di telefono nel proprio centralino (PBX). |
| L'utente non riceve mai il messaggio di posta elettronica relativo alla reimpostazione della password. | La causa più comune di questo problema è il rifiuto del messaggio da parte di un filtro protezione da posta indesiderata. Cercare il messaggio di posta elettronica nella cartella della posta indesiderata o della posta eliminata. <br> <br> Assicurarsi anche di cercare il messaggio nell'account di posta elettronica corretto. |
| Sono stati impostati criteri di reimpostazione della password, ma quando la funzionalità viene usata con un account amministratore i criteri non vengono applicati. | Microsoft gestisce e controlla i criteri di reimpostazione delle password amministratore per assicurare il massimo livello di sicurezza. |
| All'utente viene impedito di provare a reimpostare la password troppe volte in uno stesso giorno. | Per impedire agli utenti di provare a reimpostare le password troppe volte in un breve intervallo di tempo, viene applicato un meccanismo di limitazione automatico. Il meccanismo viene applicato quando: <br><ul><li>L'utente cerca di convalidare un numero di telefono cinque volte in un'ora.</li><li>L'utente cerca di usare il controllo per le domande di sicurezza cinque volte in un'ora.</li><li>L'utente cerca di reimpostare una password per lo stesso account utente cinque volte in un'ora.</li></ul>Per risolvere il problema, chiedere all'utente di attendere 24 ore dopo l'ultimo tentativo. A quel punto, sarà possibile reimpostare la password. |
| L'utente visualizza un errore quando convalida il numero di telefono. | Questo errore si verifica quando il numero di telefono immesso non corrisponde a quello archiviato. Assicurarsi che l'utente immetta il numero di telefono completo, inclusi il prefisso internazionale e locale, quando cerca di usare un metodo basato sul telefono per la reimpostazione della password. |
| Si è verificato un errore durante l'elaborazione della richiesta. | Questo errore può essere causato da molti problemi, ma in genere è dovuto a un'interruzione del servizio o a un problema di configurazione. Se l'errore si verifica e ha un impatto sull'attività aziendale, contattare il supporto tecnico Microsoft per assistenza. |

## <a name="troubleshoot-password-writeback"></a>Risolvere i problemi relativi al writeback delle password

| Tipi di errore | Soluzione |
| --- | --- |
| Il servizio di reimpostazione della password non si avvia in locale. Viene visualizzato l'errore 6800 nel log eventi dell'applicazione del computer che esegue Azure AD Connect. <br> <br> Dopo l'onboarding, gli utenti federati o con sincronizzazione di hash della password non possono reimpostare le password. | Quando il writeback delle password è abilitato, il motore di sincronizzazione chiama la libreria di writeback per eseguire la configurazione, ovvero l'onboarding, comunicando con il servizio di onboarding cloud. Gli eventuali errori che si verificano durante l'onboarding o durante l'avvio dell'endpoint Windows Communication Foundation (WCF) per il writeback delle password si riflettono nel log eventi del computer che esegue Azure AD Connect. <br> <br> Se è stato configurato il writeback, durante il riavvio del servizio Azure AD Sync (ADSync) viene avviato l'endpoint WCF. Se tuttavia l'avvio dell'endpoint non riesce, il servizio di sincronizzazione viene avviato e viene registrato l'evento 6800. La presenza di questo evento indica che l'endpoint di writeback delle password non è stato avviato. I dettagli del log per questo evento 6800 insieme alle voci del log eventi generate dal componente PasswordResetService indicano i motivi per cui non è possibile avviare l'endpoint. Esaminare gli errori nel log eventi e provare a riavviare Azure AD Connect se il writeback delle password continua a non funzionare. Se il problema persiste, provare a disabilitare e quindi riabilitare il writeback delle password.
| Quando un utente prova a reimpostare una password o a sbloccare un account con il writeback delle password abilitato, l'operazione non riesce. <br> <br> Dopo l'esecuzione dell'operazione di sblocco, nel log eventi di Azure AD Connect viene inoltre visualizzato un evento simile a: "Il motore di sincronizzazione ha restituito un errore hr=800700CE, messaggio=Il nome o l'estensione del file sono troppo lunghi". | Trovare l'account di Active Directory per Azure AD Connect e reimpostare la password in modo che non contenga più di 127 caratteri. Aprire quindi **Synchronization Service** dal menu **Start**. Passare a **Connettori** e trovare **Active Directory Connector**. Selezionare il connettore e quindi **Proprietà**. Passare alla pagina **Credenziali** e immettere la nuova password. Fare clic su **OK** per chiudere la pagina. |
| Nell'ultimo passaggio del processo di installazione di Azure AD Connect viene visualizzato un errore che indica che non è stato possibile configurare il writeback delle password. <br> <br> Il log eventi dell'applicazione Azure AD Connect contiene l'errore 32009 il cui testo indica che non è stato possibile recuperare il token di autenticazione. | Questo errore si verifica nei due casi seguenti: <br><ul><li>È stata specificata una password non corretta per l'account amministratore globale specificato all'inizio del processo di installazione di Azure AD Connect.</li><li>È stato eseguito un tentativo di usare un utente federato per l'account amministratore globale specificato all'inizio del processo di installazione di Azure AD Connect.</li></ul> Per risolvere il problema, accertarsi di non usare un account federato per l'amministratore globale specificato all'inizio del processo di installazione. Verificare anche che la password specificata sia corretta. |
| Il log eventi del computer che esegue Azure AD Connect contiene l'errore 32002 generato eseguendo PasswordResetService. <br> <br> Il messaggio indica "Errore durante la connessione a Bus di servizio. Il provider di token non è stato in grado di fornire un token di sicurezza." | L'ambiente locale non è in grado di connettersi all'endpoint del bus di servizio di Azure nel cloud. Questo errore è in genere causato da una regola del firewall che blocca la connessione in uscita a una porta o a un indirizzo Web specifico. Per altre informazioni, vedere i [prerequisiti di connettività](./connect/active-directory-aadconnect-prerequisites.md). Dopo avere aggiornato queste regole, riavviare il computer che esegue Azure AD Connect. Il writeback delle password dovrebbe funzionare di nuovo. |
| Dopo un certo periodo di tempo, gli utenti federati o con sincronizzazione di hash della password non possono reimpostare le password. | In rari casi è possibile che il servizio di writeback delle password non venga riavviato quando si riavvia Azure AD Connect. In questi casi controllare prima di tutto se il writeback delle password è abilitato in locale. A tale scopo, è possibile usare la procedura guidata di Azure AD Connect o PowerShell (vedere la sezione precedente relativa alle procedure). Se la funzionalità appare abilitata, provare ad abilitarla o a disabilitarla di nuovo tramite l'interfaccia utente o PowerShell. Se il problema persiste, provare a disinstallare completamente e a reinstallare Azure AD Connect. |
| Gli utenti federati o con sincronizzazione di hash della password che cercano di reimpostare le password visualizzano un errore dopo l'invio della password. L'errore indica che si è verificato un problema del servizio. <br ><br> Oltre a questo problema, durante le operazioni di reimpostazione della password è possibile che venga visualizzato un errore di accesso negato per l'agente di gestione nei log eventi locali. | Se nel log eventi sono presenti errori di questo tipo, verificare che l'account Active Directory Management Agent (ADMA) specificato nella procedura guidata al momento della configurazione abbia le autorizzazioni necessarie per il writeback delle password. <br> <br> Si noti che dopo aver concesso l'autorizzazione, la relativa propagazione tramite l'attività in background `sdprop` nel controller di dominio può richiedere fino a un'ora. <br> <br> Per il funzionamento della reimpostazione della password, è necessario che l'autorizzazione sia indicata nel descrittore di sicurezza dell'oggetto utente per il quale viene reimpostata la password. Finché l'autorizzazione non sarà indicata nell'oggetto utente, per la reimpostazione della password continuerà a verificarsi un errore con un messaggio di accesso negato. |
| Gli utenti federati o con sincronizzazione di hash della password che cercano di reimpostare le password visualizzano un errore dopo l'invio della password. L'errore indica che si è verificato un problema del servizio. <br> <br> Durante le operazioni di reimpostazione della password, è inoltre possibile che venga visualizzato un errore nei log eventi del servizio Azure AD Connect che indica che non è stato possibile trovare l'oggetto. | Questo errore indica di solito che il motore di sincronizzazione non è in grado di trovare l'oggetto utente nello spazio connettore di Azure AD o nell'oggetto spazio connettore di Azure AD o metaverse (MV) collegato. <br> <br> Per risolvere il problema, assicurarsi che l'utente sia effettivamente sincronizzato dall'ambiente locale ad Azure AD tramite l'istanza corrente di Azure AD Connect e controllare lo stato degli oggetti negli spazi connettore e nell'oggetto MV. Verificare che l'oggetto Servizi certificati Active Directory sia connesso all'oggetto MV tramite la regola "Microsoft.InfromADUserAccountEnabled.xxx".|
| Gli utenti federati o con sincronizzazione di hash della password che cercano di reimpostare le password visualizzano un errore dopo l'invio della password. L'errore indica che si è verificato un problema del servizio. <br> <br> In aggiunta a questo problema, durante le operazioni di reimpostazione della password, è possibile che venga visualizzato un errore nei log eventi del servizio Azure AD Connect che indica che sono state trovate più corrispondenze. | Ciò indica che il motore di sincronizzazione ha rilevato che l'oggetto MV è connesso a più oggetti Servizi certificati Active Directory tramite "Microsoft.InfromADUserAccountEnabled.xxx". Questo significa che l'utente dispone di un account abilitato in più foreste. Si noti che questo scenario non è supportato per il writeback delle password. |
| Le operazioni con le password non riescono a causa di un errore di configurazione. Il log eventi dell'applicazione contiene l'errore 6329 di Azure AD Connect con un testo simile al seguente: 0x8023061f (Operazione non riuscita perché la sincronizzazione della password non è abilitata in questo agente di gestione). | L'errore si verifica se si modifica la configurazione di Azure AD Connect per aggiungere una nuova foresta di Active Directory (o per rimuovere e aggiungere di nuovo una foresta esistente) dopo aver abilitato la funzionalità di writeback delle password. Le operazioni con le password per gli utenti in queste foreste aggiunte di recente hanno esito negativo. Per risolvere il problema, disabilitare e riabilitare la funzionalità di writeback delle password dopo avere completato le modifiche alla configurazione della foresta. |

## <a name="password-writeback-event-log-error-codes"></a>Codici di errore del log eventi di writeback delle password

Una procedura consigliata per la risoluzione dei problemi relativi al writeback delle password consiste nell'esaminare il log eventi dell'applicazione nel computer che esegue Azure AD Connect. Questo log contiene gli eventi di due origini di interesse per il writeback delle password. L'origine PasswordResetService descrive le operazioni e i problemi correlati all'operazione di writeback delle password. L'origine ADSync descrive le operazioni e i problemi correlati all'impostazione delle password nell'ambiente Active Directory.

### <a name="if-the-source-of-the-event-is-adsync"></a>Se l'origine dell'evento è ADSync

| Codice | Nome o messaggio | DESCRIZIONE |
| --- | --- | --- |
| 6329 | BAIL: MMS(4924) 0x80230619 - Una restrizione impedisce la modifica della password in quella corrente specificata. | Questo evento si verifica quando il servizio di writeback delle password cerca di impostare una password nella directory locale che non soddisfa i requisiti di validità, cronologia, complessità o filtro del dominio. <br> <br> Se è prevista una validità minima della password e di recente la password è stata modificata in tale intervallo di tempo, non sarà possibile modificarla di nuovo finché non si raggiunge il periodo di validità specificato nel dominio. A scopo di test, è consigliabile impostare la validità minima su 0. <br> <br> Se sono abilitati i requisiti per la cronologia delle password, sarà necessario selezionare una password che non sia stata usata nelle ultime *N* volte, dove *N* è l'impostazione relativa alla cronologia delle password. Se si seleziona una password che è stata usata nelle ultime *N* volte, si verifica un errore. A scopo di test, è consigliabile impostare la cronologia delle password su 0. <br> <br> Se abilitati, tutti i requisiti di complessità della password vengono applicati quando l'utente tenta di modificare o reimpostare la password. <br> <br> Se sono abilitati i filtri delle password e un utente sceglie una password che non soddisfa i criteri di filtro, l'operazione di reimpostazione o di modifica non riuscirà. |
| 6329 | MMS(3040): admaexport.cpp(2837): il server non contiene il controllo dei criteri della password LDAP. | Questo problema si verifica se il controllo LDAP_SERVER_POLICY_HINTS_OID (1.2.840.113556.1.4.2066) non è abilitato nei controller di dominio. Per usare la funzionalità di writeback delle password, è necessario abilitare il controllo. A tale scopo, i controller di dominio devono essere in Windows Server 2008 (con Service Pack più recente) o versioni successive. Se i controller di dominio sono nella versione 2008, precedente a R2, è necessario applicare anche l'[hotfix KB2386717](http://support.microsoft.com/kb/2386717). |
| HR 8023042 | Il motore di sincronizzazione ha restituito un errore hr = 80230402, messaggio = Tentativo di ottenere un oggetto non riuscito. Sono presenti voci duplicate con lo stesso ancoraggio. | Questo errore si verifica quando lo stesso ID utente è abilitato in più domini. Ad esempio, se si esegue la sincronizzazione di foreste di risorse e account e lo stesso ID utente è presente e abilitato in ogni foresta. <br> <br> Questo errore può verificarsi anche se si usa un attributo di ancoraggio non univoco (come un alias o UPN) e due utenti condividono lo stesso attributo di ancoraggio. <br> <br> Per risolvere questo problema, assicurarsi che non ci siano utenti duplicati nei domini e di usare un attributo di ancoraggio univoco per ogni utente. |

### <a name="if-the-source-of-the-event-is-passwordresetservice"></a>Se l'origine dell'evento è PasswordResetService

| Codice | Nome o messaggio | DESCRIZIONE |
| --- | --- | --- |
| 31001 | PasswordResetStart | Questo evento indica che il servizio locale ha rilevato una richiesta di reimpostazione della password per un utente federato o con sincronizzazione di hash della password originata dal cloud. Si tratta del primo evento di ogni operazione di writeback per la reimpostazione della password. |
| 31002 | PasswordResetSuccess | Questo evento indica che un utente ha selezionato una nuova password durante un'operazione di reimpostazione della password. È stato determinato che la password soddisfa i requisiti aziendali per le password. La password è stata scritta correttamente nell'ambiente Active Directory locale. |
| 31003 | PasswordResetFail | Questo evento indica che un utente ha selezionato una password che è pervenuta correttamente all'ambiente locale. Quando però è stato eseguito un tentativo di impostare la password nell'ambiente Active Directory locale, si è verificato un errore. Questo problema può verificarsi per diversi motivi: <br><ul><li>La password dell'utente non soddisfa i requisiti di validità, cronologia, complessità o filtro per il dominio. Per risolvere il problema, creare una nuova password.</li><li>L'account del servizio ADMA non ha le autorizzazioni appropriate per impostare la nuova password nell'account utente in questione.</li><li>L'account utente appartiene a un gruppo protetto, ad esempio il gruppo di amministratori di dominio o dell'organizzazione, che non consente operazioni di impostazione delle password.</li></ul>|
| 31004 | OnboardingEventStart | Questo evento si verifica se si abilita il writeback delle password con Azure AD Connect ed è stato avviato l'onboarding dell'organizzazione nel servizio Web di writeback delle password. |
| 31005 | OnboardingEventSuccess | Questo evento indica che il processo di onboarding è stato completato e che la funzionalità di writeback delle password è pronta per l'uso. |
| 31006 | ChangePasswordStart | Questo evento indica che il servizio locale ha rilevato una richiesta di modifica della password per un utente federato o con sincronizzazione di hash della password originata dal cloud. Si tratta del primo evento di ogni operazione di writeback per la modifica della password. |
| 31007 | ChangePasswordSuccess | Questo evento indica che un utente ha selezionato una nuova password durante un'operazione di modifica della password, è stato determinato che la password soddisfa i requisiti aziendali e la password è stata scritta correttamente nell'ambiente Active Directory locale. |
| 31008 | ChangePasswordFail | Questo evento indica che un utente ha selezionato una password che è pervenuta correttamente all'ambiente locale, ma quando si è cercato di impostare la password nell'ambiente Active Directory locale si è verificato un errore. Questo problema può verificarsi per diversi motivi: <br><ul><li>La password dell'utente non soddisfa i requisiti di validità, cronologia, complessità o filtro per il dominio. Per risolvere il problema, creare una nuova password.</li><li>L'account del servizio ADMA non ha le autorizzazioni appropriate per impostare la nuova password nell'account utente in questione.</li><li>L'account dell'utente appartiene a un gruppo protetto, ad esempio Domain Admins o Enterprise Admins, che non consente operazioni di impostazione delle password.</li></ul> |
| 31009 | ResetUserPasswordByAdminStart | Il servizio locale ha rilevato una richiesta di reimpostazione della password per un utente federato o con sincronizzazione di hash della password originata dall'amministratore per conto di un utente. Si tratta del primo evento di ogni operazione di writeback per la reimpostazione della password avviata da un amministratore. |
| 31010 | ResetUserPasswordByAdminSuccess | L'amministratore ha selezionato una nuova password durante un'operazione di reimpostazione della password avviata dall'amministratore. È stato determinato che la password soddisfa i requisiti aziendali per le password. La password è stata scritta correttamente nell'ambiente Active Directory locale. |
| 31011 | ResetUserPasswordByAdminFail | L'amministratore ha selezionato una password per conto dell'utente. La password è pervenuta correttamente all'ambiente locale. Quando però è stato eseguito un tentativo di impostare la password nell'ambiente Active Directory locale, si è verificato un errore. Questo problema può verificarsi per diversi motivi: <br><ul><li>La password dell'utente non soddisfa i requisiti di validità, cronologia, complessità o filtro per il dominio. Per risolvere il problema, provare a usare una nuova password.</li><li>L'account del servizio ADMA non ha le autorizzazioni appropriate per impostare la nuova password nell'account utente in questione.</li><li>L'account dell'utente appartiene a un gruppo protetto, ad esempio Domain Admins o Enterprise Admins, che non consente operazioni di impostazione delle password.</li></ul>  |
| 31012 | OffboardingEventStart | Questo evento si verifica se si disabilita il writeback delle password con Azure AD Connect e indica che è stato avviato l'offboarding dell'organizzazione nel servizio Web di writeback delle password. |
| 31013| OffboardingEventSuccess| Questo evento indica che il processo di offboarding è stato completato e che la funzionalità di writeback delle password è stata disabilitata. |
| 31014| OffboardingEventFail| Questo evento indica che il processo di offboarding non è riuscito. La causa può essere legata a un errore di autorizzazioni nel cloud oppure a un account amministratore locale specificato durante la configurazione. L'errore può verificarsi anche se si sta cercando di usare un amministratore globale cloud federato quando si disabilita il writeback delle password. Per risolvere il problema, controllare le autorizzazioni amministrative e verificare che non sia in uso un account federato durante la configurazione della funzionalità di writeback delle password.|
| 31015| WriteBackServiceStarted| Questo evento indica che il servizio di writeback delle password è stato avviato correttamente. Il servizio è pronto ad accettare le richieste di gestione delle password dal cloud.|
| 31016| WriteBackServiceStopped| Questo evento indica che il servizio di writeback delle password è stato arrestato. Qualsiasi richiesta di gestione delle password dal cloud avrà esito negativo.|
| 31017| AuthTokenSuccess| Questo evento indica l'operazione di recupero di un token di autorizzazione per l'amministratore globale specificato durante l'installazione di Azure AD Connect per avviare il processo di scaricamento o caricamento è stata eseguita correttamente.|
| 31018| KeyPairCreationSuccess| Questo evento indica che la chiave di crittografia delle password è stata creata correttamente. La chiave verrà usata per crittografare le password cloud da inviare all'ambiente locale.|
| 32000| UnknownError| Questo evento indica che si è verificato un errore sconosciuto durante un'operazione di gestione delle password. Per altri dettagli, fare riferimento al testo dell'eccezione. In caso di problemi, provare a disabilitare e quindi riabilitare il writeback delle password. Se il problema persiste, includere una copia del log eventi e le informazioni interne specificate nell'ID di traccia da inviare al personale del supporto tecnico.|
| 32001| ServiceError| Questo evento indica che si è verificato un errore di connessione al servizio cloud di reimpostazione delle password. L'errore si verifica in genere quando il servizio locale non è riuscito a connettersi al servizio Web di reimpostazione della password.|
| 32002| ServiceBusError| Questo evento indica che si è verificato un errore di connessione all'istanza del bus di servizio del tenant. Ciò può verificarsi se le connessioni in uscita nell'ambiente locale sono bloccate. Verificare che nel firewall siano consentite le connessioni su TCP 443 e verso https://ssprsbprodncu-sb.accesscontrol.windows.net/ e riprovare. Se il problema persiste, provare a disabilitare e quindi riabilitare il writeback delle password.|
| 32003| InPutValidationError| Questo evento indica che l'input passato all'API del servizio Web non è valido. Riprovare a eseguire l'operazione.|
| 32004| DecryptionError| Questo evento indica che si è verificato un errore di decrittografia della password ricevuta dal cloud. La causa potrebbe essere una mancata corrispondenza della chiave di decrittografia tra il servizio cloud e l'ambiente locale. Per risolvere il problema, disabilitare e quindi riabilitare il writeback delle password nell'ambiente locale.|
| 32005| ConfigurationError| Durante il caricamento, le informazioni specifiche del tenant vengono salvate in un file di configurazione nell'ambiente locale. Questo evento indica che si è verificato un errore durante il salvataggio del file o che durante l'avvio del servizio si è verificato un errore di lettura del file. Per risolvere il problema, provare a disabilitare e quindi riabilitare il writeback delle password per forzare la riscrittura del file di configurazione.|
| 32007| OnBoardingConfigUpdateError| Durante l'onboarding vengono inviati dati dal cloud al servizio di reimpostazione della password locale. I dati vengono quindi scritti in un file in memoria prima di essere inviati al servizio di sincronizzazione per l'archiviazione sicura su disco. Questo evento indica un problema di scrittura o aggiornamento dei dati in memoria. Per risolvere il problema, provare a disabilitare e quindi riabilitare il writeback delle password per forzare la riscrittura del file di configurazione.|
| 32008| ValidationError| Questo evento indica che è stata ricevuta una risposta non valida dal servizio Web di reimpostazione della password. Per risolvere il problema, provare a disabilitare e quindi riabilitare il writeback delle password.|
| 32009| AuthTokenError| Questo evento indica che non è stato possibile ottenere un token di autorizzazione per l'account amministratore globale specificato durante l'installazione di Azure AD Connect. L'errore può essere causato da una password o un nome utente non valido specificato per l'account amministratore globale. L'errore può verificarsi anche se l'account amministratore globale specificato è federato. Per risolvere il problema, ripetere la configurazione con il nome utente e la password corretti e verificare che l'amministratore sia un account gestito, solo cloud o con sincronizzazione della password.|
| 32010| CryptoError| Questo evento indica che si è verificato un errore durante la generazione della chiave di crittografia della password o durante la decrittografia di una password ricevuta dal servizio cloud. L'errore indica probabilmente un problema dell'ambiente. Per altre informazioni su come risolvere il problema, esaminare i dettagli del log eventi. È anche possibile provare a disabilitare e quindi riabilitare il servizio di writeback delle password.|
| 32011| OnBoardingServiceError| Questo evento indica che il servizio locale non è stato in grado di comunicare correttamente con il servizio Web di reimpostazione della password per avviare il processo di onboarding. Ciò può dipendere da una regola del firewall o da un problema nel recupero di un token di autenticazione per il tenant. Per risolvere il problema, verificare che le connessioni in uscita su TCP 443 e TCP 9350-9354 o verso https://ssprsbprodncu-sb.accesscontrol.windows.net/ non siano bloccate. Verificare anche che l'account amministratore di Azure AD usato per l'onboarding non sia federato.|
| 32013| OffBoardingError| Questo evento indica che il servizio locale non è stato in grado di comunicare correttamente con il servizio Web di reimpostazione della password per avviare il processo di offboarding. Ciò può dipendere da una regola del firewall o da un problema nel recupero di un token di autorizzazione per il tenant. Per risolvere il problema, assicurarsi che le connessioni in uscita sulla porta 443 o verso https://ssprsbprodncu-sb.accesscontrol.windows.net/ non siano bloccate e che l'account amministratore di Azure Active Directory usato per l'offboarding non sia federato.|
| 32014| ServiceBusWarning| Questo evento indica che è stato necessario ripetere il tentativo di connessione all'istanza del bus di servizio del tenant. In condizioni normali non dovrebbe essere un problema, ma se l'evento viene visualizzato più volte, è opportuno verificare la connessione di rete al bus di servizio, specialmente se si tratta di una connessione con larghezza di banda limitata o ad alta latenza.|
| 32015| ReportServiceHealthError| Per monitorare l'integrità del servizio di writeback delle password, vengono inviati dati heartbeat al servizio Web di reimpostazione della password ogni cinque minuti. Questo evento indica che si è verificato un errore durante l'invio delle informazioni sull'integrità al servizio Web cloud. Le informazioni sull'integrità non includono dati che identificano oggetti o informazioni personali. Si tratta semplicemente di heartbeat e statistiche di base del servizio per poter fornire informazioni sullo stato del servizio nel cloud.|
| 33001| ADUnKnownError| Questo evento indica che si è verificato un errore sconosciuto restituito da Active Directory. Per altre informazioni, verificare se nel log eventi del server Azure AD Connect sono presenti eventi dall'origine ADSync.|
| 33002| ADUserNotFoundError| Questo evento indica che l'utente che sta tentando di reimpostare o modificare una password non è stato trovato nella directory locale. L'errore può verificarsi quando l'utente è stato eliminato in locale ma non nel cloud. L'errore può anche essere dovuto a un problema di sincronizzazione. Per altre informazioni, controllare i log di sincronizzazione e i dettagli relativi alle esecuzioni della sincronizzazione più recenti.|
| 33003| ADMutliMatchError| Quando una richiesta di reimpostazione o modifica della password ha origine dal cloud, viene usato l'ancoraggio cloud specificato durante l'installazione di Azure AD Connect per determinare la modalità di collegamento della richiesta a un utente nell'ambiente locale. Questo evento indica che nella directory locale sono stati trovati due utenti con lo stesso attributo di ancoraggio cloud. Per altre informazioni, controllare i log di sincronizzazione e i dettagli relativi alle esecuzioni della sincronizzazione più recenti.|
| 33004| ADPermissionsError| Questo evento indica che l'account del servizio Active Directory Management Agent (ADMA) non ha le autorizzazioni appropriate nell'account in questione per impostare una nuova password. Assicurarsi che l'account ADMA nella foresta dell'utente abbia le autorizzazioni di modifica e reimpostazione delle password per tutti gli oggetti nella foresta. Per altre informazioni su come impostare le autorizzazioni, vedere Passaggio 4: Impostare le autorizzazioni di Active Directory appropriate.|
| 33005| ADUserAccountDisabled| Questo evento indica che è stato eseguito un tentativo di reimpostare o modificare una password per un account disabilitato in locale. Abilitare l'account e ripetere l'operazione.|
| 33006| ADUserAccountLockedOut| Questo evento indica che è stato eseguito un tentativo di reimpostare o modificare una password per un account bloccato in locale. I blocchi possono verificarsi quando un utente ha tentato troppe volte di eseguire un'operazione di modifica o reimpostazione della password in un breve intervallo di tempo. Sbloccare l'account e ripetere l'operazione.|
| 33007| ADUserIncorrectPassword| Questo evento indica che l'utente ha specificato una password corrente non corretta durante l'esecuzione di un'operazione di modifica della password. Specificare la password corrente corretta e riprovare.|
| 33008| ADPasswordPolicyError| Questo evento si verifica quando il servizio di writeback delle password cerca di impostare una password nella directory locale che non soddisfa i requisiti di validità, cronologia, complessità o filtro del dominio. <br> <br> Se è prevista una validità minima della password e di recente la password è stata modificata in tale intervallo di tempo, non sarà possibile modificarla di nuovo finché non si raggiunge il periodo di validità specificato nel dominio. A scopo di test, è consigliabile impostare la validità minima su 0. <br> <br> Se sono abilitati i requisiti per la cronologia delle password, sarà necessario selezionare una password che non sia stata usata nelle ultime *N* volte, dove *N* è l'impostazione relativa alla cronologia delle password. Se si seleziona una password che è stata usata nelle ultime *N* volte, si verifica un errore. A scopo di test, è consigliabile impostare la cronologia delle password su 0. <br> <br> Se abilitati, tutti i requisiti di complessità della password vengono applicati quando l'utente tenta di modificare o reimpostare la password. <br> <br> Se sono abilitati i filtri delle password e un utente sceglie una password che non soddisfa i criteri di filtro, l'operazione di reimpostazione o di modifica non riuscirà.|
| 33009| ADConfigurationError| Questo evento indica che si è verificato un problema durante la scrittura di una password nella directory locale, a causa di un problema di configurazione con Active Directory. Per altre informazioni sull'errore, verificare se nel log eventi dell'applicazione del computer che esegue Azure AD Connect sono presenti messaggi del servizio ADSync.|

## <a name="troubleshoot-password-writeback-connectivity"></a>Risolvere i problemi relativi alla connettività di writeback delle password

Se si verificano interruzioni del servizio con il componente di writeback delle password di Azure AD Connect, ecco alcuni passaggi rapidi che è possibile eseguire per risolvere il problema:

* [Verificare la connettività della rete](#confirm-network-connectivity)
* [Riavviare il servizio di sincronizzazione Azure AD Connect](#restart-the-azure-ad-connect-sync-service)
* [Disabilitare e riabilitare la funzionalità di writeback delle password](#disable-and-re-enable-the-password-writeback-feature)
* [Installare la versione più recente di Azure AD Connect](#install-the-latest-azure-ad-connect-release)
* [Risolvere un problema relativo al writeback delle password](#troubleshoot-password-writeback)

In generale, per ripristinare il servizio il più rapidamente possibile, è consigliabile eseguire questi passaggi nell'ordine indicato in precedenza.

### <a name="confirm-network-connectivity"></a>Verificare la connettività della rete

Il punto di errore più comune è che il firewall e/o le porte proxy e i timeout di inattività non sono configurati correttamente. 

Per Azure AD Connect versione 1.1.443.0 e successive, è necessario l'accesso HTTPS in uscita agli indirizzi seguenti:

   - passwordreset.microsoftonline.com
   - servicebus.windows.net

Per una maggiore granularità, fare riferimento all'elenco degli [intervalli di indirizzi IP dei data center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653) che viene aggiornato ogni mercoledì e reso effettivo il lunedì successivo.

Per altre informazioni, vedere i prerequisiti di connettività nell'articolo [Prerequisiti di Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md).



### <a name="restart-the-azure-ad-connect-sync-service"></a>Riavviare il servizio di sincronizzazione Azure AD Connect

Per risolvere i problemi di connettività o altri problemi temporanei, riavviare il servizio di sincronizzazione Azure AD Connect:

   1. Con un account amministratore selezionare **Start** nel server che esegue Azure AD Connect.
   2. Immettere **services.msc** nel campo di ricerca e premere **INVIO**.
   3. Cercare la voce **Microsoft Azure AD Sync**.
   4. Fare clic con il pulsante destro del mouse sulla voce relativa al servizio, scegliere **Riavvia** e attendere il completamento dell'operazione.

   ![Riavviare il servizio Azure AD Sync][Service restart]

Questi passaggi consentono di ristabilire la connessione con il servizio cloud e risolvere eventuali interruzioni che si sono verificate. Se il riavvio del servizio ADSync non risolve il problema, è consigliabile provare a disabilitare e quindi riabilitare la funzionalità di writeback delle password.

### <a name="disable-and-re-enable-the-password-writeback-feature"></a>Disabilitare e riabilitare la funzionalità di writeback delle password

Per risolvere i problemi di connettività, disabilitare e quindi riabilitare la funzionalità di writeback delle password:

   1. Con un account amministratore aprire la procedura di configurazione guidata di Azure AD Connect.
   2. In **Connessione ad Azure AD** immettere le credenziali di amministratore globale di Azure AD.
   3. In **Connessione ad AD DS** immettere le credenziali di amministratore di AD Domain Services.
   4. In **Identificazione univoca per gli utenti** fare clic su **Avanti**.
   5. In **Funzionalità facoltative** deselezionare la casella di controllo **Writeback password**.
   6. Fare clic su **Avanti** nelle pagine rimanenti senza apportare alcuna modifica fino a quando non viene visualizzata la pagina **Pronto per la configurazione**.
   7. Verificare che nella pagina **Pronto per la configurazione** l'opzione **Writeback password** sia **disabilitata** e quindi fare clic sul pulsante verde **Configura** per salvare le modifiche.
   8. In **Operazione completata** deselezionare l'opzione **Sincronizza adesso** e quindi fare clic su **Fine** per chiudere la procedura guidata.
   9. Aprire di nuovo la procedura guidata di configurazione di Azure AD Connect.
   10. Ripetere i passaggi da 2 a 8, verificando di selezionare l'opzione **Writeback password** nella schermata **Funzionalità facoltative** per riabilitare il servizio.

Questi passaggi consentono di ristabilire la connessione con il servizio cloud e di risolvere eventuali interruzioni che si sono verificate.

Se disabilitando e quindi riabilitando la funzionalità di writeback delle password il problema non si risolve, è consigliabile provare a reinstallare Azure AD Connect.

### <a name="install-the-latest-azure-ad-connect-release"></a>Installare la versione più recente di Azure AD Connect

La reinstallazione di Azure AD Connect potrebbe risolvere i problemi di connettività e di configurazione tra i servizi cloud e l'ambiente Active Directory locale.

Si consiglia di eseguire questo passaggio solo dopo aver provato a eseguire i due passaggi descritti in precedenza.

> [!WARNING]
> Se le regole di sincronizzazione sono state personalizzate, *eseguire il backup prima di procedere con l'aggiornamento e ridistribuire manualmente le regole dopo aver completato l'operazione*.

   1. Scaricare la versione più recente di Azure AD Connect dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=615771).
   2. Poiché Azure AD Connect è già stato installato, è necessario eseguire un aggiornamento sul posto per aggiornare l'installazione di Azure AD Connect alla versione più recente.
   3. Eseguire il pacchetto scaricato e seguire le istruzioni visualizzate per aggiornare il computer che esegue Azure AD Connect.

I passaggi precedenti dovrebbero consentire di ristabilire la connessione con il servizio cloud e di risolvere eventuali interruzioni che si sono verificate.

Se l'installazione della versione più recente del server Azure AD Connect non risolve il problema, è consigliabile provare a disabilitare e quindi riabilitare il writeback delle password come passaggio finale, dopo avere installato la versione più recente.

## <a name="verify-that-azure-ad-connect-has-the-required-permission-for-password-writeback"></a>Verificare che Azure AD Connect abbia l'autorizzazione necessaria per il writeback delle password

Per eseguire il writeback delle password, Azure AD Connect richiede l'autorizzazione **Reimposta password** di Active Directory. Per verificare se Azure AD Connect ha l'autorizzazione per uno specifico account utente di Active Directory locale, è possibile usare la funzionalità di autorizzazione valida di Windows:

   1. Accedere al server Azure AD Connect e avviare **Synchronization Service Manager** selezionando **Start** > **Synchronization Service**.
   2. Nella scheda **Connettori** selezionare il connettore **Active Directory Domain Services** locale e quindi selezionare **Proprietà**.  

   ![Autorizzazione valida - passaggio 2](./media/active-directory-passwords-troubleshoot/checkpermission01.png)  
  
   3. Nella finestra popup selezionare **Connetti a foresta Active Directory** e annotare la proprietà **Nome utente**. Questa proprietà corrisponde all'account di Active Directory Domain Services usato da Azure AD Connect per eseguire la sincronizzazione della directory. Per consentire ad Azure AD Connect di eseguire il writeback delle password l'account di Active Directory Domain Services deve avere l'autorizzazione di reimpostazione della password.  
   
   ![Autorizzazione valida - passaggio 3](./media/active-directory-passwords-troubleshoot/checkpermission02.png) 
  
   4. Accedere a un controller di dominio locale e avviare l'applicazione **Utenti e computer di Active Directory**.
   5. Selezionare **Visualizza** e verificare che l'opzione **Funzionalità avanzate** sia abilitata.  
   
   ![Autorizzazione valida - passaggio 5](./media/active-directory-passwords-troubleshoot/checkpermission03.png) 
  
   6. Cercare l'account utente di Active Directory che si vuole verificare. Fare clic con il pulsante destro del mouse sull'account e scegliere **Proprietà**.  
   
   ![Autorizzazione valida - passaggio 6](./media/active-directory-passwords-troubleshoot/checkpermission04.png) 

   7. Nella finestra popup passare alla scheda **Sicurezza** e selezionare **Avanzate**.  
   
   ![Autorizzazione valida - passaggio 7](./media/active-directory-passwords-troubleshoot/checkpermission05.png) 
   
   8. Nella finestra popup **Advanced Security Settings for Administrator** (Impostazioni di sicurezza avanzate per l'amministratore) passare alla scheda **Accesso valido**.
   9. Fare clic su **Selezionare un utente**, selezionare l'account di Active Directory Domain Services usato da Azure AD Connect (vedere il passaggio 3) e quindi selezionare **Visualizza accesso valido**.  
   
   ![Autorizzazione valida - passaggio 9](./media/active-directory-passwords-troubleshoot/checkpermission06.png) 
  
   10. Scorrere verso il basso e cercare **Reimposta password**. Se la voce è selezionata, significa che l'account di Active Directory Domain Services ha l'autorizzazione per reimpostare la password dell'account utente di Active Directory selezionato.  
   
   ![Autorizzazione valida - passaggio 10](./media/active-directory-passwords-troubleshoot/checkpermission07.png)  

## <a name="azure-ad-forums"></a>Forum di Azure AD

In caso di domande generiche su Azure AD e la reimpostazione della password self-service, è possibile richiedere assistenza alla community sui [forum di Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). La community è composta da ingegneri, responsabili di prodotto, MVP e informatici.

## <a name="contact-microsoft-support"></a>Contattare il supporto Microsoft

Se non si riesce a trovare la risposta a un problema, i team di supporto Microsoft sono sempre disponibili per offrire maggiore assistenza.

Per garantire un supporto adeguato, verrà richiesto il maggior numero di dettagli possibile al momento dell'apertura di un caso. Tali dettagli includono:

* **Descrizione generale dell'errore**: Qual è l'errore? il comportamento notato, e le modalità in cui è possibile riprodurre l'errore. Fornire il maggior numero di dettagli possibili.
* **Pagina**: Quale pagina era visualizzata quando si è verificato l'errore? Includere l'URL, se possibile, e uno screenshot della pagina.
* **Codice di supporto**: Qual è il codice di supporto generato quando è stato visualizzato l'errore?
    * Per trovare questo codice, riprodurre l'errore, quindi fare clic sul collegamento **Codice di supporto** nella parte inferiore della schermo e inviare al personale del supporto tecnico il GUID risultante.

    ![Trovare il codice di supporto nella parte inferiore della schermata][Support code]

    * Se è visualizzata una pagina senza un codice di supporto nella parte inferiore, premere F12 ed eseguire una ricerca di SID e CID, quindi inviare i due risultati al personale del supporto tecnico.
* **Data, ora e fuso orario**: includere la data e l'ora precisa *con il fuso orario* di quando si è verificato l'errore.
* **ID utente**: Quale utente ha visualizzato l'errore? Ad esempio, *user@contoso.com*.
    * Indicare se si tratta di un utente federato,
    * Si tratta di un utente con sincronizzazione di hash della password?
    * Si tratta di un utente solo cloud?
* **Licenze**: All'utente è assegnata una licenza di Azure AD Premium o Azure AD Basic?
* **Log eventi dell'applicazione**: se si usa il writeback delle password e l'errore si verifica nell'infrastruttura locale, includere una copia compressa del log eventi dell'applicazione del server Azure AD Connect.



[Service restart]: ./media/active-directory-passwords-troubleshoot/servicerestart.png "Riavviare il servizio Azure AD Sync"
[Support code]: ./media/active-directory-passwords-troubleshoot/supportcode.png "Il codice di supporto si trova in basso a destra nella finestra"

## <a name="next-steps"></a>Passaggi successivi

Gli articoli seguenti offrono altre informazioni sull'uso della reimpostazione della password con Azure AD:

* [Come completare l'implementazione della reimpostazione della password self-service per gli utenti](active-directory-passwords-best-practices.md)
* [Reimpostare o modificare la password](active-directory-passwords-update-your-own-password.md)
* [Registrarsi per la reimpostazione della password self-service](active-directory-passwords-reset-register.md)
* [Domande sulle licenze](active-directory-passwords-licensing.md)
* [Dati usati dalla reimpostazione della password self-service e dati da immettere per gli utenti](active-directory-passwords-data.md)
* [Metodi di autenticazione disponibili per gli utenti](active-directory-passwords-how-it-works.md#authentication-methods)
* [Opzioni dei criteri per la reimpostazione della password self-service](active-directory-passwords-policy.md)
* [Panoramica del writeback delle password](active-directory-passwords-writeback.md)
* [Come creare un report sull'attività relativa alla reimpostazione della password self-service](active-directory-passwords-reporting.md)
* [Informazioni sulle opzioni della reimpostazione della password self-service](active-directory-passwords-how-it-works.md)
* [Altre informazioni non illustrate altrove](active-directory-passwords-faq.md)
