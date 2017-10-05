---
title: Importare un'API in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come importare un'API e le relative operazioni in Gestione API di Azure.
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
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="f64ad-103">Come importare la definizione di un'API con le operazioni in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f64ad-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="f64ad-104">In Gestione API è possibile creare nuove API e aggiungere manualmente le operazioni oppure è possibile importare l'API insieme alle operazioni in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="f64ad-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="f64ad-105">Le API e le relative operazioni possono essere importate usando i seguenti formati.</span><span class="sxs-lookup"><span data-stu-id="f64ad-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="f64ad-106">WADL</span><span class="sxs-lookup"><span data-stu-id="f64ad-106">WADL</span></span>
* <span data-ttu-id="f64ad-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="f64ad-107">Swagger</span></span>

<span data-ttu-id="f64ad-108">In questa guida viene illustrato come creare una nuova API e importarne le operazioni in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="f64ad-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="f64ad-109">Per informazioni su come creare un'API e aggiungere le operazioni, vedere [Come creare le API][How to create APIs] e [Come aggiungere operazioni a un'API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="f64ad-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="f64ad-110"><a name="import-api"> </a>Importare un'API</span><span class="sxs-lookup"><span data-stu-id="f64ad-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="f64ad-111">Le API vengono create e configurate nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f64ad-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="f64ad-112">Per accedere al portale di pubblicazione, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="f64ad-113">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f64ad-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="f64ad-115">Fare clic su **APi** dal menu **Gestione API** sulla sinistra, quindi scegliere **Importa API**.</span><span class="sxs-lookup"><span data-stu-id="f64ad-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Importa API][api-management-import-apis]

<span data-ttu-id="f64ad-117">La finestra **Importa API** contiene tre schede che corrispondono alle tre modalità con cui è possibile fornire la specifica API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="f64ad-118">**Da Appunti** consente di incollare la specifica API nella casella di testo indicata.</span><span class="sxs-lookup"><span data-stu-id="f64ad-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="f64ad-119">**Da file** consente di sfogliare e selezionare il file che contiene la specifica API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="f64ad-120">**Da URL** consente di fornire l'URL alla specifica per l'API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Formato di importazione API][api-management-import-api-clipboard]

<span data-ttu-id="f64ad-122">Dopo aver fornito la specifica API, usare i pulsanti di opzione a destra per indicare il formato della specifica.</span><span class="sxs-lookup"><span data-stu-id="f64ad-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="f64ad-123">Sono supportati i seguenti formati.</span><span class="sxs-lookup"><span data-stu-id="f64ad-123">The following formats are supported.</span></span>

* <span data-ttu-id="f64ad-124">WADL</span><span class="sxs-lookup"><span data-stu-id="f64ad-124">WADL</span></span>
* <span data-ttu-id="f64ad-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="f64ad-125">Swagger</span></span>

<span data-ttu-id="f64ad-126">Quindi, immettere un **Suffisso dell'URL dell'API Web**.</span><span class="sxs-lookup"><span data-stu-id="f64ad-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="f64ad-127">Il suffisso viene aggiunto all'URL di base del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="f64ad-128">L'URL di base è comune a tutte le API ospitate in un'istanza di un servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="f64ad-129">Gestione API distingue le API in base al suffisso, quindi è necessario che questo sia univoco per ciascuna API in ciascuna istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f64ad-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="f64ad-130">Dopo aver immesso tutti i valori, fare clic su **Salva** per creare l'API e le operazioni associate.</span><span class="sxs-lookup"><span data-stu-id="f64ad-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="f64ad-131">Per un'esercitazione relativa all'importazione di un'API di calcolatrice di base in formato Swagger, vedere [Gestire la prima API in Gestione API di Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f64ad-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="f64ad-132"><a name="export-api"> </a> Esportare un'API</span><span class="sxs-lookup"><span data-stu-id="f64ad-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="f64ad-133">Oltre a importare nuove API, è possibile esportare le definizioni delle API dal portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f64ad-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="f64ad-134">Per farlo, fare clic su **Esporta API** dalla scheda **Riepilogo** dell'**API**.</span><span class="sxs-lookup"><span data-stu-id="f64ad-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Esporta API][api-management-export-api]

<span data-ttu-id="f64ad-136">Le API possono essere esportate con WADL o Swagger.</span><span class="sxs-lookup"><span data-stu-id="f64ad-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="f64ad-137">Selezionare il formato desiderato, fare clic su **Salva**e scegliere il percorso in cui salvare il file.</span><span class="sxs-lookup"><span data-stu-id="f64ad-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Formato di esportazione API][api-management-export-api-format]

## <span data-ttu-id="f64ad-139"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f64ad-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f64ad-140">Dopo aver creato un'API ed importato le operazioni, è possibile rivedere e configurare tutte le impostazioni aggiuntive, aggiungere l'API a un prodotto e pubblicarla in modo che sia disponibile per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="f64ad-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="f64ad-141">Per altre informazioni, vedere le seguenti guide.</span><span class="sxs-lookup"><span data-stu-id="f64ad-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="f64ad-142">[Come configurare le impostazioni API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="f64ad-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="f64ad-143">[Come creare e pubblicare un prodotto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="f64ad-143">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
