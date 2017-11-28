---
title: aaaInstall Visual Studio e SSDT per SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="2e2a0-103">Installare Visual Studio e SSDT per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2e2a0-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="2e2a0-104">applicazioni toodevelop per SQL Data Warehouse, è consigliabile utilizzare hello più recente di Visual Studio con la versione più recente hello di SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="2e2a0-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="2e2a0-105">È supportato anche Visual Studio 2013 Update 5 con SSDT per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="2e2a0-106">Utilizzo di Visual Studio con SSDT sarà toouse hello Esplora oggetti di SQL Server toovisually esplorare le tabelle, viste, stored procedure e molti altri oggetti in SQL Data Warehouse, nonché di eseguire query.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="2e2a0-107">SQL Data Warehouse non supporta ancora i progetti di database di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="2e2a0-108">Questa funzionalità verrà aggiunta in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="2e2a0-109">Passaggio 1: Installare Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e2a0-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="2e2a0-110">Seguire questi toodownload collegamenti e installare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="2e2a0-111">Se si dispone già di Visual Studio 2013 o versione successiva, è possibile ignorare tooStep 2, installare SSDT.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="2e2a0-112">[Scaricare Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="2e2a0-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="2e2a0-113">Seguire hello [installazione di Visual Studio] [ Installing Visual Studio] Guida su MSDN e scegliere le configurazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="2e2a0-114">Passaggio 2: Installare SSDT</span><span class="sxs-lookup"><span data-stu-id="2e2a0-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="2e2a0-115">tooinstall SSDT per Visual Studio è sufficiente selezionare un aggiornamento di SSDT da Visual Studio eseguendo la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="2e2a0-116">In Visual Studio fare clic su **Strumenti** / **Estensioni e aggiornamenti**</span><span class="sxs-lookup"><span data-stu-id="2e2a0-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="2e2a0-117"> / **Aggiornamenti**</span><span class="sxs-lookup"><span data-stu-id="2e2a0-117"> / **Updates**</span></span>
2. <span data-ttu-id="2e2a0-118">Selezionare **Aggiornamenti del prodotto**, quindi cercare **Aggiornamento di Microsoft SQL Server per strumenti di database**</span><span class="sxs-lookup"><span data-stu-id="2e2a0-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="2e2a0-119">Se non viene trovato un aggiornamento, è necessario installare la versione più recente hello.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="2e2a0-120">tooconfirm SSDT è installato, fare clic su **Guida** / **su Microsoft Visual Studio** e cercare di SQL Server Data Tools nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="2e2a0-121">versione più recente di Hello di SSDT è 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="2e2a0-122">Se hello opzione tooinstall non è disponibile da Visual Studio, in alternativa è possibile visitare lo hello [di Download di SSDT] [ SSDT Download] pagina toodownload e installare SSDT manualmente.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e2a0-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e2a0-123">Next steps</span></span>
<span data-ttu-id="2e2a0-124">Ora che si dispone di hello la versione più recente di SSDT, si è pronti troppo[connettersi] [ connect] tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2e2a0-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Scaricare Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
