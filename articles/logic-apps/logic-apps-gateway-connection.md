---
title: Accesso alle risorse di dati locali per le App per la logica di Azure | Microsoft Docs
description: Configurare il gateway dati locale in moda da poter accedere alle origini dati in locale dalle app per la logica
keywords: accesso ai dati, locale, trasferimento dei dati, crittografia, origini dei dati
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="52df6-104">Accedere alle origini dati in locale dalle app per la logica con il gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="52df6-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="52df6-105">Per accedere alle origini dati in locale dalle app per la logica, configurare un gateway dati locale che le app per la logica possono usare con i connettori supportati.</span><span class="sxs-lookup"><span data-stu-id="52df6-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="52df6-106">Il gateway funge da ponte che fornisce il trasferimento rapido dei dati e la crittografia tra le origini di dati in locale e le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="52df6-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="52df6-107">Il gateway inoltra i dati da origini locali sui canali crittografati tramite il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="52df6-108">Tutto il traffico ha origine come traffico sicuro in uscita dall'agente di gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="52df6-109">Altre informazioni sul [funzionamento del gateway dati](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="52df6-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="52df6-110">Il gateway supporta le connessioni alle origine dati locali seguenti:</span><span class="sxs-lookup"><span data-stu-id="52df6-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="52df6-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="52df6-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="52df6-112">DB2</span><span class="sxs-lookup"><span data-stu-id="52df6-112">DB2</span></span>  
*   <span data-ttu-id="52df6-113">File system</span><span class="sxs-lookup"><span data-stu-id="52df6-113">File System</span></span>
*   <span data-ttu-id="52df6-114">Informix</span><span class="sxs-lookup"><span data-stu-id="52df6-114">Informix</span></span>
*   <span data-ttu-id="52df6-115">MQ</span><span class="sxs-lookup"><span data-stu-id="52df6-115">MQ</span></span>
*   <span data-ttu-id="52df6-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="52df6-116">MySQL</span></span>
*   <span data-ttu-id="52df6-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="52df6-117">Oracle Database</span></span>
*   <span data-ttu-id="52df6-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="52df6-118">PostgreSQL</span></span>
*   <span data-ttu-id="52df6-119">Server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="52df6-119">SAP Application Server</span></span> 
*   <span data-ttu-id="52df6-120">Server messaggi SAP</span><span class="sxs-lookup"><span data-stu-id="52df6-120">SAP Message Server</span></span>
*   <span data-ttu-id="52df6-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="52df6-121">SharePoint</span></span>
*   <span data-ttu-id="52df6-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="52df6-122">SQL Server</span></span>
*   <span data-ttu-id="52df6-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="52df6-123">Teradata</span></span>

<span data-ttu-id="52df6-124">Questa procedura mostra come configurare il gateway dati locale per lavorare con le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="52df6-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="52df6-125">Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="52df6-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="52df6-126">Per informazioni su come usare il gateway con altri servizi, vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="52df6-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="52df6-127">Gateway dati locale di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="52df6-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="52df6-128">Gateway dati locale di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="52df6-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="52df6-129">Gateway dati locale di Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="52df6-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="52df6-130">Gateway dati locale di Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="52df6-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="52df6-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="52df6-131">Requirements</span></span>

