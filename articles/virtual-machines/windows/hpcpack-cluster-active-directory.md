---
title: Cluster HPC Pack con Azure Active Directory | Documentazione Microsoft
description: Informazioni su come integrare un cluster HPC Pack 2016 in Azure con Azure Active Directory
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
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="cd041-103">Gestire un cluster HPC Pack in Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd041-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="cd041-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supporta l'integrazione con [Azure Active Directory](../../active-directory/index.md) (Azure AD) per gli amministratori che distribuiscono un cluster HPC Pack in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd041-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="cd041-105">Seguire i passaggi descritti in questo articolo per le attività di alto livello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd041-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="cd041-106">Integrare manualmente il cluster HPC Pack con il proprio tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd041-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="cd041-107">Gestire e pianificare i processi nel cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="cd041-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="cd041-108">L'integrazione di una soluzione cluster HPC Pack con Azure AD si attiene ai passaggi standard da seguire per integrare altri servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="cd041-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="cd041-109">In questo articolo si presuppone di avere dimestichezza con la gestione utente di base in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd041-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="cd041-110">Per altre informazioni e aspetti di fondo, consultare la [documentazione di Azure Active Directory](../../active-directory/index.md) e la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="cd041-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="cd041-111">Vantaggi dell'integrazione</span><span class="sxs-lookup"><span data-stu-id="cd041-111">Benefits of integration</span></span>


<span data-ttu-id="cd041-112">Azure Active Directory (Azure AD) è il servizio di gestione di identità e directory basato sul cloud e multi-tenant che offre un accesso SSO alle soluzioni cloud.</span><span class="sxs-lookup"><span data-stu-id="cd041-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="cd041-113">L'integrazione di un cluster HPC Pack con Azure AD consente di raggiungere gli obiettivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd041-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="cd041-114">Rimuovere il tradizionale controller di dominio di Active Directory dal cluster HPC Pack,</span><span class="sxs-lookup"><span data-stu-id="cd041-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="cd041-115">così da contribuire a ridurre i costi di manutenzione del cluster se non è necessario per l'azienda, oltre ad accelerare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cd041-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="cd041-116">Sfruttare i vantaggi seguenti che vengono offerti da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="cd041-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="cd041-117">Single sign-on</span><span class="sxs-lookup"><span data-stu-id="cd041-117">Single sign-on</span></span> 
    *   <span data-ttu-id="cd041-118">Uso di un'identità di Active Directory locale per il cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="cd041-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Ambiente di Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="cd041-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cd041-120">Prerequisites</span></span>
