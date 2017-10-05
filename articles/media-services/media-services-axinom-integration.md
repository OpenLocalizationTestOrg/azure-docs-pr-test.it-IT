---
title: Uso di Axinom per distribuire licenze Widevine a Servizi multimediali di Azure | Microsoft Docs
description: Questo articolo illustra come usare Servizi multimediali di Azure per distribuire un flusso crittografato in modo dinamico da Servizi multimediali di Azure mediante DRM di PlayReady e Widevine. La licenza per PlayReady viene distribuita dal server licenze PlayReady di Servizi multimediali, mentre la licenza per Widevine viene distribuita dal server licenze Axinom.
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
ms.openlocfilehash: 64e8d4a88ea78e0de065e5a2c12dba4885e08bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-axinom-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="a0d02-104">Uso di Axinom per fornire licenze Widevine ai Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="a0d02-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0d02-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="a0d02-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="a0d02-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="a0d02-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a0d02-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a0d02-107">Overview</span></span>
<span data-ttu-id="a0d02-108">Servizi multimediali di Azure (AMS) ha aggiunto la protezione dinamica Google Widevine. Per altre informazioni, vedere il [blog di Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).</span><span class="sxs-lookup"><span data-stu-id="a0d02-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="a0d02-109">Azure Media Player (AMP) ha aggiunto anche il supporto per Widevine. Per informazioni dettagliate, vedere il [documento su AMP](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="a0d02-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="a0d02-110">Ciò offre molti vantaggi per lo streaming di contenuto DASH protetto da CENC con DRM multi-native (PlayReady e Widevine) in browser moderni dotati di MSE ed EME.</span><span class="sxs-lookup"><span data-stu-id="a0d02-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="a0d02-111">A partire da Servizi Multimediali .NET SDK versione 3.5.2, Servizi multimediali consente di configurare il modello di licenza Widevine e ottenere licenze Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="a0d02-112">È anche possibile usare i partner AMS seguenti per facilitare la distribuzione di licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) e [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="a0d02-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="a0d02-113">Questo articolo illustra come integrare e testare il server licenze Widevine gestito da Axinom.</span><span class="sxs-lookup"><span data-stu-id="a0d02-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="a0d02-114">In particolare, illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d02-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="a0d02-115">Configurazione della Common Encryption dinamica con DRM multiplo (PlayReady e Widevine) con URL di acquisizione licenze corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a0d02-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="a0d02-116">Generazione di un token JWT per soddisfare i requisiti del server licenze.</span><span class="sxs-lookup"><span data-stu-id="a0d02-116">Generating a JWT token in order to meet the license server requirements;</span></span>
* <span data-ttu-id="a0d02-117">Sviluppo di un'app Azure Media Player che gestisce l'acquisizione di licenze con l'autenticazione con token JWT.</span><span class="sxs-lookup"><span data-stu-id="a0d02-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="a0d02-118">Il sistema completo e il flusso di chiavi simmetriche, ID della chiave, semi chiave, token JTW e relative attestazioni può essere descritto in modo ottimale tramite il diagramma seguente.</span><span class="sxs-lookup"><span data-stu-id="a0d02-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span></span>

