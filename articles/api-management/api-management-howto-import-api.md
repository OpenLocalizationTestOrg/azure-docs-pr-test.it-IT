---
title: aaaImport un'API in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come tooimport un'API e le relative operazioni in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Come tooimport hello definizione di un'API con le operazioni di gestione API di Azure
In Gestione API, è possibile creare nuove API e operazioni hello aggiunte manualmente o hello API può essere importati insieme a operazioni di hello in un unico passaggio.

Le API e le relative operazioni possono essere importate utilizzando i seguenti formati hello.

* WADL
* Swagger

In questa guida viene illustrato come creare una nuova API e importarne le operazioni in un unico passaggio. Per informazioni sulla creazione manuale di un'API e l'aggiunta di operazioni, vedere [come toocreate API] [ How toocreate APIs] e [come tooadd operazioni tooan API] [ How tooadd operations tooan API].

## <a name="import-api"></a>Importare un'API
API create e configurate nel portale di pubblicazione hello. Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.

![Portale di pubblicazione][api-management-management-console]

Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importare API**.

![Importa API][api-management-import-apis]

Hello **importazione API** finestra contiene tre schede corrispondenti specifica hello API tooprovide di toohello tre modi.

* **Dagli Appunti** consente specifica hello API toopaste nella casella di testo hello.
* **Dal file** consente toobrowse tooand hello selezionare contenente la specifica di hello API.
* **Dall'URL** consente toosupply hello toohello la specifica URL per hello API.

![Formato di importazione API][api-management-import-api-clipboard]

Dopo aver fornito specifica hello API, usare i pulsanti hello sul formato di hello tooindicate destra hello specifica. Hello seguenti formati è supportato.

* WADL
* Swagger

Quindi, immettere un **Suffisso dell'URL dell'API Web**. Si tratta di URL di base toohello accodato per il servizio Gestione API. URL di base Hello è comune per tutte le API ospitate in ogni istanza di un servizio di gestione API. Gestione API consente di distinguere le API per il suffisso e pertanto suffisso hello deve essere univoco per ogni API in un'istanza specifica del servizio Gestione API.

Una volta tutti i valori, fare clic su **salvare** toocreate hello API e hello associati operazioni. 

> [!NOTE]
> Per un'esercitazione relativa all'importazione di un'API di calcolatrice di base in formato Swagger, vedere [Gestire la prima API in Gestione API di Azure](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Esportare un'API
In aggiunta tooimporting nuove API, è possibile esportare le definizioni di hello delle API dal portale di pubblicazione hello. toodo in tal caso, fare clic su **esportare API** da hello **scheda riepilogo** del **API**.

![Esporta API][api-management-export-api]

Le API possono essere esportate con WADL o Swagger. Selezionare il formato desiderato di hello, fare clic su **salvare**e scegliere il percorso di hello toosave file hello.

![Formato di esportazione API][api-management-export-api-format]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creata un'API e operazioni hello importate, è possibile esaminare e configurare eventuali impostazioni aggiuntive, aggiungere hello API tooa prodotto e pubblicarlo in modo che sia disponibile per gli sviluppatori. Per ulteriori informazioni, vedere hello seguenti guide.

* [Come impostazioni tooconfigure API][How tooconfigure API settings]
* [Come toocreate e pubblicazione di un prodotto][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
