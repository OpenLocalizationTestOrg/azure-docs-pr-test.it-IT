---
title: aaaHow tooview correlati asset di dati in Azure Data Catalog | Documenti Microsoft
description: Questo articolo spiega come tooview correlati asset di dati di un asset di dati selezionato in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="c2504-103">Correlazione asset di dati in Azure Data Catalog tooview?</span><span class="sxs-lookup"><span data-stu-id="c2504-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="c2504-104">Azure Data Catalog consente tooview dati asset correlati tooa selezionato dati asset e visualizzare le relazioni tra loro.</span><span class="sxs-lookup"><span data-stu-id="c2504-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="c2504-105">Origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="c2504-105">Supported data sources</span></span> 
<span data-ttu-id="c2504-106">Quando si registra l'asset di dati da hello seguenti origini dati, Azure Data Catalog registra automaticamente i metadati relativi a relazioni di join tra gli asset di dati hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="c2504-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="c2504-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c2504-107">SQL Server</span></span>
- <span data-ttu-id="c2504-108">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="c2504-108">Azure SQL Database</span></span>
- <span data-ttu-id="c2504-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="c2504-109">MySQL</span></span>
- <span data-ttu-id="c2504-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="c2504-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="c2504-111">Visualizzare gli asset di dati correlati</span><span class="sxs-lookup"><span data-stu-id="c2504-111">View related data assets</span></span>
<span data-ttu-id="c2504-112">tooview asset di dati che sono set di dati correlati tooa selezionato, utilizzare hello **relazioni** scheda come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="c2504-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog - Visualizzare gli asset di dati correlati](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="c2504-114">In questo esempio sono presenti due relazioni per hello selezionato **ProductSubcategory** asset di dati:</span><span class="sxs-lookup"><span data-stu-id="c2504-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="c2504-115">Colonna ProductSubcategoryID della tabella Product hello ha una relazione di chiave esterna con ProductSubcategoryID colonna della tabella ProductSubcategory hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="c2504-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="c2504-116">ProductCategoryID colonna della tabella ProductSubCategory hello ha una relazione di chiave esterna con ProductCategoryID colonna della tabella ProductCategory hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="c2504-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="c2504-117">Si noti la direzione hello della freccia hello nella visualizzazione ad albero di relazioni hello.</span><span class="sxs-lookup"><span data-stu-id="c2504-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="c2504-118">toosee ulteriori dettagli, ad esempio nome completo di hello della colonna hello, spostare il mouse di hello su e viene visualizzato un toohello simile popup seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="c2504-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog - Elemento popup della relazione](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="c2504-120">tooinclude relazioni tra gli asset che sono già stati registrati, registrare nuovamente tali risorse.</span><span class="sxs-lookup"><span data-stu-id="c2504-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2504-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2504-121">Next steps</span></span>
- [<span data-ttu-id="c2504-122">Come asset di dati toomanage</span><span class="sxs-lookup"><span data-stu-id="c2504-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
