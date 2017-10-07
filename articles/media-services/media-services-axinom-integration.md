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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Utilizzando Axinom toodeliver Widevine licenze tooAzure servizi multimediali
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Panoramica
Servizi multimediali di Azure (AMS) ha aggiunto la protezione dinamica Google Widevine. Per altre informazioni, vedere il [blog di Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/). Azure Media Player (AMP) ha aggiunto anche il supporto per Widevine. Per informazioni dettagliate, vedere il [documento su AMP](http://amp.azure.net/libs/amp/latest/docs/). Ciò offre molti vantaggi per lo streaming di contenuto DASH protetto da CENC con DRM multi-native (PlayReady e Widevine) in browser moderni dotati di MSE ed EME.

A partire da Media Services .NET SDK versione 3.5.2 hello, servizi multimediali consente di tooconfigure Widevine modello di licenza e ottenere licenze Widevine. È inoltre possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

In questo articolo viene descritto come toointegrate e test Widevine licenza server gestito da Axinom. In particolare, illustra le operazioni seguenti:  

* Configurazione della Common Encryption dinamica con DRM multiplo (PlayReady e Widevine) con URL di acquisizione licenze corrispondenti.
* Generazione di un token JWT in requisiti del server licenze hello toomeet ordine;
* Sviluppo di un'app Azure Media Player che gestisce l'acquisizione di licenze con l'autenticazione con token JWT.

Hello completa del sistema e il flusso di contenuto che Key, chiave ID seme chiave, il token JTW e relative attestazioni possono essere descritti meglio dalla seguente diagramma hello hello.

![DASH e CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Protezione del contenuto
Per la configurazione dinamica protezione e criteri di distribuzione delle chiavi, vedere il blog del Mingfei: [come tooconfigure Widevine pacchetti con servizi multimediali di Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

È possibile configurare protezione CENC dinamica con multi-DRM per DASH streaming con entrambi i seguenti hello:

1. Protezione PlayReady per Microsoft Edge e IE11, che potrebbero presentare restrizioni relative all'autorizzazione con token. criteri con restrizione token Hello devono essere accompagnato da un token emesso da un servizio (token di sicurezza), ad esempio Azure Active Directory.
2. Protezione Widevine per Chrome. Può richiedere l'autenticazione con token tramite token emessi da un altro servizio token di sicurezza. 

Per informazioni sui motivi per cui non è possibile usare Azure Active Directory come servizio token di sicurezza per il server licenze Widevine di Axinom, vedere [Generazione di token JWT](media-services-axinom-integration.md#jwt-token-generation) .

### <a name="considerations"></a>Considerazioni
1. È necessario utilizzare hello che axinom specificato seme chiave (8888000000000000000000000000000000000000) e selezionato o generato chiave ID toogenerate hello contenuti chiave per la configurazione del servizio di distribuzione delle chiavi. Server licenze Axinom rilascerà tutte le licenze che contiene contenute chiavi basate su hello stessa chiave di valore di inizializzazione, che è valida per il test e produzione.
2. URL di acquisizione della licenza Hello Widevine per il test: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). Sono consentiti sia HTTP che HTTS.

## <a name="azure-media-player-preparation"></a>Preparazione di Azure Media Player
Azure Media Player v1.4.0 supporta la riproduzione di contenuto AMS incluso dinamicamente in pacchetti con PlayReady e Widevine DRM.
Se il server licenze Widevine non richiede l'autenticazione del token, non è necessario eseguire ulteriori che occorre tootest toodo un trattino di contenuto protetto da Widevine. Per un esempio, il team di hello AMP fornisce una semplice [esempio](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), in cui è possibile visualizzare lo stesso risultato in bordo e IE11 con PlayReady e Chrome con Widevine.
server di licenze Widevine Hello fornito da Axinom richiede l'autenticazione con token JWT. token JWT Hello deve toobe inviata con la richiesta di licenza tramite un'intestazione HTTP "X-AxDRM-messaggio". A tale scopo, è necessario hello tooadd javascript nella pagina web hello hosting AMP prima origine hello impostazione seguente:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

il resto di Hello del codice AMP è standard AMP API, come nel documento AMP [qui](http://amp.azure.net/libs/amp/latest/docs/).

Si noti che hello sopra javascript per l'impostazione dell'intestazione di autorizzazione personalizzato è ancora un approccio a breve termine prima ufficiale hello approccio a lungo termine amp viene rilasciato.

## <a name="jwt-token-generation"></a>Generazione di token JWT
Il server licenze Axinom Widevine per il test richiede l'autenticazione tramite token JWT. Inoltre, uno di hello attestazioni in token JWT hello è di un tipo di oggetto complesso anziché il tipo di dati primitivi.

Sfortunatamente, Azure AD può emettere solo token JWT con tipi primitivi. Analogamente, API di .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler e JwtPayload) consente solo il tipo di oggetto complesso tooinput come attestazioni. Tuttavia, le attestazioni di hello ancora vengono serializzate come stringa. Pertanto non è possibile usare uno qualsiasi dei hello due per generare i token JWT hello per richiesta licenze Widevine.

Di John Sheehan [pacchetto Nuget di JWT](https://www.nuget.org/packages/JWT) soddisfa hello esigenze in modo verrà toouse questo pacchetto Nuget.

Di seguito è codice hello per generare i token JWT con hello necessari attestazioni come richiesto dal server licenze Axinom Widevine per il test:

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

Server licenze Axinom Widevine

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Considerazioni
1. Anche se il servizio di distribuzione licenze PlayReady dei Servizi multimediali di Azure richiede il prefisso "Bearer=" per il token di autenticazione, il server licenze Axinom Widevine non lo usa.
2. chiave di comunicazione Axinom Hello viene utilizzata come chiave di firma. Si noti che la chiave di hello è una stringa esadecimale, tuttavia devono essere considerata come una serie di byte non è una stringa per la codifica. Questo risultato viene ottenuto dal metodo hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Recupero dell'ID chiave
Si può notare che nel codice hello per la generazione di un JWT token ID chiave è obbligatorio. Poiché i token JWT hello deve toobe pronto prima del caricamento player AMP, esigenze di ID chiave toobe recuperato nell'ordine token JWT toogenerate.

Naturalmente, esistono diversi modi tooget tenere della chiave ID. Ad esempio, è possibile archiviare l'ID chiave insieme ai metadati dei contenuti in un database. In alternativa, è possibile recuperare l'ID chiave dal file DASH MPD (Media Presentation Description), codice Hello riportato di seguito è per hello quest'ultimo.

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

## <a name="summary"></a>Riepilogo
Con l'ultima aggiunta del supporto Widevine sia la protezione dei contenuti di servizi multimediali Azure e Azure Media Player, siamo in grado di tooimplement streaming di trattino + native Multi-DRM (PlayReady + Widevine) con sia servizio di licenza PlayReady in licenza AMS e Widevine server da Axinom hello seguendo i browser moderni:

* Chrome
* Microsoft Edge in Windows 10
* IE 11 in Windows 8.1 e Windows 10
* (Desktop) Firefox e Safari su Mac (non iOS) sono anche supportate tramite Silverlight e hello stesso URL con Azure Media Player

Hello i parametri seguenti sono necessari nel server di licenze di hello soluzione minima sfruttando Axinom Widevine. Ad eccezione di chiave ID, rest hello dei parametri forniti da Axinom in base all'impostazione delle server Widevine.

| . | Modalità di utilizzo |
| --- | --- |
| ID chiave di comunicazione |Deve essere incluso come valore di attestazione hello "com_key_id" in token JWT (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione). |
| Chiave di comunicazione |Deve essere utilizzata come chiave di firma di token JWT hello (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione). |
| Seme chiave |Deve essere utilizzato toogenerate chiave simmetrica con qualsiasi fornito il contenuto di ID chiave (vedere [questo](media-services-axinom-integration.md#content-protection) sezione). |
| L'URL di acquisizione della licenza Widevine. |È necessario usare la configurazione dei criteri di recapito asset per il flusso DASH. Vedere [questa](media-services-axinom-integration.md#content-protection) sezione. |
| ID della chiave del contenuto |Deve essere incluso come parte del valore di hello dell'attestazione messaggio il diritto di token JWT (vedere [questo](media-services-axinom-integration.md#jwt-token-generation) sezione). |

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Ringraziamenti
Desideriamo hello tooacknowledge seguente persone che hanno contribuito per la creazione di questo documento: Kristjan Jõgi di Axinom Mingfei Yan e Amit Rajput.

