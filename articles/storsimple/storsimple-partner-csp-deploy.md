---
title: aaaMicrosoft StorSimple di Azure e panoramica del programma di Provider di soluzioni Cloud | Documenti Microsoft
description: Cenni preliminari sul hello StorSimple e CSP per i partner di StorSimple.
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
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="f69d0-103">Distribuire un array virtuale StorSimple per il Cloud Solution Provider Program</span><span class="sxs-lookup"><span data-stu-id="f69d0-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="f69d0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f69d0-104">Overview</span></span>

<span data-ttu-id="f69d0-105">Array virtuale StorSimple può essere distribuito da partner di hello Provider di soluzioni Cloud (CSP) per i loro clienti.</span><span class="sxs-lookup"><span data-stu-id="f69d0-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="f69d0-106">Un partner CSP può creare un Servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f69d0-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="f69d0-107">Questo servizio può essere utilizzati toodeploy e gestire StorSimple Virtual Array e hello associata condivisioni, volumi e i backup.</span><span class="sxs-lookup"><span data-stu-id="f69d0-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="f69d0-108">In questo articolo viene descritto come partner CSP può aggiungere un cliente o un nuovo cliente esistente tooan di sottoscrizione e quindi creare una matrice virtuale StorSimple toodeploy un servizio nel CSP.</span><span class="sxs-lookup"><span data-stu-id="f69d0-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f69d0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f69d0-109">Prerequisites</span></span>

<span data-ttu-id="f69d0-110">Prima di iniziare, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="f69d0-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="f69d0-111">Sono registrati in programma CSP hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="f69d0-112">Disporre di credenziali di accesso valide per il [Centro per i partner](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f69d0-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="f69d0-113">credenziali Hello consentono toosign nuovi clienti toohello Partner tooadd portale, cercare i clienti o passare il conto cliente tooa dal dashboard Partner hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="f69d0-114">Hello CSP può fungere da un amministratore di StorSimple per conto cliente hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f69d0-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="f69d0-115">Aggiungere un cliente</span><span class="sxs-lookup"><span data-stu-id="f69d0-115">Add a customer</span></span>

