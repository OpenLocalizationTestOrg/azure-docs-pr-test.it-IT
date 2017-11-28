---
title: "livello di compatibilità aaaData modello in Analysis Services di Azure | Documenti Microsoft"
description: "Informazioni sul livello di compatibilità del modello di dati tabulari."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="46d4b-103">Livello di compatibilità per i modelli tabulari di Analysis Services</span><span class="sxs-lookup"><span data-stu-id="46d4b-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="46d4b-104">*Livello di compatibilità* fa riferimento toorelease specifici comportamenti nel motore di Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="46d4b-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="46d4b-105">Livello di compatibilità toohello modifiche in genere coincide con le versioni principali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="46d4b-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="46d4b-106">Queste modifiche vengono inoltre implementate in entrambe le piattaforme analogia toomaintain Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="46d4b-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="46d4b-107">Le modifiche del livello di compatibilità influiscono anche sulle funzionalità disponibili nei modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="46d4b-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="46d4b-108">Ad esempio, DirectQuery e i metadati degli oggetti tabulari sono implementazioni diverse in base al livello di compatibilità hello.</span><span class="sxs-lookup"><span data-stu-id="46d4b-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="46d4b-109">Azure Analysis Services supporta modelli tabulari con livelli di compatibilità 1200 e 1400 di hello.</span><span class="sxs-lookup"><span data-stu-id="46d4b-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="46d4b-110">livello di compatibilità più recente di Hello è 1400.</span><span class="sxs-lookup"><span data-stu-id="46d4b-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="46d4b-111">Questo livello corrisponde a SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="46d4b-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="46d4b-112">Le funzionalità principali nel livello di compatibilità 1400 hello includono:</span><span class="sxs-lookup"><span data-stu-id="46d4b-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="46d4b-113">Nuova infrastruttura per la connettività dati e per l'importazione in modelli tabulari con il supporto delle API TOM e degli script TMSL.</span><span class="sxs-lookup"><span data-stu-id="46d4b-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="46d4b-114">Questa nuova funzionalità consente il supporto per origini dati aggiuntive, ad esempio l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="46d4b-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="46d4b-115">Funzionalità di trasformazione e mashup dei dati tramite Recupera dati ed espressioni M.</span><span class="sxs-lookup"><span data-stu-id="46d4b-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="46d4b-116">Le misure supportano una proprietà Espressione di righe di dettaglio con un'espressione DAX.</span><span class="sxs-lookup"><span data-stu-id="46d4b-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="46d4b-117">Questa proprietà consente di strumenti client quali Microsoft Excel toodrill toodetailed dati da un report aggregato.</span><span class="sxs-lookup"><span data-stu-id="46d4b-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="46d4b-118">Ad esempio, quando gli utenti di visualizzare le vendite totali per una regione e un mese, è possibile visualizzare dettagli dell'ordine hello associata.</span><span class="sxs-lookup"><span data-stu-id="46d4b-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="46d4b-119">Sicurezza a livello di oggetto per la tabella e colonna i nomi di inoltre toohello dati all'interno di essi.</span><span class="sxs-lookup"><span data-stu-id="46d4b-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="46d4b-120">Supporto migliorato per le gerarchie incomplete.</span><span class="sxs-lookup"><span data-stu-id="46d4b-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="46d4b-121">Miglioramenti per prestazioni e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="46d4b-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="46d4b-122">Impostare il livello di compatibilità</span><span class="sxs-lookup"><span data-stu-id="46d4b-122">Set compatibility level</span></span> 
 <span data-ttu-id="46d4b-123">Quando si crea un nuovo progetto di modello tabulare in SSDT, è possibile specificare il livello di compatibilità di hello in hello **progettazione di modelli tabulari** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="46d4b-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="46d4b-125">Se si seleziona hello **non visualizzare più questo messaggio** opzione, il livello di compatibilità hello specificato come valore predefinito di hello di utilizzare tutti i progetti successivi.</span><span class="sxs-lookup"><span data-stu-id="46d4b-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="46d4b-126">È possibile modificare a livello di compatibilità predefinito hello in SSDT in **strumenti** > **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="46d4b-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="46d4b-127">un progetto di modello tabulare esistente in SSDT, hello set tooupgrade **livello di compatibilità** proprietà nel modello hello **proprietà** finestra.</span><span class="sxs-lookup"><span data-stu-id="46d4b-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="46d4b-128">Tenere presente, l'aggiornamento a livello di compatibilità hello è irreversibile.</span><span class="sxs-lookup"><span data-stu-id="46d4b-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="46d4b-129">Controllare il livello di compatibilità per un database con modello tabulare in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="46d4b-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="46d4b-130">In SQL Server Management Studio, fare clic sul nome del database hello > **proprietà** > **livello di compatibilità**.</span><span class="sxs-lookup"><span data-stu-id="46d4b-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="46d4b-131">Controllare il livello di compatibilità supportato per un server in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="46d4b-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="46d4b-132">In SQL Server Management Studio, fare clic sul nome del server hello > **proprietà** > **livello di compatibilità supportato**.</span><span class="sxs-lookup"><span data-stu-id="46d4b-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="46d4b-133">Questa proprietà specifica hello massimo livello di compatibilità di un database che verrà eseguiti nel server di hello (escluso preview).</span><span class="sxs-lookup"><span data-stu-id="46d4b-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="46d4b-134">Impossibile modificare il livello di compatibilità di Hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="46d4b-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="46d4b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46d4b-135">Next steps</span></span>
  <span data-ttu-id="46d4b-136">[Creare un modello nel portale di Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="46d4b-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="46d4b-137">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="46d4b-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
