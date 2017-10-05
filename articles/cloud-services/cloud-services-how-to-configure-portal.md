---
title: Come configurare un servizio cloud (portale) | Documentazione Microsoft
description: Informazioni su come configurare un servizio cloud in Azure. Informazioni su come aggiornare la configurazione del servizio cloud e configurare l'accesso remoto per le istanze del ruolo. Questi esempi utilizzano il portale di Azure.
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
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="28987-105">Come configurare i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="28987-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28987-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28987-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="28987-107">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="28987-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="28987-108">È possibile configurare le impostazioni più comuni di un servizio cloud nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28987-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="28987-109">In alternativa, se si preferisce aggiornare direttamente i file di configurazione, scaricare un file di configurazione del servizio da aggiornare, quindi caricare il file aggiornato e aggiornare il servizio cloud con le modifiche apportate alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="28987-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="28987-110">In ogni caso, per gli aggiornamenti della configurazione viene effettuato il push in tutte le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="28987-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="28987-111">È anche possibile gestire le istanze dei ruoli del servizio cloud o creare una connessione Desktop remoto per tali servizi.</span><span class="sxs-lookup"><span data-stu-id="28987-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="28987-112">Azure può garantire il 99,95 di disponibilità del servizio durante gli aggiornamenti della configurazione solo se si dispone di almeno due istanze del ruolo per ogni ruolo.</span><span class="sxs-lookup"><span data-stu-id="28987-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="28987-113">In questo modo, una macchina virtuale può elaborare le richieste dei client mentre l'altra viene aggiornata.</span><span class="sxs-lookup"><span data-stu-id="28987-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="28987-114">Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="28987-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="28987-115">Modificare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="28987-115">Change a cloud service</span></span>
<span data-ttu-id="28987-116">Dopo aver aperto il [portale di Azure](https://portal.azure.com/), passare al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="28987-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="28987-117">Da qui è possibile gestire molti aspetti.</span><span class="sxs-lookup"><span data-stu-id="28987-117">From here, you manage many aspects of it.</span></span>

![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="28987-119">I collegamenti **Impostazioni** o **Tutte le impostazioni** consentono di accedere al pannello **Impostazioni** nel quale è possibile modificare le **proprietà** e la **configurazione**, gestire i **certificati**, configurare le **regole di avviso** e gestire gli **utenti** che hanno accesso a questo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="28987-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Pannello delle impostazioni del servizio cloud di Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="28987-121">Gestire la versione del sistema operativo guest</span><span class="sxs-lookup"><span data-stu-id="28987-121">Manage Guest OS version</span></span>

<span data-ttu-id="28987-122">Per impostazione predefinita, Azure aggiorna periodicamente il sistema operativo guest all'immagine supportata più recente nella famiglia di sistemi operativi specificata nella configurazione del servizio (file con estensione cscfg), ad esempio Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="28987-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="28987-123">Se è necessario fare riferimento a una versione specifica del sistema operativo, è possibile configurarla nel pannello **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="28987-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Configurare la versione del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="28987-125">La scelta di una versione specifica del sistema operativo comporta la disabilitazione degli aggiornamenti automatici del sistema operativo e rende l'applicazione di patch a carico dell'utente.</span><span class="sxs-lookup"><span data-stu-id="28987-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="28987-126">È necessario assicurarsi che le istanze del ruolo ricevano gli aggiornamenti. In caso contrario, si rischia l'esposizione dell'applicazione a vulnerabilità della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="28987-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="28987-127">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="28987-127">Monitoring</span></span>
<span data-ttu-id="28987-128">È possibile aggiungere avvisi al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="28987-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="28987-129">Fare clic su **Impostazioni** > **Regole di avviso** > **Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="28987-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="28987-130">Da qui è possibile configurare un avviso.</span><span class="sxs-lookup"><span data-stu-id="28987-130">From here, you can setup an alert.</span></span> <span data-ttu-id="28987-131">La casella di riepilogo a discesa **Metrica** consente di configurare un avviso per i tipi di dati seguenti.</span><span class="sxs-lookup"><span data-stu-id="28987-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="28987-132">Lettura disco</span><span class="sxs-lookup"><span data-stu-id="28987-132">Disk read</span></span>
* <span data-ttu-id="28987-133">Scrittura disco</span><span class="sxs-lookup"><span data-stu-id="28987-133">Disk write</span></span>
* <span data-ttu-id="28987-134">Rete in ingresso</span><span class="sxs-lookup"><span data-stu-id="28987-134">Network in</span></span>
* <span data-ttu-id="28987-135">Rete in uscita</span><span class="sxs-lookup"><span data-stu-id="28987-135">Network out</span></span>
* <span data-ttu-id="28987-136">Percentuale CPU</span><span class="sxs-lookup"><span data-stu-id="28987-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="28987-137">Configurazione del monitoraggio da un riquadro della metrica</span><span class="sxs-lookup"><span data-stu-id="28987-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="28987-138">Invece di usare **Impostazioni** > **Regole di avviso** è possibile fare clic su uno dei riquadri metrici nella sezione **Monitoraggio** del pannello del **servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="28987-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Monitoraggio del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="28987-140">Da qui è possibile personalizzare il grafico usato con il riquadro oppure aggiungere una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="28987-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="28987-141">Riavviare il computer, ricreare l'immagine o creare una connessione Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="28987-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="28987-142">In questo momento non è possibile configurare Desktop remoto con il **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="28987-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="28987-143">È tuttavia possibile configurarlo con il [portale di Azure classico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) o [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="28987-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="28987-144">Per iniziare, fare clic sull'istanza del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="28987-144">First, click on the cloud service instance.</span></span>

![Istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="28987-146">Dal pannello visualizzato è possibile avviare una connessione Desktop remoto, riavviare l'istanza o ricrearne l'immagine in remoto (iniziare con un'immagine aggiornata).</span><span class="sxs-lookup"><span data-stu-id="28987-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Pulsanti di istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="28987-148">Riconfigurare il file con estensione cscfg</span><span class="sxs-lookup"><span data-stu-id="28987-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="28987-149">Potrebbe essere necessario riconfigurare il servizio cloud con il file di [configurazione del servizio (CSCFG)](cloud-services-model-and-package.md#cscfg).</span><span class="sxs-lookup"><span data-stu-id="28987-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="28987-150">È prima necessario scaricare il file con estensione cscfg, modificarlo, quindi caricarlo.</span><span class="sxs-lookup"><span data-stu-id="28987-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="28987-151">Fare clic sull'icona **Impostazioni** o sul collegamento **Tutte le impostazioni** per aprire il pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="28987-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="28987-153">Fare clic sull’elemento **Configurazione** .</span><span class="sxs-lookup"><span data-stu-id="28987-153">Click on the **Configuration** item.</span></span>

    ![Blade Configurazione](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="28987-155">Fare clic sul pulsante **Download** .</span><span class="sxs-lookup"><span data-stu-id="28987-155">Click on the **Download** button.</span></span>

    ![Download](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="28987-157">Dopo aver aggiornato il file di configurazione del servizio, caricare e applicare gli aggiornamenti della configurazione:</span><span class="sxs-lookup"><span data-stu-id="28987-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Caricamento](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="28987-159">Selezionare il file con estensione cscfg e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28987-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28987-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28987-160">Next steps</span></span>
* <span data-ttu-id="28987-161">Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28987-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="28987-162">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28987-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="28987-163">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28987-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="28987-164">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="28987-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
