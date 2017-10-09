---
title: Azure interna aaaCreate bilanciamento del carico - PowerShell classico | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell nel modello di distribuzione classica hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) tramite PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Servizi cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Creare un set con servizio di bilanciamento del carico interno per le macchine virtuali

toocreate un bilanciamento del carico interno impostato e hello server che invierà i tooit di traffico, è necessario seguente hello toodo:

1. Creare un'istanza interna il bilanciamento del carico che fungerà da endpoint hello in arrivo traffico toobe con bilanciato del carico tra i server hello di un set con carico bilanciato.
2. Aggiungere gli endpoint corrispondenti toohello le macchine virtuali che riceveranno il traffico in ingresso hello.
3. Configurare i server hello che invieranno hello traffico toobe con bilanciamento del carico toosend loro traffico toohello indirizzo IP virtuale (VIP) dell'istanza di hello interno il bilanciamento del carico.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Passaggio 1: Creare un'istanza del bilanciamento del carico interno

Per un servizio cloud esistente o un servizio cloud distribuito in una rete virtuale regionale, è possibile creare un'istanza di bilanciamento del carico interno con hello seguenti comandi di Windows PowerShell:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Si noti che questo utilizzo di hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) cmdlet di Windows PowerShell Usa hello di parametri defaultprobe. Per altre informazioni sui set di parametri aggiuntivi, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Passaggio 2: Aggiungere l'istanza di bilanciamento del carico interno toohello endpoint

Di seguito è fornito un esempio:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Passaggio 3: Configurare il server toosend i relativi endpoint di bilanciamento del carico interno nuovo traffico toohello

Configurare hello server il cui traffico corso toobe con carico bilanciato toouse hello nuovo indirizzo IP (Buongiorno VIP) del hello istanza interno il bilanciamento del carico eccessivo. Questo è hello indirizzo sul quale hello bilanciamento del carico interno è in ascolto l'istanza. Nella maggior parte dei casi, è necessario toojust aggiungere o modificare un record DNS per hello VIP dell'istanza di bilanciamento del carico interno hello.

Se si specifica l'indirizzo IP hello durante la creazione dell'istanza di bilanciamento del carico interno hello hello, si dispone già di hello VIP. In caso contrario, è possibile visualizzare il VIP hello da hello seguenti comandi:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse questi comandi, immettere i valori hello e Rimuovi hello < e >. Di seguito è fornito un esempio:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Dalla visualizzazione hello di hello comando Get-AzureInternalLoadBalancer, prendere nota indirizzo IP hello e rendere server tooyour di hello le modifiche necessarie o tooensure i record DNS che il traffico venga inviato toohello VIP.

> [!NOTE]
> piattaforma Microsoft Azure Hello utilizza un indirizzo IPv4 statico, instradabile pubblicamente per un'ampia gamma di scenari di amministrazione. indirizzo IP Hello è 168.63.129.16. Questo indirizzo IP non deve essere bloccato da alcun firewall, perché potrebbe causare un comportamento imprevisto.
> Con tooAzure riguardo interno il bilanciamento del carico, viene utilizzato questo indirizzo IP dal monitoraggio probe di stato di integrità hello toodetermine bilanciamento del carico hello per le macchine virtuali in un set con carico bilanciato. Se un gruppo di sicurezza di rete è utilizzata toorestrict traffico tooAzure le macchine virtuali in un set di internamente con bilanciamento del carico o applicato tooa Subnet rete virtuale, assicurarsi che una regola di sicurezza di rete viene aggiunto il traffico tooallow 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Esempio di bilanciamento del carico interno

toostep illustra il processo di fine tooend hello di creazione di un set con carico bilanciato per due configurazioni di esempio, vedere hello seguenti sezioni.

### <a name="an-internet-facing-multi-tier-application"></a>Applicazione multilivello con connessione Internet

Si desidera tooprovide un servizio di database con carico bilanciato per un set di server web con connessione Internet. Entrambi i set di server sono ospitati in un unico servizio cloud di Azure. La porta Web server traffico tooTCP 1433 deve essere distribuita tra due macchine virtuali nel livello di database hello. Figura 1 mostra la configurazione hello.

![Set con carico bilanciato interno per il livello di database hello](./media/load-balancer-internal-getstarted/IC736321.png)

configurazione di Hello è costituita dai seguenti hello:

* Hello servizio cloud che ospita macchine virtuali hello è denominato mytestcloud.
* il server di database di Hello due esistenti sono denominati DB1, DB2.
* I server Web nel livello web hello connettono i server di database toohello nel livello di database hello utilizzando l'indirizzo IP privato hello. Un'altra opzione è toouse DNS per la rete virtuale hello e registrare manualmente un record A per il set di bilanciamento del carico interno con carico hello.

i comandi seguenti Hello configurano una nuova istanza di bilanciamento del carico interno denominata **ILBset** e aggiungere le macchine virtuali endpoint toohello corrispondente toohello due server di database:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Rimuovere una configurazione del bilanciamento del carico interno

tooremove una macchina virtuale come un endpoint da un'istanza di servizio di bilanciamento del carico interno, hello di utilizzare i comandi seguenti:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse questi comandi, inserire i valori hello, rimozione hello < e >.

Di seguito è fornito un esempio:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove un'istanza di servizio di bilanciamento del carico interno da un servizio cloud, hello di utilizzare i comandi seguenti:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse questi comandi, inserire il valore di hello e rimuovere hello < e >.

Di seguito è fornito un esempio:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Altre informazioni sui cmdlet per servizio di bilanciamento del carico interno

tooobtain ulteriori informazioni sui cmdlet di bilanciamento del carico interno, eseguire hello comandi al prompt di Windows PowerShell seguente:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

