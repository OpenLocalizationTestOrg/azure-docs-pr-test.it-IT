---
title: "Usare PowerShell per creare una macchina virtuale con un server di report in modalità nativa | Microsoft Docs"
description: "Questo argomento descrive e illustra la distribuzione e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure. "
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
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="251cb-103">Usare PowerShell per creare una macchina virtuale di Azure con un server di report in modalità nativa</span><span class="sxs-lookup"><span data-stu-id="251cb-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="251cb-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="251cb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="251cb-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="251cb-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="251cb-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="251cb-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="251cb-107">Questo argomento descrive e illustra la distribuzione e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="251cb-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="251cb-108">I passaggi descritti in questo documento usano una combinazione di operazioni manuali per creare la macchina virtuale e uno script di Windows PowerShell per configurare Reporting Services nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="251cb-109">Lo script di configurazione include l'apertura di una porta del firewall per HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="251cb-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="251cb-110">Se non è necessario **HTTPS** nel server di report, **saltare il passaggio 2**.</span><span class="sxs-lookup"><span data-stu-id="251cb-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="251cb-111">Dopo aver creato la macchina virtuale con il passaggio 1, vedere la sezione Usare lo script per configurare il server di report e HTTP.</span><span class="sxs-lookup"><span data-stu-id="251cb-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="251cb-112">Dopo aver eseguito lo script, il server di report è pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="251cb-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="251cb-113">Prerequisiti e presupposti</span><span class="sxs-lookup"><span data-stu-id="251cb-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="251cb-114">**Sottoscrizione di Azure**: verificare il numero di core disponibili nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="251cb-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="251cb-115">Se si crea la dimensione di macchina virtuale consigliata **A3**, sono necessari **4** core disponibili.</span><span class="sxs-lookup"><span data-stu-id="251cb-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="251cb-116">Se si usa la dimensione di macchina virtuale **A2**, sono necessari **2** core disponibili.</span><span class="sxs-lookup"><span data-stu-id="251cb-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="251cb-117">Per verificare il limite di core della sottoscrizione, nel portale di Azure classico fare clic su IMPOSTAZIONI nel riquadro a sinistra e quindi su UTILIZZO nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="251cb-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="251cb-118">Per aumentare la quota di core, contattare il [supporto tecnico di Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="251cb-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="251cb-119">Per informazioni sulle dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="251cb-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="251cb-120">**Scripting di Windows PowerShell**: l'argomento presuppone una conoscenza di base di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="251cb-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="251cb-121">Per altre informazioni sull'uso di Windows PowerShell, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="251cb-122">Avvio di Windows PowerShell in Windows Server</span><span class="sxs-lookup"><span data-stu-id="251cb-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="251cb-123">Introduzione a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="251cb-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="251cb-124">Passaggio 1: Eseguire il provisioning di una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="251cb-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="251cb-125">Passare al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="251cb-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="251cb-126">Fare clic su **Macchine virtuali** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="251cb-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![macchine virtuali di microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="251cb-128">Fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="251cb-128">Click **New**.</span></span>
   
    ![pulsante nuovo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="251cb-130">Fare clic su **Da raccolta**.</span><span class="sxs-lookup"><span data-stu-id="251cb-130">Click **From Gallery**.</span></span>
   
    ![nuova macchina virtuale dalla raccolta](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="251cb-132">Scegliere **SQL Server 2014 RTM Standard - Windows Server 2012 R2** e fare clic sulla freccia per continuare.</span><span class="sxs-lookup"><span data-stu-id="251cb-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="251cb-134">Se è necessaria la funzionalità per le sottoscrizioni basate sui dati di Reporting Services, scegliere **SQL Server 2014 RTM Enterprise - Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="251cb-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="251cb-135">Per altre informazioni sulle edizioni di SQL Server e sul supporto delle funzionalità, vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="251cb-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="251cb-136">Nella pagina **Configurazione macchina virtuale** modificare i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="251cb-137">Se è presente più di una **DATA DI RILASCIO VERSIONE**, selezionare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="251cb-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="251cb-138">**Nome macchina virtuale**: il nome della macchina virtuale viene usato anche nella pagina di configurazione successiva come nome DNS del servizio cloud predefinito.</span><span class="sxs-lookup"><span data-stu-id="251cb-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="251cb-139">Il nome DNS deve essere univoco nel servizio Azure.</span><span class="sxs-lookup"><span data-stu-id="251cb-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="251cb-140">È consigliabile configurare la macchina virtuale con un nome di computer che descriva ciò per cui viene usata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="251cb-141">Ad esempio, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="251cb-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="251cb-142">**Piano**: Standard.</span><span class="sxs-lookup"><span data-stu-id="251cb-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="251cb-143">**Dimensioni: A3** è la dimensione di macchina virtuale consigliata per i carichi di lavoro di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="251cb-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="251cb-144">Se una macchina virtuale viene usata solo come server di report, è sufficiente la dimensione di macchina virtuale A2, a meno che il server di report non debba supportare un elevato carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="251cb-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="251cb-145">Per informazioni sui prezzi delle macchine virtuali, vedere [Macchine virtuali - Prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="251cb-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="251cb-146">**Nuovo nome utente**: il nome specificato viene creato come amministratore nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="251cb-147">**Nuova password** e **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="251cb-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="251cb-148">Questa password viene usata per il nuovo account di amministratore ed è consigliabile usare una password complessa.</span><span class="sxs-lookup"><span data-stu-id="251cb-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="251cb-149">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-149">Click **Next**.</span></span> <span data-ttu-id="251cb-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="251cb-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="251cb-151">Nella pagina successiva, modificare i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="251cb-152">**Servizio cloud**: selezionare **Crea un nuovo servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="251cb-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="251cb-153">**Nome DNS del servizio cloud**: è il nome DNS pubblico del servizio cloud associato alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="251cb-154">Il nome predefinito è il nome immesso per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="251cb-155">Se nei passaggi successivi dell'argomento si crea un certificato SSL attendibile, il nome DNS viene usato con il valore "**Rilasciato a**" per il certificato.</span><span class="sxs-lookup"><span data-stu-id="251cb-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="251cb-156">**Area/Gruppo di affinità/Rete virtuale**: scegliere l'area più vicina agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="251cb-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="251cb-157">**Account di archiviazione**: usare un account di archiviazione generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="251cb-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="251cb-158">**Set di disponibilità**: nessuno.</span><span class="sxs-lookup"><span data-stu-id="251cb-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="251cb-159">**ENDPOINT**: mantenere gli endpoint **Desktop remoto** e **PowerShell** e quindi aggiungere un endpoint HTTP o HTTPS, a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="251cb-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="251cb-160">**HTTP**: le porte pubbliche e private predefinite hanno il numero **80**.</span><span class="sxs-lookup"><span data-stu-id="251cb-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="251cb-161">Si noti che se si usa una porta privata diversa dalla porta 80, sarà necessario modificare il parametro **$HTTPport = 80** nello script HTTP.</span><span class="sxs-lookup"><span data-stu-id="251cb-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="251cb-162">**HTTPS**: le porte pubbliche e private predefinite hanno il numero **443**.</span><span class="sxs-lookup"><span data-stu-id="251cb-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="251cb-163">Come procedura consigliata, modificare la porta privata e configurare il firewall e il server di report per usare la porta privata.</span><span class="sxs-lookup"><span data-stu-id="251cb-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="251cb-164">Per altre informazioni sugli endpoint, vedere [Come configurare le comunicazioni con una macchina virtuale](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="251cb-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="251cb-165">Si noti che se si usa una porta diversa dalla 443, è necessario modificare il parametro **$HTTPsport = 443** nello script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="251cb-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="251cb-166">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="251cb-166">Click next .</span></span> ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="251cb-168">Nell'ultima pagina della procedura guidata lasciare selezionata l'impostazione predefinita **Installa l'agente di macchine virtuali** .</span><span class="sxs-lookup"><span data-stu-id="251cb-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="251cb-169">I passaggi descritti in questo argomento non usano l'agente di macchine virtuali, ma se si prevede di usare questa macchina virtuale, le estensioni e l'agente di macchine virtuali consentono di migliorare la gestione delle comunicazioni.</span><span class="sxs-lookup"><span data-stu-id="251cb-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="251cb-170">Per altre informazioni sull'agente di macchine virtuali, vedere l'articolo relativo ad [agente di macchine virtuali ed estensioni - Parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="251cb-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="251cb-171">Una delle estensioni predefinite installate e in esecuzione è l'estensione "BGINFO" che visualizza sul desktop della macchina virtuale le informazioni di sistema, ad esempio l'IP interno e lo spazio libero su disco.</span><span class="sxs-lookup"><span data-stu-id="251cb-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="251cb-172">Fare clic su Completa.</span><span class="sxs-lookup"><span data-stu-id="251cb-172">Click complete .</span></span> ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="251cb-174">Lo **Stato** della macchina virtuale viene visualizzato come **Avvio (provisioning)** durante il processo di provisioning e come **In esecuzione** quando la macchina virtuale è disponibile e pronta all'uso.</span><span class="sxs-lookup"><span data-stu-id="251cb-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="251cb-175">Passaggio 2: Creare un certificato del server</span><span class="sxs-lookup"><span data-stu-id="251cb-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="251cb-176">Se HTTPS non è necessario nel server di report, è possibile **ignorare il passaggio 2** e passare alla sezione **Usare lo script per configurare il server di report e HTTP**.</span><span class="sxs-lookup"><span data-stu-id="251cb-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="251cb-177">Usare lo script HTTP per configurare rapidamente il server di report e renderlo pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="251cb-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="251cb-178">Per usare HTTPS nella macchina virtuale, è necessario un certificato SSL attendibile.</span><span class="sxs-lookup"><span data-stu-id="251cb-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="251cb-179">A seconda dello scenario, è possibile usare uno dei due metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="251cb-180">Un certificato SSL valido emesso da un'autorità di certificazione (CA) e ritenuto attendibile da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="251cb-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="251cb-181">I certificati dell'autorità di certificazione radice devono essere distribuiti tramite il programma Microsoft Root Certificate.</span><span class="sxs-lookup"><span data-stu-id="251cb-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="251cb-182">Per altre informazioni su questo programma, vedere l'articolo relativo al [programma SSL Root Certificate per Windows e Windows Phone 8 (CA membro)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e l'articolo di [introduzione al programma Microsoft Root Certificate](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="251cb-183">Un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="251cb-183">A self-signed certificate.</span></span> <span data-ttu-id="251cb-184">I certificati autofirmati non sono consigliati per gli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="251cb-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="251cb-185">Per usare un certificato creato da un'autorità di certificazione (CA) attendibile</span><span class="sxs-lookup"><span data-stu-id="251cb-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="251cb-186">**Richiedere un certificato del server per il sito Web di un'autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="251cb-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="251cb-187">È possibile usare la Gestione guidata certificati server Web per generare un file di richiesta certificato (Certreq.txt) che si invia a un'autorità di certificazione o per generare una richiesta per un'autorità di certificazione online.</span><span class="sxs-lookup"><span data-stu-id="251cb-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="251cb-188">Ad esempio, Servizi certificati Microsoft in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="251cb-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="251cb-189">A seconda del livello di garanzia di identificazione offerto dal certificato del server, possono trascorrere da alcuni giorni a diversi mesi perché l'autorità di certificazione approvi la richiesta e invii un file di certificato.</span><span class="sxs-lookup"><span data-stu-id="251cb-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="251cb-190">Per altre informazioni su come richiedere i certificati del server, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="251cb-191">Usare [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="251cb-192">Strumenti di sicurezza per l'amministrazione di Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="251cb-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="251cb-193">Strumenti di sicurezza per l'amministrazione di Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="251cb-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="251cb-194">Il campo **Rilasciato a** del certificato SSL attendibile deve essere uguale al **Nome DNS del servizio cloud** usato per la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="251cb-195">**Installare il certificato nel server Web**.</span><span class="sxs-lookup"><span data-stu-id="251cb-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="251cb-196">In questo caso, il server Web è la macchina virtuale che ospita il server di report. Il sito Web verrà creato nei passaggi successivi durante la configurazione di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="251cb-197">Per altre informazioni sull'installazione del certificato nel server Web tramite lo snap-in MMC Certificati, vedere l'articolo relativo all'[installazione di un certificato del server](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="251cb-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="251cb-198">Se si desidera usare lo script incluso in questo argomento per configurare il server di report, viene richiesto il valore **Identificazione personale** dei certificati come parametro dello script.</span><span class="sxs-lookup"><span data-stu-id="251cb-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="251cb-199">Vedere la sezione successiva per informazioni dettagliate su come ottenere l'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="251cb-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="251cb-200">Assegnare il certificato al server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="251cb-201">L'assegnazione viene completata nella sezione successiva, quando si configura il server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="251cb-202">Per usare il certificato autofirmato delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="251cb-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="251cb-203">Un certificato autofirmato viene creato nella macchina virtuale quando viene eseguito il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="251cb-204">Il nome del certificato è uguale al nome DNS della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="251cb-205">Per evitare errori relativi al certificato, è necessario che il certificato sia attendibile per la macchina virtuale e tutti gli utenti del sito.</span><span class="sxs-lookup"><span data-stu-id="251cb-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="251cb-206">Per rendere attendibile l'autorità di certificazione radice del certificato nella macchina virtuale locale, aggiungere il certificato alle **Autorità di certificazione radice attendibili**.</span><span class="sxs-lookup"><span data-stu-id="251cb-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="251cb-207">Di seguito è riportato un riepilogo dei passaggi necessari.</span><span class="sxs-lookup"><span data-stu-id="251cb-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="251cb-208">Per informazioni dettagliate su come rendere attendibile l'autorità di certificazione, vedere l'articolo relativo all' [installazione di un certificato del server](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="251cb-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="251cb-209">Nel portale di Azure classico selezionare la macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="251cb-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="251cb-210">A seconda della configurazione del browser, potrebbe essere richiesto di salvare un file con estensione rdp per la connessione alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![connettersi alla macchina virtuale di azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="251cb-212">Usare il nome della macchina virtuale, il nome utente e la password configurati durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="251cb-213">Nella figura seguente, ad esempio, il nome della macchina virtuale è **ssrsnativecloud** e il nome utente è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="251cb-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="251cb-215">Eseguire mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="251cb-215">Run mmc.exe.</span></span> <span data-ttu-id="251cb-216">Per altre informazioni, vedere [Procedura: Visualizzare certificati con lo snap-in MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="251cb-217">Nel menu **File** dell'applicazione console aggiungere lo snap-in **Certificati**, selezionare **Account computer** quando richiesto e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="251cb-218">Selezionare il **computer locale** da gestire e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="251cb-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="251cb-219">Fare clic su **OK**, espandere i nodi **Certificati - Personale** e quindi fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="251cb-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="251cb-220">Il nome del certificato è costituito dal nome DNS della macchina virtuale e termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="251cb-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="251cb-221">Fare clic con il pulsante destro del mouse sul nome del certificato e scegliere **Copia**.</span><span class="sxs-lookup"><span data-stu-id="251cb-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="251cb-222">Espandere il nodo **Autorità di certificazione radice attendibili**, fare clic con il pulsante destro del mouse su **Certificati** e quindi scegliere **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="251cb-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="251cb-223">Per convalidare, fare doppio clic sul nome del certificato in **Autorità di certificazione radice attendibili** e, se non si sono verificati errori, il certificato è visibile.</span><span class="sxs-lookup"><span data-stu-id="251cb-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="251cb-224">Se si vuole usare lo script HTTPS incluso in questo argomento per configurare il server di report, è necessario specificare il valore di **Identificazione personale** dei certificati come parametro dello script.</span><span class="sxs-lookup"><span data-stu-id="251cb-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="251cb-225">**Per ottenere il valore di identificazione personale**, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="251cb-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="251cb-226">È disponibile anche un esempio di PowerShell per recuperare l'identificazione personale nella sezione [Usare lo script per configurare il server di report e HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="251cb-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="251cb-227">Fare doppio clic sul nome del certificato, ad esempio ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="251cb-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="251cb-228">Fare clic sulla scheda **Dettagli** .</span><span class="sxs-lookup"><span data-stu-id="251cb-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="251cb-229">Fare clic su **Identificazione personale**.</span><span class="sxs-lookup"><span data-stu-id="251cb-229">Click **Thumbprint**.</span></span> <span data-ttu-id="251cb-230">Il valore dell'identificazione personale viene visualizzato nel campo dei dettagli, ad esempio ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="251cb-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="251cb-231">Copiare l'identificazione personale e salvare il valore per usarlo successivamente o modificare lo script.</span><span class="sxs-lookup"><span data-stu-id="251cb-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="251cb-232">(*) Prima di eseguire lo script, rimuovere gli spazi tra le coppie di valori.</span><span class="sxs-lookup"><span data-stu-id="251cb-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="251cb-233">Ad esempio, l'identificazione personale citata in precedenza ora sarebbe ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="251cb-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="251cb-234">Assegnare il certificato al server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="251cb-235">L'assegnazione viene completata nella sezione successiva, quando si configura il server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="251cb-236">Se si usa un certificato SSL autofirmato, il nome del certificato corrisponde già al nome host della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="251cb-237">Pertanto, il DNS del computer è già registrato a livello globale ed è accessibile da qualsiasi client.</span><span class="sxs-lookup"><span data-stu-id="251cb-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="251cb-238">Passaggio 3: Configurare il server di report</span><span class="sxs-lookup"><span data-stu-id="251cb-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="251cb-239">Questa sezione illustra la configurazione della macchina virtuale come server di report di Reporting Services in modalità nativa.</span><span class="sxs-lookup"><span data-stu-id="251cb-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="251cb-240">Per configurare il server di report, è possibile usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="251cb-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="251cb-241">Usare lo script per configurare il server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="251cb-242">Usare Gestione configurazione per configurare il server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="251cb-243">Per istruzioni più dettagliate, vedere la sezione [Connettersi alla macchina virtuale e avviare Gestione configurazione di Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="251cb-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="251cb-244">**Nota sull'autenticazione:** l'autenticazione di Windows è il metodo di autenticazione consigliato ed è l'autenticazione predefinita di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="251cb-245">Solo gli utenti configurati nella macchina virtuale possono accedere a Reporting Services ed essere assegnati ai ruoli di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="251cb-246">Usare lo script per configurare il server di report e HTTP</span><span class="sxs-lookup"><span data-stu-id="251cb-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="251cb-247">Per usare lo script di Windows PowerShell per configurare il server di report, completare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="251cb-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="251cb-248">La configurazione include HTTP e non HTTPS.</span><span class="sxs-lookup"><span data-stu-id="251cb-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="251cb-249">Nel portale di Azure classico selezionare la macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="251cb-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="251cb-250">A seconda della configurazione del browser, potrebbe essere richiesto di salvare un file con estensione rdp per la connessione alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![connettersi alla macchina virtuale di azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="251cb-252">Usare il nome della macchina virtuale, il nome utente e la password configurati durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="251cb-253">Nella figura seguente, ad esempio, il nome della macchina virtuale è **ssrsnativecloud** e il nome utente è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="251cb-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="251cb-255">Nella macchina virtuale aprire **Windows PowerShell ISE** con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="251cb-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="251cb-256">PowerShell ISE è installato per impostazione predefinita in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="251cb-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="251cb-257">È consigliabile usare ISE anziché una finestra standard di Windows PowerShell in modo da poter incollare lo script in ISE, modificare e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="251cb-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="251cb-258">In Windows PowerShell ISE scegliere **Mostra riquadro di script** dal menu **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="251cb-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="251cb-259">Copiare lo script seguente e incollarlo nel riquadro di script di Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="251cb-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
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
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
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
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
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
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
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
5. <span data-ttu-id="251cb-260">Se la macchina virtuale è stata creata con una porta HTTP diversa da 80, modificare il parametro $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="251cb-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="251cb-261">Lo script è attualmente configurato per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="251cb-262">Per eseguire lo script per Reporting Services, modificare la parte della versione del percorso dello spazio dei nomi in "v11", nell'istruzione Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="251cb-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="251cb-263">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="251cb-263">Run the script.</span></span>

<span data-ttu-id="251cb-264">**Convalida**: per verificare la funzionalità di base del server di report, vedere [Verificare la configurazione](#verify-the-configuration) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="251cb-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="251cb-265">Usare lo script per configurare il server di report e HTTPS</span><span class="sxs-lookup"><span data-stu-id="251cb-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="251cb-266">Per usare Windows PowerShell per configurare il server di report, completare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="251cb-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="251cb-267">La configurazione include HTTPS e non HTTP.</span><span class="sxs-lookup"><span data-stu-id="251cb-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="251cb-268">Nel portale di Azure classico selezionare la macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="251cb-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="251cb-269">A seconda della configurazione del browser, potrebbe essere richiesto di salvare un file con estensione rdp per la connessione alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![connettersi alla macchina virtuale di azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="251cb-271">Usare il nome della macchina virtuale, il nome utente e la password configurati durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="251cb-272">Nella figura seguente, ad esempio, il nome della macchina virtuale è **ssrsnativecloud** e il nome utente è **testuser**.</span><span class="sxs-lookup"><span data-stu-id="251cb-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="251cb-274">Nella macchina virtuale aprire **Windows PowerShell ISE** con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="251cb-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="251cb-275">PowerShell ISE è installato per impostazione predefinita in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="251cb-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="251cb-276">È consigliabile usare ISE anziché una finestra standard di Windows PowerShell in modo da poter incollare lo script in ISE, modificare e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="251cb-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="251cb-277">Per abilitare l'esecuzione di script, eseguire il comando di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="251cb-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="251cb-278">Quindi per verificare i criteri, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="251cb-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="251cb-279">In **Windows PowerShell ISE** scegliere **Mostra riquadro di script** dal menu **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="251cb-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="251cb-280">Copiare lo script seguente e incollarlo nel riquadro di script Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="251cb-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
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
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
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
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
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
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
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
6. <span data-ttu-id="251cb-281">Modificare il parametro **$certificatehash** nello script:</span><span class="sxs-lookup"><span data-stu-id="251cb-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="251cb-282">Si tratta di un parametro **obbligatorio** .</span><span class="sxs-lookup"><span data-stu-id="251cb-282">This is a **required** parameter.</span></span> <span data-ttu-id="251cb-283">Se il valore del certificato non è stato salvato nei passaggi precedenti, usare uno dei metodi seguenti per copiare il valore hash del certificato dall'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="251cb-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="251cb-284">Nella macchina virtuale, aprire Windows PowerShell ISE ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="251cb-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="251cb-285">L'output sarà simile al seguente: Se lo script restituisce una riga vuota, la macchina virtuale non dispone, ad esempio, di un certificato configurato.</span><span class="sxs-lookup"><span data-stu-id="251cb-285">The output will look similar to the following.</span></span> <span data-ttu-id="251cb-286">Per informazioni, vedere la sezione [Per usare il certificato autofirmato delle macchine virtuali](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="251cb-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="251cb-287">OPPURE</span><span class="sxs-lookup"><span data-stu-id="251cb-287">OR</span></span>
   * <span data-ttu-id="251cb-288">Eseguire mmc.exe nella macchina virtuale e quindi aggiungere lo snap-in **Certificati** .</span><span class="sxs-lookup"><span data-stu-id="251cb-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="251cb-289">Nel nodo **Autorità di certificazione radice attendibili** fare doppio clic sul nome del certificato.</span><span class="sxs-lookup"><span data-stu-id="251cb-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="251cb-290">Se si usa il certificato autofirmato della macchina virtuale, il nome del certificato è costituito dal nome DNS della macchina virtuale e termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="251cb-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="251cb-291">Fare clic sulla scheda **Dettagli** .</span><span class="sxs-lookup"><span data-stu-id="251cb-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="251cb-292">Fare clic su **Identificazione personale**.</span><span class="sxs-lookup"><span data-stu-id="251cb-292">Click **Thumbprint**.</span></span> <span data-ttu-id="251cb-293">Il valore dell'identificazione personale viene visualizzato nel campo dei dettagli, ad esempio af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="251cb-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="251cb-294">**Prima di eseguire lo script**, rimuovere gli spazi tra le coppie di valori.</span><span class="sxs-lookup"><span data-stu-id="251cb-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="251cb-295">Ad esempio, af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="251cb-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="251cb-296">Modificare il parametro **$httpsport** :</span><span class="sxs-lookup"><span data-stu-id="251cb-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="251cb-297">Se si usa la porta 443 per l'endpoint HTTPS, non è necessario aggiornare questo parametro nello script.</span><span class="sxs-lookup"><span data-stu-id="251cb-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="251cb-298">In caso contrario, usare il valore della porta selezionato durante la configurazione dell'endpoint privato HTTPS nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="251cb-299">Modificare il parametro **$DNSName** :</span><span class="sxs-lookup"><span data-stu-id="251cb-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="251cb-300">Lo script è configurato per un certificato con caratteri jolly $DNSName="+".</span><span class="sxs-lookup"><span data-stu-id="251cb-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="251cb-301">Se non si desidera configurare un'associazione del certificato con caratteri jolly, rimuovere il commento $DNSName="+" e abilitare la riga seguente, il riferimento $DNSNAme completo, ##$DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="251cb-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="251cb-302">Modificare il valore $DNSName se non si desidera usare il nome DNS della macchina virtuale per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="251cb-303">Se si usa il parametro, anche il certificato deve usare questo nome ed è necessario registrare il nome a livello globale in un server DNS.</span><span class="sxs-lookup"><span data-stu-id="251cb-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="251cb-304">Lo script è attualmente configurato per Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="251cb-305">Per eseguire lo script per Reporting Services, modificare la parte della versione del percorso dello spazio dei nomi in "v11", nell'istruzione Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="251cb-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="251cb-306">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="251cb-306">Run the script.</span></span>

<span data-ttu-id="251cb-307">**Convalida**: per verificare la funzionalità di base del server di report, vedere [Verificare la configurazione](#verify-the-connection) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="251cb-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="251cb-308">Per verificare l'associazione del certificato, aprire un prompt dei comandi con privilegi amministrativi e quindi eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="251cb-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="251cb-309">Il risultato include quanto segue:</span><span class="sxs-lookup"><span data-stu-id="251cb-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="251cb-310">Usare Gestione configurazione per configurare il server di report</span><span class="sxs-lookup"><span data-stu-id="251cb-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="251cb-311">Se non si desidera eseguire lo script di PowerShell per configurare il server di report, seguire i passaggi descritti in questa sezione per usare Gestione configurazione di Reporting Services in modalità nativa per configurare il server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="251cb-312">Nel portale di Azure classico selezionare la macchina virtuale e fare clic su Connetti.</span><span class="sxs-lookup"><span data-stu-id="251cb-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="251cb-313">Usare il nome utente e la password configurati durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![connettersi alla macchina virtuale di azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="251cb-315">Eseguire Windows Update e installare gli aggiornamenti nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="251cb-316">Se è necessario un riavvio della macchina virtuale, riavviare la macchina virtuale e riconnettersi alla macchina virtuale dal portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="251cb-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="251cb-317">Dal menu Start della macchina virtuale digitare **Reporting Services** e aprire **Gestione configurazione Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="251cb-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="251cb-318">Lasciare i valori predefiniti per il **nome server** e l'**istanza del server di report**.</span><span class="sxs-lookup"><span data-stu-id="251cb-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="251cb-319">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-319">Click **Connect**.</span></span>
5. <span data-ttu-id="251cb-320">Nel riquadro a sinistra fare clic su **URL servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="251cb-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="251cb-321">Per impostazione predefinita, Reporting Services è configurato per la porta HTTP 80 con IP "Tutti assegnati".</span><span class="sxs-lookup"><span data-stu-id="251cb-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="251cb-322">Per aggiungere HTTPS:</span><span class="sxs-lookup"><span data-stu-id="251cb-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="251cb-323">In **Certificato SSL**selezionare il certificato da usare, ad esempio [nome macchina virtuale].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="251cb-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="251cb-324">Se non è elencato alcun certificato, vedere la sezione **Passaggio 2: Creare un certificato del server** per informazioni su come installare e rendere attendibile il certificato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="251cb-325">In **Porta SSL**scegliere 443.</span><span class="sxs-lookup"><span data-stu-id="251cb-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="251cb-326">Se l'endpoint privato HTTPS è configurato nella macchina virtuale con una porta privata diversa, usare quel valore.</span><span class="sxs-lookup"><span data-stu-id="251cb-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="251cb-327">Fare clic su **Applica** e attendere il completamento dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="251cb-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="251cb-328">Nel riquadro a sinistra fare clic su **Database**.</span><span class="sxs-lookup"><span data-stu-id="251cb-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="251cb-329">Fare clic su **Modifica database**.</span><span class="sxs-lookup"><span data-stu-id="251cb-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="251cb-330">Fare clic su **Crea un nuovo database del server di report** e quindi su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="251cb-331">Come nome di macchina virtuale lasciare il **Nome server** predefinito e come **Tipo di autenticazione** lasciare il valore predefinito **Utente corrente** - **Sicurezza integrata**.</span><span class="sxs-lookup"><span data-stu-id="251cb-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="251cb-332">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-332">Click **Next**.</span></span>
   4. <span data-ttu-id="251cb-333">Lasciare il **Nome database** predefinito come **ReportServer** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="251cb-334">Lasciare **Credenziali del servizio** come **Tipo di autenticazione** predefinito e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="251cb-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="251cb-335">Fare clic su **Avanti** on the **Riepilogo** .</span><span class="sxs-lookup"><span data-stu-id="251cb-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="251cb-336">Dopo aver completato la configurazione, fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="251cb-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="251cb-337">Nel riquadro sinistro fare clic su **URL Gestione report**.</span><span class="sxs-lookup"><span data-stu-id="251cb-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="251cb-338">Lasciare **Report** come **Directory virtuale** predefinita e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="251cb-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="251cb-339">Fare clic su **Esci** per chiudere Gestione configurazione di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="251cb-340">Passaggio 4: Aprire la porta di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="251cb-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="251cb-341">Se si usa uno script per configurare il server di report, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="251cb-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="251cb-342">Lo script include un passaggio per aprire la porta del firewall.</span><span class="sxs-lookup"><span data-stu-id="251cb-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="251cb-343">I valori predefiniti sono la porta 80 per HTTP e la porta 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="251cb-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="251cb-344">Per connettersi in modalità remota a Gestione report o al server di report sulla macchina virtuale, è necessario un endpoint TCP nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="251cb-345">È necessario per aprire la stessa porta nel firewall della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="251cb-346">L'endpoint è stato creato quando è stato eseguito il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="251cb-347">Questa sezione fornisce le informazioni di base su come aprire la porta del firewall.</span><span class="sxs-lookup"><span data-stu-id="251cb-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="251cb-348">Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="251cb-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="251cb-349">Se si usa uno script per configurare il server di report, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="251cb-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="251cb-350">Lo script include un passaggio per aprire la porta del firewall.</span><span class="sxs-lookup"><span data-stu-id="251cb-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="251cb-351">Se per HTTPS è configurata una porta privata diversa da 443, modificare lo script seguente in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="251cb-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="251cb-352">Per aprire la porta **443** in Windows Firewall, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="251cb-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="251cb-353">Aprire una finestra di Windows PowerShell con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="251cb-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="251cb-354">Se è stata usata una porta diversa da 443 quando è stato configurato l'endpoint HTTPS nella macchina virtuale, aggiornare la porta nel comando seguente e quindi eseguire il comando:</span><span class="sxs-lookup"><span data-stu-id="251cb-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="251cb-355">Completata l'esecuzione del comando, verrà visualizzato **OK** al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="251cb-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="251cb-356">Per verificare che la porta è aperta, aprire una finestra di Windows PowerShell ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="251cb-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="251cb-357">Verificare la configurazione</span><span class="sxs-lookup"><span data-stu-id="251cb-357">Verify the configuration</span></span>
<span data-ttu-id="251cb-358">Per verificare che la funzionalità di base del server di report funzioni, aprire il browser con privilegi amministrativi e quindi passare ai seguenti URL del server di report e della gestione report:</span><span class="sxs-lookup"><span data-stu-id="251cb-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="251cb-359">Nella macchina virtuale passare all'URL del server di report:</span><span class="sxs-lookup"><span data-stu-id="251cb-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="251cb-360">Nella macchina virtuale passare all'URL della gestione report:</span><span class="sxs-lookup"><span data-stu-id="251cb-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="251cb-361">Dal computer locale passare a Gestione report **remota** nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="251cb-362">Aggiornare il nome DNS nell'esempio seguente nel modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="251cb-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="251cb-363">Quando viene richiesta una password, usare le credenziali di amministratore create quando è stato eseguito il provisioning della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="251cb-364">Il nome utente è nel formato [dominio]\[nome utente], dove il dominio è il nome computer della macchina virtuale, ad esempio ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="251cb-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="251cb-365">Se non si usa HTTP**S**, rimuovere la **S** dall'URL.</span><span class="sxs-lookup"><span data-stu-id="251cb-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="251cb-366">Vedere la sezione successiva per informazioni sulla creazione di utenti aggiuntivi nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="251cb-367">Dal computer locale passare all'URL del server di report remoto.</span><span class="sxs-lookup"><span data-stu-id="251cb-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="251cb-368">Aggiornare il nome DNS nell'esempio seguente nel modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="251cb-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="251cb-369">Se non si usa HTTPS, rimuovere la S dall'URL.</span><span class="sxs-lookup"><span data-stu-id="251cb-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="251cb-370">Creare utenti e assegnare ruoli</span><span class="sxs-lookup"><span data-stu-id="251cb-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="251cb-371">Dopo aver configurato e verificato il server di report, un'attività amministrativa comune consiste nel creare uno o più utenti e assegnare agli utenti i ruoli di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="251cb-372">Per altre informazioni, vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="251cb-372">For more information, see the following:</span></span>

* [<span data-ttu-id="251cb-373">Creare un account utente locale</span><span class="sxs-lookup"><span data-stu-id="251cb-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="251cb-374">[Concedere l'accesso utente a un server di report (Gestione report)](https://msdn.microsoft.com/library/ms156034.aspx)</span><span class="sxs-lookup"><span data-stu-id="251cb-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="251cb-375">Creare e gestire le assegnazioni di ruoli</span><span class="sxs-lookup"><span data-stu-id="251cb-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="251cb-376">Per creare e pubblicare i report in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="251cb-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="251cb-377">Nella tabella seguente vengono riepilogate alcune delle opzioni disponibili per la pubblicazione di report esistenti da un computer locale nel server di report ospitato nella macchina virtuale di Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="251cb-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="251cb-378">**RS.exe script**: usare lo script RS.exe per copiare gli elementi del report da un server di report esistente nella macchina virtuale di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="251cb-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="251cb-379">Per altre informazioni, vedere la sezione "Da modalità nativa a modalità nativa - Macchina virtuale di Microsoft Azure" in [Script di esempio rs.exe di Reporting Services per la migrazione del contenuto tra server di report](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="251cb-380">**Generatore report**: la macchina virtuale include la versione ClickOnce di Generatore report di Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="251cb-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="251cb-381">Per avviare il Generatore report per la prima volta sulla macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="251cb-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="251cb-382">Avviare il browser con privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="251cb-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="251cb-383">Passare a Gestione report nella macchina virtuale e fare clic su **Generatore report** sulla barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="251cb-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="251cb-384">Per altre informazioni, vedere [Installazione, disinstallazione e supporto di Generatore report](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="251cb-385">**SQL Server Data Tools - Macchina virtuale**: se la macchina virtuale è stata creata con SQL Server 2012, SQL Server Data Tools è installato nella macchina virtuale e può essere usato per creare **progetti server di report** e report nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="251cb-386">SQL Server Data Tools è in grado di pubblicare i report nel server di report sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="251cb-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="251cb-387">Se la macchina virtuale è stata creata con SQL server 2014, è possibile installare SQL Server Data Tools - Business Intelligence per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="251cb-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="251cb-388">Per altre informazioni, vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="251cb-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="251cb-389">Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="251cb-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="251cb-390">Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="251cb-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="251cb-391">SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="251cb-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="251cb-392">**SQL Server Data Tools - Remoto**: nel computer locale creare un progetto di Reporting Services in SQL Server Data Tools contenente i report di Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="251cb-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="251cb-393">Configurare il progetto per connettersi all'URL del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="251cb-393">Configure the project to connect to the web service URL.</span></span>
  
    ![proprietà del progetto ssdt per un progetto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="251cb-395">**Utilizzare script**: usare lo script per copiare il contenuto del server di report.</span><span class="sxs-lookup"><span data-stu-id="251cb-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="251cb-396">Per altre informazioni, vedere [Script di esempio rs.exe di Reporting Services per la migrazione del contenuto tra server di report](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="251cb-397">Ridurre i costi se non si usa la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="251cb-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="251cb-398">Per ridurre i costi delle macchine virtuali di Azure quando non sono in uso, spegnere la macchina virtuale dal portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="251cb-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="251cb-399">Se per spegnere la macchina virtuale si usano le opzioni di risparmio energia di Windows, i costi associati alla macchina virtuale verranno addebitati comunque.</span><span class="sxs-lookup"><span data-stu-id="251cb-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="251cb-400">Per ridurre i costi, è necessario spegnere la macchina virtuale nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="251cb-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="251cb-401">Se la macchina virtuale non è più necessaria, eliminarla insieme ai file con estensione vhd associati per evitare l'addebito dei costi di archiviazione. Per altre informazioni, vedere la sezione Domande frequenti in [Prezzi di Macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="251cb-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="251cb-402">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="251cb-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="251cb-403">Risorse</span><span class="sxs-lookup"><span data-stu-id="251cb-403">Resources</span></span>
* <span data-ttu-id="251cb-404">Per contenuti analoghi relativi alla distribuzione di un server singolo di SQL Server Business Intelligence e SharePoint 2013, vedere l'articolo relativo all' [uso di Windows PowerShell per creare una macchina virtuale di Azure con SQL Server BI e SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="251cb-405">Per contenuti analoghi relativi a una distribuzione con più server di SQL Server Business Intelligence e SharePoint 2013, vedere l'articolo relativo alla [distribuzione di SQL Server Business Intelligence in Macchine virtuali di Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="251cb-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="251cb-406">Per informazioni generali relative alle distribuzioni di SQL Server Business Intelligence in Macchine virtuali di Azure, vedere [SQL Server Business Intelligence in Macchine virtuali di Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="251cb-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="251cb-407">Per altre informazioni sul calcolo delle spese di calcolo di Azure, vedere la scheda Macchine virtuali del [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="251cb-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="251cb-408">Contenuti della community</span><span class="sxs-lookup"><span data-stu-id="251cb-408">Community Content</span></span>
* <span data-ttu-id="251cb-409">Per istruzioni dettagliate su come creare un server di report di Reporting Services in modalità nativa senza usare lo script, vedere l'articolo relativo all' [hosting del servizio di report SQL in macchine virtuali di Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="251cb-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="251cb-410">Collegamenti ad altre risorse di SQL Server in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="251cb-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="251cb-411">Panoramica di SQL Server in Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="251cb-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

