---
title: servizio di gestione di dispositivi StorSimple aaaDeploy | Documenti Microsoft
description: Viene illustrato come toocreate e delete hello del servizio di gestione di dispositivi StorSimple nel portale di Azure hello e descrive come toomanage hello chiave di registrazione del servizio.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="1dce4-103">Distribuire il servizio di gestione di dispositivi StorSimple hello per Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="1dce4-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="1dce4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1dce4-104">Overview</span></span>

<span data-ttu-id="1dce4-105">servizio di gestione di dispositivi StorSimple Hello in esecuzione in Microsoft Azure e si connette dispositivi StorSimple toomultiple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="1dce4-106">Dopo aver creato il servizio di hello, è possibile utilizzare i dispositivi di hello toomanage da hello Microsoft Azure portale in esecuzione in un browser.</span><span class="sxs-lookup"><span data-stu-id="1dce4-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="1dce4-107">In questo modo toomonitor tutti i dispositivi che sono connesso toohello dispositivo StorSimple Manager hello del servizio da un'unica posizione centrale, riducendo così al minimo carico amministrativo.</span><span class="sxs-lookup"><span data-stu-id="1dce4-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="1dce4-108">Hello comuni attività correlati tooa servizio di gestione di dispositivi StorSimple sono:</span><span class="sxs-lookup"><span data-stu-id="1dce4-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="1dce4-109">Creare un servizio</span><span class="sxs-lookup"><span data-stu-id="1dce4-109">Create a service</span></span>
* <span data-ttu-id="1dce4-110">Eliminare un servizio</span><span class="sxs-lookup"><span data-stu-id="1dce4-110">Delete a service</span></span>
* <span data-ttu-id="1dce4-111">Ottenere una chiave di registrazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="1dce4-111">Get hello service registration key</span></span>
* <span data-ttu-id="1dce4-112">Rigenerare la chiave di registrazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="1dce4-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="1dce4-113">In questa esercitazione viene descritto come tooperform di hello attività precedenti.</span><span class="sxs-lookup"><span data-stu-id="1dce4-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="1dce4-114">informazioni di Hello contenute in questo articolo sono applicabile solo matrici virtuale tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="1dce4-115">Per ulteriori informazioni su StorSimple serie 8000, visitare troppo[distribuire un servizio StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="1dce4-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="1dce4-116">Creare un servizio</span><span class="sxs-lookup"><span data-stu-id="1dce4-116">Create a service</span></span>

<span data-ttu-id="1dce4-117">toocreate un servizio, è necessario toohave:</span><span class="sxs-lookup"><span data-stu-id="1dce4-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="1dce4-118">Una sottoscrizione con un contratto Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="1dce4-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="1dce4-119">Un account di archiviazione di Microsoft Azure attivo</span><span class="sxs-lookup"><span data-stu-id="1dce4-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="1dce4-120">le informazioni di fatturazione che viene utilizzate per la gestione accessi Hello</span><span class="sxs-lookup"><span data-stu-id="1dce4-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="1dce4-121">È inoltre possibile toogenerate un account di archiviazione quando si crea il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="1dce4-122">Un singolo servizio può gestire più dispositivi,</span><span class="sxs-lookup"><span data-stu-id="1dce4-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="1dce4-123">ma un dispositivo non può estendersi a più servizi.</span><span class="sxs-lookup"><span data-stu-id="1dce4-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="1dce4-124">Una grande organizzazione può avere più toowork di istanze di servizio con diverse sottoscrizioni, organizzazioni o anche percorsi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1dce4-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="1dce4-125">È necessario istanze separate di dispositivi della serie StorSimple 8000 toomanage servizio StorSimple Manager di dispositivi e le matrici virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="1dce4-126">Eseguire hello seguendo i passaggi toocreate un servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="1dce4-127">Eliminare un servizio</span><span class="sxs-lookup"><span data-stu-id="1dce4-127">Delete a service</span></span>

<span data-ttu-id="1dce4-128">Prima di eliminare un servizio, verificare che non sia usato da dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="1dce4-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="1dce4-129">Se il servizio di hello è in uso, disattivare i dispositivi connesso hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="1dce4-130">operazione di disattivazione Hello dividere hello connessione tra il dispositivo di hello e servizio hello, ma conservare i dati del dispositivo hello nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1dce4-131">Dopo l'eliminazione di un servizio, operazione hello non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="1dce4-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="1dce4-132">Qualsiasi dispositivo che utilizza il servizio hello sarà necessario toobe delle impostazioni di fabbrica prima che possa essere usato con un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="1dce4-133">In questo scenario, i dati locali di hello sul dispositivo hello, nonché la configurazione di hello, andranno persi.</span><span class="sxs-lookup"><span data-stu-id="1dce4-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="1dce4-134">Eseguire hello seguendo i passaggi toodelete un servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="1dce4-135">toodelete un servizio</span><span class="sxs-lookup"><span data-stu-id="1dce4-135">toodelete a service</span></span>

1. <span data-ttu-id="1dce4-136">Andare troppo**tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="1dce4-136">Go too**All resources**.</span></span> <span data-ttu-id="1dce4-137">Ricercare il servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="1dce4-138">Selezionare servizio hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="1dce4-138">Select hello service that you wish toodelete.</span></span>
   
    ![Selezionare servizio toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="1dce4-140">Passare tooyour servizio dashboard tooensure esistono dispositivi non connesso toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="1dce4-141">Se non sono presenti dispositivi registrati con questo servizio, verrà visualizzato anche un effetto di toohello messaggio banner.</span><span class="sxs-lookup"><span data-stu-id="1dce4-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="1dce4-142">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="1dce4-142">Click **Delete**.</span></span>
   
    ![Delete service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="1dce4-144">Quando viene richiesta la conferma, fare clic su **Sì** nella notifica di conferma hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Confermare l'eliminazione del servizio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="1dce4-146">Potrebbe richiedere alcuni minuti per hello servizio toobe eliminato.</span><span class="sxs-lookup"><span data-stu-id="1dce4-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="1dce4-147">Dopo aver hello servizio viene eliminato correttamente, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="1dce4-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Eliminazione del servizio riuscita](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="1dce4-149">elenco di Hello dei servizi verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="1dce4-149">hello list of services will be refreshed.</span></span>

 ![Elenco aggiornato dei servizi](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="1dce4-151">Ottenere una chiave di registrazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="1dce4-151">Get hello service registration key</span></span>
<span data-ttu-id="1dce4-152">Dopo avere creato un servizio, è necessario tooregister dispositivo StorSimple con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="1dce4-153">tooregister del primo dispositivo StorSimple, si sarà necessario hello chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="1dce4-154">tooregister ulteriori dispositivi con un servizio StorSimple esistente, è necessario sia la chiave di registrazione hello e hello chiave DEK del servizio (che viene generato nel primo dispositivo hello durante la registrazione).</span><span class="sxs-lookup"><span data-stu-id="1dce4-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="1dce4-155">Per ulteriori informazioni sulla chiave di crittografia di hello servizio dati, vedere [sicurezza in StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="1dce4-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="1dce4-156">È possibile ottenere la chiave di registrazione hello accedendo hello **chiavi** pannello per il servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="1dce4-157">Eseguire hello seguendo i passaggi tooget hello chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="1dce4-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="1dce4-158">chiave di registrazione del servizio hello tooget</span><span class="sxs-lookup"><span data-stu-id="1dce4-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="1dce4-159">In hello **Gestione dispositivi StorSimple** pannello andare troppo**Management &gt;**  **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="1dce4-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="1dce4-161">In hello **chiavi** viene visualizzata una chiave di registrazione del servizio di pannello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="1dce4-162">Chiave di registrazione hello copia utilizzando l'icona di copia hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="1dce4-163">Mantenere una chiave di registrazione del servizio hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="1dce4-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="1dce4-164">Sarà necessario questa chiave, nonché hello chiave DEK del servizio, tooregister ulteriori dispositivi con questo servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="1dce4-165">Dopo aver ottenuto una chiave di registrazione del servizio hello, sarà necessario tooconfigure il dispositivo tramite Windows PowerShell hello per l'interfaccia di StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="1dce4-166">Rigenerare la chiave di registrazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="1dce4-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="1dce4-167">Se si è obbligatorio tooperform rotazione delle chiavi o se l'elenco di hello degli amministratori del servizio è stato modificato, sarà necessario tooregenerate una chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="1dce4-168">Quando si rigenera la chiave hello, nuova chiave hello viene utilizzato solo per registrare i dispositivi successivi.</span><span class="sxs-lookup"><span data-stu-id="1dce4-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="1dce4-169">i dispositivi Hello già registrati sono interessati da questo processo.</span><span class="sxs-lookup"><span data-stu-id="1dce4-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="1dce4-170">Eseguire hello seguendo i passaggi tooregenerate una chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="1dce4-171">chiave di registrazione del servizio hello tooregenerate</span><span class="sxs-lookup"><span data-stu-id="1dce4-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="1dce4-172">In hello **Gestione dispositivi StorSimple** pannello andare troppo**Management &gt;**  **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="1dce4-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="1dce4-174">In hello **chiavi** pannello, fare clic su **rigenerare**.</span><span class="sxs-lookup"><span data-stu-id="1dce4-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Fare clic su Rigenera](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="1dce4-176">In hello **Rigenera chiave di registrazione** pannello revisione hello azione necessaria per la hello chiavi vengono rigenerate.</span><span class="sxs-lookup"><span data-stu-id="1dce4-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="1dce4-177">Tutti i dispositivi successivi hello che sono registrati con questo servizio utilizzerà una nuova chiave di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="1dce4-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="1dce4-178">Fare clic su **rigenerare** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1dce4-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="1dce4-179">Una volta completata la registrazione di hello si riceverà la notifica.</span><span class="sxs-lookup"><span data-stu-id="1dce4-179">You will be notified after hello registration is complete.</span></span>
   
   ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="1dce4-181">Verrà visualizzata una nuova chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-181">A new service registration key will appear.</span></span>
   
    ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="1dce4-183">Copiare la chiave e salvarla per registrare eventuali nuovi dispositivi con il servizio.</span><span class="sxs-lookup"><span data-stu-id="1dce4-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dce4-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1dce4-184">Next steps</span></span>
* <span data-ttu-id="1dce4-185">Informazioni su come troppo[iniziare](storsimple-virtual-array-deploy1-portal-prep.md) con un Array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1dce4-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="1dce4-186">Informazioni su come troppo[amministrare il dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1dce4-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

