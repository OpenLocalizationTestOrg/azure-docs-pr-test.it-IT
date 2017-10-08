---
title: 'La connessione di rete virtuale tooanother rete virtuale: CLI di Azure | Documenti Microsoft'
description: Questo articolo illustra la connessione tra reti virtuali tramite Azure Resource Manager e l'interfaccia della riga di comando di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configurare una connessione gateway VPN tra reti virtuali usando l'interfaccia della riga di comando di Azure

In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali. Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni. Quando le reti virtuali connessione da sottoscrizioni diverse, le sottoscrizioni di hello non necessaria toobe associato hello stesso tenant di Active Directory. 

passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello e utilizzano CLI di Azure. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connettersi tra modelli di distribuzione diversi - Portale di Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connettersi tra modelli di distribuzione diversi - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. Se le reti virtuali si trovano in hello stessa area, è opportuno tooconsider collegarli tramite Peering reti virtuali. Peering reti virtuali non usa un gateway VPN. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).

La comunicazione tra reti virtuali può essere associata a configurazioni multisito. Consente di stabilire le topologie di rete che combinano connettività cross-premise con connettività di rete virtuale tra, come illustrato nel seguente diagramma hello:

![Informazioni sulle connessioni](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Perché connettere reti virtuali?

Si consiglia le reti virtuali tooconnect per hello seguenti motivi:

* **Presenza e ridondanza in più aree geografiche**

  * È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.
  * Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure. Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.
* **Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**

  * Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse a causa di tooisolation o i requisiti amministrativi.

Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo.

### <a name="which-set-of-steps-should-i-use"></a>Quale procedura è consigliabile seguire?

Questo articolo riporta due diverse procedure. Un set di passaggi per [hello di reti virtuali che si trovano nella stessa sottoscrizione](#samesub)e un altro per [reti virtuali che risiedono in diverse sottoscrizioni](#difsub).

## <a name="samesub"></a>Connettere reti virtuali presenti hello stessa sottoscrizione

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo). Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Pianificare gli intervalli di indirizzi IP

In hello alla procedura seguente, vengono create due reti virtuali insieme le subnet gateway rispettivi e configurazioni. È quindi creare una connessione VPN tra hello due reti virtuali. È importante tooplan hello indirizzi IP per la configurazione di rete. Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo. In questi esempi non viene incluso un server DNS. Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Utilizziamo hello seguente i valori negli esempi di hello:

**Valori per TestVNet1:**

* Nome della rete virtuale: TestVNet1
* Gruppo di risorse: TestRG1
* Location: Stati Uniti orientali
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP pubblico: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valori per TestVNet4:**

* Nome della rete virtuale: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Gruppo di risorse: TestRG4
* Località: Stati Uniti occidentali
* GatewayName: VNet4GW
* IP pubblico: VNet4GWIP
* VPNType: RouteBased
* Connessione: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>Passaggio 1: connettere tooyour sottoscrizione

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Passaggio 2: Creare e configurare TestVNet1

1. Creare un gruppo di risorse.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Creare subnet TestVNet1 e hello per TestVNet1. Questo esempio crea una rete virtuale denominata TestVNet1 e una subnet denominata FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Creare uno spazio di indirizzi aggiuntivi per la subnet di back-end hello. Si noti che in questo passaggio è specificare sia lo spazio degli indirizzi di hello creato in precedenza e hello ulteriore spazio degli indirizzi che si desidera tooadd. Infatti, hello [aggiornamento rete virtuale di rete az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando sovrascrive le impostazioni precedenti hello. Verificare che toospecify tutti i prefissi di indirizzo hello quando si utilizza questo comando.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Creare subnet back-end hello.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Creare subnet del gateway hello. Si noti che la subnet gateway hello è denominata 'GatewaySubnet'. Questo nome è obbligatorio. In questo esempio subnet del gateway hello utilizza un /27. Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando almeno /28 o /27. In questo modo per sufficiente indirizzi tooaccommodate possibili configurazioni aggiuntive che è possibile in hello future.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta. Si noti che hello AllocationMethod è dinamico. È possibile specificare l'indirizzo IP hello che si desidera toouse. È il gateway tooyour allocata in modo dinamico.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Creare il gateway di rete virtuale hello per TestVNet1. Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased. Se si esegue questo comando hello utilizzando il parametro '-- Nessun - wait', non sono visibili eventuali commenti e suggerimenti o output. Hello '-- Nessun - wait' parametro consente toocreate gateway hello in background hello. Questo significa che tale gateway VPN hello termine della creazione immediatamente. Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway hello SKU in uso.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Passaggio 3: Creare e configurare TestVNet4

1. Creare un gruppo di risorse.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Creare TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Creare altre subnet per TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Creare subnet del gateway hello.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Richiedere un indirizzo IP pubblico.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Creare il gateway di rete virtuale TestVNet4 hello.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Passaggio 4: creare connessioni hello

Ora sono disponibili due reti virtuali con i gateway VPN. passaggio successivo Hello è connessioni gateway VPN di toocreate tra il gateway di rete virtuale hello. Se è stata utilizzata negli esempi di hello sopra riportati, i gateway si trovano in gruppi di risorse diverso. Quando il gateway si trovano in gruppi di risorse diversi, è necessario tooidentify e specificare l'ID di risorsa hello per ogni gateway per stabilire una connessione. Se le reti virtuali si trovano in hello stesso gruppo di risorse, è possibile utilizzare hello [secondo set di istruzioni](#samerg) perché non è necessario l'ID di risorsa toospecify hello.

### <a name="diffrg"></a>tooconnect reti virtuali che si trovano in diversi gruppi di risorse

1. Ottenere ID risorsa di VNet1GW hello dall'output di hello di hello comando seguente:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Nell'output di hello, trovare hello "id:" riga. i valori di Hello virgolette hello sono necessari toocreate hello connessione nella sezione successiva hello. Copiare questi editor di testo tooa valori, ad esempio Blocco note, in modo che sia possibile incollarli facilmente quando si crea la connessione.

  Output di esempio:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Copiare i valori hello dopo **"id":** virgolette hello.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Ottenere hello ID risorsa di VNet4GW e copia hello valori tooa editor di testo.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Creare hello TestVNet1 tooTestVNet4 connessione. In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4. È una chiave condivisa a cui fa riferimento negli esempi di hello. È possibile utilizzare i valori per la chiave condivisa hello. cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni. Creazione di una connessione richiede poco toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Creare hello TestVNet4 tooTestVNet1 connessione. Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1. Assicurarsi che le chiavi condivise hello corrispondano. Richiede pochi minuti connessione hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Verificare le connessioni. Vedere [Verificare la connessione](#verify).

### <a name="samerg"></a>tooconnect reti virtuali che risiedono in hello stesso gruppo di risorse

1. Creare hello TestVNet1 tooTestVNet4 connessione. In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4. Gruppi di risorse di notifica hello sono hello stesso negli esempi di hello. È inoltre possibile visualizzare una chiave condivisa a cui fa riferimento negli esempi di hello. È possibile utilizzare i valori per la chiave condivisa hello, tuttavia, la chiave condivisa hello deve corrispondere per entrambe le connessioni. Creazione di una connessione richiede poco toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Creare hello TestVNet4 tooTestVNet1 connessione. Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1. Assicurarsi che le chiavi condivise hello corrispondano. Richiede pochi minuti connessione hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Verificare le connessioni. Vedere [Verificare la connessione](#verify).

## <a name="difsub"></a>Connettere reti virtuali che si trovano in sottoscrizioni diverse

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5, Hello reti virtuali si trovano diverse sottoscrizioni. le sottoscrizioni di Hello non è necessario toobe associato hello stesso tenant di Active Directory. nei passaggi Hello per questa configurazione aggiunge una connessione di rete virtuale a aggiuntiva in ordine tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Passaggio 5: Creare e configurare TestVNet1

Queste istruzioni continuano da passi hello in hello sezioni precedenti. È necessario completare [passaggio 1](#Connect) e [passaggio 2](#TestVNet1) toocreate e configurare TestVNet1 e hello Gateway VPN per TestVNet1. Per questa configurazione, non è necessario toocreate TestVNet4 dalla sezione precedente hello, sebbene se viene creato, non creerà conflitti con questa procedura. Al termine, continuare con il passaggio 6 (sotto).

### <a name="verifyranges"></a>Passaggio 6: verificare gli intervalli di indirizzi IP hello

Quando si creano connessioni aggiuntive, è importante tooverify che non si sovrapponga a spazio di indirizzi IP hello della nuova rete virtuale hello con uno qualsiasi di altri intervalli di rete virtuale o intervalli di gateway di rete locale. Per questo esercizio, è possibile utilizzare i seguenti valori per hello TestVNet5 hello:

**Valori per TestVNet5:**

* Nome della rete virtuale: TestVNet5
* Gruppo di risorse: TestRG5
* Ubicazione: Giappone orientale
* TestVNet5: 10.51.0.0/16 e 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP pubblico: VNet5GWIP
* VPNType: RouteBased
* Connessione: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>Passaggio 7: Creare e configurare TestVNet5

Questo passaggio deve essere eseguito nel contesto di hello di hello nuova sottoscrizione 5 di sottoscrizione. Questa parte può essere eseguita dall'amministratore di hello in un'altra organizzazione che possiede la sottoscrizione hello. tooswitch tra l'utilizzo di sottoscrizioni ' elenco di account az - tutti ' toolist hello account tooyour disponibili sottoscrizioni, quindi utilizzare ' set di account az - sottoscrizione <subscriptionID>' tooswitch toohello sottoscrizione che si desidera toouse.

1. Verificare che si sono connessi tooSubscription 5, quindi crea un gruppo di risorse.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Creare TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Aggiungere le subnet.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Aggiungi subnet gateway hello.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Richiedere un indirizzo IP pubblico.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Creare il gateway TestVNet5 hello

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Passaggio 8: creare connessioni hello

Verranno suddivise in questo passaggio in due sessioni CLI contrassegnato come **[sottoscrizione 1]**, e **[sottoscrizione 5]** perché sono gateway hello in diverse sottoscrizioni hello. tooswitch tra l'utilizzo di sottoscrizioni ' elenco di account az - tutti ' toolist hello account tooyour disponibili sottoscrizioni, quindi utilizzare ' set di account az - sottoscrizione <subscriptionID>' tooswitch toohello sottoscrizione che si desidera toouse.

1. **[Sottoscrizione 1]**  Accedi e connettersi tooSubscription 1. Comando che segue hello esecuzione tooget hello nome e l'ID di hello Gateway dall'output di hello:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copia output di hello per "id:". Inviare hello ID e nome hello di hello rete virtuale (VNet1GW) toohello amministratore del gateway di 5 sottoscrizione tramite posta elettronica o un altro metodo.

  Output di esempio:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Sottoscrizione 5]**  Accedi e connettersi tooSubscription 5. Comando che segue hello esecuzione tooget hello nome e l'ID di hello Gateway dall'output di hello:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copia output di hello per "id:". Inviare hello ID e nome hello di hello rete virtuale (VNet5GW) toohello amministratore del gateway 1 sottoscrizione tramite posta elettronica o un altro metodo.

3. **[Sottoscrizione 1]**  In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet5. È possibile utilizzare i valori per la chiave condivisa hello, tuttavia, la chiave condivisa hello deve corrispondere per entrambe le connessioni. Creazione di una connessione può richiedere poco toocomplete. Assicurarsi che ci si connette tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Sottoscrizione 5]**  Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet5 tooTestVNet1. Verificare che tale hello condiviso in corrispondenza delle chiavi e che ci si connette tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Verificare le connessioni hello
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi

* Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per ulteriori informazioni, vedere hello [macchine virtuali-documentazione](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
