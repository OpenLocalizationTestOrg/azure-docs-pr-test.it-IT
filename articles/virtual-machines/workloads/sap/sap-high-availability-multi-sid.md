---
title: una configurazione di multi-SID di SAP in Azure aaaCreate | Documenti Microsoft
description: "Configurazione di multi-SID Guida toohigh disponibilità SAP NetWeaver in macchine virtuali Windows"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>Creare una configurazione di SAP NetWeaver a più SID

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

A settembre 2016 Microsoft ha rilasciato una funzionalità con cui è possibile gestire più indirizzi IP virtuali usando un servizio di bilanciamento del carico interno di Azure. Questa funzionalità esiste già nel servizio di bilanciamento del carico esterno Azure hello.

Se si dispone di una distribuzione di SAP, è possibile utilizzare un toocreate bilanciamento di carico interno una configurazione cluster di Windows per SAP ASCS/SCS, come documentato in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows] [ sap-ha-guide].

Questo articolo illustra come toomove da una singola ASCS/SCS installazione tooan SAP più SID configurazione installando aggiuntive SAP ASCS/SCS istanze del cluster in un cluster di Windows Server Failover Clustering (WSFC) esistente. Al termine di questo processo, verrà configurato un cluster a più SID di SAP.


## <a name="prerequisites"></a>Prerequisiti
È già stato configurato un cluster WSFC in cui viene utilizzato per un'istanza di SAP ASCS/SCS, come descritto in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows] [ sap-ha-guide] e come illustrato nella figura seguente.

