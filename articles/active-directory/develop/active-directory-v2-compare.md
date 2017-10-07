---
title: "aaaWhat è diverso in endpoint v 2.0 di Azure AD hello? | Microsoft Docs"
description: Un confronto tra hello originale Azure AD e gli endpoint di hello v 2.0.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Che cos'è diverso su endpoint v 2.0 hello?
Se si ha familiarità con Azure Active Directory o sono integrate le app con Azure AD in hello precedente, possono essere presenti alcune differenze nell'endpoint v 2.0 hello che non è normalmente.  Questo documento descrive tali differenze per una maggiore comprensione da parte dell'utente.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Account Microsoft e account Azure AD
endpoint di Hello v 2.0 consentono agli sviluppatori di App toowrite che accettano Accedi dagli Accounts di Microsoft Azure AD account e, utilizzando un endpoint singolo auth.  In questo modo si hello toowrite possibilità completamente account indipendente; l'app è possibile che non riconosce il tipo di hello di hello utente esegue l'accesso con account.  Naturalmente, si *possibile* rendere la tua app tenere presente il tipo di hello dell'account viene utilizzato in una determinata sessione, ma non è necessario.

Ad esempio, se l'app chiama hello [Microsoft Graph](https://graph.microsoft.io), alcune funzionalità aggiuntive e i dati saranno utenti tooenterprise disponibili, ad esempio i siti di SharePoint o i dati di Directory.  Ma per molte azioni, ad esempio [la lettura di posta elettronica dell'utente](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), codice hello può essere scritti esattamente hello uguale per gli account Microsoft Accounts sia Azure AD.  

