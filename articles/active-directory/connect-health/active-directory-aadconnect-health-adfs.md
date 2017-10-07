---
title: Azure AD Connect Health con AD FS aaaUsing | Documenti Microsoft
description: Si tratta come pagina di hello Azure AD Connect Health toomonitor locale infrastruttura ADFS.
services: active-directory
documentationcenter: 
author: karavar
manager: femila
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
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Monitorare AD FS con Azure AD Connect Health
Hello seguente documentazione è toomonitoring specifico dell'infrastruttura di ADFS con Azure AD Connect Health. Per informazioni sul monitoraggio di Azure Active Directory Connect (Sincronizzazione) con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md). Per informazioni sul monitoraggio di Servizi di dominio Active Directory con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Avvisi per AD FS
Hello Azure AD Connect Health sezione degli avvisi fornisce che si hello elenco degli avvisi attivi. Ogni avviso include informazioni pertinenti, procedure di risoluzione e collegamenti toorelated documentazione.

È possibile fare doppio clic su un tooopen, avvisi attivi o risolti un nuovo pannello con informazioni aggiuntive, passaggi da eseguire tooresolve hello, avviso e la documentazione di toorelevant di collegamenti. Inoltre, è possibile visualizzare i dati cronologici avvisi risolti in hello precedente.

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Analisi di utilizzo per AD FS
Utilizzo Analitica Azure integrità di connettersi AD Foundation analizza il traffico di autenticazione hello del server federativo. Fare doppio clic sulla casella analitica hello utilizzo tooopen hello utilizzo analitica pannello, che illustra diverse metriche e i raggruppamenti.

