---
title: Panoramica del modello di licenza aaaWidevine | Documenti Microsoft
description: In questo argomento fornisce una panoramica di un modello di licenza Widevine utilizzati licenze Widevine tooconfigure.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Panoramica del modello di licenza Widevine
## <a name="overview"></a>Panoramica
Servizi multimediali di Azure consente ora licenze Widevine tooconfigure e richiesta. Quando si tenta di lettore dell'utente finale hello tooplay il contenuto protetto Widevine, una richiesta è inviato toohello licenza recapito servizio tooobtain una licenza. Se il servizio licenze hello Approva richiesta di hello, che possono essere emessi licenza hello client toohello inviato e può essere utilizzato toodecrypt e play hello contenuto specificato.

La richiesta per la licenza Widevine è formattata come messaggio JSON.  

>[!NOTE]
> È possibile scegliere toocreate un messaggio vuoto con nessun valori solo "{}" e verrà creato un modello di licenza con tutti i valori predefiniti. valore predefinito di Hello funziona per la maggior parte dei casi. Ad esempio, per scenari di distribuzione licenze basati su MS che devono essere sempre predefiniti. Se è necessario tooset hello "provider" e "content_id" valori, un provider deve corrispondere alle credenziali di Google Widevine.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Messaggio JSON
| Nome | Valore | Descrizione |
| --- | --- | --- |
| payload |Stringa con codifica Base64 |richiesta di licenza Hello inviato da un client. |
| content_id |Stringa con codifica Base64 |Identificatore utilizzato tooderive KeyId(s) e contenuto delle chiavi per ogni content_key_specs.track_type. |
| provider |string |Toolook utilizzati chiavi simmetriche e criteri. Se viene usata la distribuzione delle chiavi MS per la distribuzione di licenze Widevine, questo parametro viene ignorato. |
| policy_name |string |Nome di un criterio precedentemente registrato. Facoltativo |
| allowed_track_types |enum |SD_ONLY o SD_HD. Consente di specificare le chiavi simmetriche da includere in una licenza |
| content_key_specs |Matrice di strutture JSON. Vedere la sezione **Specifiche della chiave simmetrica** riportata di seguito |Un controllo con granularità maggiore sul contenuto delle chiavi tooreturn. Per informazioni, vedere la sezione Specifiche della chiave simmetrica riportata di seguito.  È possibile specificare solo uno dei valori allowed_track_types e content_key_specs. |
| use_policy_overrides_exclusively |boolean. true o false |Usare gli attributi di criteri specificati in policy_overrides e omettere tutti i criteri memorizzati in precedenza. |
| policy_overrides |Struttura JSON, vedere la sezione **Override dei criteri** riportata di seguito |Impostazioni di criteri per questa licenza.  Nell'evento hello questo asset è un criterio predefinito, verranno utilizzati questi valori specificati. |
| session_init |Struttura JSON, vedere la sezione **Inizializzazione della sessione** riportata di seguito |Dati facoltativi passati toolicense. |
| parse_only |boolean. true o false |richiesta di licenza Hello viene analizzato, ma nessuna licenza viene generata. Tuttavia, i valori maschera hello licenza richiesta vengono restituiti in risposta hello. |

## <a name="content-key-specs"></a>Specifiche della chiave simmetrica
Se esiste un criterio esistente, non è toospecify non è necessario uno qualsiasi dei hello valori hello contenuto chiave specifica.  criteri di Hello preesistente associato a questo contenuto sarà utilizzato toodetermine hello output protezione, ad esempio HDCP e CGMS.  Se un criterio esistente non è registrato con hello Server licenze Widevine, provider di contenuti hello può inserire i valori di hello nella richiesta di licenza hello.   

Ogni content_key_specs deve essere specificato per tutte le tracce, indipendentemente dal use_policy_overrides_exclusively opzione hello. 

| Nome | Valore | Description |
| --- | --- | --- |
| content_key_specs track_type |string |Nome di un tipo di traccia. Se content_key_specs è specificata nella richiesta di licenza hello, assicurarsi che toospecify che tenere traccia di tutti i tipi in modo esplicito. Errore toodo pertanto comporta tooplayback errore ultime 10 secondi. |
| content_key_specs  <br/> security_level |Valore UInt32 |Definisce i requisiti di affidabilità client per la riproduzione. <br/> 1 - È richiesta una soluzione di crittografia white box basata su software. <br/> 2 - È necessaria una soluzione di crittografia software e un decodificatore offuscato. <br/> 3 - operazioni di crittografia e materiale chiave hello devono essere eseguite all'interno di un ambiente di esecuzione trusted sottoposti a backup hardware. <br/> 4 - hello crittografia e la decodifica del contenuto deve essere eseguita in un ambiente di esecuzione trusted sottoposti a backup hardware.  <br/> 5 - hello crittografia, la decodifica e tutte le gestione del supporto di hello (compressi e) deve essere gestito in un ambiente di esecuzione trusted sottoposti a backup hardware. |
| content_key_specs <br/> required_output_protection.hdc |Stringa - uno di: HDCP_NONE, HDCP_V1, HDCP_V2 |Indica se è necessario il protocollo HDCP |
| content_key_specs <br/>key |Stringa con  <br/>codifica Base64 |Contenuto toouse chiave per la traccia. Se specificato, hello track_type o key_id è obbligatorio.  Questa opzione consente ai provider di contenuti hello chiave simmetrica di hello tooinject per la traccia anziché consentire a server licenze Widevine generare o cercare una chiave. |
| content_key_specs.key_id |Stringa binaria con codifica Base64, 16 byte |Identificatore univoco per la chiave di hello. |

