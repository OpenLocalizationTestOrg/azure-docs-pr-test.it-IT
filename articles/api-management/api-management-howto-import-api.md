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
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="8a310-103">Come tooimport hello definizione di un'API con le operazioni di gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="8a310-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="8a310-104">In Gestione API, è possibile creare nuove API e operazioni hello aggiunte manualmente o hello API può essere importati insieme a operazioni di hello in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="8a310-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="8a310-105">Le API e le relative operazioni possono essere importate utilizzando i seguenti formati hello.</span><span class="sxs-lookup"><span data-stu-id="8a310-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="8a310-106">WADL</span><span class="sxs-lookup"><span data-stu-id="8a310-106">WADL</span></span>
* <span data-ttu-id="8a310-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="8a310-107">Swagger</span></span>

<span data-ttu-id="8a310-108">In questa guida viene illustrato come creare una nuova API e importarne le operazioni in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="8a310-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="8a310-109">Per informazioni sulla creazione manuale di un'API e l'aggiunta di operazioni, vedere [come toocreate API] [ How toocreate APIs] e [come tooadd operazioni tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="8a310-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="8a310-110"><a name="import-api"></a>Importare un'API</span><span class="sxs-lookup"><span data-stu-id="8a310-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="8a310-111">API create e configurate nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8a310-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="8a310-112">Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8a310-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="8a310-113">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8a310-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="8a310-115">Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importare API**.</span><span class="sxs-lookup"><span data-stu-id="8a310-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Importa API][api-management-import-apis]

<span data-ttu-id="8a310-117">Hello **importazione API** finestra contiene tre schede corrispondenti specifica hello API tooprovide di toohello tre modi.</span><span class="sxs-lookup"><span data-stu-id="8a310-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="8a310-118">**Dagli Appunti** consente specifica hello API toopaste nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="8a310-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="8a310-119">**Dal file** consente toobrowse tooand hello selezionare contenente la specifica di hello API.</span><span class="sxs-lookup"><span data-stu-id="8a310-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="8a310-120">**Dall'URL** consente toosupply hello toohello la specifica URL per hello API.</span><span class="sxs-lookup"><span data-stu-id="8a310-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Formato di importazione API][api-management-import-api-clipboard]

<span data-ttu-id="8a310-122">Dopo aver fornito specifica hello API, usare i pulsanti hello sul formato di hello tooindicate destra hello specifica.</span><span class="sxs-lookup"><span data-stu-id="8a310-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="8a310-123">Hello seguenti formati è supportato.</span><span class="sxs-lookup"><span data-stu-id="8a310-123">hello following formats are supported.</span></span>

* <span data-ttu-id="8a310-124">WADL</span><span class="sxs-lookup"><span data-stu-id="8a310-124">WADL</span></span>
* <span data-ttu-id="8a310-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="8a310-125">Swagger</span></span>

<span data-ttu-id="8a310-126">Quindi, immettere un **Suffisso dell'URL dell'API Web**.</span><span class="sxs-lookup"><span data-stu-id="8a310-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="8a310-127">Si tratta di URL di base toohello accodato per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8a310-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="8a310-128">URL di base Hello è comune per tutte le API ospitate in ogni istanza di un servizio di gestione API.</span><span class="sxs-lookup"><span data-stu-id="8a310-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="8a310-129">Gestione API consente di distinguere le API per il suffisso e pertanto suffisso hello deve essere univoco per ogni API in un'istanza specifica del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8a310-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="8a310-130">Una volta tutti i valori, fare clic su **salvare** toocreate hello API e hello associati operazioni.</span><span class="sxs-lookup"><span data-stu-id="8a310-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="8a310-131">Per un'esercitazione relativa all'importazione di un'API di calcolatrice di base in formato Swagger, vedere [Gestire la prima API in Gestione API di Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a310-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="8a310-132"><a name="export-api"></a> Esportare un'API</span><span class="sxs-lookup"><span data-stu-id="8a310-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="8a310-133">In aggiunta tooimporting nuove API, è possibile esportare le definizioni di hello delle API dal portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8a310-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="8a310-134">toodo in tal caso, fare clic su **esportare API** da hello **scheda riepilogo** del **API**.</span><span class="sxs-lookup"><span data-stu-id="8a310-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Esporta API][api-management-export-api]

<span data-ttu-id="8a310-136">Le API possono essere esportate con WADL o Swagger.</span><span class="sxs-lookup"><span data-stu-id="8a310-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="8a310-137">Selezionare il formato desiderato di hello, fare clic su **salvare**e scegliere il percorso di hello toosave file hello.</span><span class="sxs-lookup"><span data-stu-id="8a310-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Formato di esportazione API][api-management-export-api-format]

## <span data-ttu-id="8a310-139"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a310-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="8a310-140">Dopo aver creata un'API e operazioni hello importate, è possibile esaminare e configurare eventuali impostazioni aggiuntive, aggiungere hello API tooa prodotto e pubblicarlo in modo che sia disponibile per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="8a310-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="8a310-141">Per ulteriori informazioni, vedere hello seguenti guide.</span><span class="sxs-lookup"><span data-stu-id="8a310-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="8a310-142">[Come impostazioni tooconfigure API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="8a310-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="8a310-143">[Come toocreate e pubblicazione di un prodotto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="8a310-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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
