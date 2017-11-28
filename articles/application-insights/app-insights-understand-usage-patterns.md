---
title: aaaAzure Application Insights grafici a imbuto
description: "Informazioni su come utilizzare grafici a imbuto toodiscover la modalità di interazione con l'applicazione ai clienti."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="2bc42-103">Scoprire come i clienti con l'applicazione hello Application Insights grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="2bc42-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="2bc42-104">Analisi utilizzo software conoscenza è di business tooyour di fondamentale importanza hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="2bc42-105">Se l'applicazione è costituita da più fasi, è necessario tooknow se la maggior parte dei clienti progrediscono intero processo hello o terminano processo hello in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="2bc42-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="2bc42-106">avanzamento Hello attraverso una serie di passaggi in un'applicazione web è noto come "a imbuto".</span><span class="sxs-lookup"><span data-stu-id="2bc42-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="2bc42-107">È possibile utilizzare hello Application Insights grafici a imbuto toogain approfondite gli utenti e i tassi di conversione dettagliate di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2bc42-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="2bc42-108">Introduzione a pannello di grafici a imbuto hello</span><span class="sxs-lookup"><span data-stu-id="2bc42-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="2bc42-109">toolearn modo più semplice di Hello sui grafici a imbuto è toowalk ma un esempio.</span><span class="sxs-lookup"><span data-stu-id="2bc42-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="2bc42-110">Hello nelle figure seguenti illustrano i proprietari di hello passaggi di un'attività di commercio elettronico richiederebbe toolearn interagiscono tra i clienti con le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="2bc42-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="2bc42-111">Creare il proprio imbuto</span><span class="sxs-lookup"><span data-stu-id="2bc42-111">Create your funnel</span></span>
<span data-ttu-id="2bc42-112">Prima di creare il grafico a imbuto, è necessario toodecide sulla domanda hello desiderato tooanswer.</span><span class="sxs-lookup"><span data-stu-id="2bc42-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="2bc42-113">Ad esempio, è necessario tooknow quanti clienti visualizzando l'home pagina, fare clic su un annuncio.</span><span class="sxs-lookup"><span data-stu-id="2bc42-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="2bc42-114">In questo esempio, i proprietari di hello di hello aziendale di Fabrikam Fiber desidera percentuale hello tooknow dei clienti che effettuano un acquisto dopo l'aggiunta di elementi tootheir carrello degli acquisti durante l'ultimo mese hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="2bc42-115">Ecco i passaggi di hello hanno toocreate relativi a imbuto.</span><span class="sxs-lookup"><span data-stu-id="2bc42-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="2bc42-116">Fare clic hello pulsante nuovo nel Pannello di grafici a imbuto hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="2bc42-117">Selezionare intervallo di tempo hello del "Ultimo mese" hello **intervallo di tempo** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2bc42-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="2bc42-118">Seleziona hello **pagina prodotto** evento da hello **passaggio 1** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2bc42-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="2bc42-119">Seleziona hello **Aggiungi tooshopping carrello** evento da hello **passaggio 2** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2bc42-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="2bc42-120">Seleziona hello **fare clic su Acquista** evento da hello **passaggio 3** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2bc42-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="2bc42-121">Aggiungere un grafico a imbuto toohello nome e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="2bc42-122">Hello figura seguente illustra il pannello di grafici a imbuto hello dati hello genera l'errore.</span><span class="sxs-lookup"><span data-stu-id="2bc42-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="2bc42-123">Da qui hello proprietari di Fabrikam possono vedere durante la settimana scorsa hello, 22,7% dei clienti che ha aggiunto un elemento di tootheir market carrello acquisti hello completato.</span><span class="sxs-lookup"><span data-stu-id="2bc42-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="2bc42-124">Possono inoltre verificare che % 1 di clienti hello scelto un annuncio prima di visitare la pagina di prodotto hello e 20% dei clienti effettuata la disconnessione dopo aver completato l'acquisto.</span><span class="sxs-lookup"><span data-stu-id="2bc42-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Pannello Imbuti con dati](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="2bc42-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bc42-126">Next steps</span></span>
- <span data-ttu-id="2bc42-127">Altre informazioni sull'[analisi dell'utilizzo](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bc42-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
