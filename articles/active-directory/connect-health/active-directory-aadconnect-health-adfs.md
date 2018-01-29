---
title: Uso di Azure AD Connect Health con AD FS | Microsoft Docs
description: "Questa è la pagina di Azure AD Connect Health che illustra come monitorare l'infrastruttura AD FS locale."
services: active-directory
documentationcenter: 
author: karavar
manager: mtillman
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 834dbbd0be30181de1a71df05d2867be0e1c59b4
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Monitorare AD FS con Azure AD Connect Health
La documentazione seguente è specifica per il monitoraggio dell'infrastruttura AD FS con Azure AD Connect Health. Per informazioni sul monitoraggio di Azure Active Directory Connect (Sincronizzazione) con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md). Per informazioni sul monitoraggio di Servizi di dominio Active Directory con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Avvisi per AD FS
La sezione degli avvisi di Azure AD Connect Health contiene l'elenco degli avvisi attivi. Ogni avviso include informazioni pertinenti, la procedura di risoluzione e collegamenti alla documentazione correlata.

È possibile fare doppio clic su un avviso attivo o risolto per aprire un nuovo pannello con informazioni aggiuntive, procedure utili per risolvere l'avvisto e collegamenti alla documentazione rilevante. È anche possibile visualizzare dati storici sugli avvisi risolti in passato.

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Analisi di utilizzo per AD FS
Analisi di utilizzo di Azure AD Connect Health analizza il traffico di autenticazione dei server federativi. È possibile fare doppio clic sulla casella dell'analisi di utilizzo per aprire il pannello corrispondente, che mostra diverse metriche e diversi raggruppamenti.

> [!NOTE]
> Per poter usare l'analisi di utilizzo con AD FS, è necessario verificare che il controllo di AD FS sia abilitato. Per altre informazioni, vedere [Abilitare il controllo per AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

Per selezionare altre metriche, specificare un intervallo di tempo o modificare il raggruppamento, è sufficiente fare clic con il pulsante destro del mouse sul pannello dell'analisi di utilizzo e scegliere Modifica grafico. È quindi possibile specificare l'intervallo di tempo, selezionare metriche diverse e cambiare il raggruppamento. È possibile visualizzare la distribuzione del traffico di autenticazione in "metriche" diverse e raggruppare ogni metrica con i parametri di raggruppamento pertinenti descritti nella sezione seguente:

**Metrica: richieste totali**, numero totale di richieste elaborate dal servizio AD FS.

|Raggruppa per | Cosa significa il raggruppamento e perché è utile? |
| --- | --- |
| Tutti | Mostra il conteggio del numero totale di richieste elaborate da tutti i server AD FS.|
| Applicazione | Raggruppa le richieste totali in base alla relying party di destinazione. Questo raggruppamento è utile per conoscere la percentuale del traffico totale ricevuta da ogni applicazione. |
|  Server |Raggruppa le richieste totali in base al server che ha elaborato la richiesta. Questo raggruppamento è utile per conoscere la distribuzione del carico del traffico totale.
| Aggiunta all'area di lavoro |Raggruppa le richieste totali in base al fatto che provengano da dispositivi aggiunti all'area di lavoro (noti). Questo raggruppamento è utile per conoscere se le risorse sono accessibili con dispositivi sconosciuti all'infrastruttura di gestione delle identità. |
|  Metodo di autenticazione | Raggruppa le richieste totali in base al metodo di autenticazione usato per l'autenticazione. Questo raggruppamento è utile per conoscere il metodo di autenticazione comune usato per l'autenticazione. Di seguito sono indicati i metodi di autenticazione possibili  <ol> <li>Autenticazione integrata di Windows (Windows)</li> <li>Autenticazione basata su moduli (Forms)</li> <li>SSO (Single Sign On)</li> <li>Autenticazione certificato X509 (certificato)</li> <br>Se i server federativi ricevono la richiesta con un cookie SSO, tale richiesta viene considerata SSO (Single Sign-On). In questi casi, se il cookie è valido, all'utente non viene chiesto di fornire le credenziali e ottiene l'accesso trasparente all'applicazione. Questo comportamento è normale se sono presenti più relying party protette dai server federativi. |
| Percorso di rete | Raggruppa le richieste totali in base al percorso di rete dell'utente. Può essere Intranet o Extranet. Questo raggruppamento è utile per conoscere la percentuale del traffico proveniente dalla Intranet e dalla Extranet. |


**Metrica: totale richieste non riuscite**, numero totale di richieste non riuscite elaborate dal servizio federativo. (Questa metrica è disponibile solo in AD FS per Windows Server 2012 R2)

|Raggruppa per | Cosa significa il raggruppamento e perché è utile? |
| --- | --- |
| Tipo di errore | Mostra il numero di errori in base ai tipi di errore predefiniti. Questo raggruppamento è utile per conoscere i tipi di errori comuni. <ul><li>Nome utente o password non corretta: errori causati da un nome utente o una password non corretta.</li> <li>"Blocco Extranet": errori causati dalle richieste ricevute da un utente per il quale è stato bloccato l'accesso alla Extranet. </li><li> "Password scaduta": errori causati da utenti che effettuano l'accesso con una password scaduta.</li><li>"Account disabilitato": errori causati da utenti che effettuano l'accesso con un account disabilitato.</li><li>"Autenticazione dispositivo": errori causati da utenti che non riescono ad autenticarsi con Autenticazione dispositivo.</li><li>"Autenticazione certificato utente": errori causati da utenti che non riescono ad autenticarsi a causa di un certificato non valido.</li><li>"MFA": errori causati da utenti che non riescono ad autenticarsi con Multi-Factor Authentication.</li><li>"Altre credenziali" e "Autorizzazione rilascio": errori causati da errori di autorizzazione.</li><li>"Delega rilascio": errori causati da errori di delega rilascio.</li><li>"Accettazione token": errori causati dal rifiuto da parte di AD FS del token di un provider di identità di terze parti.</li><li>"Protocollo": errore causato da errori del protocollo.</li><li>"Sconosciuto": tutti gli errori. Eventuali altri errori che non rientrano nelle categorie definite.</li> |
| Server | Raggruppa gli errori in base al server. Questo raggruppamento è utile per conoscere la distribuzione degli errori nei server. Una distribuzione non uniforme potrebbe indicare che un server è in uno stato difettoso. |
| Percorso di rete | Raggruppa gli errori in base al percorso di rete delle richieste (Intranet ed Extranet). Questo raggruppamento è utile per conoscere il tipo di richieste che hanno esito negativo. |
|  Applicazione | Raggruppa gli errori in base all'applicazione di destinazione (relying party). Questo raggruppamento è utile per conoscere l'applicazione di destinazione che sta visualizzando il maggior numero di errori. |

