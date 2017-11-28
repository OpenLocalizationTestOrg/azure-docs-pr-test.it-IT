---
title: aaaHow tooconfigure un servizio cloud (portale) | Documenti Microsoft
description: Informazioni su come dei servizi cloud tooconfigure in Azure. Informazioni di configurazione del servizio cloud tooupdate hello e configurare accesso remoto toorole istanze. Questi esempi utilizzano hello portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="ee258-105">Come tooConfigure dei servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="ee258-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee258-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ee258-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="ee258-107">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="ee258-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="ee258-108">È possibile configurare le impostazioni di hello più comunemente usato per un servizio cloud nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ee258-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="ee258-109">In alternativa, se si desidera tooupdate i file di configurazione direttamente, scaricare un tooupdate di file di configurazione del servizio e quindi caricare hello aggiornare file e aggiornamento hello servizio cloud con le modifiche alla configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="ee258-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="ee258-110">In entrambi i casi, gli aggiornamenti della configurazione hello vengono inviati tooall le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee258-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="ee258-111">È inoltre possibile gestire le istanze di hello dei ruoli del servizio cloud o desktop remoto in essi.</span><span class="sxs-lookup"><span data-stu-id="ee258-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="ee258-112">Azure per garantire la disponibilità del servizio al 99,95% durante hello gli aggiornamenti della configurazione se si dispone di almeno due istanze del ruolo per ogni ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee258-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="ee258-113">Che consente una macchina virtuale tooprocess client richieste durante l'aggiornamento hello altri.</span><span class="sxs-lookup"><span data-stu-id="ee258-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="ee258-114">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="ee258-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="ee258-115">Modificare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ee258-115">Change a cloud service</span></span>
<span data-ttu-id="ee258-116">Dopo l'apertura hello [portale di Azure](https://portal.azure.com/), passare servizio cloud tooyour.</span><span class="sxs-lookup"><span data-stu-id="ee258-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="ee258-117">Da qui è possibile gestire molti aspetti.</span><span class="sxs-lookup"><span data-stu-id="ee258-117">From here, you manage many aspects of it.</span></span>

