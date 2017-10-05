---
title: "Configurare gruppi di disponibilità Always On in macchine virtuali di Azure con PowerShell | Microsoft Docs"
description: "Questa esercitazione usa risorse che sono state create con il modello di distribuzione classico. Usare PowerShell per creare un gruppo di disponibilità Always On in Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="fa7af-104">Configurare gruppi di disponibilità Always On in macchine virtuali di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa7af-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa7af-105">Classica: interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="fa7af-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="fa7af-106">[Classica: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="fa7af-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="fa7af-107">Prima di iniziare, considerare che ora è possibile completare questa attività nel modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="fa7af-108">Per le nuove distribuzioni è consigliabile usare il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa7af-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="fa7af-109">Vedere [gruppi di disponibilità Always On di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa7af-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa7af-110">Per le distribuzioni più recenti si consiglia di usare il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa7af-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fa7af-111">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa7af-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fa7af-112">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="fa7af-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="fa7af-113">Le macchine virtuali di Azure possono consentire agli amministratori di database di abbassare i costi di un sistema di SQL Server a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="fa7af-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="fa7af-114">Questa esercitazione illustra come implementare un gruppo di disponibilità tramite un end-to-end di SQL Server Always On in un ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="fa7af-115">Al termine dell'esercitazione la soluzione SQL Server AlwaysOn in Azure sarà composta dagli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="fa7af-116">Una rete virtuale contenente più subnet, tra cui una subnet front-end e una back-end.</span><span class="sxs-lookup"><span data-stu-id="fa7af-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="fa7af-117">Un controller di dominio con un dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa7af-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="fa7af-118">Due macchine virtuali di SQL Server distribuite nella subnet di back-end e aggiunte al dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa7af-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="fa7af-119">Un cluster di failover di Windows a 3 nodi con il modello di quorum Maggioranza dei nodi.</span><span class="sxs-lookup"><span data-stu-id="fa7af-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="fa7af-120">Un gruppo di disponibilità con due repliche con commit sincrono di un database di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="fa7af-121">Questo scenario viene scelto per la semplicità, non per la convenienza o altri fattori di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="fa7af-122">È possibile, ad esempio, ridurre il numero di macchine virtuali per un gruppo di disponibilità con due repliche per risparmiare ore di calcolo in Azure, usando il controller di dominio come condivisione file di controllo del quorum in un cluster di failover a 2 nodi.</span><span class="sxs-lookup"><span data-stu-id="fa7af-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="fa7af-123">Questo metodo consente di ridurre di un'unità il numero di macchine virtuali rispetto alla configurazione precedente.</span><span class="sxs-lookup"><span data-stu-id="fa7af-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="fa7af-124">Questa esercitazione ha lo scopo di illustrare la procedura necessaria per configurare la soluzione descritta in precedenza senza approfondire i dettagli di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="fa7af-125">Pertanto, anziché illustrare i passaggi di configurazione a livello di interfaccia utente grafica, vengono usati gli script di PowerShell per eseguire rapidamente ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="fa7af-126">Nell’esercitazione si presuppongono le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="fa7af-127">Si dispone già di un account Azure con la sottoscrizione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="fa7af-128">Sono stati installati i [cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa7af-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fa7af-129">Si ha già una conoscenza approfondita dei gruppi di disponibilità Always On per soluzioni locali.</span><span class="sxs-lookup"><span data-stu-id="fa7af-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="fa7af-130">Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa7af-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="fa7af-131">Connettersi alla sottoscrizione di Azure e creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fa7af-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="fa7af-132">In una finestra di PowerShell nel computer locale importare il modulo Azure, scaricare il file di impostazioni di pubblicazione nel computer e connettere la sessione di PowerShell alla sottoscrizione di Azure importando le impostazioni di pubblicazione scaricate.</span><span class="sxs-lookup"><span data-stu-id="fa7af-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="fa7af-133">Il comando **Get-AzurePublishSettingsFile** genera automaticamente un certificato di gestione con Azure e lo scarica nel computer.</span><span class="sxs-lookup"><span data-stu-id="fa7af-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="fa7af-134">Viene aperto un browser in automatico e viene richiesto di immettere le credenziali dell'account Microsoft per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="fa7af-135">Il file **.publishsettings** scaricato contiene tutte le informazioni necessarie per gestire la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="fa7af-136">Dopo aver salvato il file in una directory locale, importarlo usando il comando **Import-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa7af-137">Il file .publishsettings contiene le credenziali (non codificate) usate per amministrare le sottoscrizioni e i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="fa7af-138">La procedura consigliata di sicurezza per questo file consiste nell'archiviarlo temporaneamente all'esterno delle directory di origine, ad esempio nella cartella Raccolte\Documenti, e quindi eliminarlo al termine dell'importazione.</span><span class="sxs-lookup"><span data-stu-id="fa7af-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="fa7af-139">Un utente malintenzionato che riesce ad accedere al file .publishsettings può modificare, creare ed eliminare i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="fa7af-140">Definire una serie di variabili con cui si creerà l'infrastruttura IT cloud.</span><span class="sxs-lookup"><span data-stu-id="fa7af-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="fa7af-141">Prestare attenzione a quanto segue per assicurarsi che i comandi funzionino correttamente in un secondo momento:</span><span class="sxs-lookup"><span data-stu-id="fa7af-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="fa7af-142">Le variabili **$storageAccountName** e **$dcServiceName** devono essere univoche perché vengono usate per identificare rispettivamente l'account di archiviazione cloud e il server cloud su Internet.</span><span class="sxs-lookup"><span data-stu-id="fa7af-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="fa7af-143">I nomi specificati per le variabili **$affinityGroupName** e **$virtualNetworkName** sono configurati nel documento di configurazione della rete virtuale che verrà usato in seguito.</span><span class="sxs-lookup"><span data-stu-id="fa7af-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="fa7af-144">**$sqlImageName** viene specificato il nome aggiornato dell'immagine della macchina virtuale in cui è contenuto SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="fa7af-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="fa7af-145">Per semplicità, **Contoso!000** corrisponde alla stessa password usata nel corso dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fa7af-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="fa7af-146">Creare un set di affinità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="fa7af-147">Creare una rete virtuale importando un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa7af-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="fa7af-148">Il file di configurazione contiene il documento XML seguente.</span><span class="sxs-lookup"><span data-stu-id="fa7af-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="fa7af-149">In breve, specifica una rete virtuale denominata **ContosoNET** nel gruppo di affinità denominato **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="fa7af-150">Include lo spazio degli indirizzi **10.10.0.0/16** e dispone di due subnet, **10.10.1.0/24** e **10.10.2.0/24**, che sono rispettivamente la subnet anteriore e la subnet posteriore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="fa7af-151">Nella subnet anteriore è possibile inserire applicazioni client quali Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fa7af-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="fa7af-152">Nella subnet posteriore è possibile inserire le macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="fa7af-153">Se si modificano le variabili **$affinityGroupName** e **$virtualNetworkName**, è necessario modificare anche i nomi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="fa7af-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="fa7af-154">Creare un account di archiviazione associato al gruppo di affinità creato e impostarlo come account di archiviazione corrente nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fa7af-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="fa7af-155">Creare il server controller di dominio nel nuovo servizio cloud e nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-155">Create the domain controller server in the new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="fa7af-156">Questi comandi inoltrati tramite pipe consente di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="fa7af-157">**New-AzureVMConfig** consente di creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="fa7af-158">**Add-AzureProvisioningConfig** fornisce i parametri di configurazione di un server Windows autonomo.</span><span class="sxs-lookup"><span data-stu-id="fa7af-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="fa7af-159">**Add-AzureDataDisk** consente di aggiungere il disco dati che verrà usato per l'archiviazione dei dati di Active Directory, con l'opzione di memorizzazione nella cache impostata su Nessuna.</span><span class="sxs-lookup"><span data-stu-id="fa7af-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="fa7af-160">**New-AzureVM** consente di creare un nuovo servizio cloud e la nuova macchina virtuale di Azure nel nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa7af-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="fa7af-161">Al termine del provisioning della nuova macchina virtuale, scaricare il file del desktop remoto nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fa7af-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="fa7af-162">Poiché il provisioning della nuova macchina virtuale di Azure richiede molto tempo, tramite il ciclo `while` verrà continuata l'esecuzione del polling della nuova macchina virtuale finché non è pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="fa7af-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="fa7af-163">A questo punto, il provisioning del server del controller di dominio è completato.</span><span class="sxs-lookup"><span data-stu-id="fa7af-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="fa7af-164">Si configurerà quindi il dominio di Active Directory nel server del controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="fa7af-165">Uscire dalla finestra di PowerShell aperta nel computer locale,</span><span class="sxs-lookup"><span data-stu-id="fa7af-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="fa7af-166">che verrà usata di nuovo in un secondo momento per creare le due macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="fa7af-167">Configurare il controller di dominio</span><span class="sxs-lookup"><span data-stu-id="fa7af-167">Configure the domain controller</span></span>
1. <span data-ttu-id="fa7af-168">Connettersi al server del controller di dominio avviando il file del desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="fa7af-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="fa7af-169">Usare il nome utente dell'amministratore della macchina, AzureAdmin e la password **Contoso!000**specificata durante la creazione della nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="fa7af-170">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="fa7af-171">Eseguire il comando **DCPROMO.EXE** per installare il dominio **corp.contoso.com**, con le directory dei dati nell'unità M.</span><span class="sxs-lookup"><span data-stu-id="fa7af-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="fa7af-172">Al termine dell'esecuzione del comando, la macchina virtuale viene riavviata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fa7af-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="fa7af-173">Connettersi di nuovo al server del controller di dominio avviando il file del desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="fa7af-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="fa7af-174">Questa volta accedere come **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="fa7af-175">Aprire una finestra di PowerShell in modalità amministratore e importare il modulo Active Directory PowerShell usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa7af-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="fa7af-176">Eseguire i comandi indicati di seguito per aggiungere tre utenti al dominio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-176">Run the following commands to add three users to the domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="fa7af-177">**CORP\Install** viene usato per configurare tutti gli elementi correlati alle istanze del servizio SQL Server, al cluster di failover e al gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="fa7af-178">**CORP\SQLSvc1** e **CORP\SQLSvc2** vengono usati come account del servizio SQL Server per le due macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="fa7af-179">Eseguire quindi i comandi indicati di seguito per concedere a **CORP\Install** le autorizzazioni per creare oggetti computer nel dominio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="fa7af-180">Il GUID specificato in precedenza è il GUID per il tipo di oggetto computer.</span><span class="sxs-lookup"><span data-stu-id="fa7af-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="fa7af-181">L'account **CORP\Install** deve disporre delle autorizzazioni **Leggi tutte le proprietà** e **Crea oggetti computer** per creare gli oggetti Active Directory per il cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="fa7af-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="fa7af-182">L'autorizzazione **Leggi tutte le proprietà** è già assegnata a CORP\Install per impostazione predefinita, quindi non è necessario concederla in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="fa7af-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="fa7af-183">Per altre informazioni sulle autorizzazioni necessarie per creare il cluster di failover, vedere [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx) (Guida dettagliata del cluster di failover relativa alla configurazione di account in Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fa7af-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="fa7af-184">Dopo aver completato la configurazione di Active Directory e degli oggetti utente, si procederà alla creazione di due macchine virtuali di SQL Server che verranno aggiunte al dominio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="fa7af-185">Creare le macchine virtuali di SQL Server</span><span class="sxs-lookup"><span data-stu-id="fa7af-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="fa7af-186">Continuare a usare la finestra di PowerShell aperta sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="fa7af-187">Definire le variabili aggiuntive seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-187">Define the following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="fa7af-188">L'indirizzo IP **10.10.0.4** viene in genere assegnato alla prima macchina virtuale creata nella subnet **10.10.0.0/16** della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="fa7af-189">È necessario verificare che corrisponda all'indirizzo del server del controller di dominio eseguendo **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="fa7af-190">Eseguire i comandi seguenti inoltrati tramite pipe per creare la prima VM nel cluster di failover, denominata **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="fa7af-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="fa7af-191">Si noti quanto segue riguardo al comando precedente:</span><span class="sxs-lookup"><span data-stu-id="fa7af-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="fa7af-192">**New-AzureVMConfig** consente di creare una configurazione di macchina virtuale con il nome del set di disponibilità desiderato.</span><span class="sxs-lookup"><span data-stu-id="fa7af-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="fa7af-193">Le macchine virtuali successive verranno create con lo stesso nome del set di disponibilità, affinché siano aggiunte allo stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="fa7af-194">**Add-AzureProvisioningConfig** consente di aggiungere la macchina virtuale al dominio di Active Directory creato.</span><span class="sxs-lookup"><span data-stu-id="fa7af-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="fa7af-195">**Set AzureSubnet** consente di inserire la macchina virtuale nella subnet posteriore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="fa7af-196">**New-AzureVM** consente di creare un nuovo servizio cloud e la nuova macchina virtuale di Azure nel nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fa7af-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="fa7af-197">Il parametro **DnsSettings** specifica che l'indirizzo IP del server DNS per i server nel nuovo servizio cloud è **10.10.0.4**,</span><span class="sxs-lookup"><span data-stu-id="fa7af-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="fa7af-198">ovvero l'indirizzo IP del server del controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="fa7af-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="fa7af-199">Questo parametro è necessario per consentire di aggiungere correttamente le nuove macchine virtuali nel servizio cloud al dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa7af-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="fa7af-200">Senza questo parametro, è necessario configurare manualmente le impostazioni IPv4 nella macchina virtuale per usare il server del controller di dominio come server DNS primario dopo il provisioning della macchina virtuale e aggiungere quindi tale macchina virtuale al dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa7af-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="fa7af-201">Eseguire i comandi inoltrati tramite pipe indicati di seguito per creare le macchine virtuali di SQL Server, denominate **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="fa7af-202">Si noti quanto segue riguardo i comandi precedenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="fa7af-203">**New-AzureVMConfig** usa lo stesso nome del set di disponibilità del server del controller di dominio e l'immagine di SQL Server 2012 Service Pack 1 Enterprise Edition nella raccolta di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fa7af-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="fa7af-204">Consente inoltre di impostare il disco del sistema operativo sulla modalità sola lettura della cache (scrittura non consentita).</span><span class="sxs-lookup"><span data-stu-id="fa7af-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="fa7af-205">È consigliabile eseguire la migrazione dei file di database in un disco dati separato collegato alla macchina virtuale e configurarlo senza lettura né scrittura nella cache.</span><span class="sxs-lookup"><span data-stu-id="fa7af-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="fa7af-206">Il passaggio successivo consigliato consiste tuttavia nel rimuovere la scrittura nella cache sul disco del sistema operativo, non essendo possibile rimuovere la lettura della cache su tale disco.</span><span class="sxs-lookup"><span data-stu-id="fa7af-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="fa7af-207">**Add-AzureProvisioningConfig** consente di aggiungere la macchina virtuale al dominio di Active Directory creato.</span><span class="sxs-lookup"><span data-stu-id="fa7af-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="fa7af-208">**Set AzureSubnet** consente di inserire la macchina virtuale nella subnet posteriore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="fa7af-209">**Add-AzureEndpoint** consente di aggiungere endpoint di accesso in modo da consentire alle applicazioni client di accedere a tali istanze dei servizi SQL Server su Internet.</span><span class="sxs-lookup"><span data-stu-id="fa7af-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="fa7af-210">A ContosoSQL1 e ContosoSQL2 vengono assegnate porte diverse.</span><span class="sxs-lookup"><span data-stu-id="fa7af-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="fa7af-211">**New-AzureVM** consente di creare la nuova macchina virtuale di SQL Server nello stesso servizio cloud di ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="fa7af-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="fa7af-212">È necessario inserire le macchine virtuali nello stesso servizio cloud se si desidera includerle nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="fa7af-213">Attendere il provisioning di ogni macchina virtuale e per ciascuna macchina virtuale scaricare il relativo file del desktop remoto nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fa7af-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="fa7af-214">Il ciclo `for` si ripete nelle tre nuove macchine virtuali ed esegue i comandi all'interno delle parentesi graffe di livello principale per ognuna di esse.</span><span class="sxs-lookup"><span data-stu-id="fa7af-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="fa7af-215">Completato il provisioning, le macchine virtuali di SQL Server sono in esecuzione, ma vengono installate con SQL Server usando le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="fa7af-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="fa7af-216">Inizializzare le macchine virtuali del cluster di failover</span><span class="sxs-lookup"><span data-stu-id="fa7af-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="fa7af-217">In questa sezione è necessario modificare i tre server da usare nel cluster di failover e nell'installazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="fa7af-218">In particolare:</span><span class="sxs-lookup"><span data-stu-id="fa7af-218">Specifically:</span></span>

* <span data-ttu-id="fa7af-219">Tutti i server: è necessario installare la funzionalità **Failover Clustering**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="fa7af-220">Tutti i server: è necessario aggiungere **CORP\Install** come **amministratore** del computer.</span><span class="sxs-lookup"><span data-stu-id="fa7af-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="fa7af-221">Solo ContosoSQL1 e ContosoSQL2: è necessario aggiungere **CORP\Install** come ruolo **sysadmin** nel database predefinito.</span><span class="sxs-lookup"><span data-stu-id="fa7af-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="fa7af-222">Solo ContosoSQL1 e ContosoSQL2: è necessario aggiungere **NT AUTHORITY\System** come account di accesso con le autorizzazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="fa7af-223">Alterare eventuali gruppi di disponibilità</span><span class="sxs-lookup"><span data-stu-id="fa7af-223">Alter any availability group</span></span>
  * <span data-ttu-id="fa7af-224">Connettersi a SQL</span><span class="sxs-lookup"><span data-stu-id="fa7af-224">Connect SQL</span></span>
  * <span data-ttu-id="fa7af-225">Visualizzare lo stato del server</span><span class="sxs-lookup"><span data-stu-id="fa7af-225">View server state</span></span>
* <span data-ttu-id="fa7af-226">Solo ContosoSQL1 e ContosoSQL2: l protocollo **TCP** è già abilitato nella VM di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="fa7af-227">Sarà tuttavia necessario aprire il firewall per l'accesso remoto di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="fa7af-228">A questo punto è possibile iniziare.</span><span class="sxs-lookup"><span data-stu-id="fa7af-228">Now, you're ready to start.</span></span> <span data-ttu-id="fa7af-229">A partire da **ContosoQuorum**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fa7af-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="fa7af-230">Connettersi a **ContosoQuorum** avviando i file desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="fa7af-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="fa7af-231">Usare il nome utente dell'amministratore della macchina, **AzureAdmin** e la password **Contoso!000** specificata durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="fa7af-232">Verificare che i computer siano stati aggiunti correttamente a **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="fa7af-233">Prima di procedere, attendere la fine dell'esecuzione delle attività di inizializzazione automatiche nell'ambito dell'installazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="fa7af-234">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="fa7af-235">Installare la funzionalità Clustering di failover di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa7af-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="fa7af-236">Aggiungere **CORP\Install** come amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="fa7af-237">Disconnettersi da ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="fa7af-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="fa7af-238">Le operazioni relative a questo server sono state completate.</span><span class="sxs-lookup"><span data-stu-id="fa7af-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="fa7af-239">Inizializzare quindi **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="fa7af-240">Seguire la procedura descritta di seguito, che è identica per entrambe le macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="fa7af-241">Connettersi alle due macchine virtuali di SQL Server avviando i file del desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="fa7af-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="fa7af-242">Usare il nome utente dell'amministratore della macchina, **AzureAdmin** e la password **Contoso!000** specificata durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="fa7af-243">Verificare che i computer siano stati aggiunti correttamente a **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="fa7af-244">Prima di procedere, attendere la fine dell'esecuzione delle attività di inizializzazione automatiche nell'ambito dell'installazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="fa7af-245">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="fa7af-246">Installare la funzionalità Clustering di failover di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa7af-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="fa7af-247">Aggiungere **CORP\Install** come amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="fa7af-248">Importare il provider PowerShell per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="fa7af-249">Aggiungere **CORP\Install** come ruolo sysadmin per l'istanza predefinita di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="fa7af-250">Aggiungere **NT AUTHORITY\System** come account di accesso con le tre autorizzazioni descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fa7af-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="fa7af-251">Aprire il firewall per l'accesso remoto di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="fa7af-252">Disconnettersi da entrambe le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fa7af-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="fa7af-253">A questo punto, è possibile procedere con la configurazione del gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="fa7af-254">Il provider PowerShell per SQL Server verrà usato per eseguire tutte le operazioni in **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="fa7af-255">Configurare il gruppo di disponibilità</span><span class="sxs-lookup"><span data-stu-id="fa7af-255">Configure the availability group</span></span>
1. <span data-ttu-id="fa7af-256">Connettersi di nuovo a **ContosoSQL1** avviando i file del desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="fa7af-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="fa7af-257">Anziché accedere con l'account del computer, eseguire l'accesso con **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="fa7af-258">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa7af-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="fa7af-259">Definire le variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa7af-259">Define the following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="fa7af-260">Importare il provider PowerShell per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="fa7af-261">Modificare l'account del servizio SQL Server per ContosoSQL1 in CORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="fa7af-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="fa7af-262">Modificare l'account del servizio SQL Server per ContosoSQL2 in CORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="fa7af-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="fa7af-263">Scaricare **CreateAzureFailoverCluster.ps1** dalla pagina [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) (Creare il cluster di failover per i gruppi di disponibilità AlwaysOn in una VM di Azure) nella directory di lavoro locale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="fa7af-264">Usare lo script per creare un cluster di failover funzionale.</span><span class="sxs-lookup"><span data-stu-id="fa7af-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="fa7af-265">Per informazioni importanti sull'interazione del servizio Clustering di failover di Windows con la rete di Azure, vedere [Disponibilità elevata e ripristino di emergenza per SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa7af-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="fa7af-266">Passare alla directory di lavoro e creare il cluster di failover con lo script scaricato.</span><span class="sxs-lookup"><span data-stu-id="fa7af-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="fa7af-267">Abilitare i gruppi di disponibilità Always On per le istanze predefinite di SQL Server in **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="fa7af-268">Creare una directory di backup e concedere le autorizzazioni per gli account del servizio SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa7af-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="fa7af-269">Usare questa directory per preparare il database di disponibilità nella replica secondaria.</span><span class="sxs-lookup"><span data-stu-id="fa7af-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="fa7af-270">Creare un database in **ContosoSQL1** denominato **MyDB1**, eseguire un backup completo e un backup dei log e ripristinarli in **ContosoSQL2** con l'opzione **WITH NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="fa7af-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="fa7af-271">Creare gli endpoint dei gruppi di disponibilità nelle macchine virtuali di SQL Server e impostare le autorizzazioni appropriate negli endpoint.</span><span class="sxs-lookup"><span data-stu-id="fa7af-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="fa7af-272">Creare le repliche di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-272">Create the availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="fa7af-273">Creare infine il gruppo di disponibilità e creare un join tra la replica secondaria e il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="fa7af-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="fa7af-274">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa7af-274">Next steps</span></span>
<span data-ttu-id="fa7af-275">SQL Server Always On è stato correttamente implementato mediante la creazione di un gruppo di disponibilità in Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7af-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="fa7af-276">Per configurare un listener per questo gruppo di disponibilità, vedere [Configurare un listener ILB per gruppi di disponibilità Always On in Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="fa7af-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="fa7af-277">Per altre informazioni sull'uso di SQL Server in Azure, vedere [Panoramica di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa7af-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
