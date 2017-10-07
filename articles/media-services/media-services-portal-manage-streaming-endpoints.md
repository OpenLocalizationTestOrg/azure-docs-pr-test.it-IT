---
title: gli endpoint con hello portale di Azure di streaming aaaManage | Documenti Microsoft
description: Questo argomento viene illustrato come endpoint di streaming toomanage con hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Gestire gli endpoint di streaming con hello portale di Azure

Questo argomento viene illustrato come toouse hello gli endpoint di streaming toomanage portale Azure. 

>[!NOTE]
>Verificare che hello tooreview [Panoramica](media-services-streaming-endpoints-overview.md) argomento. 

Per informazioni su come tooscale hello endpoint di streaming, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.

## <a name="start-managing-streaming-endpoints"></a>Iniziare a gestire gli endpoint di streaming 

Gestione endpoint di streaming per il tuo account, toostart hello seguente.

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** pannello seleziona **gli endpoint di Streaming**.
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.

## <a name="adddelete-a-streaming-endpoint"></a>Aggiungere o eliminare un endpoint di streaming

>[!NOTE]
>Impossibile eliminare l'endpoint di streaming predefinito di Hello.

tooadd/eliminazione tramite endpoint di streaming hello portale di Azure, hello seguenti:

1. tooadd un endpoint di streaming, fare clic su hello **+ Endpoint** nella parte superiore di hello della pagina hello. 

    Più endpoint di Streaming è necessario se si prevede di toohave CDN diversa o una rete CDN e l'accesso diretto.

2. Premere un endpoint di streaming, toodelete **eliminare** pulsante.      
3. Fare clic su hello **avviare** hello toostart pulsante endpoint di streaming.
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Configurazione di Endpoint di Streaming hello
Endpoint di streaming consente hello tooconfigure le proprietà seguenti:

* Controllo di accesso
* Controllo cache
* Criteri di accesso tra siti

Per informazioni dettagliate su queste proprietà, vedere [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

È possibile configurare l'endpoint di streaming eseguendo hello seguenti:

1. Selezionare hello desiderato tooconfigure endpoint di streaming.
2. Fare clic su **Impostazioni**.

Di seguito una breve descrizione dei campi hello.

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Criteri massima della cache: durata cache tooconfigure utilizzati per gli asset serviti tramite questo endpoint di streaming. Se è impostato alcun valore, viene usato predefinito di hello. i valori predefiniti di Hello possono anche essere definiti direttamente nell'archiviazione di Azure. Se la rete CDN Azure è abilitata per hello endpoint di streaming, non è necessario impostare tooless di valore dei criteri della cache hello di 600 secondi.  
2. Indirizzi IP consentiti: gli indirizzi IP toospecify che sia possibile usare tooconnect toohello pubblicati endpoint di streaming. Se nessun indirizzo IP specificato, qualsiasi indirizzo IP sarebbe in grado di tooconnect. È possibile specificare gli indirizzi IP come un singolo indirizzo IP (ad esempio "10.0.0.1"), un intervallo IP con un indirizzo IP e una subnet mask CIDR (ad esempio "10.0.0.1/22") o un intervallo IP con un indirizzo IP e una subnet mask decimale puntata (ad esempio "10.0.0.1(255.255.255.0)").
3. Configurazione per l'autenticazione dell'intestazione firma Akamai: utilizzato toospecify configurazione richiesta di autenticazione intestazione firma dai server Akamai. La scadenza è in formato UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Scalabilità dell'endpoint di streaming Premium

Per altre informazioni, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.

## <a id="enable_cdn"></a>Abilitare l'integrazione della rete CDN di Azure

Quando si crea un nuovo account, l'integrazione della rete CDN di Azure dell'endpoint di streaming predefinita viene abilitata per impostazione predefinita.

Se in seguito si abilita toodisable/hello CDN, l'endpoint di streaming deve essere in hello **arrestato** stato. Potrebbero richiedere alcune ore too2 per hello rete CDN di Azure integration tooget abilitata e per hello modifiche toobe active tra tutti hello POP della rete CDN. Tuttavia, è possibile avviare l'endpoint di streaming e flusso senza interruzioni da endpoint di streaming hello e una volta completato l'integrazione di hello, flusso hello verrà fornito da hello CDN. Durante il periodo di provisioning hello sarà l'endpoint di streaming in **avvio** e non è possibile osservare degredad prestazioni.

Integrazione della rete CDN è abilitata in tutte le aree Goverment Federal ed execpt di centri dati di Azure hello Cina.

Una volta attivato, hello **controllo di accesso**, **nome host personalizzato** e **autenticazione della firma Akamai** configurazione Ottiene disabilitata.
 
> [!IMPORTANT]
> L'integrazione di Servizi multimediali di Azure con la rete CDN di Azure è implementata nella **rete CDN di Azure da Verizon** per gli endpoint di streaming standard. Gli endpoint di streaming Premium possono essere configurati usando tutti **i provider e i livelli di prezzo della rete CDN di Azure**. Per ulteriori informazioni sulle funzionalità di rete CDN di Azure, vedere hello [Panoramica della rete CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Considerazioni aggiuntive

* Quando rete CDN è abilitata per un endpoint di streaming, i client non è possibile richiedere contenuto direttamente dall'origine di hello. Se è necessario hello possibilità tootest i contenuti con o senza rete CDN, è possibile creare un altro endpoint di streaming che non è abilitata CDN.
* I flusso rimane hostname endpoint hello uguale dopo l'abilitazione della rete CDN. Non è necessario toomake qualsiasi flusso di lavoro servizi di supporto tooyour di modifiche dopo aver abilitata la rete CDN. Ad esempio, se il nome host dell'endpoint di streaming è strasbourg.streaming.mediaservices.windows.net, dopo l'abilitazione della rete CDN, hello esatta stesso nome host viene utilizzato.
* Per i nuovi endpoint di streaming, è possibile abilitare CDN semplicemente creando un nuovo endpoint; per gli endpoint di streaming esistenti, è necessario endpoint hello di arresto toofirst e quindi abilitare o disabilitare hello CDN.
* L'endpoint di streaming standard può essere configurato solo tramite **il provider della rete CDN Standard di Verizon** nel portale di gestione di Azure. Tuttavia, è possibile abilitare altri provider della rete CDN di Azure usando le API REST.

## <a name="configure-cdn-profile"></a>Configurazione del profilo della rete CDN

È possibile configurare il profilo CDN hello selezionando hello **gestire CDN** pulsante dall'alto hello.

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