![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="ee258-119">Hello **impostazioni** o **tutte le impostazioni** collegamenti determina l'apertura dei hello **impostazioni** pannello in cui è possibile modificare hello **proprietà**, modificare hello **Configurazione**, gestire hello **certificati**, il programma di installazione **regole di avviso**e gestire hello **utenti** che dispongono dell'accesso toothis servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ee258-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Pannello delle impostazioni del servizio cloud di Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="ee258-121">Gestire la versione del sistema operativo guest</span><span class="sxs-lookup"><span data-stu-id="ee258-121">Manage Guest OS version</span></span>

<span data-ttu-id="ee258-122">Per impostazione predefinita, Azure Aggiorna periodicamente il guest immagine del sistema operativo toohello più recenti supportate all'interno di hello famiglia di sistemi operativi specificati nella configurazione del servizio (con estensione cscfg), ad esempio Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ee258-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="ee258-123">Se è necessario tootarget una specifica versione del sistema operativo, è possibile impostare in hello **configurazione** blade.</span><span class="sxs-lookup"><span data-stu-id="ee258-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Configurare la versione del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="ee258-125">La scelta di una versione specifica del sistema operativo comporta la disabilitazione degli aggiornamenti automatici del sistema operativo e rende l'applicazione di patch a carico dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ee258-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="ee258-126">È necessario assicurarsi che le istanze del ruolo ricezione degli aggiornamenti o potrebbe esporre le vulnerabilità toosecurity l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ee258-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="ee258-127">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="ee258-127">Monitoring</span></span>
<span data-ttu-id="ee258-128">È possibile aggiungere il servizio cloud tooyour di avvisi.</span><span class="sxs-lookup"><span data-stu-id="ee258-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="ee258-129">Fare clic su **Impostazioni** > **Regole di avviso** > **Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="ee258-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="ee258-130">Da qui è possibile configurare un avviso.</span><span class="sxs-lookup"><span data-stu-id="ee258-130">From here, you can setup an alert.</span></span> <span data-ttu-id="ee258-131">Con hello **metrica** elenchi a discesa, è possibile configurare un avviso per hello seguenti tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="ee258-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="ee258-132">Lettura disco</span><span class="sxs-lookup"><span data-stu-id="ee258-132">Disk read</span></span>
* <span data-ttu-id="ee258-133">Scrittura disco</span><span class="sxs-lookup"><span data-stu-id="ee258-133">Disk write</span></span>
* <span data-ttu-id="ee258-134">Rete in ingresso</span><span class="sxs-lookup"><span data-stu-id="ee258-134">Network in</span></span>
* <span data-ttu-id="ee258-135">Rete in uscita</span><span class="sxs-lookup"><span data-stu-id="ee258-135">Network out</span></span>
* <span data-ttu-id="ee258-136">Percentuale CPU</span><span class="sxs-lookup"><span data-stu-id="ee258-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="ee258-137">Configurazione del monitoraggio da un riquadro della metrica</span><span class="sxs-lookup"><span data-stu-id="ee258-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="ee258-138">Anziché utilizzare **impostazioni** > **le regole di avviso**, è possibile fare clic su uno dei riquadri di metrica hello in hello **monitoraggio** sezione di hello **Cloud servizio** blade.</span><span class="sxs-lookup"><span data-stu-id="ee258-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Monitoraggio del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="ee258-140">Da qui è possibile personalizzare il grafico di hello utilizzato con il riquadro hello o aggiungere una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="ee258-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="ee258-141">Riavviare il computer, ricreare l'immagine o creare una connessione Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="ee258-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="ee258-142">In questo momento non è possibile configurare desktop remoto utilizzando hello **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ee258-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="ee258-143">Tuttavia, è possibile configurarlo tramite hello [portale di Azure classico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), o tramite [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ee258-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="ee258-144">Fare clic sull'istanza di servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="ee258-144">First, click on hello cloud service instance.</span></span>

![Istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="ee258-146">Da hello pannello visualizzato è possibile avviare una connessione desktop remoto, riavviare in remoto hello istanza o in modalità remota istanza hello ricreazione dell'immagine (inizia con un'immagine aggiornata).</span><span class="sxs-lookup"><span data-stu-id="ee258-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Pulsanti di istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="ee258-148">Riconfigurare il file con estensione cscfg</span><span class="sxs-lookup"><span data-stu-id="ee258-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="ee258-149">Potrebbe essere necessario tooreconfigure il servizio cloud tramite hello [configurazione del servizio (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="ee258-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="ee258-150">È necessario innanzitutto toodownload il file con estensione cscfg del file, modificarlo e caricarlo.</span><span class="sxs-lookup"><span data-stu-id="ee258-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="ee258-151">Fare clic su hello **impostazioni** icona o hello **tutte le impostazioni** collegamento tooopen backup hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="ee258-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="ee258-153">Fare clic su hello **configurazione** elemento.</span><span class="sxs-lookup"><span data-stu-id="ee258-153">Click on hello **Configuration** item.</span></span>

    ![Blade Configurazione](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="ee258-155">Fare clic su hello **scaricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ee258-155">Click on hello **Download** button.</span></span>

    ![Scaricare](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="ee258-157">Dopo aver aggiornato il file di configurazione servizio hello, caricare e applicare gli aggiornamenti della configurazione hello:</span><span class="sxs-lookup"><span data-stu-id="ee258-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Carica](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="ee258-159">Selezionare i file con estensione cscfg hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee258-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee258-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee258-160">Next steps</span></span>
* <span data-ttu-id="ee258-161">Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee258-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="ee258-162">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee258-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="ee258-163">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee258-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="ee258-164">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee258-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
