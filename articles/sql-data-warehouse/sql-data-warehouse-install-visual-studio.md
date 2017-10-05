---
title: Installare Visual Studio e SSDT per SQL Data Warehouse | Microsoft Docs
description: Installare Visual Studio e SQL Server Data Tools (SSDT) per Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="e12f5-103">Installare Visual Studio e SSDT per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e12f5-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="e12f5-104">Per sviluppare applicazioni per SQL Data Warehouse, è consigliabile usare la versione più recente di Visual Studio con la versione più recente di SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="e12f5-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="e12f5-105">È supportato anche Visual Studio 2013 Update 5 con SSDT per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e12f5-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="e12f5-106">L'uso di Visual Studio con SSDT consentirà di usare Esplora oggetti di SQL Server per esplorare visivamente tabelle, viste, stored procedure e molti altri oggetti in SQL Data Warehouse, nonché eseguire query.</span><span class="sxs-lookup"><span data-stu-id="e12f5-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="e12f5-107">SQL Data Warehouse non supporta ancora i progetti di database di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e12f5-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="e12f5-108">Questa funzionalità verrà aggiunta in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="e12f5-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="e12f5-109">Passaggio 1: Installare Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e12f5-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="e12f5-110">Seguire questi collegamenti per scaricare e installare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e12f5-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="e12f5-111">Se Visual Studio 2013 o versione successiva è già installato, è possibile procedere al passaggio 2 per installare SSDT.</span><span class="sxs-lookup"><span data-stu-id="e12f5-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="e12f5-112">[Scaricare Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="e12f5-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="e12f5-113">Seguire le istruzioni di [Installazione di Visual Studio][Installing Visual Studio] in MSDN e scegliere le configurazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e12f5-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="e12f5-114">Passaggio 2: Installare SSDT</span><span class="sxs-lookup"><span data-stu-id="e12f5-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="e12f5-115">Per installare SSDT per Visual Studio è sufficiente selezionare un aggiornamento di SSDT dall'interno di Visual Studio seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e12f5-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="e12f5-116">In Visual Studio fare clic su **Strumenti** / **Estensioni e aggiornamenti**</span><span class="sxs-lookup"><span data-stu-id="e12f5-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="e12f5-117"> / **Aggiornamenti**</span><span class="sxs-lookup"><span data-stu-id="e12f5-117"> / **Updates**</span></span>
2. <span data-ttu-id="e12f5-118">Selezionare **Aggiornamenti del prodotto**, quindi cercare **Aggiornamento di Microsoft SQL Server per strumenti di database**</span><span class="sxs-lookup"><span data-stu-id="e12f5-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="e12f5-119">Se non viene trovato un aggiornamento, significa che la versione più recente è già installata.</span><span class="sxs-lookup"><span data-stu-id="e12f5-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="e12f5-120">Per verificare che SSDT sia installato, fare clic su **Guida** / **Informazioni su Microsoft Visual Studio** e cercare SQL Server Data Tools nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="e12f5-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="e12f5-121">La versione più recente di SSDT è 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="e12f5-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="e12f5-122">Se l'opzione di installazione non è disponibile da Visual Studio, in alternativa è possibile visitare la pagina [Scaricare SQL Server Data Tools (SSDT)][SSDT Download] per scaricare e installare SSDT manualmente.</span><span class="sxs-lookup"><span data-stu-id="e12f5-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e12f5-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e12f5-123">Next steps</span></span>
<span data-ttu-id="e12f5-124">Dopo aver installato la versione più recente di SSDT, è possibile [connettersi][connect] a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e12f5-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="e12f5-125">[Scaricare Visual Studio]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="e12f5-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