![Istanza di SAP ASCS/SCS a disponibilità elevata][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>Architettura di destinazione

Hello obiettivo è tooinstall più ABAP di SAP ASCS o SCS Java di SAP in cluster le istanze in hello stesso cluster WSFC, come illustrato di seguito:

![Più istanze in cluster di SAP ASCS/SCS in Azure][sap-ha-guide-figure-6002]

> [!NOTE]
>È un toohello limita il numero di indirizzi IP privati di front-end per ogni servizio di bilanciamento del carico interno di Azure.
>
>numero massimo di Hello di istanze di SAP ASCS/SCS in un cluster WSFC è uguale toohello il numero massimo di indirizzi IP privati di front-end per ogni servizio di bilanciamento del carico interno di Azure.
>

Per informazioni sui limiti del servizio di bilanciamento del carico vedere "IP front-end privato per ogni servizio di bilanciamento del carico" in [Limiti relativi alle reti - Azure Resource Manager][networking-limits-azure-resource-manager].

Panoramica di completa Hello con due sistemi SAP a disponibilità elevata è analogo al seguente:

![Configurazione a più SID di SAP a disponibilità elevata con due SID di sistema SAP][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> il programma di installazione di Hello deve soddisfare hello seguenti condizioni:
> - Hello devono condividere le istanze SAP ASCS/SCS hello stesso cluster WSFC.
> - Ogni SID DBMS deve avere un cluster WSFC dedicato.
> - I server applicazioni SAP che appartengono a sistema SAP tooone SID devono avere le proprie macchine virtuali di dedicato.


## <a name="prepare-hello-infrastructure"></a>Preparare l'infrastruttura di hello
tooprepare dell'infrastruttura, è possibile installare un'altra istanza di SAP ASCS/SCS con hello seguenti parametri:

| Nome parametro | Valore |
| --- | --- |
| SID di SAP ASCS/SCS |pr1-lb-ascs |
| Servizio di bilanciamento del carico interno di SAP DBMS | PR5 |
| Nome host virtuale SAP | pr5-sap-cl |
| Indirizzo IP dell'host virtuale di SAP ASCS/SCS (indirizzo IP aggiuntivo del servizio di bilanciamento del carico di Azure) | 10.0.0.50 |
| Numero di istanza di SAP ASCS/SCS | 50 |
| Porta di probe del servizio di bilanciamento del carico interno per l'istanza aggiuntiva di SAP ASCS/SCS | 62350 |

> [!NOTE]
> Per le istanze nel cluster di SAP ASCS/SCS, ogni indirizzo IP richiede una porta probe univoca. Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico interno di Azure usa la porta probe 62300, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 62300.
>
>Per gli scopi prefissati viene usata la porta probe 62350 perché la porta probe 62300 è già stata riservata.

È possibile installare altre istanze di SAP ASCS/SCS nel cluster WSFC esistente hello con due nodi:

| Ruolo macchina virtuale | Nome host macchina virtuale | Indirizzo IP statico |
| --- | --- | --- |
| 1° nodo del cluster per l'istanza di ASCS/SCS |pr1-ascs-0 |10.0.0.10 |
| 2° nodo del cluster per l'istanza di ASCS/SCS |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Creare un nome host virtuale per l'istanza di SAP ASCS/SCS hello cluster sul server DNS hello

È possibile creare una voce DNS per il nome host virtuale hello dell'istanza di hello ASCS/SCS tramite hello seguenti parametri:

| Nuovo nome host virtuale di SAP ASCS/SCS | Indirizzo IP associato |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

nuovo nome host di Hello e indirizzo IP vengono visualizzate nella hello gestore DNS, come illustrato nella seguente schermata hello:

![Elenco di gestore DNS evidenziazione hello definito voce DNS per hello nuovo SAP ASCS/SCS virtuale nome cluster e indirizzo TCP/IP][sap-ha-guide-figure-6004]

Hello per la creazione di una voce DNS anche descritta in dettaglio in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-9.1.1].

> [!NOTE]
> Hello nuovo indirizzo IP che si assegna il nome host virtuale toohello di hello aggiuntive ASCS/SCS dell'istanza deve essere hello come hello nuovo indirizzo IP di bilanciamento del carico di Azure SAP toohello assegnato.
>
>In questo scenario, l'indirizzo IP hello è 10.0.0.50.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>Aggiungere un IP indirizzo tooan esistente Azure bilanciamento del carico interno tramite PowerShell

toocreate più di un'istanza di SAP ASCS/SCS in hello WSFC stesso cluster, utilizzare PowerShell tooadd un tooan di indirizzo IP del bilanciamento del carico interno di Azure esistente. Ogni indirizzo IP richiede regole di bilanciamento del carico, una porta probe, un pool di indirizzi IP front-end e un pool back-end propri.

Hello script seguente aggiunge un nuovo IP indirizzo tooan bilanciamento del carico esistente. Aggiornare le variabili di PowerShell hello per l'ambiente. script Hello creerà necessarie tutte le regole di bilanciamento del carico per tutte le porte di SAP ASCS/SCS.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
Dopo l'esecuzione di script hello, hello risultati vengono visualizzati in hello portale di Azure, come illustrato nella seguente schermata hello:

![Nuovo pool IP front-end di hello portale di Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>Aggiungere dischi toocluster macchine e configurare hello SIOS cluster quota disco

È necessario aggiungere un nuovo disco cluster condiviso per ogni istanza di SAP ASCS/SCS aggiuntiva. Per Windows Server 2012 R2, disco condivisione del cluster WSFC hello attualmente in uso è una soluzione software SIOS DataKeeper di hello.

Hello seguenti:
1. Aggiungere un altro disco o i dischi di hello stessa dimensione (che è necessario toostripe) tooeach di hello nodi del cluster e formattare il testo.
2. Configurare la replica di archiviazione con SIOS DataKeeper.

Questa procedura si presuppone che SIOS DataKeeper già stato installato nel computer del cluster WSFC hello. Se è stato installato, è ora necessario configurare la replica tra computer hello. il processo di Hello è descritto dettagliatamente in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-8.12.3.3].  

![Il mirroring per il nuovo disco di condivisione di SAP ASCS/SCS di hello sincrono DataKeeper][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>Distribuire le VM per i server applicazioni SAP e il cluster DBMS

Preparazione dell'infrastruttura di hello toocomplete per secondo sistema SAP di hello, hello seguenti:

1. Distribuire VM dedicate per i server applicazioni SAP e inserirle nel proprio gruppo di disponibilità dedicato.
2. Distribuire VM dedicate per il cluster DBMS e inserirle nel proprio gruppo di disponibilità dedicato.


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Installare il sistema SAP NetWeaver SID2 secondo di hello

processo completo di Hello di installazione di un sistema SAP SID2 secondo è descritto in hello principale [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-9].

procedura Hello è come segue:

1. [Installare hello SAP primo nodo del cluster][sap-ha-guide-9.1.2].  
 In questo passaggio si installa SAP con un'istanza ASCS/SCS a disponibilità elevata in hello **nodo del cluster WSFC esistente 1**.

2. [Modificare il profilo di SAP hello dell'istanza ASCS/SCS hello][sap-ha-guide-9.1.3].

3. [Configurare una porta probe][sap-ha-guide-9.1.4].  
 In questo passaggio si sta configurando una porta probe SAP-SID2-IP della risorsa nel cluster SAP tramite PowerShell. Eseguire questa configurazione su uno dei nodi del cluster di SAP ASCS/SCS hello.

4. [Installare l'istanza del database hello] [sap a disponibilità elevata-Guida-9.2].  
 In questo passaggio si sta installando DBMS in un cluster WSFC dedicato.

5. [Installare secondo nodo del cluster hello] [sap a disponibilità elevata-Guida-9.3].  
 In questo passaggio, si sta installando SAP con un'istanza ASCS/SCS a disponibilità elevata nel nodo del cluster esistente WSFC hello 2.

6. Aprire le porte del Firewall di Windows per l'istanza di SAP ASCS/SCS hello e ProbePort.  
 In entrambi i nodi del cluster usati per le istanze di SAP ASCS/SCS si stanno aprendo tutte le porte di Windows Firewall usate da SAP ASCS/SCS. Queste porte sono elencate in hello [Guida per la disponibilità elevata di SAP NetWeaver in macchine virtuali Windows][sap-ha-guide-8.8].  
 Inoltre aprire hello Azure carico interno del servizio di bilanciamento porta probe, ovvero 62350 in questo scenario.

7. [Modificare il tipo di avvio dell'istanza di servizio SAP Hiamanti Windows hello hello][sap-ha-guide-9.4].

8. [Installare server primario applicazioni SAP hello] [ sap-ha-guide-9.5] sul nuovo hello dedicato macchina virtuale.

9. [Installare server aggiuntivi di applicazioni SAP hello] [ sap-ha-guide-9.6] sul nuovo hello dedicato macchina virtuale.

10. [Test di failover di istanza di SAP ASCS/SCS hello e la replica di SIOS][sap-ha-guide-10].

## <a name="next-steps"></a>Passaggi successivi

- [Limiti relativi alle reti: Azure Resource Manager][networking-limits-azure-resource-manager]
- [Più indirizzi VIP per Azure Load Balancer][load-balancer-multivip-overview]
- [SAP NetWeaver in macchine virtuali Windows: guida alle funzionalità di disponibilità elevata][sap-ha-guide]
