---
title: aaa "prospettive di Azure Analysis Services tutorial lezione 8 crea | Documenti di Microsoft"
description: Viene descritto come toocreate prospettive in hello progetto tutorial Azure Analysis Services.
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="37d19-103">Lezione 8: Creare prospettive</span><span class="sxs-lookup"><span data-stu-id="37d19-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="37d19-104">In questa lezione verrà creata una prospettiva Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="37d19-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="37d19-105">Una prospettiva definisce un subset visualizzabile di un modello che offre punti di vista mirati, specifici di un'azienda o specifici di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="37d19-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="37d19-106">Quando un utente si connette tooa modello utilizzando una prospettiva, vengono visualizzati solo gli oggetti modello (tabelle, colonne, misure, gerarchie e indicatori KPI) come campi definiti in tale prospettiva.</span><span class="sxs-lookup"><span data-stu-id="37d19-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="37d19-107">vedere, più toolearn [prospettive](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="37d19-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="37d19-108">Hello prospettiva Internet Sales è stato creato in questa lezione esclude l'oggetto della tabella DimCustomer hello.</span><span class="sxs-lookup"><span data-stu-id="37d19-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="37d19-109">Quando si crea una prospettiva che esclude determinati oggetti dalla visualizzazione, l'oggetto esiste ancora nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="37d19-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="37d19-110">ma non è visibile in un elenco di campi del client per la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="37d19-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="37d19-111">Le colonne e le misure calcolate, indipendentemente dal fatto che siano incluse o meno in una prospettiva, possono comunque essere calcolate in base ai dati degli oggetti esclusi.</span><span class="sxs-lookup"><span data-stu-id="37d19-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="37d19-112">scopo di Hello in questa lezione è toodescribe come toocreate prospettive e acquisire familiarità con gli strumenti di creazione di modelli tabulari hello.</span><span class="sxs-lookup"><span data-stu-id="37d19-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="37d19-113">Se successivamente si espande questo tabelle aggiuntive tooinclude di modello, è possibile creare ulteriori prospettive toodefine diversi punti di vista del modello di hello, ad esempio, vendite e inventario.</span><span class="sxs-lookup"><span data-stu-id="37d19-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="37d19-114">Stimato toocomplete ora questa lezione: **cinque minuti**</span><span class="sxs-lookup"><span data-stu-id="37d19-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="37d19-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="37d19-115">Prerequisites</span></span>  
<span data-ttu-id="37d19-116">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="37d19-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="37d19-117">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 7: creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="37d19-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="37d19-118">Creare prospettive</span><span class="sxs-lookup"><span data-stu-id="37d19-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="37d19-119">toocreate una prospettiva Internet Sales</span><span class="sxs-lookup"><span data-stu-id="37d19-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="37d19-120">Fare clic su hello **modello** menu > **prospettive** > **crea e Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="37d19-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="37d19-121">In hello **prospettive** la finestra di dialogo, fare clic su **nuova prospettiva**.</span><span class="sxs-lookup"><span data-stu-id="37d19-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="37d19-122">Fare doppio clic su hello **nuova prospettiva** intestazione di colonna e quindi rinominare **Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="37d19-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="37d19-123">Selezionare hello tutte le tabelle di hello *tranne* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="37d19-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="37d19-125">In una lezione successiva, utilizzare hello analizza in Excel funzionalità tootest questa prospettiva.</span><span class="sxs-lookup"><span data-stu-id="37d19-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="37d19-126">Hello elenco campi tabella pivot di Excel include ogni tabella ad eccezione di tabella DimCustomer hello.</span><span class="sxs-lookup"><span data-stu-id="37d19-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="37d19-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37d19-127">What's next?</span></span>
<span data-ttu-id="37d19-128">[Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="37d19-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