* <span data-ttu-id="52df6-132">È necessario già disporre del [gateway dati locale installato in un computer locale](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="52df6-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="52df6-133">Quando si accede al portale di Azure, è necessario usare lo stesso account aziendale o dell'istituto di istruzione usato per [installare il gateway dati locale](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="52df6-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="52df6-134">L'account di accesso deve avere anche una sottoscrizione di Azure da usare quando si crea una risorsa di gateway nel portale di Azure per l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="52df6-135">L'installazione del gateway non può essere già richiesta da una risorsa del gateway di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="52df6-136">È possibile associare l'installazione del gateway a una sola risorsa del gateway di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="52df6-137">L'attestazione avviene quando si crea la risorsa per il gateway in modo che l'installazione non sia disponibile per le altre risorse.</span><span class="sxs-lookup"><span data-stu-id="52df6-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="52df6-138">Configurare la connessione al gateway dati</span><span class="sxs-lookup"><span data-stu-id="52df6-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="52df6-139">1. Installare il gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="52df6-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="52df6-140">Se l'utente non lo hai già fatto, seguire la [procedura per installare il gateway dati locale](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="52df6-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="52df6-141">Prima di continuare con gli altri passaggi, assicurarsi di aver installato il gateway dati in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="52df6-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="52df6-142">2. Creare una risorsa di Azure per il gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="52df6-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="52df6-143">Dopo aver installato il gateway in un computer locale, è necessario creare il gateway dati come una risorsa in Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="52df6-144">Questo passaggio associa anche la risorsa di gateway con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="52df6-145">Accedere al [Portale di Azure](https://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="52df6-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="52df6-146">Assicurarsi di usare lo stesso indirizzo di posta elettronica aziendale o dell'istituto di istruzione usato per installare il gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="52df6-147">Nel menu a sinistra in Azure, scegliere **Nuovo** > **Integrazione aziendale** > **Gateway dati locale** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="52df6-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Trovare "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="52df6-149">Nel pannello **Crea gateway di connessione** fornire questi dettagli per creare la risorsa di gateway dati:</span><span class="sxs-lookup"><span data-stu-id="52df6-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="52df6-150">**Nome**: inserire un nome per la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="52df6-151">**Sottoscrizione**: selezionare la sottoscrizione di Azure da associare alla risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="52df6-152">La presente sottoscrizione deve essere la stessa sottoscrizione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="52df6-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="52df6-153">La sottoscrizione predefinita si basa sull'account di Azure usato per accedere.</span><span class="sxs-lookup"><span data-stu-id="52df6-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="52df6-154">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente per distribuire la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="52df6-155">I gruppi di risorse consentono di gestire gli asset di Azure correlati come una raccolta.</span><span class="sxs-lookup"><span data-stu-id="52df6-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="52df6-156">**Percorso**: Azure limita questo percorso alla stessa area selezionata per il servizio cloud di gateway durante [l'installazione del gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="52df6-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="52df6-157">Assicurarsi che il percorso della risorsa di gateway corrisponda al percorso del servizio cloud di gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="52df6-158">In caso contrario, l'installazione del gateway potrebbe non essere visualizzata nell'elenco dei gateway installati da selezionare nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="52df6-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="52df6-159">È possibile usare aree diverse per la risorsa del gateway e per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="52df6-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="52df6-160">**Nome installazione**: se l'installazione del gateway non è già selezionata, selezionare il gateway installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="52df6-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="52df6-161">Per aggiungere la risorsa del gateway al dashboard di Azure, scegliere **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="52df6-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="52df6-162">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="52df6-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="52df6-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="52df6-163">For example:</span></span>

    ![Fornire i dettagli per creare il gateway dati locale](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="52df6-165">Per trovare o visualizzare il gateway di dati in qualsiasi momento, dal menu principale di Azure a sinistra, passare ad **Altri servizi**>**Integrazione aziendale** > **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="52df6-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Passare ad "Altri servizi", "Integrazione aziendale", "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="52df6-167">3. Connettere l'app per la logica al gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="52df6-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="52df6-168">Ora che è stata creata la risorsa per il gateway dati ed è stata associata la sottoscrizione di Azure alla risorsa, creare una connessione tra l'app per la logica e il gateway dati.</span><span class="sxs-lookup"><span data-stu-id="52df6-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="52df6-169">Il percorso di connessione del gateway deve essere presente nella stessa area dell'app per la logica, ma è possibile usare un gateway dati esistente in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="52df6-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="52df6-170">Nel portale di Azure, creare o aprire l'app per la logica nella finestra di progettazione dell'App per la logica.</span><span class="sxs-lookup"><span data-stu-id="52df6-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="52df6-171">Aggiungere un connettore che supporta la connettività locale, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="52df6-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="52df6-172">Seguendo l'ordine indicato, selezionare **Connect via on-premises data gateway** (Esegui connessione tramite il gateway dati locale), fornire un nome di connessione univoco e le informazioni necessarie, quindi selezionare la risorsa del gateway dati da usare.</span><span class="sxs-lookup"><span data-stu-id="52df6-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="52df6-173">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="52df6-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="52df6-174">Un nome di connessione univoco consente di identificare facilmente la connessione in un secondo momento, soprattutto quando si creano più connessioni.</span><span class="sxs-lookup"><span data-stu-id="52df6-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="52df6-175">Se applicabile, è necessario includere anche il dominio completo per il proprio nome utente.</span><span class="sxs-lookup"><span data-stu-id="52df6-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![Creare una connessione tra l'app per la logica e il gateway dati](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="52df6-177">A questo punto, la connessione del gateway è pronta per l'app per la logica da usare.</span><span class="sxs-lookup"><span data-stu-id="52df6-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="52df6-178">Modificare le impostazioni di connessione del gateway</span><span class="sxs-lookup"><span data-stu-id="52df6-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="52df6-179">Dopo aver creato una connessione al gateway per l'app per la logica, è possibile voler procedere all'aggiornamento delle impostazioni in un secondo momento per quella connessione specifica.</span><span class="sxs-lookup"><span data-stu-id="52df6-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="52df6-180">Per trovare la connessione del gateway:</span><span class="sxs-lookup"><span data-stu-id="52df6-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="52df6-181">Nel pannello dell'app per la logica, sotto **Strumenti di sviluppo**, selezionare **Connessioni API**.</span><span class="sxs-lookup"><span data-stu-id="52df6-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="52df6-182">Il pannello **Connessioni API** mostra tutte le connessioni API associate alla propria app per la logica, incluse le connessioni del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Passare all'app per la logica, selezionare "Connessioni API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="52df6-184">In alternativa, dal menu principale di Azure a sinistra, passare ad **Altri servizi** > **Web e servizi mobili** > **Connessioni API** per tutte le connessioni API, comprese le connessioni del gateway, che sono associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="52df6-185">In alternativa, dal menu principale di Azure a sinistra, passare a **Tutte le risorse** per tutte le connessioni API, comprese le connessioni del gateway, che sono associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="52df6-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="52df6-186">Selezionare la connessione del gateway che si desidera visualizzare o modificare e scegliere **Modifica connessione API**.</span><span class="sxs-lookup"><span data-stu-id="52df6-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="52df6-187">Se gli aggiornamenti non hanno effetto, provare ad [arrestare e riavviare il servizio Windows del gateway](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="52df6-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="52df6-188">Cambiare o eliminare una risorsa gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="52df6-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="52df6-189">Per creare una risorsa del gateway diversa, associare il gateway a una risorsa diversa o rimuovere la risorsa per il gateway, è possibile eliminare la risorsa del gateway senza modificare l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52df6-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="52df6-190">Dal menu principale di Azure a sinistra, passare a **Tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="52df6-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="52df6-191">Individuare e selezionare la risorsa del gateway dati.</span><span class="sxs-lookup"><span data-stu-id="52df6-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="52df6-192">Scegliere **Gateway dati locale** e, sulla barra degli strumenti della risorse, scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="52df6-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="52df6-193">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="52df6-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="52df6-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52df6-194">Next steps</span></span>

* [<span data-ttu-id="52df6-195">Proteggere le app per la logica</span><span class="sxs-lookup"><span data-stu-id="52df6-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="52df6-196">Esempi e scenari comuni per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="52df6-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
