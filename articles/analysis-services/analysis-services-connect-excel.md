---
title: Connettersi ad Azure Analysis Services con Excel | Microsoft Docs
description: Informazioni su come connettersi a un server di Azure Analysis Services usando Excel.
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
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="d757a-103">Connettersi con Excel</span><span class="sxs-lookup"><span data-stu-id="d757a-103">Connect with Excel</span></span>

<span data-ttu-id="d757a-104">Dopo aver creato un server in Azure e aver distribuito un modello tabulare nel server, è possibile connettersi e iniziare l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="d757a-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="d757a-105">Connettersi in Excel</span><span class="sxs-lookup"><span data-stu-id="d757a-105">Connect in Excel</span></span>

<span data-ttu-id="d757a-106">La connessione a un server in Excel è supportata tramite Dati in Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="d757a-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="d757a-107">La connessione tramite l'Importazione guidata tabella in Power Pivot non è supportata.</span><span class="sxs-lookup"><span data-stu-id="d757a-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="d757a-108">**Per connettersi in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="d757a-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="d757a-109">In Excel 2016, sulla barra multifunzione **Dati**, fare clic su **Recupera dati esterni** > **Da altre origini** > **Da Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="d757a-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="d757a-110">Nella Connessione guidata dati, in **Nome Server**, immettere il nome del server, inclusi il protocollo e l'URI.</span><span class="sxs-lookup"><span data-stu-id="d757a-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="d757a-111">In **Credenziali di accesso** selezionare **Usa nome utente e password seguenti** e quindi digitare il nome utente dell'organizzazione, ad esempio nancy@adventureworks.com, e la password.</span><span class="sxs-lookup"><span data-stu-id="d757a-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Connettersi dall'accesso a Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="d757a-113">In **Seleziona database e tabella** selezionare il database e il modello o la prospettiva e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="d757a-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Connettersi dal modello di selezione in Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="d757a-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d757a-115">See also</span></span>
<span data-ttu-id="d757a-116">[Librerie client](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="d757a-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="d757a-117">Gestire il server</span><span class="sxs-lookup"><span data-stu-id="d757a-117">Manage your server</span></span>](analysis-services-manage.md)     


