---
title: Proxy dell'applicazione aaaTroubleshoot | Documenti Microsoft
description: Include informazioni su come errori tootroubleshoot nel Proxy dell'applicazione AD Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Risolvere i problemi e i messaggi di errore del proxy dell'applicazione
Se l'accesso a un'applicazione pubblicata o in una pubblicazione di applicazioni, si verificano errori, controllare hello seguenti opzioni toosee se il Proxy di applicazione di Microsoft Azure AD funziona correttamente:

* Servizi di Windows hello aprirlo console e verificare che hello **connettore Proxy dell'applicazione Microsoft AAD** servizio è abilitato e in esecuzione. È inoltre possibile toolook nella pagina delle proprietà del servizio Proxy di applicazione hello, come illustrato nella seguente immagine hello:  
  ![Schermata della finestra delle proprietà del connettore Proxy applicazione di Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Aprire il Visualizzatore eventi e cercare gli eventi correlati al connettore del proxy di applicazione in **Registri applicazioni e servizi** > **Microsoft** > **AadApplicationProxy** > **Connector** > **Admin**.
* Se necessario, i log più dettagliati sono disponibili da [accensione hello registri di sessione connettore Proxy dell'applicazione](application-proxy-understand-connectors.md#under-the-hood).

Per ulteriori informazioni sullo strumento di risoluzione dei problemi di hello Azure AD, vedere [risoluzione dei problemi di rete prerequisiti del strumento toovalidate connettore](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>pagina Hello non viene eseguito correttamente
È possibile che si verifichino problemi di rendering o di funzionamento dell'applicazione, ma che non vengano visualizzati messaggi di errore specifici. Ciò può verificarsi se è stato pubblicato percorso articolo hello, ma un'applicazione hello richiede il contenuto presente all'esterno di tale percorso.

Ad esempio, se si esegue la pubblicazione hello percorso https://yourapp/app ma applicazione hello chiama le immagini in https://yourapp/media, essi non eseguiti. Assicurarsi di pubblicare un'applicazione hello utilizzando hello percorso livello più alto è necessario tooinclude tutto il contenuto rilevante. In questo esempio il percorso sarebbe http://yourapp/.

Se si modifica il contenuto di tooinclude a cui fa riferimento di percorso, ma ancora necessario tooland utenti su un collegamento più approfondito nel percorso di hello, vedere hello post di blog [collegamento a destra impostazione hello per le applicazioni di Proxy dell'applicazione nel Pannello di accesso hello Azure AD e app di Office 365 utilità di avvio](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Errori del connettore

Hello utilizzare [Azure AD applicazione Proxy porte Test strumento connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify che il connettore può raggiungere il servizio di Proxy applicazione hello. Come minimo, assicurarsi che area Stati Uniti centro hello e hello area più vicina tooyou hanno tutti i segni di spunta verde. La presenza di più segni di spunta verdi indica una maggiore resilienza. 

Se la registrazione ha esito negativo durante l'installazione guidata del connettore hello, esistono due modi motivo hello tooview errore hello. Una ricerca nel registro eventi di hello in **applicazioni e servizi Logs\Microsoft\AadApplicationProxy\Connector\Admin**, o hello esecuzione dopo il comando di Windows PowerShell:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Dopo aver individuato l'errore Connector hello dal registro eventi di hello, usare questa tabella di problema di hello tooresolve errori comuni:

| Errore | Procedure consigliate |
| ----- | ----------------- |
| Registrazione del connettore non è riuscita: verificare che è stato abilitato il Proxy di applicazione nel portale di gestione Azure hello e immesso correttamente il nome utente di Active Directory e la password. Errore: "Si sono verificati uno o più errori". | Se si chiude la finestra di registrazione hello senza tooAzure AD accedere, eseguire nuovamente la creazione guidata connettore hello e registrare hello connettore. <br><br> Se la finestra di registrazione hello viene aperto e quindi si chiude immediatamente senza consentire all'utente toolog in, probabilmente si verificherà questo errore. L'errore si verifica quando viene rilevato un errore di rete nel sistema. Assicurarsi che sia possibile tooconnect da un sito Web pubblico tooa browser e che hello porte siano aperte come specificato in [prerequisiti del Proxy di applicazione](active-directory-application-proxy-enable.md). |
| Nella finestra di registrazione hello viene visualizzato un errore non crittografato. Impossibile proseguire | Se viene visualizzato questo errore e chiude la finestra hello, immesse hello errato username o password. Riprovare. |
| Registrazione del connettore non è riuscita: verificare che è stato abilitato il Proxy di applicazione nel portale di gestione Azure hello e immesso correttamente il nome utente di Active Directory e la password. Errore: ' AADSTS50059: nessuna informazione di identificazione del tenant in una richiesta di hello trovati o in cui è inclusa qualsiasi condizione di ricerca dal servizio e le credenziali di URI dell'entità non è riuscita. | Si sta tentando di toosign utilizzando un Account Microsoft e non a un dominio che fa parte dell'ID organizzazione hello della directory hello che si sta tentando di tooaccess. Assicurarsi che gli amministratori hello fa parte di hello stesso nome di dominio come dominio tenant hello, ad esempio, se hello Azure AD è contoso.com, salve deve essere admin@contoso.com. |
| Non è stato possibile tooretrieve hello criteri di esecuzione correnti per l'esecuzione di script di PowerShell. | Se hello installazione del connettore non riesce, controllare toomake assicurarsi che i criteri di esecuzione di PowerShell non sono disabilitato. <br><br>1. Aprire Editor criteri di gruppo hello.<br>2. Andare troppo**configurazione Computer** > **modelli amministrativi** > **componenti di Windows**  >   **Windows PowerShell** fare doppio clic su **Turn on Script Execution**.<br>. 3 è possibile impostare il criterio di esecuzione hello tooeither **non configurato** o **abilitato**. Se impostato troppo**abilitato**, assicurarsi che in Opzioni, hello criteri di esecuzione viene impostato tooeither **Consenti script locali e script remoti firmati** o troppo**consentire tutti gli script**. |
| Connettore non è stato possibile configurazione hello toodownload. | il certificato client Hello del connettore, utilizzato per l'autenticazione è scaduto. Ciò può verificarsi anche se si dispone di hello che connettore installato dietro un proxy. In questo caso, hello connettore non è possibile accedere a Internet hello e non sarà in grado di tooprovide applicazioni tooremote utenti. Rinnovare l'attendibilità manualmente tramite hello `Register-AppProxyConnector` cmdlet in Windows PowerShell. Se il connettore si trova dietro un proxy, è necessario toogrant Internet toohello connettore gli account di accesso "servizi di rete" e "sistema locale". Questa operazione può essere eseguita concedendo loro l'accesso Proxy toohello o impostando li toobypass hello proxy. |
| Registrazione del connettore non è riuscita: verificare che si è un amministratore globale del hello tooregister Active Directory Connector. Errore: ' hello registrazione richiesta è stata negata.' | si sta tentando di toolog con alias di Hello non è un amministratore nel dominio. Il connettore viene sempre installato per la directory di hello proprietario hello del dominio dell'utente. Assicurarsi che si sta tentando di toosign con account di amministratore hello è tenant di Azure AD toohello autorizzazioni globali. |

## <a name="kerberos-errors"></a>Errori di Kerberos

Questa tabella descrive hello più comune errori provengono dal programma di installazione di Kerberos e la configurazione e vengono forniti alcuni suggerimenti per la risoluzione.

| Errore | Procedure consigliate |
| ----- | ----------------- |
| Non è stato possibile tooretrieve hello criteri di esecuzione correnti per l'esecuzione di script di PowerShell. | Se hello installazione del connettore non riesce, controllare toomake assicurarsi che i criteri di esecuzione di PowerShell non sono disabilitato.<br><br>1. Aprire Editor criteri di gruppo hello.<br>2. Andare troppo**configurazione Computer** > **modelli amministrativi** > **componenti di Windows**  >   **Windows PowerShell** fare doppio clic su **Turn on Script Execution**.<br>. 3 è possibile impostare il criterio di esecuzione hello tooeither **non configurato** o **abilitato**. Se impostato troppo**abilitato**, assicurarsi che in Opzioni, hello criteri di esecuzione viene impostato tooeither **Consenti script locali e script remoti firmati** o troppo**consentire tutti gli script**. |
| 12008 - azure AD superato hello massimo numero di autenticazione Kerberos consentiti tentativi toohello server di back-end. | Questo errore può indicare una configurazione errata tra Azure AD e hello back-end, server applicazioni o un problema di configurazione di data e ora su entrambi i computer. server di back-end Hello ha rifiutato il ticket di Kerberos hello creato da Azure AD. Verificare che servizi di Azure e server applicazioni back-end di hello siano configurate correttamente. Assicurarsi che i server applicazioni back-end di hello e configurazione di data e ora di hello in hello Azure AD sono sincronizzate. |
| 13016 - azure AD non è possibile recuperare un ticket Kerberos per conto di utente hello poiché non esiste alcun UPN nel bordo hello token o nel cookie di accesso hello. | Si verifica un problema con la configurazione di STS hello. Correggere hello attestazione UPN configurazione nel servizio token di sicurezza hello. |
| 13019 - azure AD non è possibile recuperare un ticket Kerberos per conto di utente hello a causa di hello seguente errore generale dell'API. | Questo evento può indicare una configurazione errata tra Azure AD e server di controller di dominio hello o un problema di configurazione di data e ora su entrambi i computer. controller di dominio Hello ha rifiutato il ticket di Kerberos hello creato da Azure AD. Verificare che servizi di Azure e server applicazioni back-end di hello sono configurati correttamente, soprattutto hello SPN configurazione. Verificare che hello Azure AD sia toohello aggiunti a un dominio nello stesso dominio come hello tooensure di controller di dominio che hello controller di dominio stabilisce relazioni di trust con Azure AD. Assicurarsi che il controller di dominio hello e configurazione di data e ora di hello in hello Azure AD sono sincronizzate. |
| 13020 - azure AD non è possibile recuperare un ticket Kerberos per conto di utente hello SPN server back-end di hello non è definito. | Questo evento può indicare una configurazione errata tra Azure AD e server di controller di dominio hello o un problema di configurazione di data e ora su entrambi i computer. controller di dominio Hello ha rifiutato il ticket di Kerberos hello creato da Azure AD. Verificare che servizi di Azure e server applicazioni back-end di hello sono configurati correttamente, soprattutto hello SPN configurazione. Verificare che hello Azure AD sia toohello aggiunti a un dominio nello stesso dominio come hello tooensure di controller di dominio che hello controller di dominio stabilisce relazioni di trust con Azure AD. Assicurarsi che il controller di dominio hello e configurazione di data e ora di hello in hello Azure AD sono sincronizzate. |
| 13022 - azure AD non può autenticare l'utente hello perché il server di back-end hello risponde tooKerberos i tentativi di autenticazione con un errore HTTP 401. | Questo evento può indicare una configurazione errata tra Azure AD e hello back-end, server applicazioni o un problema di configurazione di data e ora su entrambi i computer. server di back-end Hello ha rifiutato il ticket di Kerberos hello creato da Azure AD. Verificare che servizi di Azure e server applicazioni back-end di hello siano configurate correttamente. Assicurarsi che i server applicazioni back-end di hello e configurazione di data e ora di hello in hello Azure AD sono sincronizzate. |

## <a name="end-user-errors"></a>Errori utente finale

Questo elenco enumera gli errori che gli utenti finali possono verificarsi quando si tenta di app hello tooaccess ed esito negativo. 

| Errore | Procedure consigliate |
| ----- | ----------------- |
| Hello Impossibile visualizzare la pagina hello. | L'utente può visualizzare questo errore quando si tenta di tooaccess hello app pubblicata se l'applicazione hello è un'applicazione di autenticazione integrata di Windows. Hello definito nome SPN per l'applicazione potrebbe non essere corretta. Per le app di autenticazione integrata di Windows, verificare che SPN configurate per l'applicazione hello sia corretto. |
| Hello Impossibile visualizzare la pagina hello. | L'utente può visualizzare questo errore quando si tenta di tooaccess hello app pubblicata se l'applicazione hello è un'applicazione di OWA. Questo potrebbe essere causato da uno dei seguenti hello:<br><li>Hello definito nome SPN per l'applicazione non è corretta. Verificare che SPN configurate per l'applicazione hello sia corretto.</li><li>Hello utente che ha tentato di un'applicazione hello tooaccess utilizza un account Microsoft anziché hello toosign account aziendale appropriato in, hello utente o un utente guest. Verificare che hello utente consente l'accesso usando il proprio account aziendale che corrispondenze hello dominio di hello pubblicata l'applicazione. Gli utenti con account Microsoft o guest non possono accedere alle applicazioni con autenticazione integrata di Windows.</li><li>utente di Hello che ha tentato di un'applicazione hello tooaccess non è definito correttamente per l'applicazione hello sul lato locale. Assicurarsi che l'utente disponga delle autorizzazioni appropriate di hello come definito per l'applicazione back-end hello sul computer locale. |
| Non è possibile accedere a questa app aziendale. Si sono tooaccess non autorizzato l'applicazione. Autorizzazione non riuscita. Verificare che l'utente hello tooassign con applicazione toothis di accesso. | Questo errore possono verificarsi gli utenti durante il tentativo di tooaccess hello app pubblicata se utilizzano gli account Microsoft anziché toosign loro account aziendale in. Anche gli utenti guest possono visualizzare questo errore. Gli utenti con account Microsoft o guest non possono accedere alle applicazioni con autenticazione integrata di Windows. Verificare che hello utente consente l'accesso usando il proprio account aziendale che corrispondenze hello dominio di hello pubblicata l'applicazione.<br><br>Non assegnati utente hello per questa applicazione. Passare toohello **applicazione** scheda e in **utenti e gruppi**, assegnare l'utente o applicazione toothis di gruppo utente. |
| Non è possibile accedere a questa app aziendale in questo momento. Riprovare più tardi... connettore hello timeout. | Questo errore possono verificarsi gli utenti durante il tentativo di tooaccess hello app pubblicata se non sono definiti correttamente per l'applicazione hello sul lato locale. Assicurarsi che gli utenti dispongano delle autorizzazioni appropriate di hello come definito per l'applicazione back-end hello sul computer locale. |
| Non è possibile accedere a questa app aziendale. Si sono tooaccess non autorizzato l'applicazione. Autorizzazione non riuscita. Assicurarsi che l'utente hello dispone di una licenza per Azure Active Directory Premium o Basic. | Questo errore possono verificarsi gli utenti durante il tentativo di tooaccess hello app pubblicata se non sono stati assegnati in modo esplicito con una licenza Premium/Basis dall'amministratore del sottoscrittore hello. Passare Active Directory del sottoscrittore toohello **licenze** scheda e verificare che l'utente o il gruppo viene assegnato una licenza Premium o Basic. |

## <a name="my-error-wasnt-listed-here"></a>L'errore non è riportato in questi elenchi

Se si verifica un errore o un problema con Proxy dell'applicazione Azure Active Directory che non è elencato in questa Guida alla risoluzione dei problemi, desideriamo toohear su di esso. Inviare un messaggio di posta elettronica tooour [team feedback](mailto:aadapfeedback@microsoft.com) con dettagli hello è stato rilevato un errore hello.

## <a name="see-also"></a>Vedere anche
* [Abilitare il proxy di applicazione per Azure Active Directory](active-directory-application-proxy-enable.md)
* [Pubblicare le applicazioni con il proxy di applicazione](active-directory-application-proxy-publish.md)
* [Abilita Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
