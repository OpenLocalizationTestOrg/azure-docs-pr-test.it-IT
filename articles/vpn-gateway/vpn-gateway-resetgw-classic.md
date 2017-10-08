---
title: Reimpostare un tooreestablish gateway VPN di Azure tunnel IPsec | Documenti Microsoft
description: In questo articolo illustra la reimpostazione del tunnel IPsec di tooreestablish Gateway VPN di Azure. articolo Hello applica gateway tooVPN hello classic e modelli di distribuzione di gestione risorse di hello.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Reimpostare un gateway VPN

La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito. In questo caso, i dispositivi VPN locali sono tutte le funzioni correttamente, ma sono tooestablish non è possibile tunnel IPsec con gateway VPN di Azure hello. Questo articolo consente di reimpostare il gateway VPN.

### <a name="what-happens-during-a-reset"></a>Cosa accade durante un ripristino

Un gateway VPN di Azure è costituito da due istanze di macchina virtuale in esecuzione in una configurazione di standby attivo. Quando si reimposta il gateway di hello, riavvio gateway hello e quindi riapplica hello cross-premise tooit configurazioni. gateway Hello mantiene l'indirizzo IP pubblico hello che è già stato assegnato. Ciò significa che non è necessario configurazione del router VPN hello tooupdate con un nuovo indirizzo IP pubblico per il gateway VPN di Azure.

Quando si esegue gateway di hello tooreset comando hello, hello attivo corrente del gateway VPN di Azure hello è stato riavviato immediatamente. Vi sarà un gap breve durante il failover hello dal hello active istanza (in corso il riavvio), toohello standby. gap Hello deve essere inferiore al minuto.

Se la connessione hello non viene ripristinata dopo il riavvio del primo hello, problema hello stesso comando nuovamente tooreboot hello seconda VM istanza (hello nuovo gateway active). Se due riavvii hello richiesto tooback indietro, esisterà un periodo leggermente più lungo in entrambe le istanze di macchina virtuale (attive e standby) sono in corso il riavvio. In questo modo un gap più connettività VPN hello, backup too2 too4 minuti per il riavvio di hello toocomplete macchine virtuali.

Dopo due riavvii, se si verificano ancora problemi di connettività tra più sedi locali, aprire una richiesta di supporto da hello portale di Azure.

## <a name="before"></a>Prima di iniziare

Prima di ripristinare il gateway, verificare gli elementi chiave hello elencati di seguito per ogni tunnel VPN IPsec da sito a sito (S2S). Mancata corrispondenza negli elementi hello comporterà la disconnessione di hello di tunnel VPN S2S. Verifica e la correzione delle configurazioni di hello per le sedi locali e i gateway VPN di Azure consente di riavvii non necessari e interruzioni per hello altre connessioni di lavoro nei gateway hello.

Verificare i seguenti elementi prima di reimpostare il gateway hello:

* Hello Internet IP (VIP) per entrambi gateway VPN di Azure hello e che hello locale gateway VPN siano configurate correttamente in entrambi hello Azure e hello locale VPN i criteri.
* chiave precondivisa Hello devono essere hello stesso nei gateway VPN di Azure sia in locale.
* Se si applica configurazione IPsec/IKE specifico, ad esempio la crittografia, algoritmi di hash e PFS (Perfect Forward Secrecy), assicurarsi che entrambi hello Azure e i gateway VPN locale disponga hello stesse configurazioni.

## <a name="portal"></a>Portale di Azure

È possibile reimpostare un gateway di gestione risorse VPN tramite hello portale di Azure. Se si desidera tooreset un gateway classico, vedere hello [PowerShell](#resetclassic) passaggi.

### <a name="resource-manager-deployment-model"></a>Modello di distribuzione di Gestione risorse

1. Aprire hello [portale di Azure](https://portal.azure.com) e passare toohello gateway di rete virtuale di gestione risorse che si desidera tooreset.
2. Nel Pannello di hello per gateway di rete virtuale hello, fare clic su 'Reset'.

  ![Pannello di reimpostazione gateway VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. In hello reimpostare pannello, fare clic su hello **reimpostare** pulsante.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Modello di distribuzione di Gestione risorse

Hello cmdlet per la reimpostazione di un gateway è **reimpostazione AzureRmVirtualNetworkGateway**. Prima di eseguire una reimpostazione, assicurarsi di disporre hello l'ultima versione di hello [cmdlet PowerShell di gestione risorse](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Hello seguente esempio mostra come reimpostare un gateway di rete virtuale denominato VNet1GW nel gruppo di risorse TestRG1 hello:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Risultato:

Quando si riceve un valore restituito, si può presupporre hello gateway reimpostazione è stata eseguita correttamente. Tuttavia, non è nothing nel risultato restituito hello che indica in modo esplicito tale reimpostazione hello ha avuto esito positivo. Se si desidera toolook strettamente in hello cronologia toosee esattamente quando gateway hello reimpostazione si è verificato, è possibile visualizzare tali informazioni in hello [portale di Azure](https://portal.azure.com). Nel portale di hello passare troppo**'GatewayName' -> integrità delle risorse**.

### <a name="resetclassic"></a>Modello di distribuzione classica

Hello cmdlet per la reimpostazione di un gateway è **Reset-AzureVNetGateway**. Prima di eseguire una reimpostazione, assicurarsi di disporre hello l'ultima versione di hello [i cmdlet PowerShell di gestione del servizio (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Hello esempio seguente viene reimpostato gateway hello per una rete virtuale denominata "ContosoVNet":

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Risultato:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>

gateway hello tooreset, utilizzare hello [az-gateway di rete virtuale rete reimpostare](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando. Hello seguente esempio mostra come reimpostare un gateway di rete virtuale denominato VNet5GW nel gruppo di risorse TestRG5 hello:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Risultato:

Quando si riceve un valore restituito, si può presupporre hello gateway reimpostazione è stata eseguita correttamente. Tuttavia, non è nothing nel risultato restituito hello che indica in modo esplicito tale reimpostazione hello ha avuto esito positivo. Se si desidera toolook strettamente in hello cronologia toosee esattamente quando gateway hello reimpostazione si è verificato, è possibile visualizzare tali informazioni in hello [portale di Azure](https://portal.azure.com). Nel portale di hello passare troppo**'GatewayName' -> integrità delle risorse**.
