---
title: logica aaaRetry hello Media Services SDK per .NET | Documenti Microsoft
description: argomento Hello offre una panoramica della logica di riesecuzione in hello Media Services SDK per .NET.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Ripetere la logica nell'hello Media Services SDK per .NET
Quando si usano i servizi di Microsoft Azure, possono verificarsi errori temporanei. Se si verifica un errore temporaneo, nella maggior parte dei casi, dopo alcuni tentativi hello operazione ha esito positivo. Hello Media Services SDK per .NET implementa hello tentativi logica toohandle errori temporanei associati a eccezioni ed errori causati da richieste web, l'esecuzione di query, salvare le modifiche e operazioni di archiviazione.  Per impostazione predefinita, hello Media Services SDK per .NET esegue quattro tentativi prima di generare nuovamente un'applicazione hello eccezione tooyour. codice Hello nell'applicazione deve quindi gestire correttamente questa eccezione.  

 di seguito Hello è un'indicazione dei criteri di richiesta di servizio Web, archiviazione, Query e SaveChanges breve:  

* criteri di archiviazione Hello viene utilizzato per le operazioni di archiviazione blob (caricamento o download di file di asset).  
* Hello criterio di richiesta Web viene utilizzato per le richieste web generico (ad esempio, per ottenere token di autenticazione e la risoluzione utenti hello cluster endpoint).  
* Hello criteri di Query viene utilizzato per eseguire query sulle entità da altre (ad esempio, mediaContext.Assets.Where(...)).  
* Hello SaveChanges criteri viene utilizzata per eseguire qualsiasi operazione che modifica i dati all'interno del servizio di hello (ad esempio, la creazione di un'entità a un'entità, chiamare una funzione di servizio per un'operazione di aggiornamento).  
  
  Questo argomento vengono elencati i tipi di eccezione e la logica di riesecuzione dei codici di errore che vengono gestiti da hello Media Services SDK per .NET.  

## <a name="exception-types"></a>Tipi di eccezioni
Hello nella tabella seguente vengono descritte le eccezioni che hello Media Services SDK per .NET gestisce o non gestisce per alcune operazioni che possono causare errori temporanei.  

| Eccezione | Richiesta Web | Archiviazione | Query | Salvataggio di modifiche |
| --- | --- | --- | --- | --- |
| WebException<br/>Per ulteriori informazioni, vedere hello [codici di stato WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) sezione. |Sì |Sì |Sì |Sì |
| DataServiceClientException<br/> Per altre informazioni, vedere [Codici di stato dell'errore HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sì |Sì |Sì |
| DataServiceQueryException<br/> Per altre informazioni, vedere [Codici di stato dell'errore HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sì |Sì |Sì |
| DataServiceRequestException<br/> Per altre informazioni, vedere [Codici di stato dell'errore HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sì |Sì |Sì |
| DataServiceTransportException |No |No |Sì |Sì |
| TimeoutException |Sì |Sì |Sì |No |
| SocketException |Sì |Sì |Sì |Sì |
| StorageException |No |Sì |No |No |
| IOException |No |Sì |No |No |

### <a name="WebExceptionStatus"></a> Codici di stato di WebException
Hello nella tabella seguente mostra per errore WebException viene implementata la logica di ripetizione di codici hello. Hello [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) enumerazione definisce i codici di stato hello.  

| Stato | Richiesta Web | Archiviazione | Query | Salvataggio di modifiche |
| --- | --- | --- | --- | --- |
| ConnectFailure |Sì |Sì |Sì |Sì |
| NameResolutionFailure |Sì |Sì |Sì |Sì |
| ProxyNameResolutionFailure |Sì |Sì |Sì |Sì |
| SendFailure |Sì |Sì |Sì |Sì |
| PipelineFailure |Sì |Sì |Sì |No |
| ConnectionClosed |Sì |Sì |Sì |No |
| KeepAliveFailure |Sì |Sì |Sì |No |
| UnknownError |Sì |Sì |Sì |No |
| ReceiveFailure |Sì |Sì |Sì |No |
| RequestCanceled |Sì |Sì |Sì |No |
| Timeout |Sì |Sì |Sì |No |
| ProtocolError <br/>tentativo di Hello ProtocolError è controllata dalla gestione di codice di stato HTTP hello. Per altre informazioni, vedere [Codici di stato dell'errore HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Sì |Sì |Sì |Sì |

### <a name="HTTPStatusCode"></a> Codici di stato dell'errore HTTP
Quando le operazioni di Query e SaveChanges generano DataServiceClientException, DataServiceQueryException o DataServiceQueryException, hello codice di stato HTTP errore viene restituito nella proprietà StatusCode hello.  Hello nella tabella seguente mostra i cui codici di errore viene implementata la logica di ripetizione hello.  

| Stato | Richiesta Web | Archiviazione | Query | Salvataggio di modifiche |
| --- | --- | --- | --- | --- |
| 401 |No |Sì |No |No |
| 403 |No |Sì<br/>Gestione della ripetizione dei tentativi con attese più lunghe. |No |No |
| 408 |Sì |Sì |Sì |Sì |
| 429 |Sì |Sì |Sì |Sì |
| 500 |Sì |Sì |Sì |No |
| 502 |Sì |Sì |Sì |No |
| 503 |Sì |Sì |Sì |Sì |
| 504 |Sì |Sì |Sì |No |

Se si desidera tootake un'occhiata al momento dell'implementazione effettiva hello di hello Media Services SDK per la logica di riesecuzione .NET, vedere [-sdk-per-servizi multimediali di azure](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

