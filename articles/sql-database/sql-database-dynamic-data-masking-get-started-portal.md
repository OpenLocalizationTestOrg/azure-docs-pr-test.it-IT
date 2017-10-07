---
title: 'Portale di Azure: Maschera dati dinamica del database SQL di Azure | Documentazione Microsoft'
description: "La modalità di avvio tooget con Database SQL la maschera dati dinamica in hello portale di Azure"
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
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="14022-103">Introduzione a Database SQL la maschera dati dinamica con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="14022-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="14022-104">In questo argomento illustra come tooimplement [la maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md) con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="14022-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="14022-105">È anche possibile implementare con maschera dati dinamica [cmdlet del Database di SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="14022-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="14022-106">Impostare la maschera dati dinamica per il database utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="14022-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="14022-107">Avvio hello portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="14022-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="14022-108">Passare il pannello impostazioni toohello del database hello che include i dati sensibili hello desiderato toomask.</span><span class="sxs-lookup"><span data-stu-id="14022-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="14022-109">Fare clic su hello **maschera dati dinamica** riquadro che consente di avviare hello **maschera dati dinamica** Pannello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="14022-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="14022-110">In alternativa, è possibile scorrere verso il basso toohello **operazioni** sezione e fare clic su **maschera dati dinamica**.</span><span class="sxs-lookup"><span data-stu-id="14022-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="14022-112">In hello **maschera dati dinamica** pannello configurazione potrebbe essere visualizzato alcune colonne di database tale motore indicazioni hello è contrassegnata per la maschera.</span><span class="sxs-lookup"><span data-stu-id="14022-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="14022-113">Ordinare tooaccept indicazioni hello, è sufficiente scegliere **Aggiungi maschera** per una o più colonne e una maschera verrà create in base al tipo di hello predefinito per questa colonna.</span><span class="sxs-lookup"><span data-stu-id="14022-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="14022-114">È possibile modificare hello funzione di maschera facendo clic sulla regola per la maschera hello e modifica hello maschera campo tooa diverso formato di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="14022-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="14022-115">Tooclick assicurarsi di essere **salvare** toosave le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="14022-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="14022-117">una maschera per qualsiasi colonna del database, nella parte superiore di hello di hello tooadd **maschera dati dinamica** configurazione fare clic su pannello **Aggiungi maschera** tooopen hello **Aggiungi regola di maschera** Pannello di configurazione</span><span class="sxs-lookup"><span data-stu-id="14022-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="14022-119">Seleziona hello **Schema**, **tabella** e **colonna** hello toodefine designato campo che verrà nascosta.</span><span class="sxs-lookup"><span data-stu-id="14022-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="14022-120">Scegliere un **formato maschera del campo** dall'elenco di hello della maschera di categorie di dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="14022-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="14022-122">Fare clic su **salvare** nel set di hello tooupdate pannello regole di maschera le regole di criteri di maschera dati dinamica hello di maschera dati hello.</span><span class="sxs-lookup"><span data-stu-id="14022-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="14022-123">Utenti SQL hello di tipo o identità di Azure ad che devono essere esclusi dalla maschera e ha accesso a dati riservati toohello non mascherato.</span><span class="sxs-lookup"><span data-stu-id="14022-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="14022-124">Deve trattarsi di un elenco di utenti separati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="14022-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="14022-125">Si noti che gli utenti con privilegi di amministratore dispongano sempre di dati senza maschera di accesso toohello originale.</span><span class="sxs-lookup"><span data-stu-id="14022-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Riquadro di spostamento](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="14022-127">toomake hello così di livello applicazione è possibile visualizzare i dati sensibili per gli utenti con privilegi di applicazione, aggiungere hello utente SQL o un'applicazione hello identità AAD utilizza database hello tooquery.</span><span class="sxs-lookup"><span data-stu-id="14022-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="14022-128">È consigliabile che questo elenco contiene un numero minimo di esposizione toominimize gli utenti con privilegi di dati sensibili hello.</span><span class="sxs-lookup"><span data-stu-id="14022-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="14022-129">Fare clic su **salvare** in Criteri di configurazione pannello toosave hello maschera nuove o aggiornate di maschera dati hello.</span><span class="sxs-lookup"><span data-stu-id="14022-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="14022-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14022-130">Next steps</span></span>

* <span data-ttu-id="14022-131">Per una panoramica, vedere l'articolo su [Maschera dati dinamica](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14022-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="14022-132">È anche possibile implementare con maschera dati dinamica [cmdlet del Database di SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="14022-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