L'integrazione dell'app con account Microsoft e Azure AD è ora un processo semplice.  È possibile utilizzare un singolo set di endpoint, una singola libreria e una singola app registrazione toogain accesso tooboth hello aziendali e tecnologie.  toolearn hello v 2.0 endpoint, estrarre ulteriori informazioni sugli [hello Panoramica](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Nuovo portale di registrazione delle app
un'applicazione che funziona con endpoint v 2.0 hello tooregister, è necessario utilizzare un nuovo portale di registrazione di app: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Si tratta di hello portale in cui è possibile ottenere un ID applicazione, personalizzare l'aspetto di hello della pagina di accesso dell'applicazione e altro ancora.  È sufficiente portale hello tooaccess è un account Microsoft con tecnologia - account personale o dell'istituto di istruzione/lavoro.

## <a name="one-app-id-for-all-platforms"></a>ID app univoco per tutte le piattaforme
Se si usa Azure Active Directory, è possibile che siano state registrate più app diverse per un unico progetto.  Ad esempio, se è stata compilata sia un sito Web e un'app iOS, è necessario tooregister li separatamente, con due ID applicazione diverso. portale di registrazione Hello Azure AD app forzato questa distinzione è toomake durante la registrazione:

![Interfaccia utente della registrazione dell'applicazione precedente](../../media/active-directory-v2-flows/old_app_registration.PNG)

Analogamente, se si disponeva di un sito Web e di un'API Web back-end, è possibile che ogni elemento sia stato registrato come un'app separata in Azure AD.  In alternativa, se si disponeva di un'app per iOS e di un'app per Android, è possibile che siano state registrate due app diverse.  La registrazione di ogni componente di un'applicazione ha portato toosome comportamenti imprevisti per gli sviluppatori e i relativi clienti:

* Ogni componente visualizzate come un'applicazione separata nel tenant di Azure Active Directory hello di ogni cliente.
* Quando un amministratore tenant tentato tooapply criteri per gestire l'accesso a o eliminare un'app, hanno toodo in questo caso per ogni componente dell'applicazione hello.
* Quando i clienti acconsentito tooan applicazione, ogni componente viene visualizzato nella schermata di consenso hello come applicazione distinta.

Con endpoint v 2.0 hello, è ora possibile registrare tutti i componenti del progetto come una registrazione singola app e usare un singolo Id applicazione per l'intero progetto.  È possibile aggiungere diversi tooa "piattaforme" ogni progetto e fornire le informazioni necessarie hello per ogni piattaforma che aggiunti.  Naturalmente, è possibile creare quante più App come si desidera che a seconda dei requisiti, ma per la maggior parte di hello dei casi, un solo Id applicazione deve essere necessarie.

Il nostro obiettivo è che verrà portano tooa più semplificato la gestione delle app e l'esperienza di sviluppo e creare una visualizzazione consolidata più di un singolo progetto se si lavora su.

## <a name="scopes-not-resources"></a>Ambiti e non risorse
In Azure Active Directory un'app può comportarsi come una **risorsa** o come un destinatario di token.  Una risorsa è possibile definire un numero di **ambiti** o **oAuth2Permissions** che riconosce, consentendo di risorse di toothat toorequest token per un determinato set di ambiti di applicazioni client.  Si consideri l'API di Azure AD Graph hello come un esempio di una risorsa:

* Identificatore della risorsa o `AppID URI`: `https://graph.windows.net/`
* Ambiti o `OAuth2Permissions`: `Directory.Read`, `Directory.Write` e così via  

Tutto ciò vale per l'endpoint di hello hello v 2.0.  Un'app può comunque comportarsi come una risorsa, definire gli ambiti ed essere identificata da un URI.  Le applicazioni client possono richiedere ancora gli ambiti di accesso toothose.  Tuttavia, il modo di hello in cui un client richiede tali autorizzazioni è stato modificato.  In hello precedente, un OAuth 2.0 autorizzare tooAzure richiesta AD stato simile:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

in cui hello **risorse** parametro indicato richiede l'autorizzazione per quali app client hello di risorse.  Azure AD calcolato autorizzazioni hello richieste dall'applicazione hello in base alla configurazione statico nel portale di Azure hello e token emessi, di conseguenza.  A questo punto, hello stesso OAuth 2.0 autorizzare richiesta ha un aspetto simile:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

in cui hello **ambito** parametro indica quale app hello risorsa e le autorizzazioni richiede l'autorizzazione per. Hello desiderato risorsa è ancora molto presente nella richiesta di hello - semplicemente è stato incluso in ognuno dei valori di hello del parametro di ambito hello.  Utilizzando il parametro di ambito hello in questo modo consente più conformi alla specifica OAuth 2.0 hello hello v 2.0 endpoint toobe e più strettamente allineato consigliate comuni.  Consente inoltre di App tooperform [consenso incrementale](#incremental-and-dynamic-consent), descritto nella sezione successiva hello.

## <a name="incremental-and-dynamic-consent"></a>Consenso incrementale e dinamico
App registrato in Azure AD necessari in precedenza toospecify dispongono delle autorizzazioni necessarie di OAuth 2.0 in hello portale di Azure, al momento della creazione di app:

![Interfaccia utente della registrazione delle autorizzazioni](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

un'app necessarie sono state configurate le autorizzazioni di Hello **staticamente**.  Anche se questa configurazione di hello app tooexist consentiti nel portale di Azure hello e mantenuta codice hello utile e semplice, presenta alcuni problemi per gli sviluppatori:

* Un'app aveva tooknow tutte hello autorizzazioni è necessario in fase di creazione di app.  La possibilità di aggiungere le autorizzazioni in fasi successive era un processo difficile.
* Un'app aveva tooknow tutte le risorse di hello mai acceda anticipatamente.  È difficile toocreate App che accedono a un numero arbitrario di risorse.
* Un'app aveva toorequest tutte le autorizzazioni di hello che sarebbe necessario al momento hello del primo accesso dell'utente.  In alcuni casi ciò ha portato tooa molto lungo elenco di autorizzazioni che gli utenti finali di approvazione accesso dell'applicazione hello Accedi iniziale sconsigliato.

Con l'endpoint di hello v 2.0, è possibile specificare autorizzazioni hello esigenze app **dinamicamente**, in fase di esecuzione durante il normale utilizzo dell'app.  toodo in tal caso, è possibile specificare hello definisce l'ambito delle esigenze di app in qualsiasi punto nel tempo includendoli in hello `scope` parametro di una richiesta di autorizzazione:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Hello precedente richiede l'autorizzazione per hello app tooread un utente di Azure AD directory dati, nonché directory tootheir di scrittura dei dati.  Se l'utente di hello ha acconsentito autorizzazioni toothose in hello precedente per questa app specifica, sarà sufficiente immettere le proprie credenziali e accedere ad app hello.  Se l'utente hello non ha accettato le condizioni tooany queste autorizzazioni, endpoint v 2.0 hello chiederà utente hello per le autorizzazioni toothose consenso.  toolearn altre, è possibile leggere fino in [ambiti, autorizzazione e autorizzazioni](active-directory-v2-scopes.md).

Consentire a un'app toorequest autorizzazioni in modo dinamico tramite hello `scope` parametro consente di effettuare un controllo completo esperienza dell'utente.  Se si desidera, è possibile scegliere toofrontload il consenso dell'utente esperienza e chiedere di tutte le autorizzazioni in una richiesta di autorizzazione iniziale.  O se l'app richiede un numero elevato di autorizzazioni, è possibile scegliere toogather tali autorizzazioni utente hello in modo incrementale, come tentano toouse determinate funzionalità dell'app nel tempo.

## <a name="well-known-scopes"></a>Ambiti conosciuti
#### <a name="offline-access"></a>Accesso offline
Le app usando endpoint v 2.0 hello uso può essere necessario hello di una nuova autorizzazione nota per le app - hello `offline_access` ambito.  Tutte le app saranno necessario toorequest questa autorizzazione se sono richieste risorse tooaccess per conto di hello di un utente per un periodo prolungato di tempo, anche quando l'utente hello potrebbe non essere attivamente usando hello app.  Hello `offline_access` ambito verrà visualizzato come utente toohello in consenso dialogs "Accedere ai dati non in linea", l'utente che ha hello deve accettare.  Richiedente hello `offline_access` autorizzazione abiliterà il tooreceive app web OAuth 2.0 refresh_tokens dall'endpoint di hello v 2.0.  I token di aggiornamento hanno una durata elevata e possono essere scambiati con nuovi token di accesso di OAuth 2.0 per periodi prolungati di accesso.  

Se l'app non viene richiesta hello `offline_access` ambito, non riceverà refresh_tokens.  Ciò significa che quando si Riscatta un authorization_code nel flusso di codice di autorizzazione OAuth 2.0 hello, si riceveranno solo nuovamente access_token da hello `/token` endpoint.  Tale token di accesso rimarrà valido per un breve periodo di tempo (in genere un'ora), per poi scadere.  A questo punto nel tempo, necessarie per l'app tooredirect hello utente indietro toohello `/authorize` tooretrieve endpoint authorization_code una nuova.  Durante questo reindirizzamento, utente hello può o non venga necessario tooenter nuovamente le proprie credenziali o nuovamente consenso toopermissions, in base al tipo di hello hello di app.

altre informazioni sull'estrazione OAuth 2.0, refresh_tokens e access_tokens, hello toolearn [riferimento al protocollo v 2.0](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, profilo e indirizzo di posta elettronica
In passato, hello più elementare OpenID Connect flusso di accesso con Azure Active Directory fornisce una serie di informazioni sull'utente hello in id_token risultante hello.  le attestazioni Hello in un id_token possono includere nome dell'utente hello, username preferito, indirizzo di posta elettronica, ID di oggetto e altro ancora.

È ora limitazione informazioni hello che hello sono `openid` ambito consente all'app l'accesso a.  ambito 'openid' Hello solo consentire all'utente di hello app toosign in e un identificatore specifico dell'app per utente hello di ricezione.  Se si desiderano tooobtain informazioni personali (PII) sull'utente hello nell'app, necessarie per l'app toorequest ulteriori autorizzazioni utente hello.  Microsoft sta introducendo due nuovi ambiti: hello `email` e `profile` ambiti, che consentono di toodo così.

Hello `email` ambito è molto semplice: consente l'indirizzo di posta elettronica principale dell'utente le app accesso toohello tramite hello `email` id_token hello di attestazione.  Hello `profile` ambito mette a disposizione il tooall accesso app altre informazioni di base sull'utente hello-loro nome, nome utente preferito, ID di oggetto e così via.

In questo modo è toocode l'app in maniera minima riservatezza: è possibile solo richiedere utente hello set hello di informazioni che l'app richiede toodo relativo processo.  Per ulteriori informazioni su questi ambiti, vedere troppo[hello riferimento a un ambito v 2.0](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Attestazioni nei token
Hello attestazioni nei token rilasciati da endpoint v 2.0 hello non saranno identici tootokens emesso dagli endpoint di Azure AD in genere disponibili hello - migrazione toohello nuovo servizio App non deve presupporre che un'attestazione specifica sarà disponibile in id_tokens o access_tokens. toolearn sulle attestazioni specifiche di hello generato nei token v 2.0, vedere hello [riferimento token v 2.0](active-directory-v2-tokens.md).

## <a name="limitations"></a>Limitazioni
Esistono alcune restrizioni toobe considerare quando si utilizza punto v 2.0 hello.  Consultare toohello [doc limitazioni v 2.0](active-directory-v2-limitations.md) toosee se uno qualsiasi di queste restrizioni si applicano tooyour particolare scenario.
