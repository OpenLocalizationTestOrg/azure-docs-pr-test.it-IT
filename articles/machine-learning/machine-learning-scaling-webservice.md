---
title: concorrenza tooincrease aaaHow di un servizio web Azure Machine Learning | Documenti Microsoft
description: Informazioni su come concorrenza tooincrease un Azure Machine Learning servizio web tramite l'aggiunta di altri endpoint.
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure machine learning, servizi Web, messa in funzione, scalabilità, endpoint, concorrenza"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="bcd31-104">Ridimensionamento di un servizio Web di Azure Machine Learning con l'aggiunta di altri endpoint</span><span class="sxs-lookup"><span data-stu-id="bcd31-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="bcd31-105">Questo argomento vengono descritte le tecniche applicabile tooa **classico** servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bcd31-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="bcd31-106">Per impostazione predefinita, ogni servizio Web pubblicato toosupport configurato 20 richieste simultanee e può essere a un massimo di 200 richieste simultanee.</span><span class="sxs-lookup"><span data-stu-id="bcd31-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="bcd31-107">Hello portale di Azure classico offre un modo tooset questo valore, Azure Machine Learning consente di ottimizzare automaticamente hello impostazione tooprovide hello migliori prestazioni per il servizio web e hello portale valore viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="bcd31-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="bcd31-108">Se si prevede di API hello toocall con un carico superiore al valore Max Concurrent Calls 200 supporterà, è necessario creare più endpoint in hello stesso servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bcd31-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="bcd31-109">È quindi possibile distribuire casualmente il carico tra tutti gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="bcd31-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="bcd31-110">Hello il ridimensionamento di un servizio Web è un'attività comune.</span><span class="sxs-lookup"><span data-stu-id="bcd31-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="bcd31-111">Tooscale alcuni motivi sono toosupport più di 200 richieste simultanee, aumentare la disponibilità tramite più endpoint o fornire endpoint separati per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="bcd31-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="bcd31-112">È possibile aumentare la scalabilità hello aggiungendo altri endpoint per hello stesso servizio Web tramite [portale di Azure classico](https://manage.windowsazure.com/) o hello [servizio Web di Azure Machine Learning](https://services.azureml.net/) portale.</span><span class="sxs-lookup"><span data-stu-id="bcd31-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="bcd31-113">Per altre informazioni sull'aggiunta di nuovi endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="bcd31-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="bcd31-114">Tenere presente che può essere negativo se non si chiama hello API con una frequenza elevata di conseguenza utilizzando un numero elevato di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="bcd31-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="bcd31-115">Se si inserisce un carico relativamente ridotto in un'API configurata per un carico elevato, è possibile visualizzare i timeout sporadici e/o picchi di latenza hello.</span><span class="sxs-lookup"><span data-stu-id="bcd31-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="bcd31-116">Hello che sincrone API vengono in genere utilizzate in situazioni in cui si desidera una bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="bcd31-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="bcd31-117">Latenza qui implica tempo hello necessario per l'API di hello toocomplete una richiesta e non viene tenuto in considerazione i ritardi di rete.</span><span class="sxs-lookup"><span data-stu-id="bcd31-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="bcd31-118">Si supponga di avere un'API con una latenza di 50 ms.</span><span class="sxs-lookup"><span data-stu-id="bcd31-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="bcd31-119">toofully utilizzare la capacità disponibile hello con livello di velocità elevata e Max Concurrent Calls = 20, è necessario toocall questa API 20 * 1000 / = 400 50 volte al secondo.</span><span class="sxs-lookup"><span data-stu-id="bcd31-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="bcd31-120">Questa estensione ulteriormente, un numero massimo di chiamate simultanee pari a 200 consente si toocall hello API 4000 volte al secondo, presupponendo una latenza di 50 ms.</span><span class="sxs-lookup"><span data-stu-id="bcd31-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
