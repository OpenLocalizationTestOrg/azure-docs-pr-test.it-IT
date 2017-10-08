---
title: 'Connettersi a una rete virtuale di tooanother di rete virtuale di Azure: portale | Documenti Microsoft'
description: Creare una connessione gateway VPN tra reti virtuali usando Gestione risorse e hello portale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Configurare una connessione del gateway VPN per rete virtuale a utilizzando hello portale di Azure

In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali. Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni. Quando le reti virtuali connessione da sottoscrizioni diverse, le sottoscrizioni di hello non necessaria toobe associato hello stesso tenant di Active Directory. 

passaggi di Hello in questo articolo si applicano toohello modello di distribuzione di gestione delle risorse e utilizzano hello portale di Azure. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connettersi tra modelli di distribuzione diversi - Portale di Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connettersi tra modelli di distribuzione diversi - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. Se le reti virtuali si trovano in hello stessa area, è opportuno tooconsider collegarli tramite Peering reti virtuali. Peering reti virtuali non usa un gateway VPN. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).

La comunicazione tra reti virtuali può essere associata a configurazioni multisito. Consente di stabilire le topologie di rete che combinano connettività cross-premise con connettività di rete virtuale tra, come illustrato nel seguente diagramma hello:

![Informazioni sulle connessioni](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "Informazioni sulle connessioni")

### <a name="why-connect-virtual-networks"></a>Perché connettere reti virtuali?

Si consiglia le reti virtuali tooconnect per hello seguenti motivi:

* **Presenza e ridondanza in più aree geografiche**
  
  * È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.
  * Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure. Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.
* **Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**
  
  * Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse a causa di tooisolation o i requisiti amministrativi.

Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo. Si noti che se le reti virtuali in diverse sottoscrizioni, è possibile creare nel portale di hello connessione hello. È possibile usare [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) o l'[interfaccia della riga di comando](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Impostazioni di esempio

Quando si utilizzano questi passaggi come esercizio, è possibile utilizzare i valori delle impostazioni di esempio hello. A scopo esemplificativo, vengono usati più spazi di indirizzi per ogni rete virtuale, anche se per le configurazioni da rete virtuale a rete virtuale non sono necessari.

**Valori per TestVNet1:**

* Nome della rete virtuale: TestVNet1
* Spazio di indirizzi: 10.11.0.0/16
  * Nome subnet: FrontEnd
  * Intervallo di indirizzi subnet: 10.11.0.0/24
* Gruppo di risorse: TestRG1
* Location: Stati Uniti orientali
* Spazio di indirizzi: 10.12.0.0/16
  * Nome subnet: BackEnd
  * Intervallo di indirizzi subnet: 10.12.0.0/24
* Nome Subnet del gateway: GatewaySubnet (in modo da consentire il riempimento automatico nel portale di hello)
  * Intervallo di indirizzi subnet del gateway: 10.11.255.0/27
* Server DNS: Utilizzare l'indirizzo IP di hello del Server DNS
* Nome gateway di rete virtuale: TestVNet1GW
* Tipo di gateway: VPN
* Tipo VPN: Basato su route
* SKU: Selezionare hello desiderato toouse SKU di Gateway
* Nome dell'indirizzo IP pubblico: TestVNet1GWIP
* Valori di connessione:
  * Nome: TestVNet1toTestVNet4
  * Chiave condivisa: È possibile creare personalmente la chiave condivisa hello. In questo esempio viene usato il valore abc123. la cosa importante Hello è che quando si crea una connessione di hello tra reti virtuali hello, hello valore deve corrispondere.

**Valori per TestVNet4:**

* Nome della rete virtuale: TestVNet4
* Spazio di indirizzi: 10.41.0.0/16
  * Nome subnet: FrontEnd
  * Intervallo di indirizzi subnet: 10.41.0.0/24
