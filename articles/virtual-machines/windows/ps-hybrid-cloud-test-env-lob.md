---
title: Ambiente di test di applicazioni LOB | Microsoft Docs
description: Informazioni su come creare un'applicazione line-of-business basata su Web in un ambiente cloud ibrido per professionisti IT o test di sviluppo.
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
ms.openlocfilehash: 8e9a380458bfede80ed0fc1ee7e62b0caec09501
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="51584-103">Configurazione di un'applicazione LOB basata sul Web in un cloud ibrido per l'esecuzione di test</span><span class="sxs-lookup"><span data-stu-id="51584-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="51584-104">Questo argomento descrive la creazione di un ambiente cloud ibrido simulato per testare un'applicazione line-of-business basata su Web ospitata in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="51584-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="51584-105">Di seguito è riportata la configurazione risultante.</span><span class="sxs-lookup"><span data-stu-id="51584-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="51584-106">Questa configurazione è costituita da:</span><span class="sxs-lookup"><span data-stu-id="51584-106">This configuration consists of:</span></span>

* <span data-ttu-id="51584-107">Una rete locale simulata ospitata in Azure (la rete virtuale TestLab).</span><span class="sxs-lookup"><span data-stu-id="51584-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="51584-108">Una rete virtuale cross-premise ospitata in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="51584-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="51584-109">Una connessione VPN da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="51584-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="51584-110">Un server LOB basato sul Web, SQL Server e un controller di dominio secondario nella rete virtuale TestVNET.</span><span class="sxs-lookup"><span data-stu-id="51584-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="51584-111">Questa configurazione rappresenta una base e un punto di partenza comune da cui è possibile:</span><span class="sxs-lookup"><span data-stu-id="51584-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="51584-112">Sviluppare e testare le applicazioni LOB ospitate in Internet Information Services (IIS) con un back-end del database di SQL Server 2014 in Azure.</span><span class="sxs-lookup"><span data-stu-id="51584-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="51584-113">Eseguire il test di questo carico di lavoro IT basato sul cloud ibrido simulato.</span><span class="sxs-lookup"><span data-stu-id="51584-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="51584-114">La configurazione di questo ambiente di test cloud ibrido prevede tre fasi principali:</span><span class="sxs-lookup"><span data-stu-id="51584-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="51584-115">Configurare l'ambiente cloud ibrido simulato.</span><span class="sxs-lookup"><span data-stu-id="51584-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="51584-116">Configurare il computer SQL server (SQL1).</span><span class="sxs-lookup"><span data-stu-id="51584-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="51584-117">Configurare il server LOB (LOB1).</span><span class="sxs-lookup"><span data-stu-id="51584-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="51584-118">Questo carico di lavoro richiede una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="51584-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="51584-119">Se si ha una sottoscrizione di MSDN o di Visual Studio, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="51584-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="51584-120">Per un esempio di applicazione LOB di produzione ospitata in Azure, vedere il progetto di architettura **Applicazioni line-of-business** in [Progetti e diagrammi dell’architettura del Software Microsoft](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="51584-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="51584-121">Fase 1: Configurare l'ambiente cloud ibrido simulato</span><span class="sxs-lookup"><span data-stu-id="51584-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="51584-122">Creare l'[ambiente di test cloud ibrido simulato](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51584-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="51584-123">Poiché l'ambiente di test non richiede la presenza del server APP1 nella subnet Corpnet, è possibile arrestarlo per il momento.</span><span class="sxs-lookup"><span data-stu-id="51584-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="51584-124">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="51584-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="51584-125">Fase 2: Configurare il computer SQL server (SQL1)</span><span class="sxs-lookup"><span data-stu-id="51584-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="51584-126">Dal portale di Azure avviare il computer DC2, se necessario.</span><span class="sxs-lookup"><span data-stu-id="51584-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="51584-127">Successivamente, creare una macchina virtuale per SQL1 con questi comandi in un prompt dei comandi di Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="51584-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="51584-128">Per usare questi comandi, inserire i valori delle variabili e rimuovere i caratteri <and>.</span><span class="sxs-lookup"><span data-stu-id="51584-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="51584-129">Usare il portale di Azure per connettersi a SQL1 con l'account amministratore locale di SQL1.</span><span class="sxs-lookup"><span data-stu-id="51584-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="51584-130">Configurare quindi le regole di Windows Firewall per consentire il traffico di SQL Server e per i test di connettività di base.</span><span class="sxs-lookup"><span data-stu-id="51584-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="51584-131">Da un prompt dei comandi di Windows PowerShell a livello di amministratore in SQL1 eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="51584-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="51584-132">Il comando ping restituirà quattro risposte dall'indirizzo IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="51584-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="51584-133">Aggiungere quindi il disco dati aggiuntivo in SQL1 come nuovo volume con la lettera di unità F:.</span><span class="sxs-lookup"><span data-stu-id="51584-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="51584-134">Nel riquadro sinistro di Server Manager fare clic su **Servizi file e archiviazione**, quindi scegliere **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="51584-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="51584-135">Nel riquadro del contenuto nel gruppo **Dischi** fare clic su **disco 2** (con la **Partizione** impostata su **Sconosciuto**).</span><span class="sxs-lookup"><span data-stu-id="51584-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="51584-136">Fare clic su **Attività**, quindi su **Nuovo volume**.</span><span class="sxs-lookup"><span data-stu-id="51584-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="51584-137">Nella pagina Operazioni preliminari della creazione guidata nuovo volume fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="51584-138">Nella pagina Selezionare il server e il disco fare clic su **Disco 2**, quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="51584-139">Quando richiesto, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="51584-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="51584-140">Nella pagina Specifica dimensioni del volume fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="51584-141">Nella pagina Assegnare a una lettera di unità o cartella fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="51584-142">Nella pagina Selezionare le impostazioni del file system fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="51584-143">Nella pagina Conferma selezioni, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="51584-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="51584-144">Al termine, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="51584-144">When complete, click **Close**.</span></span>

