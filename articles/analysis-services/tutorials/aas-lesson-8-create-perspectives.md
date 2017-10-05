---
title: 'Esercitazione su Azure Analysis Services - Lezione 8: Creare prospettive | Microsoft Docs'
description: Descrive come creare prospettive nel progetto per l'esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="27ed8-103">Lezione 8: Creare prospettive</span><span class="sxs-lookup"><span data-stu-id="27ed8-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="27ed8-104">In questa lezione verrà creata una prospettiva Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="27ed8-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="27ed8-105">Una prospettiva definisce un subset visualizzabile di un modello che offre punti di vista mirati, specifici di un'azienda o specifici di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="27ed8-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="27ed8-106">Quando un utente si connette a un modello usando una prospettiva, vengono visualizzati solo gli oggetti del modello (tabelle, colonne, misure, gerarchie e indicatori KPI) come campi definiti in tale prospettiva.</span><span class="sxs-lookup"><span data-stu-id="27ed8-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="27ed8-107">Per altre informazioni, vedere [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular) (Prospettive).</span><span class="sxs-lookup"><span data-stu-id="27ed8-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="27ed8-108">La prospettiva Internet Sales che viene creata in questa lezione esclude l'oggetto tabella DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="27ed8-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="27ed8-109">Quando si crea una prospettiva che esclude determinati oggetti dalla visualizzazione, l'oggetto esiste ancora nel modello,</span><span class="sxs-lookup"><span data-stu-id="27ed8-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="27ed8-110">ma non è visibile in un elenco di campi del client per la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="27ed8-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="27ed8-111">Le colonne e le misure calcolate, indipendentemente dal fatto che siano incluse o meno in una prospettiva, possono comunque essere calcolate in base ai dati degli oggetti esclusi.</span><span class="sxs-lookup"><span data-stu-id="27ed8-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="27ed8-112">Lo scopo di questa lezione è descrivere come creare prospettive e acquisire familiarità con gli strumenti per la creazione di modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="27ed8-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="27ed8-113">Se successivamente si espande questo modello per includere ulteriori tabelle, è possibile creare altre prospettive per definire punti di vista diversi del modello, ad esempio, inventario e vendite.</span><span class="sxs-lookup"><span data-stu-id="27ed8-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="27ed8-114">Tempo previsto per il completamento della lezione: **cinque minuti**</span><span class="sxs-lookup"><span data-stu-id="27ed8-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="27ed8-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27ed8-115">Prerequisites</span></span>  
<span data-ttu-id="27ed8-116">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="27ed8-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="27ed8-117">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 7: Creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="27ed8-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="27ed8-118">Creare prospettive</span><span class="sxs-lookup"><span data-stu-id="27ed8-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="27ed8-119">Per creare una prospettiva Internet Sales</span><span class="sxs-lookup"><span data-stu-id="27ed8-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="27ed8-120">Fare clic sul menu **Modello** > **Prospettive** > **Crea e gestisci**.</span><span class="sxs-lookup"><span data-stu-id="27ed8-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="27ed8-121">Nella finestra di dialogo **Prospettive** fare clic su **Nuova prospettiva**.</span><span class="sxs-lookup"><span data-stu-id="27ed8-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="27ed8-122">Fare doppio clic sull'intestazione di colonna **Nuova prospettiva** e quindi rinominarla **Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="27ed8-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="27ed8-123">Selezionare tutte le tabelle *tranne* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="27ed8-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="27ed8-125">In una lezione successiva si userà la funzionalità Analizza in Excel per testare questa prospettiva.</span><span class="sxs-lookup"><span data-stu-id="27ed8-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="27ed8-126">L'elenco dei campi della tabella pivot di Excel include tutte le tabelle tranne DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="27ed8-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="27ed8-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27ed8-127">What's next?</span></span>
<span data-ttu-id="27ed8-128">[Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="27ed8-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
