---
title: origini dei dati in locale per le app di Azure logica aaaAccess | Documenti Microsoft
description: Configurare gateway dati locale di hello per accedere a origini dati in locale da App per la logica
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
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="ecc54-104">Accedere alle origini dati in locale da app logica con gateway dati locale di hello</span><span class="sxs-lookup"><span data-stu-id="ecc54-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="ecc54-105">origini dati tooaccess in locale da App per la logica, impostare da un gateway dati locale che App per la logica è possibile utilizzare con i connettori supportati.</span><span class="sxs-lookup"><span data-stu-id="ecc54-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="ecc54-106">gateway Hello funge da ponte che fornisce il trasferimento dei dati rapido e la crittografia tra origini dati in locale e App per la logica.</span><span class="sxs-lookup"><span data-stu-id="ecc54-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="ecc54-107">gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ecc54-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="ecc54-108">Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="ecc54-109">Altre informazioni, vedere [funzionamento gateway dati hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="ecc54-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="ecc54-110">gateway Hello supporta le connessioni delle origini dati toothese in locale:</span><span class="sxs-lookup"><span data-stu-id="ecc54-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="ecc54-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="ecc54-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="ecc54-112">DB2</span><span class="sxs-lookup"><span data-stu-id="ecc54-112">DB2</span></span>  
*   <span data-ttu-id="ecc54-113">File system</span><span class="sxs-lookup"><span data-stu-id="ecc54-113">File System</span></span>
*   <span data-ttu-id="ecc54-114">Informix</span><span class="sxs-lookup"><span data-stu-id="ecc54-114">Informix</span></span>
*   <span data-ttu-id="ecc54-115">MQ</span><span class="sxs-lookup"><span data-stu-id="ecc54-115">MQ</span></span>
*   <span data-ttu-id="ecc54-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="ecc54-116">MySQL</span></span>
*   <span data-ttu-id="ecc54-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="ecc54-117">Oracle Database</span></span>
*   <span data-ttu-id="ecc54-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ecc54-118">PostgreSQL</span></span>
*   <span data-ttu-id="ecc54-119">Server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="ecc54-119">SAP Application Server</span></span> 
*   <span data-ttu-id="ecc54-120">Server messaggi SAP</span><span class="sxs-lookup"><span data-stu-id="ecc54-120">SAP Message Server</span></span>
*   <span data-ttu-id="ecc54-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ecc54-121">SharePoint</span></span>
*   <span data-ttu-id="ecc54-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ecc54-122">SQL Server</span></span>
*   <span data-ttu-id="ecc54-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="ecc54-123">Teradata</span></span>

<span data-ttu-id="ecc54-124">Questi passaggi mostrano come tooset backup hello locale toowork gateway dati con le applicazioni di logica.</span><span class="sxs-lookup"><span data-stu-id="ecc54-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="ecc54-125">Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ecc54-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="ecc54-126">Per informazioni su come toouse hello gateway con altri servizi, vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="ecc54-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="ecc54-127">Gateway dati locale di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="ecc54-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="ecc54-128">Gateway dati locale di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ecc54-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="ecc54-129">Gateway dati locale di Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="ecc54-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="ecc54-130">Gateway dati locale di Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="ecc54-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="ecc54-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ecc54-131">Requirements</span></span>

