---
title: aaaHPC Pack cluster con Azure Active Directory | Documenti Microsoft
description: Informazioni su come toointegrate un' 2016 Pack HPC cluster in Azure con Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="72588-103">Gestire un cluster HPC Pack in Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72588-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="72588-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supporta l'integrazione con [Azure Active Directory](../../active-directory/index.md) (Azure AD) per gli amministratori che distribuiscono un cluster HPC Pack in Azure.</span><span class="sxs-lookup"><span data-stu-id="72588-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="72588-105">Seguire i passaggi di hello in questo articolo per hello seguenti attività di livello elevata:</span><span class="sxs-lookup"><span data-stu-id="72588-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="72588-106">Integrare manualmente il cluster HPC Pack con il proprio tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72588-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="72588-107">Gestire e pianificare i processi nel cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="72588-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="72588-108">Integrazione di una soluzione di cluster HPC Pack con Azure AD segue i passaggi standard toointegrate altri servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="72588-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="72588-109">In questo articolo si presuppone di avere dimestichezza con la gestione utente di base in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72588-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="72588-110">Per ulteriori informazioni e in background, vedere hello [documentazione di Azure Active Directory](../../active-directory/index.md) e hello seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="72588-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="72588-111">Vantaggi dell'integrazione</span><span class="sxs-lookup"><span data-stu-id="72588-111">Benefits of integration</span></span>


<span data-ttu-id="72588-112">Azure Active Directory (Azure AD) è un multi-tenant basati su cloud directory e identità del servizio di gestione che fornisce accesso single sign-on (SSO) toocloud soluzioni.</span><span class="sxs-lookup"><span data-stu-id="72588-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="72588-113">Integrazione di un cluster HPC Pack con Azure AD è possibile realizzare hello gli obiettivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="72588-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="72588-114">Rimuovere i controller di dominio Active Directory tradizionale hello dal cluster HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="72588-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="72588-115">Questo può ridurre i costi di hello di Gestione cluster di hello se questo non è necessario per l'azienda e processo di distribuzione di velocizzare hello.</span><span class="sxs-lookup"><span data-stu-id="72588-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="72588-116">Sfruttare hello seguenti vantaggi che vengono attivata la modalità da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="72588-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="72588-117">Single sign-on</span><span class="sxs-lookup"><span data-stu-id="72588-117">Single sign-on</span></span> 
    *   <span data-ttu-id="72588-118">Uso di un'identità di Active Directory locale per il cluster HPC Pack hello in Azure</span><span class="sxs-lookup"><span data-stu-id="72588-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Ambiente di Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="72588-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72588-120">Prerequisites</span></span>
