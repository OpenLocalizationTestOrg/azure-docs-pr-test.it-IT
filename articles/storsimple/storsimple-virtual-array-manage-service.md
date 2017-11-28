---
title: Distribuire il servizio Gestione dispositivi StorSimple | Documentazione Microsoft
description: Descrive le procedure per creare ed eliminare il servizio Gestione dispositivi StorSimple nel portale di Azure e per gestire la chiave di registrazione del servizio.
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="7d289-103">Distribuire il servizio Gestione dispositivi StorSimple per l'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d289-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="7d289-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7d289-104">Overview</span></span>

<span data-ttu-id="7d289-105">Il servizio Gestione dispositivi StorSimple viene eseguito in Microsoft Azure e si connette a più dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="7d289-106">Dopo aver creato il servizio, è possibile usarlo per gestire i dispositivi tramite il portale di Microsoft Azure in esecuzione in un browser.</span><span class="sxs-lookup"><span data-stu-id="7d289-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="7d289-107">Ciò consente di monitorare tutti i dispositivi connessi al servizio Gestione dispositivi StorSimple da un'unica posizione centrale, con una conseguente riduzione del carico amministrativo.</span><span class="sxs-lookup"><span data-stu-id="7d289-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="7d289-108">Le attività comuni correlate a un servizio Gestione dispositivi StorSimple sono:</span><span class="sxs-lookup"><span data-stu-id="7d289-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="7d289-109">Creare un servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-109">Create a service</span></span>
* <span data-ttu-id="7d289-110">Eliminare un servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-110">Delete a service</span></span>
* <span data-ttu-id="7d289-111">Ottenere la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-111">Get the service registration key</span></span>
* <span data-ttu-id="7d289-112">Rigenerare la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-112">Regenerate the service registration key</span></span>

<span data-ttu-id="7d289-113">Questa esercitazione descrive come eseguire ognuna delle attività precedenti.</span><span class="sxs-lookup"><span data-stu-id="7d289-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="7d289-114">Le informazioni contenute in questo articolo si applicano solo all'array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="7d289-115">Per altre informazioni su StorSimple serie 8000, andare a [Distribuire il servizio StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="7d289-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="7d289-116">Creare un servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-116">Create a service</span></span>

<span data-ttu-id="7d289-117">Per creare un servizio, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="7d289-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="7d289-118">Una sottoscrizione con un contratto Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="7d289-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="7d289-119">Un account di archiviazione di Microsoft Azure attivo</span><span class="sxs-lookup"><span data-stu-id="7d289-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="7d289-120">Le informazioni di fatturazione usate per la gestione degli accessi</span><span class="sxs-lookup"><span data-stu-id="7d289-120">The billing information that is used for access management</span></span>

<span data-ttu-id="7d289-121">È inoltre possibile scegliere di generare un account di archiviazione al momento della creazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="7d289-122">Un singolo servizio può gestire più dispositivi,</span><span class="sxs-lookup"><span data-stu-id="7d289-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="7d289-123">ma un dispositivo non può estendersi a più servizi.</span><span class="sxs-lookup"><span data-stu-id="7d289-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="7d289-124">Una grande impresa può avere più istanze del servizio per lavorare con diverse sottoscrizioni, organizzazioni o anche percorsi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7d289-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="7d289-125">Per gestire dispositivi StorSimple serie 8000 e array virtuali StorSimple sono necessarie istanze separate del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="7d289-126">Per creare un servizio, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="7d289-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="7d289-127">Eliminare un servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-127">Delete a service</span></span>

<span data-ttu-id="7d289-128">Prima di eliminare un servizio, verificare che non sia usato da dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="7d289-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="7d289-129">Se il servizio è in uso, disattivare i dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="7d289-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="7d289-130">L'operazione di disattivazione interromperà la connessione tra il dispositivo e il servizio mantenendo i dati del dispositivo nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7d289-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d289-131">Dopo che un servizio è stato eliminato, l'operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="7d289-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="7d289-132">Sarà necessario ripristinare le impostazioni predefinite di ogni dispositivo che usa questo servizio prima che il dispositivo possa essere usato con un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="7d289-133">In questo scenario i dati locali sul dispositivo e la configurazione andranno persi.</span><span class="sxs-lookup"><span data-stu-id="7d289-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="7d289-134">Per eliminare un servizio, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="7d289-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="7d289-135">Per eliminare un servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-135">To delete a service</span></span>

