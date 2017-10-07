---
title: notifiche del processo con .NET aaaUse Azure Webhook toomonitor servizi multimediali | Documenti Microsoft
description: Informazioni su come le notifiche del processo toouse Azure Webhook toomonitor servizi multimediali. Nell'esempio di codice Hello viene scritto in c# e utilizza hello Media Services SDK per .NET.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a61fe157-81b1-45c1-89f2-224b7ef55869
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/06/2017
ms.author: juliako
ms.openlocfilehash: b7df597da20e551cb2a02cd21c96c7bddf9e1a66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-webhooks-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="f33d0-104">Usare le notifiche di processo servizi multimediali di Azure Webhook toomonitor con .NET</span><span class="sxs-lookup"><span data-stu-id="f33d0-104">Use Azure WebHooks toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="f33d0-105">Quando si eseguono i processi, spesso richiedono un avanzamento del processo tootrack modo.</span><span class="sxs-lookup"><span data-stu-id="f33d0-105">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="f33d0-106">È possibile monitorare le notifiche dei processi di Servizi multimediali tramite webhook di Azure o [archiviazione code di Azure](media-services-dotnet-check-job-progress-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="f33d0-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="f33d0-107">Questo argomento viene illustrato come toowork con Webhook.</span><span class="sxs-lookup"><span data-stu-id="f33d0-107">This topic shows how toowork with Webhooks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f33d0-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f33d0-108">Prerequisites</span></span>

<span data-ttu-id="f33d0-109">di seguito Hello sono esercitazione hello toocomplete necessarie:</span><span class="sxs-lookup"><span data-stu-id="f33d0-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="f33d0-110">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="f33d0-110">An Azure account.</span></span> <span data-ttu-id="f33d0-111">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f33d0-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f33d0-112">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f33d0-112">A Media Services account.</span></span> <span data-ttu-id="f33d0-113">toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f33d0-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f33d0-114">Comprensione delle [come toouse Azure funzioni](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f33d0-114">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="f33d0-115">Rivedere anche [Associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="f33d0-115">Also, review [Azure functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md).</span></span>

<span data-ttu-id="f33d0-116">Questo argomento illustra come</span><span class="sxs-lookup"><span data-stu-id="f33d0-116">This topic shows how to</span></span>

*  <span data-ttu-id="f33d0-117">Definire una funzione di Azure che è toowebhooks toorespond personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f33d0-117">Define an Azure Function that is customized toorespond toowebhooks.</span></span> 
    
    <span data-ttu-id="f33d0-118">In questo caso, hello webhook viene attivata da servizi multimediali quando il processo di codifica viene modificato lo stato.</span><span class="sxs-lookup"><span data-stu-id="f33d0-118">In this case, hello webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="f33d0-119">funzione Hello è in attesa di hello webhook chiamata da notifiche di servizi multimediali e pubblica asset di output di hello una volta terminato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f33d0-119">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="f33d0-120">Prima di continuare, assicurarsi di comprendere come funzionano le [associazioni HTTP e webhook in Funzioni di Azure](../azure-functions/functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="f33d0-120">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="f33d0-121">Aggiungere un'attività di codifica tooyour webhook e specificare l'URL del webhook hello e una chiave privata che questo webhook risponde a.</span><span class="sxs-lookup"><span data-stu-id="f33d0-121">Add a webhook tooyour encoding task and specify hello webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="f33d0-122">Nell'esempio hello illustrato di seguito, il codice hello Crea attività di codifica hello è un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="f33d0-122">In hello example shown here, hello code that creates hello encoding task is a console app.</span></span>

## <a name="setting-up-webhook-notification-azure-functions"></a><span data-ttu-id="f33d0-123">Configurazione delle funzioni di Azure per la notifica di webhook</span><span class="sxs-lookup"><span data-stu-id="f33d0-123">Setting up "webhook notification" Azure functions</span></span>

<span data-ttu-id="f33d0-124">codice Hello in questa sezione viene illustrata un'implementazione di una funzione di Azure è un webhook.</span><span class="sxs-lookup"><span data-stu-id="f33d0-124">hello code in this section shows an implementation of an Azure function that is a webhook.</span></span> <span data-ttu-id="f33d0-125">In questo esempio, la funzione hello è in attesa di hello webhook chiamata da notifiche di servizi multimediali e pubblica asset di output di hello una volta terminato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f33d0-125">In this sample, hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span>

<span data-ttu-id="f33d0-126">Hello webhook prevede una firma di chiave (credenziali) toomatch hello uno è passato quando si configura l'endpoint di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f33d0-126">hello webhook expects a signing key (credential) toomatch hello one you pass when you configure hello notification endpoint.</span></span> <span data-ttu-id="f33d0-127">chiave di firma Hello è hello 64 byte con codificata Base64 valore tooprotect utilizzato e protetta il callback di Webhook da servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33d0-127">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="f33d0-128">Nel seguente codice di hello, hello **VerifyWebHookRequestSignature** metodo hello verifica nel messaggio di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="f33d0-128">In hello following code, hello **VerifyWebHookRequestSignature** method does hello verification on hello notification message.</span></span> <span data-ttu-id="f33d0-129">scopo di Hello di questa convalida è tooensure che hello messaggio è stato inviato da servizi multimediali di Azure e non è stato alterato.</span><span class="sxs-lookup"><span data-stu-id="f33d0-129">hello purpose of this validation is tooensure that hello message was sent by Azure Media Services and hasn’t been tampered with.</span></span> <span data-ttu-id="f33d0-130">firma Hello è facoltativo per le funzioni di Azure perché contiene hello **codice** valore come parametro di query sulla sicurezza TLS (Transport Layer).</span><span class="sxs-lookup"><span data-stu-id="f33d0-130">hello signature is optional for Azure functions as it has hello **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

<span data-ttu-id="f33d0-131">È possibile trovare la definizione di hello di varie funzioni di Media Services .NET Azure (incluso hello illustrato in questo argomento) [qui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="f33d0-131">You can find hello definition of various Media Services .NET Azure functions (including hello one shown in this topic) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

<span data-ttu-id="f33d0-132">Hello listato di codice seguente vengono illustrate hello definizioni di parametri di funzione di Azure e tre i file associati a hello Azure funzione: function.json, Project e run.csx.</span><span class="sxs-lookup"><span data-stu-id="f33d0-132">hello following code listing shows hello definitions of Azure function parameters and three files that are associated with hello Azure function: function.json, project.json, and run.csx.</span></span>

### <a name="application-settings"></a><span data-ttu-id="f33d0-133">Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f33d0-133">Application settings</span></span> 

<span data-ttu-id="f33d0-134">Hello nella tabella seguente vengono illustrati hello parametri usati da hello Azure funzione definita in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f33d0-134">hello following table shows hello parameters that are used by hello Azure function defined in this section.</span></span> 

|<span data-ttu-id="f33d0-135">Nome</span><span class="sxs-lookup"><span data-stu-id="f33d0-135">Name</span></span>|<span data-ttu-id="f33d0-136">Definizione</span><span class="sxs-lookup"><span data-stu-id="f33d0-136">Definition</span></span>|<span data-ttu-id="f33d0-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="f33d0-137">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="f33d0-138">AMSAccount</span><span class="sxs-lookup"><span data-stu-id="f33d0-138">AMSAccount</span></span>|<span data-ttu-id="f33d0-139">Nome dell'account AMS.</span><span class="sxs-lookup"><span data-stu-id="f33d0-139">Your AMS account name.</span></span> |<span data-ttu-id="f33d0-140">juliakomediaservices</span><span class="sxs-lookup"><span data-stu-id="f33d0-140">juliakomediaservices</span></span>|
|<span data-ttu-id="f33d0-141">AMSKey</span><span class="sxs-lookup"><span data-stu-id="f33d0-141">AMSKey</span></span> |<span data-ttu-id="f33d0-142">Chiave dell'account AMS.</span><span class="sxs-lookup"><span data-stu-id="f33d0-142">Your AMS account key.</span></span> | <span data-ttu-id="f33d0-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span><span class="sxs-lookup"><span data-stu-id="f33d0-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span></span>|
|<span data-ttu-id="f33d0-144">MediaServicesStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="f33d0-144">MediaServicesStorageAccountName</span></span> |<span data-ttu-id="f33d0-145">Nome dell'account di archiviazione hello associata con l'account di sistema AMS.</span><span class="sxs-lookup"><span data-stu-id="f33d0-145">A name of hello storage account that is associated with your AMS account.</span></span>| <span data-ttu-id="f33d0-146">storagepkeewmg5c3peq</span><span class="sxs-lookup"><span data-stu-id="f33d0-146">storagepkeewmg5c3peq</span></span>|
|<span data-ttu-id="f33d0-147">MediaServicesStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f33d0-147">MediaServicesStorageAccountKey</span></span> |<span data-ttu-id="f33d0-148">Chiave dell'account di archiviazione hello associata con l'account di sistema AMS.</span><span class="sxs-lookup"><span data-stu-id="f33d0-148">A key of hello storage account that is associated with your AMS account.</span></span>|
|<span data-ttu-id="f33d0-149">SigningKey</span><span class="sxs-lookup"><span data-stu-id="f33d0-149">SigningKey</span></span> |<span data-ttu-id="f33d0-150">Chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="f33d0-150">A signing key.</span></span>| <span data-ttu-id="f33d0-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="f33d0-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="f33d0-152">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="f33d0-152">WebHookEndpoint</span></span> | <span data-ttu-id="f33d0-153">Indirizzo di un endpoint di webhook.</span><span class="sxs-lookup"><span data-stu-id="f33d0-153">A webhook endpoint address.</span></span> | <span data-ttu-id="f33d0-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span><span class="sxs-lookup"><span data-stu-id="f33d0-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

### <a name="functionjson"></a><span data-ttu-id="f33d0-155">function.json</span><span class="sxs-lookup"><span data-stu-id="f33d0-155">function.json</span></span>

<span data-ttu-id="f33d0-156">file function.json Hello definisce l'associazione di funzione hello e altre impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f33d0-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="f33d0-157">Hello runtime utilizza questo toomonitor gli eventi di file toodetermine hello e come toopass e dati restituiti dalla funzionano esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f33d0-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> 

    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [
        "post",
        "get",
        "put",
        "update",
        "patch"
          ]
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
    
### <a name="projectjson"></a><span data-ttu-id="f33d0-158">project.json</span><span class="sxs-lookup"><span data-stu-id="f33d0-158">project.json</span></span>

<span data-ttu-id="f33d0-159">file Project JSON Hello contiene dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f33d0-159">hello project.json file contains dependencies.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="f33d0-160">run.csx</span><span class="sxs-lookup"><span data-stu-id="f33d0-160">run.csx</span></span>

<span data-ttu-id="f33d0-161">Hello codice c# seguente viene illustrata una definizione di una funzione di Azure è un webhook.</span><span class="sxs-lookup"><span data-stu-id="f33d0-161">hello following C# code shows a definition of an Azure function that is a webhook.</span></span> <span data-ttu-id="f33d0-162">funzione Hello è in attesa di hello webhook chiamata da notifiche di servizi multimediali e pubblica asset di output di hello una volta terminato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f33d0-162">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 


>[!NOTE]
><span data-ttu-id="f33d0-163">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f33d0-163">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f33d0-164">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="f33d0-164">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f33d0-165">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="f33d0-165">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    ///////////////////////////////////////////////////
    #r "Newtonsoft.Json"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using System.Globalization;
    using Newtonsoft.Json;
    using Microsoft.Azure;
    using System.Net;
    using System.Security.Cryptography;

    internal const string SignatureHeaderKey = "sha256";
    internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
    static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
    static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");
    static string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    static string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static CloudMediaContext _context = null;

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

        Task<byte[]> taskForRequestBody = req.Content.ReadAsByteArrayAsync();
        byte[] requestBody = await taskForRequestBody;

        string jsonContent = await req.Content.ReadAsStringAsync();
        log.Info($"Request Body = {jsonContent}");

        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-signature", out values))
        {
        byte[] signingKey = Convert.FromBase64String(_signingKey);
        string signatureFromHeader = values.FirstOrDefault();

        if (VerifyWebHookRequestSignature(requestBody, signatureFromHeader, signingKey))
        {
            string requestMessageContents = Encoding.UTF8.GetString(requestBody);

            NotificationMessage msg = JsonConvert.DeserializeObject<NotificationMessage>(requestMessageContents);

            if (VerifyHeaders(req, msg, log))
            { 
            string newJobStateStr = (string)msg.Properties.Where(j => j.Key == "NewState").FirstOrDefault().Value;
            if (newJobStateStr == "Finished")
            {
                _context = new CloudMediaContext(new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey));

                if(_context!=null)   
                {                        
                string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                log.Info($"URL toohello manifest for client streaming using HLS protocol: {urlForClientStreaming}");
                }
            }

            return req.CreateResponse(HttpStatusCode.OK, string.Empty);
            }
            else
            {
            log.Info($"VerifyHeaders failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyHeaders failed.");
            }
        }
        else
        {
            log.Info($"VerifyWebHookRequestSignature failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyWebHookRequestSignature failed.");
        }
        }

        return req.CreateResponse(HttpStatusCode.BadRequest, "Generic Error.");
    }

    private static string PublishAndBuildStreamingURLs(String jobID)
    {
        IJob job = _context.Jobs.Where(j => j.Id == jobID).FirstOrDefault();
        IAsset asset = job.OutputMediaAssets.FirstOrDefault();

        // Create a 30-day readonly access policy. 
        // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
        TimeSpan.FromDays(30),
        AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy,
        DateTime.UtcNow.AddMinutes(-5));


        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                    EndsWith(".ism")).
                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest" +  "(format=m3u8-aapl)";
        return urlForClientStreaming;

    }

    private static bool VerifyWebHookRequestSignature(byte[] data, string actualValue, byte[] verificationKey)
    {
        using (var hasher = new HMACSHA256(verificationKey))
        {
        byte[] sha256 = hasher.ComputeHash(data);
        string expectedValue = string.Format(CultureInfo.InvariantCulture, SignatureHeaderValueTemplate, ToHex(sha256));

        return (0 == String.Compare(actualValue, expectedValue, System.StringComparison.Ordinal));
        }
    }

    private static bool VerifyHeaders(HttpRequestMessage req, NotificationMessage msg, TraceWriter log)
    {
        bool headersVerified = false;

        try
        {
        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-mediaservices-accountid", out values))
        {
            string accountIdHeader = values.FirstOrDefault();
            string accountIdFromMessage = msg.Properties["AccountId"];

            if (0 == string.Compare(accountIdHeader, accountIdFromMessage, StringComparison.OrdinalIgnoreCase))
            {
            headersVerified = true;
            }
            else
            {
            log.Info($"accountIdHeader={accountIdHeader} does not match accountIdFromMessage={accountIdFromMessage}");
            }
        }
        else
        {
            log.Info($"Header ms-mediaservices-accountid not found.");
        }
        }
        catch (Exception e)
        {
        log.Info($"VerifyHeaders hit exception {e}");
        headersVerified = false;
        }

        return headersVerified;
    }

    private static readonly char[] HexLookup = new char[] { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };

    /// <summary>
    /// Converts a <see cref="T:byte[]"/> tooa hex-encoded string.
    /// </summary>
    private static string ToHex(byte[] data)
    {
        if (data == null)
        {
        return string.Empty;
        }

        char[] content = new char[data.Length * 2];
        int output = 0;
        byte d;
        for (int input = 0; input < data.Length; input++)
        {
        d = data[input];
        content[output++] = HexLookup[d / 0x10];
        content[output++] = HexLookup[d % 0x10];
        }
        return new string(content);
    }

    internal enum NotificationEventType
    {
        None = 0,
        JobStateChange = 1,
        NotificationEndPointRegistration = 2,
        NotificationEndPointUnregistration = 3,
        TaskStateChange = 4,
        TaskProgress = 5
    }
    
    internal sealed class NotificationMessage
    {
        public string MessageVersion { get; set; }
        public string ETag { get; set; }
        public NotificationEventType EventType { get; set; }
        public DateTime TimeStamp { get; set; }
        public IDictionary<string, string> Properties { get; set; }
    }

