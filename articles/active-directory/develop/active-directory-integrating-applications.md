---
title: le applicazioni con Azure Active Directory aaaIntegrating | Documenti Microsoft
description: Informazioni dettagliate su come tooadd, aggiornare o rimuovere un'applicazione in Azure Active Directory (Azure AD).
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Integrazione di applicazioni con Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Gli sviluppatori aziendali e fornitori di software-as-a-service (SaaS) possono sviluppare servizi cloud commerciali o applicazioni line of business che può essere integrato con Azure Active Directory (Azure AD) tooprovide sicuro l'accesso e l'autorizzazione per i relativi servizi. toointegrate un'applicazione o un servizio con Azure AD, uno sviluppatore deve innanzitutto registrare dettagli hello dell'applicazione con Azure AD tramite hello portale di Azure classico.

Questo articolo illustra come tooadd, aggiornare o rimuovere un'applicazione in Azure AD. Si apprenderà sui diversi tipi di applicazioni che possono essere integrate con Azure AD, la modalità di hello tooconfigure tooaccess le applicazioni ad altre risorse, ad esempio API web e altro ancora.

vedere toolearn ulteriori informazioni su hello due Azure AD oggetti che rappresentano una relazione tra di hello tra di essi, e l'applicazione registrata [oggetti applicazione e oggetti entità servizio](active-directory-application-objects.md); toolearn ulteriori informazioni sulle linee guida del marchio hello è deve utilizzare durante lo sviluppo di applicazioni con Azure Active Directory, vedere [linee guida sulla personalizzazione per le app integrata](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Aggiunta di un'applicazione
Qualsiasi applicazione che richiede la funzionalità di hello toouse di Azure AD deve prima essere registrato in un tenant di Azure AD. Questo processo di registrazione comporta l'assegnazione dei dettagli di Azure AD sull'applicazione, ad esempio hello URL in cui è disponibile, hello risposte toosend URL dopo aver autenticato un utente, hello URI che identifica un'applicazione hello e così via.

Se si sta creando un'applicazione web che richiede solo toosupport sign-in per gli utenti in Azure AD, è semplicemente possibile seguire le istruzioni di hello seguenti. Se l'applicazione richiede le credenziali o le autorizzazioni di un'API web tooaccess tooa o necessario tooallow utenti da altre tooaccess i tenant che Azure AD, vedere [aggiornamento di un'applicazione](#updating-an-application) toocontinue sezione sulla configurazione dell'applicazione.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>una nuova applicazione nel portale di Azure hello tooregister
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.
4. Seguire le istruzioni di hello e creare una nuova applicazione. Per ottenere esempi specifici per applicazioni Web o per applicazioni native, vedere le [Guide introduttive](active-directory-developers-guide.md).
  * Per le applicazioni Web, fornire hello **Sign-On URL**, ovvero URL di base hello dell'app, in cui gli utenti possono accedere ad esempio `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Per le applicazioni Native, fornire un **URI di reindirizzamento**, quali Azure AD Usa tooreturn token risposte. Immettere un'applicazione, tooyour specifico valore. ad esempio`http://MyFirstAADApp`
5. Dopo aver completato la registrazione, Azure AD le assegna all'applicazione un identificatore client univoci, hello l'ID dell'applicazione. È stato aggiunto l'applicazione e si verrà reindirizzati toohello pagina di avvio rapido per l'applicazione. A seconda dell'applicazione web o un'applicazione nativa, verranno visualizzate diverse opzioni sull'applicazione di tooyour tooadd funzionalità aggiuntive. Dopo aver aggiunto l'applicazione, è possibile iniziare l'aggiornamento del toosign di utenti applicazione tooenable in, accedere ad API web in altre applicazioni o configurare l'applicazione multi-tenant (che consente all'applicazione di altre organizzazioni tooaccess).

> [!NOTE]
> Per impostazione predefinita, registrazione dell'applicazione hello appena creato è configurato tooallow utenti toosign la directory in tooyour applicazione.
> 
> 

