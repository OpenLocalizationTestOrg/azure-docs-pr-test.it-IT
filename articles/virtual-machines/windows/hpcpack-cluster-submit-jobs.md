---
title: aaaSubmit tooan di processi HPC Pack del cluster in Azure | Documenti Microsoft
description: Informazioni su come tooset backup un toosubmit del computer locale i processi cluster HPC Pack tooan in Azure
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
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="b4cc4-103">Inviare i processi HPC da un cluster di HPC Pack locale computer tooan distribuito in Azure</span><span class="sxs-lookup"><span data-stu-id="b4cc4-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b4cc4-104">Configurare un tooa di processi locali client computer toosubmit [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="b4cc4-105">Questo articolo illustra come tooset in un computer client locale strumenti toosubmit processo su cluster toohello HTTPS in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="b4cc4-106">In questo modo, più utenti di cluster possono inviare processi tooa basato su cloud cluster HPC Pack, ma senza la connessione diretta toohello macchina virtuale del nodo head o l'accesso a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Invio di un cluster di tooa processo in Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="b4cc4-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4cc4-108">Prerequisites</span></span>
* <span data-ttu-id="b4cc4-109">**Nodo head di HPC Pack distribuito in una macchina virtuale di Azure** -è consigliabile utilizzare strumenti automatizzati, ad esempio un [modello di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) o [script Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nodo head di toodeploy hello e cluster.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="b4cc4-110">È necessario il nome DNS hello del nodo head hello e credenziali di hello di un amministratore cluster per completare i passaggi di hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="b4cc4-111">**Computer client** : è necessario un computer client Windows o Windows server in grado di eseguire le utilità client di HPC Pack (vedere i [requisiti di sistema](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="b4cc4-112">Se si desidera solo portale web di HPC Pack hello toouse o processi toosubmit API REST, è possibile utilizzare tutti i computer client di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="b4cc4-113">**Supporto di installazione di HPC Pack** -tooinstall hello utilità client di HPC Pack, il pacchetto di installazione gratuito hello per la versione più recente di HPC Pack (HPC Pack 2012 R2) è disponibile il [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="b4cc4-114">Assicurarsi di scaricare hello stessa versione di HPC Pack installato nel nodo head hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="b4cc4-115">Passaggio 1: Installare e configurare i componenti web di hello nel nodo head hello</span><span class="sxs-lookup"><span data-stu-id="b4cc4-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="b4cc4-116">tooenable un cluster toohello di processi toosubmit di interfaccia REST su HTTPS, assicurarsi che i componenti web di HPC Pack hello siano configurati nel nodo head di HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="b4cc4-117">Se non sono già installati, installare i componenti web di hello eseguendo il file di installazione HpcWebComponents.msi hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="b4cc4-118">Quindi, configurare i componenti di hello eseguendo uno script di HPC PowerShell hello **set-hpcwebcomponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="b4cc4-119">Per le procedure dettagliate, vedere [installare i componenti Web di hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="b4cc4-120">Alcuni modelli di avvio rapido di Azure per HPC Pack installare e configurare i componenti web di hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="b4cc4-121">Se si utilizza hello [script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) cluster hello toocreate, è facoltativamente possibile installare e configurare i componenti web di hello come parte della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="b4cc4-122">**componenti web di hello tooinstall**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="b4cc4-123">Connessione macchina virtuale del nodo head toohello utilizzando hello credenziali di amministratore del cluster.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="b4cc4-124">Dalla cartella di installazione di HPC Pack hello, eseguire HpcWebComponents.msi nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="b4cc4-125">Seguire i passaggi hello nei componenti web di hello guidata tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="b4cc4-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="b4cc4-126">**componenti web di hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="b4cc4-127">Nel nodo head hello, avviare HPC PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="b4cc4-128">toochange toohello percorso della directory dello script di configurazione hello, hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="b4cc4-129">tooconfigure hello interfaccia REST e avviare hello servizio Web HPC, hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="b4cc4-130">Quando richiesto tooselect un certificato, scegliere il certificato di hello corrispondente toohello nome DNS pubblico del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="b4cc4-131">Ad esempio, se si distribuisce nodo head di hello macchina virtuale utilizzando il modello di distribuzione classica hello, nome certificato hello è simile a CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="b4cc4-132">Se si Usa modello di distribuzione di gestione risorse di hello, nome certificato hello simile CN =&lt;*HeadNodeDnsName*&gt;.&lt; *area*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4cc4-133">Selezionare il certificato in un secondo momento quando si invia nodo head toohello di processi da un computer locale.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="b4cc4-134">Non selezionare né configurare un certificato corrispondente al nome del computer del nodo head di hello nel dominio di Active Directory hello toohello (ad esempio CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="b4cc4-135">portale web di hello tooconfigure per l'invio di processi, hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="b4cc4-136">Al termine dell'esecuzione dello script hello, arrestare e riavviare il servizio Utilità di pianificazione processi HPC hello digitando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="b4cc4-137">Passaggio 2: Installare le utilità client di HPC Pack hello in un computer locale</span><span class="sxs-lookup"><span data-stu-id="b4cc4-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="b4cc4-138">Se si desidera utilità client di HPC Pack hello tooinstall nel computer in uso, scaricare i file di installazione di HPC Pack (installazione completa) dal hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="b4cc4-139">Quando si inizia installazione hello, scegliere l'opzione di installazione di hello per hello **utilità client di HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="b4cc4-140">nodo head di toohello processi toosubmit VM degli strumenti client di HPC Pack hello toouse, inoltre necessario un certificato dal nodo head hello tooexport e installarlo nel computer client hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="b4cc4-141">deve essere certificato Hello. Formato CER.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="b4cc4-142">**certificato di hello tooexport dal nodo head hello**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="b4cc4-143">Nel nodo head hello, aggiungere hello certificati snap-in tooa Microsoft Management Console per hello account Computer locale.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="b4cc4-144">Per i passaggi tooadd hello snap-in, vedere [aggiungere hello Snap-in certificati tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="b4cc4-145">Nella struttura della console hello espandere **certificati-Computer locale** > **personale**, quindi fare clic su **certificati**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="b4cc4-146">Individuare il certificato hello configurato per i componenti web di HPC Pack hello in [passaggio 1: installare e configurare i componenti web di hello nel nodo head hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (ad esempio CN =&lt;*HeadNodeDnsName* &gt;. n e t).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="b4cc4-147">Fare doppio clic su certificato hello e fare clic su **tutte le attività** > **esportare**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="b4cc4-148">In hello esportazione guidata certificati, fare clic su **Avanti**e assicurarsi che **No, non esportare la chiave privata di hello** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="b4cc4-149">Seguire hello rimanenti passaggi di hello guidata tooexport hello certificato DER con codifica binaria x. 509 (. Formato CER).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="b4cc4-150">**certificato di hello tooimport nel computer client hello**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="b4cc4-151">Copiare il certificato hello esportato da hello nodo head tooa cartella hello computer client.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="b4cc4-152">Nel computer client hello eseguire certmgr. msc.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="b4cc4-153">In Gestione certificati espandere **Certificati - Utente corrente** > **Autorità di certificazione principale attendibili**, fare clic con il pulsante destro del mouse su **Certificati**, quindi fare clic su **All Tasks** (Tutte le attività) > **Importa**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="b4cc4-154">In Importazione guidata certificati hello, fare clic su **Avanti** e seguire hello passaggi tooimport hello certificato esportato dal hello nodo head toohello archivio Autorità di certificazione radice attendibili.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="b4cc4-155">È possibile visualizzare un avviso di sicurezza, perché l'autorità di certificazione hello nel nodo head hello non viene riconosciuto dal computer client hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="b4cc4-156">A scopo di test, è possibile ignorare questo avviso e completamento importazione del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="b4cc4-157">Passaggio 3: Eseguire test processi nel cluster hello</span><span class="sxs-lookup"><span data-stu-id="b4cc4-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="b4cc4-158">la configurazione, riprovare i processi in esecuzione su hello cluster in Azure da hello tooverify locale computer.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="b4cc4-159">Ad esempio, è possibile utilizzare gli strumenti di HPC Pack GUI o i comandi della riga di comando toosubmit processi toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="b4cc4-160">È possibile utilizzare anche un processi toosubmit portale basato sul web.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="b4cc4-161">**toorun i comandi di invio processi nel computer client hello**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="b4cc4-162">In un computer client in cui sono installate utilità client di HPC Pack hello, avviare un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="b4cc4-163">Digitare un comando di esempio.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-163">Type a sample command.</span></span> <span data-ttu-id="b4cc4-164">Ad esempio, toolist tutti i processi nel cluster hello, digitare un comando di simili tooone di hello seguenti, in base al nome DNS completo hello del nodo head hello:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="b4cc4-165">oppure</span><span class="sxs-lookup"><span data-stu-id="b4cc4-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="b4cc4-166">Utilizzare hello nome DNS completo del nodo head hello, non hello indirizzo IP nell'URL dell'utilità di pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="b4cc4-167">Se si specifica l'indirizzo IP di hello, viene visualizzato un errore simile troppo "certificato server hello deve tooeither presentano una catena di trust o toobe inserito nell'archivio radice attendibile hello valida."</span><span class="sxs-lookup"><span data-stu-id="b4cc4-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="b4cc4-168">Quando richiesto, digitare il nome di utente hello (in formato hello &lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore di cluster HPC hello o un altro utente cluster configurato.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="b4cc4-169">È possibile scegliere toostore credenziali hello in locale per più operazioni del processo.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="b4cc4-170">Verrà visualizzato un elenco di processi.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-170">A list of jobs appears.</span></span>

<span data-ttu-id="b4cc4-171">**toouse Gestione processi HPC nel computer client hello**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="b4cc4-172">Se si non archiviano le credenziali di dominio per un utente del cluster in precedenza durante l'invio di un processo, è possibile aggiungere le credenziali di hello in Gestione credenziali.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="b4cc4-173">a.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-173">a.</span></span> <span data-ttu-id="b4cc4-174">Nel Pannello di controllo su computer client hello, avviare Gestione credenziali.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="b4cc4-175">b.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-175">b.</span></span> <span data-ttu-id="b4cc4-176">Fare clic su **Credenziali Windows** > **Aggiungi credenziali generiche**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="b4cc4-177">c.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-177">c.</span></span> <span data-ttu-id="b4cc4-178">Specificare l'indirizzo Internet hello (ad esempio https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler o https://&lt;HeadNodeDnsName&gt;.&lt; area&gt;.cloudapp.azure.com/HpcScheduler) e il nome utente hello (&lt;DomainName&gt;\\&lt;UserName&gt;) e la password dell'amministratore di cluster hello o un altro utente cluster configurato.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="b4cc4-179">Nel computer client hello, avviare Gestione processi HPC.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="b4cc4-180">In hello **Seleziona nodo Head** della finestra di dialogo tipo hello URL toohello nodo head in Azure (ad esempio https://&lt;HeadNodeDnsName&gt;. c o https://&lt;HeadNodeDnsName&gt;. &lt;area&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="b4cc4-181">Gestione processi HPC apre e visualizza un elenco di processi nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="b4cc4-182">**portale web di hello toouse in esecuzione nel nodo head hello**</span><span class="sxs-lookup"><span data-stu-id="b4cc4-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="b4cc4-183">Avviare un web browser nel computer client hello e immettere uno dei seguenti indirizzi, in base al nome DNS completo hello del nodo head hello hello:</span><span class="sxs-lookup"><span data-stu-id="b4cc4-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="b4cc4-184">oppure</span><span class="sxs-lookup"><span data-stu-id="b4cc4-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="b4cc4-185">In hello protezione della finestra di dialogo visualizzata digitare le credenziali di dominio hello del messaggio per l'amministratore cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="b4cc4-186">È anche possibile aggiungere altri utenti cluster in ruoli diversi.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="b4cc4-187">Vedere [Gestione degli utenti del cluster](https://technet.microsoft.com/library/ff919335.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="b4cc4-188">visualizzazione elenco dei processi toohello viene visualizzato il portale web di Hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="b4cc4-189">Fare clic su un processo di esempio che restituisce la stringa hello "Hello World" dal cluster hello, toosubmit **nuovo processo** nella navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="b4cc4-190">In hello **nuovo processo** pagina **dalle pagine di invio**, fare clic su **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="b4cc4-191">verrà visualizzata la pagina di invio processo Hello.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="b4cc4-192">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-192">Click **Submit**.</span></span> <span data-ttu-id="b4cc4-193">Se richiesto, fornire le credenziali di dominio hello del messaggio per l'amministratore cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="b4cc4-194">il processo di Hello viene inviato e viene visualizzato l'ID di processo hello hello **processi personali** pagina.</span><span class="sxs-lookup"><span data-stu-id="b4cc4-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="b4cc4-195">risultati di hello tooview hello del processo di cui è stata inviata, fare clic su ID di processo hello e quindi fare clic su **Visualizza attività** output del comando hello tooview (in **Output**).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4cc4-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4cc4-196">Next steps</span></span>
* <span data-ttu-id="b4cc4-197">È inoltre possibile inviare i processi toohello cluster Azure con hello [API REST di HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="b4cc4-198">Se si desidera toosubmit i processi di cluster da un client Linux, vedere hello Python sample in hello [HPC Pack 2012 R2 SDK e codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="b4cc4-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