* <span data-ttu-id="72588-121">**Cluster HPC Pack 2016 distribuito nelle macchine virtuali di Azure**: per la procedura vedere [Distribuire un cluster HPC Pack 2016 in Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="72588-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="72588-122">È necessario il nome DNS hello del nodo head hello e credenziali di hello di un amministratore cluster per completare i passaggi di hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="72588-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="72588-123">L'integrazione di Azure Active Directory non è supportata nelle versioni di HPC Pack precedenti a quella del 2016.</span><span class="sxs-lookup"><span data-stu-id="72588-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="72588-124">**Computer client** -è necessario un Windows o Windows Server client computer eseguito troppo HPC Pack utilità client.</span><span class="sxs-lookup"><span data-stu-id="72588-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="72588-125">Se si desidera solo portale web di HPC Pack hello toouse o processi toosubmit API REST, è possibile utilizzare tutti i computer client di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="72588-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="72588-126">**Utilità client di HPC Pack** -installare le utilità client di HPC Pack hello nel computer client hello tramite pacchetto di installazione gratuito hello disponibile da Microsoft Download Center hello.</span><span class="sxs-lookup"><span data-stu-id="72588-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="72588-127">Passaggio 1: Registrare i server di cluster HPC hello con tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72588-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="72588-128">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="72588-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="72588-129">Fare clic su **Active Directory** in hello menu a sinistra e quindi fare clic sulla directory desiderata di hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72588-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="72588-130">È necessario disporre risorse tooaccess autorizzazione nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="72588-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="72588-131">Fare clic su **Utenti** e verificare la presenza di account utente già creati o configurati.</span><span class="sxs-lookup"><span data-stu-id="72588-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="72588-132">Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="72588-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="72588-133">Immettere le seguenti informazioni nella procedura guidata hello hello:</span><span class="sxs-lookup"><span data-stu-id="72588-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="72588-134">**Nome**: HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="72588-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="72588-135">**Tipo**: selezionare **Applicazione Web e/o API Web**</span><span class="sxs-lookup"><span data-stu-id="72588-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="72588-136">**URL di accesso**: hello URL di base per un esempio di hello, per impostazione predefinita`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="72588-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="72588-137">**URI ID app** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="72588-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="72588-138">Sostituire `<Directory_name`> con nome completo del tenant di Azure AD, ad esempio, hello `hpclocal.onmicrosoft.com`e sostituire `<application_name>` con nome hello scelto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="72588-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="72588-139">Dopo aver aggiunto l'applicazione hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="72588-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="72588-140">Configurare hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="72588-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="72588-141">Selezionare **Sì** per **L'applicazione è multi-tenant**</span><span class="sxs-lookup"><span data-stu-id="72588-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="72588-142">Selezionare **Sì** per **utente assegnazione tooaccess obbligatorio app**.</span><span class="sxs-lookup"><span data-stu-id="72588-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="72588-143">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72588-143">Click **Save**.</span></span> <span data-ttu-id="72588-144">Al termine del salvataggio, fare clic su **Gestisci manifesto**.</span><span class="sxs-lookup"><span data-stu-id="72588-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="72588-145">Questa azione permette di scaricare il file JavaScript Object Notation (JSON) del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72588-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="72588-146">Modifica manifesto di hello scaricato individuando hello `appRoles` impostazione e l'aggiunta di hello ruolo applicazione seguente:</span><span class="sxs-lookup"><span data-stu-id="72588-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="72588-147">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="72588-147">Save hello file.</span></span> <span data-ttu-id="72588-148">Quindi, nel portale di hello, fare clic su **Gestisci manifesto** > **carica manifesto**.</span><span class="sxs-lookup"><span data-stu-id="72588-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="72588-149">È quindi possibile caricare hello modificato manifesto.</span><span class="sxs-lookup"><span data-stu-id="72588-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="72588-150">Fare clic su **Utenti**, selezionare un utente e fare clic su **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="72588-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="72588-151">Assegnare un utente toohello (HpcUsers o HpcAdminMirror) hello ruoli disponibili.</span><span class="sxs-lookup"><span data-stu-id="72588-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="72588-152">Ripetere questo passaggio con altri utenti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="72588-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="72588-153">Per informazioni generali sugli utenti del cluster, vedere [Gestione di utenti cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="72588-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="72588-154">gli utenti toomanage, è consigliabile utilizzare Pannello di anteprima di Azure Active Directory hello hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72588-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="72588-155">Passaggio 2: Registrare i client di cluster HPC hello con tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72588-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="72588-156">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="72588-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="72588-157">Fare clic su **Active Directory** in hello menu a sinistra e quindi fare clic sulla directory desiderata di hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72588-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="72588-158">È necessario disporre risorse tooaccess autorizzazione nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="72588-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="72588-159">Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="72588-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="72588-160">Immettere le seguenti informazioni nella procedura guidata hello hello:</span><span class="sxs-lookup"><span data-stu-id="72588-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="72588-161">**Nome**: HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="72588-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="72588-162">**Tipo**: selezionare **Applicazione client nativa**</span><span class="sxs-lookup"><span data-stu-id="72588-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="72588-163">**URI di reindirizzamento** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="72588-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="72588-164">Dopo aver aggiunto l'applicazione hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="72588-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="72588-165">Hello copia **ID Client** valore e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="72588-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="72588-166">poiché servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72588-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="72588-167">In **autorizzazioni tooother applicazioni**, fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="72588-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="72588-168">Cercare e aggiungere un'applicazione hello HpcPackClusterServer (creata nel passaggio 1).</span><span class="sxs-lookup"><span data-stu-id="72588-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="72588-169">In hello **autorizzazioni delegate** elenco a discesa Seleziona **HpcClusterServer accesso**.</span><span class="sxs-lookup"><span data-stu-id="72588-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="72588-170">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72588-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="72588-171">Passaggio 3: Configurare un cluster HPC hello</span><span class="sxs-lookup"><span data-stu-id="72588-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="72588-172">Connettersi toohello HPC Pack 2016 nodo head in Azure.</span><span class="sxs-lookup"><span data-stu-id="72588-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="72588-173">Avviare HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72588-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="72588-174">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="72588-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="72588-175">dove</span><span class="sxs-lookup"><span data-stu-id="72588-175">where</span></span>

    * <span data-ttu-id="72588-176">`AADTenant`Specifica nome del tenant hello Azure AD, ad esempio`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="72588-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="72588-177">`AADClientAppId`Specifica l'ID client hello per le app hello creata nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="72588-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="72588-178">Riavviare il servizio di HpcSchedulerStateful hello.</span><span class="sxs-lookup"><span data-stu-id="72588-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="72588-179">In un cluster con più nodi head, è possibile eseguire i seguenti comandi PowerShell hello nodo head tooswitch hello replica primaria per il servizio HpcSchedulerStateful hello hello:</span><span class="sxs-lookup"><span data-stu-id="72588-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="72588-180">Passaggio 4: Gestire e inviare i processi da client hello</span><span class="sxs-lookup"><span data-stu-id="72588-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="72588-181">utilità client di HPC Pack tooinstall hello nel computer in uso, scaricare i file di installazione di HPC Pack 2016 (installazione completa) dal Microsoft Download Center hello.</span><span class="sxs-lookup"><span data-stu-id="72588-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="72588-182">Quando si inizia installazione hello, scegliere l'opzione di installazione di hello per hello **utilità client di HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="72588-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="72588-183">tooprepare hello client computer, installare il certificato di hello utilizzato durante [l'installazione del cluster HPC](hpcpack-2016-cluster.md) nel computer client hello.</span><span class="sxs-lookup"><span data-stu-id="72588-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="72588-184">Usa Windows standard certificato gestione procedure tooinstall hello certificato pubblico toohello **certificati – utente corrente** > **autorità di certificazione radice attendibili** archiviare.</span><span class="sxs-lookup"><span data-stu-id="72588-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="72588-185">È ora possibile eseguire i comandi di HPC Pack hello o utilizzare hello GUI di gestione di processi di HPC Pack toosubmit e gestire i processi di cluster con l'account di hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72588-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="72588-186">Per le opzioni invio del processo, vedere [cluster HPC di inviare processi tooan HPC Pack in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="72588-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="72588-187">Quando si tenta di tooconnect toohello cluster HPC Pack in Azure per hello prima volta, viene visualizzata una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="72588-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="72588-188">Immettere il toolog le credenziali di Azure AD in.</span><span class="sxs-lookup"><span data-stu-id="72588-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="72588-189">token Hello viene quindi memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="72588-189">hello token is then cached.</span></span> <span data-ttu-id="72588-190">Cluster di toohello le connessioni successive in Azure usare hello memorizzati nella cache di token, a meno che le modifiche di autenticazione o hello memorizzati nella cache viene cancellata.</span><span class="sxs-lookup"><span data-stu-id="72588-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="72588-191">Ad esempio, dopo aver completato i passaggi precedenti hello, è possibile eseguire query per i processi da un client locale come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="72588-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="72588-192">Cmdlet utili per l'invio di processi con l'integrazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72588-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="72588-193">Gestire cache locale del token hello</span><span class="sxs-lookup"><span data-stu-id="72588-193">Manage hello local token cache</span></span>

<span data-ttu-id="72588-194">HPC Pack 2016 fornisce due nuovi cmdlet di PowerShell HPC toomanage hello locale della cache dei token.</span><span class="sxs-lookup"><span data-stu-id="72588-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="72588-195">Questi cmdlet sono utili per inviare processi in modo non interattivo.</span><span class="sxs-lookup"><span data-stu-id="72588-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="72588-196">Vedere hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="72588-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="72588-197">Impostare le credenziali di hello per l'invio di processi tramite account hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="72588-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="72588-198">In alcuni casi, è consigliabile toorun del processo hello nell'utente del cluster HPC hello (per un cluster HPC con dominio, eseguire come utente di un dominio, per un cluster HPC non appartenenti a un dominio, eseguire con un account utente locale nel nodo head hello).</span><span class="sxs-lookup"><span data-stu-id="72588-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="72588-199">Utilizzare hello le credenziali di hello tooset i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="72588-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="72588-200">Quindi inviare il processo di hello come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="72588-200">Then submit hello job as follows.</span></span> <span data-ttu-id="72588-201">Hello processo/attività viene eseguita in $localUser sui nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="72588-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="72588-202">Se `–Credential` non è specificato con `Submit-HpcJob`, hello processo o attività viene eseguito con un account utente locale mappato come hello account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72588-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="72588-203">(cluster HPC hello crea un utente locale con stesso nome come attività di Azure AD account toorun hello hello hello).</span><span class="sxs-lookup"><span data-stu-id="72588-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="72588-204">Impostare i dati estesi per hello account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72588-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="72588-205">Ciò è utile quando si esegue un processo MPI in nodi di Linux utilizzando account hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72588-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="72588-206">Impostare i dati estesi per hello account AD Azure stesso</span><span class="sxs-lookup"><span data-stu-id="72588-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="72588-207">Impostare i dati estesi ed eseguire come utente del cluster HPC</span><span class="sxs-lookup"><span data-stu-id="72588-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