![DASH e CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="a0d02-120">Protezione del contenuto</span><span class="sxs-lookup"><span data-stu-id="a0d02-120">Content Protection</span></span>
<span data-ttu-id="a0d02-121">Per configurare la protezione dinamica e i criteri di distribuzione delle chiavi, vedere il blog di Mingfei relativo a [come configurare la creazione di pacchetti Widevine con Servizi multimediali di Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="a0d02-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="a0d02-122">È possibile configurare la protezione CENC dinamica con DRM multiplo per lo streaming DASH in modo che includa gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d02-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span></span>

1. <span data-ttu-id="a0d02-123">Protezione PlayReady per Microsoft Edge e IE11, che potrebbero presentare restrizioni relative all'autorizzazione con token.</span><span class="sxs-lookup"><span data-stu-id="a0d02-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="a0d02-124">I criteri con restrizione token devono essere associati a un token emesso da un servizio token di sicurezza, ad esempio Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0d02-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="a0d02-125">Protezione Widevine per Chrome. Può richiedere l'autenticazione con token tramite token emessi da un altro servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a0d02-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="a0d02-126">Per informazioni sui motivi per cui non è possibile usare Azure Active Directory come servizio token di sicurezza per il server licenze Widevine di Axinom, vedere [Generazione di token JWT](media-services-axinom-integration.md#jwt-token-generation) .</span><span class="sxs-lookup"><span data-stu-id="a0d02-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="a0d02-127">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a0d02-127">Considerations</span></span>
1. <span data-ttu-id="a0d02-128">È necessario usare il seme chiave specificato da Axinom (8888000000000000000000000000000000000000) e l'ID chiave generato o selezionato per generare la chiave simmetrica per la configurazione del servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="a0d02-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span></span> <span data-ttu-id="a0d02-129">Il server licenze Axinom emetterà tutte le licenze contenenti chiavi simmetriche basate sullo stesso seme chiave, valido per il test e la produzione.</span><span class="sxs-lookup"><span data-stu-id="a0d02-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="a0d02-130">URL di acquisizione di licenze Widevine per i test: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="a0d02-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="a0d02-131">Sono consentiti sia HTTP che HTTS.</span><span class="sxs-lookup"><span data-stu-id="a0d02-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="a0d02-132">Preparazione di Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="a0d02-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="a0d02-133">Azure Media Player v1.4.0 supporta la riproduzione di contenuto AMS incluso dinamicamente in pacchetti con PlayReady e Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="a0d02-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="a0d02-134">Se il server licenze Widevine non richiede l'autenticazione tramite token, non sono necessarie altre operazioni per testare un contenuto DASH protetto da Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span></span> <span data-ttu-id="a0d02-135">Per un esempio, il team AMP fornisce un semplice [esempio](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), dove è possibile vederlo funzionante nel bordo e in IE11 con PlayReady e Chrome con Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="a0d02-136">Il server licenze Widevine fornito da Axinom richiede l'autenticazione tramite token JWT.</span><span class="sxs-lookup"><span data-stu-id="a0d02-136">The Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="a0d02-137">Il token JWT deve essere inviato con la richiesta di licenza tramite un'intestazione HTTP "X-AxDRM-Message".</span><span class="sxs-lookup"><span data-stu-id="a0d02-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="a0d02-138">Per questo scopo è necessario aggiungere il codice javascript seguente nella pagina Web che ospita AMP prima di configurare l'origine:</span><span class="sxs-lookup"><span data-stu-id="a0d02-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="a0d02-139">Il resto del codice di Azure Media Player è un'API di Azure Media Player standard, come illustrato in [questo](http://amp.azure.net/libs/amp/latest/docs/)documento su Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="a0d02-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="a0d02-140">Si noti che il codice javascript precedente per la configurazione dell'intestazione di autorizzazione personalizzata costituisce ancora un approccio a breve termine, prima del rilascio dell'approccio ufficiale a lungo termine in Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="a0d02-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="a0d02-141">Generazione di token JWT</span><span class="sxs-lookup"><span data-stu-id="a0d02-141">JWT Token Generation</span></span>
<span data-ttu-id="a0d02-142">Il server licenze Axinom Widevine per il test richiede l'autenticazione tramite token JWT.</span><span class="sxs-lookup"><span data-stu-id="a0d02-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="a0d02-143">Una delle attestazioni nel token JWT, inoltre, è di tipo oggetto complesso, invece di tipo di dati primitivi.</span><span class="sxs-lookup"><span data-stu-id="a0d02-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="a0d02-144">Sfortunatamente, Azure AD può emettere solo token JWT con tipi primitivi.</span><span class="sxs-lookup"><span data-stu-id="a0d02-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="a0d02-145">Analogamente, l'API .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler e JwtPayload) consente solo di inserire tipi di oggetto complessi come attestazioni.</span><span class="sxs-lookup"><span data-stu-id="a0d02-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span></span> <span data-ttu-id="a0d02-146">Le attestazioni vengono tuttavia serializzate comunque come stringa.</span><span class="sxs-lookup"><span data-stu-id="a0d02-146">However, the claims are still serialized as string.</span></span> <span data-ttu-id="a0d02-147">Non è quindi possibile usarle per generare il token JWT per la richiesta di licenza Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span></span>

<span data-ttu-id="a0d02-148">Il [pacchetto NuGet JWT](https://www.nuget.org/packages/JWT) di John Sheehan soddisfa le esigenze specifiche, quindi verrà usato.</span><span class="sxs-lookup"><span data-stu-id="a0d02-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span></span>

<span data-ttu-id="a0d02-149">Il codice seguente consente di generare il token JWT con le attestazioni necessarie, in base a quanto richiesto dal server licenze Axinom Widevine per i test:</span><span class="sxs-lookup"><span data-stu-id="a0d02-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span></span>

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
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string to byte[] Note: Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string to byte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "The binary key cannot have an odd number of digits: {0}", hexString));
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

<span data-ttu-id="a0d02-150">Server licenze Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="a0d02-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="a0d02-151">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a0d02-151">Considerations</span></span>
1. <span data-ttu-id="a0d02-152">Anche se il servizio di distribuzione licenze PlayReady dei Servizi multimediali di Azure richiede il prefisso "Bearer=" per il token di autenticazione, il server licenze Axinom Widevine non lo usa.</span><span class="sxs-lookup"><span data-stu-id="a0d02-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="a0d02-153">La chiave di comunicazione Axinom viene usata come chiave di firma.</span><span class="sxs-lookup"><span data-stu-id="a0d02-153">The Axinom communication key is used as signing key.</span></span> <span data-ttu-id="a0d02-154">Si noti che la chiave è una stringa esadecimale, ma deve essere considerata come una serie di byte, non una stringa, durante la codifica.</span><span class="sxs-lookup"><span data-stu-id="a0d02-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="a0d02-155">Questo risultato viene ottenuto tramite il metodo ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="a0d02-155">This is achieved by the method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="a0d02-156">Recupero dell'ID chiave</span><span class="sxs-lookup"><span data-stu-id="a0d02-156">Retrieving Key ID</span></span>
<span data-ttu-id="a0d02-157">Come si può notare, l'ID chiave è necessario nel codice per la generazione di un token JWT.</span><span class="sxs-lookup"><span data-stu-id="a0d02-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="a0d02-158">Poiché il token JWT deve essere pronto prima di caricare il lettore di Azure Media Player, è necessario recuperare l'ID chiave per generare il token JWT.</span><span class="sxs-lookup"><span data-stu-id="a0d02-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span></span>

<span data-ttu-id="a0d02-159">È ovviamente possibile ottenere l'ID chiave in molti modi.</span><span class="sxs-lookup"><span data-stu-id="a0d02-159">Of course there are multiple ways to get hold of key ID.</span></span> <span data-ttu-id="a0d02-160">Ad esempio, è possibile archiviare l'ID chiave insieme ai metadati dei contenuti in un database.</span><span class="sxs-lookup"><span data-stu-id="a0d02-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="a0d02-161">In alternativa, è possibile recuperare l'ID chiave dal file DASH MPD (Media Presentation Description),</span><span class="sxs-lookup"><span data-stu-id="a0d02-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="a0d02-162">usando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="a0d02-162">The code below is for the latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="a0d02-163">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a0d02-163">Summary</span></span>
<span data-ttu-id="a0d02-164">La recente aggiunta del supporto per Widevine nella protezione del contenuto di Servizi multimediali di Azure e in Azure Media Player consente di implementare lo streaming di DASH + DRM multi-native (PlayReady + Widevine) con il server licenze PlayReady nei Servizi multimediali di Azure e un server licenze Widevine di Axinom per i browser moderni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d02-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span></span>

* <span data-ttu-id="a0d02-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="a0d02-165">Chrome</span></span>
* <span data-ttu-id="a0d02-166">Microsoft Edge in Windows 10</span><span class="sxs-lookup"><span data-stu-id="a0d02-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="a0d02-167">IE 11 in Windows 8.1 e Windows 10</span><span class="sxs-lookup"><span data-stu-id="a0d02-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="a0d02-168">Anche Firefox (Desktop) e Safari on Mac (non iOS) sono supportati tramite Silverlight e lo stesso URL con Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="a0d02-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span></span>

<span data-ttu-id="a0d02-169">I parametri seguenti sono necessari nella soluzione minima che sfrutta il server licenze Axinom Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="a0d02-170">Ad eccezione dell'ID chiave, il resto dei parametri viene fornito da Axinom in base alla configurazione del server Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="a0d02-171">Parametro</span><span class="sxs-lookup"><span data-stu-id="a0d02-171">Parameter</span></span> | <span data-ttu-id="a0d02-172">Modalità di utilizzo</span><span class="sxs-lookup"><span data-stu-id="a0d02-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="a0d02-173">ID chiave di comunicazione</span><span class="sxs-lookup"><span data-stu-id="a0d02-173">Communication key ID</span></span> |<span data-ttu-id="a0d02-174">Deve essere incluso come valore di attestazione "com_key_id" nel token JWT. Vedere [questa](media-services-axinom-integration.md#jwt-token-generation) sezione.</span><span class="sxs-lookup"><span data-stu-id="a0d02-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="a0d02-175">Chiave di comunicazione</span><span class="sxs-lookup"><span data-stu-id="a0d02-175">Communication key</span></span> |<span data-ttu-id="a0d02-176">Deve essere utilizzato come chiave di firma di token JWT (vedere [questa](media-services-axinom-integration.md#jwt-token-generation) sezione).</span><span class="sxs-lookup"><span data-stu-id="a0d02-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="a0d02-177">Seme chiave</span><span class="sxs-lookup"><span data-stu-id="a0d02-177">Key seed</span></span> |<span data-ttu-id="a0d02-178">Deve essere usato per generare la chiave simmetrica con qualsiasi ID della chiave simmetrica. Vedere [questa](media-services-axinom-integration.md#content-protection) sezione.</span><span class="sxs-lookup"><span data-stu-id="a0d02-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="a0d02-179">L'URL di acquisizione della licenza Widevine.</span><span class="sxs-lookup"><span data-stu-id="a0d02-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="a0d02-180">È necessario usare la configurazione dei criteri di recapito asset per il flusso DASH. Vedere [questa](media-services-axinom-integration.md#content-protection) sezione.</span><span class="sxs-lookup"><span data-stu-id="a0d02-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="a0d02-181">ID della chiave del contenuto</span><span class="sxs-lookup"><span data-stu-id="a0d02-181">Content Key ID</span></span> |<span data-ttu-id="a0d02-182">Deve essere incluso come parte del valore del reclamo del messaggio di attestazione del diritto di token JWT (vedere [questa](media-services-axinom-integration.md#jwt-token-generation) sezione).</span><span class="sxs-lookup"><span data-stu-id="a0d02-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="a0d02-183">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a0d02-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0d02-184">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a0d02-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="a0d02-185">Ringraziamenti</span><span class="sxs-lookup"><span data-stu-id="a0d02-185">Acknowledgments</span></span>
<span data-ttu-id="a0d02-186">Microsoft è lieta di conferire un riconoscimento alle persone seguenti che hanno contribuito alla realizzazione di questo documento: Kristjan Jõgi di Axinom, Mingfei Yan e Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="a0d02-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

