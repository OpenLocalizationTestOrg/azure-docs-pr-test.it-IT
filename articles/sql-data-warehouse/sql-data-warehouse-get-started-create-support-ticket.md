---
title: aaaHow toocreate un ticket di supporto per SQL Data Warehouse | Documenti Microsoft
description: Come supporto toocreate ticket in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="d3479-103">Modalità di concessione ticket toocreate un supporto per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d3479-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="d3479-104">In caso di problemi con SQL Data Warehouse, creare un ticket di supporto per ottenere assistenza dal team tecnico.</span><span class="sxs-lookup"><span data-stu-id="d3479-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="d3479-105">A partire da 20/12/2016, controllo di integrità risorsa hello in hello portale di Azure non è preciso.</span><span class="sxs-lookup"><span data-stu-id="d3479-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="d3479-106">Stiamo lavorando attivamente toofix questo problema.</span><span class="sxs-lookup"><span data-stu-id="d3479-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="d3479-107">Creare un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="d3479-107">Create a support ticket</span></span>
1. <span data-ttu-id="d3479-108">Aprire hello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d3479-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d3479-109">Nella schermata iniziale di hello, fare clic su hello **Guida e supporto** riquadro.</span><span class="sxs-lookup"><span data-stu-id="d3479-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Guida e supporto tecnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="d3479-111">In hello della Guida e supporto, fare clic su **Crea richiesta di supporto**.</span><span class="sxs-lookup"><span data-stu-id="d3479-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nuova richiesta di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="d3479-113">Seleziona hello **richiesta è di tipo**.</span><span class="sxs-lookup"><span data-stu-id="d3479-113">Select hello **Request Type**.</span></span>
   
    ![tipo di richiesta](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="d3479-115">Per impostazione predefinita, ogni server SQL, ad esempio myserver.database.windows.net, ha una **Quota DTU** pari a 45.000.</span><span class="sxs-lookup"><span data-stu-id="d3479-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="d3479-116">Questa quota è semplicemente un limite di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d3479-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="d3479-117">È possibile aumentare la quota per la creazione di un ticket di supporto e selezionando *Quota* come tipo di richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="d3479-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="d3479-118">le DTU, è necessario moltiplicare toocalculate hello 7.5 da hello totale [DWU] [ DWU] necessari.</span><span class="sxs-lookup"><span data-stu-id="d3479-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="d3479-119">Ad esempio, si desidera toohost due DW6000s su un server SQL server, sarà necessario richiedere una quota DTU di 90.000.</span><span class="sxs-lookup"><span data-stu-id="d3479-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="d3479-120">È possibile visualizzare il consumo di DTU corrente dal pannello hello SQL server nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="d3479-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="d3479-121">Il database sia in pausa e riavviato conteggiati per la quota di DTU hello.</span><span class="sxs-lookup"><span data-stu-id="d3479-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="d3479-122">Seleziona hello **sottoscrizione** che gli host hello database con problema hello segnalato.</span><span class="sxs-lookup"><span data-stu-id="d3479-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Sottoscrizione](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="d3479-124">Selezionare **SQL Data Warehouse** come hello risorse.</span><span class="sxs-lookup"><span data-stu-id="d3479-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Risorsa](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="d3479-126">Selezionare il proprio [piano di supporto di Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="d3479-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="d3479-127">**fatturazione, quota e gestione delle sottoscrizioni** è disponibile per tutti i livelli.</span><span class="sxs-lookup"><span data-stu-id="d3479-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="d3479-128">Il supporto **in garanzia** viene fornito tramite il supporto tecnico [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier].</span><span class="sxs-lookup"><span data-stu-id="d3479-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="d3479-129">Problemi di riparazione sono i problemi riscontrati dai clienti durante l'utilizzo di Azure in cui è presente un ragionevole supporre che problema hello Microsoft ha causato.</span><span class="sxs-lookup"><span data-stu-id="d3479-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="d3479-130">**Sviluppatore esperto** e **servizi di consulenza** sono disponibili all'indirizzo hello [Professional Direct] [ Professional Direct] e [Premier] [ Premier] livelli di supporto.</span><span class="sxs-lookup"><span data-stu-id="d3479-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="d3479-131">Se si dispone di un Premier il piano di supporto, è possibile segnalare anche SQL Data Warehouse problemi su hello [portale online Microsoft Premier][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="d3479-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="d3479-132">Vedere [piani di supporto tecnico di Azure] [ Azure support plan] toolearn ulteriori informazioni sulle varie supporta i piani ambito, risposta volte, sui prezzi, hello e così via.  Per domande frequenti sul supporto di Azure, vedere [Domande frequenti sul supporto di Azure][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="d3479-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Piano di supporto](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="d3479-134">Seleziona hello **tipo di problema** e **categoria**.</span><span class="sxs-lookup"><span data-stu-id="d3479-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="d3479-135">In questo esempio, abbiamo scelto "Strumenti" come tipo di problema hello e "Strumenti Client" come categoria di hello.</span><span class="sxs-lookup"><span data-stu-id="d3479-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Categoria del tipo di problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="d3479-137">Descrivere il problema di hello e hello livello di impatto aziendale.</span><span class="sxs-lookup"><span data-stu-id="d3479-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Descrizione del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="d3479-139">Le **informazioni di contatto** per il ticket di supporto saranno precompilate.</span><span class="sxs-lookup"><span data-stu-id="d3479-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="d3479-140">Aggiornare le informazioni, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d3479-140">Update this if necessary.</span></span>
    
    ![Informazioni di contatto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="d3479-142">Fare clic su **crea** toosubmit hello richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="d3479-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="d3479-143">Monitorare un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="d3479-143">Monitor a support ticket</span></span>
<span data-ttu-id="d3479-144">Dopo che è stata inviata una richiesta di supporto hello, il team di supporto tecnico di Azure hello contatterà l'utente.</span><span class="sxs-lookup"><span data-stu-id="d3479-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="d3479-145">toocheck la stato della richiesta e i dettagli, fare clic su **Gestisci richieste di supporto** dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="d3479-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Controlla stato](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="d3479-147">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="d3479-147">Other Resources</span></span>
<span data-ttu-id="d3479-148">Inoltre, è possibile connettersi con hello community di SQL Data Warehouse sul [Overflow dello Stack] [ Stack Overflow] o hello [forum MSDN di Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="d3479-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