* <span data-ttu-id="cd041-121">**Cluster HPC Pack 2016 distribuito nelle macchine virtuali di Azure**: per la procedura vedere [Distribuire un cluster HPC Pack 2016 in Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cd041-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="cd041-122">Per completare la procedura descritta in questo articolo, sono necessari il nome DNS del nodo head e le credenziali di un amministratore del cluster.</span><span class="sxs-lookup"><span data-stu-id="cd041-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cd041-123">L'integrazione di Azure Active Directory non è supportata nelle versioni di HPC Pack precedenti a quella del 2016.</span><span class="sxs-lookup"><span data-stu-id="cd041-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="cd041-124">**Computer client**: per eseguire le utilità client di HPC Pack è necessario un computer client Windows o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cd041-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="cd041-125">Se si prevede di inviare i processi solo tramite il portale Web di HPC Pack o l'API REST, è possibile usare un computer client qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="cd041-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="cd041-126">**Utilità client di HPC Pack**: installare le utilità client di HPC Pack nel computer client usando il pacchetto di installazione gratuito disponibile nell'Area Download Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd041-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="cd041-127">Passaggio 1: Registrare il server del cluster HPC con il proprio tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd041-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="cd041-128">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd041-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cd041-129">Fare clic su **Active Directory** nel menu a sinistra e selezionare la directory desiderata nella propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd041-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="cd041-130">È necessario disporre dell'autorizzazione per accedere alle risorse nella directory.</span><span class="sxs-lookup"><span data-stu-id="cd041-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="cd041-131">Fare clic su **Utenti** e verificare la presenza di account utente già creati o configurati.</span><span class="sxs-lookup"><span data-stu-id="cd041-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="cd041-132">Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="cd041-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="cd041-133">Immettere le seguenti informazioni nella procedura guidata:</span><span class="sxs-lookup"><span data-stu-id="cd041-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="cd041-134">**Nome**: HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="cd041-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="cd041-135">**Tipo**: selezionare **Applicazione Web e/o API Web**</span><span class="sxs-lookup"><span data-stu-id="cd041-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="cd041-136">**URL di accesso**: l'URL di base per l'esempio, che per impostazione predefinita è `https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="cd041-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="cd041-137">**URI ID app** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="cd041-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="cd041-138">Sostituire `<Directory_name`> con il nome completo del tenant di Azure AD, ad esempio `hpclocal.onmicrosoft.com` e sostituire `<application_name>` con il nome scelto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cd041-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="cd041-139">Dopo aver aggiunto l'app, fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="cd041-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="cd041-140">Configurare le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd041-140">Configure the following properties:</span></span>
    * <span data-ttu-id="cd041-141">Selezionare **Sì** per **L'applicazione è multi-tenant**</span><span class="sxs-lookup"><span data-stu-id="cd041-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="cd041-142">Selezionare **Sì** per **Assegnazione utente obbligatoria per l'accesso all'app**.</span><span class="sxs-lookup"><span data-stu-id="cd041-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="cd041-143">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="cd041-143">Click **Save**.</span></span> <span data-ttu-id="cd041-144">Al termine del salvataggio, fare clic su **Gestisci manifesto**.</span><span class="sxs-lookup"><span data-stu-id="cd041-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="cd041-145">Questa azione permette di scaricare il file JavaScript Object Notation (JSON) del manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cd041-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="cd041-146">Modificare il manifesto scaricato individuando l'impostazione `appRoles` e aggiungendo il ruolo dell'applicazione seguente:</span><span class="sxs-lookup"><span data-stu-id="cd041-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
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
7. <span data-ttu-id="cd041-147">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="cd041-147">Save the file.</span></span> <span data-ttu-id="cd041-148">Dopodiché, fare clic su **Gestisci manifesto** > **Carica manifesto** nel portale.</span><span class="sxs-lookup"><span data-stu-id="cd041-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="cd041-149">È quindi possibile caricare il manifesto modificato.</span><span class="sxs-lookup"><span data-stu-id="cd041-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="cd041-150">Fare clic su **Utenti**, selezionare un utente e fare clic su **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="cd041-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="cd041-151">Assegnare uno dei ruoli disponibili (HpcUsers o HpcAdminMirror) all'utente.</span><span class="sxs-lookup"><span data-stu-id="cd041-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="cd041-152">Ripetere questo passaggio con altri utenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="cd041-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="cd041-153">Per informazioni generali sugli utenti del cluster, vedere [Gestione di utenti cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="cd041-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="cd041-154">Per gestire gli utenti è consigliabile usare il pannello di anteprima di Azure Active Directory nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd041-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="cd041-155">Passaggio 2: Registrare il client del cluster HPC con il proprio tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd041-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="cd041-156">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd041-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cd041-157">Fare clic su **Active Directory** nel menu a sinistra e selezionare la directory desiderata nella propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd041-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="cd041-158">È necessario disporre dell'autorizzazione per accedere alle risorse nella directory.</span><span class="sxs-lookup"><span data-stu-id="cd041-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="cd041-159">Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.</span><span class="sxs-lookup"><span data-stu-id="cd041-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="cd041-160">Immettere le seguenti informazioni nella procedura guidata:</span><span class="sxs-lookup"><span data-stu-id="cd041-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="cd041-161">**Nome**: HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="cd041-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="cd041-162">**Tipo**: selezionare **Applicazione client nativa**</span><span class="sxs-lookup"><span data-stu-id="cd041-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="cd041-163">**URI di reindirizzamento** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="cd041-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="cd041-164">Dopo aver aggiunto l'app, fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="cd041-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="cd041-165">Copiare il valore **ID client** e salvarlo,</span><span class="sxs-lookup"><span data-stu-id="cd041-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="cd041-166">poiché servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cd041-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="cd041-167">In **Autorizzazioni per altre applicazioni** fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="cd041-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="cd041-168">Cercare e aggiungere l'applicazione HpcPackClusterServer (creata nel passaggio 1).</span><span class="sxs-lookup"><span data-stu-id="cd041-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="cd041-169">Nell'elenco a discesa **Autorizzazioni delegate** selezionare **Accedi a HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="cd041-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="cd041-170">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="cd041-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="cd041-171">Passaggio 3: Configurare il cluster HPC</span><span class="sxs-lookup"><span data-stu-id="cd041-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="cd041-172">Connettersi al nodo head di HPC Pack 2016 in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd041-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="cd041-173">Avviare HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd041-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="cd041-174">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd041-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="cd041-175">dove</span><span class="sxs-lookup"><span data-stu-id="cd041-175">where</span></span>

    * <span data-ttu-id="cd041-176">`AADTenant` specifica il nome del tenant di Azure AD, ad esempio `hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="cd041-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="cd041-177">`AADClientAppId` specifica l'ID client per l'app creata nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="cd041-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="cd041-178">Riavviare il servizio HpcSchedulerStateful.</span><span class="sxs-lookup"><span data-stu-id="cd041-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="cd041-179">In un cluster con più nodi head è possibile eseguire i comandi PowerShell seguenti nel nodo head per passare alla replica primaria del servizio HpcSchedulerStateful:</span><span class="sxs-lookup"><span data-stu-id="cd041-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="cd041-180">Passaggio 4: Gestire e inviare i processi dal client</span><span class="sxs-lookup"><span data-stu-id="cd041-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="cd041-181">Per installare le utilità client di HPC Pack 2016 nel computer, scaricare i file di installazione (installazione completa) dall'Area download Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd041-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="cd041-182">All'inizio della procedura di installazione, scegliere l'opzione di installazione per le **utilità client di HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="cd041-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="cd041-183">Per preparare il computer client, installare il certificato usato durante la [configurazione del cluster HPC](hpcpack-2016-cluster.md) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="cd041-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="cd041-184">Seguire le procedure di gestione del certificato di Windows standard per installare il certificato pubblico nell'archivio **Certificati – utente corrente** > **Autorità di certificazione principale attendibili**.</span><span class="sxs-lookup"><span data-stu-id="cd041-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="cd041-185">È ora possibile eseguire i comandi di HPC Pack o usare l'interfaccia grafica utente del gestore processi di HPC Pack per inviare e gestire i processi cluster usando l'account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd041-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="cd041-186">Per le opzioni di invio di un processo vedere [Inviare i processi HPC a un cluster HPC in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="cd041-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="cd041-187">Quando si tenta di connettersi al cluster HPC Pack in Azure per la prima volta, viene visualizzata una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="cd041-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="cd041-188">Immettere le credenziali di Azure AD per accedere.</span><span class="sxs-lookup"><span data-stu-id="cd041-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="cd041-189">Il token viene quindi memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="cd041-189">The token is then cached.</span></span> <span data-ttu-id="cd041-190">Per i successivi tentativi di connessione al cluster in Azure verrà usato il token memorizzato nella cache, salvo modifica dell'autenticazione o cancellazione della cache.</span><span class="sxs-lookup"><span data-stu-id="cd041-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="cd041-191">Ad esempio, dopo aver completato i passaggi precedenti, è possibile eseguire una query per i processi da un client locale nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="cd041-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="cd041-192">Cmdlet utili per l'invio di processi con l'integrazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd041-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="cd041-193">Gestire la cache locale dei token</span><span class="sxs-lookup"><span data-stu-id="cd041-193">Manage the local token cache</span></span>

<span data-ttu-id="cd041-194">HPC Pack 2016 offre due nuovi cmdlet di HPC PowerShell per gestire la cache locale dei token.</span><span class="sxs-lookup"><span data-stu-id="cd041-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="cd041-195">Questi cmdlet sono utili per inviare processi in modo non interattivo.</span><span class="sxs-lookup"><span data-stu-id="cd041-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="cd041-196">Vedere l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="cd041-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="cd041-197">Impostare le credenziali per l'invio di processi con l'account di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd041-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="cd041-198">A volte, è consigliabile eseguire il processo con l'utente del cluster HPC (per un cluster HPC aggiunto a un dominio, eseguito come utente di un dominio, ma per un cluster HPC non appartenente a un dominio, eseguire come un utente locale nel nodo head).</span><span class="sxs-lookup"><span data-stu-id="cd041-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="cd041-199">Per impostare le credenziali, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd041-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="cd041-200">Dopodiché, inviare il processo come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cd041-200">Then submit the job as follows.</span></span> <span data-ttu-id="cd041-201">Il processo/attività viene eseguito in $localUser sui nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="cd041-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="cd041-202">Se `–Credential` non viene specificato con `Submit-HpcJob`, il processo/attività viene eseguito sotto un utente mappato in locale come account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd041-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="cd041-203">Il cluster HPC crea un utente locale con lo stesso nome dell'account di Azure AD per eseguire l'attività.</span><span class="sxs-lookup"><span data-stu-id="cd041-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="cd041-204">Impostare i dati estesi per l'account Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd041-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="cd041-205">Ciò è utile quando si esegue un processo MPI in nodi di Linux utilizzando l'account Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd041-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="cd041-206">Impostare i dati estesi per l'account Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd041-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="cd041-207">Impostare i dati estesi ed eseguire come utente del cluster HPC</span><span class="sxs-lookup"><span data-stu-id="cd041-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

