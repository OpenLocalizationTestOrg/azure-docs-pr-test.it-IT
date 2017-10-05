---
title: Come visualizzare gli asset di dati correlati in Azure Data Catalog | Microsoft Docs
description: In questo articolo viene illustrato come visualizzare gli asset di dati correlati di un asset di dati selezionato in Azure Data Catalog.
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
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="34415-103">Come visualizzare gli asset di dati correlati in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="34415-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="34415-104">Azure Data Catalog consente di visualizzare gli asset di dati correlati in un asset di dati selezionato e di visualizzare le relazioni esistenti tra di essi.</span><span class="sxs-lookup"><span data-stu-id="34415-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="34415-105">Origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="34415-105">Supported data sources</span></span> 
<span data-ttu-id="34415-106">Quando si registrano gli asset di dati dalle origini dati seguenti, Azure Data Catalog registra automaticamente i metadati relativi alle relazioni di join tra gli asset di dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="34415-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="34415-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="34415-107">SQL Server</span></span>
- <span data-ttu-id="34415-108">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="34415-108">Azure SQL Database</span></span>
- <span data-ttu-id="34415-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="34415-109">MySQL</span></span>
- <span data-ttu-id="34415-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="34415-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="34415-111">Visualizzare gli asset di dati correlati</span><span class="sxs-lookup"><span data-stu-id="34415-111">View related data assets</span></span>
<span data-ttu-id="34415-112">Per visualizzare gli asset di dati che sono correlati a un set di dati selezionato, usare la scheda **Relazioni** come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="34415-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog - Visualizzare gli asset di dati correlati](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="34415-114">In questo esempio sono presenti due relazioni per l'asset di dati **ProductSubcategory** selezionato:</span><span class="sxs-lookup"><span data-stu-id="34415-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="34415-115">La colonna ProductSubcategoryID della tabella Prodotto dispone di una relazione di chiave esterna con la colonna ProductSubcategoryID della tabella ProductSubcategory selezionata.</span><span class="sxs-lookup"><span data-stu-id="34415-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="34415-116">La colonna ProductCategoryID della tabella ProductSubCategory dispone di una relazione di chiave esterna con la colonna ProductCategoryID della tabella ProductCategory selezionata.</span><span class="sxs-lookup"><span data-stu-id="34415-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="34415-117">Si noti la direzione della freccia nella visualizzazione struttura ad albero delle relazioni.</span><span class="sxs-lookup"><span data-stu-id="34415-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="34415-118">Per visualizzare altri dettagli, ad esempio il nome completo della colonna, spostare il puntatore del mouse verso l'alto per mostrare un elemento popup simile a quello dell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="34415-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog - Elemento popup della relazione](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="34415-120">Per includere le relazioni tra gli asset già registrati, è necessario registrare nuovamente gli asset.</span><span class="sxs-lookup"><span data-stu-id="34415-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34415-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34415-121">Next steps</span></span>
- [<span data-ttu-id="34415-122">Come gestire gli asset di dati</span><span class="sxs-lookup"><span data-stu-id="34415-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)