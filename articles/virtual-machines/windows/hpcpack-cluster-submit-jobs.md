---
title: Inviare processi a un cluster HPC Pack in Azure | Microsoft Docs
description: Informazioni su come configurare un computer locale per l'invio di processi a un cluster HPC Pack in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: d5953f1e1dd2deb4d871bd67352a6a5b2ae13dbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="e11ca-103">Inviare i processi HPC da un computer locale a un cluster HPC Pack distribuito in Azure</span><span class="sxs-lookup"><span data-stu-id="e11ca-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e11ca-104">Configurare un computer client locale per l'invio di processi a un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e11ca-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="e11ca-105">In questo articolo viene illustrato come configurare un computer locale con gli strumenti client per inviare processi tramite HTTPS al cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="e11ca-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="e11ca-106">In questo modo, più utenti di cluster possono inviare processi a un cluster HPC Pack basato sul cloud, ma senza connettersi direttamente alla VM del nodo head o accedere a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e11ca-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Invio di un processo a un cluster in Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="e11ca-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e11ca-108">Prerequisites</span></span>
* <span data-ttu-id="e11ca-109">**Nodo head HPC Pack distribuito in una VM di Azure**: si consiglia l'uso di strumenti automatizzati, ad esempio un [modello di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) o uno [script di Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) per distribuire il nodo head e il cluster.</span><span class="sxs-lookup"><span data-stu-id="e11ca-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="e11ca-110">Per completare la procedura descritta in questo articolo, sono necessari il nome DNS del nodo head e le credenziali di un amministratore del cluster.</span><span class="sxs-lookup"><span data-stu-id="e11ca-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="e11ca-111">**Computer client** : è necessario un computer client Windows o Windows server in grado di eseguire le utilità client di HPC Pack (vedere i [requisiti di sistema](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e11ca-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="e11ca-112">Se si prevede di inviare i processi solo tramite il portale Web di HPC Pack o l'API REST, è possibile usare un computer client qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="e11ca-113">**Supporto di installazione di HPC Pack** : per installare il client di HPC Pack, è disponibile gratuitamente il pacchetto di installazione dell'ultima versione di HPC Pack (HPC Pack 2012 R2) è disponibile per il download nell' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="e11ca-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="e11ca-114">Verificare di avere scaricato la stessa versione di HPC Pack installata nella VM del nodo head.</span><span class="sxs-lookup"><span data-stu-id="e11ca-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="e11ca-115">Passaggio 1: installare e configurare i componenti Web nel nodo head</span><span class="sxs-lookup"><span data-stu-id="e11ca-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="e11ca-116">Per consentire a un'interfaccia REST di inviare processi al cluster tramite HTTPS, assicurarsi che i componenti Web di HPC Pack siano configurati nel nodo head HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e11ca-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="e11ca-117">Se non sono ancora installati, per prima cosa procedere all'installazione dei componenti Web eseguendo il file di installazione HpcWebComponents.msi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="e11ca-118">Configurare quindi i componenti eseguendo lo script di HPC PowerShell **Set-HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="e11ca-119">Per le procedure dettagliate, vedere [Installare i componenti Web di Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11ca-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="e11ca-120">Alcuni modelli di avvio rapido di Azure per HPC Pack installano e configurano i componenti Web automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e11ca-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="e11ca-121">Se si usa lo [script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) per creare il cluster, è possibile scegliere di installare e configurare i componenti Web durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e11ca-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="e11ca-122">**Per installare i componenti Web**</span><span class="sxs-lookup"><span data-stu-id="e11ca-122">**To install the web components**</span></span>

1. <span data-ttu-id="e11ca-123">Connettersi alla macchina virtuale del nodo head usando le credenziali di amministratore del cluster.</span><span class="sxs-lookup"><span data-stu-id="e11ca-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="e11ca-124">Dalla cartella di installazione di HPC Pack, eseguire HpcWebComponents.msi nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="e11ca-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="e11ca-125">Seguire i passaggi della procedura guidata per installare i componenti Web</span><span class="sxs-lookup"><span data-stu-id="e11ca-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="e11ca-126">**Per configurare i componenti Web**</span><span class="sxs-lookup"><span data-stu-id="e11ca-126">**To configure the web components**</span></span>

