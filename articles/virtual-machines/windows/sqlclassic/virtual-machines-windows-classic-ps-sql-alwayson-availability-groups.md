---
title: "aaaConfigure hello sempre nel gruppo di disponibilità su una macchina virtuale di Azure tramite PowerShell | Documenti Microsoft"
description: "In questa esercitazione Usa risorse che sono state create con il modello di distribuzione classica hello. Utilizzare PowerShell toocreate un gruppo di disponibilità AlwaysOn in Azure."
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
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="409d2-104">Configurare hello sempre nel gruppo di disponibilità su una macchina virtuale di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="409d2-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="409d2-105">Classica: interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="409d2-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="409d2-106">[Classica: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="409d2-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="409d2-107">Prima di iniziare, considerare che ora è possibile completare questa attività nel modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="409d2-108">Per le nuove distribuzioni è consigliabile usare il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="409d2-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="409d2-109">Vedere [gruppi di disponibilità Always On di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="409d2-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409d2-110">È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="409d2-111">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="409d2-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="409d2-112">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="409d2-113">Macchine virtuali di Azure (VM) consente di costo toolower hello gli amministratori del database di un sistema di SQL Server a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="409d2-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="409d2-114">Questa esercitazione viene illustrato come tooimplement una disponibilità gruppo utilizzando SQL Server Always On end-to-end in un ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="409d2-115">Al fine di hello dell'esercitazione hello, la soluzione SQL Server Always On in Azure sarà composta dagli hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="409d2-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="409d2-116">Una rete virtuale contenente più subnet, tra cui una subnet front-end e una back-end.</span><span class="sxs-lookup"><span data-stu-id="409d2-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="409d2-117">Un controller di dominio con un dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="409d2-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="409d2-118">Due macchine virtuali di Server SQL che sono distribuiti toohello subnet di back-end e toohello aggiunti a un dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="409d2-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="409d2-119">Un cluster di failover Windows tre nodi con modello di quorum maggioranza dei nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="409d2-120">Un gruppo di disponibilità con due repliche con commit sincrono di un database di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="409d2-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="409d2-121">Questo scenario viene scelto per la semplicità, non per la convenienza o altri fattori di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="409d2-122">Ad esempio, è possibile ridurre numero hello di macchine virtuali per un toosave gruppo di disponibilità con due repliche sulle ore di calcolo in Azure tramite il controller di dominio hello come hello quorum condivisione file di controllo in un cluster di failover a due nodi.</span><span class="sxs-lookup"><span data-stu-id="409d2-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="409d2-123">Questo metodo riduce il numero VM hello rispetto hello di sopra di configurazione.</span><span class="sxs-lookup"><span data-stu-id="409d2-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="409d2-124">Questa esercitazione è destinata hello passaggi che sono necessari tooset backup hello tooshow descritto soluzione precedente, senza approfondire i dettagli di hello di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="409d2-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="409d2-125">Di conseguenza, invece che fornisce i passaggi di configurazione GUI hello, viene utilizzato PowerShell scripting tootake si rapidamente tramite ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="409d2-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="409d2-126">Questa esercitazione si presuppone l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="409d2-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="409d2-127">Si dispone già di un account Azure con sottoscrizione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="409d2-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="409d2-128">È stato installato hello [cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="409d2-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="409d2-129">Si ha già una conoscenza approfondita dei gruppi di disponibilità Always On per soluzioni locali.</span><span class="sxs-lookup"><span data-stu-id="409d2-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="409d2-130">Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="409d2-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="409d2-131">Connettere tooyour sottoscrizione di Azure e creare la rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="409d2-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="409d2-132">In una finestra di PowerShell nel computer locale, importare hello modulo Azure, scaricare hello macchina tooyour file di impostazioni di pubblicazione e connettere il tooyour sessione PowerShell sottoscrizione di Azure importando le impostazioni di pubblicazione scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="409d2-133">Hello **Get-AzurePublishSettingsFile** comando genera automaticamente un certificato di gestione con Azure e lo scarica tooyour macchina.</span><span class="sxs-lookup"><span data-stu-id="409d2-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="409d2-134">Viene automaticamente aperto un browser e sei le credenziali dell'account Microsoft hello tooenter richiesta per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="409d2-135">Hello scaricato **publishsettings** file contiene tutte le informazioni di hello necessario toomanage la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="409d2-136">Dopo aver salvato la directory di file tooa locale, importarlo tramite hello **Import-AzurePublishSettingsFile** comando.</span><span class="sxs-lookup"><span data-stu-id="409d2-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="409d2-137">file con estensione publishsettings Hello contiene le credenziali (non codificate) vengono utilizzati tooadminister i servizi e le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="409d2-138">Hello protezione consigliata per questo file è toostore viene temporaneamente all'esterno delle directory di origine (ad esempio, nella cartella di raccolte\documenti hello) e quindi eliminarlo una volta terminata l'importazione di hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="409d2-139">Un utente malintenzionato ottiene il file con estensione publishsettings toohello di accesso possa modificare, creare ed eliminare i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="409d2-140">Definire una serie di variabili che si userà toocreate l'infrastruttura IT cloud.</span><span class="sxs-lookup"><span data-stu-id="409d2-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="409d2-141">Prestare attenzione toohello seguente tooensure che i comandi funzionino correttamente in un secondo momento:</span><span class="sxs-lookup"><span data-stu-id="409d2-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="409d2-142">Le variabili **$storageAccountName** e **$dcServiceName** deve essere univoco perché sono utilizzati tooidentify l'account di archiviazione cloud e il server del cloud, rispettivamente, su hello Internet.</span><span class="sxs-lookup"><span data-stu-id="409d2-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="409d2-143">i nomi specificati per le variabili di Hello **$affinityGroupName** e **$virtualNetworkName** configurati nel documento di configurazione di rete virtuale hello che verrà utilizzato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="409d2-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="409d2-144">**$sqlImageName** specifica il nome di hello aggiornato dell'immagine di macchina virtuale hello contenente SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="409d2-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="409d2-145">Per semplicità, **Contoso! 000** è hello stessa password utilizzata nel corso esercitazione intera hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="409d2-146">Creare un set di affinità.</span><span class="sxs-lookup"><span data-stu-id="409d2-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="409d2-147">Creare una rete virtuale importando un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="409d2-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="409d2-148">file di configurazione Hello contiene hello seguente documento XML.</span><span class="sxs-lookup"><span data-stu-id="409d2-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="409d2-149">In breve, specifica una rete virtuale denominata **ContosoNET** nel gruppo di affinità hello chiamato **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="409d2-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="409d2-150">Dispone di spazio degli indirizzi hello **10.10.0.0/16** e dispone di due subnet, **10.10.1.0/24** e **10.10.2.0/24**, che sono subnet di hello anteriore e posteriore, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="409d2-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="409d2-151">subnet front-Hello è dove è possibile inserire applicazioni client quali Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="409d2-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="409d2-152">subnet di back-Hello è in cui inserire le macchine virtuali di hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="409d2-153">Se si modifica hello **$affinityGroupName** e **$virtualNetworkName** variabili in precedenza, è necessario modificare anche hello corrispondenti ai nomi.</span><span class="sxs-lookup"><span data-stu-id="409d2-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

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

5. <span data-ttu-id="409d2-154">Creare un account di archiviazione associato hello gruppo di affinità creato e impostarlo come account di archiviazione corrente hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="409d2-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="409d2-155">Creare server di controller di dominio hello in hello nuovo cloud service e set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="409d2-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

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

    <span data-ttu-id="409d2-156">Questi comandi reindirizzati hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="409d2-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="409d2-157">**New-AzureVMConfig** consente di creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="409d2-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="409d2-158">**Aggiungere-AzureProvisioningConfig** offre hello parametri di configurazione di un server Windows autonomo.</span><span class="sxs-lookup"><span data-stu-id="409d2-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="409d2-159">**Aggiungere-AzureDataDisk** aggiunge il disco dati hello che verrà utilizzato per archiviare i dati di Active Directory, con l'opzione set tooNone di memorizzazione nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="409d2-160">**New-AzureVM** crea un nuovo servizio cloud e hello nuova macchina virtuale di Azure nel nuovo servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="409d2-161">Attendere hello nuova VM toobe stato effettuato il provisioning e scaricare directory di lavoro tooyour hello file desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="409d2-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="409d2-162">Poiché hello nuova macchina virtuale di Azure accetta un tooprovision molto tempo, hello `while` ciclo continua toopoll hello nuova macchina virtuale finché è pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="409d2-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

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

<span data-ttu-id="409d2-163">server del controller di dominio Hello ora correttamente il provisioning.</span><span class="sxs-lookup"><span data-stu-id="409d2-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="409d2-164">Successivamente, si configurerà il dominio di Active Directory hello in questo server di controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="409d2-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="409d2-165">Lasciare aperta la finestra di PowerShell hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="409d2-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="409d2-166">Si userà nuovamente toocreate successive hello due macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="409d2-167">Configurare il controller di dominio hello</span><span class="sxs-lookup"><span data-stu-id="409d2-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="409d2-168">Connessione server di controller di dominio toohello avviando i file del desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="409d2-169">Utilizzare AzureAdmin di nome utente e la password dell'amministratore del computer hello **Contoso! 000**, specificato al momento della creazione hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="409d2-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="409d2-170">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="409d2-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="409d2-171">Eseguire il seguente hello **DCPROMO. EXE** tooset comando backup hello **corp.contoso.com** dominio, con directory dei dati hello sull'unità M.</span><span class="sxs-lookup"><span data-stu-id="409d2-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

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

    <span data-ttu-id="409d2-172">Al termine del comando hello, hello VM viene riavviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="409d2-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="409d2-173">Connettere nuovamente toohello server controller di dominio avviando i file del desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="409d2-174">Questa volta accedere come **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="409d2-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="409d2-175">Aprire una finestra di PowerShell in modalità amministratore e importare il modulo di Active Directory PowerShell hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="409d2-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="409d2-176">Eseguire hello seguente dominio di toohello di comandi tooadd tre utenti.</span><span class="sxs-lookup"><span data-stu-id="409d2-176">Run hello following commands tooadd three users toohello domain.</span></span>

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

    <span data-ttu-id="409d2-177">**CORP\Install** è tooconfigure utilizzati tutti gli elementi correlati toohello le istanze del servizio SQL Server, il cluster di failover di hello e gruppo di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="409d2-178">**CORP\SQLSvc1** e **CORP\SQLSvc2** vengono utilizzati come account del servizio SQL Server hello per le macchine virtuali di hello due SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="409d2-179">Esempio hello successivo, eseguire i comandi toogive **CORP\Install** hello oggetti computer toocreate di autorizzazioni nel dominio hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="409d2-180">Hello GUID specificato in precedenza è hello GUID per il tipo di oggetto computer hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="409d2-181">Hello **CORP\Install** account deve hello **Leggi tutte le proprietà** e **crea oggetti Computer** hello toocreate autorizzazione Active Directory gli oggetti per il failover hello cluster.</span><span class="sxs-lookup"><span data-stu-id="409d2-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="409d2-182">Hello **Leggi tutte le proprietà** già autorizzazione tooCORP\Install per impostazione predefinita, pertanto non è necessario toogrant, in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="409d2-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="409d2-183">Per ulteriori informazioni sulle autorizzazioni che sono necessari il cluster di failover di toocreate hello, vedere [Guida dettagliata al Cluster di Failover: configurazione di account in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="409d2-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="409d2-184">Ora che è stata completata la configurazione di Active Directory e gli oggetti utente hello, viene creata due macchine virtuali di SQL Server e aggiungerle toothis dominio.</span><span class="sxs-lookup"><span data-stu-id="409d2-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="409d2-185">Creare macchine virtuali di hello SQL Server</span><span class="sxs-lookup"><span data-stu-id="409d2-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="409d2-186">Continuare toouse hello PowerShell finestra aperta sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="409d2-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="409d2-187">Definire hello variabili aggiuntive seguenti:</span><span class="sxs-lookup"><span data-stu-id="409d2-187">Define hello following additional variables:</span></span>

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

    <span data-ttu-id="409d2-188">indirizzo IP di Hello **10.10.0.4** viene in genere assegnata toohello prima VM creati in hello **10.10.0.0/16** subnet della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="409d2-189">È necessario verificare che sia questo indirizzo hello del server del controller di dominio eseguendo **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="409d2-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="409d2-190">Esecuzione hello seguente hello toocreate comandi reindirizzati prima macchina virtuale in cluster di failover hello, denominato **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="409d2-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="409d2-191">Si noti segue hello riguardanti hello comando precedente:</span><span class="sxs-lookup"><span data-stu-id="409d2-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="409d2-192">**Nuovo AzureVMConfig** crea una configurazione della macchina virtuale con nome del set di disponibilità desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="409d2-193">Hello macchine virtuali successive verranno create con hello stesso nome set di disponibilità in modo che si è aggiunto toohello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="409d2-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="409d2-194">**Aggiungere-AzureProvisioningConfig** join hello dominio di Active Directory toohello macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="409d2-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="409d2-195">**Set-AzureSubnet** posizioni hello VM nella subnet back-hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="409d2-196">**New-AzureVM** crea un nuovo servizio cloud e hello nuova macchina virtuale di Azure nel nuovo servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="409d2-197">Hello **DnsSettings** parametro specifica il server DNS hello per i server nel nuovo servizio cloud di hello hello è l'indirizzo IP hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="409d2-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="409d2-198">Questo è l'indirizzo IP di hello del server di controller di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="409d2-199">Questo parametro è necessario tooenable hello nuove macchine virtuali nel dominio di Active Directory toohello toojoin servizio cloud hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="409d2-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="409d2-200">Senza questo parametro, è necessario impostare manualmente le impostazioni IPv4 hello del server controller di dominio VM toouse hello come server DNS primario hello dopo hello VM viene eseguito il provisioning e quindi accedere al dominio Active Directory toohello VM hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="409d2-201">Esecuzione hello seguente reindirizzato comandi toocreate hello macchine virtuali di SQL Server, denominata **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="409d2-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="409d2-202">Si noti segue hello riguardanti hello comandi precedenti:</span><span class="sxs-lookup"><span data-stu-id="409d2-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="409d2-203">**Nuovo AzureVMConfig** utilizza hello stesso nome di set di disponibilità come server del controller di dominio hello e utilizza hello immagine di SQL Server 2012 Service Pack 1 Enterprise Edition nella raccolta di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="409d2-204">Imposta inoltre hello operativo sistema disco tooread sola cache (scrittura non consentita).</span><span class="sxs-lookup"><span data-stu-id="409d2-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="409d2-205">Si consiglia di migrare hello database file tooa disco dati separato toohello macchina virtuale, collegare e configurarlo senza lettura né scrittura nella cache.</span><span class="sxs-lookup"><span data-stu-id="409d2-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="409d2-206">Tuttavia, hello successivo consigliato consiste tooremove cache in scrittura sul disco del sistema operativo hello perché non è possibile rimuovere lettura della cache su disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="409d2-207">**Aggiungere-AzureProvisioningConfig** join hello dominio di Active Directory toohello macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="409d2-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="409d2-208">**Set-AzureSubnet** posizioni hello VM nella subnet back-hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="409d2-209">**Aggiungere-AzureEndpoint** aggiunge endpoint di accesso in modo che le applicazioni client possono accedere a queste istanze di servizi di SQL Server su Internet hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="409d2-210">TooContosoSQL1 e ContosoSQL2, vengono assegnate diverse porte.</span><span class="sxs-lookup"><span data-stu-id="409d2-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="409d2-211">**New-AzureVM** crea hello nuova VM SQL Server in hello stesso servizio cloud in cui ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="409d2-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="409d2-212">È necessario inserire le macchine virtuali hello in hello stesso servizio cloud se si desidera toobe in hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="409d2-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="409d2-213">Attendere la directory di lavoro di file del desktop remoto tooyour toobe ogni macchina virtuale completamente il provisioning e toodownload ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="409d2-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="409d2-214">Hello `for` ciclo scorre hello tre nuove macchine virtuali ed esegue i comandi di hello all'interno delle parentesi graffe principale hello per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="409d2-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
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

    <span data-ttu-id="409d2-215">macchine virtuali di Hello SQL Server viene ora eseguito il provisioning e in esecuzione, ma sono installati con SQL Server con le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="409d2-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="409d2-216">Inizializzare il cluster di failover hello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="409d2-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="409d2-217">In questa sezione, è necessario toomodify hello e tre i server che verrà utilizzato nel cluster di failover hello e installazione di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="409d2-218">In particolare:</span><span class="sxs-lookup"><span data-stu-id="409d2-218">Specifically:</span></span>

* <span data-ttu-id="409d2-219">Tutti i server: È necessario hello tooinstall **Clustering di Failover** funzionalità.</span><span class="sxs-lookup"><span data-stu-id="409d2-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="409d2-220">Tutti i server: È necessario tooadd **CORP\Install** come macchina hello **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="409d2-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="409d2-221">Solo ContosoSQL1 e ContosoSQL2: È necessario tooadd **CORP\Install** come un **sysadmin** ruolo nel database predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="409d2-222">Solo ContosoSQL1 e ContosoSQL2: È necessario tooadd **NT AUTHORITY\System** come accesso aggiuntivo con hello queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="409d2-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="409d2-223">Alterare eventuali gruppi di disponibilità</span><span class="sxs-lookup"><span data-stu-id="409d2-223">Alter any availability group</span></span>
  * <span data-ttu-id="409d2-224">Connettersi a SQL</span><span class="sxs-lookup"><span data-stu-id="409d2-224">Connect SQL</span></span>
  * <span data-ttu-id="409d2-225">Visualizzare lo stato del server</span><span class="sxs-lookup"><span data-stu-id="409d2-225">View server state</span></span>
* <span data-ttu-id="409d2-226">Solo ContosoSQL1 e ContosoSQL2: hello **TCP** è già abilitato nella macchina virtuale SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="409d2-227">Tuttavia, è comunque necessario firewall hello tooopen per l'accesso remoto di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="409d2-228">A questo punto, sei pronto toostart.</span><span class="sxs-lookup"><span data-stu-id="409d2-228">Now, you're ready toostart.</span></span> <span data-ttu-id="409d2-229">A partire da **ContosoQuorum**, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="409d2-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="409d2-230">Connettersi troppo**ContosoQuorum** avviando i file del desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="409d2-231">Utilizzare nome utente dell'amministratore del computer hello **AzureAdmin** e la password **Contoso! 000**, specificata durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="409d2-232">Verificare che i computer hello siano stati aggiunti correttamente troppo**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="409d2-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="409d2-233">Attendere hello toofinish di installazione di SQL Server che esegue attività di inizializzazione hello automatizzata prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="409d2-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="409d2-234">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="409d2-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="409d2-235">Installare la funzionalità Clustering di Failover di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="409d2-236">Aggiungere **CORP\Install** come amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="409d2-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="409d2-237">Disconnettersi da ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="409d2-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="409d2-238">Le operazioni relative a questo server sono state completate.</span><span class="sxs-lookup"><span data-stu-id="409d2-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="409d2-239">Inizializzare quindi **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="409d2-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="409d2-240">Attenersi alla procedura hello seguente, che è identici per entrambe le macchine virtuali di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="409d2-241">Connettere le macchine virtuali di toohello due SQL Server avviando i file del desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="409d2-242">Utilizzare nome utente dell'amministratore del computer hello **AzureAdmin** e la password **Contoso! 000**, specificata durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="409d2-243">Verificare che i computer hello siano stati aggiunti correttamente troppo**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="409d2-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="409d2-244">Attendere hello toofinish di installazione di SQL Server che esegue attività di inizializzazione hello automatizzata prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="409d2-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="409d2-245">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="409d2-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="409d2-246">Installare la funzionalità Clustering di Failover di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="409d2-247">Aggiungere **CORP\Install** come amministratore locale.</span><span class="sxs-lookup"><span data-stu-id="409d2-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="409d2-248">Importare hello PowerShell Provider per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="409d2-249">Aggiungere **CORP\Install** come ruolo sysadmin hello per istanza di SQL Server predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="409d2-250">Aggiungere **NT AUTHORITY\System** come accesso aggiuntivo con autorizzazioni di hello tre descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="409d2-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="409d2-251">Aprire il firewall hello per l'accesso remoto di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="409d2-252">Disconnettersi da entrambe le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="409d2-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="409d2-253">Infine, si è il gruppo di disponibilità hello tooconfigure pronto.</span><span class="sxs-lookup"><span data-stu-id="409d2-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="409d2-254">Si userà hello PowerShell Provider per SQL Server tooperform di hello usati per **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="409d2-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="409d2-255">Configurare il gruppo di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="409d2-255">Configure hello availability group</span></span>
1. <span data-ttu-id="409d2-256">Connettersi troppo**ContosoSQL1** nuovamente avviando i file del desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="409d2-257">Anziché effettuato l'accesso utilizzando l'account del computer hello, accedere utilizzando **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="409d2-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="409d2-258">Aprire una finestra di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="409d2-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="409d2-259">Definire hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="409d2-259">Define hello following variables:</span></span>

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
4. <span data-ttu-id="409d2-260">Importare hello PowerShell Provider per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="409d2-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="409d2-261">Modificare l'account del servizio SQL Server hello per ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="409d2-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="409d2-262">Modificare l'account del servizio SQL Server hello per ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="409d2-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="409d2-263">Scaricare **CreateAzureFailoverCluster.ps1** da [creare Cluster di Failover per gruppi di disponibilità AlwaysOn nella macchina virtuale di Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello directory di lavoro locale.</span><span class="sxs-lookup"><span data-stu-id="409d2-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="409d2-264">Si utilizzerà questo toohelp script creare un cluster di failover funzionale.</span><span class="sxs-lookup"><span data-stu-id="409d2-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="409d2-265">Per informazioni importanti sull'interazione del Clustering di Failover di Windows con hello Azure di rete, vedere [elevata disponibilità e ripristino di emergenza per SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="409d2-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="409d2-266">Modificare la directory di lavoro tooyour e creare il cluster di failover di hello con script hello scaricato.</span><span class="sxs-lookup"><span data-stu-id="409d2-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="409d2-267">Abilitare sempre gruppi di disponibilità per le istanze di SQL Server predefinite hello in **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="409d2-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="409d2-268">Creare una directory di backup e concedere le autorizzazioni per gli account del servizio SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="409d2-269">Utilizzare questo database di disponibilità hello tooprepare directory sulla replica secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="409d2-270">Creare un database in **ContosoSQL1** chiamato **MyDB1**, eseguire un backup completo e un backup del log e ripristinarli su **ContosoSQL2** con hello **WITH NORECOVERY** opzione.</span><span class="sxs-lookup"><span data-stu-id="409d2-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="409d2-271">Creare endpoint dei gruppi disponibilità hello in hello macchine virtuali di SQL Server e impostare autorizzazioni appropriate di hello sugli endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="409d2-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

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
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="409d2-272">Creare hello repliche di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="409d2-272">Create hello availability replicas.</span></span>

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
14. <span data-ttu-id="409d2-273">Infine, creare il gruppo di disponibilità hello e gruppo di disponibilità toohello join hello replica secondaria.</span><span class="sxs-lookup"><span data-stu-id="409d2-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="409d2-274">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="409d2-274">Next steps</span></span>
<span data-ttu-id="409d2-275">SQL Server Always On è stato correttamente implementato mediante la creazione di un gruppo di disponibilità in Azure.</span><span class="sxs-lookup"><span data-stu-id="409d2-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="409d2-276">tooconfigure un listener per questo gruppo di disponibilità, vedere [configurare un listener del bilanciamento del carico interno per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="409d2-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="409d2-277">Per altre informazioni sull'uso di SQL Server in Azure, vedere [Panoramica di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="409d2-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
