---
title: aaaManage Azure riservato di indirizzi IP (classico) - finestra di PowerShell | Documenti Microsoft
description: Comprendere gli indirizzi IP riservati (classico) e in che modo toomanage loro tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Indirizzi IP riservati (classica)

> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modello](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))

Gli indirizzi IP in Azure rientrano in due categorie: indirizzi dinamici e indirizzi riservati. Gli indirizzi IP pubblici gestiti da Azure sono dinamici per impostazione predefinita. Che indica che l'indirizzo IP di hello utilizzato per un determinato servizio cloud (VIP) o tooaccess una macchina virtuale o istanza del ruolo direttamente (ILPIP) è possibile modificare da tootime ora, quando le risorse arrestare o arrestate (deallocate).

tooprevent da indirizzi IP di modifica, è possibile riservare un indirizzo IP. Gli indirizzi IP riservati possono essere utilizzato solo come un indirizzo VIP, assicurandosi di tale indirizzo IP di hello per il servizio cloud hello rimane hello stesso, anche se le risorse vengono arrestate o arrestate (deallocate). Inoltre, è possibile convertire utilizzato come indirizzo IP riservato tooa VIP gli indirizzi IP dinamici esistente.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come un indirizzo pubblico IP statico usando tooreserve hello [il modello di distribuzione di gestione risorse](virtual-network-ip-addresses-overview-arm.md).

gli indirizzi toolearn più sull'indirizzo IP in Azure, leggere hello [gli indirizzi IP](virtual-network-ip-addresses-overview-classic.md) articolo.

## <a name="when-do-i-need-a-reserved-ip"></a>Quando è necessario un indirizzo IP riservato?
* **Si desidera tooensure che hello IP riservato nella sottoscrizione**. Se si desidera tooreserve un indirizzo IP che non viene rilasciato dalla sottoscrizione in nessuna circostanza, è necessario utilizzare un indirizzo IP pubblico riservato.  
* **Si desidera che il toostay IP con il servizio cloud anche attraverso arrestato o DEALLOCATE (VM) di stato**. Se si desidera toobe il servizio a cui accede utilizzando un indirizzo IP che non cambia, anche quando le macchine virtuali in hello cloud servizio vengono arrestate o arrestare (deallocato).
* **Si desidera che il traffico in uscita da Azure usi un indirizzo IP prevedibile tooensure**. È possibile il locale firewall configurato tooallow solo il traffico da indirizzi IP specifici. Riserva un indirizzo IP, si conosce l'indirizzo IP di origine hello indirizzo e non sono necessarie regole firewall a causa di modifiche IP tooan tooupdate.

## <a name="faq"></a>domande frequenti
1. È possibile usare un indirizzo IP riservato per tutti i servizi di Azure? <br>
    No. Gli indirizzi IP riservati possono essere usati solo per le macchine virtuali e per i ruoli delle istanze del servizio cloud esposti mediante un indirizzo VIP.
