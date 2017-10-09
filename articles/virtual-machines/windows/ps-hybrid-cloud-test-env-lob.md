---
title: ambiente di test dell'applicazione aaaLOB | Documenti Microsoft
description: Informazioni di ambiente per cloud toocreate una basata sul web, applicazione line of business in un ambiente ibrido IT pro o il test di sviluppo.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="b5214-103">Configurazione di un'applicazione LOB basata sul Web in un cloud ibrido per l'esecuzione di test</span><span class="sxs-lookup"><span data-stu-id="b5214-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="b5214-104">Questo argomento descrive la creazione di un ambiente cloud ibrido simulato per testare un'applicazione line-of-business basata su Web ospitata in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b5214-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="b5214-105">Di seguito è riportata la configurazione risultante hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b5214-106">Questa configurazione è costituita da:</span><span class="sxs-lookup"><span data-stu-id="b5214-106">This configuration consists of:</span></span>

* <span data-ttu-id="b5214-107">Una rete locale simulato ospitata in Azure (Buongiorno TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="b5214-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="b5214-108">Una rete virtuale cross-premise ospitata in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="b5214-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="b5214-109">Una connessione VPN da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b5214-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="b5214-110">Un server LOB basato su web, SQL server e il controller di dominio secondario nella rete virtuale di hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="b5214-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="b5214-111">Questa configurazione rappresenta una base e un punto di partenza comune da cui è possibile:</span><span class="sxs-lookup"><span data-stu-id="b5214-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="b5214-112">Sviluppare e testare le applicazioni LOB ospitate in Internet Information Services (IIS) con un back-end del database di SQL Server 2014 in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5214-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="b5214-113">Eseguire il test di questo carico di lavoro IT basato sul cloud ibrido simulato.</span><span class="sxs-lookup"><span data-stu-id="b5214-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="b5214-114">Esistono tre fasi principali toosetting un ambiente di testing cloud ibrida:</span><span class="sxs-lookup"><span data-stu-id="b5214-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="b5214-115">Configurare l'ambiente di cloud ibrido simulato hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="b5214-116">Configurare i computer hello SQL server (SQL1).</span><span class="sxs-lookup"><span data-stu-id="b5214-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="b5214-117">Configurare server LOB hello (LOB1).</span><span class="sxs-lookup"><span data-stu-id="b5214-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="b5214-118">Questo carico di lavoro richiede una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5214-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="b5214-119">Se si ha una sottoscrizione di MSDN o di Visual Studio, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="b5214-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="b5214-120">Per un esempio di un'applicazione LOB ospitata in Azure di produzione, vedere hello **applicazioni Line of business** progetto iniziale di architettura in [diagrammi dell'architettura Software Microsoft e i disegni](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="b5214-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="b5214-121">Fase 1: Configurare l'ambiente di cloud ibrido simulato hello</span><span class="sxs-lookup"><span data-stu-id="b5214-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="b5214-122">Creare hello [ambiente di test di cloud ibrido simulato](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5214-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b5214-123">Perché questo ambiente di test non richiede la presenza di hello del server di hello APP1 in subnet Corpnet hello, è possibile arrestarlo per ora.</span><span class="sxs-lookup"><span data-stu-id="b5214-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="b5214-124">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b5214-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="b5214-125">Fase 2: Configurare i computer hello SQL server (SQL1)</span><span class="sxs-lookup"><span data-stu-id="b5214-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="b5214-126">Dal portale di Azure hello, avviare il computer di DC2 hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="b5214-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="b5214-127">Successivamente, creare una macchina virtuale per SQL1 con questi comandi in un prompt dei comandi di Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="b5214-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="b5214-128">Toorunning precedenti questi comandi, immettere hello i valori delle variabili e Rimuovi hello < e > caratteri.</span><span class="sxs-lookup"><span data-stu-id="b5214-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b5214-129">Utilizzare hello tooSQL1 tooconnect portale Azure utilizzando l'account amministratore locale hello di SQL1.</span><span class="sxs-lookup"><span data-stu-id="b5214-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="b5214-130">A questo punto, configurare il test di connettività di base di Windows Firewall regole tooallow e traffico di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b5214-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="b5214-131">Da un prompt dei comandi di Windows PowerShell a livello di amministratore in SQL1 eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="b5214-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b5214-132">comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="b5214-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b5214-133">Successivamente, aggiungere hello disco dati supplementare in SQL1 come un nuovo volume con lettera dell'unità f: hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="b5214-134">Nel riquadro sinistro hello di Server Manager, fare clic su **servizi File e archiviazione**, quindi fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="b5214-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="b5214-135">Nel riquadro contenuti hello in hello **dischi** gruppo, fare clic su **disco 2** (con hello **partizione** impostare troppo**sconosciuto**).</span><span class="sxs-lookup"><span data-stu-id="b5214-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="b5214-136">Fare clic su **Attività**, quindi su **Nuovo volume**.</span><span class="sxs-lookup"><span data-stu-id="b5214-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="b5214-137">Hello prima pagina della creazione guidata nuovo Volume hello, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="b5214-138">Nel server di selezionare hello hello e pagina su disco, fare clic su **disco 2**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="b5214-139">Quando richiesto, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5214-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="b5214-140">Specifica dimensioni hello della pagina volume hello hello, scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="b5214-141">Pagina hello assegnare tooa unità lettera o una cartella, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="b5214-142">Nella pagina Impostazioni di hello selezionare il file system, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="b5214-143">Nella pagina Conferma selezioni per hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="b5214-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="b5214-144">Al termine, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="b5214-144">When complete, click **Close**.</span></span>

<span data-ttu-id="b5214-145">Eseguire questi comandi al prompt dei comandi di Windows PowerShell hello in SQL1:</span><span class="sxs-lookup"><span data-stu-id="b5214-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="b5214-146">Successivamente, dominio SQL1 toohello CORP Windows Server Active Directory con i comandi al prompt di Windows PowerShell hello in SQL1.</span><span class="sxs-lookup"><span data-stu-id="b5214-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b5214-147">Account hello CORP\User1 quando viene richiesto di utilizzare le credenziali dell'account di dominio toosupply per hello **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="b5214-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b5214-148">Dopo il riavvio, usare hello tooconnect portale Azure tooSQL1 *con account di amministratore locale hello di SQL1*.</span><span class="sxs-lookup"><span data-stu-id="b5214-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="b5214-149">A questo punto, configurare SQL Server 2014 toouse hello unità f per i nuovi database e le autorizzazioni dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="b5214-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="b5214-150">Dalla schermata Start hello digitare **SQL Server Management**, quindi fare clic su **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="b5214-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="b5214-151">In **connettersi tooServer**, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="b5214-152">Nel riquadro dell'albero di Esplora oggetti hello, fare doppio clic su **SQL1**, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b5214-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="b5214-153">In hello **le proprietà del Server** finestra, fare clic su **le impostazioni del Database**.</span><span class="sxs-lookup"><span data-stu-id="b5214-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="b5214-154">Individuare hello **percorsi predefiniti Database** e impostare i valori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5214-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="b5214-155">Per **dati**, digitare il percorso hello **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="b5214-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="b5214-156">Per **Log**, digitare il percorso hello **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="b5214-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="b5214-157">Per **Backup**, digitare il percorso hello **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="b5214-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="b5214-158">Nota: Solo i nuovi database utilizzeranno questi percorsi.</span><span class="sxs-lookup"><span data-stu-id="b5214-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="b5214-159">Fare clic su hello **OK** finestra hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="b5214-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="b5214-160">In hello **Esplora oggetti** riquadro dell'albero, aprire **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="b5214-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="b5214-161">Fare clic con il pulsante destro del mouse su **Account di accesso**, quindi scegliere **Nuovo account di accesso**.</span><span class="sxs-lookup"><span data-stu-id="b5214-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="b5214-162">In **Nome account di accesso** digitare **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="b5214-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="b5214-163">In hello **i ruoli del Server** pagina, fare clic su **sysadmin**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5214-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="b5214-164">Chiudere Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b5214-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="b5214-165">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b5214-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="b5214-166">Fase 3: Configurare il server LOB hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="b5214-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="b5214-167">Innanzitutto, creare una macchina virtuale per LOB1 con questi comandi al prompt dei comandi di Azure PowerShell hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="b5214-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b5214-168">Usare quindi hello tooconnect portale Azure tooLOB1 con le credenziali di hello dell'account di amministratore locale hello del LOB1.</span><span class="sxs-lookup"><span data-stu-id="b5214-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="b5214-169">Configurare quindi il traffico tooallow una regola Windows Firewall per verificare la connettività di base.</span><span class="sxs-lookup"><span data-stu-id="b5214-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="b5214-170">Da un prompt dei comandi di Windows PowerShell a livello di amministratore in LOB1 eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="b5214-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b5214-171">comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="b5214-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b5214-172">Aggiungere quindi LOB1 toohello CORP dominio Active Directory con questi comandi al prompt di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b5214-173">Account hello CORP\User1 quando viene richiesto di utilizzare le credenziali dell'account di dominio toosupply per hello **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="b5214-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b5214-174">Dopo il riavvio, usare hello tooconnect portale Azure tooLOB1 con hello CORP\User1 account e password.</span><span class="sxs-lookup"><span data-stu-id="b5214-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="b5214-175">Configurare LOB1 per IIS e verificare l'accesso da CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="b5214-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="b5214-176">In Server Manager fare clic su **Aggiungi ruoli e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="b5214-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="b5214-177">In hello **prima di iniziare** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="b5214-178">In hello **Selezione tipo di installazione** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="b5214-179">In hello **Selezione server di destinazione** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="b5214-180">In hello **i ruoli del Server** pagina, fare clic su **Server Web (IIS)** nell'elenco di hello di **ruoli**.</span><span class="sxs-lookup"><span data-stu-id="b5214-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="b5214-181">Quando richiesto, fare clic su **Aggiungi funzionalità**, quindi su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="b5214-182">In hello **Selezione funzionalità** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="b5214-183">In hello **Server Web (IIS)** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="b5214-184">In hello **Selezione servizi ruolo** pagina, selezionare o deselezionare le caselle di controllo hello per i servizi di hello è necessario per il test dell'applicazione LOB e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b5214-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="b5214-185">In hello **Conferma selezioni per l'installazione** pagina, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="b5214-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="b5214-186">Attendere finché non viene completata l'installazione di hello dei componenti e quindi fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="b5214-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="b5214-187">Dal portale di Azure hello, connettere computer CLIENT1 toohello con le credenziali dell'account di hello CORP\User1 e quindi avviare Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b5214-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="b5214-188">Nella barra degli indirizzi hello digitare **http://lob1/** e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="b5214-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="b5214-189">Si dovrebbe vedere pagina web di IIS 8 predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="b5214-190">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b5214-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b5214-191">Questo ambiente è ora pronto per toodeploy è basata sul web applicazione sulle funzionalità LOB1 e i test da CLIENT1 nella subnet Corpnet hello.</span><span class="sxs-lookup"><span data-stu-id="b5214-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="b5214-192">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b5214-192">Next step</span></span>
* <span data-ttu-id="b5214-193">Aggiungere una nuova macchina virtuale utilizzando hello [portale di Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5214-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