* <span data-ttu-id="ecc54-132">È necessario disporre già [installato gateway dati hello in un computer locale](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="ecc54-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="ecc54-133">Quando si accede toohello portale di Azure, si dispone di toouse hello stesso lavoro o scuola account che è stata usata troppo[installare il gateway dati locale di hello](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="ecc54-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="ecc54-134">L'account di accesso deve inoltre avere toouse una sottoscrizione di Azure quando si crea una risorsa per il gateway in hello portale di Azure per l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc54-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="ecc54-135">L'installazione del gateway non può essere già richiesta da una risorsa del gateway di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc54-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="ecc54-136">È possibile associare la risorsa di Azure gateway un gateway installazione tooonly.</span><span class="sxs-lookup"><span data-stu-id="ecc54-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="ecc54-137">Attestazione si verifica quando si crea risorsa gateway hello in modo che l'installazione di hello non è disponibile per le altre risorse.</span><span class="sxs-lookup"><span data-stu-id="ecc54-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="ecc54-138">Impostare la connessione del gateway dati hello</span><span class="sxs-lookup"><span data-stu-id="ecc54-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="ecc54-139">1. Installare il gateway dati locale di hello</span><span class="sxs-lookup"><span data-stu-id="ecc54-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="ecc54-140">Se hai già fatto, seguire hello [il gateway dati locale di passaggi tooinstall hello](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="ecc54-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="ecc54-141">Prima di continuare con hello altri passaggi, assicurarsi che il gateway dati di hello è stato installato in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="ecc54-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="ecc54-142">2. Creare una risorsa di Azure per il gateway dati locale di hello</span><span class="sxs-lookup"><span data-stu-id="ecc54-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="ecc54-143">Dopo aver installato il gateway hello in un computer locale, è necessario creare il gateway dati come risorsa in Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc54-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="ecc54-144">Questo passaggio associa anche la risorsa di gateway con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc54-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="ecc54-145">Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="ecc54-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="ecc54-146">Assicurarsi che toouse hello stesso lavoro di Azure o l'indirizzo e-mail dell'istituto di istruzione usato gateway hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="ecc54-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="ecc54-147">Nel menu a sinistra di hello in Azure, scegliere **New** > **Enterprise Integration** > **gateway dati locale** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ecc54-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Trovare "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="ecc54-149">In hello **crea gateway di connessione** pannello fornire toocreate questi dettagli della risorsa del gateway dati:</span><span class="sxs-lookup"><span data-stu-id="ecc54-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="ecc54-150">**Nome**: inserire un nome per la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc54-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="ecc54-151">**Sottoscrizione**: selezionare hello tooassociate sottoscrizione di Azure alla risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc54-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="ecc54-152">La sottoscrizione deve essere hello app logica stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ecc54-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="ecc54-153">sottoscrizione predefinita Hello è basata su account di Azure utilizzato toosign in hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="ecc54-154">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente per distribuire la risorsa del gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc54-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="ecc54-155">I gruppi di risorse consentono di gestire gli asset di Azure correlati come una raccolta.</span><span class="sxs-lookup"><span data-stu-id="ecc54-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="ecc54-156">**Percorso**: Azure limita questo toohello percorso stessa area che è stato selezionato per il servizio cloud gateway di hello durante [dell'installazione del gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="ecc54-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="ecc54-157">Verificare che il percorso di risorsa gateway hello corrisponda posizione del servizio cloud gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="ecc54-158">In caso contrario, l'installazione del gateway potrebbe non essere nell'elenco a gateway installato hello è tooselect nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="ecc54-159">È possibile usare aree diverse per la risorsa del gateway e per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ecc54-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="ecc54-160">**Nome di installazione**: se l'installazione del gateway non è già selezionata, selezionare il gateway hello installata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ecc54-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="ecc54-161">tooadd hello gateway risorsa tooyour dashboard di Azure, scegliere **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="ecc54-162">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="ecc54-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ecc54-163">For example:</span></span>

    ![Fornire dettagli toocreate gateway dati locale](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="ecc54-165">toofind o vista il gateway dati in qualsiasi momento, hello Azure sinistro menu principale, andare troppo **più servizi** > **Enterprise Integration** > **dati locali Gateway**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Andare troppo "Più servizi", "Integrazione di Enterprise", "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="ecc54-167">3. Connettere il gateway dati locale di logica app toohello</span><span class="sxs-lookup"><span data-stu-id="ecc54-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="ecc54-168">Dopo aver creato la risorsa del gateway dati e associati alla sottoscrizione di Azure alla risorsa, creare una connessione tra il gateway dati logica app e hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc54-169">Il percorso di connessione del gateway deve essere presente in hello stessa area dell'app logica, ma è possibile utilizzare un gateway dati esistente in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="ecc54-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="ecc54-170">In hello portale di Azure, creare o aprire l'app logica nella finestra di progettazione logica App.</span><span class="sxs-lookup"><span data-stu-id="ecc54-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="ecc54-171">Aggiungere un connettore che supporta la connettività locale, ad esempio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecc54-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="ecc54-172">Selezionare lo stesso ordine hello illustrato, **Connetti tramite il gateway dati locale**, fornire un nome univoco della connessione hello le informazioni necessarie e selezionare una risorsa per il gateway dati hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="ecc54-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="ecc54-173">Al termine dell'operazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="ecc54-174">Un nome di connessione univoco consente di identificare facilmente la connessione in un secondo momento, soprattutto quando si creano più connessioni.</span><span class="sxs-lookup"><span data-stu-id="ecc54-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="ecc54-175">Se applicabile, è necessario includere anche dominio hello per il proprio nome utente.</span><span class="sxs-lookup"><span data-stu-id="ecc54-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Creare una connessione tra l'app per la logica e il gateway dati](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="ecc54-177">Complimenti, la connessione del gateway è pronta per il toouse app logica.</span><span class="sxs-lookup"><span data-stu-id="ecc54-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="ecc54-178">Modificare le impostazioni di connessione del gateway</span><span class="sxs-lookup"><span data-stu-id="ecc54-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="ecc54-179">Dopo aver creato una connessione gateway per l'app logica, è le impostazioni di hello aggiornamento toolater per tale connessione specifico.</span><span class="sxs-lookup"><span data-stu-id="ecc54-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="ecc54-180">connessione al gateway toofind hello:</span><span class="sxs-lookup"><span data-stu-id="ecc54-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="ecc54-181">Nel pannello app logica hello in **gli strumenti di sviluppo**selezionare **connessioni API**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="ecc54-182">Hello **connessioni API** riquadro vengono visualizzate tutte le connessioni delle API associate all'app di logica, incluse le connessioni di gateway.</span><span class="sxs-lookup"><span data-stu-id="ecc54-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Passare tooyour logica app, selezionare "Connessioni API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="ecc54-184">O, hello Azure sinistro menu principale, andare troppo **più servizi** > **Web e servizi mobili** > **connessioni API** per tutte le connessioni di API, tra cui le connessioni gateway, che sono associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc54-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="ecc54-185">In alternativa, hello Azure sinistro menu principale, accedere troppo**tutte le risorse** per tutte le connessioni di API, comprese le connessioni di gateway, che sono associate alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc54-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="ecc54-186">Selezionare una connessione al gateway hello che desidera tooview o modificare e scegliere **connessione modificare API**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="ecc54-187">Se gli aggiornamenti non avrà effetto, provare a [arrestare e riavviare il servizio di Windows gateway hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="ecc54-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="ecc54-188">Cambiare o eliminare una risorsa gateway dati locale</span><span class="sxs-lookup"><span data-stu-id="ecc54-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="ecc54-189">associare il gateway a una risorsa diversa toocreate una risorsa, gateway diverso o rimuovere risorse gateway hello, è possibile eliminare una risorsa per il gateway hello senza influire sull'installazione del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ecc54-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="ecc54-190">Hello Azure sinistro menu principale, andare troppo**tutte le risorse**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="ecc54-191">Individuare e selezionare la risorsa del gateway dati.</span><span class="sxs-lookup"><span data-stu-id="ecc54-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="ecc54-192">Scegliere **Gateway dati locale**, sulla barra degli strumenti risorse hello, scegliere **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="ecc54-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="ecc54-193">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ecc54-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="ecc54-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ecc54-194">Next steps</span></span>

* [<span data-ttu-id="ecc54-195">Proteggere le app per la logica</span><span class="sxs-lookup"><span data-stu-id="ecc54-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="ecc54-196">Esempi e scenari comuni per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="ecc54-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