<span data-ttu-id="51584-145">Eseguire questi comandi al prompt dei comandi di Windows PowerShell in SQL1:</span><span class="sxs-lookup"><span data-stu-id="51584-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="51584-146">Aggiungere SQL1 al dominio CORP di Windows Server Active Directory con questi comandi al prompt di Windows PowerShell in SQL1.</span><span class="sxs-lookup"><span data-stu-id="51584-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="51584-147">Usare l'account CORP\User1 quando viene richiesto di specificare le credenziali dell'account di dominio per il comando **Add-Computer**.</span><span class="sxs-lookup"><span data-stu-id="51584-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="51584-148">Dopo il riavvio, usare il portale di Azure per connettersi a SQL1 *con l'account amministratore locale di SQL1*.</span><span class="sxs-lookup"><span data-stu-id="51584-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="51584-149">Configurare quindi SQL Server 2014 in modo che usi l'unità F: per i nuovi database e per le autorizzazioni dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="51584-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="51584-150">Dalla schermata Start digitare **SQL Server Management**, quindi fare clic su **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="51584-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="51584-151">In **Connetti al server** fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="51584-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="51584-152">Nel riquadro dell'albero Esplora oggetti, fare doppio clic su **SQL1**, quindi fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="51584-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="51584-153">Nella finestra **Proprietà server** fare clic su **Impostazioni database**.</span><span class="sxs-lookup"><span data-stu-id="51584-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="51584-154">Individuare **Percorsi predefiniti del Database** e impostare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="51584-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="51584-155">Per **Dati**, digitare il percorso **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="51584-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="51584-156">Per **Log**, digitare il percorso **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="51584-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="51584-157">Per **Backup**, digitare il percorso **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="51584-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="51584-158">Nota: Solo i nuovi database utilizzeranno questi percorsi.</span><span class="sxs-lookup"><span data-stu-id="51584-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="51584-159">Fare clic su **OK** per chiudere la finestra.</span><span class="sxs-lookup"><span data-stu-id="51584-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="51584-160">Nel riquadro dell'albero **Esplora oggetti** aprire **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="51584-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="51584-161">Fare clic con il pulsante destro del mouse su **Account di accesso**, quindi scegliere **Nuovo account di accesso**.</span><span class="sxs-lookup"><span data-stu-id="51584-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="51584-162">In **Nome account di accesso** digitare **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="51584-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="51584-163">Nella pagina **Ruoli server** fare clic su **sysadmin**, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="51584-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="51584-164">Chiudere Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="51584-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="51584-165">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="51584-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="51584-166">Fase 3: Configurare il server LOB (LOB1)</span><span class="sxs-lookup"><span data-stu-id="51584-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="51584-167">Creare prima di tutto una macchina virtuale per LOB1 con questi comandi in un prompt dei comandi di Azure PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="51584-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="51584-168">Usare quindi il portale di Azure per connettersi a LOB1 con le credenziali dell'account amministratore locale di LOB1.</span><span class="sxs-lookup"><span data-stu-id="51584-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="51584-169">Configurare quindi una regola di Windows Firewall per permettere il traffico per il test della connettività di base.</span><span class="sxs-lookup"><span data-stu-id="51584-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="51584-170">Da un prompt dei comandi di Windows PowerShell a livello di amministratore in LOB1 eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="51584-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="51584-171">Il comando ping restituirà quattro risposte dall'indirizzo IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="51584-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="51584-172">Aggiungere LOB1 al dominio CORP di Active Directory con questi comandi al prompt di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51584-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="51584-173">Usare l'account CORP\User1 quando viene richiesto di specificare le credenziali dell'account di dominio per il comando **Add-Computer**.</span><span class="sxs-lookup"><span data-stu-id="51584-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="51584-174">Dopo il riavvio, usare il portale di Azure per connettersi a LOB1 con l'account CORP\User1 e la password.</span><span class="sxs-lookup"><span data-stu-id="51584-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="51584-175">Configurare LOB1 per IIS e verificare l'accesso da CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="51584-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="51584-176">In Server Manager fare clic su **Aggiungi ruoli e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="51584-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="51584-177">Nella pagina **Prima di iniziare** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="51584-178">Nella pagina **Selezione tipo di installazione** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="51584-179">Nella pagina **Selezione server di destinazione** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="51584-180">Nella pagina **Ruoli server** fare clic su **Web Server (IIS)** nell'elenco **Ruoli**.</span><span class="sxs-lookup"><span data-stu-id="51584-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="51584-181">Quando richiesto, fare clic su **Aggiungi funzionalità**, quindi su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="51584-182">Nella pagina **Selezione funzionalità** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="51584-183">Nella pagina **Server Web (IIS)** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="51584-184">Nella pagina **Selezione servizi ruolo** selezionare o deselezionare le caselle di controllo per i servizi necessari per i test dell'applicazione LOB, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="51584-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="51584-185">Nella pagina **Conferma selezioni per l'installazione** fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="51584-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="51584-186">Attendere il completamento dell'installazione dei componenti, quindi fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="51584-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="51584-187">Dal portale di Azure connettersi al computer CLIENT1 con le credenziali dell'account CORP\User1 e quindi avviare Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="51584-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="51584-188">Nella barra degli indirizzi digitare **http://lob1/**, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="51584-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="51584-189">Viene visualizzata la pagina Web IIS 8 predefinita.</span><span class="sxs-lookup"><span data-stu-id="51584-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="51584-190">Questa è la configurazione corrente.</span><span class="sxs-lookup"><span data-stu-id="51584-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="51584-191">Questo ambiente è ora pronto per la distribuzione dell'applicazione basata su Web in LOB1 e per i test delle funzionalità da CLIENT1 nella subnet Corpnet.</span><span class="sxs-lookup"><span data-stu-id="51584-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="51584-192">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="51584-192">Next step</span></span>
* <span data-ttu-id="51584-193">Aggiungere una nuova macchina virtuale usando il [portale di Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51584-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

