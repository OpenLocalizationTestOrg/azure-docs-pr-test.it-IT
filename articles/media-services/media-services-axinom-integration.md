---
title: le licenze di servizi multimediali tooAzure aaaUsing Axinom toodeliver Widevine | Documenti Microsoft
description: In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs. la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e viene recapitata licenze Widevine dal server licenze Axinom.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="c2680-104">Utilizzando Axinom toodeliver Widevine licenze tooAzure servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="c2680-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2680-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="c2680-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="c2680-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="c2680-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c2680-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2680-107">Overview</span></span>
<span data-ttu-id="c2680-108">Servizi multimediali di Azure (AMS) ha aggiunto la protezione dinamica Google Widevine. Per altre informazioni, vedere il [blog di Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).</span><span class="sxs-lookup"><span data-stu-id="c2680-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="c2680-109">Azure Media Player (AMP) ha aggiunto anche il supporto per Widevine. Per informazioni dettagliate, vedere il [documento su AMP](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="c2680-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="c2680-110">Ciò offre molti vantaggi per lo streaming di contenuto DASH protetto da CENC con DRM multi-native (PlayReady e Widevine) in browser moderni dotati di MSE ed EME.</span><span class="sxs-lookup"><span data-stu-id="c2680-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="c2680-111">A partire da Media Services .NET SDK versione 3.5.2 hello, servizi multimediali consente di tooconfigure Widevine modello di licenza e ottenere licenze Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="c2680-112">È inoltre possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="c2680-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="c2680-113">In questo articolo viene descritto come toointegrate e test Widevine licenza server gestito da Axinom.</span><span class="sxs-lookup"><span data-stu-id="c2680-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="c2680-114">In particolare, illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2680-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="c2680-115">Configurazione della Common Encryption dinamica con DRM multiplo (PlayReady e Widevine) con URL di acquisizione licenze corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="c2680-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="c2680-116">Generazione di un token JWT in requisiti del server licenze hello toomeet ordine;</span><span class="sxs-lookup"><span data-stu-id="c2680-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="c2680-117">Sviluppo di un'app Azure Media Player che gestisce l'acquisizione di licenze con l'autenticazione con token JWT.</span><span class="sxs-lookup"><span data-stu-id="c2680-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="c2680-118">Hello completa del sistema e il flusso di contenuto che Key, chiave ID seme chiave, il token JTW e relative attestazioni possono essere descritti meglio dalla seguente diagramma hello hello.</span><span class="sxs-lookup"><span data-stu-id="c2680-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH e CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="c2680-120">Protezione del contenuto</span><span class="sxs-lookup"><span data-stu-id="c2680-120">Content Protection</span></span>
<span data-ttu-id="c2680-121">Per la configurazione dinamica protezione e criteri di distribuzione delle chiavi, vedere il blog del Mingfei: [come tooconfigure Widevine pacchetti con servizi multimediali di Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="c2680-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="c2680-122">È possibile configurare protezione CENC dinamica con multi-DRM per DASH streaming con entrambi i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="c2680-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="c2680-123">Protezione PlayReady per Microsoft Edge e IE11, che potrebbero presentare restrizioni relative all'autorizzazione con token.</span><span class="sxs-lookup"><span data-stu-id="c2680-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="c2680-124">criteri con restrizione token Hello devono essere accompagnato da un token emesso da un servizio (token di sicurezza), ad esempio Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2680-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="c2680-125">Protezione Widevine per Chrome. Può richiedere l'autenticazione con token tramite token emessi da un altro servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c2680-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="c2680-126">Per informazioni sui motivi per cui non è possibile usare Azure Active Directory come servizio token di sicurezza per il server licenze Widevine di Axinom, vedere [Generazione di token JWT](media-services-axinom-integration.md#jwt-token-generation) .</span><span class="sxs-lookup"><span data-stu-id="c2680-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="c2680-127">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="c2680-127">Considerations</span></span>
1. <span data-ttu-id="c2680-128">È necessario utilizzare hello che axinom specificato seme chiave (8888000000000000000000000000000000000000) e selezionato o generato chiave ID toogenerate hello contenuti chiave per la configurazione del servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="c2680-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="c2680-129">Server licenze Axinom rilascerà tutte le licenze che contiene contenute chiavi basate su hello stessa chiave di valore di inizializzazione, che è valida per il test e produzione.</span><span class="sxs-lookup"><span data-stu-id="c2680-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="c2680-130">URL di acquisizione della licenza Hello Widevine per il test: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="c2680-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="c2680-131">Sono consentiti sia HTTP che HTTS.</span><span class="sxs-lookup"><span data-stu-id="c2680-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="c2680-132">Preparazione di Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="c2680-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="c2680-133">Azure Media Player v1.4.0 supporta la riproduzione di contenuto AMS incluso dinamicamente in pacchetti con PlayReady e Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="c2680-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="c2680-134">Se il server licenze Widevine non richiede l'autenticazione del token, non è necessario eseguire ulteriori che occorre tootest toodo un trattino di contenuto protetto da Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="c2680-135">Per un esempio, il team di hello AMP fornisce una semplice [esempio](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), in cui è possibile visualizzare lo stesso risultato in bordo e IE11 con PlayReady e Chrome con Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="c2680-136">server di licenze Widevine Hello fornito da Axinom richiede l'autenticazione con token JWT.</span><span class="sxs-lookup"><span data-stu-id="c2680-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="c2680-137">token JWT Hello deve toobe inviata con la richiesta di licenza tramite un'intestazione HTTP "X-AxDRM-messaggio".</span><span class="sxs-lookup"><span data-stu-id="c2680-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="c2680-138">A tale scopo, è necessario hello tooadd javascript nella pagina web hello hosting AMP prima origine hello impostazione seguente:</span><span class="sxs-lookup"><span data-stu-id="c2680-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="c2680-139">il resto di Hello del codice AMP è standard AMP API, come nel documento AMP [qui](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="c2680-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="c2680-140">Si noti che hello sopra javascript per l'impostazione dell'intestazione di autorizzazione personalizzato è ancora un approccio a breve termine prima ufficiale hello approccio a lungo termine amp viene rilasciato.</span><span class="sxs-lookup"><span data-stu-id="c2680-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="c2680-141">Generazione di token JWT</span><span class="sxs-lookup"><span data-stu-id="c2680-141">JWT Token Generation</span></span>
<span data-ttu-id="c2680-142">Il server licenze Axinom Widevine per il test richiede l'autenticazione tramite token JWT.</span><span class="sxs-lookup"><span data-stu-id="c2680-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="c2680-143">Inoltre, uno di hello attestazioni in token JWT hello è di un tipo di oggetto complesso anziché il tipo di dati primitivi.</span><span class="sxs-lookup"><span data-stu-id="c2680-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="c2680-144">Sfortunatamente, Azure AD può emettere solo token JWT con tipi primitivi.</span><span class="sxs-lookup"><span data-stu-id="c2680-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="c2680-145">Analogamente, API di .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler e JwtPayload) consente solo il tipo di oggetto complesso tooinput come attestazioni.</span><span class="sxs-lookup"><span data-stu-id="c2680-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="c2680-146">Tuttavia, le attestazioni di hello ancora vengono serializzate come stringa.</span><span class="sxs-lookup"><span data-stu-id="c2680-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="c2680-147">Pertanto non è possibile usare uno qualsiasi dei hello due per generare i token JWT hello per richiesta licenze Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="c2680-148">Di John Sheehan [pacchetto Nuget di JWT](https://www.nuget.org/packages/JWT) soddisfa hello esigenze in modo verrà toouse questo pacchetto Nuget.</span><span class="sxs-lookup"><span data-stu-id="c2680-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="c2680-149">Di seguito è codice hello per generare i token JWT con hello necessari attestazioni come richiesto dal server licenze Axinom Widevine per il test:</span><span class="sxs-lookup"><span data-stu-id="c2680-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="c2680-150">Server licenze Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="c2680-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="c2680-151">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="c2680-151">Considerations</span></span>
1. <span data-ttu-id="c2680-152">Anche se il servizio di distribuzione licenze PlayReady dei Servizi multimediali di Azure richiede il prefisso "Bearer=" per il token di autenticazione, il server licenze Axinom Widevine non lo usa.</span><span class="sxs-lookup"><span data-stu-id="c2680-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="c2680-153">chiave di comunicazione Axinom Hello viene utilizzata come chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="c2680-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="c2680-154">Si noti che la chiave di hello è una stringa esadecimale, tuttavia devono essere considerata come una serie di byte non è una stringa per la codifica.</span><span class="sxs-lookup"><span data-stu-id="c2680-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="c2680-155">Questo risultato viene ottenuto dal metodo hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="c2680-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="c2680-156">Recupero dell'ID chiave</span><span class="sxs-lookup"><span data-stu-id="c2680-156">Retrieving Key ID</span></span>
<span data-ttu-id="c2680-157">Si può notare che nel codice hello per la generazione di un JWT token ID chiave è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="c2680-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="c2680-158">Poiché i token JWT hello deve toobe pronto prima del caricamento player AMP, esigenze di ID chiave toobe recuperato nell'ordine token JWT toogenerate.</span><span class="sxs-lookup"><span data-stu-id="c2680-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="c2680-159">Naturalmente, esistono diversi modi tooget tenere della chiave ID.</span><span class="sxs-lookup"><span data-stu-id="c2680-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="c2680-160">Ad esempio, è possibile archiviare l'ID chiave insieme ai metadati dei contenuti in un database.</span><span class="sxs-lookup"><span data-stu-id="c2680-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="c2680-161">In alternativa, è possibile recuperare l'ID chiave dal file DASH MPD (Media Presentation Description),</span><span class="sxs-lookup"><span data-stu-id="c2680-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="c2680-162">codice Hello riportato di seguito è per hello quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="c2680-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="c2680-163">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c2680-163">Summary</span></span>
<span data-ttu-id="c2680-164">Con l'ultima aggiunta del supporto Widevine sia la protezione dei contenuti di servizi multimediali Azure e Azure Media Player, siamo in grado di tooimplement streaming di trattino + native Multi-DRM (PlayReady + Widevine) con sia servizio di licenza PlayReady in licenza AMS e Widevine server da Axinom hello seguendo i browser moderni:</span><span class="sxs-lookup"><span data-stu-id="c2680-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="c2680-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="c2680-165">Chrome</span></span>
* <span data-ttu-id="c2680-166">Microsoft Edge in Windows 10</span><span class="sxs-lookup"><span data-stu-id="c2680-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="c2680-167">IE 11 in Windows 8.1 e Windows 10</span><span class="sxs-lookup"><span data-stu-id="c2680-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="c2680-168">(Desktop) Firefox e Safari su Mac (non iOS) sono anche supportate tramite Silverlight e hello stesso URL con Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="c2680-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="c2680-169">Hello i parametri seguenti sono necessari nel server di licenze di hello soluzione minima sfruttando Axinom Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="c2680-170">Ad eccezione di chiave ID, rest hello dei parametri forniti da Axinom in base all'impostazione delle server Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="c2680-171">.</span><span class="sxs-lookup"><span data-stu-id="c2680-171">Parameter</span></span> | <span data-ttu-id="c2680-172">Modalità di utilizzo</span><span class="sxs-lookup"><span data-stu-id="c2680-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="c2680-173">ID chiave di comunicazione</span><span class="sxs-lookup"><span data-stu-id="c2680-173">Communication key ID</span></span> |<span data-ttu-id="c2680-174">Deve essere incluso come valore di attestazione hello "com_key_id" in token JWT (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione).</span><span class="sxs-lookup"><span data-stu-id="c2680-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c2680-175">Chiave di comunicazione</span><span class="sxs-lookup"><span data-stu-id="c2680-175">Communication key</span></span> |<span data-ttu-id="c2680-176">Deve essere utilizzata come chiave di firma di token JWT hello (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione).</span><span class="sxs-lookup"><span data-stu-id="c2680-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c2680-177">Seme chiave</span><span class="sxs-lookup"><span data-stu-id="c2680-177">Key seed</span></span> |<span data-ttu-id="c2680-178">Deve essere utilizzato toogenerate chiave simmetrica con qualsiasi fornito il contenuto di ID chiave (vedere [questo](media-services-axinom-integration.md#content-protection) sezione).</span><span class="sxs-lookup"><span data-stu-id="c2680-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="c2680-179">L'URL di acquisizione della licenza Widevine.</span><span class="sxs-lookup"><span data-stu-id="c2680-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="c2680-180">È necessario usare la configurazione dei criteri di recapito asset per il flusso DASH. Vedere [questa](media-services-axinom-integration.md#content-protection) sezione.</span><span class="sxs-lookup"><span data-stu-id="c2680-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="c2680-181">ID della chiave del contenuto</span><span class="sxs-lookup"><span data-stu-id="c2680-181">Content Key ID</span></span> |<span data-ttu-id="c2680-182">Deve essere incluso come parte del valore di hello dell'attestazione messaggio il diritto di token JWT (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione).</span><span class="sxs-lookup"><span data-stu-id="c2680-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="c2680-183">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="c2680-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c2680-184">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c2680-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="c2680-185">Ringraziamenti</span><span class="sxs-lookup"><span data-stu-id="c2680-185">Acknowledgments</span></span>
<span data-ttu-id="c2680-186">Desideriamo hello tooacknowledge seguente persone che hanno contribuito per la creazione di questo documento: Kristjan Jõgi di Axinom Mingfei Yan e Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="c2680-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

