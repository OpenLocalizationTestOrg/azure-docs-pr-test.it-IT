---
title: aaaConnecting tooMedia servizi Account usando .NET
description: Questo argomento viene illustrato come tooconnect tooMedia servizi abbonamento .NET.
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Connessione tooMedia Account Services con Media Services SDK per .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

In questo argomento viene descritto come tooobtain tooMicrosoft una connessione a livello di codice servizi multimediali di Azure quando si programma con hello Media Services SDK per .NET.

## <a name="connecting-toomedia-services"></a>La connessione di servizi tooMedia
tooconnect tooMedia servizi a livello di codice, è necessario avere già configurato un account Azure, configurato servizi multimediali nell'account e quindi configurare un progetto di Visual Studio per lo sviluppo con hello Media Services SDK per .NET. Per ulteriori informazioni, vedere il programma di installazione per lo sviluppo con hello Media Services SDK per .NET.

Alla fine di hello del processo di installazione di account servizi multimediali hello, ottenuto seguente hello necessari valori di connessione. Utilizzare queste connessioni a livello di codice toomake tooMedia servizi.

* Nome dell'account di Servizi multimediali
* Chiave dell'account di Servizi multimediali

toofind questi valori, visitare il portale di gestione di Azure toohello, selezionare l'account del servizio di supporto e fare clic su hello "**GESTISCI CHIAVI**" sull'icona nella parte inferiore di hello della finestra portale hello. Facendo clic su hello icona Avanti tooeach testo casella copie hello valore toohello Appunti di sistema.

## <a name="creating-a-cloudmediacontext-instance"></a>Creazione di un'istanza di CloudMediaContext
programmazione con Media Services è necessario toocreate toostart un **CloudMediaContext** istanza che rappresenta il contesto di server hello. Hello **CloudMediaContext** include riferimenti tooimportant insiemi inclusi i processi, asset, file, i criteri di accesso e localizzatori.

> [!NOTE]
> Hello **CloudMediaContext** classe non è thread-safe. È quindi necessario creare una nuova istanza di CloudMediaContext per ogni thread o set di operazioni.
> 
> 

CloudMediaContext include cinque overload del costruttore. È consigliato toouse costruttori che accettano **MediaServicesCredentials** come parametro. Per ulteriori informazioni, vedere hello **riutilizzo dei token del servizio controllo di accesso** che segue. 

Hello esempio seguente viene utilizzato un costruttore pubblico CloudMediaContext(MediaServicesCredentials credentials) hello:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Riutilizzo dei token del Servizio di controllo di accesso
In questa sezione viene illustrato come tooreuse Access Control Service token usando CloudMediaContext costruttori che accettano MediaServicesCredentials come parametro.

