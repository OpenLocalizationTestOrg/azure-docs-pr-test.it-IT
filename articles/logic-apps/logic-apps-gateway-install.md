---
title: Installare il gateway dati locale - App per la logica di Azure | Microsoft Docs
description: Prima di accedere alle origini dei dati in locale, installare il gateway di dati locale per il trasferimento rapido dei dati e la crittografia tra le origini dati locale e le app per la logica
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
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="7e9e5-104">Installare il gateway dati locale per le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="7e9e5-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="7e9e5-105">Prima che le app per la logica possano accedere alle origini di dati in locale, è necessario installare e configurare il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="7e9e5-106">Il gateway funge da ponte che fornisce il trasferimento rapido dei dati e la crittografia tra sistemi locali e le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="7e9e5-107">Il gateway inoltra i dati da origini locali sui canali crittografati tramite il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="7e9e5-108">Tutto il traffico ha origine come traffico sicuro in uscita dall'agente di gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="7e9e5-109">Altre informazioni sul [funzionamento del gateway dati](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="7e9e5-110">Il gateway supporta le connessioni alle origine dati locali seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="7e9e5-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="7e9e5-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="7e9e5-112">DB2</span><span class="sxs-lookup"><span data-stu-id="7e9e5-112">DB2</span></span>  
*   <span data-ttu-id="7e9e5-113">File system</span><span class="sxs-lookup"><span data-stu-id="7e9e5-113">File System</span></span>
*   <span data-ttu-id="7e9e5-114">Informix</span><span class="sxs-lookup"><span data-stu-id="7e9e5-114">Informix</span></span>
*   <span data-ttu-id="7e9e5-115">MQ</span><span class="sxs-lookup"><span data-stu-id="7e9e5-115">MQ</span></span>
*   <span data-ttu-id="7e9e5-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="7e9e5-116">MySQL</span></span>
*   <span data-ttu-id="7e9e5-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="7e9e5-117">Oracle Database</span></span>
*   <span data-ttu-id="7e9e5-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7e9e5-118">PostgreSQL</span></span>
*   <span data-ttu-id="7e9e5-119">Server applicazioni SAP</span><span class="sxs-lookup"><span data-stu-id="7e9e5-119">SAP Application Server</span></span> 
*   <span data-ttu-id="7e9e5-120">Server messaggi SAP</span><span class="sxs-lookup"><span data-stu-id="7e9e5-120">SAP Message Server</span></span>
*   <span data-ttu-id="7e9e5-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="7e9e5-121">SharePoint</span></span>
*   <span data-ttu-id="7e9e5-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7e9e5-122">SQL Server</span></span>
*   <span data-ttu-id="7e9e5-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="7e9e5-123">Teradata</span></span>

