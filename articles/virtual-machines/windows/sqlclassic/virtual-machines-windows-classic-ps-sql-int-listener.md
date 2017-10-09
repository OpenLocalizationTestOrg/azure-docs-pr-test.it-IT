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
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Configurare un listener ILB per gruppi di disponibilità AlwaysOn in Azure
> [!div class="op_single_selector"]
> * [Listener interno](../classic/ps-sql-int-listener.md)
> * [Listener esterno](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Panoramica

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo descrive l'utilizzo di hello del modello di distribuzione classica hello. È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.

vedere un listener per un gruppo di disponibilità Always On nel modello di gestione risorse di hello, tooconfigure [configurare un bilanciamento del carico per un gruppo di disponibilità AlwaysOn in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

Il gruppo di disponibilità può contenere repliche solo locali, solo di Azure oppure sia locali che di Azure per le configurazioni ibride. Le repliche di Azure possono risiedere all'interno di hello stessa area o in più aree geografiche che utilizzano più reti virtuali. Hello in questo articolo si presuppone che sia già [configurato un gruppo di disponibilità](../classic/portal-sql-alwayson-availability-groups.md) , ma non è ancora stato configurato un listener.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Linee guida e limitazioni per listener interni
uso di Hello di un bilanciamento del carico interno (ILB) con un listener del gruppo di disponibilità in Azure è soggetto toohello alle linee guida:

* listener del gruppo di disponibilità Hello è supportato in Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Un solo listener del gruppo di disponibilità interno è supportata per ogni servizio cloud, perché i listener di hello configurato toohello bilanciamento del carico interno ed è presente un solo bilanciamento del carico interno per ogni servizio cloud. Tuttavia, è possibile toocreate più listener esterno. Per altre informazioni, vedere [Configurare un listener esterno per i gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinare l'accessibilità di hello del listener hello
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Questo articolo illustra la creazione di un listener che usa un servizio di bilanciamento del carico interno. Se è necessario un listener pubblico o esterno, vedere versione di hello di questo articolo viene illustrata l'impostazione di un [listener esterno](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Creare endpoint VM con bilanciamento del carico con Direct Server Return
Creare innanzitutto un bilanciamento del carico interno eseguendo script hello più avanti in questa sezione.

Creare un endpoint con carico bilanciato per ogni VM che ospita una replica di Azure. Se si dispongono di repliche in più aree, ogni replica per tale area deve essere in hello stesso cloud servizio hello stessa rete virtuale di Azure. La creazione di repliche del gruppo di disponibilità che si estendono su più aree di Azure richiede la configurazione di più reti virtuali. Per ulteriori informazioni sulla configurazione tra la connettività di rete virtuale, vedere [configurare la connettività di rete di rete virtuale toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Nel portale di Azure hello, andare tooeach macchina virtuale che ospita un dettagli hello tooview di replica.

2. Fare clic su hello **endpoint** scheda per ogni macchina virtuale.

3. Verificare che hello **nome** e **porta pubblica** dell'endpoint di listener hello che si desidera toouse non sono già in uso. Nell'esempio hello in questa sezione, è il nome di hello *MyEndpoint*, e la porta hello è *1433*.

4. Nel client locale, scaricare e installare più recente di hello [modulo PowerShell](https://azure.microsoft.com/downloads/).

5. Avviare Azure PowerShell.  
    Apre una nuova sessione PowerShell, con hello Azure amministrativi moduli caricati.

6. Eseguire `Get-AzurePublishSettingsFile`. Questo cmdlet conduce toodownload browser tooa pubblica Impostazioni tooa locale directory del file. Potrebbero essere richieste le credenziali di accesso per la sottoscrizione di Azure.

7. Eseguire il seguente hello `Import-AzurePublishSettingsFile` comando con il percorso di hello di hello pubblicare file di impostazioni che è stato scaricato:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Dopo la pubblicazione hello viene importato il file di impostazioni, è possibile gestire la sottoscrizione di Azure nella sessione di PowerShell hello.

8. Per *ILB* assegnare un indirizzo IP statico. Esaminare una configurazione di rete virtuale corrente hello eseguendo hello comando seguente:

        (Get-AzureVNetConfig).XMLConfiguration
9. Hello nota *Subnet* nome per la subnet hello che include macchine virtuali di hello che ospitano repliche hello. Questo nome viene utilizzato nel parametro hello $SubnetName nello script hello.

10. Hello nota *VirtualNetworkSite* nome e hello avvio *AddressPrefix* per subnet hello che include macchine virtuali di hello che ospitano repliche hello. Cercare un indirizzo IP disponibile, passando entrambi toohello valori `Test-AzureStaticVNetIP` comando ed esaminando hello *AvailableAddresses*. Ad esempio, se hello rete virtuale è denominata *MyVNet* e dispone di un intervallo di indirizzi di subnet che inizia in corrispondenza *172.16.0.128*, comando che segue hello vengono elencati gli indirizzi disponibili:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Selezionare uno degli indirizzi disponibili hello e usarlo nel parametro hello $ILBStaticIP dello script hello nel passaggio successivo hello.

12. Copiare hello editor di testo tooa script PowerShell seguente e impostare toosuit di hello i valori delle variabili dell'ambiente. Per alcuni parametri sono stati forniti valori predefiniti.  

    Le distribuzioni esistenti che usano i gruppi di affinità non potranno aggiungere un servizio di bilanciamento del carico interno. Per altre informazioni sui requisiti per il servizio di bilanciamento del carico interno, vedere la [panoramica del bilanciamento del carico interno](../../../load-balancer/load-balancer-internal-overview.md).

    Inoltre, se il gruppo di disponibilità si estende su aree di Azure, è necessario eseguire hello script una volta in ogni Data Center per servizio cloud hello e i nodi che si trovano in Data Center in questione.

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

13. Dopo aver impostato le variabili di hello, hello copia crearne uno script da hello testo editor tooyour PowerShell sessione toorun. Se il messaggio hello viene comunque mostrata  **>>** , premere INVIO nuovamente script hello che toomake viene avviata l'esecuzione.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Se necessario, verificare che KB2854082 sia installato.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Aprire le porte del firewall hello nei nodi di gruppo di disponibilità
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Creare listener del gruppo di disponibilità hello

Creare listener del gruppo di disponibilità hello in due passaggi. Innanzitutto, creare la risorsa di cluster punto di accesso client hello e configurare le dipendenze. In secondo luogo, è possibile configurare le risorse cluster hello in PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Creare il punto di accesso client hello e configurare le dipendenze di cluster hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurare le risorse di cluster hello in PowerShell
1. Per bilanciamento del carico interno, è necessario utilizzare l'indirizzo IP hello di hello bilanciamento del carico interno è stato creato in precedenza. tooobtain questo IP indirizzo in PowerShell, hello utilizzare lo script seguente:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. In uno dei hello macchine virtuali, copiare uno script di PowerShell hello per l'editor di testo tooa del sistema operativo e quindi impostare le variabili di hello toohello valori annotati in precedenza.

    Per Windows Server 2012 o versioni successive, utilizzare hello lo script seguente:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Per Windows Server 2008 R2, utilizzare hello lo script seguente:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Dopo aver impostato le variabili di hello, aprire una finestra di Windows PowerShell con privilegi elevata, Incolla hello crearne uno script dall'editor di testo hello nel toorun di sessione di PowerShell. Se il messaggio hello viene comunque mostrata  **>>** , premere INVIO nuovamente toomake certi che venga avviato script hello in esecuzione.

4. Ripetere i passaggi precedenti per ogni macchina virtuale hello.  
    Questo script consente di configurare la risorsa indirizzo IP hello con indirizzo IP di hello del servizio cloud hello e imposta altri parametri, ad esempio la porta probe hello. Quando la risorsa indirizzo IP hello viene portata online, può rispondere toohello polling sulla porta probe hello dall'endpoint con bilanciamento del carico hello creato in precedenza.

## <a name="bring-hello-listener-online"></a>Portare online listener hello
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Operazioni di completamento della procedura
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Listener del gruppo di disponibilità hello test (hello nella stessa rete virtuale)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