[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (noto anche come servizio di controllo di accesso o ACS) è un servizio basato su cloud che fornisce un modo semplice di autenticazione e autorizzazione accesso toogain utenti tootheir le applicazioni web. Servizi multimediali di Microsoft Azure controlla l'accesso tooits servizi tramite il protocollo OAuth che richiede un token ACS. Servizi multimediali riceve i token ACS hello da un server di autorizzazione.

Quando si sviluppa con hello Media Services SDK, è possibile scegliere gestiscono toonot token hello perché hello Gestioni codice SDK per è. Tuttavia, consentendo agli sviluppatori di hello SDK gestire completamente le richieste di token ACS hello token lead toounnecessary. Le richieste di token richiede tempo e utilizza risorse di hello client e server. Inoltre, server ACS hello limita le richieste di hello se frequenza hello è troppo alto. limite di Hello è di 30 richieste al secondo, vedere [limitazioni del servizio ACS](https://msdn.microsoft.com/library/gg185909.aspx) per altri dettagli.

A partire da Media Services SDK versione 3.0.0.0 hello, è possibile riutilizzare i token ACS hello. Hello **CloudMediaContext** costruttori che accettano **MediaServicesCredentials** come parametro consentono di token ACS hello condivisione tra più contesti. Hello MediaServicesCredentials classe incapsula le credenziali di servizi multimediali di hello. Se è disponibile un token ACS e l'ora di scadenza è noto, è possibile creare una nuova istanza di MediaServicesCredentials con token hello e passarlo come costruttore toohello di CloudMediaContext. Si noti che hello Media Services SDK Aggiorna automaticamente i token ogni volta che scadono. Esistono due modi i token ACS tooreuse, come illustrato nell'esempio hello riportato di seguito.

* È possibile memorizzare nella cache di hello **MediaServicesCredentials** oggetto in memoria (ad esempio, una variabile di classe statici). Quindi, passare costruttore CloudMediaContext toohello dell'oggetto memorizzato nella cache di hello. oggetto MediaServicesCredentials Hello contiene un token ACS che può essere riutilizzato se è ancora valido. Se il token di hello non è valido, che verrà aggiornato da hello toohello MediaServicesCredentials costruttore utilizzando le credenziali di hello Media Services SDK.
  
    Si noti che hello **MediaServicesCredentials** oggetto Ottiene un token valido dopo hello RefreshToken viene chiamato. Hello **CloudMediaContext** hello chiamate **RefreshToken** metodo hello costruttore. Se si prevede di archiviazione esterna tooan toosave hello i valori del token, prendere toocheck che hello TokenExpiration valore sia valido prima di salvare i dati del token hello. Se non è valido, chiamare RefreshToken prima di procedere alla memorizzazione nella cache.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* È inoltre possibile memorizzare nella cache hello AccessToken valori stringa e hello TokenExpiration. i valori Hello in un secondo momento potrebbe essere utilizzato toocreate MediaServicesCredentials un nuovo oggetto con i dati memorizzati nella cache di hello del token.  Ciò è particolarmente utile per scenari in cui il token hello può essere condiviso in modo sicuro tra più processi o computer.
  
    Hello frammenti di codice seguente chiamano hello metodi SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage e UpdateTokenDataInExternalStorageIfNeeded non definiti in questo esempio. È possibile definire questi metodi toostore, recuperare e aggiornare i dati token in un archivio esterno. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Utilizzare hello salvata token valori toocreate MediaServicesCredentials.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Aggiornare copia token hello nel caso in cui il token hello è stato aggiornato da Media Services SDK hello. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Se si hanno più account di servizi multimediali (ad esempio, per la condivisione del carico o Geo-distribuzione) è possibile memorizzare nella cache oggetti MediaServicesCredentials utilizzo hello System.Collections.Concurrent.ConcurrentDictionary insieme (Buongiorno Raccolta di ConcurrentDictionary rappresenta una raccolta thread-safe di coppie chiave/valore che è possibile accedere contemporaneamente da più thread). È quindi possibile utilizzare le credenziali memorizzate nella cache di hello tooget di hello GetOrAdd (metodo). 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>La connessione di account di servizi multimediali tooa si trova nell'area di hello Cina settentrionale
Se l'account si trova nell'area di hello Cina settentrionale, usare hello costruttore seguente:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

ad esempio:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Archiviazione dei valori di connessione nella configurazione
È un consigliabile toostore connessione valori, particolarmente sensibili, ad esempio il nome dell'account e la password, nella configurazione. Inoltre, si tratta di dati di configurazione sensibili tooencrypt una procedura consigliata. È possibile crittografare hello intero file di configurazione utilizzando hello Windows Encrypting File System (EFS). Selezionare tooenable EFS in un file, il pulsante destro del mouse hello file **proprietà**e abilitare la crittografia in hello **avanzate** scheda Impostazioni. In alternativa, è possibile creare una soluzione personalizzata per crittografare parti selezionate di un file di configurazione tramite la configurazione protetta. Vedere l'argomento relativo alla [crittografia delle informazioni di configurazione usando la configurazione protetta](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Hello seguenti il file app. config contiene valori di connessione hello necessario. Hello valori hello <appSettings> elemento sono valori hello necessario ottenuti nel processo di installazione di account servizi multimediali hello.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve i valori di connessione della configurazione, è possibile utilizzare hello **ConfigurationManager** e quindi assegnare toofields valori hello nel codice:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

