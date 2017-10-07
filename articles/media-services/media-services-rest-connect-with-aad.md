---
title: aaaUse tooaccess l'autenticazione di Azure AD API di servizi multimediali di Azure con REST | Documenti Microsoft
description: Informazioni su come tooaccess API di servizi multimediali di Azure con l'autenticazione di Azure Active Directory tramite REST.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Usare Azure AD authentication tooaccess hello Azure API dei servizi multimediali con REST

il team di servizi multimediali di Azure Hello è stata rilasciata a supporto dell'autenticazione di Azure Active Directory (Azure AD) per l'accesso a servizi multimediali di Azure. Inoltre annunciato piani toodeprecate Access Control di Azure l'autenticazione del servizio per l'accesso a servizi multimediali. Poiché ogni sottoscrizione di Azure e ogni account di servizi multimediali è tenant tooan collegato AD Azure, supporto per l'autenticazione di Azure AD offre diversi vantaggi di sicurezza. Per informazioni dettagliate su questa modifica e la migrazione (se si utilizza hello Media Services .NET SDK per app), vedere l'esempio hello post di blog e articoli:

- [Azure Media Services announces support for Azure AD and deprecation of Access Control authentication](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation) (Servizi multimediali di Azure annuncia il supporto per Azure AD e dichiara deprecata l'autenticazione del servizio Controllo di accesso)
- [Access Azure Media Services API by using Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md) (Accedere all'API Servizi multimediali di Microsoft Azure tramite l'autenticazione di Azure AD)
- [Usare l'autenticazione di Azure AD tooaccess API di servizi multimediali di Azure con Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Introduzione ad Azure AD authentication utilizzando hello portale di Azure](media-services-portal-get-started-with-aad.md)

Alcuni clienti necessario toodevelop le relative soluzioni di servizi multimediali in hello seguenti vincoli:

*   Utilizzano un linguaggio di programmazione che non è Microsoft .NET o Visual c# o l'ambiente di runtime hello non è Windows.
*   Librerie di Azure AD, ad esempio librerie di autenticazione di Active Directory non sono disponibili per hello linguaggio di programmazione o non possono essere utilizzate per il proprio ambiente di runtime.

Alcuni clienti hanno sviluppato applicazioni tramite l'API REST sia per l'autenticazione del servizio Controllo di accesso che per l'accesso a Servizi multimediali di Microsoft Azure. In questi casi, è necessario un hello solo toouse modo API REST per l'autenticazione di Azure AD e accedere a servizi multimediali di Azure successive. È necessario toonot si basano su una delle librerie di hello Azure AD o su hello Media Services .NET SDK. Questo articolo descrive una soluzione e offre codice di esempio per questo scenario. Poiché il codice hello tutte le chiamate API REST, senza la dipendenza su qualsiasi AD Azure o libreria di servizi multimediali di Azure, il codice hello può facilmente essere tradotte tooany altro linguaggio di programmazione.

> [!IMPORTANT]
> Attualmente servizi multimediali supporta modello di autenticazione hello Azure Access Control services. L'autenticazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018. Si consiglia di migrare il modello di autenticazione di Azure AD toohello appena possibile.


## <a name="design"></a>Progettazione

In questo articolo, si usa hello dopo l'autenticazione e autorizzazione:

*  Protocollo di autorizzazione: OAuth 2.0. OAuth 2.0 è uno standard di sicurezza Web che riguarda sia l'autenticazione che l'autorizzazione. Questo standard, supportato da Google, Microsoft, Facebook e PayPal, è stato ratificato nell'ottobre 2012. Microsoft supporta stabilmente gli standard OAuth 2.0 e OpenID Connect in diversi servizi e in più librerie client, tra cui Azure Active Directory, Open Web Interface for .NET (OWIN) Katana e le librerie di Azure AD.
*  Tipo di concessione: credenziali client. Le credenziali del client è uno dei tipi di concessione quattro hello in OAuth 2.0. e viene spesso usato per l'accesso all'API Microsoft Graph di Azure AD.
*  Modalità di autenticazione: entità servizio. Hello altre modalità di autenticazione è autenticazione interattivo o utente.

Un totale di quattro applicazioni o servizi sono coinvolti nel flusso di autenticazione e autorizzazione hello Azure AD per l'utilizzo di servizi multimediali. flusso di hello e i servizi e applicazioni Hello sono descritti in hello nella tabella seguente:

|Tipo di applicazione |Applicazione |Flusso|
|---|---|---|
|Client | App o soluzione del cliente | Questa applicazione (in realtà, il proxy) viene registrata nel tenant di Azure AD hello in cui hello Azure media di sottoscrizione e hello risiede l'account di servizio. Hello dell'entità servizio dell'applicazione hello registrato viene quindi concessa con ruolo di proprietario o collaboratore nel controllo di accesso (IAM) dell'account del servizio di supporto hello hello. entità servizio Hello è rappresentato da hello segreto dell'app client ID e client. |
|Provider di identità (IDP) | Azure AD come IDP | entità di servizio app registrato Hello (ID client e il segreto client) è stato autenticato da Azure AD come provider di identità hello. Questa autenticazione viene eseguita internamente e in modo implicito. Come flusso di credenziali client, il client di hello viene autenticato anziché utente hello. |
|Servizio token di sicurezza/Server OAuth | Azure AD come servizio token di sicurezza | Dopo l'autenticazione da IDP hello (o OAuth Server in termini di OAuth 2.0), un token di accesso o JSON Web Token (JWT) viene rilasciato da Azure AD come servizio token di sicurezza/OAuth Server per la risorsa di livello intermedio toohello di accesso: in questo caso, hello endpoint API REST di servizi multimediali. |
|Risorsa | API REST di Servizi multimediali | Ogni chiamata API REST di servizi multimediali è autorizzata da un token di accesso che viene generato da Azure AD come servizio token di sicurezza o server OAuth hello. |

Se si esegue il codice di esempio hello e acquisizione un token di accesso o un token JWT, hello JWT ha hello gli attributi seguenti:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Ecco i mapping di hello tra attributi hello in hello JWT hello quattro applicazioni o servizi nella tabella precedente hello:

|Tipo di applicazione |Applicazione |Attributo JWT |
|---|---|---|
|Client |App o soluzione del cliente |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". ID client Hello di un'applicazione AD tooAzure verrà registrato nella sezione successiva hello. |
|Provider di identità (IDP) | Azure AD come IDP |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Hello GUID è il tenant di ID di Microsoft hello (microsoft.onmicrosoft.com). Ogni tenant ha un proprio ID univoco. |
|Servizio token di sicurezza/Server OAuth |Azure AD come servizio token di sicurezza | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Hello GUID è il tenant di ID di Microsoft hello (microsoft.onmicrosoft.com). |
|Risorsa | API REST di Servizi multimediali |aud: "https://rest.media.azure.net". destinatario Hello o gruppo di destinatari del token di accesso hello. |

## <a name="steps-for-setup"></a>Procedura per la configurazione

tooregister e configurare un'applicazione Azure AD per l'autenticazione di Azure AD e tooobtain un token di accesso per richiamare l'endpoint API REST di servizi multimediali di Azure hello, hello completo alla procedura seguente:

1.  In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), registrare un tenant toohello Azure AD di Azure AD applicazione (ad esempio, wzmediaservice) (ad esempio, microsoft.onmicrosoft.com). È possibile registrare l'applicazione come app Web o come app nativa. È anche possibile scegliere un URL di sign-on e un URL di risposta, ad esempio http://wzmediaservice.com per entrambi.
2. In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), visitare toohello **configura** scheda dell'applicazione. Hello nota **ID client**. quindi in **Chiavi** generare una **chiave client** (segreto client). 

    > [!NOTE] 
    > Prendere nota della chiave privata client hello. Non verrà più visualizzato.
    
