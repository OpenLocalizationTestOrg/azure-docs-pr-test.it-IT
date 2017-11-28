---
title: gateway di dati locale aaaInstall - App Azure per la logica | Documenti Microsoft
description: Prima di accedere a origini dati in locale, installare il gateway di dati hello locale per il trasferimento dei dati rapido e la crittografia tra origini dati in locale e la logica App
keywords: accesso ai dati, locale, trasferimento dei dati, crittografia, origini dei dati
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="3d9e7-104">Installare il gateway dati locale di hello per le app di logica di Azure</span><span class="sxs-lookup"><span data-stu-id="3d9e7-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="3d9e7-105">Prima di App per la logica può accedere a origini dati in locale, è necessario installare e configurare gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="3d9e7-106">gateway Hello funge da ponte che fornisce il trasferimento dei dati rapido e la crittografia tra i sistemi locali e le app di logica.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="3d9e7-107">gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="3d9e7-108">Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="3d9e7-109">Altre informazioni, vedere [funzionamento gateway dati hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="3d9e7-110">gateway Hello supporta le connessioni delle origini dati toothese in locale:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="3d9e7-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="3d9e7-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="3d9e7-112">DB2</span><span class="sxs-lookup"><span data-stu-id="3d9e7-112">DB2</span></span>  
*   <span data-ttu-id="3d9e7-113">File system</span><span class="sxs-lookup"><span data-stu-id="3d9e7-113">File System</span></span>
*   <span data-ttu-id="3d9e7-114">Informix</span><span class="sxs-lookup"><span data-stu-id="3d9e7-114">Informix</span></span>
*   <span data-ttu-id="3d9e7-115">MQ</span><span class="sxs-lookup"><span data-stu-id="3d9e7-115">MQ</span></span>
*   <span data-ttu-id="3d9e7-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="3d9e7-116">MySQL</span></span>
*   <span data-ttu-id="3d9e7-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="3d9e7-117">Oracle Database</span></span>
*   <span data-ttu-id="3d9e7-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3d9e7-118">PostgreSQL</span></span>
*   <span data-ttu-id="3d9e7-119">Server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="3d9e7-119">SAP Application Server</span></span> 
*   <span data-ttu-id="3d9e7-120">Server messaggi SAP</span><span class="sxs-lookup"><span data-stu-id="3d9e7-120">SAP Message Server</span></span>
*   <span data-ttu-id="3d9e7-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d9e7-121">SharePoint</span></span>
*   <span data-ttu-id="3d9e7-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3d9e7-122">SQL Server</span></span>
*   <span data-ttu-id="3d9e7-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="3d9e7-123">Teradata</span></span>

