---
title: 'Portale di Azure: Maschera dati dinamica del database SQL di Azure | Documentazione Microsoft'
description: Introduzione alla funzione Maschera dati dinamica del database SQL nel portale di Azure
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="a7fda-103">Introduzione alla funzione Maschera dati dinamica del database SQL nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7fda-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="a7fda-104">Questo argomento illustra come implementare la funzione [Maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md) con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fda-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="a7fda-105">È anche possibile implementare tale funzione tramite [cmdlet del database SQL di Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o l'[API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7fda-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="a7fda-106">Configurare il mascheramento dei dati dinamici per il database tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7fda-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="a7fda-107">Avviare il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7fda-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a7fda-108">Accedere al pannello di configurazione del database che include i dati sensibili a cui si desidera applicare la maschera.</span><span class="sxs-lookup"><span data-stu-id="a7fda-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="a7fda-109">Fare clic sul riquadro **Maschera dati dinamica**. Verrà aperto il pannello di configurazione **Maschera dati dinamica**.</span><span class="sxs-lookup"><span data-stu-id="a7fda-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="a7fda-110">In alternativa, è possibile scorrere verso il basso fino alla sezione **Operazioni** e fare clic su **Mascheramento dei dati dinamici**.</span><span class="sxs-lookup"><span data-stu-id="a7fda-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="a7fda-112">Nel pannello di configurazione **Maschera dati dinamica** potrebbero essere visualizzate alcune colonne del database che il motore di raccomandazioni ha contrassegnato per l'applicazione della maschera.</span><span class="sxs-lookup"><span data-stu-id="a7fda-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="a7fda-113">Per accettare i suggerimenti, è sufficiente fare clic su **Aggiungi maschera** per una o più colonne e verrà creata una maschera in base al tipo predefinito per questa colonna.</span><span class="sxs-lookup"><span data-stu-id="a7fda-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="a7fda-114">È possibile modificare la funzione maschera facendo clic sulla regola di maschera e modificando il formato maschera del campo su un formato diverso a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="a7fda-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="a7fda-115">Assicurarsi di salvare le impostazioni facendo clic su **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a7fda-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="a7fda-117">Per aggiungere una maschera a una colonna del database, nella parte superiore del pannello di configurazione **Maschera dati dinamica** fare clic su **Aggiungi maschera** per aprire il pannello di configurazione **Aggiungi regola di maschera**.</span><span class="sxs-lookup"><span data-stu-id="a7fda-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="a7fda-119">Selezionare lo **schema**, la **tabella** e la **colonna** per definire i campi designati a cui verrà applicata la maschera.</span><span class="sxs-lookup"><span data-stu-id="a7fda-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="a7fda-120">Scegliere un **Formato maschera del campo** dall'elenco di categorie maschera dei dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="a7fda-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="a7fda-122">Fare clic su **Salva** nel pannello delle regole di maschera dei dati per aggiornare il set di regole di maschera nei criteri della maschera dati dinamica.</span><span class="sxs-lookup"><span data-stu-id="a7fda-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="a7fda-123">Digitare gli utenti SQL o le identità AAD da escludere dalla maschera e che hanno accesso ai dati sensibili senza maschera.</span><span class="sxs-lookup"><span data-stu-id="a7fda-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="a7fda-124">Deve trattarsi di un elenco di utenti separati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="a7fda-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="a7fda-125">Si noti che gli utenti con privilegi di amministratore dispongono sempre dell'accesso ai dati originali senza maschera.</span><span class="sxs-lookup"><span data-stu-id="a7fda-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="a7fda-127">Per fare in modo che il livello dell'applicazione consenta la visualizzazione dei dati sensibili per gli utenti dell'applicazione con privilegi, aggiungere l'utente SQL o l'identità AAD usata dall'applicazione per eseguire query nel database.</span><span class="sxs-lookup"><span data-stu-id="a7fda-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="a7fda-128">È altamente consigliabile che l'elenco contenga un numero limitato di utenti con privilegi per ridurre al minimo l'esposizione dei dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="a7fda-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="a7fda-129">Fare clic su **Salva** nel pannello di configurazione della maschera dati per salvare il criterio di maschera nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="a7fda-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7fda-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7fda-130">Next steps</span></span>

* <span data-ttu-id="a7fda-131">Per una panoramica, vedere l'articolo su [Maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a7fda-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="a7fda-132">È anche possibile implementare tale funzione tramite [cmdlet del database SQL di Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o l'[API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7fda-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>