3.  In hello [portale di Azure](http://ms.portal.azure.com), visitare l'account di servizi multimediali toohello. Seleziona hello **controllo di accesso** riquadro (IAM). Aggiungere un nuovo membro che ha hello proprietario o collaboratore hello. Per entità di hello, cercare il nome di applicazione hello registrato nel passaggio 1 (in questo esempio, wzmediaservice).

## <a name="info-toocollect"></a>Info toocollect

tooprepare REST per la generazione di codice, raccogliere hello tooinclude punti dati nel codice hello seguenti:

*   Azure AD come endpoint servizio token di sicurezza: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Da questo endpoint si richiede un token di accesso JWT. Inoltre tooserving come un provider di identità, Azure AD funge anche da un servizio token di sicurezza. Azure AD emette un token JWT per l'accesso alle risorse (token di accesso). Un token JWT ha varie attestazioni.
*   API REST di Servizi multimediali di Microsoft come risorsa o gruppo di destinatari: https://rest.media.azure.net.
*   ID client: vedere il passaggio 2 in [Procedura per la configurazione](#steps-for-setup).
*   Segreto client: vedere il passaggio 2 in [Procedura per la configurazione](#steps-for-setup).
*   L'endpoint dell'API REST account servizi multimediali in hello seguente formato:

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    Si tratta hello endpoint in cui tutte le API REST di servizi multimediali vengono effettuate chiamate dell'applicazione. ad esempio, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

È quindi possibile inserire queste cinque parametri nel file Web. config o App. config, toouse nel codice.

## <a name="sample-code"></a>Codice di esempio

È possibile trovare il codice di esempio hello in [autenticazione di Azure AD per l'accesso di Azure Media Services: sia tramite l'API REST](https://github.com/willzhan/WAMSRESTSoln).

codice di esempio Hello è costituito da due parti:

*   Un progetto di libreria DLL che contiene tutto il codice hello API REST di Azure AD autenticazione e autorizzazione. Include inoltre un metodo per effettuare chiamate toohello API REST di servizi multimediali endpoint dell'API REST, con il token di accesso di hello.
*   Un client console di test, che avvia l'autenticazione di Azure AD e chiama un'API REST di Servizi multimediali diversa.

progetto di esempio Hello presenta tre caratteristiche:

*   Autenticazioni AD Azure tramite le credenziali del client hello concedono utilizzando solo hello API REST.
*   Accesso servizi multimediali di Azure utilizzando solo hello API REST.
*   Accesso di archiviazione Azure tramite hello solo l'API REST (come toocreate utilizzato un account di servizi multimediali, tramite l'API REST).


## <a name="where-is-hello-refresh-token"></a>Dove si trova il token di aggiornamento hello?

Potrebbero richiedere alcuni lettori: dove è il token di aggiornamento hello? e perché non venga usato in questo caso.

scopo di Hello di un token di aggiornamento non è un token di accesso toorefresh. In alternativa, è toobypass progettato l'intervento dell'utente o l'autenticazione dell'utente finale e comunque ricevere un token di accesso valido quando scade un token precedente. Un nome più appropriato per un token di aggiornamento potrebbe essere qualcosa di simile a "token di rinnovo dell'accesso con bypass dell'utente".

Se si utilizza hello flusso (nome utente e password, che agisce per conto dell'utente) concedere l'autorizzazione di OAuth 2.0, un token di aggiornamento consente di ottenere un accesso rinnovato token senza richiedere l'intervento dell'utente. Tuttavia, per hello OAuth 2.0 concessione di credenziali client del flusso descritti in questo articolo, il client hello opera per proprio conto. Non è necessario l'intervento dell'utente in tutti, e il server di autorizzazione hello non deve necessariamente troppo (e non) forniscono un token di aggiornamento. Se si esegue il debug hello **GetUrlEncodedJWT** metodo, si nota che la risposta hello dall'endpoint token hello ha un token di accesso, ma nessun token di aggiornamento.

## <a name="next-steps"></a>Passaggi successivi

Introduzione a [caricamento file account tooyour](media-services-dotnet-upload-files.md).