1. <span data-ttu-id="7d289-136">Passare a **Tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="7d289-136">Go to **All resources**.</span></span> <span data-ttu-id="7d289-137">Ricercare il servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="7d289-138">Selezionare il servizio da eliminare.</span><span class="sxs-lookup"><span data-stu-id="7d289-138">Select the service that you wish to delete.</span></span>
   
    ![Selezionare il servizio da eliminare](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="7d289-140">Passare al dashboard del servizio per verificare che non siano presenti dispositivi connessi al servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="7d289-141">Se non sono presenti dispositivi registrati con questo servizio, verrà visualizzato un messaggio di intestazione in proposito.</span><span class="sxs-lookup"><span data-stu-id="7d289-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="7d289-142">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="7d289-142">Click **Delete**.</span></span>
   
    ![Delete service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="7d289-144">Quando viene richiesta la conferma, fare clic su **Sì** nella notifica di conferma.</span><span class="sxs-lookup"><span data-stu-id="7d289-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Confermare l'eliminazione del servizio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="7d289-146">L'eliminazione del servizio può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="7d289-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="7d289-147">Dopo aver eliminato correttamente il servizio, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="7d289-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Eliminazione del servizio riuscita](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="7d289-149">L'elenco dei servizi verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7d289-149">The list of services will be refreshed.</span></span>

 ![Elenco aggiornato dei servizi](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="7d289-151">Ottenere la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-151">Get the service registration key</span></span>
<span data-ttu-id="7d289-152">Dopo aver creato un servizio, è necessario registrare il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="7d289-153">Per registrare il primo dispositivo StorSimple, è necessaria la chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="7d289-154">Per registrare altri dispositivi con un servizio StorSimple esistente, sono necessarie la chiave di registrazione e la chiave DEK del servizio (che viene generata durante la registrazione sul primo dispositivo).</span><span class="sxs-lookup"><span data-stu-id="7d289-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="7d289-155">Per altre informazioni sulla chiave DEK del servizio, vedere [Sicurezza in StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="7d289-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="7d289-156">È possibile ottenere la chiave di registrazione mediante il pannello **Chiavi** per il servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="7d289-157">Per ottenere la chiave di registrazione del servizio, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="7d289-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="7d289-158">Per ottenere la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-158">To get the service registration key</span></span>
1. <span data-ttu-id="7d289-159">In **Gestione dispositivi StorSimple** passare a **Gestione&gt;** **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="7d289-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="7d289-161">Nel pannello **Chiavi** viene visualizzata la chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="7d289-162">Copiare la chiave di registrazione usando l'icona di copia.</span><span class="sxs-lookup"><span data-stu-id="7d289-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="7d289-163">Conservare la chiave di registrazione del servizio in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="7d289-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="7d289-164">Questa chiave e la chiave DEK del servizio saranno necessarie per registrare altri dispositivi con il servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="7d289-165">Dopo aver ottenuto la chiave di registrazione del servizio, è necessario configurare il dispositivo tramite l'interfaccia di Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="7d289-166">Rigenerare la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-166">Regenerate the service registration key</span></span>
<span data-ttu-id="7d289-167">La rigenerazione di una chiave di registrazione del servizio deve essere effettuata quando è necessario eseguire la rotazione delle chiavi o se l'elenco di amministratori del servizio è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="7d289-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="7d289-168">Quando si rigenera la chiave, quest'ultima viene usata solo per registrare dispositivi successivi.</span><span class="sxs-lookup"><span data-stu-id="7d289-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="7d289-169">I dispositivi già registrati non sono interessati da questo processo.</span><span class="sxs-lookup"><span data-stu-id="7d289-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="7d289-170">Per rigenerare una chiave di registrazione del servizio, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="7d289-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="7d289-171">Per rigenerare la chiave di registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="7d289-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="7d289-172">In **Gestione dispositivi StorSimple** passare a **Gestione&gt;** **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="7d289-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="7d289-174">Nel pannello **Chiavi** fare clic su **Rigenera**.</span><span class="sxs-lookup"><span data-stu-id="7d289-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Fare clic su Rigenera](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="7d289-176">Nel pannello **Rigenera la chiave di registrazione del servizio** esaminare l'azione necessaria quando le chiavi vengono rigenerate.</span><span class="sxs-lookup"><span data-stu-id="7d289-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="7d289-177">Tutti i dispositivi successivi registrati con questo servizio useranno la nuova chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="7d289-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="7d289-178">Fare clic su **Rigenera** per confermare.</span><span class="sxs-lookup"><span data-stu-id="7d289-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="7d289-179">Al completamento della registrazione si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="7d289-179">You will be notified after the registration is complete.</span></span>
   
   ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="7d289-181">Verrà visualizzata una nuova chiave di registrazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-181">A new service registration key will appear.</span></span>
   
    ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="7d289-183">Copiare la chiave e salvarla per registrare eventuali nuovi dispositivi con il servizio.</span><span class="sxs-lookup"><span data-stu-id="7d289-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d289-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d289-184">Next steps</span></span>
* <span data-ttu-id="7d289-185">Informazioni su come [iniziare a usare](storsimple-virtual-array-deploy1-portal-prep.md) un array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d289-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="7d289-186">Informazioni su come [amministrare il dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="7d289-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

