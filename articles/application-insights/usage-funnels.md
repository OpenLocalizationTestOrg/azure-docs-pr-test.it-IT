---
title: Imbuti di Azure Application Insights
description: Informazioni su come usare gli imbuti per scoprire in che modo i clienti interagiscono con l'applicazione.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 59c4dfafc102b26e3b9873f433065715f4aec9ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="82b23-103">Informazioni sulle modalità di utilizzo dell'applicazione da parte dei clienti attraverso gli imbuti di Application Insights</span><span class="sxs-lookup"><span data-stu-id="82b23-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="82b23-104">Per un'azienda è di primaria importanza analizzare l'utilizzo del software da parte dei clienti.</span><span class="sxs-lookup"><span data-stu-id="82b23-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="82b23-105">Se l'applicazione implica più fasi, è necessario sapere se la maggior parte dei clienti prosegue lungo l'intero processo o se lo termina in un determinato punto.</span><span class="sxs-lookup"><span data-stu-id="82b23-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="82b23-106">L'avanzamento attraverso una serie di passaggi in un'applicazione Web è noto come "imbuto".</span><span class="sxs-lookup"><span data-stu-id="82b23-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="82b23-107">È possibile usare gli imbuti di Application Insights per ottenere informazioni approfondite sugli utenti e per monitorare i tassi di conversione a ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="82b23-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="82b23-108">Introduzione al pannello Imbuti</span><span class="sxs-lookup"><span data-stu-id="82b23-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="82b23-109">Il modo più semplice per imparare a usare gli imbuti consiste nel seguire un esempio.</span><span class="sxs-lookup"><span data-stu-id="82b23-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="82b23-110">Le illustrazioni seguenti mostrano i passaggi che i proprietari di un'azienda di e-commerce devono seguire per scoprire in che modo i clienti interagiscono con l'applicazione Web dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="82b23-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="82b23-111">Creare il proprio imbuto</span><span class="sxs-lookup"><span data-stu-id="82b23-111">Create your funnel</span></span>
<span data-ttu-id="82b23-112">Prima di creare il proprio imbuto, è necessario decidere a quale domanda si intende rispondere.</span><span class="sxs-lookup"><span data-stu-id="82b23-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="82b23-113">Si potrebbe ad esempio voler scoprire quanti clienti tra quelli che visitano la home page del sito selezionano un annuncio.</span><span class="sxs-lookup"><span data-stu-id="82b23-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="82b23-114">In questo esempio, i proprietari della società Fabrikam Fiber desiderano conoscere la percentuale di clienti che ha effettuato l'acquisto dopo avere aggiunto articoli al carrello acquisti nell'ultimo mese.</span><span class="sxs-lookup"><span data-stu-id="82b23-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="82b23-115">Ecco i passaggi per creare l'imbuto.</span><span class="sxs-lookup"><span data-stu-id="82b23-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="82b23-116">Fare clic sul pulsante Nuovo nel pannello Imbuti.</span><span class="sxs-lookup"><span data-stu-id="82b23-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="82b23-117">Selezionare l'intervallo di tempo "Ultimo mese" dal menu a discesa **Intervallo di tempo**.</span><span class="sxs-lookup"><span data-stu-id="82b23-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="82b23-118">Selezionare l'evento **Product page** (Pagina prodotto) dall'elenco a discesa **Step 1** (Passaggio 1).</span><span class="sxs-lookup"><span data-stu-id="82b23-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="82b23-119">Selezionare l'evento **Add to shopping cart** (Aggiungi al carrello acquisti) dall'elenco a discesa **Step 2** (Passaggio 2).</span><span class="sxs-lookup"><span data-stu-id="82b23-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="82b23-120">Selezionare l'evento **Click purchase** (Clic su acquisto) dall'elenco a discesa **Step 3** (Passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="82b23-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="82b23-121">Aggiungere un nome per l'imbuto e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="82b23-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="82b23-122">La figura seguente mostra i dati generati dal pannello Imbuti.</span><span class="sxs-lookup"><span data-stu-id="82b23-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="82b23-123">Da qui i proprietari di Fabrikam possono vedere che, durante l'ultima settimana, il 22,7% dei clienti che hanno aggiunto un articolo al carrello acquisti ha completato l'acquisto.</span><span class="sxs-lookup"><span data-stu-id="82b23-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="82b23-124">Possono inoltre vedere che l'1% dei clienti ha fatto clic su un annuncio prima di visitare la pagina del prodotto e che il 20% dei clienti si è disconnesso dopo avere completato l'acquisto.</span><span class="sxs-lookup"><span data-stu-id="82b23-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Pannello Imbuti con dati](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="82b23-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82b23-126">Next steps</span></span>
  * [<span data-ttu-id="82b23-127">Panoramica sull'uso</span><span class="sxs-lookup"><span data-stu-id="82b23-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="82b23-128">Utenti, Sessioni ed Eventi</span><span class="sxs-lookup"><span data-stu-id="82b23-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="82b23-129">Conservazione</span><span class="sxs-lookup"><span data-stu-id="82b23-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="82b23-130">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="82b23-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="82b23-131">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="82b23-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