### <a name="function-output"></a><span data-ttu-id="f33d0-166">Output della funzione</span><span class="sxs-lookup"><span data-stu-id="f33d0-166">Function output</span></span>

<span data-ttu-id="f33d0-167">esempio Hello precedente generati dopo l'output di hello, variano i valori.</span><span class="sxs-lookup"><span data-stu-id="f33d0-167">hello example above produced hello following output, your values will vary.</span></span>

    C# HTTP trigger function processed a request. RequestUri=https://juliako001-functions.azurewebsites.net/api/Notification_Webhook_Function?code=9376d69kygoy49oft81nel8frty5cme8hb9xsjslxjhalwhfrqd79awz8ic4ieku74dvkdfgvi
    Request Body = {
      "MessageVersion": "1.1",
      "ETag": "b8977308f48858a8f224708bc963e1a09ff917ce730316b4e7ae9137f78f3b20",
      "EventType": 4,
      "TimeStamp": "2017-02-16T03:59:53.3041122Z",
      "Properties": {
        "JobId": "nb:jid:UUID:badd996c-8d7c-4ae0-9bc1-bd7f1902dbdd",
        "TaskId": "nb:tid:UUID:80e26fb9-ee04-4739-abd8-2555dc24639f",
        "NewState": "Finished",
        "OldState": "Processing",
        "AccountName": "mediapkeewmg5c3peq",
        "AccountId": "301912b0-659e-47e0-9bc4-6973f2be3424",
        "NotificationEndPointId": "nb:nepid:UUID:cb5d707b-4db8-45fe-a558-19f8d3306093"
      }
    }
    
    URL toohello manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="adding-webhook-tooyour-encoding-task"></a><span data-ttu-id="f33d0-168">Aggiunta di attività di codifica tooyour Webhook</span><span class="sxs-lookup"><span data-stu-id="f33d0-168">Adding Webhook tooyour encoding task</span></span>