<span data-ttu-id="f69d0-116">Se si aggiunge un cliente, viene automaticamente creata una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f69d0-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="f69d0-117">tooadd un cliente e creare automaticamente una sottoscrizione, eseguire operazioni nel portale di Partner hello hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="f69d0-118">Passare toohello [Partner Center](http://partnercenter.microsoft.com/) e accedere utilizzando le credenziali CSP.</span><span class="sxs-lookup"><span data-stu-id="f69d0-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="f69d0-119">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-119">Click **Dashboard**.</span></span>

     ![Dashboard nel Centro per i partner](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="f69d0-121">Nel riquadro a sinistra di hello, fare clic su **clienti**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="f69d0-122">Nel riquadro a destra hello, fare clic su **aggiungere clienti**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="f69d0-123">Immettere i dettagli di hello del cliente hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="f69d0-124">Fare clic su **Avanti: sottoscrizioni** toocreate una sottoscrizione del cliente.</span><span class="sxs-lookup"><span data-stu-id="f69d0-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Aggiungere un cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="f69d0-126">Selezionare l'offerta **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="f69d0-127">Scorri toohello alla fine della pagina di hello e fare clic su **revisione**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Verificare le informazioni sulla sottoscrizione](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="f69d0-129">Esaminare le informazioni di hello e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-129">Review hello information and click **Submit**.</span></span>

    ![Inviare la sottoscrizione](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="f69d0-131">Salvare le informazioni di conferma hello per riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="f69d0-131">Save hello confirmation information for future reference.</span></span>

    ![Salvare la conferma](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="f69d0-133">Individuare o passare toohello cliente che appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="f69d0-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="f69d0-134">Fare clic su hello **nome società** toodrill verso il basso in dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Ricerca per il cliente hello](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="f69d0-136">Nel riquadro a sinistra di hello, selezionare **gestione dei servizi**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="f69d0-137">In hello riquadro a destra in **amministrare servizi**, fare clic su **Microsoft Azure Management Portal** toosign in come amministratore di Azure per il cliente.</span><span class="sxs-lookup"><span data-stu-id="f69d0-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Accedi al portale tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="f69d0-139">Fare clic su un dispositivo di StorSimple Manager, toocreate **+ nuovo** e individuare o passare troppo**serie di dispositivi virtuali StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="f69d0-140">Per ulteriori informazioni, visitare troppo[distribuire un servizio di gestione di dispositivi StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="f69d0-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Creare un servizio Gestione dispositivi StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="f69d0-142">Aggiungere una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f69d0-142">Add a subscription</span></span>

<span data-ttu-id="f69d0-143">In alcuni casi, potrebbe essere un cliente esistente, e necessario tooadd una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f69d0-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="f69d0-144">tooadd un cliente esistente tooan di sottoscrizione, eseguire operazioni nel portale di Partner hello hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="f69d0-145">Passare toohello [Partner Center](http://partnercenter.microsoft.com/) e accedere utilizzando le credenziali CSP.</span><span class="sxs-lookup"><span data-stu-id="f69d0-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="f69d0-146">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-146">Click **Dashboard**.</span></span>

     ![Dashboard nel Centro per i partner](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="f69d0-148">Nel riquadro a sinistra di hello, fare clic su **clienti**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="f69d0-149">Individuare o passare cliente toohello che tooadd si desidera una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f69d0-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="f69d0-150">Fare clic su hello ![sull'icona di controllo di espansione](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) riga hello tooexpand di icona per il nome della società hello per il cliente.</span><span class="sxs-lookup"><span data-stu-id="f69d0-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="f69d0-151">Nei dettagli hello, fare clic su **aggiungere sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-151">In hello details, click **Add subscriptions**.</span></span>

    ![Clienti](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="f69d0-153">Controllare **Microsoft Azure** per hello **principali offerte** nella sottoscrizione di hello e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="f69d0-154">Verrà creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f69d0-154">This creates a new subscription.</span></span>

    ![Aggiungere una nuova sottoscrizione](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="f69d0-156">Dopo aver creata una nuova sottoscrizione, fare clic su **<-clienti** in hello riquadro sinistro tooreturn toohello **clienti** pagina.</span><span class="sxs-lookup"><span data-stu-id="f69d0-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="f69d0-157">Ricerca per il cliente hello per il quale una sottoscrizione è stato appena creato.</span><span class="sxs-lookup"><span data-stu-id="f69d0-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="f69d0-158">Fare clic su hello **nome società** toodrill verso il basso in dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="f69d0-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Ricerca per il cliente hello](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="f69d0-160">Nel riquadro a sinistra di hello, selezionare **gestione dei servizi**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="f69d0-161">In hello riquadro a destra in **amministrare servizi**, fare clic su **Microsoft Azure Management Portal** toosign in come amministratore di Azure per il cliente.</span><span class="sxs-lookup"><span data-stu-id="f69d0-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Accedi al portale tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="f69d0-163">Fare clic su un dispositivo di StorSimple Manager, toocreate **+ nuovo** e individuare o passare troppo**serie di dispositivi virtuali StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="f69d0-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="f69d0-164">Per ulteriori informazioni, visitare troppo[distribuire un servizio di gestione di dispositivi StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="f69d0-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Creare un servizio Gestione dispositivi StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="f69d0-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f69d0-166">Next steps</span></span>

- <span data-ttu-id="f69d0-167">Se si dispone di ulteriori domande riguardanti hello StorSimple in CSP, andare troppo[StorSimple nel CSP: domande frequenti](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f69d0-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="f69d0-168">Se si è pronti toodeploy StorSimple, andare troppo[distribuire StorSimple nel CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f69d0-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
