---
title: aaaConnect tooAzure Analysis Services con Excel | Documenti Microsoft
description: Informazioni su come tooconnect tooan Azure Analysis Services server utilizzando Excel.
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="263a1-103">Connettersi con Excel</span><span class="sxs-lookup"><span data-stu-id="263a1-103">Connect with Excel</span></span>

<span data-ttu-id="263a1-104">Dopo avere creato un server in Azure e distribuiti tooit un modello tabulare, è possibile tooconnect e iniziare l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="263a1-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="263a1-105">Connettersi in Excel</span><span class="sxs-lookup"><span data-stu-id="263a1-105">Connect in Excel</span></span>

<span data-ttu-id="263a1-106">Connessione server tooa in Excel è supportata tramite recupera dati in Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="263a1-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="263a1-107">Connessione tramite l'importazione guidata tabella hello in Power Pivot non è supportata.</span><span class="sxs-lookup"><span data-stu-id="263a1-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="263a1-108">**tooconnect in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="263a1-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="263a1-109">In Excel 2016, in hello **dati** della barra multifunzione, fare clic su **Carica dati esterni** > **da altre origini** > **da Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="263a1-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="263a1-110">Nella connessione guidata dati di hello in **nome Server**, immettere il nome di server hello compresi il protocollo e URI.</span><span class="sxs-lookup"><span data-stu-id="263a1-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="263a1-111">Quindi, nel **le credenziali di accesso**selezionare **hello utilizzare seguito nome utente e Password**e quindi digitare il nome di account utente aziendale hello, ad esempio nancy@adventureworks.come la password.</span><span class="sxs-lookup"><span data-stu-id="263a1-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Connettersi dall'accesso a Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="263a1-113">In **seleziona Database e tabella**, selezionare il database di hello e modello o una prospettiva e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="263a1-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Connettersi dal modello di selezione in Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="263a1-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="263a1-115">See also</span></span>
<span data-ttu-id="263a1-116">[Librerie client](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="263a1-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="263a1-117">Gestire il server</span><span class="sxs-lookup"><span data-stu-id="263a1-117">Manage your server</span></span>](analysis-services-manage.md)     