<span data-ttu-id="7e9e5-124">Questa procedura mostra come installare il gateway dati locale prima di [impostare una connessione tra il gateway e le app per la logica](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="7e9e5-125">Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="7e9e5-126">Per informazioni su come usare il gateway con altri servizi, vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="7e9e5-127">Gateway dati locale di Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="7e9e5-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="7e9e5-128">Gateway dati locale di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7e9e5-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="7e9e5-129">Gateway dati locale di Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="7e9e5-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="7e9e5-130">Gateway dati locale di Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="7e9e5-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="7e9e5-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="7e9e5-131">Requirements</span></span>

<span data-ttu-id="7e9e5-132">**Minimo**:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-132">**Minimum**:</span></span>

* <span data-ttu-id="7e9e5-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7e9e5-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="7e9e5-134">Windows 7 versione a 64 bit o Windows Server 2008 R2 (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="7e9e5-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="7e9e5-135">**Consigliato**:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-135">**Recommended**:</span></span>

* <span data-ttu-id="7e9e5-136">8 CPU core</span><span class="sxs-lookup"><span data-stu-id="7e9e5-136">8 Core CPU</span></span>
* <span data-ttu-id="7e9e5-137">8 GB di memoria</span><span class="sxs-lookup"><span data-stu-id="7e9e5-137">8 GB Memory</span></span>
* <span data-ttu-id="7e9e5-138">Windows 2012 R2 versione a 64 bit (o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="7e9e5-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="7e9e5-139">**Considerazioni importanti**:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-139">**Important considerations**:</span></span>

* <span data-ttu-id="7e9e5-140">Installare il gateway dati locale solo su un computer locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="7e9e5-141">Non è possibile installare il gateway in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="7e9e5-142">Non è necessario installare il gateway nello stesso computer dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="7e9e5-143">Per ridurre al minimo la latenza, è possibile installare il gateway il più vicino possibile all'origine dati o nello stesso computer, presupponendo che si disponga delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="7e9e5-144">Non installare il gateway su un computer che si disattiva o che non può connettersi a Internet perché il gateway non può essere eseguito in tali circostanze.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="7e9e5-145">Le prestazioni del gateway possono anche diminuire su una rete wireless.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="7e9e5-146">Durante l'installazione, è necessario accedere con un [account aziendale o dell'istituto di istruzione](https://docs.microsoft.com/azure/active-directory/sign-up-organization) gestito da Azure Active Directory (Azure AD), non con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="7e9e5-147">È necessario usare successivamente lo stesso account aziendale o dell'istituto di istruzione nel portale di Azure quando si crea e si associa una risorsa di gateway all'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="7e9e5-148">Si seleziona quindi la risorsa del gateway quando si crea la connessione tra l'app per la logica e l'origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="7e9e5-149">Perché è necessario usare un account di Azure AD aziendale o dell'istituto di istruzione?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="7e9e5-150">Se si è effettuata l'iscrizione a un'offerta di Office 365 senza fornire l'indirizzo di posta elettronica aziendale effettivo, l'indirizzo di accesso sarà simile a jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="7e9e5-151">Se si dispone di un gateway esistente impostato con un programma di installazione che è precedente alla versione 14.16.6317.4, non è possibile modificare il percorso del gateway eseguendo il programma di installazione più recente.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="7e9e5-152">Tuttavia, è possibile usare il programma di installazione più recente per configurare un nuovo gateway con il percorso che si desidera.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="7e9e5-153">Se si dispone di un programma di installazione di gateway che è precedente alla versione 14.16.6317.4, ma non è ancora stato installato il gateway, è possibile scaricare e usare il programma di installazione più recente.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="7e9e5-154">Installare il gateway dati</span><span class="sxs-lookup"><span data-stu-id="7e9e5-154">Install the data gateway</span></span>

1.  <span data-ttu-id="7e9e5-155">[Scaricare ed eseguire il programma di installazione di gateway in un computer locale](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="7e9e5-156">Leggere e accettare le condizioni per l'utilizzo e l'informativa sulla privacy.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="7e9e5-157">Specificare il percorso nel computer locale in cui si desidera installare il gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="7e9e5-158">Quando richiesto, accedere con il proprio account aziendale o dell'istituzione di istruzione di Azure, non con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Accedere con l'account aziendale o dell'istituto di istruzione di Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="7e9e5-160">Ora registrare il gateway installato con il [servizio cloud gateway](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="7e9e5-161">Scegliere l'opzione che **consente di registrare un nuovo gateway in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="7e9e5-162">Il servizio cloud gateway crittografa e archivia le credenziali dell'origine dati e i dettagli del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="7e9e5-163">Il servizio instrada anche le query e i relativi risultati tra l'app per la logica, il gateway dati locale e l'origine dati in locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="7e9e5-164">Specificare un nome per l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="7e9e5-165">Creare una chiave di ripristino, quindi confermarla.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="7e9e5-166">La chiave di ripristino deve contenere almeno otto caratteri.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="7e9e5-167">Assicurarsi di salvare e conservare la chiave in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="7e9e5-168">Questa chiave è necessaria anche per eseguire la migrazione, ripristinare o acquisire la proprietà di un gateway esistente.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="7e9e5-169">Per modificare l'area predefinita per il servizio cloud gateway e per il bus di servizio di Azure usato per l'installazione del gateway, scegliere **Cambia area**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Cambiare area](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="7e9e5-171">L'area predefinita è l'area associata al tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="7e9e5-172">Nel riquadro successivo aprire **Selezionare l'area** per scegliere un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Selezionare un'altra area](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="7e9e5-174">Si potrebbe ad esempio selezionare la stessa area come app per la logica o selezionare l'area più vicina all'origine dati in locale in modo da ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="7e9e5-175">Le risorse gateway e l'app per la logica possono avere posizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="7e9e5-176">Dopo l'installazione non è possibile modificare questa area.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-176">You can't change this region after installation.</span></span> <span data-ttu-id="7e9e5-177">L'area determina e limita anche la posizione in cui è possibile creare la risorsa di Azure per il gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="7e9e5-178">Pertanto, quando si crea la risorsa del gateway in Azure, assicurarsi che il percorso della risorsa corrisponda all'area selezionata durante l'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="7e9e5-179">Se si desidera usare un'area diversa per il gateway in un secondo momento, è necessario configurare un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="7e9e5-180">Al termine, scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="7e9e5-181">Seguire ora la procedura seguente nel portale di Azure per [creare una risorsa di Azure per il gateway](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="7e9e5-182">Altre informazioni sul [funzionamento del gateway dati](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="7e9e5-183">Eseguire la migrazione, ripristinare o sostituire un gateway esistente</span><span class="sxs-lookup"><span data-stu-id="7e9e5-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="7e9e5-184">Per eseguire queste attività, è necessario disporre della chiave di ripristino che è stata specificata all'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="7e9e5-185">Dal menu di avvio del computer, scegliere **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="7e9e5-186">Quando viene aperto il programma di installazione accedere con lo stesso account di Azure aziendale o dell'istituto di istruzione usato in precedenza per installare il gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="7e9e5-187">Scegliere **Eseguire la migrazione, ripristinare o acquisire la proprietà di un gateway esistente**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="7e9e5-188">Specificare la chiave di ripristino per il gateway di cui si vuole eseguire la migrazione o il ripristino o acquisire la proprietà.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="7e9e5-189">Riavviare il gateway</span><span class="sxs-lookup"><span data-stu-id="7e9e5-189">Restart the gateway</span></span>

<span data-ttu-id="7e9e5-190">Il gateway viene eseguito come un servizio Windows.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="7e9e5-191">Come qualsiasi altro servizio Windows, può essere avviato e arrestato in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="7e9e5-192">Ad esempio, è possibile aprire un prompt dei comandi con autorizzazioni elevate nel computer in cui è in esecuzione il gateway e quindi eseguire uno dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="7e9e5-193">Per arrestare il servizio, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="7e9e5-194">Per avviare il servizio, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="7e9e5-195">Account del servizio Windows</span><span class="sxs-lookup"><span data-stu-id="7e9e5-195">Windows service account</span></span>

<span data-ttu-id="7e9e5-196">Il gateway dati locale è configurato per usare `NT SERVICE\PBIEgwService` come credenziale di accesso al servizio Windows.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="7e9e5-197">Per impostazione predefinita, il gateway ha il diritto di "Accesso come servizio", per il computer in cui si installa il gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="7e9e5-198">Questo account del servizio Windows è diverso dall'account usato per la connessione a origini dati locali e dall'account di Azure aziendale o dell'istituto di istruzione usato per accedere ai servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="7e9e5-199">Configurare un firewall o proxy</span><span class="sxs-lookup"><span data-stu-id="7e9e5-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="7e9e5-200">Il gateway crea una connessione in uscita al [bus di servizio di Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="7e9e5-201">Per fornire al gateway informazioni sul proxy, vedere [Configurazione delle impostazioni proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="7e9e5-202">Per verificare se il firewall, o proxy, potrebbe bloccare le connessioni, verificare che il computer riesca effettivamente a connettersi a Internet e al [bus di servizio di Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="7e9e5-203">Da un prompt di PowerShell eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="7e9e5-204">Questo comando verifica solo la connettività di rete e la connettività per il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="7e9e5-205">Pertanto, il comando non ha nulla a che fare con il gateway o con il servizio cloud del gateway che crittografa e archivia le credenziali e i dettagli di gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="7e9e5-206">Questo comando è disponibile solo in Windows Server 2012 R2 o in una versione successiva e in Windows 8.1 o in una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="7e9e5-207">Nelle versioni precedenti del sistema operativo, è possibile usare Telnet per testare la connettività.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="7e9e5-208">Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="7e9e5-209">I risultati dovrebbero essere simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-209">Your results should look similar to this example:</span></span>

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

<span data-ttu-id="7e9e5-210">Se **TcpTestSucceeded** non è impostato su **True**, il firewall potrebbe essere la causa del blocco.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="7e9e5-211">Per la massima completezza sostituire i valori **ComputerName** e **Porta** con quelli elencati in [Configurare le porte](#configure-ports) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="7e9e5-212">Il firewall può anche bloccare le connessioni tra il bus di servizio e i data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="7e9e5-213">Se si verifica questo scenario, approvare (sbloccare) tutti gli indirizzi IP per i data center nell'area geografica.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="7e9e5-214">Per gli indirizzi IP, [ottenere l'elenco di indirizzi IP Azure qui](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="7e9e5-215">Configurare le porte</span><span class="sxs-lookup"><span data-stu-id="7e9e5-215">Configure ports</span></span>

<span data-ttu-id="7e9e5-216">Il gateway crea una connessione in uscita al [Bus di servizio di Azure](https://azure.microsoft.com/services/service-bus/) e comunica sulle porte in uscita: TCP 443 (predefinita), 5671, 5672, 9350 attraverso 9354.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="7e9e5-217">Non sono richieste porte in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="7e9e5-218">Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="7e9e5-219">NOMI DI DOMINIO</span><span class="sxs-lookup"><span data-stu-id="7e9e5-219">DOMAIN NAMES</span></span> | <span data-ttu-id="7e9e5-220">PORTE IN USCITA</span><span class="sxs-lookup"><span data-stu-id="7e9e5-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="7e9e5-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7e9e5-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7e9e5-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-222">*.analysis.windows.net</span></span> | <span data-ttu-id="7e9e5-223">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-223">443</span></span> | <span data-ttu-id="7e9e5-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7e9e5-224">HTTPS</span></span> | 
| <span data-ttu-id="7e9e5-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-225">*.login.windows.net</span></span> | <span data-ttu-id="7e9e5-226">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-226">443</span></span> | <span data-ttu-id="7e9e5-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7e9e5-227">HTTPS</span></span> | 
| <span data-ttu-id="7e9e5-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="7e9e5-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="7e9e5-229">5671-5672</span></span> | <span data-ttu-id="7e9e5-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="7e9e5-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="7e9e5-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="7e9e5-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="7e9e5-232">443, 9350-9354</span></span> | <span data-ttu-id="7e9e5-233">Listener in Inoltro del Bus di servizio su TCP (richiede 443 per l'acquisizione del token di Controllo di accesso)</span><span class="sxs-lookup"><span data-stu-id="7e9e5-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="7e9e5-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="7e9e5-235">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-235">443</span></span> | <span data-ttu-id="7e9e5-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7e9e5-236">HTTPS</span></span> | 
| <span data-ttu-id="7e9e5-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e9e5-237">*.core.windows.net</span></span> | <span data-ttu-id="7e9e5-238">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-238">443</span></span> | <span data-ttu-id="7e9e5-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7e9e5-239">HTTPS</span></span> | 
| <span data-ttu-id="7e9e5-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7e9e5-240">login.microsoftonline.com</span></span> | <span data-ttu-id="7e9e5-241">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-241">443</span></span> | <span data-ttu-id="7e9e5-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7e9e5-242">HTTPS</span></span> | 
| <span data-ttu-id="7e9e5-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="7e9e5-243">*.msftncsi.com</span></span> | <span data-ttu-id="7e9e5-244">443</span><span class="sxs-lookup"><span data-stu-id="7e9e5-244">443</span></span> | <span data-ttu-id="7e9e5-245">Usato per testare la connettività a Internet se il gateway non è raggiungibile dal servizio Power BI.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="7e9e5-246">Se è necessario approvare gli indirizzi IP anziché i domini, è possibile scaricare e usare l'[elenco di intervalli IP dei data center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="7e9e5-247">In alcuni casi, le connessioni al Bus di servizio di Azure verranno stabilite con l'indirizzo IP anziché con i nomi di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="7e9e5-248">Come funziona il gateway dati?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-248">How does the data gateway work?</span></span>

<span data-ttu-id="7e9e5-249">Il gateway dati facilita la comunicazione rapida e sicura tra l'app per la logica, il servizio cloud del gateway e l'origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="7e9e5-251">Pertanto quando l'utente nel cloud interagisce con un elemento connesso a un'origine dati in locale:</span><span class="sxs-lookup"><span data-stu-id="7e9e5-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="7e9e5-252">Il servizio cloud del gateway crea una query, insieme alle credenziali crittografate per l'origine dati, e invia la query alla coda affinché venga elaborata dal gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="7e9e5-253">Il servizio cloud del gateway analizza la query e inserisce la richiesta nel bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="7e9e5-254">Il gateway dati locale esegue il polling del bus di servizio per le richieste in sospeso.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="7e9e5-255">Il gateway riceve la query, decrittografa le credenziali e le usa per la connessione alle origini dati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="7e9e5-256">Invia quindi la query all'origine dati per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="7e9e5-257">I risultati vengono quindi inviati dall'origine dati al gateway e quindi al servizio cloud del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="7e9e5-258">Infine, il servizio cloud del gateway usa i risultati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="7e9e5-259">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="7e9e5-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="7e9e5-260">Generale</span><span class="sxs-lookup"><span data-stu-id="7e9e5-260">General</span></span>

<span data-ttu-id="7e9e5-261">**D**: È necessario un gateway per le origini dati nel cloud, ad esempio SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="7e9e5-262">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-262">
**A**: No.</span></span> <span data-ttu-id="7e9e5-263">Il gateway si connette solo alle origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="7e9e5-264">**D**: Il gateway deve essere installato nello stesso computer dell'origine dati?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="7e9e5-265">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-265">
**A**: No.</span></span> <span data-ttu-id="7e9e5-266">Il gateway si connette all'origine dati tramite le informazioni di connessione fornite.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="7e9e5-267">In questo senso il gateway può essere paragonato a un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="7e9e5-268">Il gateway deve solo potersi connettere al nome del server specificato.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="7e9e5-269">**D**: Perché è necessario usare un account di Azure aziendale o dell'istituto di istruzione per accedere?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="7e9e5-270">
**R**: È possibile usare solo un account di Azure aziendale o dell'istituto di istruzione quando si installa il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="7e9e5-271">L'account di accesso viene archiviato in un tenant gestito da Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e9e5-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7e9e5-272">Il nome dell'entità utente (UPN) dell'account di Azure AD in genere corrisponde all'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="7e9e5-273">**D**: Dove sono archiviate le credenziali?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="7e9e5-274">
**R**: Le credenziali immesse per un'origine dati vengono crittografate e archiviate nel servizio cloud del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="7e9e5-275">Le credenziali vengono quindi decrittografate nel gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="7e9e5-276">**D**: Sono previsti requisiti per la larghezza di banda della rete?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="7e9e5-277">
**R**: È consigliabile che la connessione di rete abbia una buona velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="7e9e5-278">Ogni ambiente è diverso e la quantità di dati inviati influisce sui risultati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="7e9e5-279">L'uso di ExpressRoute può contribuire a garantire un livello di velocità effettiva tra i data center di Azure e quelli locali.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="7e9e5-280">Lo strumenti di terze parti Azure Speed Test può aiutare a valutare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="7e9e5-281">**D**: Qual è la latenza per l'esecuzione di query a un'origine dati dal gateway?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="7e9e5-282">Qual è l'architettura ottimale?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-282">What is the best architecture?</span></span> <br/><span data-ttu-id="7e9e5-283">
**R**: Per ridurre la latenza di rete è consigliabile installare il gateway il più vicino possibile all'origine dati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="7e9e5-284">Installando il gateway nell'origine dati effettiva, la latenza introdotta risulterà ridotta al minimo grazie a questa prossimità.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="7e9e5-285">Si considerino anche i data center.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-285">Consider the datacenters too.</span></span> <span data-ttu-id="7e9e5-286">Se, ad esempio, il servizio usa il data center degli Stati Uniti occidentali e SQL Server è ospitato in una macchina virtuale di Azure, è opportuno che anche la macchina virtuale di Azure sia ubicata negli Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="7e9e5-287">Grazie a questa prossimità la latenza è ridotta al minimo e si evitano addebiti relativi ai dati in uscita sulla macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="7e9e5-288">**D**: In che modo i risultati vengono inviati al cloud?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="7e9e5-289">
**R**: I risultati vengono inviati tramite il Bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="7e9e5-290">**D**: Esistono connessioni in ingresso al gateway dal cloud?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="7e9e5-291">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-291">
**A**: No.</span></span> <span data-ttu-id="7e9e5-292">Il gateway usa le connessioni in uscita al bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="7e9e5-293">**D**: Cosa accade se si bloccano le connessioni in uscita?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="7e9e5-294">Cosa fare per sbloccarle?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-294">What do I need to open?</span></span> <br/><span data-ttu-id="7e9e5-295">
**R**: Visualizzare le porte e gli host usati dal gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="7e9e5-296">**D**: Come viene chiamato il servizio Windows effettivo?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="7e9e5-297">
**R**: Nei servizi il gateway è denominato servizio Power BI Gateway Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="7e9e5-298">**D**: Il servizio gateway di Windows può essere eseguito con un account Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="7e9e5-299">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-299">
**A**: No.</span></span> <span data-ttu-id="7e9e5-300">Il servizio Windows deve disporre di un account Windows valido.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="7e9e5-301">Per impostazione predefinita, il sevizio viene eseguito con il SID servizio NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="7e9e5-302">Disponibilità elevata e ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="7e9e5-302">High availability and disaster recovery</span></span>

<span data-ttu-id="7e9e5-303">**D**: Quali opzioni sono disponibili per il ripristino di emergenza?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="7e9e5-304">
**R**: È possibile usare la chiave di ripristino per ripristinare o spostare un gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="7e9e5-305">La chiave di ripristino viene specificata al momento dell'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="7e9e5-306">**D**: Qual è il vantaggio della chiave di ripristino?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="7e9e5-307">
**R**: La chiave di ripristino consente di eseguire la migrazione o di ripristinare le impostazioni del gateway in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="7e9e5-308">**D**: Esistono piani per l'abilitazione di scenari a disponibilità elevata con il gateway?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="7e9e5-309">
**R**: Questi scenari verranno implementati in futuro, ma non è ancora stato definito quando.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7e9e5-310">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7e9e5-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="7e9e5-311">**D**: Come è possibile visualizzare le query inviate all'origine dati locale?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="7e9e5-312">
**R**: È possibile abilitare la funzione di tracciamento delle query, che include le query inviate.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="7e9e5-313">Dopo aver risolto il problema, ripristinare il valore originale per il tracciamento delle query.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="7e9e5-314">Se il tracciamento delle query non viene disabilitato, si creeranno dei log più grandi.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="7e9e5-315">È anche possibile usare gli strumenti per il tracciamento delle query di cui è dotata l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="7e9e5-316">Ad esempio, è possibile usare Eventi estesi o SQL Profiler per SQL Server e Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="7e9e5-317">**D**: Dove si trovano i log del gateway?</span><span class="sxs-lookup"><span data-stu-id="7e9e5-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="7e9e5-318">
**R**: Vedere la sezione Strumenti più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="7e9e5-319">Aggiornare alla versione più recente</span><span class="sxs-lookup"><span data-stu-id="7e9e5-319">Update to the latest version</span></span>

<span data-ttu-id="7e9e5-320">Quando la versione del gateway non è aggiornata, possono emergere numerosi problemi.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="7e9e5-321">Come buona pratica, assicurarsi di usare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="7e9e5-322">Se il gateway non è stato aggiornato per un mese o più è consigliabile installarne la versione più recente e verificare se è possibile riprodurre il problema.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="7e9e5-323">Errore: Impossibile aggiungere l'utente al gruppo.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="7e9e5-324">(Utenti log delle prestazioni -2147463168 PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="7e9e5-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="7e9e5-325">Questo errore viene visualizzato se si sta tentando di installare il gateway in un controller di dominio, un'operazione non consentita.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="7e9e5-326">Assicurarsi di distribuire il gateway in un computer che non sia un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="7e9e5-327">Strumenti</span><span class="sxs-lookup"><span data-stu-id="7e9e5-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="7e9e5-328">Raccolta di log dallo strumento di configurazione del gateway</span><span class="sxs-lookup"><span data-stu-id="7e9e5-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="7e9e5-329">È possibile raccogliere numerosi log per il gateway.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="7e9e5-330">La raccolta dei log è sempre la prima operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="7e9e5-331">Log dei programmi di installazione</span><span class="sxs-lookup"><span data-stu-id="7e9e5-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="7e9e5-332">Log di configurazione</span><span class="sxs-lookup"><span data-stu-id="7e9e5-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="7e9e5-333">Log del servizio gateway Enterprise</span><span class="sxs-lookup"><span data-stu-id="7e9e5-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="7e9e5-334">Log eventi</span><span class="sxs-lookup"><span data-stu-id="7e9e5-334">Event logs</span></span>

<span data-ttu-id="7e9e5-335">I log di Gateway di gestione dati e PowerBIGateway sono reperibili in **Registri applicazioni e servizi**.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="7e9e5-336">Fiddler Trace</span><span class="sxs-lookup"><span data-stu-id="7e9e5-336">Fiddler Trace</span></span>

<span data-ttu-id="7e9e5-337">[Fiddler](http://www.telerik.com/fiddler) è uno strumento gratuito di Telerik che consente di monitorare il traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="7e9e5-338">Dal computer client è possibile visualizzare il traffico con il sevizio Power BI e il computer client.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="7e9e5-339">Questo servizio consente di visualizzare errori e altre informazioni correlate.</span><span class="sxs-lookup"><span data-stu-id="7e9e5-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e9e5-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e9e5-340">Next steps</span></span>
    
* [<span data-ttu-id="7e9e5-341">Connessione al gateway dati locale per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="7e9e5-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="7e9e5-342">Funzionalità di Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="7e9e5-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="7e9e5-343">Connettori per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="7e9e5-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