* Gruppo di risorse: TestRG1
* Località: Stati Uniti occidentali
* Spazio di indirizzi: 10.42.0.0/16
  * Nome subnet: BackEnd
  * Intervallo di indirizzi subnet: 10.42.0.0/24
* Nome GatewaySubnet: GatewaySubnet (in modo da consentire il riempimento automatico nel portale di hello)
  * Intervallo di indirizzi subnet del gateway: 10.41.255.0/27
* Server DNS: Utilizzare l'indirizzo IP di hello del Server DNS
* Nome gateway di rete virtuale: TestVNet4GW
* Tipo di gateway: VPN
* Tipo VPN: Basato su route
* SKU: Selezionare hello desiderato toouse SKU di Gateway
* Nome dell'indirizzo IP pubblico: TestVNet4GWIP
* Valori di connessione:
  * Nome: TestVNet4toTestVNet1
  * Chiave condivisa: È possibile creare personalmente la chiave condivisa hello. In questo esempio viene usato il valore abc123. la cosa importante Hello è che quando si crea una connessione di hello tra reti virtuali hello, hello valore deve corrispondere.

## <a name="CreatVNet"></a>1. Creare e configurare TestVNet1
Se si dispone già di una rete virtuale, verificare che le impostazioni di hello siano compatibili con la progettazione di gateway VPN. Prestare particolare attenzione tooany subnet che si sovrappongano con altre reti. Se sono presenti subnet che si sovrappongono, la connessione non funziona correttamente. Se la rete virtuale è configurata con le impostazioni corrette hello, è possibile iniziare i passaggi di hello in hello [specificare un server DNS](#dns) sezione.

### <a name="toocreate-a-virtual-network"></a>toocreate una rete virtuale
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Aggiungere altri spazi degli indirizzi e creare subnet
Dopo aver creato la rete virtuale è possibile aggiungere altri spazi degli indirizzi e creare subnet.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Creare una subnet del gateway
Prima della connessione del gateway di rete virtuale tooa, è necessario innanzitutto subnet del gateway hello toocreate per hello toowhich di rete virtuale si desidera tooconnect. Se possibile, è migliore toocreate una subnet del gateway con un blocco CIDR di /28 o /27 in ordine tooprovide sufficiente indirizzi requisiti di configurazione di futuri aggiuntivi tooaccommodate.

Se si sta creando questa configurazione come esercizio, fare riferimento toothese [impostazioni di esempio](#values) quando si crea la subnet del gateway.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>toocreate una subnet del gateway
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Specificare un server DNS (facoltativo)
Il server DNS non è necessario per le connessioni da rete virtuale a rete virtuale. Tuttavia, se si desidera la risoluzione dei nomi toohave per le risorse di rete virtuale tooyour distribuito, specificare un server DNS. Questa impostazione consente di specificare i server DNS hello che si vuole toouse per la risoluzione dei nomi per la rete virtuale. Non comporta la creazione di un server DNS.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. Creare un gateway di rete virtuale
In questo passaggio viene creato il gateway di rete virtuale hello per la rete virtuale. Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU. Se si sta creando questa configurazione come esercizio, è possibile fare riferimento toohello [impostazioni di esempio](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>toocreate un gateway di rete virtuale
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. Creare e configurare TestVNet4
Dopo aver configurato TestVNet1, creare TestVNet4 ripetendo i passaggi precedenti hello, sostituendo i valori hello con quelli di TestVNet4. Non è necessario toowait fino a quando il gateway di rete virtuale hello per TestVNet1 ha completato la creazione prima di configurare TestVNet4. Se si usa valori personalizzati, assicurarsi che gli spazi degli indirizzi di hello non coincidano con le reti virtuali che si desidera tooconnect per hello.

## <a name="TestVNet1Connection"></a>7. Configurare la connessione hello TestVNet1
Gateway di rete virtuale hello TestVNet1 sia TestVNet4 completati, è possibile creare connessioni gateway della rete virtuale. In questa sezione verrà creata una connessione da tooVNet4 VNet1. Questa procedura funziona solo per le reti virtuali in hello stessa sottoscrizione. Se le reti virtuali in diverse sottoscrizioni, è necessario utilizzare la connessione di hello toomake di PowerShell. Vedere hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) articolo.

1. In **tutte le risorse**, passare toohello gateway di rete virtuale per la rete virtuale. Ad esempio, **TestVNet1GW**. Fare clic su **TestVNet1GW** blade di gateway tooopen hello rete virtuale.
   
    ![Pannello connessioni](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Pannello connessioni")
2. Fare clic su **+ Aggiungi** tooopen hello **Aggiungi connessione** blade.
3. In hello **Aggiungi connessione** pannello, nel campo nome hello, digitare un nome per la connessione. Ad esempio, **TestVNet1toTestVNet4**.
   
    ![Nome connessione](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Nome connessione")
4. Per **Tipo di connessione**, Selezionare **per rete virtuale a** dall'elenco a discesa hello.
5. Hello **primo gateway di rete virtuale** valore del campo viene compilato automaticamente perché si sta creando la connessione da gateway di rete virtuale specificata hello.
6. Hello **secondo gateway di rete virtuale** campo è il gateway di rete virtuale hello di hello rete virtuale che si desidera toocreate una connessione. Fare clic su **scegliere un altro gateway di rete virtuale** tooopen hello **scegliere gateway di rete virtuale** blade.
   
    ![Aggiungi connessione](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Aggiungi connessione")
7. Gateway di rete virtuale hello visualizzazione elencati in questo pannello. Si noti che sono elencati solo i gateway di rete virtuale inclusi nella sottoscrizione. Se si desidera tooconnect tooa gateway della rete virtuale che non è incluso nella sottoscrizione, utilizzare hello [articolo PowerShell](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Fare clic su gateway della rete virtuale che si desidera tooconnect per hello.
9. In hello **chiave condivisa** , digitare una chiave condivisa per la connessione. La chiave può essere generata o creata dall'utente. In una connessione site-to-site, chiave hello usare potrebbe essere esattamente hello lo stesso per il dispositivo locale e la connessione del gateway di rete virtuale. il concetto di Hello è simile, tranne il fatto che invece di dispositivo VPN di connessione tooa, ci si connette tooanother gateway di rete virtuale.
   
    ![Chiave condivisa](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Chiave condivisa")
10. Fare clic su **OK** in hello fondo hello pannello toosave le modifiche.

## <a name="TestVNet4Connection"></a>8. Configurare la connessione hello TestVNet4
Successivamente, creare una connessione da TestVNet4 tooTestVNet1. Utilizzare hello stesso metodo di connessione di hello toocreate da TestVNet1 tooTestVNet4 utilizzato. Assicurarsi di utilizzare hello stessa chiave condivisa.

## <a name="VerifyConnection"></a>9. Verificare la connessione
Verificare la connessione hello. Per ogni gateway di rete virtuale, hello seguenti:

1. Individuare il pannello hello per gateway di rete virtuale hello. Ad esempio, **TestVNet4GW**. 
2. Nel Pannello di gateway di rete virtuale hello, fare clic su **connessioni** tooview hello connessioni pannello gateway di rete virtuale hello.

Visualizzare le connessioni di hello e verificare lo stato di hello. Dopo aver creata la connessione hello, si noterà **Succeeded** e **connesso** come hello valori di stato.

![Operazione riuscita](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Operazione riuscita")

È possibile fare doppio clic su ciascuna connessione separatamente tooview ulteriori informazioni sulla connessione hello.

![Informazioni di base](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Informazioni di base")

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale
Visualizzare i dettagli di hello domande frequenti per ulteriori informazioni sulle connessioni di rete virtuale a.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Vedere hello [macchine virtuali-documentazione](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) per ulteriori informazioni.