<span data-ttu-id="3d9e7-124">Questi passaggi mostrano come toofirst installazione hello sul gateway dati locale prima di [impostare una connessione tra gateway hello e App per la logica](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="3d9e7-125">Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="3d9e7-126">Per informazioni su come toouse hello gateway con altri servizi, vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="3d9e7-127">Gateway dati locale di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="3d9e7-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="3d9e7-128">Gateway dati locale di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="3d9e7-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="3d9e7-129">Gateway dati locale di Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="3d9e7-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="3d9e7-130">Gateway dati locale di Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="3d9e7-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="3d9e7-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="3d9e7-131">Requirements</span></span>

<span data-ttu-id="3d9e7-132">**Minimo**:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-132">**Minimum**:</span></span>

* <span data-ttu-id="3d9e7-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="3d9e7-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="3d9e7-134">Windows 7 versione a 64 bit o Windows Server 2008 R2 (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="3d9e7-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="3d9e7-135">**Consigliato**:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-135">**Recommended**:</span></span>

* <span data-ttu-id="3d9e7-136">8 CPU core</span><span class="sxs-lookup"><span data-stu-id="3d9e7-136">8 Core CPU</span></span>
* <span data-ttu-id="3d9e7-137">8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="3d9e7-137">8 GB Memory</span></span>
* <span data-ttu-id="3d9e7-138">Windows 2012 R2 versione a 64 bit (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="3d9e7-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="3d9e7-139">**Considerazioni importanti**:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-139">**Important considerations**:</span></span>

* <span data-ttu-id="3d9e7-140">Installare il gateway di dati locale hello solo in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="3d9e7-141">È possibile installare il gateway hello in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="3d9e7-142">Non si dispone di gateway hello tooinstall sul hello nello stesso computer dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="3d9e7-143">latenza toominimize, è possibile installare gateway hello più vicino come origine di dati possibili tooyour, o su hello stesso computer, presupponendo che si disponga di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="3d9e7-144">Non installare il gateway hello in un computer che consente di disattivare, passa alla toosleep o non connettersi toohello Internet perché non è possibile eseguire il gateway hello in tali circostanze.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="3d9e7-145">Le prestazioni del gateway possono anche diminuire su una rete wireless.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="3d9e7-146">Durante l'installazione, è necessario accedere con un [account aziendale o dell'istituto di istruzione](https://docs.microsoft.com/azure/active-directory/sign-up-organization) gestito da Azure Active Directory (Azure AD), non con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="3d9e7-147">Si dispone di toouse hello stesso lavoro o scuola account in un secondo momento in hello Azure portal quando si crea e associa una risorsa di gateway con l'installazione di gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="3d9e7-148">È quindi possibile selezionare la risorsa del gateway quando si crea la connessione hello tra la logica app e hello in origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="3d9e7-149">Perché è necessario usare un account di Azure AD aziendale o dell'istituto di istruzione?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="3d9e7-150">Se si è effettuata l'iscrizione a un'offerta di Office 365 senza fornire l'indirizzo di posta elettronica aziendale effettivo, l'indirizzo di accesso sarà simile a jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="3d9e7-151">Se si dispone di un gateway esistente impostato con un programma di installazione è precedente alla versione 14.16.6317.4, è possibile modificare la posizione del gateway dal programma di installazione più recente hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="3d9e7-152">Tuttavia, è possibile utilizzare hello tooset di programma di installazione più recente di un nuovo gateway con percorso hello che si desidera invece.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="3d9e7-153">Se si dispone di un programma di installazione di gateway è precedente alla versione 14.16.6317.4, ma non è stato installato il gateway, è possibile scaricare e usare hello programma di installazione più recente.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="3d9e7-154">Installare il gateway dati hello</span><span class="sxs-lookup"><span data-stu-id="3d9e7-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="3d9e7-155">[Scaricare ed eseguire il programma di installazione di hello gateway in un computer locale](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="3d9e7-156">Leggere e accettare i termini di hello di utilizzo e informativa sulla privacy.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="3d9e7-157">Specificare il percorso di hello sul computer locale in cui si desidera gateway hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="3d9e7-158">Quando richiesto, accedere con il proprio account aziendale o dell'istituzione di istruzione di Azure, non con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Accedere con l'account aziendale o dell'istituto di istruzione di Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="3d9e7-160">Registrare il gateway installato presso hello [servizio cloud gateway](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="3d9e7-161">Scegliere l'opzione che **consente di registrare un nuovo gateway in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="3d9e7-162">il servizio cloud gateway Hello crittografa e archivia le credenziali dell'origine dati e i dettagli del gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="3d9e7-163">servizio Hello indirizza anche le query e i relativi risultati tra le app per la logica, gateway dati locale di hello e l'origine dati in locale.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="3d9e7-164">Specificare un nome per l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="3d9e7-165">Creare una chiave di ripristino, quindi confermarla.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="3d9e7-166">La chiave di ripristino deve contenere almeno otto caratteri.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="3d9e7-167">Assicurarsi di salvare e conservare la chiave di hello in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="3d9e7-168">Questa chiave è necessaria inoltre quando si desidera toomigrate, ripristinare o acquisire la proprietà di un gateway esistente.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="3d9e7-169">area di toochange hello predefinita per il servizio cloud gateway hello e Bus di servizio di Azure utilizzati dall'installazione del gateway, scegliere **area Modifica**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Cambiare area](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="3d9e7-171">area predefinita Hello è area hello associata al tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="3d9e7-172">Nel riquadro successivo di hello, aprire hello **selezionare area** troppo scegliere un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Selezionare un'altra area](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="3d9e7-174">Ad esempio, si potrebbe selezionare hello app logica stessa area o hello selezionare area più vicina tooyour locale dati di origine in modo da ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="3d9e7-175">Le risorse gateway e l'app per la logica possono avere posizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="3d9e7-176">Dopo l'installazione non è possibile modificare questa area.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-176">You can't change this region after installation.</span></span> <span data-ttu-id="3d9e7-177">Determina inoltre quest'area e limita percorso hello in cui è possibile creare hello risorse di Azure per il gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="3d9e7-178">Pertanto, quando si crea la risorsa del gateway in Azure, verificare che percorso della risorsa hello corrisponda area hello selezionata durante l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="3d9e7-179">Se si desidera toouse un'area diversa per il gateway in un secondo momento, è necessario impostare di un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="3d9e7-180">Al termine, scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="3d9e7-181">Ora in cui è possibile, seguire la procedura hello Azure portal [creare una risorsa di Azure per il gateway](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="3d9e7-182">Altre informazioni, vedere [funzionamento gateway dati hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="3d9e7-183">Eseguire la migrazione, ripristinare o sostituire un gateway esistente</span><span class="sxs-lookup"><span data-stu-id="3d9e7-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="3d9e7-184">tooperform queste attività, è necessario disporre di chiave di ripristino hello che è stato specificato durante l'installazione di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="3d9e7-185">Dal menu di avvio del computer, scegliere **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="3d9e7-186">Dopo hello apre programma di installazione, eseguire l'accesso con hello stesso Azure di lavoro o scuola account precedentemente utilizzato gateway hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="3d9e7-187">Scegliere **Eseguire la migrazione, ripristinare o acquisire la proprietà di un gateway esistente**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="3d9e7-188">Specificare la chiave di ripristino e nome hello per gateway hello che si desidera eseguire, il ripristino o toomigrate sulla.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="3d9e7-189">Riavviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="3d9e7-189">Restart hello gateway</span></span>

<span data-ttu-id="3d9e7-190">gateway di Hello viene eseguito come servizio Windows.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="3d9e7-191">Come qualsiasi altro servizio di Windows, è possibile avviare e arrestare il servizio di hello in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="3d9e7-192">Ad esempio, puoi aprire un prompt dei comandi con autorizzazioni elevate in hello computer in cui è in esecuzione gateway hello ed eseguire entrambi questi comandi:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="3d9e7-193">servizio hello toostop, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="3d9e7-194">servizio hello toostart, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="3d9e7-195">Account del servizio Windows</span><span class="sxs-lookup"><span data-stu-id="3d9e7-195">Windows service account</span></span>

<span data-ttu-id="3d9e7-196">gateway dati locale di Hello impostato toouse `NT SERVICE\PBIEgwService` per Windows hello le credenziali di accesso del servizio.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="3d9e7-197">Per impostazione predefinita, il gateway hello ha diritto "Accesso come servizio" hello per macchina hello in cui si installa il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="3d9e7-198">Hello account del servizio Windows diverso dall'account hello utilizzato per la connessione a origini dati locali tooon e dal hello Azure lavoro o l'account dell'istituto di istruzione usato toosign in toocloud servizi.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="3d9e7-199">Configurare un firewall o proxy</span><span class="sxs-lookup"><span data-stu-id="3d9e7-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="3d9e7-200">gateway Hello crea una connessione in uscita troppo [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="3d9e7-201">informazioni sul proxy tooprovide per il gateway, vedere [configurare le impostazioni proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="3d9e7-202">toocheck se il firewall o proxy, potrebbe bloccare le connessioni, verificare se il computer può connettersi effettivamente toohello internet e hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="3d9e7-203">Da un prompt di PowerShell eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="3d9e7-204">Questo comando verifica solo la connettività di rete e connettività toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="3d9e7-205">Pertanto il comando hello non vengono eseguite toodo con gateway hello o un servizio cloud gateway di hello che crittografa e archivia le credenziali e i dettagli del gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="3d9e7-206">Questo comando è disponibile solo in Windows Server 2012 R2 o in una versione successiva e in Windows 8.1 o in una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="3d9e7-207">Nelle versioni precedenti del sistema operativo, è possibile utilizzare Telnet troppo testare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="3d9e7-208">Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="3d9e7-209">I risultati dovrebbero essere simili toothis esempio:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="3d9e7-210">Se **TcpTestSucceeded** non è stato impostato troppo**True**, potrebbe essere bloccato da un firewall.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="3d9e7-211">Se si desidera toobe completa, sostituire hello **ComputerName** e **porta** sotto i valori con valori di hello [configurare porte](#configure-ports) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="3d9e7-212">firewall Hello anche potrebbe bloccare le connessioni che hello che Azure Service Bus rende toohello Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="3d9e7-213">Se si verifica questo scenario, approvare (sbloccare) tutti gli indirizzi IP per i Data Center nell'area di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="3d9e7-214">Per tali indirizzi IP, [get hello Azure elenco di indirizzi IP qui](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="3d9e7-215">Configurare le porte</span><span class="sxs-lookup"><span data-stu-id="3d9e7-215">Configure ports</span></span>

<span data-ttu-id="3d9e7-216">gateway Hello crea una connessione in uscita troppo[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) e comunica su porte in uscita: TCP 443 (predefinita), 5671, 5672, 9350 a 9354.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="3d9e7-217">gateway Hello non richiede porte in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="3d9e7-218">Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="3d9e7-219">NOMI DI DOMINIO</span><span class="sxs-lookup"><span data-stu-id="3d9e7-219">DOMAIN NAMES</span></span> | <span data-ttu-id="3d9e7-220">PORTE IN USCITA</span><span class="sxs-lookup"><span data-stu-id="3d9e7-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="3d9e7-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3d9e7-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d9e7-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-222">*.analysis.windows.net</span></span> | <span data-ttu-id="3d9e7-223">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-223">443</span></span> | <span data-ttu-id="3d9e7-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3d9e7-224">HTTPS</span></span> | 
| <span data-ttu-id="3d9e7-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-225">*.login.windows.net</span></span> | <span data-ttu-id="3d9e7-226">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-226">443</span></span> | <span data-ttu-id="3d9e7-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3d9e7-227">HTTPS</span></span> | 
| <span data-ttu-id="3d9e7-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="3d9e7-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="3d9e7-229">5671-5672</span></span> | <span data-ttu-id="3d9e7-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="3d9e7-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="3d9e7-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="3d9e7-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="3d9e7-232">443, 9350-9354</span></span> | <span data-ttu-id="3d9e7-233">Listener in Inoltro del Bus di servizio su TCP (richiede 443 per l'acquisizione del token di Controllo di accesso)</span><span class="sxs-lookup"><span data-stu-id="3d9e7-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="3d9e7-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="3d9e7-235">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-235">443</span></span> | <span data-ttu-id="3d9e7-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3d9e7-236">HTTPS</span></span> | 
| <span data-ttu-id="3d9e7-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3d9e7-237">*.core.windows.net</span></span> | <span data-ttu-id="3d9e7-238">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-238">443</span></span> | <span data-ttu-id="3d9e7-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3d9e7-239">HTTPS</span></span> | 
| <span data-ttu-id="3d9e7-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3d9e7-240">login.microsoftonline.com</span></span> | <span data-ttu-id="3d9e7-241">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-241">443</span></span> | <span data-ttu-id="3d9e7-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3d9e7-242">HTTPS</span></span> | 
| <span data-ttu-id="3d9e7-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="3d9e7-243">*.msftncsi.com</span></span> | <span data-ttu-id="3d9e7-244">443</span><span class="sxs-lookup"><span data-stu-id="3d9e7-244">443</span></span> | <span data-ttu-id="3d9e7-245">Connettività internet tootest utilizzato hello gateway non è raggiungibile dal servizio Power BI hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="3d9e7-246">Se si dispone di indirizzi IP tooapprove anziché domini hello, è possibile scaricare e utilizzare hello [elenco di intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3d9e7-247">In alcuni casi, hello Azure Service Bus delle connessioni con indirizzo IP anziché nomi di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="3d9e7-248">Come funziona il gateway dati hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-248">How does hello data gateway work?</span></span>

<span data-ttu-id="3d9e7-249">gateway dati Hello facilita la comunicazione rapida e sicura tra l'app per la logica, il servizio cloud gateway hello e l'origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="3d9e7-251">Pertanto, quando utente hello nel cloud hello interagisce con un elemento che è connesso tooyour locale origine dati:</span><span class="sxs-lookup"><span data-stu-id="3d9e7-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="3d9e7-252">servizio cloud gateway di Hello crea una query, insieme alle credenziali crittografato hello per l'origine di dati, hello e invia hello query toohello coda tooprocess gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="3d9e7-253">il servizio cloud gateway Hello analizza query hello e inserisce toohello richiesta hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="3d9e7-254">gateway dati locale di Hello esegue il polling hello Azure Service Bus per le richieste in sospeso.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="3d9e7-255">gateway Hello Ottiene hello query, decrittografa le credenziali di hello e collega l'origine dati toohello con tali credenziali.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="3d9e7-256">gateway Hello invia hello query toohello origine per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="3d9e7-257">risultati di Hello vengono inviati dall'origine dati hello, toohello indietro gateway e il servizio cloud gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="3d9e7-258">Hello servizio cloud gateway Usa quindi i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="3d9e7-259">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3d9e7-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="3d9e7-260">Generale</span><span class="sxs-lookup"><span data-stu-id="3d9e7-260">General</span></span>

<span data-ttu-id="3d9e7-261">**Domande e**: è necessario un gateway per le origini dati nel cloud hello, ad esempio SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="3d9e7-262">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-262">
**A**: No.</span></span> <span data-ttu-id="3d9e7-263">Un gateway si connette a origini dati locali tooon solo.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="3d9e7-264">**Domande e**: gateway hello dispone toobe installato hello stesso computer come origine dati hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="3d9e7-265">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-265">
**A**: No.</span></span> <span data-ttu-id="3d9e7-266">gateway Hello stabilisce la connessione origine dati toohello utilizzando le informazioni di connessione hello fornito.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="3d9e7-267">Prendere in considerazione gateway hello come un'applicazione client in questo senso.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="3d9e7-268">gateway Hello sufficiente hello funzionalità tooconnect toohello nome del server che è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="3d9e7-269">**Domande e**: perché devo non è un lavoro di Azure o dell'istituto di istruzione toosign account in?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="3d9e7-270">
**Oggetto**: È possibile utilizzare un lavoro di Azure o scuola account quando si installa gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="3d9e7-271">L'account di accesso viene archiviato in un tenant gestito da Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d9e7-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3d9e7-272">Nome dell'entità utente dell'account di Azure AD (UPN) corrisponde in genere, indirizzo di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="3d9e7-273">**D**: Dove sono archiviate le credenziali?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="3d9e7-274">
**Oggetto**: credenziali hello immesse per un'origine dati vengono crittografate e archiviate nel servizio cloud gateway di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="3d9e7-275">le credenziali di Hello vengono decrittografate nel gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="3d9e7-276">**D**: Sono previsti requisiti per la larghezza di banda della rete?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="3d9e7-277">
**R**: È consigliabile che la connessione di rete abbia una buona velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="3d9e7-278">Ogni ambiente è diverso e quantità hello di invio di dati influisce sui risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="3d9e7-279">Uso di ExpressRoute può contribuire a tooguarantee un livello di velocità effettiva tra sedi locali e hello Data Center di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="3d9e7-280">È possibile utilizzare hello dello strumento di terze parti Azure Speed Test app toohelp misuratore la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="3d9e7-281">**Domande e**: che cos'è la latenza di hello per le query tooa dati di origine in esecuzione dal gateway hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="3d9e7-282">Che cos'è l'architettura migliore hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="3d9e7-283">
**Oggetto**: tooreduce latenza di rete, installare hello gateway come origine dati toohello Chiudi possibili.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="3d9e7-284">Se è possibile installare il gateway di hello sull'origine dati effettivi hello, la prossimità riduce la latenza di hello introdotta.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="3d9e7-285">Prendere in considerazione i Data Center hello troppo.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-285">Consider hello datacenters too.</span></span> <span data-ttu-id="3d9e7-286">Ad esempio, se il servizio utilizza hello Data Center di Stati Uniti occidentali e SQL Server è ospitato in una macchina virtuale di Azure, la macchina virtuale di Azure deve essere in Stati Uniti occidentali hello troppo.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="3d9e7-287">Questo prossimità riduce la latenza ed evitare addebiti in uscita sulla macchina virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="3d9e7-288">**Domande e**: come vengono inviati risultati toohello indietro cloud?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="3d9e7-289">
**Oggetto**: risultati vengono inviati tramite hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="3d9e7-290">**Domande e**: sono presenti eventuali gateway toohello le connessioni in ingresso dal cloud hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="3d9e7-291">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-291">
**A**: No.</span></span> <span data-ttu-id="3d9e7-292">gateway di Hello Usa le connessioni in uscita tooAzure Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="3d9e7-293">**D**: Cosa accade se si bloccano le connessioni in uscita?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="3d9e7-294">Cosa devo tooopen?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="3d9e7-295">
**Oggetto**: Vedere porte hello e gli host che hello Usa gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="3d9e7-296">**Domande e**: ciò che viene chiamato il servizio Windows effettivo di hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="3d9e7-297">
**Oggetto**: In servizi, il gateway di hello è chiamato servizio Power BI Enterprise Gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="3d9e7-298">**Domande e**: possibile hello servizio gateway di Windows eseguito con un account Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="3d9e7-299">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-299">
**A**: No.</span></span> <span data-ttu-id="3d9e7-300">servizio Windows Hello deve avere un account Windows valido.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="3d9e7-301">Per impostazione predefinita, il servizio di hello viene eseguito con hello SID del servizio, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="3d9e7-302">Disponibilità elevata e ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="3d9e7-302">High availability and disaster recovery</span></span>

<span data-ttu-id="3d9e7-303">**D**: Quali opzioni sono disponibili per il ripristino di emergenza?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="3d9e7-304">
**Oggetto**: È possibile utilizzare toorestore chiave di ripristino hello o spostare un gateway.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="3d9e7-305">Quando si installa il gateway di hello, specificare la chiave di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="3d9e7-306">**Domande e**: che cos'è il vantaggio di hello della chiave di ripristino hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="3d9e7-307">
**Oggetto**: chiave di ripristino hello fornisce un modo toomigrate o ripristinare le impostazioni del gateway dopo un'emergenza.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="3d9e7-308">**Domande e**: sono disponibili piani per l'abilitazione di scenari a disponibilità elevata con gateway hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="3d9e7-309">
**Oggetto**: questi scenari sono roadmap hello, ma è ancora non dispone di una sequenza temporale.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3d9e7-310">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3d9e7-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="3d9e7-311">**Domande e**: come è possibile vedere quali sono le query vengono inviate toohello origine di dati locale?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="3d9e7-312">
**Oggetto**: È possibile abilitare la traccia di query, che include le query hello che vengono inviate.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="3d9e7-313">Tenere presente che query toochange risalendo toohello valore originale al termine della risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="3d9e7-314">Se il tracciamento delle query non viene disabilitato, si creeranno dei log più grandi.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="3d9e7-315">È anche possibile usare gli strumenti per il tracciamento delle query di cui è dotata l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="3d9e7-316">Ad esempio, è possibile usare Eventi estesi o SQL Profiler per SQL Server e Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="3d9e7-317">**Domande e**: dove sono i registri di gateway hello?</span><span class="sxs-lookup"><span data-stu-id="3d9e7-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="3d9e7-318">
**R**: Vedere la sezione Strumenti più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="3d9e7-319">Aggiornare la versione più recente di toohello</span><span class="sxs-lookup"><span data-stu-id="3d9e7-319">Update toohello latest version</span></span>

<span data-ttu-id="3d9e7-320">Molti problemi possono verificarsi quando la versione di gateway hello diventa obsoleta.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="3d9e7-321">Come buona pratica, assicurarsi di utilizzare la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="3d9e7-322">Se è stato aggiornato gateway hello per un mese o più, si potrebbe si consiglia di installare una versione più recente di hello del gateway hello e verificare se è possibile riprodurre il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="3d9e7-323">Errore: Impossibile tooadd utente toogroup.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="3d9e7-324">(Utenti log delle prestazioni -2147463168 PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="3d9e7-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="3d9e7-325">È possibile che venga visualizzato questo errore se si tenta di gateway di hello tooinstall in un controller di dominio che non è supportato.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="3d9e7-326">Assicurarsi di distribuire gateway hello in un computer che non è un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="3d9e7-327">Strumenti</span><span class="sxs-lookup"><span data-stu-id="3d9e7-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="3d9e7-328">Raccogliere registri da configurer gateway hello</span><span class="sxs-lookup"><span data-stu-id="3d9e7-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="3d9e7-329">È possibile raccogliere i log per il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="3d9e7-330">Iniziare sempre con i registri di hello!</span><span class="sxs-lookup"><span data-stu-id="3d9e7-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="3d9e7-331">Log dei programmi di installazione</span><span class="sxs-lookup"><span data-stu-id="3d9e7-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="3d9e7-332">Log di configurazione</span><span class="sxs-lookup"><span data-stu-id="3d9e7-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="3d9e7-333">Log del servizio gateway Enterprise</span><span class="sxs-lookup"><span data-stu-id="3d9e7-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="3d9e7-334">Log eventi</span><span class="sxs-lookup"><span data-stu-id="3d9e7-334">Event logs</span></span>

<span data-ttu-id="3d9e7-335">È possibile trovare il Gateway di gestione di dati e PowerBIGateway registri in hello **registri applicazioni e servizi**.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="3d9e7-336">Fiddler Trace</span><span class="sxs-lookup"><span data-stu-id="3d9e7-336">Fiddler Trace</span></span>

<span data-ttu-id="3d9e7-337">[Fiddler](http://www.telerik.com/fiddler) è uno strumento gratuito di Telerik che consente di monitorare il traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="3d9e7-338">È possibile visualizzare il traffico con il servizio Power BI da computer client hello hello.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="3d9e7-339">Questo servizio consente di visualizzare errori e altre informazioni correlate.</span><span class="sxs-lookup"><span data-stu-id="3d9e7-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d9e7-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d9e7-340">Next steps</span></span>
    
* [<span data-ttu-id="3d9e7-341">Connessione dati tooon locale da App per la logica</span><span class="sxs-lookup"><span data-stu-id="3d9e7-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="3d9e7-342">Funzionalità di Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="3d9e7-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="3d9e7-343">Connettori per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="3d9e7-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
