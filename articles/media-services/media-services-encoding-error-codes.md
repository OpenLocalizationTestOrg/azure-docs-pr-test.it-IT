---
title: Servizi multimediali aaaAzure codici di errore di codifica | Documenti Microsoft
description: "In questo argomento elenca i codici di errore che possono essere restituiti nel caso in cui si è verificato un errore durante l'esecuzione dell'attività di codifica hello..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>Codici di errore di codifica

Hello nella tabella seguente sono elencati i codici di errore che possono essere restituiti nel caso in cui si è verificato un errore durante l'esecuzione dell'attività di codifica hello.  i dettagli dell'errore tooget nel codice .NET, usare hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe. i dettagli dell'errore tooget nel codice REST, usare hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API REST.

| ErrorDetail.Code | Le possibili cause dell'errore |
| --- | --- |
| Sconosciuto |Errore sconosciuto durante l'esecuzione di attività hello |
| ErrorDownloadingInputAssetMalformedContent |Categoria di errori relativa agli errori durante il download di asset di input, ad esempio nomi di file non validi, file di lunghezza zero, formati errati e così via. |
| ErrorDownloadingInputAssetServiceFailure |Categoria di errori che verranno descritti i problemi sul lato servizio hello - errori di rete o archiviazione di esempio durante il download. |
| ErrorParsingConfiguration |Categoria di errori in cui attività <see cref="MediaTask.PrivateData"/> (configurazione) non è valido, ad esempio configurazione hello non predefinito di un sistema valido o contiene codice XML non valido. |
| ErrorExecutingTaskMalformedContent |Categoria di errori durante l'esecuzione di hello dell'attività hello in cui i problemi all'interno di hello input file multimediali provocare un errore. |
| ErrorExecutingTaskUnsupportedFormat |Categoria di errori in cui il processore di contenuti multimediali hello non è in grado di elaborare il file hello forniti: formato di file multimediale non supportato o non corrisponde a hello configurazione. Ad esempio, il tentativo tooproduce un output di solo audio da un'attività che ha il solo video |
| ErrorProcessingTask |Categoria di altri errori hello processore di contenuti multimediali rilevata durante l'elaborazione di hello dell'attività hello che sono toocontent non correlati. |
| ErrorUploadingOutputAsset |Categoria di errori durante il caricamento di asset di output di hello |
| ErrorCancelingTask |Categoria di errori di toocover errori durante il tentativo di hello toocancel attività |
| TransientError |Categoria di errori toocover temporanei i problemi (ad es. problemi di rete temporanei con Azure Storage) |

Guida tooget da hello **servizi multimediali** team, aprire un [ticket di supporto](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articoli correlati
* [Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Quote e limitazioni](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