2. Di quanti indirizzi IP riservati è possibile disporre? <br>
    Per informazioni dettagliate, vedere hello [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.
3. È previsto un addebito per gli indirizzi IP riservati? <br>
    In alcuni casi sì. Per informazioni sui prezzi, vedere hello [dettagli prezzi di indirizzi IP riservati](http://go.microsoft.com/fwlink/?LinkID=398482) pagina.
4. Come è possibile riservare un indirizzo IP? <br>
    È possibile usare PowerShell, hello [API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o hello [portale di Azure](https://portal.azure.com) tooreserve un indirizzo IP in un'area di Azure. Un indirizzo IP riservato è sottoscrizione tooyour associato.
5. È possibile usare gli indirizzi IP riservati con reti virtuali basate su gruppi di affinità? <br>
    No. Gli indirizzi IP riservati sono supportati solo nelle reti virtuali di area. Gli indirizzi IP riservati non sono supportati per le reti virtuali associate a gruppi di affinità. Per ulteriori informazioni sull'associazione di una rete virtuale con un'area o un gruppo di affinità, vedere hello [sulle reti e i gruppi di affinità](virtual-networks-migrate-to-regional-vnet.md) articolo.

## <a name="manage-reserved-vips"></a>Gestire gli indirizzi VIP riservati

Assicurarsi di aver installato e configurato PowerShell completando i passaggi hello hello [installare e configurare PowerShell](/powershell/azure/overview) articolo. 

Prima di poter utilizzare gli indirizzi IP riservati, è necessario aggiungere tooyour sottoscrizione. un indirizzo IP dal pool hello dell'indirizzo IP pubblico riservato toocreate indirizzi disponibili in hello *centrale Usa* percorso, eseguire hello comando seguente:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Si noti tuttavia che non è possibile specificare quale indirizzo IP riservare. tooview quali indirizzi IP sono riservati nella sottoscrizione, eseguire dopo il comando di PowerShell, hello e osservare i valori hello per *ReservedIPName* e *indirizzo*:

```powershell
Get-AzureReservedIP
```

Output previsto:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Quando si crea un indirizzo IP riservato con PowerShell, è possibile specificare un indirizzo IP risorsa gruppo toocreate hello riservato in. Azure lo posiziona automaticamente in un gruppo di risorse denominato *Default-Networking*. Se si crea l'IP riservato hello utilizzando hello [portale di Azure](http://portal.azure.com), è possibile specificare qualsiasi gruppo di risorse desiderato. Se si crea IP hello riservato in un gruppo di risorse diverso da *predefinito rete* , tuttavia, ogni volta che si fa riferimento hello IP riservato con i comandi, ad esempio `Get-AzureReservedIP` e `Remove-AzureReservedIP`, è necessario fare riferimento a nome hello *Resource-group-name riservato-ip-nome del gruppo*.  Ad esempio, se si crea un indirizzo IP riservato denominato *myReservedIP* in un gruppo di risorse denominato *myResourceGroup*, è necessario fare riferimento a nome hello dell'IP riservato hello come *myResourceGroup gruppo myReservedIP*.   

Una volta che un indirizzo IP riservato, rimane associato tooyour sottoscrizione fino a quando non viene eliminato. toodelete un indirizzo IP riservato, hello esecuzione comando PowerShell seguente:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Riservare hello di indirizzo IP di un servizio cloud esistente
È possibile riservare un indirizzo IP hello di un servizio cloud esistente aggiungendo hello `-ServiceName` parametro. indirizzo IP di hello tooreserve di un servizio cloud *TestService* in hello *centrale Usa* percorso, eseguire il comando PowerShell seguente hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Associare un riservato IP tooa nuovo servizio cloud
Hello lo script seguente crea un indirizzo IP riservato nuovo, quindi associa tooa nuovo servizio cloud denominato *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Quando si crea un toouse IP riservato con un servizio cloud, si continuerà a fare riferimento toohello VM utilizzando *VIP:&lt;il numero di porta >* per le comunicazioni in ingresso. Riservare un indirizzo IP non significa che è possibile connettersi direttamente toohello macchina virtuale. Hello IP riservato viene assegnato toohello cloud servizio che hello macchina virtuale è stata distribuita. Se si desidera tooconnect tooa macchina virtuale con l'IP direttamente, è necessario tooconfigure un indirizzo IP pubblico a livello di istanza. Un indirizzo IP pubblico a livello di istanza è un tipo di indirizzo IP pubblico (chiamato un ILPIP) assegnato direttamente tooyour macchina virtuale. Non può essere riservato. Per altre informazioni, vedere hello [IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) articolo.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Rimuovere un indirizzo IP riservato da una distribuzione in esecuzione
un indirizzo IP riservato tooremove aggiunto tooa nuovo servizio cloud, eseguire il comando PowerShell seguente hello:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Rimozione di un indirizzo IP riservato da una distribuzione in esecuzione non rimuovere la prenotazione hello dalla sottoscrizione. Libera semplicemente hello IP toobe utilizzato da un'altra risorsa nella sottoscrizione.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Associare un tooa IP riservato in esecuzione la distribuzione
i comandi seguenti Hello creano un servizio cloud denominato *TestService2* con una nuova macchina virtuale denominata *TestVM2*. Hello esistente riservato IP denominato *MyReservedIP* viene quindi associato toohello servizio cloud.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Associare un servizio cloud di tooa IP riservato con un file di configurazione del servizio
È anche possibile associare un servizio cloud di tooa IP riservato usando un file di configurazione (CSCFG) del servizio. Hello xml di esempio seguente viene illustrato come tooconfigure un toouse servizio cloud un VIP riservato denominati *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Passaggi successivi
* Comprendere come [gli indirizzi IP](virtual-network-ip-addresses-overview-classic.md) funziona nel modello di distribuzione classica hello.
* Informazioni su [indirizzi IP privati riservati](virtual-networks-reserved-private-ip.md).
* Informazioni su [indirizzo IP pubblico a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md).