1. <span data-ttu-id="e11ca-127">Nel nodo head avviare HPC PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e11ca-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="e11ca-128">Per spostarsi sul percorso dello script di configurazione, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e11ca-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="e11ca-129">Per configurare l'interfaccia REST e avviare il servizio Web HPC, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e11ca-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="e11ca-130">Quando viene richiesto di selezionare un certificato, scegliere il certificato corrispondente al nome DNS pubblico del nodo head.</span><span class="sxs-lookup"><span data-stu-id="e11ca-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="e11ca-131">Ad esempio, se si distribuisce la VM del nodo head usando il modello di distribuzione classica, il nome del certificato ha un aspetto simile a CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e11ca-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="e11ca-132">Se si usa un modello di distribuzione di Resource Manager, il nome del certificato ha un aspetto simile a CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e11ca-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e11ca-133">È necessario selezionare questo certificato per inviare processi al nodo head da un computer locale in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="e11ca-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="e11ca-134">Non selezionare né configurare un certificato corrispondente al nome computer del nodo head nel dominio di Active Directory, ad esempio CN=*MyHPCHeadNode.HpcAzure.local*.</span><span class="sxs-lookup"><span data-stu-id="e11ca-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="e11ca-135">Per configurare il portale Web per l'invio di processi, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e11ca-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="e11ca-136">Al termine dello script, arrestare e riavviare il servizio Utilità di pianificazione dei processi HPC digitando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e11ca-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="e11ca-137">Passaggio 2: installare le utilità client di HPC Pack in un computer locale</span><span class="sxs-lookup"><span data-stu-id="e11ca-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="e11ca-138">Se si desidera installare le utilità client di HPC Pack nel computer, scaricare i file di installazione (installazione completa) dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="e11ca-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="e11ca-139">All'inizio della procedura di installazione, scegliere l'opzione di installazione per le **utilità client di HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="e11ca-140">Per usare gli strumenti client di HPC Pack per inviare processi alla VM del nodo head, è necessario anche esportare un certificato dal nodo head e installarlo nel computer client.</span><span class="sxs-lookup"><span data-stu-id="e11ca-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="e11ca-141">Il certificato deve essere in formato .CER.</span><span class="sxs-lookup"><span data-stu-id="e11ca-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="e11ca-142">**Per esportare il certificato dal nodo head**</span><span class="sxs-lookup"><span data-stu-id="e11ca-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="e11ca-143">Nel nodo head aggiungere lo snap-in Certificati a Microsoft Management Console per l'account computer locale.</span><span class="sxs-lookup"><span data-stu-id="e11ca-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="e11ca-144">Per la procedura che illustra come aggiungere lo snap-in, vedere [Aggiungere lo snap-in Certificati a MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11ca-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="e11ca-145">Nell'albero della console espandere **Certificati – Computer locale** > **Personale**, quindi fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="e11ca-146">Individuare il certificato configurato per i componenti Web di HPC Pack in [Passaggio 1: installare e configurare i componenti Web nel nodo head](#step-1:-install-and-configure-the-web-components-on-the-head-node) (ad esempio, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="e11ca-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="e11ca-147">Fare clic con il pulsante destro del mouse sul nome del certificato e scegliere **All Tasks** (Tutte le attività) > **Esporta**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="e11ca-148">In Esportazione guidata certificati fare clic su **Avanti**, quindi assicurarsi che l'opzione **Non esportare la chiave privata** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="e11ca-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="e11ca-149">Seguire i passaggi rimanenti della procedura guidata per esportare il certificato nel formato binario codificato DER X.509 (.CER).</span><span class="sxs-lookup"><span data-stu-id="e11ca-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="e11ca-150">**Per importare il certificato nel computer client**</span><span class="sxs-lookup"><span data-stu-id="e11ca-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="e11ca-151">Copiare il certificato esportato dal nodo head in una cartella nel computer client.</span><span class="sxs-lookup"><span data-stu-id="e11ca-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="e11ca-152">Nel computer client eseguire certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="e11ca-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="e11ca-153">In Gestione certificati espandere **Certificati - Utente corrente** > **Autorità di certificazione principale attendibili**, fare clic con il pulsante destro del mouse su **Certificati**, quindi fare clic su **All Tasks** (Tutte le attività) > **Importa**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="e11ca-154">Nell'Importazione guidata certificati fare clic su **Avanti** e seguire i passaggi per importare il certificato esportato dal nodo head nell'archivio Autorità di certificazione radice disponibile nell'elenco locale.</span><span class="sxs-lookup"><span data-stu-id="e11ca-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="e11ca-155">Potrebbe venire visualizzato un avviso di sicurezza perché l'autorità di certificazione nel nodo head non viene riconosciuta dal computer client.</span><span class="sxs-lookup"><span data-stu-id="e11ca-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="e11ca-156">A scopo di test è possibile ignorare questo avviso e completare l'importazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="e11ca-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="e11ca-157">Passaggio 3: eseguire processi di prova sul cluster</span><span class="sxs-lookup"><span data-stu-id="e11ca-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="e11ca-158">Per verificare la configurazione, provare a eseguire processi nel cluster in Azure usando il computer locale.</span><span class="sxs-lookup"><span data-stu-id="e11ca-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="e11ca-159">È ad esempio possibile usare gli strumenti dell'interfaccia utente grafica o gli strumenti della riga di comando di HPC Pack per inviare i processi al cluster oppure</span><span class="sxs-lookup"><span data-stu-id="e11ca-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="e11ca-160">un portale basato sul Web.</span><span class="sxs-lookup"><span data-stu-id="e11ca-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="e11ca-161">**Per eseguire comandi di invio processi nel computer client**</span><span class="sxs-lookup"><span data-stu-id="e11ca-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="e11ca-162">In un computer client con installate le utilità client HPC Pack avviare un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="e11ca-163">Digitare un comando di esempio.</span><span class="sxs-lookup"><span data-stu-id="e11ca-163">Type a sample command.</span></span> <span data-ttu-id="e11ca-164">Ad esempio, per elencare tutti i processi nel cluster, digitare un comando simile a uno dei seguenti in base al nome DNS completo del nodo head:</span><span class="sxs-lookup"><span data-stu-id="e11ca-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="e11ca-165">oppure</span><span class="sxs-lookup"><span data-stu-id="e11ca-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="e11ca-166">Nell'URL dell'Utilità di pianificazione usare il nome DNS completo del nodo head e non l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="e11ca-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="e11ca-167">Se si specifica l'indirizzo IP, viene visualizzato un errore che indica che è necessario che il certificato del server includa una catena di certificati valida o sia posizionato nell'archivio radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="e11ca-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="e11ca-168">Quando richiesto, digitare il nome utente (nel formato &lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore del cluster HPC o di un altro utente cluster configurato.</span><span class="sxs-lookup"><span data-stu-id="e11ca-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="e11ca-169">È possibile scegliere di archiviare le credenziali in locale per ulteriori operazioni di processo.</span><span class="sxs-lookup"><span data-stu-id="e11ca-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="e11ca-170">Verrà visualizzato un elenco di processi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-170">A list of jobs appears.</span></span>

<span data-ttu-id="e11ca-171">**Per usare HPC Job Manager nel computer client**</span><span class="sxs-lookup"><span data-stu-id="e11ca-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="e11ca-172">Se in precedenza le credenziali di dominio per un utente cluster non sono state archiviate quando è stato inviato il processo, è possibile aggiungerle in Gestione credenziali.</span><span class="sxs-lookup"><span data-stu-id="e11ca-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="e11ca-173">a.</span><span class="sxs-lookup"><span data-stu-id="e11ca-173">a.</span></span> <span data-ttu-id="e11ca-174">Nel Pannello di controllo del computer client avviare Gestione credenziali.</span><span class="sxs-lookup"><span data-stu-id="e11ca-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="e11ca-175">b.</span><span class="sxs-lookup"><span data-stu-id="e11ca-175">b.</span></span> <span data-ttu-id="e11ca-176">Fare clic su **Credenziali Windows** > **Aggiungi credenziali generiche**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="e11ca-177">c.</span><span class="sxs-lookup"><span data-stu-id="e11ca-177">c.</span></span> <span data-ttu-id="e11ca-178">Specificare l'indirizzo Internet (ad esempio https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler o https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler) e il nome utente (&lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore del cluster o un altro utente cluster configurato.</span><span class="sxs-lookup"><span data-stu-id="e11ca-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="e11ca-179">Nel computer client avviare Gestione processi HPC.</span><span class="sxs-lookup"><span data-stu-id="e11ca-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="e11ca-180">Nella finestra di dialogo **Select Head Node** (Seleziona nodo head) digitare l'URL del nodo head in Azure (ad esempio https://&lt;HeadNodeDnsName&gt;.cloudapp.net o https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e11ca-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="e11ca-181">Verrà visualizzato il gestore dei processi HPC con un elenco dei processi sul nodo head.</span><span class="sxs-lookup"><span data-stu-id="e11ca-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="e11ca-182">**Per usare il portale Web in esecuzione nel nodo head**</span><span class="sxs-lookup"><span data-stu-id="e11ca-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="e11ca-183">Avviare un Web browser nel computer client e immettere uno dei seguenti indirizzi in base al nome DNS completo del nodo head:</span><span class="sxs-lookup"><span data-stu-id="e11ca-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="e11ca-184">oppure</span><span class="sxs-lookup"><span data-stu-id="e11ca-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="e11ca-185">Nella finestra di dialogo di sicurezza che viene visualizzata digitare le credenziali di dominio dell'amministrazione cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="e11ca-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="e11ca-186">È anche possibile aggiungere altri utenti cluster in ruoli diversi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="e11ca-187">Vedere [Gestione degli utenti del cluster](https://technet.microsoft.com/library/ff919335.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11ca-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="e11ca-188">Verrà visualizzato l'elenco dei processi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="e11ca-189">Per inviare un processo di esempio che restituisca la stringa "Hello World" dal cluster, fare clic su **Nuovo processo** nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e11ca-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="e11ca-190">Nella sezione **From submission pages** (Dalle pagine di invio) della pagina **Nuovo processo** fare clic su **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="e11ca-191">Verrà visualizzata la pagina di invio processi.</span><span class="sxs-lookup"><span data-stu-id="e11ca-191">The job submission page appears.</span></span>
5. <span data-ttu-id="e11ca-192">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="e11ca-192">Click **Submit**.</span></span> <span data-ttu-id="e11ca-193">Se richiesto, specificare le credenziali di dominio dell'amministratore cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="e11ca-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="e11ca-194">Il processo viene inviato e, nella pagina **My Jobs** (Processi), viene visualizzato l'ID del processo.</span><span class="sxs-lookup"><span data-stu-id="e11ca-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="e11ca-195">Per visualizzare i risultati del processo inviato, fare clic sull'ID del processo e scegliere **Visualizza attività** per visualizzare l'output del comando (in **Output**).</span><span class="sxs-lookup"><span data-stu-id="e11ca-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e11ca-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e11ca-196">Next steps</span></span>
* <span data-ttu-id="e11ca-197">Per inviare processi al cluster Azure, è anche possibile usare l' [API REST HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="e11ca-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="e11ca-198">Per inviare processi cluster da un client Linux, vedere l'esempio Python in [HPC Pack 2012 R2 SDK e codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="e11ca-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
