---
title: Panoramica di Microsoft Azure StorSimple e del Cloud Solutions Provider Program | Microsoft Docs
description: Panoramica di StorSimple e del programma CSP per i partner StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="deada-103">Distribuire un array virtuale StorSimple per il Cloud Solution Provider Program</span><span class="sxs-lookup"><span data-stu-id="deada-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="deada-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="deada-104">Overview</span></span>

<span data-ttu-id="deada-105">I partner Cloud Solution Provider (CSP) possono distribuire un array virtuale StorSimple per i propri clienti.</span><span class="sxs-lookup"><span data-stu-id="deada-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="deada-106">Un partner CSP può creare un Servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="deada-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="deada-107">Questo servizio può quindi essere usato per distribuire e gestire l'array virtuale StorSimple e relativi volumi, backup e condivisioni.</span><span class="sxs-lookup"><span data-stu-id="deada-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="deada-108">In questo articolo viene descritto come un partner CSP può aggiungere un cliente o una nuova sottoscrizione a un cliente esistente e quindi creare un servizio per distribuire un array virtuale StorSimple in CSP.</span><span class="sxs-lookup"><span data-stu-id="deada-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deada-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="deada-109">Prerequisites</span></span>

<span data-ttu-id="deada-110">Prima di iniziare, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="deada-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="deada-111">Essere iscritti al programma CSP.</span><span class="sxs-lookup"><span data-stu-id="deada-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="deada-112">Disporre di credenziali di accesso valide per il [Centro per i partner](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="deada-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="deada-113">Le credenziali consentono di accedere al portale per i partner per aggiungere nuovi clienti, cercare i clienti o passare a un account cliente dal dashboard dei partner.</span><span class="sxs-lookup"><span data-stu-id="deada-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="deada-114">Il CSP può fungere da amministratore di StorSimple per conto del cliente nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="deada-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="deada-115">Aggiungere un cliente</span><span class="sxs-lookup"><span data-stu-id="deada-115">Add a customer</span></span>

<span data-ttu-id="deada-116">Se si aggiunge un cliente, viene automaticamente creata una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="deada-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="deada-117">Per aggiungere un cliente e creare automaticamente una sottoscrizione, eseguire i passaggi seguenti nel portale per i partner.</span><span class="sxs-lookup"><span data-stu-id="deada-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="deada-118">Andare al [Centro per i partner](http://partnercenter.microsoft.com/) e accedere usando le credenziali di CSP.</span><span class="sxs-lookup"><span data-stu-id="deada-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="deada-119">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="deada-119">Click **Dashboard**.</span></span>

     ![Dashboard nel Centro per i partner](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="deada-121">Nel riquadro a sinistra, fare clic su **Clienti**.</span><span class="sxs-lookup"><span data-stu-id="deada-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="deada-122">Nel riquadro a destra, fare clic su **Aggiungi clienti**.</span><span class="sxs-lookup"><span data-stu-id="deada-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="deada-123">Immettere i dettagli del cliente.</span><span class="sxs-lookup"><span data-stu-id="deada-123">Enter the details of the customer.</span></span> <span data-ttu-id="deada-124">Fare clic su **Successivo: Sottoscrizioni** per creare una sottoscrizione del cliente.</span><span class="sxs-lookup"><span data-stu-id="deada-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Aggiungere un cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="deada-126">Selezionare l'offerta **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="deada-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="deada-127">Scorrere fino alla parte inferiore della pagina e fare clic su **Verifica**.</span><span class="sxs-lookup"><span data-stu-id="deada-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Verificare le informazioni sulla sottoscrizione](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="deada-129">Verificare le informazioni e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="deada-129">Review the information and click **Submit**.</span></span>

    ![Inviare la sottoscrizione](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="deada-131">Salvare le informazioni di conferma per riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="deada-131">Save the confirmation information for future reference.</span></span>

    ![Salvare la conferma](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="deada-133">Individuare o passare al cliente appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="deada-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="deada-134">Fare clic su **Nome società** per visualizzare tutti i dettagli.</span><span class="sxs-lookup"><span data-stu-id="deada-134">Click the **Company name** to drill down into the details.</span></span>

    ![Cercare il cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="deada-136">Nel riquadro a sinistra, selezionare **Gestione servizi**.</span><span class="sxs-lookup"><span data-stu-id="deada-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="deada-137">Nel riquadro di destra, in **Amministra servizi**, fare clic su **Portale di gestione di Microsoft Azure** per accedere come amministratore di Azure per il cliente.</span><span class="sxs-lookup"><span data-stu-id="deada-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Accedere al portale di Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="deada-139">Per creare una Gestione dispositivi StorSimple, fare clic su **+Nuovo** e cercare o passare a **Serie di dispositivi virtuali StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="deada-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="deada-140">Per altre informazioni, vedere [Distribuire un servizio di Gestione dispositivi StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="deada-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Creare un servizio Gestione dispositivi StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="deada-142">Aggiungere una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="deada-142">Add a subscription</span></span>

<span data-ttu-id="deada-143">In alcuni casi, si potrebbe disporre di un cliente esistente e potrebbe essere necessario aggiungere una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="deada-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="deada-144">Per aggiungere una sottoscrizione a un cliente esistente, eseguire i passaggi seguenti nel portale per i partner.</span><span class="sxs-lookup"><span data-stu-id="deada-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="deada-145">Andare al [Centro per i partner](http://partnercenter.microsoft.com/) e accedere usando le credenziali di CSP.</span><span class="sxs-lookup"><span data-stu-id="deada-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="deada-146">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="deada-146">Click **Dashboard**.</span></span>

     ![Dashboard nel Centro per i partner](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="deada-148">Nel riquadro a sinistra, fare clic su **Clienti**.</span><span class="sxs-lookup"><span data-stu-id="deada-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="deada-149">Trovare o passare al cliente a cui si vuole aggiungere una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="deada-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="deada-150">Fare clic sull'![icona del segno di spunta Espandi](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) per espandere la riga relativa al nome della società del cliente.</span><span class="sxs-lookup"><span data-stu-id="deada-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="deada-151">Nei dettagli, fare clic su **Aggiungi sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="deada-151">In the details, click **Add subscriptions**.</span></span>

    ![Clienti](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="deada-153">Controllare **Microsoft Azure** per le **Migliori offerte** nella sottoscrizione e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="deada-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="deada-154">Verrà creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="deada-154">This creates a new subscription.</span></span>

    ![Aggiungere una nuova sottoscrizione](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="deada-156">Dopo aver creata una nuova sottoscrizione, fare clic su **<-- Clienti** nel riquadro a sinistra per tornare alla pagina **Clienti**.</span><span class="sxs-lookup"><span data-stu-id="deada-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="deada-157">Cercare il cliente per il quale è stato appena creata una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="deada-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="deada-158">Fare clic su **Nome società** per visualizzare tutti i dettagli.</span><span class="sxs-lookup"><span data-stu-id="deada-158">Click the **Company name** to drill down into the details.</span></span>

    ![Cercare il cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="deada-160">Nel riquadro a sinistra, selezionare **Gestione servizi**.</span><span class="sxs-lookup"><span data-stu-id="deada-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="deada-161">Nel riquadro di destra, in **Amministra servizi**, fare clic su **Portale di gestione di Microsoft Azure** per accedere come amministratore di Azure per il cliente.</span><span class="sxs-lookup"><span data-stu-id="deada-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Accedere al portale di Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="deada-163">Per creare una Gestione dispositivi StorSimple, fare clic su **+Nuovo** e cercare o passare a **Serie di dispositivi virtuali StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="deada-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="deada-164">Per altre informazioni, vedere [Distribuire un servizio di Gestione dispositivi StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="deada-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Creare un servizio Gestione dispositivi StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="deada-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="deada-166">Next steps</span></span>

- <span data-ttu-id="deada-167">Per altre domande su StorSimple per CSP, passare a [StorSimple per CSP: domande frequenti](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="deada-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="deada-168">Se si è pronti a distribuire StorSimple, andare a [Distribuire StorSimple per CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="deada-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
