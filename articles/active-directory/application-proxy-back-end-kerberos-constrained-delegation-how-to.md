---
title: aaaHow tooconfigure toouse di applicazione un Proxy dell'applicazione la delega vincolata Kerberos | Documenti Microsoft
description: Come tooconfigure la delega vincolata Kerberos per un'applicazione Proxy dell'applicazione AD Azure.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Come tooconfigure un toouse applicazione Proxy dell'applicazione la delega vincolata Kerberos

Hello metodi disponibili per la realizzazione di applicazioni possono variare leggermente da tooapplication applicazione e una delle opzioni di hello che il Proxy di applicazione di Azure offre subito hello, toopublished SSO è la delega vincolata Kerberos (KCD). Questo è in un host di connettore è configurato tooperform vincolata kerberos authentication toobackend applicazioni, per conto degli utenti.

procedura effettiva di Hello per abilitare la delega vincolata Kerberos è relativamente semplice e in genere non richiede più di una conoscenza generale di hello vari componenti e flusso di autenticazione che facilita la SSO. Ricerca fonte di informazioni toohelp risolvere scenari in cui KCD SSO non funziona come previsto, può essere di tipo sparse.

Di conseguenza, questo articolo si tooprovide un singolo punto di riferimento che consentono di risolvere i problemi e risoluzione automatica di alcuni dei problemi più comuni di hello che vedremo. Hello stesse ora offerta ulteriori linee guida per la diagnosi di hello più complessa e realtà dell'implementazione.

Si noti che questo articolo rende hello seguenti presupposti:

-   Proxy dell'applicazione Azure è stata distribuita come per il nostro [documentazione](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) e applicazioni di accesso generale toonon la delega vincolata Kerberos funziona come previsto.

-   applicazione di destinazione pubblicato Hello è basato sull'implementazione di IIS e di Microsoft di kerberos.

-   gli host di server e dell'applicazione Hello risiedere in un singolo dominio di Active Directory. Informazioni dettagliate sugli scenari tra domini e foreste sono disponibili nel nostro [white paper sulla delega vincolata Kerberos](http://aka.ms/KCDPaper).

-   Hello soggetto applicazione viene pubblicata in un Azure tenant con la preautenticazione abilitata e gli utenti sono previsti l'autenticazione basata su tooAzure tooauthenticate mediante i moduli. Scenari di autenticazione rich client non sono trattati in questo articolo, ma essere aggiunti a un certo punto in hello future.

## <a name="prerequisites"></a>Prerequisiti

Proxy dell'applicazione Azure può essere distribuito in pressoché qualsiasi tipo di infrastruttura o le architetture di ambiente e hello senza dubbio variano da tooorganization dell'organizzazione. Una delle cause più comuni di hello della delega vincolata Kerberos relative a problemi non sono in ambienti di hello autonomamente, ma piuttosto semplice configurazioni errate o supervisione generale.

