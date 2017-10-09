---
title: "un listener del bilanciamento del carico interno per i gruppi di disponibilità in Azure aaaConfigure | Documenti Microsoft"
description: "Questa esercitazione Usa le risorse create con il modello di distribuzione classica hello e viene creato un listener gruppo disponibilità AlwaysOn in Azure che utilizza un servizio di bilanciamento del carico interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="62c79-103">Configurare un listener ILB per gruppi di disponibilità AlwaysOn in Azure</span><span class="sxs-lookup"><span data-stu-id="62c79-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62c79-104">Listener interno</span><span class="sxs-lookup"><span data-stu-id="62c79-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="62c79-105">Listener esterno</span><span class="sxs-lookup"><span data-stu-id="62c79-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="62c79-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="62c79-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62c79-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="62c79-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="62c79-108">Questo articolo descrive l'utilizzo di hello del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="62c79-109">È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="62c79-110">vedere un listener per un gruppo di disponibilità Always On nel modello di gestione risorse di hello, tooconfigure [configurare un bilanciamento del carico per un gruppo di disponibilità AlwaysOn in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="62c79-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="62c79-111">Il gruppo di disponibilità può contenere repliche solo locali, solo di Azure oppure sia locali che di Azure per le configurazioni ibride.</span><span class="sxs-lookup"><span data-stu-id="62c79-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="62c79-112">Le repliche di Azure possono risiedere all'interno di hello stessa area o in più aree geografiche che utilizzano più reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="62c79-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="62c79-113">Hello in questo articolo si presuppone che sia già [configurato un gruppo di disponibilità](../classic/portal-sql-alwayson-availability-groups.md) , ma non è ancora stato configurato un listener.</span><span class="sxs-lookup"><span data-stu-id="62c79-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="62c79-114">Linee guida e limitazioni per listener interni</span><span class="sxs-lookup"><span data-stu-id="62c79-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="62c79-115">uso di Hello di un bilanciamento del carico interno (ILB) con un listener del gruppo di disponibilità in Azure è soggetto toohello alle linee guida:</span><span class="sxs-lookup"><span data-stu-id="62c79-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="62c79-116">listener del gruppo di disponibilità Hello è supportato in Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="62c79-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="62c79-117">Un solo listener del gruppo di disponibilità interno è supportata per ogni servizio cloud, perché i listener di hello configurato toohello bilanciamento del carico interno ed è presente un solo bilanciamento del carico interno per ogni servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="62c79-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="62c79-118">Tuttavia, è possibile toocreate più listener esterno.</span><span class="sxs-lookup"><span data-stu-id="62c79-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="62c79-119">Per altre informazioni, vedere [Configurare un listener esterno per i gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="62c79-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="62c79-120">Determinare l'accessibilità di hello del listener hello</span><span class="sxs-lookup"><span data-stu-id="62c79-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="62c79-121">Questo articolo illustra la creazione di un listener che usa un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="62c79-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="62c79-122">Se è necessario un listener pubblico o esterno, vedere versione di hello di questo articolo viene illustrata l'impostazione di un [listener esterno](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62c79-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="62c79-123">Creare endpoint VM con bilanciamento del carico con Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="62c79-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="62c79-124">Creare innanzitutto un bilanciamento del carico interno eseguendo script hello più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="62c79-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="62c79-125">Creare un endpoint con carico bilanciato per ogni VM che ospita una replica di Azure.</span><span class="sxs-lookup"><span data-stu-id="62c79-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="62c79-126">Se si dispongono di repliche in più aree, ogni replica per tale area deve essere in hello stesso cloud servizio hello stessa rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="62c79-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="62c79-127">La creazione di repliche del gruppo di disponibilità che si estendono su più aree di Azure richiede la configurazione di più reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="62c79-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="62c79-128">Per ulteriori informazioni sulla configurazione tra la connettività di rete virtuale, vedere [configurare la connettività di rete di rete virtuale toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="62c79-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="62c79-129">Nel portale di Azure hello, andare tooeach macchina virtuale che ospita un dettagli hello tooview di replica.</span><span class="sxs-lookup"><span data-stu-id="62c79-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="62c79-130">Fare clic su hello **endpoint** scheda per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62c79-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="62c79-131">Verificare che hello **nome** e **porta pubblica** dell'endpoint di listener hello che si desidera toouse non sono già in uso.</span><span class="sxs-lookup"><span data-stu-id="62c79-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="62c79-132">Nell'esempio hello in questa sezione, è il nome di hello *MyEndpoint*, e la porta hello è *1433*.</span><span class="sxs-lookup"><span data-stu-id="62c79-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="62c79-133">Nel client locale, scaricare e installare più recente di hello [modulo PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="62c79-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="62c79-134">Avviare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c79-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="62c79-135">Apre una nuova sessione PowerShell, con hello Azure amministrativi moduli caricati.</span><span class="sxs-lookup"><span data-stu-id="62c79-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="62c79-136">Eseguire `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="62c79-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="62c79-137">Questo cmdlet conduce toodownload browser tooa pubblica Impostazioni tooa locale directory del file.</span><span class="sxs-lookup"><span data-stu-id="62c79-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="62c79-138">Potrebbero essere richieste le credenziali di accesso per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="62c79-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="62c79-139">Eseguire il seguente hello `Import-AzurePublishSettingsFile` comando con il percorso di hello di hello pubblicare file di impostazioni che è stato scaricato:</span><span class="sxs-lookup"><span data-stu-id="62c79-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="62c79-140">Dopo la pubblicazione hello viene importato il file di impostazioni, è possibile gestire la sottoscrizione di Azure nella sessione di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="62c79-141">Per *ILB* assegnare un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="62c79-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="62c79-142">Esaminare una configurazione di rete virtuale corrente hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="62c79-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="62c79-143">Hello nota *Subnet* nome per la subnet hello che include macchine virtuali di hello che ospitano repliche hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="62c79-144">Questo nome viene utilizzato nel parametro hello $SubnetName nello script hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="62c79-145">Hello nota *VirtualNetworkSite* nome e hello avvio *AddressPrefix* per subnet hello che include macchine virtuali di hello che ospitano repliche hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="62c79-146">Cercare un indirizzo IP disponibile, passando entrambi toohello valori `Test-AzureStaticVNetIP` comando ed esaminando hello *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="62c79-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="62c79-147">Ad esempio, se hello rete virtuale è denominata *MyVNet* e dispone di un intervallo di indirizzi di subnet che inizia in corrispondenza *172.16.0.128*, comando che segue hello vengono elencati gli indirizzi disponibili:</span><span class="sxs-lookup"><span data-stu-id="62c79-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="62c79-148">Selezionare uno degli indirizzi disponibili hello e usarlo nel parametro hello $ILBStaticIP dello script hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="62c79-149">Copiare hello editor di testo tooa script PowerShell seguente e impostare toosuit di hello i valori delle variabili dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="62c79-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="62c79-150">Per alcuni parametri sono stati forniti valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="62c79-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="62c79-151">Le distribuzioni esistenti che usano i gruppi di affinità non potranno aggiungere un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="62c79-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="62c79-152">Per altre informazioni sui requisiti per il servizio di bilanciamento del carico interno, vedere la [panoramica del bilanciamento del carico interno](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62c79-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="62c79-153">Inoltre, se il gruppo di disponibilità si estende su aree di Azure, è necessario eseguire hello script una volta in ogni Data Center per servizio cloud hello e i nodi che si trovano in Data Center in questione.</span><span class="sxs-lookup"><span data-stu-id="62c79-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="62c79-154">Dopo aver impostato le variabili di hello, hello copia crearne uno script da hello testo editor tooyour PowerShell sessione toorun.</span><span class="sxs-lookup"><span data-stu-id="62c79-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="62c79-155">Se il messaggio hello viene comunque mostrata  **>>** , premere INVIO nuovamente script hello che toomake viene avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="62c79-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="62c79-156">Se necessario, verificare che KB2854082 sia installato.</span><span class="sxs-lookup"><span data-stu-id="62c79-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="62c79-157">Aprire le porte del firewall hello nei nodi di gruppo di disponibilità</span><span class="sxs-lookup"><span data-stu-id="62c79-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="62c79-158">Creare listener del gruppo di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="62c79-158">Create hello availability group listener</span></span>

<span data-ttu-id="62c79-159">Creare listener del gruppo di disponibilità hello in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="62c79-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="62c79-160">Innanzitutto, creare la risorsa di cluster punto di accesso client hello e configurare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="62c79-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="62c79-161">In secondo luogo, è possibile configurare le risorse cluster hello in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c79-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="62c79-162">Creare il punto di accesso client hello e configurare le dipendenze di cluster hello</span><span class="sxs-lookup"><span data-stu-id="62c79-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="62c79-163">Configurare le risorse di cluster hello in PowerShell</span><span class="sxs-lookup"><span data-stu-id="62c79-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="62c79-164">Per bilanciamento del carico interno, è necessario utilizzare l'indirizzo IP hello di hello bilanciamento del carico interno è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c79-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="62c79-165">tooobtain questo IP indirizzo in PowerShell, hello utilizzare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="62c79-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="62c79-166">In uno dei hello macchine virtuali, copiare uno script di PowerShell hello per l'editor di testo tooa del sistema operativo e quindi impostare le variabili di hello toohello valori annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c79-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="62c79-167">Per Windows Server 2012 o versioni successive, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="62c79-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="62c79-168">Per Windows Server 2008 R2, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="62c79-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="62c79-169">Dopo aver impostato le variabili di hello, aprire una finestra di Windows PowerShell con privilegi elevata, Incolla hello crearne uno script dall'editor di testo hello nel toorun di sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62c79-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="62c79-170">Se il messaggio hello viene comunque mostrata  **>>** , premere INVIO nuovamente toomake certi che venga avviato script hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="62c79-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="62c79-171">Ripetere i passaggi precedenti per ogni macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="62c79-172">Questo script consente di configurare la risorsa indirizzo IP hello con indirizzo IP di hello del servizio cloud hello e imposta altri parametri, ad esempio la porta probe hello.</span><span class="sxs-lookup"><span data-stu-id="62c79-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="62c79-173">Quando la risorsa indirizzo IP hello viene portata online, può rispondere toohello polling sulla porta probe hello dall'endpoint con bilanciamento del carico hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62c79-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="62c79-174">Portare online listener hello</span><span class="sxs-lookup"><span data-stu-id="62c79-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="62c79-175">Operazioni di completamento della procedura</span><span class="sxs-lookup"><span data-stu-id="62c79-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="62c79-176">Listener del gruppo di disponibilità hello test (hello nella stessa rete virtuale)</span><span class="sxs-lookup"><span data-stu-id="62c79-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="62c79-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62c79-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
