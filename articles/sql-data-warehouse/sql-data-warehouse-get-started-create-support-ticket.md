---
title: Come creare un ticket di supporto per SQL Data Warehouse | Documentazione Microsoft
description: Come creare un ticket di supporto per SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="76691-103">Come creare un ticket di supporto per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="76691-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="76691-104">In caso di problemi con SQL Data Warehouse, creare un ticket di supporto per ottenere assistenza dal team tecnico.</span><span class="sxs-lookup"><span data-stu-id="76691-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="76691-105">In data 20/12/2016, il controllo dell'integrità delle risorse nel portale di Azure non è accurato.</span><span class="sxs-lookup"><span data-stu-id="76691-105">As of 12/20/2016, the resource health check in the Azure portal is not accurate.</span></span> <span data-ttu-id="76691-106">Microsoft sta lavorando attivamente per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="76691-106">We are actively working to fix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="76691-107">Creare un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="76691-107">Create a support ticket</span></span>
1. <span data-ttu-id="76691-108">Aprire il [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="76691-108">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="76691-109">Nella schermata iniziale fare clic sul riquadro **Guida e supporto tecnico** .</span><span class="sxs-lookup"><span data-stu-id="76691-109">On the Home screen, click the **Help + support** tile.</span></span>
   
    ![Guida e supporto tecnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="76691-111">Nel pannello Guida e supporto tecnico fare clic su **Crea un ticket di supporto**.</span><span class="sxs-lookup"><span data-stu-id="76691-111">On the Help + Support blade, click **Create support request**.</span></span>
   
    ![Nuova richiesta di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="76691-113">Selezionare il **tipo di richiesta**.</span><span class="sxs-lookup"><span data-stu-id="76691-113">Select the **Request Type**.</span></span>
   
    ![tipo di richiesta](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="76691-115">Per impostazione predefinita, ogni server SQL, ad esempio myserver.database.windows.net, ha una **Quota DTU** pari a 45.000.</span><span class="sxs-lookup"><span data-stu-id="76691-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="76691-116">Questa quota è semplicemente un limite di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="76691-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="76691-117">È possibile aumentare la quota creando un ticket di supporto e selezionando *Quota* come tipo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="76691-117">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="76691-118">Per calcolare le esigenze in termini di DTU, moltiplicare le [DWU][DWU] totali necessarie per 7,5.</span><span class="sxs-lookup"><span data-stu-id="76691-118">To calculate your DTU needs, multiply the 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="76691-119">Se, ad esempio, si vogliono ospitare due DW6000 in una istanza di SQL Server, è necessario richiedere una quota di DTU pari a 90.000.</span><span class="sxs-lookup"><span data-stu-id="76691-119">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="76691-120">È possibile visualizzare l'utilizzo di DTU attuale nel pannello SQL Server del portale.</span><span class="sxs-lookup"><span data-stu-id="76691-120">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="76691-121">I database in pausa e non in pausa vengono conteggiati nella quota di DTU.</span><span class="sxs-lookup"><span data-stu-id="76691-121">Both paused and un-paused databases count toward the DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="76691-122">Selezionare la **sottoscrizione** che ospita il database con il problema segnalato.</span><span class="sxs-lookup"><span data-stu-id="76691-122">Select the **Subscription** that hosts the database with the problem you are reporting.</span></span>
   
    ![sottoscrizione](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="76691-124">Selezionare **SQL Data Warehouse** come risorsa.</span><span class="sxs-lookup"><span data-stu-id="76691-124">Select **SQL Data Warehouse** as the Resource.</span></span>
   
    ![Risorsa](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="76691-126">Selezionare il proprio [piano di supporto di Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="76691-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="76691-127">**fatturazione, quota e gestione delle sottoscrizioni** è disponibile per tutti i livelli.</span><span class="sxs-lookup"><span data-stu-id="76691-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="76691-128">Il supporto **in garanzia** viene fornito tramite il supporto tecnico [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="76691-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="76691-129">I problemi in garanzia si verificano quando i clienti usano Azure ed è ragionevolmente probabile che il problema sia provocato da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76691-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="76691-130">Servizi di **consulenza** e **mentoring per sviluppatori** sono disponibili solo per i livelli di supporto tecnico [Professional Direct][Professional Direct] e [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="76691-130">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="76691-131">Se si ha un piano di supporto tecnico Premier, è anche possibile segnalare problemi relativi a SQL Data Warehouse nel [portale Microsoft Premier online][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="76691-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="76691-132">Per altre informazioni sui vari piani di supporto, ad esempio su ambito, tempi di risposta, prezzi e così via, vedere la pagina relativa ai [piani di supporto di Azure][Azure support plan].  Per domande frequenti sul supporto di Azure, vedere [Domande frequenti sul supporto di Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="76691-132">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Piano di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="76691-134">Selezionare **Tipo di problema** e **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="76691-134">Select the **Problem Type** and **Category**.</span></span> <span data-ttu-id="76691-135">In questo esempio è stato scelto "Strumenti" come tipo di problema e "Strumenti client" come categoria.</span><span class="sxs-lookup"><span data-stu-id="76691-135">In this example, we have chosen "Tools" as the Problem type and "Client tools" as the category.</span></span> 
   
    ![Categoria del tipo di problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="76691-137">Descrivere il problema e scegliere il livello di impatto aziendale.</span><span class="sxs-lookup"><span data-stu-id="76691-137">Describe the problem and choose the level of business impact.</span></span>
   
    ![Descrizione del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="76691-139">Le **informazioni di contatto** per il ticket di supporto saranno precompilate.</span><span class="sxs-lookup"><span data-stu-id="76691-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="76691-140">Aggiornare le informazioni, se necessario.</span><span class="sxs-lookup"><span data-stu-id="76691-140">Update this if necessary.</span></span>
    
    ![Informazioni di contatto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="76691-142">Fare clic su **Crea** per inviare la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="76691-142">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="76691-143">Monitorare un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="76691-143">Monitor a support ticket</span></span>
<span data-ttu-id="76691-144">Dopo avere inviato la richiesta di supporto, si verrà contattati dal team di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="76691-144">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="76691-145">Per controllare i dettagli e lo stato della richiesta, fare clic su **Gestisci richieste di supporto** nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="76691-145">To check your request status and details, click **Manage support requests** on the dashboard.</span></span>

![Controlla stato](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="76691-147">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="76691-147">Other Resources</span></span>
<span data-ttu-id="76691-148">È anche possibile connettersi alla community di SQL Data Warehouse in [Stack Overflow][Stack Overflow] o nel [forum MSDN su Azure SQL Data Warehouse][Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="76691-148">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

