---
title: aaaUse tooaccess l'autenticazione di Azure AD API di servizi multimediali di Azure con .NET | Documenti Microsoft
description: Questo argomento viene illustrato come toouse tooaccess l'autenticazione di Azure Active Directory (Azure AD) di Azure Media Services API (AMS) con .NET.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Utilizzare l'autenticazione di Azure AD tooaccess API di servizi multimediali di Azure con .NET

A partire da windowsazure.mediaservices 4.0.0.4, Servizi multimediali di Azure supporta l'autenticazione basata su Azure Active Directory (Azure AD). In questo argomento illustra come toouse tooaccess l'autenticazione di Azure AD API di servizi multimediali di Azure con Microsoft .NET.

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Account di Servizi multimediali. Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).
- versione più recente Hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacchetto.
- Familiarità con l'argomento hello [accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Quando si usa l'autenticazione di Azure AD con Servizi multimediali di Azure, è possibile eseguire l'autenticazione in uno di due modi:

- **Autenticazione utente** autentica un utente hello app toointeract con risorse di servizi multimediali di Azure. applicazione interattiva Hello deve prima richiedere le credenziali utente hello. Un esempio è un'applicazione console di gestione che viene utilizzata dagli utenti autorizzati toomonitor processi di codifica o di streaming live. 
- L'**autenticazione basata su un'entità servizio** consente di eseguire l'autenticazione di un servizio. Le applicazioni che usano in genere questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati, ad esempio app Web, app per le funzioni, app per la logica, API o microservizi.

>[!IMPORTANT]
>Attualmente, Servizi multimediali di Azure supporta un modello di autenticazione di Servizio di controllo di accesso Azure. Tuttavia, autorizzazione di controllo di accesso verrà deprecato in 1 giugno 2018 toobe. È consigliabile eseguire la migrazione di modello di autenticazione di Azure Active Directory tooan appena possibile.

## <a name="get-an-azure-ad-access-token"></a>Ottenere un token di accesso di Azure AD

tooconnect toohello API di servizi multimediali di Azure con autenticazione di Azure AD, hello client app deve toorequest un token di accesso di Azure AD. Quando si utilizza client .NET di servizi multimediali hello SDK, molti dei dettagli di hello sul tooacquire un token di accesso di Azure AD vengono incapsulati e semplificato per l'utente in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) e [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classi. 

Ad esempio, non è necessario tooprovide hello Azure AD autorità, URI di risorsa di servizi multimediali oppure nativo dettagli dell'applicazione Azure AD. Questi sono valori noti che sono già configurati per hello classe provider di token di accesso AD Azure. 

Se non si utilizza .NET SDK servizi multimediali di Azure, è consigliabile utilizzare hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md). vedere tooget valori per parametri hello necessari toouse con Azure AD Authentication Library [utilizzare impostazioni di autenticazione tooaccess portale Azure AD Azure hello](media-services-portal-get-started-with-aad.md).

È inoltre possibile hello sostituire l'implementazione predefinita di hello di hello **AzureAdTokenProvider** con la propria implementazione.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Installare e configurare l'SDK .NET di Servizi multimediali di Azure

>[!NOTE] 
>autenticazione toouse Azure AD con hello Media Services .NET SDK, è necessario toohave hello più recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacchetto. Inoltre, aggiungere un riferimento toohello **ActiveDirectory** assembly. Se si utilizza un'app esistente, includere hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly. 