**Metrica: numero di utenti**, media del numero di utenti univoci che eseguono attivamente l'autenticazione con ADFS

|Raggruppa per | Cosa significa il raggruppamento e perché è utile? |
| --- | --- |
|Tutti |Questa metrica fornisce un conteggio del numero medio di utenti che usano il servizio federativo nel periodo di tempo selezionato. Gli utenti non sono raggruppati. <br>La media dipende dal periodo di tempo selezionato. |
| Applicazione |Raggruppa il numero medio di utenti in base all'applicazione di destinazione (relying party). Questo raggruppamento è utile per conoscere quanti utenti stanno usando una determinata applicazione. |

## <a name="performance-monitoring-for-ad-fs"></a>Monitoraggio delle prestazioni per AD FS
Il monitoraggio delle prestazioni di Azure AD Connect Health offre informazioni di monitoraggio sulle metriche. Se si seleziona la casella Monitoraggio, viene visualizzato un nuovo pannello che include informazioni dettagliate sulle metriche.

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Selezionando l'opzione Filtro nella parte superiore del pannello, è possibile filtrare in base al server per visualizzare le metriche di un singolo server. Per modificare le metriche, fare clic con il pulsante destro del mouse sul grafico di monitoraggio nel pannello Monitoraggio e scegliere Modifica grafico (oppure selezionare il pulsante Modifica grafico). Dal nuovo pannello visualizzato è possibile selezionare altre metriche nell'elenco a discesa e specificare un intervallo di tempo per cui visualizzare i dati delle prestazioni.

## <a name="reports-for-ad-fs"></a>Report per AD FS
Azure AD Connect Health fornisce report sulle attività e le prestazioni di AD FS. I report forniscono informazioni significative sulle attività dei server AD FS agli amministratori.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Primi 50 utenti con accessi tramite nome utente/password non riusciti
Uno dei motivi più comuni per cui una richiesta di autenticazione può non riuscire in un server AD FS è l'uso di credenziali che non sono valide, vale a dire che il nome utente o la password non è valida. Gli utenti rilevano questo problema in genere a causa di password complesse, password dimenticate o errori di digitazione.

Esistono tuttavia altri motivi che possono provocare un numero inaspettatamente elevato di richieste gestite dai server AD FS, ad esempio un'applicazione che memorizza nella cache le credenziali utente in corrispondenza con la scadenza delle credenziali oppure un utente malintenzionato che prova ad accedere a un account con una serie di password note. Questi due esempi sono motivi validi di un'eventuale picco nelle richieste.

Azure AD Connect Health per AD FS fornisce un report sui primi 50 utenti con tentativi di accesso non riusciti a causa di un nome utente o una password non valida. Questo report viene ottenuto elaborando gli eventi di controllo generati da tutti i server AD FS nelle farm.

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

All'interno del report è possibile accedere facilmente alle informazioni seguenti:

* Numero totale di richieste non riuscite con nome utente o password non valida negli ultimi 30 giorni.
* Numero medio di utenti che non sono riusciti ad accedere con un nome utente o una password non valida ogni giorno.

Facendo clic su questa parte si passa al pannello principale del report che fornisce dettagli aggiuntivi. Questo pannello include un grafico con le informazioni relative alla tendenza, utile per stabilire una baseline sulle richieste con nome utente non valido o password errata. Fornisce anche l'elenco dei primi 50 utenti con il numero di tentativi non riusciti.

Il grafico fornisce le informazioni seguenti:

* Numero totale di accessi non riusciti a causa di un nome utente o una password non valida ogni giorno.
* Numero totale di utenti univoci con accessi non riusciti ogni giorno.
* Indirizzo IP client dell'ultima richiesta

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

Il report fornisce le informazioni seguenti:

| Elemento del report | Descrizione |
| --- | --- |
| ID utente |Mostra l'ID utente che è stato usato. Questo valore corrisponde a quanto digitato dall'utente, che a volte corrisponde all'uso di un ID utente non valido. |
| Tentativi non riusciti |Mostra il numero totale di tentativi non riusciti per l'ID utente specifico. La tabella è riportata in ordine decrescente a partire dal numero maggiore di tentativi non riusciti. |
| Ultimo errore |Mostra il timestamp del momento in cui si è verificato l'ultimo errore. |
| Ultimo errore IP |Mostra l'indirizzo IP client dell'ultima richiesta non valida. |

> [!NOTE]
> Il report viene aggiornato automaticamente ogni due ore con le nuove informazioni raccolte. Di conseguenza, i tentativi di accesso nelle ultime due ore potrebbero non essere inclusi nel report.
>
>

## <a name="related-links"></a>Collegamenti correlati
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)