## <a name="policy-overrides"></a>Override dei criteri
| Nome | Valore | Description |
| --- | --- | --- |
| policy_overrides can_play |boolean. true o false |Indica che la riproduzione di hello del contenuto è consentito. Il valore predefinito è false. |
| policy_overrides can_persist |boolean. true o false |Indica che la licenza hello può essere persistente archiviazione volatile toonon per l'utilizzo offline. Il valore predefinito è false. |
| policy_overrides can_renew |Booleano: true o false |Indica che è consentito il rinnovo della licenza. Se true, la durata di hello della licenza hello può essere estesa heartbeat. Il valore predefinito è false. |
| policy_overrides license_duration_seconds |int64 |Indica l'intervallo di tempo hello per questa licenza specifica. Il valore 0 indica che non vi sia alcuna durata toohello limite. Il valore predefinito è 0. |
| policy_overrides rental_duration_seconds |int64 |Indica l'intervallo di tempo hello durante la riproduzione è consentita. Il valore 0 indica che non vi sia alcuna durata toohello limite. Il valore predefinito è 0. |
| policy_overrides playback_duration_seconds |int64 |Hello visualizzazione intervallo di tempo una volta avviata la riproduzione entro il periodo di licenza hello. Il valore 0 indica che non vi sia alcuna durata toohello limite. Il valore predefinito è 0. |
| policy_overrides renewal_server_url |string |Tutte le richieste di heartbeat (rinnovo) per la licenza devono essere diretto toohello URL specificato. Questo campo viene usato solo se can_renew è true. |
| policy_overrides renewal_delay_seconds |int64 |Numero di secondi prima che venga eseguito il primo tentativo di rinnovo, a partire dal valore license_start_time. Questo campo viene usato solo se can_renew è true. Il valore predefinito è 0 |
| policy_overrides renewal_retry_interval_seconds |int64 |Specifica il ritardo di hello in secondi tra le richieste di rinnovo delle licenze successive, in caso di errore. Questo campo viene usato solo se can_renew è true. |
| policy_overrides renewal_recovery_duration_seconds |int64 |finestra Hello di tempo, in cui la riproduzione è consentita toocontinue durante il rinnovo è ancora esito negativo a causa di problemi toobackend hello licenze server, il tentativo. Il valore 0 indica che non vi sia alcuna durata toohello limite. Questo campo viene usato solo se can_renew è true. |
| policy_overrides renew_with_usage |Booleano: true o false |Indica che la licenza hello dovrà essere inviata per il rinnovo quando viene avviato l'utilizzo. Questo campo viene usato solo se can_renew è true. |

## <a name="session-initialization"></a>Inizializzazione della sessione
| Nome | Valore | Descrizione |
| --- | --- | --- |
| provider_session_token |Stringa con codifica Base64 |Questo token di sessione viene passato in licenza hello e sarà presenti in rinnovi successivi.  token di sessione Hello non verrà mantenuto oltre le sessioni. |
| provider_client_token |Stringa con codifica Base64 |Client toosend token restituite nella risposta licenza hello.  Se la richiesta di licenza hello contiene un token di client, questo valore viene ignorato. token di Hello del client verrà mantenuto oltre le sessioni di licenza. |
| override_provider_client_token |boolean. true o false |Se false e hello richiesta licenza contiene un token di client, utilizzare il token di hello dalla richiesta hello anche se è stato specificato un token di client in questa struttura.  Se true, utilizzare sempre il token di hello specificato in questa struttura. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Configurare licenze Widevine usando tipi .NET
Servizi multimediali fornisce API .NET che consentono di configurare licenze Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Classi definite in hello Media Services .NET SDK
di seguito Hello sono definizioni di hello di questi tipi.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Esempio
Hello seguente esempio viene illustrato come le API .NET di toouse tooconfigure una licenza Widevine semplice.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Uso della crittografia comune dinamica PlayReady e/o Widevine](media-services-protect-with-drm.md)

