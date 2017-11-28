---
title: "Attività comuni di gestione di servizi cloud | Documentazione Microsoft"
description: Informazioni su come gestire i servizi cloud nel portale di Azure. Questi esempi utilizzano il portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="d8283-104">Come gestire i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="d8283-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8283-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d8283-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="d8283-106">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="d8283-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="d8283-107">Nell'area **Servizi cloud (versione classica)** del portale di Azure è possibile aggiornare un ruolo di servizio o una distribuzione, convertire una pre-distribuzione in una distribuzione di produzione, collegare risorse al servizio cloud per visualizzare le dipendenze delle risorse e ridimensionare le risorse insieme, oltre a eliminare un servizio cloud o una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d8283-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="d8283-108">Altre informazioni sul ridimensionamento del servizio cloud sono disponibili [qui](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="d8283-109">Procedura: Aggiornare un ruolo o una distribuzione del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="d8283-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="d8283-110">Se è necessario aggiornare il codice dell'applicazione per il servizio cloud, utilizzare **Aggiorna** nel blade del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="d8283-111">È possibile aggiornare un singolo ruolo o tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="d8283-111">You can update a single role or all roles.</span></span> <span data-ttu-id="d8283-112">Per eseguire l'aggiornamento, è possibile caricare un nuovo pacchetto del servizio o un nuovo file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="d8283-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="d8283-113">Nel [portale di Azure][Azure portal] selezionare il servizio cloud che si desidera aggiornare.</span><span class="sxs-lookup"><span data-stu-id="d8283-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="d8283-114">Questo passaggio consente di aprire il pannello dell'istanza del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="d8283-115">Nel blade, scegliere il pulsante **Aggiorna** .</span><span class="sxs-lookup"><span data-stu-id="d8283-115">In the blade, click the **Update** button.</span></span>

    ![Pulsante Aggiorna](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="d8283-117">Aggiornare la distribuzione con un nuovo file di pacchetto di servizio (.cspkg) e il file di configurazione del servizio (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="d8283-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="d8283-119">**Facoltativamente** aggiornare l'etichetta di distribuzione e l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d8283-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="d8283-120">Se uno o più ruoli contengono una sola istanza del ruolo, selezionare la casella di controllo **Distribuisci anche se uno o più ruoli contengono una singola istanza** per abilitare l'esecuzione dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d8283-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="d8283-121">Durante un aggiornamento del servizio cloud, Azure può garantire una percentuale di disponibilità del servizio pari solo al 99,95% se ogni ruolo contiene almeno due istanze del ruolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="d8283-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="d8283-122">Con due istanze del ruolo, una macchina virtuale elabora le richieste dei client mentre l'altra viene aggiornata.</span><span class="sxs-lookup"><span data-stu-id="d8283-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="d8283-123">Selezionare **Avvia distribuzione** per applicare l'aggiornamento al termine del caricamento del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8283-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="d8283-124">Fare clic su **OK** per iniziare l'aggiornamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="d8283-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="d8283-125">Procedura: Scambiare le distribuzioni per convertire una distribuzione di gestione temporanea in una distribuzione di produzione</span><span class="sxs-lookup"><span data-stu-id="d8283-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="d8283-126">Quando si decide di distribuire una nuova versione di un servizio cloud, è possibile eseguirne un'installazione di appoggio e testarla nell'ambiente di staging del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="d8283-127">Usare **Scambia** per scambiare gli URL di indirizzamento delle due distribuzioni e alzare di livello la nuova versione in produzione.</span><span class="sxs-lookup"><span data-stu-id="d8283-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="d8283-128">È possibile scambiare le distribuzioni dalla pagina **Cloud Services** o dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="d8283-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="d8283-129">Nel [portale di Azure][Azure portal] selezionare il servizio cloud che si desidera aggiornare.</span><span class="sxs-lookup"><span data-stu-id="d8283-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="d8283-130">Questo passaggio consente di aprire il pannello dell'istanza del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="d8283-131">Nel blade, scegliere il pulsante **Scambia** .</span><span class="sxs-lookup"><span data-stu-id="d8283-131">In the blade, click the **Swap** button.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="d8283-133">Verrà visualizzata la seguente richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="d8283-133">The following confirmation prompt opens.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="d8283-135">Dopo avere controllato le informazioni di distribuzione, fare clic su **OK** per scambiare le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d8283-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="d8283-136">Lo scambio delle distribuzioni avviene rapidamente perché l'unico elemento che cambia è rappresentato dagli indirizzi IP virtuali (VIP) delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d8283-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="d8283-137">Per ridurre i costi di calcolo, è possibile eliminare la distribuzione di gestione di staging dopo avere verificato che la distribuzione di produzione funziona nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="d8283-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="d8283-138">Domande comuni sullo scambio di distribuzioni</span><span class="sxs-lookup"><span data-stu-id="d8283-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="d8283-139">**Quali sono i prerequisiti per lo scambio delle distribuzioni?**</span><span class="sxs-lookup"><span data-stu-id="d8283-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="d8283-140">Esistono due prerequisiti chiave per lo scambio corretto di distribuzioni:</span><span class="sxs-lookup"><span data-stu-id="d8283-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="d8283-141">Se si desidera usare un indirizzo IP statico per lo slot di produzione, è necessario riservarne uno anche per lo slot di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="d8283-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="d8283-142">In caso contrario, lo scambio ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d8283-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="d8283-143">Tutte le istanze dei ruoli devono essere in esecuzione prima di poter eseguire lo scambio.</span><span class="sxs-lookup"><span data-stu-id="d8283-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="d8283-144">È possibile controllare lo stato delle istanze nel pannello Panoramica del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8283-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="d8283-145">In alternativa, è possibile usare il comando [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8283-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="d8283-146">Si noti che anche gli aggiornamenti del sistema operativo guest e le operazioni di correzione del servizio possono ostacolare il corretto scambio delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d8283-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="d8283-147">Per altre informazioni, vedere [Risolvere eventuali problemi di distribuzione dei servizi cloud](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="d8283-148">**Uno scambio comporta un tempo di inattività per l'applicazione? Come gestire questa situazione?**</span><span class="sxs-lookup"><span data-stu-id="d8283-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="d8283-149">Come descritto nella sezione precedente, lo scambio di distribuzioni è in genere veloce perché è una semplice modifica della configurazione in Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d8283-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="d8283-150">In alcuni casi, tuttavia, può richiedere più di dieci secondi e causare errori di connessione temporanei.</span><span class="sxs-lookup"><span data-stu-id="d8283-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="d8283-151">Per limitare l'impatto sui clienti, si consiglia di implementare la [logica di ripetizione dei tentativi nel client](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="d8283-152">Procedura: Collegare una risorsa a un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="d8283-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="d8283-153">Il portale di Azure non collega tra loro le risorse come nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="d8283-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="d8283-154">Distribuire invece risorse aggiuntive allo stesso gruppo di risorse usato dal servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="d8283-155">Procedura: Eliminare le distribuzioni e un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="d8283-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="d8283-156">Per eliminare un servizio cloud è necessario prima eliminare tutte le distribuzioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="d8283-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="d8283-157">Per ridurre i costi di calcolo, è possibile eliminare la distribuzione di gestione di staging dopo avere verificato che la distribuzione di produzione funziona nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="d8283-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="d8283-158">Vengono addebitati i costi di calcolo per le istanze del ruolo distribuite che sono state arrestate.</span><span class="sxs-lookup"><span data-stu-id="d8283-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="d8283-159">Per eliminare una distribuzione o il servizio cloud, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="d8283-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="d8283-160">Nel [portale di Azure][Azure portal] selezionare il servizio cloud che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="d8283-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="d8283-161">Questo passaggio consente di aprire il pannello dell'istanza del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d8283-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="d8283-162">Nel blade, scegliere il pulsante **Elimina** .</span><span class="sxs-lookup"><span data-stu-id="d8283-162">In the blade, click the **Delete** button.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="d8283-164">È possibile eliminare l'intero servizio cloud selezionando **Servizio cloud e relative distribuzioni** oppure scegliere la **Distribuzione di produzione** o la **Distribuzione di staging**.</span><span class="sxs-lookup"><span data-stu-id="d8283-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="d8283-166">Scegliere il pulsante **Elimina** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d8283-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="d8283-167">Per eliminare il servizio cloud fare clic su **Delete cloud service**.</span><span class="sxs-lookup"><span data-stu-id="d8283-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="d8283-168">Quindi, alla richiesta di conferma fare clic su **Yes**.</span><span class="sxs-lookup"><span data-stu-id="d8283-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8283-169">Quando un servizio cloud viene eliminato e viene configurato il monitoraggio dettagliato, è necessario eliminare manualmente i dati dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d8283-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="d8283-170">Per informazioni sull'ubicazione delle tabelle di metriche, vedere [questo articolo](cloud-services-how-to-monitor.md) :</span><span class="sxs-lookup"><span data-stu-id="d8283-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="d8283-171">Procedura: Trovare altre informazioni sulle distribuzioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="d8283-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="d8283-172">Il pannello **Panoramica** comprende una barra di stato in alto.</span><span class="sxs-lookup"><span data-stu-id="d8283-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="d8283-173">Quando si fa clic sulla barra, si apre un nuovo pannello che visualizza le informazioni sugli errori.</span><span class="sxs-lookup"><span data-stu-id="d8283-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="d8283-174">Se la distribuzione non contiene errori, il pannello delle informazioni è vuoto.</span><span class="sxs-lookup"><span data-stu-id="d8283-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="d8283-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8283-176">Next steps</span></span>
* <span data-ttu-id="d8283-177">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="d8283-178">Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="d8283-179">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="d8283-180">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8283-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