## <a name="updating-an-application"></a>Aggiornamento di un'applicazione
Dopo l'applicazione è stato registrato con Azure AD, potrebbe essere necessario aggiornare toobe tooprovide tooweb le API di accesso, essere resa disponibile in altre organizzazioni e altro ancora. In questa sezione descrive diversi modi in cui potrebbe essere necessario tooconfigure ulteriormente l'applicazione. Innanzitutto si inizierà con una panoramica di hello il Framework di consenso, ovvero toounderstand importante se si siano compilando applicazioni/API di risorse che verranno usate dalle applicazioni client compilate dagli sviluppatori dell'organizzazione o un'altra organizzazione.

Per ulteriori informazioni su hello autenticazione modo funziona in Azure AD, vedere [scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Panoramica del framework di consenso hello
Il framework di consenso di Azure AD rende facile toodevelop web di multi-tenant e applicazioni client native che devono tooaccess web API protette da un tenant di Azure AD diverso dal hello in cui è registrata un'applicazione hello client. Queste API web includono hello API di Microsoft Graph (tooaccess Azure Active Directory, Intune e servizi di Office 365) e altri servizi Microsoft API, inoltre tooyour proprietari API web. framework di Hello è basato su un utente o un amministratore di fornire il consenso tooan applicazione che richiede toobe registrate nella directory, che possono comportare l'accesso ai dati di directory.

Ad esempio, se un'applicazione client web necessita di informazioni del calendario tooread sull'utente hello da Office 365, tale utente sarà richiesto tooconsent toohello client applicazione. Dopo aver ottenuto il consenso, un'applicazione client hello essere in grado di toocall hello Microsoft Graph API per conto di utente hello e utilizzare le informazioni del calendario hello in base alle esigenze. Hello [Microsoft Graph API](https://graph.microsoft.io) fornisce accesso toodata in Office 365 (ad esempio calendari e messaggi di Exchange, siti ed elenchi di SharePoint, i documenti da OneDrive, blocchi appunti di OneNote, Planner, cartelle di lavoro di attività Excel, e così via), nonché gli utenti e gruppi da Azure AD e altri oggetti di dati da altri servizi cloud Microsoft. 

il framework di consenso Hello è basato su OAuth 2.0 e i relativi flussi diversi, ad esempio di codice di autorizzazione concedono autorizzazioni e le credenziali client, mediante client pubblici o riservati. Tramite OAuth 2.0, Azure AD rende possibili toobuild molti tipi diversi di applicazioni client, ad esempio come in un telefono, Tablet PC, server o un'applicazione web e accedere a risorse toohello richiesto.

Per ulteriori informazioni sul framework di consenso hello, vedere [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md)e per informazioni su come ottenere l'accesso autorizzato tooOffice 365 tramite Microsoft Graph, vedere [l'autenticazione dell'App con Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Esempio di esperienza di consenso hello
Hello seguenti passaggi verranno illustrato il funzionamento dell'esperienza di consenso hello per sviluppatore dell'applicazione hello e utente.

1. Nella pagina di configurazione dell'applicazione client web nel portale di Azure hello, impostare le autorizzazioni di hello che richiede l'applicazione utilizzando i menu hello in hello sezione autorizzazioni necessarie.
   
    ![Autorizzazioni tooother applicazioni](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Tenere presente che sono state aggiornate le autorizzazioni dell'applicazione, un'applicazione hello è in esecuzione, e un utente è su toouse per hello prima volta. Se un'applicazione hello non ha già acquisito un'applicazione hello token, accesso o di aggiornamento deve tooobtain endpoint di autorizzazione toogo tooAzure AD un codice di autorizzazione che può essere utilizzati tooacquire un nuovo accesso e un token di aggiornamento.
3. Se l'utente hello non è già autenticato, verranno richieste toosign in tooAzure Active Directory.
   
    ![Accesso utente o amministratore tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Dopo l'accesso utente hello, Azure AD determinerà se l'utente di hello deve toobe mostrato una pagina di consenso. Questo aspetto dipende dal fatto utente hello (o l'amministratore della propria organizzazione) è già concesso il consenso dell'applicazione hello. Se non è già stato concesso il consenso, Azure AD richiederà hello utente il consenso e visualizzerà le autorizzazioni necessarie hello deve toofunction. set di Hello di autorizzazioni che viene visualizzato nella finestra di dialogo di consenso hello sono hello uguale a ciò che è stata selezionata nella autorizzazioni delegate hello in hello portale di Azure.
   
    ![Esperienza di autorizzazione utente](./media/active-directory-integrating-applications/consent.png)
5. Dopo hello utente concede il consenso, è possibile che l'applicazione tooyour, che può essere riscattato tooacquire un token di accesso e token di aggiornamento viene restituito un codice di autorizzazione. Per ulteriori informazioni su questo flusso, vedere hello [sezione tooweb API dell'applicazione web](active-directory-authentication-scenarios.md#web-application-to-web-api) sezione [scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).

6. Come amministratore, è anche possibile acconsente le autorizzazioni delegate tooan dell'applicazione per conto di tutti gli utenti di hello nel tenant. Ciò impedirà il dialogo di consenso hello venga visualizzato per ogni utente nel tenant di hello. È possibile farlo da hello [portale di Azure](https://portal.azure.com) dalla pagina dell'applicazione. Da hello **impostazioni** pannello per l'applicazione, fare clic su **autorizzazioni obbligatorie** e fare clic su hello **concedere autorizzazioni** pulsante. 

    ![Concedere le autorizzazioni per il consenso esplicito dell'amministratore](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Concedere il consenso esplicito utilizzando hello **concedere autorizzazioni** pulsante è attualmente richiesti per applicazioni a pagina singola (SPA) utilizzando ADAL.js, come token di accesso hello richiesta senza una richiesta di consenso, avrà esito negativo se il consenso non è già concessa.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurazione dell'applicazione client tooaccess web API
Affinché un riservate/web client application toobe in grado di tooparticipate in un flusso di concessione di autorizzazione che richiede l'autenticazione (e ottenere un token di accesso), è necessario stabilire credenziali protette. metodo di autenticazione predefinito di Hello supportato dal portale di Azure hello è l'ID Client + chiave simmetrica. In questa sezione verrà illustrate chiave segreta di hello configurazione passaggi necessari tooprovide hello credenziali del client.

Inoltre, prima che possa un client accesso un'API web esposti da un'applicazione della risorsa (ie: API di Microsoft Graph), il framework di consenso hello garantisce hello il client ottiene hello autorizzazioni concesse autorizzazioni hello necessari, in base alle richieste. Per impostazione predefinita, tutte le applicazioni possono scegliere le autorizzazioni da Azure Active Directory (API Graph) e API di gestione del servizio di Azure, con l'autorizzazione "Abilita accesso e lettura del profilo utente" hello Azure AD già selezionata per impostazione predefinita. Se l'applicazione client viene registrata in un tenant di Azure AD per Office 365, saranno disponibili per la selezione anche le API Web e le autorizzazioni per SharePoint ed Exchange Online. È possibile selezionare [due tipi di autorizzazioni](active-directory-dev-glossary.md#permissions) in hello caselle di riepilogo desiderato successivo toohello web API:

* Autorizzazioni per l'applicazione: L'applicazione client deve tooaccess hello web API direttamente come se stessa (Nessun contesto utente). Questo tipo di autorizzazione richiede il consenso dell'amministratore e non è disponibile per le applicazioni client native.
* Le autorizzazioni delegate: L'applicazione client deve tooaccess hello web API come utente connesso di hello, ma con accesso limitato dall'autorizzazione hello selezionato. Questo tipo di autorizzazione può essere concesse da un utente, a meno che l'autorizzazione di hello viene configurata come richiedere il consenso dell'amministratore. 

> [!NOTE]
> Aggiunta di un'applicazione di autorizzazione delegata tooan non verranno concesse automaticamente consenso toohello utenti nel tenant di hello, come in hello portale classico di Azure. Hello utenti devono eseguire manualmente acconsentire per hello aggiunto delegate le autorizzazioni in fase di esecuzione, a meno che l'amministratore di hello hello **concedere autorizzazioni** pulsante hello **autorizzazioni obbligatorie** sezione della pagina di applicazione hello in hello portale di Azure. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>credenziali tooadd o tooaccess autorizzazioni web API
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. tooadd una chiave privata per le credenziali dell'applicazione web, fare clic su sezione "Chiavi" hello dal pannello impostazioni hello.  
   
   * Aggiungere una descrizione per la chiave e selezionare una durata di 1 o 2 anni. 
   * colonna all'estrema destra Hello conterrà valore chiave hello, dopo aver salvato le modifiche alla configurazione di hello. Essere nuovamente toocome che toothis sezione e copia dopo è stato raggiunto salvata, pertanto sarà necessario per utilizzare nell'applicazione client durante l'autenticazione in fase di esecuzione.
5. tooadd autorizzazioni tooaccess API risorsa dal client, fare clic su sezione "Autorizzazioni necessarie" hello dal pannello impostazioni hello. 
   
   * In primo luogo, fare clic su pulsante "Aggiungi" hello.
   * Fare clic su "Selezionare un'API" tooselect hello tipo risorse desiderate toopick da.
   * Sfoglia elenco hello di API disponibili o utilizzare tooselect casella di ricerca hello applicazioni hello risorse disponibili nella directory che espongono un'API web. Fare clic sulla risorsa hello è interessati, quindi fare clic su **selezionare**.
   * Una volta selezionato, è possibile spostare toohello **selezionare autorizzazioni** menu, in cui è possibile selezionare hello "applicazione le autorizzazioni" e "delega" per l'applicazione.
   
6. Al termine, fare clic su hello **eseguita** pulsante.

> [!NOTE]
> Facendo clic su hello **eseguita** anche automaticamente impostate le autorizzazioni di hello per l'applicazione nella directory in base alle autorizzazioni di hello applicazioni tooother configurata.  È possibile visualizzare queste autorizzazioni applicazione osservando l'applicazione hello **impostazioni** blade.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configurazione di una web tooexpose di risorse dell'applicazione API
È possibile sviluppare un'API web e renderlo disponibile tooclient applicazioni esponendo accesso [ambiti](active-directory-dev-glossary.md#scopes) e [ruoli](active-directory-dev-glossary.md#roles). Un'API web correttamente configurata viene resa disponibile come hello altre API web Microsoft, tra cui hello API Graph e hello API di Office 365. Gli ambiti e i ruoli di accesso vengono esposti con il [manifesto dell'applicazione](active-directory-dev-glossary.md#application-manifest), ovvero un file JSON che rappresenta la configurazione dell'identità dell'applicazione.  

Hello successiva sezione verrà illustrato come gli ambiti tooexpose accesso, modificando il manifesto dell'applicazione hello risorse.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Aggiunta di applicazione risorse tooyour gli ambiti di accesso
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. Fare clic su **manifesto** da hello applicazione pagina tooopen hello inline editor del manifesto. 
5. Sostituire "oauth2Permissions" nodo con hello seguente frammento di codice JSON. Questo frammento è riportato un esempio di come tooexpose un ambito noto come "rappresentazione dell'utente", che consente un toogive proprietario di risorse di un'applicazione client a un tipo di delegato accesso tooa risorse. Assicurarsi di modificare testo hello e i valori per la propria applicazione:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    il valore di id Hello deve essere un nuovo GUID generato creati utilizzando un [lo strumento di generazione di GUID](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) o a livello di codice. Rappresenta un identificatore univoco per l'autorizzazione di hello esposto dall'API web hello. Una volta che il client è configurato in modo appropriato toorequest accesso tooyour web API e le chiamate API web di hello, presenta un token JWT OAuth 2.0 con hello (scp) di ambito attestazione set toohello valore precedente, che in questo caso è user_impersonation.
   
   > [!NOTE]
   > Se necessario, è possibile esporre altri ambiti successivamente. Tenere presente che l'API Web può esporre più ambiti associati a molte funzioni diverse. Ora è possibile controllare l'accesso toohello API web utilizzando l'ambito di hello (scp) attestazione nel token JWT OAuth 2.0 hello ricevuto.
   > 
   > 
6. Fare clic su **salvare** manifesto hello toosave. Web che API è ora configurato toobe utilizzato da altre applicazioni nella directory.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>API web di hello tooverify è esposto tooother applicazioni nella directory
1. Scegliere dal menu superiore hello **registrazioni di App**selezionare hello desiderato dell'applicazione client si desidera tooconfigure accesso toohello web API e passa a pannello impostazioni toohello.
2. Da hello **autorizzazioni obbligatorie** selezionare hello web API che è stata appena esposta un'autorizzazione per. Dal menu a discesa hello autorizzazioni delegate, selezionare nuova autorizzazione hello.

![Visualizzazione di autorizzazioni Elenco azioni](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Ulteriori informazioni sul manifesto dell'applicazione hello
manifesto dell'applicazione Hello funge effettivamente da un meccanismo per aggiornare l'entità applicazione hello, che definisce tutti gli attributi della configurazione di identità di un'applicazione Azure AD, inclusi gli ambiti di accesso API hello descritto. Per ulteriori informazioni sulle entità applicazione hello, vedere hello [documentazione entità applicazione API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). In essa contenuti, informazioni di riferimento complete su hello entità membri utilizzati toospecify autorizzazioni per l'applicazione per l'API:  

* il membro appRoles Hello, che è una raccolta di [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) entità che possono essere utilizzati toodefine hello **autorizzazioni applicazione** per un'API web  
* il membro oauth2Permissions Hello, che è una raccolta di [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) entità che possono essere utilizzati toodefine hello **autorizzazioni delegate** per un'API web

Per ulteriori informazioni sull'applicazione concetti manifesti in generale, fare riferimento troppo[manifesto dell'applicazione Azure Active Directory di conoscenza hello](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>L'accesso a hello Graph di Azure AD e Office 365 tramite le API di Microsoft Graph  
Come API precedente, inoltre l'accesso tooexposing/menzionate nelle applicazioni di risorsa, è inoltre possibile aggiornare il tooaccess applicazione client API esposte dalle risorse di Microsoft.  Hello Microsoft Graph API, che viene chiamato "Microsoft Graph" nell'elenco di hello di autorizzazioni tooother applicazioni, è disponibile o tutte le applicazioni che sono registrate con Azure AD. Se si sta registrando l'applicazione client in un tenant di Azure AD a cui è stato eseguito il provisioning da Office 365, è possibile accedere anche le autorizzazioni di hello esposte dall'API di Microsoft Graph toovarious risorse di Office 365 hello.

Per una discussione completa per gli ambiti di accesso esposti dall'API di Microsoft Graph, vedere hello [gli ambiti di autorizzazione | Concetti relativi all'API di Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes) articolo.

> [!NOTE]
> A causa di limitazione attuale tooa, possono chiamare solo le applicazioni client native hello API Azure AD Graph se usano una autorizzazione "Accesso alla directory dell'organizzazione" hello.  Questa restrizione non è valida per le applicazioni Web.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Configurazione di applicazioni multi-tenant
Quando si aggiunge un tooAzure applicazione Active Directory, è consigliabile toobe l'applicazione accessibile solo agli utenti dell'organizzazione. In alternativa, è opportuno toobe l'applicazione accede agli utenti di organizzazioni esterne. Questi due tipi applicazione sono chiamate applicazioni single-tenant e applicazioni multi-tenant. È possibile modificare la configurazione hello di un toomake applicazione single-tenant è un'applicazione multi-tenant, che in questa sezione vengono illustrate di seguito.

È importante toonote hello differenze un'applicazione multi-tenant e un singolo tenant:  

* Un'applicazione single-tenant è destinata all'uso in un'organizzazione. In genere si tratta di un'applicazione line-of-business scritte da uno sviluppatore aziendale. Un'applicazione single-tenant deve solo toobe accedere gli utenti in una directory e di conseguenza, è necessario solo toobe il provisioning in una directory.
* Un'applicazione multi-tenant è destinata all'uso in più organizzazioni. Si tratta di un'applicazione Web SaaS (Software-as-a-Service) scritta in genere da un fornitore di software indipendente (ISV). Applicazioni multi-tenant necessario toobe eseguito il provisioning in ogni directory in cui verranno utilizzati, che richiede tooregister consenso utente o un amministratore li, supportati tramite il framework di consenso hello Azure AD. Si noti che tutte le applicazioni client native multi-tenant per impostazione predefinita quando vengono installati nel dispositivo del proprietario della risorsa hello. Vedere hello Panoramica di hello sezione il Framework di consenso per altre informazioni sul framework di consenso hello.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Abilitazione degli utenti esterni toogrant risorse tootheir di accesso dell'applicazione
Se si scrive un'applicazione che si desidera toomake tooyour disponibili clienti o partner all'esterno dell'organizzazione, è necessario tooupdate definizione dell'applicazione hello in hello portale di Azure.

> [!NOTE]
> Se si abilita il multi-tenant, è necessario assicurarsi che l'URI ID app dell'applicazione faccia parte di un dominio verificato. Inoltre, hello Return URL deve iniziare con https://. Per altre informazioni, vedere [Oggetti applicazione e oggetti entità servizio](active-directory-application-objects.md).
> 
> 

tooenable app tooyour di accesso per gli utenti esterni: 

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. Dal pannello impostazioni hello, fare clic su **proprietà** e hello capovolto **con Multi-tenant** passare troppo**Sì**.

Dopo avere apportato hello modificare sopra, utenti e amministratori di altre organizzazioni sarà in grado di toogrant directory tootheir di accesso dell'applicazione e altri dati.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Framework di consenso di Azure AD hello in fase di esecuzione di trigger
framework di consenso hello toouse, le applicazioni client di multi-tenant devono richiedere l'autorizzazione mediante OAuth 2.0. [Esempi di codice](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) sono tooshow disponibile come un'applicazione web, l'applicazione nativa o autorizzazione richieste di applicazioni server/daemon codici e accedere ai token toocall le API web.

L'applicazione Web può offrire anche un'esperienza di iscrizione agli utenti. Se si offre un'esperienza di iscrizione, è previsto che l'utente hello farà clic su un pulsante di iscrizione che reindirizzamento hello browser toohello OAuth 2.0 di Azure AD autorizzare endpoint o un endpoint userinfo OpenID Connect. Questi endpoint consentono hello applicazione tooget informazioni nuovo utente hello controllando id_token hello. Fase di iscrizione hello in seguito verrà visualizzata con un toohello simile prompt consenso illustrato in precedenza in hello Panoramica di hello sezione il Framework di consenso utente hello.

In alternativa, l'applicazione web può inoltre offrire un'esperienza che consente agli amministratori troppo "iscrivere la propria società". Questa esperienza anche reindirizza toohello utente hello Azure AD OAuth 2.0 autorizza un endpoint. In questo caso, tuttavia, si passa un prompt dei comandi = admin_consent toohello parametro autorizzare endpoint tooforce hello amministratore esperienza di consenso, in cui hello amministratore concederà il consenso per conto della propria organizzazione. Solo un utente che esegue l'autenticazione con un account appartenente al ruolo amministratore globale toohello può fornire il consenso; altri verrà visualizzato un errore. Volta concesso il consenso, risposta hello conterrà admin_consent = true. Quando si Riscatta un token di accesso, verrà visualizzato anche un id_token che fornisce informazioni sull'organizzazione hello e amministratore hello che effettuato l'iscrizione per l'applicazione.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Abilitazione della concessione implicita OAuth 2.0 per le applicazioni a singola pagina
Singola pagina dell'applicazione (stabilimenti termali) sono in genere strutturate con un front-end JavaScript con intensa attività che viene eseguita nel browser hello, che chiama tooperform di back-end web API dell'applicazione hello la logica di business. Per stabilimenti termali ospitati in Azure AD, usare l'utente di concessione implicita OAuth 2.0 tooauthenticate hello con Azure AD e ottenere un token che è possibile utilizzare toosecure richiama da tooits di client dell'applicazione hello JavaScript API web di fine. Dopo che l'utente hello ha concesso il consenso, questo stesso protocollo di autenticazione può essere utilizzato tooobtain token toosecure chiamate tra il client hello e altre risorse di API web configurati per l'applicazione hello. toolearn ulteriori informazioni su Concedi autorizzazione implicita hello e decidere se è adatta per lo scenario di applicazione, vedere [hello conoscenza implicita OAuth2 concedere del flusso di Azure Active Directory ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Per impostazione predefinita, la concessione implicita OAuth 2.0 è disabilitata per le applicazioni. È possibile abilitare concessione implicita OAuth 2.0 per l'applicazione hello impostazione `oauth2AllowImplicitFlow` valore nel relativo [manifesto dell'applicazione](active-directory-application-manifest.md), ovvero un file JSON che rappresenta la configurazione di identità dell'applicazione.

#### <a name="tooenable-oauth-20-implicit-grant"></a>concessione implicita OAuth 2.0 tooenable
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. Dalla pagina dell'applicazione hello, fare clic su **manifesto** editor del manifesto tooopen hello inline.
   Individuare e impostare il valore di "oauth2AllowImplicitFlow" hello troppo "true". Per impostazione predefinita il valore è "false".
   
    `"oauth2AllowImplicitFlow": true,`
5. Salvare il manifesto hello aggiornato. Dopo il salvataggio, web che API è ora configurato utenti tooauthenticate di toouse concessione implicita OAuth 2.0.


## <a name="removing-an-application"></a>Rimozione di un'applicazione
In questa sezione viene descritto come tooremove un'applicazione di Azure AD del tenant.

### <a name="removing-an-application-authored-by-your-organization"></a>Rimozione di un'applicazione autorizzata dall'organizzazione
Si tratta di applicazioni di hello visualizzati nell'area filtro "Applicazioni proprietà dell'azienda" hello nella pagina principale del "Applicazioni" hello per tenant di Azure AD. In termini tecnici, queste sono applicazioni che è stato registrato manualmente tramite hello portale di Azure classico, o a livello di programmazione tramite PowerShell o hello API Graph. Più precisamente, sono rappresentate sia da un oggetto applicazione che da un oggetto entità servizio nel tenant. Per altre informazioni, vedere [Oggetti applicazione e oggetti entità servizio](active-directory-application-objects.md) .

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>un'applicazione single-tenant dalla directory tooremove
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. Dalla pagina dell'applicazione hello, fare clic su **eliminare**.
5. Fare clic su **Sì** nel messaggio di conferma hello.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>un'applicazione multi-tenant dalla directory tooremove
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere il tenant di Azure AD selezionando l'account in hello angolo superiore destro della pagina hello.
3. Scegliere dal menu superiore, hello **Azure Active Directory**, fare clic su **registrazioni di App**, quindi fare clic su un'applicazione hello desiderato tooconfigure. Questa verrà visualizzata la pagina di avvio rapido dell'applicazione toohello, nonché aprire il pannello impostazioni hello per un'applicazione hello.
4. Scegliere dal pannello impostazioni hello, **proprietà** e hello capovolto **con Multi-tenant** passare troppo**n**. Ciò consente di convertire l'applicazione toobe single-tenant, ma un'applicazione hello rimarrà in un'organizzazione che ha già concesso il consenso tooit.
5. Fare clic su hello **eliminare** pulsante dalla pagina dell'applicazione hello.
6. Fare clic su **Sì** nel messaggio di conferma hello.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Rimozione di un'applicazione multi-tenant autorizzata da un'altra organizzazione
Si tratta di un subset delle applicazioni di hello visualizzati nell'area filtro "Applicazioni usate dall'azienda" hello nella pagina principale "applicazioni" hello per tenant di Azure AD, in particolare quelli che non sono elencate nell'elenco "Applicazioni proprietà dell'azienda" hello di hello. In termini tecnici, si tratta di applicazioni multi-tenant registrate durante il processo di consenso hello. Più precisamente, sono rappresentate solo da un oggetto entità servizio. Per altre informazioni, vedere [Oggetti applicazione e oggetti entità servizio](active-directory-application-objects.md) .

Amministratore della società hello deve avere un accesso di tooremove sottoscrizione di Azure tramite il portale di Azure hello in ordine tooremove directory tooyour di accesso di un'applicazione multi-tenant (dopo avere concesso il consenso). In alternativa, amministratore della società hello può utilizzare hello [i cmdlet di Azure AD PowerShell](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove accesso.

## <a name="next-steps"></a>Passaggi successivi
* Vedere hello [linee guida sulla personalizzazione per le app integrata](active-directory-branding-guidelines.md) per suggerimenti su indicazioni visive per l'app.
* Per ulteriori informazioni sulla relazione hello tra gli oggetti applicazione e dell'entità servizio dell'applicazione, vedere [oggetti applicazione e oggetti entità servizio](active-directory-application-objects.md).
* vedere toolearn ulteriori informazioni su hello ruolo hello app manifesto viene riprodotto [manifesto dell'applicazione di conoscenza hello Azure Active Directory](active-directory-application-manifest.md)
* Vedere hello [glossario di Azure AD per sviluppatori](active-directory-dev-glossary.md) per le definizioni di alcuni dei concetti di hello per sviluppatori di Azure Active Directory (AD).
* Visitare hello [manuale dello sviluppatore di Active Directory](active-directory-developers-guide.md) per una panoramica dello sviluppatore di tutti i relativi contenuti.