Per questo motivo, i suggerimenti sono sempre toostart, verificare di aver soddisfatto tutti hello prerequisiti disposti nel nostro main [tramite la delega vincolata Kerberos SSO con articolo Proxy dell'applicazione hello](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) prima di avviare la risoluzione dei problemi.

In particolare hello della sezione su come configurare la delega vincolata Kerberos nella versione 2012 R2, come si utilizza un approccio fondamentalmente diverso tooconfiguring la delega vincolata Kerberos, nelle versioni precedenti di Windows, ma anche in considerazione diverse altre considerazioni sulla modalità:

-   Non è raro che un tooopen server membro di dominio una finestra di dialogo canale protetto con un controller di dominio specifico. Spostare quindi tooanother finestra di dialogo in qualsiasi momento, quindi host connettore in genere non dovrebbe essere limitato toobeing toocommunicate in grado di con i controller di dominio specifici del sito locale.

-   Simile toohello sopra punto, gli scenari tra domini si basano su riferimenti che indirizzano un tooDCs host connettore che potrebbero essere presenti di fuori di perimetro della rete locale hello. In questo scenario è ugualmente importante toomake che sono anche consentire il traffico a partire tooDCs che rappresentano altri rispettivi domini, altrimenti la delega non riuscire.

-   Laddove possibile, è consigliabile evitare di posizionare dispositivi IPS/IDS attivi tra gli host del connettore e i controller di dominio, in quanto sono spesso altamente intrusivi e interferiscono con il traffico RPC di base

In quanto desideriamo tooresolve problemi rapidamente e in effetti, può richiedere tempo, pertanto laddove possibile provare e si hello più semplice di scenari di test di delega. salve altre variabili che occorrerà, hello più potrebbe essere toocontend con. Ad esempio, limitando il testing tooa singolo connettore consente di risparmiare tempo prezioso e connettori aggiuntivi possono essere aggiunti dopo la risoluzione di problemi di hello.

Alcuni fattori ambientali possono inoltre contribuire tooan problema, quindi nuovamente se è possibile limitare i hello architettura tooa ridotta al minimo per il test. Ad esempio, i firewall interno configurato in modo errato gli ACL non sono comuni, pertanto, se possibile disporre di tutto il traffico da un connettore consentito direttamente attraverso i controller di dominio toohello e applicazione back-end. 

In realtà hello assoluto migliore sul posto tooposition i connettori è vicino destinazioni tootheir come può essere. La presenza di un firewall inline durante i test aggiunge inutili complessità e potrebbe prolungare le indagini.

In sostanza, che cosa costituisce un problema di delega vincolata Kerberos? Bene, non esiste più indicazioni classiche di SSO KCD esito negativo e hello segni prima di un problema in genere manifestano sotto hello browser.

   ![Errore di configurazione della delega vincolata Kerberos](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Autorizzazione non riuscita a causa di autorizzazioni toomissing](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

tutti che presentino hello stesso sintomo di esito negativo tooperform SSO e di conseguenza negazione hello applicazione toohello di accesso utente.

## <a name="troubleshooting"></a>Risoluzione dei problemi

La modalità quindi risolvere il problema dipende dal problema hello e sintomi osservati. Prima di passare qualsiasi ulteriore sarebbe suggeriamo hello seguenti collegamenti, in quanto contengono informazioni utili, che potrebbe non ancora provenire tra:

-   [Risolvere i problemi e i messaggi di errore del proxy dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Errori di Kerberos](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Utilizzo dell'accesso Single Sign-On quando le identità cloud e locali non sono identiche](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Se si dispone di questa misura, quindi hello principale problema sicuramente esiste. È necessario toodig più approfondita, quindi avviare separando flusso hello in tre fasi distinte che è possibile risolvere.

**pre-L'autenticazione di client** -utente esterno di hello autenticazione tooAzure tramite un browser.

Essere in grado di toopre-autenticazione tooAzure è fondamentale per toofunction KCD SSO. Questa fase deve essere verificata e gestita in prima istanza, in presenza di errori. Si noti che fase di pre-autenticazione hello non ha alcuna relazione tooKCD o hello pubblicata l'applicazione. Deve essere abbastanza semplice toocorrect eventuali discrepanze dall'integrità hello soggetto conto corrente esiste in Azure e non è disabilitato o bloccato. risposta di errore Hello nel browser hello è causa di hello toounderstand in genere sufficientemente descrittivo. Se non si è certi, è inoltre possibile verificare il nostro altri tooverify di documenti di risolvere il problema.

**Servizio di delega** -hello connettore del Proxy di Azure ottenere kerberos ticket di servizio da un KDC (centro distribuzione Kerberos), per conto degli utenti.

le comunicazioni esterne Hello tra client hello e hello Azure front-end non dovrebbero avere alcun impatto sulla delega vincolata Kerberos, qualsiasi diverso da garantire che il funzionamento. Si tratta pertanto hello servizio Proxy di Azure può essere fornita con un ID utente valido che tooobtain usato un ticket kerberos. Senza questa delega vincolata Kerberos non sarebbe possibile e l'operazione avrebbe esito negativo.

Come indicato in precedenza, i messaggi di errore di hello browser forniscono in genere alcuni indizi buona sul motivo per cui operazioni non sono stati superati. Verificare che toonote all'ID attività hello e timestamp in risposta hello come in questo modo gli eventi di tooactual toocorrelate hello comportamento nel registro eventi di hello Azure Proxy.

   ![Errore di configurazione della delega vincolata Kerberos](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

E le voci corrispondenti verrebbe visualizzato il registro eventi di hello visto come eventi 13019 o 12027 hello. È possibile trovare i registri eventi connettore in hello **registri applicazioni e servizi** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Connettore**&gt;**Admin**.

   ![Evento 13019 del log eventi del proxy dell'applicazione](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Evento 12027 del log eventi del proxy dell'applicazione](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Utilizzare un record nel sistema DNS interno per l'indirizzo dell'applicazione hello e non un record CName

-   Riconfermare che ospitano connettore hello è stata concessa hello diritti toodelegate toohello designato SPN dell'account di destinazione e che **utilizza un qualsiasi protocollo di autenticazione** è selezionata. Questo argomento è trattato nel nostro articolo principale sulla [configurazione di SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)

-   Verificare che sia presente una sola istanza di hello SPN esistenti in Active Directory eseguendo un **setspn - x** da un prompt dei comandi in qualsiasi host membro di dominio

-   Controllare toosee se un criterio di dominio viene applicato hello toolimit [dimensione massima di token kerberos emesso](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), come il connettore di hello impedire di ottenere un token, se trovato toobe eccessivo

Una traccia di rete di acquisizione scambi hello tra host connettore hello e un dominio KDC sarebbe quindi hello migliore passaggio successivo recupero più basso livello dettagli sui problemi di hello. Queste informazioni sono disponibili nel [white paper di approfondimento sulla risoluzione dei problemi](https://aka.ms/proxytshootpaper).

Se si verificano problemi per le richieste, verrà visualizzato un evento nei registri hello che informa che l'autenticazione non riuscita applicazione toohello restituzione 401. Ciò indica in genere tale applicazione di destinazione hello rifiuto il ticket, quindi procedere con hello dopo una fase successiva.

**Applicazione di destinazione** -consumer hello del ticket kerberos hello fornito dal connettore hello

Questo connettore hello fase viene previsto toohave inviato un kerberos ticket toohello back-end, come un'intestazione all'interno di richiesta di hello prima dell'applicazione.

-   Utilizzo dell'applicazione hello URL interno definito nel portale di hello, verificare che un'applicazione hello sia accessibile direttamente dal browser hello in host connettore hello. A questo punto sarà possibile eseguire l'accesso. Dettagli su questa operazione sono disponibili nella pagina di risoluzione dei problemi di connettore hello.

-   Ancora nell'host di connettore hello, verificare che l'autenticazione tra il browser hello hello e un'applicazione hello utilizza kerberos, effettuando una delle seguenti hello:

1.  Eseguire gli strumenti di sviluppo (**F12**) in Internet Explorer o usare [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) dall'host connettore hello. Passare applicazione toohello utilizzando URL interno hello e controllare le intestazioni di autorizzazione WWW restituite in risposta hello da un'applicazione hello offerto hello, tooensure che una negoziazione o kerberos è presente. Un blob successive kerberos restituito nella risposta hello da hello browser toohello applicazione iniziano in genere con **YII**, pertanto si tratta di una buona indicazione di kerberos in play. NTLM su hello invece iniziano sempre con **TlRMTVNTUAAB**, che legge NTLMSSP quando decodificare da Base64. Se viene visualizzato **TlRMTVNTUAAB** all'avvio di hello del blob hello, ciò significa che Kerberos è **non** disponibili. In caso contrario, Kerberos dovrebbe essere disponibile.

  * Si noti che se si utilizza Fiddler, questo metodo, sarebbe necessario disattivare temporaneamente la protezione estesa sulla configurazione dell'applicazione hello in IIS.

     ![Finestra di controllo di rete del browser](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Figura:* poiché non inizia con TIRMTVNTUAAB, questo esempio indica che Kerberos è disponibile. Si tratta di un esempio di un BLOB Kerberos che non inizia con YII.

2.  Rimuovere temporaneamente NTLM dall'elenco di provider di hello in IIS del sito e accesso app direttamente da Internet Explorer nell'host di connettore. Con NTLM non è più nell'elenco dei provider hello, si dovrebbe essere in grado di tooaccess un'applicazione hello utilizza solo Kerberos. In caso di errore, che suggerisce che si è verificato un problema con la configurazione dell'applicazione hello e l'autenticazione Kerberos non funziona.

Se Kerberos non è disponibile, l'autenticazione dell'applicazione hello controllo negoziano le impostazioni di IIS toomake che è elencato in primo piano, con NTLM immediatamente di sotto. (Not Negotiate:kerberos o Negotiate:PKU2U). Procedere solo se Kerberos funziona.

   ![Provider di autenticazione di Windows](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Con Kerberos e NTLM sul posto, consente di disattivare temporaneamente ora pre-autenticazione per un'applicazione hello nel portale di hello. Verificare se è possibile accedere da hello internet utilizzando l'URL esterno hello. Si dovrebbe essere tooauthenticate richiesta e deve essere in grado di toodo in modo con hello stesso account hello utilizzato in un passaggio precedente. In caso contrario, questo indica un problema con un'applicazione back-end hello e non la delega vincolata Kerberos affatto.

-   Ora riabilitare pre-autenticazione nel portale di hello e l'autenticazione tramite Azure mediante il tentativo di applicazione toohello tooconnect tramite URL esterno di. Se SSO non è riuscita, si dovrebbe vedere un messaggio di errore non consentito nel browser hello più eventi 13022 nel registro hello:

    *Connettore Proxy dell'applicazione Microsoft AAD non può autenticare l'utente hello perché il server di back-end hello risponde tooKerberos i tentativi di autenticazione con un errore HTTP 401.*

    ![Errore HTTP 401 non consentito](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Controllare il pool di applicazioni configurato hello hello IIS applicazione tooensure è hello toouse configurato stesso account hello SPN è stato configurato in Active Directory, passando in IIS, come illustrato di seguito

    ![Finestra di configurazione dell'applicazione IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Quando si conosce l'identità di hello, emettere seguente hello da un prompt dei comandi toomake a cmd che questo account viene configurato in modo definito con hello SPN in questione. Ad esempio, **setspn – q http/spn.wacketywack.com**

    ![Finestra di comando SetSPN](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Verificare che hello SPN definiti in base alle impostazioni dell'applicazione hello portale hello è hello dello stesso nome SPN che è configurato con account di Active Directory di destinazione hello in uso dal pool di applicazioni dell'applicazione hello

   ![Configurazione del nome SPN nel Portale di Azure](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Andare a IIS e seleziona hello **Editor di configurazione** l'opzione per un'applicazione hello e passare troppo**system.webServer/security/authentication/windowsAuthentication** toomake che tale **UseAppPoolCredentials** è impostato tootrue

   ![Opzione delle credenziali dei pool di applicazioni della configurazione IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Pur essendo utile per migliorare le prestazioni di hello di operazioni di Kerberos, lasciare abilitata la modalità Kernel causa anche il ticket hello per hello richiesta servizio toobe decrittografati tramite l'account del computer. Sistema locale hello, in modo che l'interruzione di tootrue set anche detta delega vincolata Kerberos quando un'applicazione hello è ospitata in più server in una farm.

-   Come un'ulteriore verifica, è inoltre possibile hello toodisable **estesi** protezione troppo. Sono stati rilevati gli scenari in cui si ha dimostrato toobreak la delega vincolata Kerberos abilitando configurazioni molto specifiche, in cui un'applicazione viene pubblicata come una sottocartella del sito Web predefinito hello. Questa stessa è configurato per l'autenticazione anonima solo, lasciando hello intero le finestre di dialogo visualizzate in grigio suggerendo sarebbero gli oggetti figlio non eredita le impostazioni di active. Ma dove possibile, è sempre consigliabile con questa opzione, quindi test, ma non dimenticare toorestore questo tooenabled.

Questi controlli aggiuntivi devono avere metterti in toostart traccia tramite l'applicazione pubblicata. È possibile procedere con e selezione di connettori aggiuntivi che sono anche configurato toodelegate, ma se sono presenti ulteriori operazioni è sarebbe preferibile una lettura di questa procedura dettagliata tecnica approfondita [Guida completa di hello per risolvere i problemi di Azure AD applicazione Proxy](https://aka.ms/proxytshootpaper)

Se si è ancora impossibile tooprogress il problema, supporto potrebbe essere maggiore di tooassist lieta e continuare da qui. Creare un ticket di supporto direttamente nel portale di hello e i tecnici raggiungerà tooyou.

## <a name="other-scenarios"></a>Altri scenari

-   Proxy dell'applicazione di Azure richiede un ticket Kerberos prima di inviare l'applicazione tooan richiesta. Alcune applicazioni di terze parti 3rd, ad esempio Server Tableau non desidera che questo metodo di autenticazione e piuttosto prevede hello più tradizionali negoziazioni tootake luogo. prima richiesta Hello è anonima, consentendo di hello applicazione toorespond con tipi di autenticazione hello che supporta tramite 401.

-   Autenticazione a doppio hop: generalmente usata negli scenari con applicazioni a livelli, con un back-end e un front-end che richiedono l'autenticazione, ad esempio SQL Reporting Services.

## <a name="next-steps"></a>Passaggi successivi
[Configurare la delega vincolata Kerberos (KCD) in un dominio gestito](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
