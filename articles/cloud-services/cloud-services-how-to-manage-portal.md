---
title: "attività di gestione del servizio cloud aaaCommon | Documenti Microsoft"
description: Informazioni su come dei servizi cloud toomanage in hello portale di Azure. Questi esempi utilizzano hello portale di Azure.
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
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="26d70-104">Come tooManage dei servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="26d70-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26d70-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="26d70-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="26d70-106">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="26d70-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="26d70-107">In hello **servizi Cloud (classico)** area di hello Azure portale, è possibile aggiornare un ruolo del servizio o una distribuzione, alzare di livello un tooproduction pre-distribuzione, collegare servizio cloud di risorse tooyour in questo modo è possibile visualizzare risorse hello dipendenze e la scala hello risorse insieme ed eliminare un servizio cloud o una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="26d70-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="26d70-108">Ulteriori informazioni su come tooscale il servizio cloud è disponibile [qui](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="26d70-109">Procedura: Aggiornare un ruolo o una distribuzione del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="26d70-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="26d70-110">Se è necessario codice dell'applicazione hello tooupdate per il servizio cloud, utilizzare **aggiornamento** nel Pannello di servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="26d70-111">È possibile aggiornare un singolo ruolo o tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="26d70-111">You can update a single role or all roles.</span></span> <span data-ttu-id="26d70-112">tooupdate, è possibile caricare un nuovo pacchetto del servizio o un file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="26d70-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="26d70-113">In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da tooupdate.</span><span class="sxs-lookup"><span data-stu-id="26d70-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="26d70-114">Questo passaggio apre il pannello di istanza del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="26d70-115">Nel Pannello di hello, fare clic su hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26d70-115">In hello blade, click hello **Update** button.</span></span>

    ![Pulsante Aggiorna](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="26d70-117">Aggiornare la distribuzione di hello con un nuovo file del pacchetto del servizio (con estensione cspkg) e i file di configurazione del servizio (cscfg).</span><span class="sxs-lookup"><span data-stu-id="26d70-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="26d70-119">**Facoltativamente** aggiornare l'etichetta della distribuzione hello e account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="26d70-120">Se i ruoli hanno solo un'istanza del ruolo, selezionare hello **Distribuisci anche se uno o più ruoli contengono una singola istanza** tooenable hello aggiornamento tooproceed.</span><span class="sxs-lookup"><span data-stu-id="26d70-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="26d70-121">Durante un aggiornamento del servizio cloud, Azure può garantire una percentuale di disponibilità del servizio pari solo al 99,95% se ogni ruolo contiene almeno due istanze del ruolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="26d70-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="26d70-122">Con due istanze del ruolo, una macchina virtuale elabora le richieste client mentre altri hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="26d70-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="26d70-123">Controllare **avviare distribuzione** aggiornamento hello toohave applicato dopo il caricamento di hello del pacchetto di hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="26d70-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="26d70-124">Fare clic su **OK** toobegin hello servizio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="26d70-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="26d70-125">Procedura: scambiare le distribuzioni toopromote tooproduction una distribuzione di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="26d70-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="26d70-126">Quando si decide di toodeploy una nuova versione di un servizio cloud, fase e testare la nuova release dell'ambiente di gestione temporanea del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="26d70-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="26d70-127">Utilizzare **scambiare** tooswitch hello URL da cui hello due distribuzioni vengono indirizzate e alzare di livello un nuovo tooproduction versione.</span><span class="sxs-lookup"><span data-stu-id="26d70-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="26d70-128">È possibile scambiare le distribuzioni da hello **servizi Cloud** hello o pagina dashboard.</span><span class="sxs-lookup"><span data-stu-id="26d70-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="26d70-129">In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da tooupdate.</span><span class="sxs-lookup"><span data-stu-id="26d70-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="26d70-130">Questo passaggio apre il pannello di istanza del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="26d70-131">Nel Pannello di hello, fare clic su hello **scambiare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26d70-131">In hello blade, click hello **Swap** button.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="26d70-133">Hello richiesta di conferma seguente viene aperto.</span><span class="sxs-lookup"><span data-stu-id="26d70-133">hello following confirmation prompt opens.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="26d70-135">Dopo aver verificato le informazioni di distribuzione hello, fare clic su **OK** distribuzioni hello tooswap.</span><span class="sxs-lookup"><span data-stu-id="26d70-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="26d70-136">lo scambio di distribuzioni Hello possa avvenire rapidamente perché hello unico elemento che viene modificato è hello gli indirizzi IP virtuali (VIP) per le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="26d70-137">toosave calcolo dei costi, è possibile eliminare hello distribuzione di gestione temporanea dopo aver verificato che la distribuzione di produzione funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="26d70-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="26d70-138">Domande comuni sullo scambio di distribuzioni</span><span class="sxs-lookup"><span data-stu-id="26d70-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="26d70-139">**Quali sono i prerequisiti hello per le distribuzioni di effettuare lo swapping?**</span><span class="sxs-lookup"><span data-stu-id="26d70-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="26d70-140">Esistono due prerequisiti chiave per lo scambio corretto di distribuzioni:</span><span class="sxs-lookup"><span data-stu-id="26d70-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="26d70-141">Se si desidera usare un indirizzo IP statico toouse slot di produzione, è necessario riservare uno slot di gestione temporanea anche.</span><span class="sxs-lookup"><span data-stu-id="26d70-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="26d70-142">In caso contrario, lo scambio di hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="26d70-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="26d70-143">Tutte le istanze dei ruoli devono essere in esecuzione prima di poter eseguire lo scambio di hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="26d70-144">È possibile controllare lo stato di hello delle istanze del pannello della panoramica hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26d70-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="26d70-145">In alternativa, è possibile utilizzare hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26d70-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="26d70-146">Si noti che gli aggiornamenti del sistema operativo Guest e le operazioni di correzione del servizio può essere causato anche distribuzione Scambia toofail.</span><span class="sxs-lookup"><span data-stu-id="26d70-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="26d70-147">Per altre informazioni, vedere [Risolvere eventuali problemi di distribuzione dei servizi cloud](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="26d70-148">**Uno scambio comporta un tempo di inattività per l'applicazione? Come gestire questa situazione?**</span><span class="sxs-lookup"><span data-stu-id="26d70-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="26d70-149">Come descritto nella sezione precedente di hello, in quanto è solo una modifica della configurazione nel servizio di bilanciamento carico di Azure hello è rapido in genere uno scambio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="26d70-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="26d70-150">In alcuni casi, tuttavia, può richiedere più di dieci secondi e causare errori di connessione temporanei.</span><span class="sxs-lookup"><span data-stu-id="26d70-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="26d70-151">i clienti tooyour impatto toolimit, si consiglia di implementare [logica di ripetizione dei client](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="26d70-152">Procedura: collegamento di un servizio cloud di risorse tooa</span><span class="sxs-lookup"><span data-stu-id="26d70-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="26d70-153">Hello portale di Azure non è collegato risorse insieme come hello corrente portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="26d70-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="26d70-154">In alternativa, distribuire risorse aggiuntive toohello stesso gruppo di risorse utilizzato dal servizio Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="26d70-155">Procedura: Eliminare le distribuzioni e un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="26d70-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="26d70-156">Per eliminare un servizio cloud è necessario prima eliminare tutte le distribuzioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="26d70-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="26d70-157">toosave calcolo dei costi, è possibile eliminare hello distribuzione di gestione temporanea dopo aver verificato che la distribuzione di produzione funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="26d70-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="26d70-158">Vengono addebitati i costi di calcolo per le istanze del ruolo distribuite che sono state arrestate.</span><span class="sxs-lookup"><span data-stu-id="26d70-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="26d70-159">Utilizzare hello seguendo procedure toodelete una distribuzione o il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="26d70-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="26d70-160">In hello [portale di Azure][Azure portal], selezionare il servizio di cloud hello da toodelete.</span><span class="sxs-lookup"><span data-stu-id="26d70-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="26d70-161">Questo passaggio apre il pannello di istanza del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="26d70-162">Nel Pannello di hello, fare clic su hello **eliminare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26d70-162">In hello blade, click hello **Delete** button.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="26d70-164">È possibile eliminare hello intero servizio cloud controllando **servizio Cloud e le relative distribuzioni** oppure scegliere uno hello **distribuzione di produzione** o hello **distribuzione di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="26d70-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="26d70-166">Fare clic su hello **eliminare** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="26d70-167">servizio cloud di hello toodelete, fare clic su **servizio cloud Delete**.</span><span class="sxs-lookup"><span data-stu-id="26d70-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="26d70-168">Al prompt di conferma hello, quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="26d70-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="26d70-169">Quando viene eliminato un servizio cloud e il monitoraggio dettagliato è configurato, è necessario eliminare manualmente i dati di hello dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="26d70-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="26d70-170">Per informazioni su dove toofind hello tabelle di metrica, vedere [questo](cloud-services-how-to-monitor.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="26d70-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="26d70-171">Procedura: Trovare altre informazioni sulle distribuzioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="26d70-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="26d70-172">Hello **Panoramica** blade dispone di una barra di stato nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="26d70-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="26d70-173">Quando si fa clic sulla barra di hello, un nuovo pannello aprirà e visualizzerà le informazioni di errore.</span><span class="sxs-lookup"><span data-stu-id="26d70-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="26d70-174">Se la distribuzione di hello non contiene errori, pannello informazioni hello è vuoto.</span><span class="sxs-lookup"><span data-stu-id="26d70-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Scambio di servizi cloud](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="26d70-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26d70-176">Next steps</span></span>
* <span data-ttu-id="26d70-177">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="26d70-178">Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="26d70-179">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="26d70-180">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26d70-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
