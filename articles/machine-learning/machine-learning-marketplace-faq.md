---
title: (deprecato) Domande frequenti sulla pubblicazione e sull'uso di app di Machine Learning in Azure Marketplace | Documentazione Microsoft
description: (deprecato) Domande frequenti sulla pubblicazione di app di Machine Learning in Azure Marketplace
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="621e9-103">(deprecato) Domande frequenti sulla pubblicazione e sull'uso di app di Machine Learning in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="621e9-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="621e9-104">DataMarket e Servizi dati verranno ritirati e le sottoscrizioni esistenti verranno ritirate e annullate a partire dal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="621e9-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="621e9-105">Di conseguenza, questo articolo è deprecato.</span><span class="sxs-lookup"><span data-stu-id="621e9-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="621e9-106">In alternativa, è possibile pubblicare gli esperimenti di Machine Learning in [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) a vantaggio della community scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="621e9-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="621e9-107">Per altre informazioni, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="621e9-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="621e9-108">Domande sull'utilizzo da Marketplace</span><span class="sxs-lookup"><span data-stu-id="621e9-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="621e9-109">**1. Perché viene generato il messaggio di errore seguente dopo l'immissione di dati di input per il servizio Web?**</span><span class="sxs-lookup"><span data-stu-id="621e9-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="621e9-110">**La richiesta ha avuto come risultato un timeout di back-end o un errore di back-end. Il team sta esaminando questo problema. Ci scusiamo per l'inconveniente. (500)**</span><span class="sxs-lookup"><span data-stu-id="621e9-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="621e9-111">È possibile che i parametri di input immessi non siano conformi al formato richiesto per il servizio Web specifico.</span><span class="sxs-lookup"><span data-stu-id="621e9-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="621e9-112">Fare riferimento al collegamento seguente relativo alla documentazione per individuare il formato corretto per i parametri di input e per informazioni sulle limitazioni di questo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="621e9-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="621e9-113">**2. Se si copia il collegamento all'API per il servizio Web disponibile in "Esplorare il set di dati" e lo si incolla in un'altra finestra del browser, quali credenziali è necessario usare per accedere ai risultati e come vengono visualizzati?**</span><span class="sxs-lookup"><span data-stu-id="621e9-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="621e9-114">È consigliabile usare l'account Marketplace come nome utente e la chiave dell'account principale come password.</span><span class="sxs-lookup"><span data-stu-id="621e9-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="621e9-115">La chiave dell'account principale è disponibile nella pagina **Esplorare il set di dati**, sotto la descrizione del servizio Web (fare clic sul pulsante **Mostra**).</span><span class="sxs-lookup"><span data-stu-id="621e9-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="621e9-116">È possibile che il risultato venga visualizzato nel browser o che sia disponibile per il download, a seconda del browser usato.</span><span class="sxs-lookup"><span data-stu-id="621e9-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="621e9-117">**3. Perché viene generato il messaggio di errore seguente dopo l'immissione di dati di input per il servizio Web nella pagina "Esplorare il set di dati"?**</span><span class="sxs-lookup"><span data-stu-id="621e9-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="621e9-118">**Si è verificato un errore imprevisto durante l'elaborazione della richiesta. Riprovare più tardi.**</span><span class="sxs-lookup"><span data-stu-id="621e9-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="621e9-119">È possibile che uno o più parametri di input del servizio Web abbiano superato il limite di lunghezza durante l'utilizzo del servizio Web nella pagina **Esplorare il set di dati** del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="621e9-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="621e9-120">I servizi possono essere chiamati con una lunghezza di input maggiore usando i metodi HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="621e9-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="621e9-121">Per esempi, vedere l'argomento relativo alle [soluzioni di esempio sull'uso di R in Machine Learning e pubblicate in Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="621e9-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="621e9-122">**4. Perché non riesco a visualizzare i risultati nella scheda "ESPLORA API" nello Store del portale di Azure classico?**</span><span class="sxs-lookup"><span data-stu-id="621e9-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="621e9-123">Si tratta di un problema noto con il Marketplace del portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="621e9-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="621e9-124">Il team è impegnato nella risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="621e9-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="621e9-125">Domande sulla pubblicazione da Azure Machine Learning nel Marketplace</span><span class="sxs-lookup"><span data-stu-id="621e9-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="621e9-126">**1. Perché i logo, le immagini e il numero di transazioni non vengono aggiornati per il servizio Web?**</span><span class="sxs-lookup"><span data-stu-id="621e9-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="621e9-127">I logo e le immagini vengono memorizzati nella cache del portale di pubblicazione e potrebbero essere necessari fino a 10 giorni per l'aggiornamento del nuovo logo o della nuova immagine nel portale.</span><span class="sxs-lookup"><span data-stu-id="621e9-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="621e9-128">**2. Perché nella scheda "Dettagli" del servizio Web nel Marketplace viene visualizzato un errore?**</span><span class="sxs-lookup"><span data-stu-id="621e9-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="621e9-129">Si tratta di un problema noto del Marketplace durante la connessione ad Azure Machine Learning per ottenere informazioni dettagliate sui servizi.</span><span class="sxs-lookup"><span data-stu-id="621e9-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="621e9-130">Il team è impegnato nella risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="621e9-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="621e9-131">**3. Perché il codice R di esempio nei servizi Web di Azure Machine Learning non funziona per l'uso dei servizi Web nel Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="621e9-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="621e9-132">I sistemi di autenticazione presentano differenze in caso di connessione diretta ai servizi Web di Azure Machine Learning rispetto alla connessione a questi servizi Web tramite il Marketplace.</span><span class="sxs-lookup"><span data-stu-id="621e9-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="621e9-133">I servizi disponibili in Marketplace sono servizi OData e possono essere chiamati tramite metodi GET o POST.</span><span class="sxs-lookup"><span data-stu-id="621e9-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="621e9-134">**4. Perché i collegamenti per il supporto delle offerte del servizio Web non vengono aggiornati correttamente per alcune offerte?**</span><span class="sxs-lookup"><span data-stu-id="621e9-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="621e9-135">I collegamenti per il supporto sono globali per le singole entità di pubblicazione e non sono specifici per le singole offerte.</span><span class="sxs-lookup"><span data-stu-id="621e9-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="621e9-136">**5. Come si pubblica un servizio Web con modalità di input batch nel Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="621e9-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="621e9-137">La modalità di input batch non è attualmente supportata nei servizi Web del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="621e9-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="621e9-138">**6. A chi ci si deve rivolgere per ottenere supporto in caso di domande su come diventare un'entità di pubblicazione di dati o in caso di problemi durante la pubblicazione?**</span><span class="sxs-lookup"><span data-stu-id="621e9-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="621e9-139">Per altre informazioni, contattare il team di Azure Marketplace in <mailto:datamarketbd@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="621e9-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

