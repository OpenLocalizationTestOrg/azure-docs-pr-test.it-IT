---
title: "aaaUse PowerShell tooCreate una macchina virtuale con una modalità Server di Report nativa | Documenti Microsoft"
description: "In questo argomento vengono descritte e illustrate distribuzione hello e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="0d53c-103">Utilizzare PowerShell tooCreate un Azure VM con un Server in modalità nativa Report</span><span class="sxs-lookup"><span data-stu-id="0d53c-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0d53c-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d53c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d53c-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0d53c-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="0d53c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="0d53c-107">In questo argomento vengono descritte e illustrate distribuzione hello e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d53c-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="0d53c-108">Hello passaggi di questo utilizzo di documento, una combinazione di macchina virtuale di hello toocreate passaggi manuali e script di Windows PowerShell tooconfigure Reporting Services su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="0d53c-109">script di configurazione Hello include l'apertura di una porta del firewall per HTTP o HTTPs.</span><span class="sxs-lookup"><span data-stu-id="0d53c-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="0d53c-110">Se non è necessario **HTTPS** nel server di report, hello **saltare il passaggio 2**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="0d53c-111">Dopo aver creato hello VM nel passaggio 1, passare toohello sezione utilizza script tooconfigure hello server di rapporti e HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d53c-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="0d53c-112">Dopo l'esecuzione di script hello, il server di report di hello è toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="0d53c-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="0d53c-113">Prerequisiti e presupposti</span><span class="sxs-lookup"><span data-stu-id="0d53c-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="0d53c-114">**Sottoscrizione di Azure**: verificare il numero di core disponibili nella sottoscrizione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="0d53c-115">Se si crea una dimensione della macchina virtuale consigliata hello **A3**, è necessario **4** core disponibili.</span><span class="sxs-lookup"><span data-stu-id="0d53c-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="0d53c-116">Se si usa la dimensione di macchina virtuale **A2**, sono necessari **2** core disponibili.</span><span class="sxs-lookup"><span data-stu-id="0d53c-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="0d53c-117">limite di core hello tooverify della sottoscrizione, in hello portale di Azure classico, fare clic su impostazioni nel riquadro sinistro di hello e quindi fare clic su utilizzo nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="0d53c-118">tooincrease hello quota core, contatta [supporto Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="0d53c-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="0d53c-119">Per informazioni sulle dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d53c-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="0d53c-120">**Scripting di Windows PowerShell**: argomento hello si presuppone una conoscenza di base di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d53c-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="0d53c-121">Per ulteriori informazioni sull'utilizzo di Windows PowerShell, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="0d53c-122">Avvio di Windows PowerShell in Windows Server</span><span class="sxs-lookup"><span data-stu-id="0d53c-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="0d53c-123">Introduzione a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d53c-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="0d53c-124">Passaggio 1: Eseguire il provisioning di una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d53c-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="0d53c-125">Sfoglia toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0d53c-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="0d53c-126">Fare clic su **macchine virtuali** nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![macchine virtuali di microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="0d53c-128">Fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-128">Click **New**.</span></span>
   
    ![pulsante nuovo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="0d53c-130">Fare clic su **Da raccolta**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-130">Click **From Gallery**.</span></span>
   
    ![nuova macchina virtuale dalla raccolta](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="0d53c-132">Fare clic su **SQL Server 2014 RTM Standard – Windows Server 2012 R2** e quindi fare clic su toocontinue freccia hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="0d53c-134">Se è necessario funzionalità sottoscrizioni guidate dai dati di Reporting Services hello, scegliere **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="0d53c-135">Per ulteriori informazioni sulle edizioni di SQL Server e il supporto di funzionalità, vedere [funzionalità supportate dalle edizioni di SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="0d53c-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="0d53c-136">In hello **configurazione della macchina virtuale** pagina, modificare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="0d53c-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="0d53c-137">Se è presente più di **data di rilascio versione**, selezionare hello versione più recente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="0d53c-138">**Nome della macchina virtuale**: nome del computer hello viene anche utilizzato nella pagina Configurazione successiva hello come hello predefinito nome DNS servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="0d53c-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="0d53c-139">nome DNS Hello deve essere univoco tra hello servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d53c-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="0d53c-140">Provare a configurare hello macchina virtuale con un nome di computer che descrive quale hello macchina virtuale viene utilizzata per.</span><span class="sxs-lookup"><span data-stu-id="0d53c-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="0d53c-141">Ad esempio, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="0d53c-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="0d53c-142">**Piano**: Standard.</span><span class="sxs-lookup"><span data-stu-id="0d53c-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="0d53c-143">**Dimensioni: A3** hello consiglia di dimensioni delle macchine Virtuali per carichi di lavoro di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0d53c-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="0d53c-144">Se una macchina virtuale viene utilizzata solo come server di report, è sufficiente una dimensione A2, a meno che il server di report hello di cui si verifichi un elevato carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0d53c-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="0d53c-145">Per informazioni sui prezzi delle macchine virtuali, vedere [Macchine virtuali - Prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="0d53c-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="0d53c-146">**Nuovo nome utente**: nome hello specificato viene creato come amministratore in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="0d53c-147">**Nuova password** e **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="0d53c-148">Questa password viene utilizzata per il nuovo account di amministratore hello e, è consigliabile che utilizzare una password complessa.</span><span class="sxs-lookup"><span data-stu-id="0d53c-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="0d53c-149">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-149">Click **Next**.</span></span> <span data-ttu-id="0d53c-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="0d53c-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="0d53c-151">Nella pagina successiva di hello, modificare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="0d53c-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="0d53c-152">**Servizio cloud**: selezionare **Crea un nuovo servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="0d53c-153">**Nome DNS del servizio cloud**: si tratta di nome DNS pubblico hello di hello servizio Cloud associato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="0d53c-154">nome predefinito Hello è hello digitato nel nome della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="0d53c-155">Se nei passaggi successivi di argomento hello, si crea un certificato SSL attendibile e il nome DNS hello è utilizzato per il valore di hello di hello "**rilasciato a**" del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="0d53c-156">**Affinità di area/gruppo/rete virtuale**: scegliere gli utenti finali hello area più vicini tooyour.</span><span class="sxs-lookup"><span data-stu-id="0d53c-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="0d53c-157">**Account di archiviazione**: usare un account di archiviazione generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="0d53c-158">**Set di disponibilità**: nessuno.</span><span class="sxs-lookup"><span data-stu-id="0d53c-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="0d53c-159">**Gli endpoint** Keep hello **Desktop remoto** e **PowerShell** endpoint e quindi aggiungere l'endpoint HTTP o HTTPS, a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="0d53c-160">**HTTP**: hello predefinito porte pubbliche e private sono **80**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="0d53c-161">Si noti che se si utilizza una porta privata diversa dalla 80, modificare **$HTTPport = 80** nello script http hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="0d53c-162">**HTTPS**: hello predefinito porte pubbliche e private sono **443**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="0d53c-163">Una procedura consigliata è toochange porta privata di hello e configurare il firewall e hello report server toouse hello porta privata.</span><span class="sxs-lookup"><span data-stu-id="0d53c-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="0d53c-164">Per ulteriori informazioni sugli endpoint, vedere [come configurare la comunicazione con una macchina virtuale tooSet](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d53c-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="0d53c-165">Si noti che se si usa una porta diversa dalla 443, modificare il parametro hello **$HTTPsport = 443** in hello script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0d53c-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="0d53c-166">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-166">Click next .</span></span> ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="0d53c-168">Hello ultima pagina della procedura guidata hello, mantenere l'impostazione predefinita di hello **installazione agente della macchina virtuale hello** selezionato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="0d53c-169">Hello passaggi in questo argomento non usano agente VM hello ma se si prevede di tookeep questa macchina virtuale, estensioni e agente VM hello consentirà tooenhance he CM.</span><span class="sxs-lookup"><span data-stu-id="0d53c-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="0d53c-170">Per ulteriori informazioni sull'agente VM hello, vedere [agente VM ed estensioni-parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="0d53c-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="0d53c-171">Uno dei hello estensioni predefinite installate e in esecuzione è l'estensione "BGINFO" hello che visualizza sul desktop VM hello, informazioni di sistema, ad esempio l'indirizzo IP interno e libera spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="0d53c-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="0d53c-172">Fare clic su Completa.</span><span class="sxs-lookup"><span data-stu-id="0d53c-172">Click complete .</span></span> ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="0d53c-174">Hello **stato** di macchina virtuale viene visualizzato come hello **avvio in corso (Provisioning)** durante il processo di provisioning hello e viene visualizzato come **esecuzione** quando hello macchina virtuale è disponibile e pronta toouse.</span><span class="sxs-lookup"><span data-stu-id="0d53c-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="0d53c-175">Passaggio 2: Creare un certificato del server</span><span class="sxs-lookup"><span data-stu-id="0d53c-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="0d53c-176">Se non si usa HTTPS nel server di report hello, è possibile **saltare il passaggio 2** e passare la sezione toohello **usare HTTP e server di report di script tooconfigure hello**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="0d53c-177">Utilizzare hello HTTP script tooquickly configurare il server di report hello e report hello server sarà toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="0d53c-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="0d53c-178">In ordine toouse HTTPS su hello VM, è necessario un certificato SSL attendibile.</span><span class="sxs-lookup"><span data-stu-id="0d53c-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="0d53c-179">A seconda dello scenario, è possibile utilizzare uno dei seguenti due metodi hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="0d53c-180">Un certificato SSL valido emesso da un'autorità di certificazione (CA) e ritenuto attendibile da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d53c-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="0d53c-181">i certificati radice della CA Hello sono necessari toobe distribuiti tramite hello programma Microsoft Root Certificate.</span><span class="sxs-lookup"><span data-stu-id="0d53c-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="0d53c-182">Per ulteriori informazioni su questo programma, vedere [Windows e Windows Phone 8 SSL programma Root Certificate (autorità di certificazione membro)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e [toohello introduzione programma Microsoft Root Certificate](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="0d53c-183">Un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-183">A self-signed certificate.</span></span> <span data-ttu-id="0d53c-184">I certificati autofirmati non sono consigliati per gli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="0d53c-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="0d53c-185">toouse un certificato creato da un'autorità di certificati attendibili (CA)</span><span class="sxs-lookup"><span data-stu-id="0d53c-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="0d53c-186">**Richiedere un certificato server per il sito Web di hello da un'autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="0d53c-187">È possibile utilizzare Gestione guidata certificati Server Web hello entrambi toogenerate un file di richiesta di certificato (Certreq.txt) inviare tooa autorità di certificazione o toogenerate una richiesta per un'autorità di certificazione online.</span><span class="sxs-lookup"><span data-stu-id="0d53c-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="0d53c-188">Ad esempio, Servizi certificati Microsoft in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="0d53c-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="0d53c-189">A seconda di livello hello garanzia di identificazione offerto dal certificato del server, è alcuni mesi tooseveral giorni tooapprove autorità di certificazione hello la richiesta e inviare un file di certificato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="0d53c-190">Per ulteriori informazioni sulla richiesta di un server di certificati, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="0d53c-191">Usare [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="0d53c-192">Sicurezza strumenti tooAdminister Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="0d53c-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="0d53c-193">Strumenti di sicurezza tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0d53c-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="0d53c-194">Hello **rilasciato a** campo di hello attendibile il certificato SSL deve essere hello stesso come hello **nome DNS del servizio Cloud** usati per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="0d53c-195">**Installare il certificato di server hello nel server Web hello**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="0d53c-196">in questo caso, server Web Hello è hello macchina virtuale che ospita il server di report di hello e sito Web di hello viene creato nei passaggi successivi quando si configura Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="0d53c-197">Per ulteriori informazioni sull'installazione certificato server hello sul server Web hello utilizzando lo snap-in MMC certificato hello, vedere [installare un certificato Server](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="0d53c-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="0d53c-198">Se si desidera toouse hello script incluso in questo argomento, il server di report tooconfigure hello, hello valore certificati hello **identificazione personale** è richiesto come parametro dello script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="0d53c-199">Nella sezione hello Avanti per informazioni dettagliate su come tooobtain hello identificazione personale del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="0d53c-200">Assegnare server di report toohello certificato server hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="0d53c-201">assegnazione di Hello è completata nella sezione successiva di hello quando si configura il server di report hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="0d53c-202">hello toouse certificato autofirmato macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="0d53c-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="0d53c-203">Un certificato autofirmato è stato creato su hello VM quando è stato eseguito il provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="0d53c-204">certificato Hello è hello stesso nome come nome DNS VM hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="0d53c-205">Errori di certificato tooavoid ordine, è necessario che il certificato hello è considerato attendibile in hello macchina virtuale stessa e anche da tutti gli utenti del sito hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="0d53c-206">CA radice hello tootrust del certificato hello in hello macchina virtuale locale, aggiungere hello certificato toohello **autorità di certificazione radice attendibili**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="0d53c-207">di seguito Hello è un riepilogo dei passaggi di hello necessari.</span><span class="sxs-lookup"><span data-stu-id="0d53c-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="0d53c-208">Per informazioni dettagliate su come tootrust hello autorità di certificazione, vedere [installare un certificato Server](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="0d53c-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="0d53c-209">Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="0d53c-210">A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="0d53c-212">Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="0d53c-213">In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="0d53c-215">Eseguire mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="0d53c-215">Run mmc.exe.</span></span> <span data-ttu-id="0d53c-216">Per ulteriori informazioni, vedere [procedura: visualizzare certificati con hello Snap-in MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="0d53c-217">In un'applicazione console hello **File** menu, aggiungere hello **certificati** snap-in, selezionare **Account Computer** quando richiesto e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="0d53c-218">Selezionare **Computer locale** toomanage e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="0d53c-219">Fare clic su **Ok** e quindi espandere hello **certificati - personale** nodi e quindi fare clic su **certificati**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="0d53c-220">Hello certificato è citato dopo il nome DNS hello di hello VM e termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="0d53c-221">Nome del certificato hello destro e fare clic su **copia**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="0d53c-222">Espandere hello **autorità di certificazione radice attendibili** nodo e quindi rapida **certificati** e quindi fare clic su **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="0d53c-223">toovalidate, doppio clic sul nome certificato hello in **autorità di certificazione radice attendibili** e verificare che non siano presenti errori e viene visualizzato il certificato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="0d53c-224">Se si desidera toouse hello HTTPS script incluso in questo argomento, il server di report tooconfigure hello, hello valore certificati hello **identificazione personale** è richiesto come parametro dello script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="0d53c-225">**valore di identificazione personale hello tooget**, completare la procedura seguente hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="0d53c-226">È inoltre disponibile un'identificazione digitale di PowerShell esempio tooretrieve hello nella sezione [utilizzano server di report di script tooconfigure hello e HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="0d53c-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="0d53c-227">Fare doppio clic sul nome di hello del certificato di hello, ad esempio ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0d53c-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="0d53c-228">Fare clic su hello **dettagli** scheda.</span><span class="sxs-lookup"><span data-stu-id="0d53c-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="0d53c-229">Fare clic su **Identificazione personale**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-229">Click **Thumbprint**.</span></span> <span data-ttu-id="0d53c-230">il valore di Hello dell'identificazione digitale hello viene visualizzato nel campo dei dettagli hello, ad esempio a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9C 2C fb 2f.</span><span class="sxs-lookup"><span data-stu-id="0d53c-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="0d53c-231">Copiare l'identificazione personale hello e salvare il valore di hello per un momento successivo o modificare script hello adesso.</span><span class="sxs-lookup"><span data-stu-id="0d53c-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="0d53c-232">(*) Prima di eseguire script hello, rimuovere hello gli spazi tra coppie di hello di valori.</span><span class="sxs-lookup"><span data-stu-id="0d53c-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="0d53c-233">Ad esempio identificazione personale hello annotata in precedenza sarebbe a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="0d53c-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="0d53c-234">Assegnare server di report toohello certificato server hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="0d53c-235">assegnazione di Hello è completata nella sezione successiva di hello quando si configura il server di report hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="0d53c-236">Se si utilizza un certificato SSL autofirmato, nome hello hello certificato corrisponde già a hostname hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="0d53c-237">Pertanto, hello DNS della macchina hello è già registrato globalmente e sono accessibili da qualsiasi client.</span><span class="sxs-lookup"><span data-stu-id="0d53c-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="0d53c-238">Passaggio 3: Configurare hello Server di Report</span><span class="sxs-lookup"><span data-stu-id="0d53c-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="0d53c-239">In questa sezione illustra la configurazione hello VM come un server di report in modalità nativa di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="0d53c-240">È possibile utilizzare uno dei seguenti server di report di metodi tooconfigure hello hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="0d53c-241">Utilizzare server di report di hello script tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="0d53c-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="0d53c-242">Utilizzare Gestione configurazione tooConfigure hello Server di Report.</span><span class="sxs-lookup"><span data-stu-id="0d53c-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="0d53c-243">Per istruzioni più dettagliate, vedere la sezione hello [toohello connessione macchina virtuale e avviare Gestione configurazione Reporting Services di hello](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="0d53c-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="0d53c-244">**Nota sull'autenticazione:** l'autenticazione di Windows hello metodo di autenticazione consigliato ed è l'autenticazione di Reporting Services predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="0d53c-245">Solo gli utenti che sono configurati su hello VM possono accedere a Reporting Services e assegnato tooReporting ruoli di servizi.</span><span class="sxs-lookup"><span data-stu-id="0d53c-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="0d53c-246">Utilizzare server di report di script tooconfigure hello e HTTP</span><span class="sxs-lookup"><span data-stu-id="0d53c-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="0d53c-247">toouse hello Windows PowerShell script tooconfigure hello server di report, hello completo alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="0d53c-248">configurazione di Hello include HTTP, HTTPS non:</span><span class="sxs-lookup"><span data-stu-id="0d53c-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="0d53c-249">Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="0d53c-250">A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="0d53c-252">Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="0d53c-253">In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="0d53c-255">In hello macchina virtuale, aprire **Windows PowerShell ISE** con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="0d53c-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="0d53c-256">Hello PowerShell ISE è installato per impostazione predefinita in Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="0d53c-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="0d53c-257">È consigliabile che usare hello ISE anziché una finestra standard di Windows PowerShell, che può incollare script hello in hello ISE, modificare script hello e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="0d53c-258">In Windows PowerShell ISE, fare clic su hello **vista** menu e quindi fare clic su **Mostra riquadro di Script**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="0d53c-259">Copiare lo script seguente hello e incollare hello script nel riquadro di script di Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="0d53c-260">Se hello VM è stato creato con una porta HTTP diversa dalla 80, modificare il parametro hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="0d53c-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="0d53c-261">script Hello è attualmente configurato per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="0d53c-262">Se si desidera script hello toorun per Reporting Services, modificare lo spazio dei nomi di hello percorso toohello parte versione hello troppo "v11" nell'istruzione hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="0d53c-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="0d53c-263">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-263">Run hello script.</span></span>

<span data-ttu-id="0d53c-264">**Convalida**: tooverify che funzionalità di server di report di base hello sia operativa, vedere hello [configurazione hello verificare](#verify-the-configuration) sezione più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0d53c-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="0d53c-265">Utilizzare server di report di script tooconfigure hello e HTTPS</span><span class="sxs-lookup"><span data-stu-id="0d53c-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="0d53c-266">toouse Windows PowerShell tooconfigure hello server di report, hello completo alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="0d53c-267">configurazione di Hello include HTTPS, ma non HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d53c-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="0d53c-268">Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="0d53c-269">A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="0d53c-271">Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="0d53c-272">In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="0d53c-274">In hello macchina virtuale, aprire **Windows PowerShell ISE** con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="0d53c-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="0d53c-275">Hello PowerShell ISE è installato per impostazione predefinita in Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="0d53c-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="0d53c-276">È consigliabile che usare hello ISE anziché una finestra standard di Windows PowerShell, che può incollare script hello in hello ISE, modificare script hello e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="0d53c-277">tooenable l'esecuzione di script, eseguire il comando di Windows PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="0d53c-278">È quindi possibile eseguire i seguenti criteri hello tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="0d53c-279">In **Windows PowerShell ISE**, fare clic su hello **vista** menu e quindi fare clic su **Mostra riquadro di Script**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="0d53c-280">Copiare hello seguente script e incollarlo nel riquadro di script di Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="0d53c-281">Modificare hello **$certificatehash** parametro nello script hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="0d53c-282">Si tratta di un parametro **obbligatorio** .</span><span class="sxs-lookup"><span data-stu-id="0d53c-282">This is a **required** parameter.</span></span> <span data-ttu-id="0d53c-283">Se non è stato salvato il valore di certificato hello nei passaggi precedenti hello, utilizzare uno dei seguenti valore hash del certificato hello toocopy metodi di identificazione personale certificati hello hello.:</span><span class="sxs-lookup"><span data-stu-id="0d53c-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="0d53c-284">Nella macchina virtuale hello, aprire Windows PowerShell ISE ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d53c-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="0d53c-285">output di Hello avrà un aspetto simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="0d53c-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="0d53c-286">Se lo script di hello restituisce una riga vuota, hello macchina virtuale non dispone di un certificato configurato, ad esempio, vedere la sezione hello [toouse hello certificato autofirmato macchine virtuali](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="0d53c-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="0d53c-287">OPPURE</span><span class="sxs-lookup"><span data-stu-id="0d53c-287">OR</span></span>
   * <span data-ttu-id="0d53c-288">Hello macchina virtuale eseguire mmc.exe e quindi aggiungere hello **certificati** snap-in.</span><span class="sxs-lookup"><span data-stu-id="0d53c-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="0d53c-289">In hello **autorità di certificazione radice attendibili** nodo fare doppio clic sul nome del certificato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="0d53c-290">Se si utilizza hello autofirmato di hello macchina virtuale, il certificato di hello denominato in base al nome DNS hello di hello macchina virtuale e termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="0d53c-291">Fare clic su hello **dettagli** scheda.</span><span class="sxs-lookup"><span data-stu-id="0d53c-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="0d53c-292">Fare clic su **Identificazione personale**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-292">Click **Thumbprint**.</span></span> <span data-ttu-id="0d53c-293">il valore di Hello dell'identificazione digitale hello viene visualizzato nel campo dei dettagli hello, ad esempio af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="0d53c-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="0d53c-294">**Prima di eseguire script hello**, rimuovere gli spazi tra coppie di hello di valori hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="0d53c-295">Ad esempio, af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="0d53c-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="0d53c-296">Modificare hello **$httpsport** parametro:</span><span class="sxs-lookup"><span data-stu-id="0d53c-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="0d53c-297">Se si utilizza la porta 443 per endpoint HTTPS hello, quindi non è necessario tooupdate questo parametro nello script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="0d53c-298">In caso contrario, utilizzare il valore di porta hello selezionato durante la configurazione di endpoint privato HTTPS hello in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="0d53c-299">Modificare hello **$DNSName** parametro:</span><span class="sxs-lookup"><span data-stu-id="0d53c-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="0d53c-300">script Hello è configurato per un certificato con caratteri jolly $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="0d53c-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="0d53c-301">Se si esegue l'operazione non tooconfigure desiderata per un binding al certificato con caratteri jolly, commento $DNSName = "+"e abilitare la seguente riga hello completo $DNSNAme il riferimento, # # $DNSName="$server.cloudapp.net hello".</span><span class="sxs-lookup"><span data-stu-id="0d53c-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="0d53c-302">Modificare il valore di hello $DNSName se non si desidera il nome DNS della macchina virtuale hello di toouse per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="0d53c-303">Se si usa il parametro hello, certificato hello è necessario utilizzare anche il nome e si registra il nome di hello a livello globale in un server DNS.</span><span class="sxs-lookup"><span data-stu-id="0d53c-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="0d53c-304">script Hello è attualmente configurato per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="0d53c-305">Se si desidera script hello toorun per Reporting Services, modificare lo spazio dei nomi di hello percorso toohello parte versione hello troppo "v11" nell'istruzione hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="0d53c-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="0d53c-306">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-306">Run hello script.</span></span>

<span data-ttu-id="0d53c-307">**Convalida**: tooverify che funzionalità di server di report di base hello sia operativa, vedere hello [configurazione hello verificare](#verify-the-connection) sezione più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0d53c-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="0d53c-308">binding al certificato hello tooverify aprire un prompt dei comandi con privilegi amministrativi e quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d53c-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="0d53c-309">il risultato di Hello includerà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="0d53c-310">Utilizzare Gestione configurazione tooConfigure hello Server di Report</span><span class="sxs-lookup"><span data-stu-id="0d53c-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="0d53c-311">Se non si desidera toorun script di PowerShell di hello tooconfigure server di report di hello, seguire i passaggi di hello in questa sezione toouse hello Reporting Services in modalità nativa tooconfigure hello report server di configuration manager.</span><span class="sxs-lookup"><span data-stu-id="0d53c-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="0d53c-312">Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="0d53c-313">Usa il nome utente hello e la password configurati durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="0d53c-315">Eseguire Windows update e installare gli aggiornamenti toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="0d53c-316">Se è necessario un riavvio della macchina virtuale hello, riavviare hello macchina virtuale e riconnettersi toohello macchina virtuale dal portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="0d53c-317">Dal menu di avvio hello in hello macchina virtuale, digitare **Reporting Services** e aprire **Gestione configurazione Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="0d53c-318">Lasciare i valori predefiniti di hello per **nome Server** e **istanza Server di Report**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="0d53c-319">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-319">Click **Connect**.</span></span>
5. <span data-ttu-id="0d53c-320">Nel riquadro di sinistra hello, fare clic su **URL servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="0d53c-321">Per impostazione predefinita, Reporting Services è configurato per la porta HTTP 80 con IP "Tutti assegnati".</span><span class="sxs-lookup"><span data-stu-id="0d53c-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="0d53c-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="0d53c-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="0d53c-323">In **certificato SSL**: hello selezionare certificato toouse, ad esempio [nome macchina virtuale]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0d53c-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="0d53c-324">Se non sono elencati certificati, vedere la sezione hello **passaggio 2: creare un certificato Server** per informazioni su come tooinstall e attendibilità hello certificato su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="0d53c-325">In **Porta SSL**scegliere 443.</span><span class="sxs-lookup"><span data-stu-id="0d53c-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="0d53c-326">Se è configurato l'endpoint privato HTTPS hello in hello macchina virtuale con una porta privata diversa, utilizzare quel valore.</span><span class="sxs-lookup"><span data-stu-id="0d53c-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="0d53c-327">Fare clic su **applica** e attendere toocomplete operazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="0d53c-328">Nel riquadro di sinistra hello, fare clic su **Database**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="0d53c-329">Fare clic su **Modifica database**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="0d53c-330">Fare clic su **Crea un nuovo database del server di report** e quindi su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="0d53c-331">Lasciare l'impostazione predefinita hello **nome Server**: hello VM assegnare il nome e valore predefinito di hello **tipo di autenticazione** come **utente corrente** – **lasicurezzaintegrata**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="0d53c-332">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-332">Click **Next**.</span></span>
   4. <span data-ttu-id="0d53c-333">Lasciare l'impostazione predefinita hello **nome del Database** come **ReportServer** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="0d53c-334">Lasciare l'impostazione predefinita hello **tipo di autenticazione** come **credenziali del servizio** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="0d53c-335">Fare clic su **Avanti** su hello **riepilogo** pagina.</span><span class="sxs-lookup"><span data-stu-id="0d53c-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="0d53c-336">Una volta completata la configurazione hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="0d53c-337">Nel riquadro di sinistra hello, fare clic su **URL gestione Report**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="0d53c-338">Lasciare l'impostazione predefinita hello **Directory virtuale** come **report** e fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="0d53c-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="0d53c-339">Fare clic su **uscita** tooclose hello Gestione configurazione Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="0d53c-340">Passaggio 4: Aprire la porta di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="0d53c-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="0d53c-341">Se si usa uno hello script tooconfigure hello server di report, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0d53c-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="0d53c-342">una porta del firewall hello tooopen passaggio è incluso uno script di Hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="0d53c-343">valore predefinito di Hello è la porta 80 per HTTP e la porta 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0d53c-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="0d53c-344">tooconnect in modalità remota tooReport Manager o hello Report Server nella macchina virtuale hello, un Endpoint TCP è obbligatorio in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="0d53c-345">È necessario tooopen hello stessa porta nel firewall della macchina virtuale di hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="0d53c-346">Hello endpoint è stato creato quando è stato eseguito il provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="0d53c-347">In questa sezione fornisce informazioni di base in modo tooopen hello porta del firewall.</span><span class="sxs-lookup"><span data-stu-id="0d53c-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="0d53c-348">Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d53c-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="0d53c-349">Se si utilizza server di report hello tooconfigure hello script, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="0d53c-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="0d53c-350">una porta del firewall hello tooopen passaggio è incluso uno script di Hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="0d53c-351">Se è configurata una porta privata per HTTPS diversa dalla 443, modificare hello lo script seguente in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="0d53c-352">porta tooopen **443** su hello Windows Firewall, completare i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="0d53c-353">Aprire una finestra di Windows PowerShell con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="0d53c-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="0d53c-354">Se si utilizza una porta diversa dalla 443 durante la configurazione di endpoint HTTPS hello in hello macchina virtuale, aggiornare la porta di hello in hello comando seguente e quindi eseguire il comando di hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="0d53c-355">Al termine del comando di hello, **Ok** viene visualizzato nel prompt dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="0d53c-356">tooverify che porta hello è aperto, aprire una finestra di Windows PowerShell e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d53c-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="0d53c-357">Verificare la configurazione di hello</span><span class="sxs-lookup"><span data-stu-id="0d53c-357">Verify hello configuration</span></span>
<span data-ttu-id="0d53c-358">tooverify che la funzionalità server di report di base hello ora sia in esecuzione, aprire il browser con privilegi amministrativi e quindi Sfoglia toohello seguenti report di gestione report server URL:</span><span class="sxs-lookup"><span data-stu-id="0d53c-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="0d53c-359">In hello VM, visitare toohello URL server di report:</span><span class="sxs-lookup"><span data-stu-id="0d53c-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="0d53c-360">In hello VM, visitare toohello URL di gestione report:</span><span class="sxs-lookup"><span data-stu-id="0d53c-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="0d53c-361">Dal computer locale, passare toohello **remoto** Gestione report in VM hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="0d53c-362">Aggiornare il nome DNS hello in hello seguente esempio come appropriato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="0d53c-363">Quando viene richiesto di immettere una password, utilizzare le credenziali di amministratore hello creato quando è stato eseguito il provisioning hello VM.</span><span class="sxs-lookup"><span data-stu-id="0d53c-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="0d53c-364">nome utente di Hello è hello [dominio]\[nome utente] formato, dove dominio hello è hello VM nome, ad esempio ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="0d53c-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="0d53c-365">Se non si utilizza HTTP**S**, rimuovere hello **s** nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="0d53c-366">Nella sezione hello Avanti per informazioni sulla creazione di altri utenti nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="0d53c-367">Dal computer locale, passare toohello URL del server di report remoto.</span><span class="sxs-lookup"><span data-stu-id="0d53c-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="0d53c-368">Aggiornare il nome DNS hello in hello seguente esempio come appropriato.</span><span class="sxs-lookup"><span data-stu-id="0d53c-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="0d53c-369">Se non si utilizza HTTPS, è possibile rimuovere hello s hello URL.</span><span class="sxs-lookup"><span data-stu-id="0d53c-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="0d53c-370">Creare utenti e assegnare ruoli</span><span class="sxs-lookup"><span data-stu-id="0d53c-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="0d53c-371">Dopo la configurazione e la verifica hello server di report, un'attività amministrativa comune è toocreate uno o più utenti e assegnare i ruoli di servizi tooReporting di utenti.</span><span class="sxs-lookup"><span data-stu-id="0d53c-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="0d53c-372">Per ulteriori informazioni, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="0d53c-373">Creare un account utente locale</span><span class="sxs-lookup"><span data-stu-id="0d53c-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="0d53c-374">[Concedere l'accesso utente tooa il Server di Report (gestione Report)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="0d53c-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="0d53c-375">Creare e gestire le assegnazioni di ruoli</span><span class="sxs-lookup"><span data-stu-id="0d53c-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="0d53c-376">tooCreate e pubblicare report toohello macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d53c-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="0d53c-377">Hello nella tabella seguente vengono riepilogati alcuni dei report esistenti hello opzioni toopublish disponibile da un server di report locale computer toohello ospitato in hello macchina virtuale di Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="0d53c-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="0d53c-378">**Lo script RS.exe**: utilizzare RS.exe script toocopy gli elementi del report da e tooyour server di report esistente macchina virtuale di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0d53c-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="0d53c-379">Per ulteriori informazioni, vedere la sezione hello "modalità nativa tooNative modalità-macchina virtuale di Microsoft Azure" in [Sample Reporting Services rs.exe Script tooMigrate contenuto tra server di Report](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="0d53c-380">**Generatore report**: macchina virtuale di hello inclusa hello-versione ClickOnce di Generatore Report di Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0d53c-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="0d53c-381">hello Generatore Report di toostart prima volta sulla macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="0d53c-382">Avviare il browser con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="0d53c-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="0d53c-383">Gestione tooreport sulla macchina virtuale hello e fare clic su **Generatore Report** nella barra multifunzione hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="0d53c-384">Per altre informazioni, vedere [Installazione, disinstallazione e supporto di Generatore report](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="0d53c-385">**SQL Server Data Tools: Macchina virtuale**: se hello VM è stato creato con SQL Server 2012 e SQL Server Data Tools sia installato nella macchina virtuale hello e può essere utilizzato toocreate **progetti Server di Report** e report sulla hello virtuale macchina.</span><span class="sxs-lookup"><span data-stu-id="0d53c-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="0d53c-386">SQL Server Data Tools è possibile pubblicare server di report di toohello hello report sulla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="0d53c-387">Se è stato creato con SQL server 2014 hello VM, è possibile installare SQL Server Data Tools - BI per visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d53c-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="0d53c-388">Per ulteriori informazioni, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="0d53c-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="0d53c-389">Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0d53c-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="0d53c-390">Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="0d53c-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="0d53c-391">SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="0d53c-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="0d53c-392">**SQL Server Data Tools - Remoto**: nel computer locale creare un progetto di Reporting Services in SQL Server Data Tools contenente i report di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="0d53c-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="0d53c-393">Configurare l'URL del servizio web tooconnect toohello hello progetto.</span><span class="sxs-lookup"><span data-stu-id="0d53c-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![proprietà del progetto ssdt per un progetto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="0d53c-395">**Utilizzare script**: utilizzare contenuto del server di report toocopy di script.</span><span class="sxs-lookup"><span data-stu-id="0d53c-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="0d53c-396">Per ulteriori informazioni, vedere [Sample Reporting Services rs.exe Script tooMigrate contenuto tra server di Report](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="0d53c-397">Ridurre i costi se non si utilizza hello VM</span><span class="sxs-lookup"><span data-stu-id="0d53c-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="0d53c-398">toominimize addebiti per le macchine virtuali di Azure quando non è in uso, è stato chiuso hello macchina virtuale dal portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="0d53c-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="0d53c-399">Se si utilizzano opzioni di risparmio energia di Windows hello all'interno di un tooshut VM verso il basso hello VM, viene comunque addebitato hello stesso importo per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0d53c-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="0d53c-400">gli addebiti tooreduce, è necessario tooshut hello VM nel portale di Azure classico hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="0d53c-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="0d53c-401">Se non è più necessario hello VM, ricordare di hello toodelete VM e hello spese di archiviazione tooavoid file VHD associato. Per ulteriori informazioni, vedere la sezione di hello domande frequenti al [dettagli prezzi-macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="0d53c-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="0d53c-402">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="0d53c-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="0d53c-403">Risorse</span><span class="sxs-lookup"><span data-stu-id="0d53c-403">Resources</span></span>
* <span data-ttu-id="0d53c-404">Per contenuti analoghi relativi tooa distribuzione a server singolo di SQL Server Business Intelligence e SharePoint 2013, vedere [tooCreate utilizzare Windows PowerShell una macchina virtuale Azure con SQL Server BI e SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="0d53c-405">Per simile tooa correlati contenuto distribuzione multiserver di SQL Server Business Intelligence e SharePoint 2013, vedere [distribuire SQL Server Business Intelligence in macchine virtuali di Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53c-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="0d53c-406">Per informazioni generali toodeployments correlati di SQL Server Business Intelligence in macchine virtuali di Azure, vedere [SQL Server Business Intelligence in macchine virtuali di Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0d53c-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="0d53c-407">Per ulteriori informazioni sul costo hello addebiti di calcolo di Azure, vedere scheda macchine virtuali hello del [calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="0d53c-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="0d53c-408">Contenuti della community</span><span class="sxs-lookup"><span data-stu-id="0d53c-408">Community Content</span></span>
* <span data-ttu-id="0d53c-409">Per istruzioni dettagliate su come toocreate una modalità nativa di Reporting Services server di report senza usare lo script, vedere [di Hosting SQL Reporting Services nella macchina virtuale Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="0d53c-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="0d53c-410">Risorse tooother collegamenti per SQL Server in macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="0d53c-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="0d53c-411">Panoramica di SQL Server in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="0d53c-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