<span data-ttu-id="f33d0-169">In questa sezione viene visualizzato il codice hello che aggiunge un tooa notifica webhook attività.</span><span class="sxs-lookup"><span data-stu-id="f33d0-169">In this section, hello code that adds a webhook notification tooa Task is shown.</span></span> <span data-ttu-id="f33d0-170">È inoltre possibile aggiungere una notifica di livello di processo, che dovrebbe essere più utile per un processo con attività concatenate.</span><span class="sxs-lookup"><span data-stu-id="f33d0-170">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="f33d0-171">Creare una nuova applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f33d0-171">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="f33d0-172">Immettere nome, percorso e soluzione nome hello e quindi fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="f33d0-172">Enter hello Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="f33d0-173">Utilizzare [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33d0-173">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure Media Services.</span></span>
3. <span data-ttu-id="f33d0-174">Aggiornare il file App.config con valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="f33d0-174">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="f33d0-175">Nome e chiave di Servizi multimediali di Azure che invieranno notifiche,</span><span class="sxs-lookup"><span data-stu-id="f33d0-175">Azure Media Services name and key that will be sending notifications,</span></span> 
    * <span data-ttu-id="f33d0-176">URL del webhook che prevede notifiche hello tooget,</span><span class="sxs-lookup"><span data-stu-id="f33d0-176">webhook URL that expects tooget hello notifications,</span></span> 
    * <span data-ttu-id="f33d0-177">Hello chiave corrispondente alla chiave hello che prevede il webhook per la firma.</span><span class="sxs-lookup"><span data-stu-id="f33d0-177">hello signing key that matches hello key that your webhook expects.</span></span> <span data-ttu-id="f33d0-178">chiave di firma Hello è hello 64 byte con codificata Base64 valore tooprotect utilizzato e protetta il callback di Webhook da servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33d0-178">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. <span data-ttu-id="f33d0-179">Aggiornare il file Program.cs hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f33d0-179">Update your Program.cs file with hello following code:</span></span>

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from hello App.config file.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];
            private static readonly string _webHookEndpoint =
                ConfigurationManager.AppSettings["WebhookURL"];
            private static readonly string _signingKey =
                 ConfigurationManager.AppSettings["WebhookSigningKey"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {

                // Used hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(new MediaServicesCredentials(
                        _mediaServicesAccountName,
                        _mediaServicesAccountKey));

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with hello name "FunctionWebHook"

                var existingEndpoint = _context.NotificationEndPoints.Where(e => e.Name == "FunctionWebHook").FirstOrDefault();
                INotificationEndPoint endpoint = null;

                if (existingEndpoint != null)
                {
                Console.WriteLine("webhook endpoint already exists");
                endpoint = (INotificationEndPoint)existingEndpoint;
                }
                else
                {
                endpoint = _context.NotificationEndPoints.Create("FunctionWebHook",
                    NotificationEndPointType.WebHook, _webHookEndpoint, keyBytes);
                Console.WriteLine("Notification Endpoint Created with Key : {0}", keyBytes.ToString());
                }

                // Declare a new encoding job with hello Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass tooit hello name of hello 
                // processor toouse for hello specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add hello WebHook notification toothis Task and request all notification state changes.
                // Note that you can also add a job level notification
                // which would be more useful for a job with chained tasks.  
                if (endpoint != null)
                {
                task.TaskNotificationSubscriptions.AddNew(NotificationJobState.All, endpoint, true);
                Console.WriteLine("Created Notification Subscription for endpoint: {0}", _webHookEndpoint);
                }
                else
                {
                Console.WriteLine("No Notification Endpoint is being used");
                }

                job.Submit();

                Console.WriteLine("Expect WebHook toobe triggered for hello Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook toobe triggered for hello Task ID: {0}", task.Id);

                Console.WriteLine("Job Submitted");

            }
            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                return processor;
            }

            }
        }

## <a name="next-step"></a><span data-ttu-id="f33d0-180">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f33d0-180">Next step</span></span>
<span data-ttu-id="f33d0-181">Analizzare i percorsi di apprendimento dei Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f33d0-181">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f33d0-182">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f33d0-182">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