> [!NOTE]
> toouse utilizzo Analitica con ADFS, è necessario assicurarsi che sia abilitato il controllo di ADFS. Per altre informazioni, vedere [Abilitare il controllo per AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect altre metriche, specificare un intervallo di tempo o raggruppamento hello toochange, fare clic sul grafico di hello utilizzo analitica e selezionare Modifica grafico. È quindi possibile specificare l'intervallo di tempo hello, selezionare una metrica e modificare il raggruppamento di hello. È possibile visualizzare la distribuzione hello hello del traffico di autenticazione in base a differenti "metriche" e raggruppare ogni metrica usando i parametri rilevanti "Raggruppa per" descritti nella seguente sezione hello:

**Metrica: richieste totali**, numero totale di richieste elaborate dal servizio AD FS.

|Raggruppa per | Cosa significa raggruppamento hello e perché è utile? |
| --- | --- |
| Tutti | Indica il numero di hello del numero totale di richieste elaborate da tutti i server ADFS.|
| Applicazione | Gruppi di hello richieste totali in base hello destinata relying party. Questo raggruppamento è utile toounderstand l'applicazione che riceve la percentuale di traffico totale hello. |
|  Server |Gruppi di hello totale delle richieste basate su server hello che ha elaborato la richiesta hello. Questo raggruppamento è utile toounderstand distribuzione del carico hello del traffico totale hello.
| Aggiunta all'area di lavoro |Gruppi di hello richieste totali in base provenienti da dispositivi all'area di lavoro (nota). Questo raggruppamento è utile toounderstand se le risorse sono accessibili tramite i dispositivi dell'infrastruttura di identità toohello sconosciuto. |
|  Metodo di autenticazione | Gruppi di hello totale delle richieste basate sul metodo di autenticazione hello utilizzato per l'autenticazione. Questo raggruppamento è utile toounderstand hello metodo di autenticazione comune che viene utilizzato per l'autenticazione. Di seguito sono metodi di autenticazione possibili hello <ol> <li>Autenticazione integrata di Windows (Windows)</li> <li>Autenticazione basata su moduli (Forms)</li> <li>SSO (Single Sign On)</li> <li>Autenticazione certificato X509 (certificato)</li> <br>Se i server federativi hello ricevano la richiesta di hello con un Cookie SSO, tale richiesta viene conteggiata come SSO (Single Sign On). In questi casi, se hello cookie è valido, utente hello non viene chiesto tooprovide credenziali e ottiene l'accesso trasparente toohello applicazione. Questo comportamento è comune se si dispone di più relying party protette dai server federativi hello. |
| Percorso di rete | Gruppi di hello richieste totali in base al percorso di rete hello dell'utente hello. Può essere Intranet o Extranet. Questo raggruppamento è utile tooknow la percentuale di traffico hello proviene dalla rete intranet hello o extranet. |


**Metrica: Totale richieste non riuscite di** -numero totale di hello richieste non riuscite elaborate dal servizio federativo hello. (Questa metrica è disponibile solo in AD FS per Windows Server 2012 R2)

|Raggruppa per | Cosa significa raggruppamento hello e perché è utile? |
| --- | --- |
| Tipo di errore | Mostra il numero di hello di errori in base ai tipi di errore predefinite. Questo raggruppamento è utile toounderstand hello i tipi comuni di errori. <ul><li>Nome utente o la Password non corretta: degli errori dovuti tooincorrect username o password.</li> <li>"Il blocco della extranet": errori a causa di richieste toohello ricevute da un utente a cui è stato bloccato dalla extranet </li><li> "Password scaduta": errori a causa di accesso toousers con una password scaduta.</li><li>"Account disabilitato": errori a causa di registrazione toousers con un account disabilitato.</li><li>"L'autenticazione del dispositivo": errori a causa di errori toousers tooauthenticate utilizzando l'autenticazione del dispositivo.</li><li>"L'autenticazione del certificato utente": errori a causa di errori toousers tooauthenticate a causa di un certificato non valido.</li><li>"MFA": errori a causa di errori toouser tooauthenticate utilizzando l'autenticazione a più fattori.</li><li>"Altri Credential": "Autorizzazione di rilascio": errori a causa di errori tooauthorization.</li><li>"Rilascio delega": errori a causa di errori di delega tooissuance.</li><li>"Token accettazione": errori a causa di rifiuto tooADFS hello token da un Provider di identità di terze parti.</li><li>"Protocol": errore a causa di errori tooprotocol.</li><li>"Sconosciuto": tutti gli errori. Eventuali altri errori che non rientrano in hello definite categorie.</li> |
| Server | Gruppi di hello errori basati su server hello. Questo raggruppamento è la distribuzione di errore hello toounderstand utile tra server. Una distribuzione non uniforme potrebbe indicare che un server è in uno stato difettoso. |
| Percorso di rete | Gruppi di hello gli errori in base al percorso di rete hello di richieste di hello (extranet e intranet). Questo raggruppamento è utile toounderstand hello le richieste che non sono stati superati. |
|  Applicazione | Gruppi di hello errori in base a un'applicazione hello destinata (relying party). Questo raggruppamento è utile toounderstand l'applicazione di destinazione visualizzi maggior numero di errori. |

**Metrica: numero di utenti**, media del numero di utenti univoci che eseguono attivamente l'autenticazione con ADFS

|Raggruppa per | Cosa significa raggruppamento hello e perché è utile? |
| --- | --- |
|Tutti |Questa metrica fornisce un conteggio del numero medio di utenti con servizio federativo hello in intervallo di tempo selezionato hello. gli utenti di Hello non sono raggruppati. <br>Media Hello dipende da hello intervallo di tempo selezionato. |
| Applicazione |Numero medio di hello gruppi di utenti basati su hello è destinata l'applicazione (componente). Questo raggruppamento è utile toounderstand l'applicazione che utilizza il numero di utenti. |

## <a name="performance-monitoring-for-ad-fs"></a>Monitoraggio delle prestazioni per AD FS
Il monitoraggio delle prestazioni di Azure AD Connect Health offre informazioni di monitoraggio sulle metriche. Selezionare casella monitoraggio hello, aprire un nuovo pannello con informazioni dettagliate sulle metriche di hello.

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Selezionando l'opzione di filtro hello nella parte superiore di hello del pannello hello, è possibile filtrare per server toosee metriche di un singolo server. metrica toochange, fare clic sul hello grafico in hello monitoraggio blade di monitoraggio e scegliere Modifica grafico (o un pulsante di modifica grafico selezionare hello). Dal pannello nuova hello visualizzata, è possibile selezionare altre metriche dall'elenco a discesa hello e specificare un intervallo di tempo per la visualizzazione dei dati sulle prestazioni di hello.

## <a name="reports-for-ad-fs"></a>Report per AD FS
Azure AD Connect Health fornisce report sulle attività e le prestazioni di AD FS. I report forniscono informazioni significative sulle attività dei server AD FS agli amministratori.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Primi 50 utenti con accessi tramite nome utente/password non riusciti
Uno dei motivi più comuni di hello per una richiesta di autenticazione non riuscita in un server AD FS è una richiesta con credenziali non valide, vale a dire un nome utente errato o una password. Si verifica in genere toousers scadenza password toocomplex, password dimenticate o errori di digitazione.

Ma esistono altri motivi che possono comportare un numero imprevisto di richieste gestite dal server ADFS, ad esempio: un'applicazione che memorizza nella cache le credenziali dell'utente e le credenziali di hello scadono o un utente malintenzionato che toosign in un account con una serie di password note. I due esempi seguenti sono validi motivi che possono provocare sovraccarichi tooa nelle richieste.

Azure AD Connect Health per ad FS fornisce un report sui primi 50 utenti con tentativi di accesso a causa di tooinvalid username o password. Questo report viene ottenuto dall'elaborazione di eventi di controllo hello generati da tutti i server nella farm hello hello AD FS

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

All'interno di questo report è necessario un accesso semplice toohello seguenti tipi di informazioni:

* Numero totale di richieste non riuscite con nome utente/password errata in hello ultimi 30 giorni
* Numero medio di utenti che non sono riusciti ad accedere con un nome utente o una password non valida ogni giorno.

Facendo clic su questa parte accetta toohello blade di report principale che fornisce dettagli aggiuntivi. Questo pannello comprende un grafico con l'analisi delle informazioni toohelp stabilire una linea di base sulle richieste con password o nome utente errato. Inoltre, fornisce hello elenco di utenti primi 50 con numero di tentativi non riusciti di hello.

grafico Hello fornisce hello le seguenti informazioni:

* Hello n. totale di accessi non riusciti a causa di tooa nome utente/password errate in base al giorno.
* Hello n. totale di utenti univoci che non è stato possibile gli account di accesso in base al giorno.
* Indirizzo IP client dell'ultima richiesta

![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

report di Hello fornisce hello le seguenti informazioni:

| Elemento del report | Descrizione |
| --- | --- |
| ID utente |ID utente hello mostra che è stato utilizzato. Questo valore è quali hello utente digitato, che in alcuni casi è hello ID utente errato in uso. |
| Tentativi non riusciti |Mostra hello n. totale di tentativi non riusciti per tale ID utente specifico. tabella di Hello è ordinata con hello numero massimo di tentativi non riusciti in ordine decrescente. |
| Ultimo errore |Mostra il timestamp hello quando hello ultimo errore. |
| Ultimo errore IP |Mostra l'indirizzo IP del Client hello dalla richiesta non valida più recente di hello. |

> [!NOTE]
> Questo report viene aggiornato automaticamente dopo ogni due ore con hello nuove informazioni raccolti all'interno di quel momento. Di conseguenza, i tentativi di accesso all'interno delle ultime due ore hello potrebbero non inclusi nel report hello.
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