1. Creare una nuova applicazione console C# in Visual Studio.
2. Hello utilizzare [windowsazure. mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall pacchetto NuGet **Azure Media Services .NET SDK**. 

    tooadd riferimenti utilizzando NuGet, richiedere hello alla procedura seguente: in **Esplora**, nome del progetto hello e quindi scegliere **Gestione pacchetti NuGet**. Cercare quindi **windowsazure.mediaservices** e fare clic su **Installa**.
    
    -oppure-

    Esecuzione hello il seguente comando in **Package Manager Console** in Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Aggiungere **utilizzando** tooyour il codice sorgente.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Usare l'autenticazione utente

tooconnect toohello API del servizio di supporto di Azure con l'opzione di autenticazione utente hello, hello client app deve toorequest un token di Azure AD tramite hello seguenti parametri:  

- Endpoint tenant di Azure AD. le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure. Passare il mouse su hello utente connesso nell'angolo superiore destro di hello.
- URI di risorsa per Servizi multimediali.
- ID client dell'applicazione Servizi multimediali (nativa). 
- URI di reindirizzamento dell'applicazione Servizi multimediali (nativa). 

i valori Hello per questi parametri possono essere disponibili nella **AzureEnvironments.AzureCloudEnvironment**. Hello **AzureEnvironments.AzureCloudEnvironment** costante è un supporto in hello .NET SDK tooget impostazioni delle variabili di ambiente destra hello per un Data Center di Azure pubblico. 

Contiene le impostazioni di ambiente predefinite per l'accesso a servizi multimediali di hello solo i centri dati pubblici. Per le regioni cloud sovrane o governative è possibile usare rispettivamente **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvironment** o **AzureGermanCloudEnvironment**.

Hello esempio di codice seguente viene creato un token:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart programmazione in servizi multimediali, è necessario toocreate un **CloudMediaContext** istanza che rappresenta il contesto di server hello. Hello **CloudMediaContext** include riferimenti tooimportant insiemi inclusi i processi, asset, file, i criteri di accesso e localizzatori. 

È inoltre necessario hello toopass **URI per i servizi REST di supporti della risorsa** toohello **CloudMediaContext** costruttore. URI della risorsa hello tooget per i servizi REST di supporti, accedi toohello portale di Azure, selezionare l'account di servizi multimediali di Azure, selezionare **l'accesso all'API**, quindi selezionare **la connessione di servizi multimediali tooAzure con l'utente autenticazione**. 

Hello codice seguente viene creato un **CloudMediaContext** istanza:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Hello di esempio seguente viene illustrato come toocreate hello il contesto di token e hello Azure AD:

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Se si verifica un'eccezione che indica "server remoto hello ha restituito un errore: non autorizzato (401)," hello vedere [il controllo degli accessi](media-services-use-aad-auth-to-access-ams-api.md#access-control) sezione di accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AD Azure.

## <a name="use-service-principal-authentication"></a>Usare l'autenticazione basata su entità servizio
    
tooconnect toohello API di servizi multimediali di Azure con l'opzione dell'entità servizio di hello, l'applicazione di livello intermedio (API web o applicazione web) con, è necessario un token di Azure AD toorequests hello seguenti parametri:  

- Endpoint tenant di Azure AD. le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure. Passare il mouse su hello utente connesso nell'angolo superiore destro di hello.
- URI di risorsa per Servizi multimediali.
- I valori dell'applicazione Azure AD: hello **ID Client** e **segreto Client**.

i valori per hello Hello **ID Client** e **segreto Client** parametri è reperibile nel portale di Azure hello. Per ulteriori informazioni, vedere [Introduzione a Azure AD mediante l'autenticazione hello Azure portal](media-services-portal-get-started-with-aad.md).

Hello esempio di codice seguente crea un token tramite hello **AzureAdTokenCredentials** costruttore che accetta **AzureAdClientSymmetricKey** come parametro: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

È inoltre possibile specificare hello **AzureAdTokenCredentials** costruttore che accetta **AzureAdClientCertificate** come parametro. 

Per istruzioni su come toocreate e configurare un certificato in un formato che può essere utilizzato da Azure AD, vedere [tooAzure AD App daemon con certificati - passaggi di configurazione manuale di autenticazione](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart programmazione in servizi multimediali, è necessario toocreate un **CloudMediaContext** istanza che rappresenta il contesto di server hello. È inoltre necessario hello toopass **URI per i servizi REST di supporti della risorsa** toohello **CloudMediaContext** costruttore. È possibile ottenere hello **URI per i servizi REST di supporti della risorsa** valore hello anche portale di Azure.

Hello codice seguente viene creato un **CloudMediaContext** istanza:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Hello di esempio seguente viene illustrato come toocreate hello il contesto di token e hello Azure AD:

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Passaggi successivi

Introduzione a [caricamento file account tooyour](media-services-dotnet-upload-files.md).
