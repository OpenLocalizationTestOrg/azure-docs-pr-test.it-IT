---
title: 'Connettere una rete virtuale a un''altra rete virtuale con una connessione da rete virtuale a rete virtuale: interfaccia della riga di comando di Azure | Microsoft Docs'
description: Questo articolo illustra in modo dettagliato come connettere reti virtuali usando una connessione da rete virtuale a rete virtuale e l'interfaccia della riga di comando di Azure.
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
ms.date: 11/29/2017
ms.author: cherylmc
ms.openlocfilehash: 663e3cb35308b354c7221e34ac6fcfc8eda15f2a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configurare una connessione gateway VPN tra reti virtuali usando l'interfaccia della riga di comando di Azure

Questo articolo mostra come connettere reti virtuali tramite il tipo di connessione da rete virtuale a rete virtuale. Le reti virtuali possono trovarsi in aree geografiche uguali o diverse e in sottoscrizioni uguali o diverse. Quando si connettono reti virtuali da sottoscrizioni diverse, non è necessario che le sottoscrizioni siano associate allo stesso tenant di Active Directory.

La procedura illustrata in questo articolo si applica al modello di distribuzione Resource Manager e usano l'interfaccia della riga di comando di Azure. È anche possibile creare questa configurazione usando strumenti o modelli di distribuzione diversi selezionando un'opzione differente nell'elenco seguente:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connettersi tra modelli di distribuzione diversi - Portale di Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connettersi tra modelli di distribuzione diversi - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

## <a name="about"></a>Informazioni sulla connessione di reti virtuali

Ci sono diversi modi per connettere le reti virtuali. Le sezioni seguenti descrivono i diversi metodi di connessione delle reti virtuali.

### <a name="vnet-to-vnet"></a>Tra reti virtuali

La configurazione di una connessione da rete virtuale a rete virtuale rappresenta un buon metodo per connettere facilmente le reti virtuali. La connessione di una rete virtuale a un'altra rete virtuale tramite il tipo di connessione da rete virtuale a rete virtuale è simile alla creazione di una connessione IPsec da sito a sito in una posizione locale. Entrambi i tipi di connettività usano un gateway VPN per fornire un tunnel sicuro tramite IPsec/IKE ed entrambi funzionano in modo analogo durante la comunicazione. La differenza tra i tipi di connessione è costituita dal modo in cui viene configurato il gateway di rete locale. Quando si crea una connessione da rete virtuale a rete virtuale, non viene visualizzato lo spazio indirizzi del gateway di rete locale, che viene creato e popolato automaticamente. Se si aggiorna lo spazio indirizzi per una rete virtuale, l'altra rete virtuale eseguirà automaticamente il routing allo spazio indirizzi aggiornato. La creazione di una connessione da rete virtuale a rete virtuale è in genere più veloce e semplice rispetto alla creazione di una connessione da sito a sito tra reti virtuali.

### <a name="connecting-vnets-using-site-to-site-ipsec-steps"></a>Connessione di reti virtuali tramite la procedura di connessione da sito a sito (IPsec)

Se si usa una configurazione di rete complessa, potrebbe essere preferibile connettersi alle reti virtuali usando la procedura di connessione [da sito a sito](vpn-gateway-howto-site-to-site-resource-manager-cli.md) invece di quella di connessione da rete virtuale a rete virtuale. Con la procedura di connessione da sito a sito, è necessario creare e configurare manualmente i gateway di rete locali. Il gateway di rete locale per ogni rete virtuale considera l'altra rete virtuale come sito locale. Ciò consente di specificare uno spazio indirizzi aggiuntivo per il gateway di rete locale per il routing del traffico. Se lo spazio indirizzi per una rete virtuale cambia, è necessario aggiornare manualmente di conseguenza il gateway di rete locale corrispondente. L'aggiornamento non avviene automaticamente.

### <a name="vnet-peering"></a>Peering reti virtuali

È possibile connettere le reti virtuali tramite il peering reti virtuali. Il peering reti virtuali non usa un gateway VPN e presenta vincoli diversi. I [prezzi per il peering reti virtuali](https://azure.microsoft.com/pricing/details/virtual-network) vengono inoltre calcolati in modo diverso rispetto ai [prezzi per il gateway VPN da rete virtuale a rete virtuale](https://azure.microsoft.com/pricing/details/vpn-gateway). Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).

## <a name="why"></a>Vantaggi di una connessione da rete virtuale a rete virtuale

È possibile connettere le reti virtuali con una connessione da rete virtuale a rete virtuale per i motivi seguenti:

* **Presenza e ridondanza in più aree geografiche**

  * È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.
  * Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure. Un esempio importante è rappresentato dalla configurazione SQL AlwaysOn con gruppi di disponibilità distribuiti in più aree di Azure.
* **Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**

  * All'interno di una stessa area è possibile configurare applicazioni multilivello con più reti virtuali connesse tra loro a causa dell'isolamento o di requisiti amministrativi.

La comunicazione tra reti virtuali può essere associata a configurazioni multisito. Questo permette di definire topologie di rete che consentono di combinare la connettività cross-premise con la connettività tra reti virtuali.

## <a name="steps"></a>Quale procedura per la connessione da rete virtuale a rete virtuale è preferibile seguire?

Questo articolo illustra due diverse procedure di connessione da rete virtuale a rete virtuale. Una per le [reti virtuali che si trovano nella stessa sottoscrizione](#samesub) e una per le [reti virtuali che si trovano in sottoscrizioni diverse](#difsub). 

Per questo esercizio è possibile combinare le configurazioni oppure sceglierne una da usare. Tutte le configurazioni usano il tipo di connessione da rete virtuale a rete virtuale. Il traffico di rete viene trasmesso tra le reti virtuali connesse direttamente tra loro. In questo esercizio, il traffico da TestVNet4 non viene indirizzato a TestVNet5.

* [Reti virtuali che si trovano nella stessa sottoscrizione:](#samesub) la procedura per questa configurazione usa TestVNet1 e TestVNet4.

  ![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

* [Reti virtuali che si trovano in sottoscrizioni diverse:](#difsub) la procedura per questa configurazione usa TestVNet1 e TestVNet5.

  ![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)


## <a name="samesub"></a>Connettere reti virtuali che si trovano nella stessa sottoscrizione

### <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare, installare la versione più recente dei comandi dell'interfaccia della riga di comando (2.0 o successiva). Per informazioni sull'installazione dei comandi dell'interfaccia della riga di comando, vedere [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).

### <a name="Plan"></a>Pianificare gli intervalli di indirizzi IP

Nei passaggi seguenti vengono create due reti virtuali con le rispettive subnet del gateway e configurazioni. Viene quindi creata una connessione VPN tra le due reti virtuali. È importante pianificare gli intervalli di indirizzi IP per la configurazione di rete. Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo. In questi esempi non viene incluso un server DNS. Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Negli esempi vengono usati i valori seguenti:

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
* Connection(1to5): VNet1toVNet5 (per reti virtuali in diverse sottoscrizioni)

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

### <a name="Connect"></a>Passaggio 1: Connettersi alla sottoscrizione

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Passaggio 2: Creare e configurare TestVNet1

1. Creare un gruppo di risorse.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Creare TestVNet1 e le subnet per TestVNet1. Questo esempio crea una rete virtuale denominata TestVNet1 e una subnet denominata FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Creare uno spazio indirizzi aggiuntivo per la subnet back-end. Si noti che in questo passaggio vengono specificati sia lo spazio indirizzi creato prima che lo spazio indirizzi aggiuntivo che si vuole aggiungere. Infatti il comando [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_update) sovrascrive le impostazioni precedenti. Quando si usa questo comando, assicurarsi di specificare tutti i prefissi degli indirizzi.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Creare la subnet back-end.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Creare la subnet del gateway. Si noti che la subnet del gateway viene denominata "GatewaySubnet". Questo nome è obbligatorio. In questo esempio, la subnet del gateway usa /27. Nonostante sia possibile creare una subnet del gateway con dimensioni di /29 soltanto, è consigliabile crearne una più grande che includa più indirizzi selezionando almeno /28 o /27. In questo modo saranno disponibili indirizzi sufficienti per supportare in futuro le possibili configurazioni aggiuntive desiderate.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Richiedere un indirizzo IP pubblico da allocare per il gateway che verrà creato per la rete virtuale. Si noti che AllocationMethod è dinamico. Non è possibile specificare l'indirizzo IP che si desidera usare. Viene allocato in modo dinamico per il gateway.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Creare il gateway di rete virtuale per TestVNet1. Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased. Se si esegue questo comando usando il parametro '--no-wait', non viene visualizzato alcun output o commento. Il parametro "--no-wait" consente la creazione in background del gateway. Questo non significa che la creazione del gateway VPN termina immediatamente. La creazione di un gateway spesso richiede anche più di 45 minuti di tempo a seconda dell'SKU gateway usato.

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
4. Creare la subnet del gateway.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Richiedere un indirizzo IP pubblico.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Creare il gateway di rete virtuale TestVNet4.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Passaggio 4: Creare le connessioni

Ora sono disponibili due reti virtuali con i gateway VPN. Il passaggio successivo prevede la creazione di connessioni gateway VPN tra i gateway di rete virtuale. Se sono stati usati gli esempi precedenti, i gateway di rete virtuale sono in gruppi di risorse diversi. Quando i gateway sono in gruppi di risorse diversi, è necessario identificare e specificare gli ID risorsa per ogni gateway quando si stabilisce una connessione. Se le reti virtuali sono nello stesso gruppo di risorse, è possibile usare il [secondo set di istruzioni](#samerg) perché non è necessario specificare gli ID risorsa.

### <a name="diffrg"></a>Per connettere reti virtuali che si trovano in gruppi di risorse diversi

1. Ottenere l'ID di risorsa di VNet1GW dall'output del comando seguente:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Nell'output trovare la riga "id:". I valori tra virgolette sono necessari per creare la connessione nella sezione successiva. Copiare questi valori in un editor di testo, ad esempio il Blocco note, per poterli incollare facilmente quando si crea la connessione.

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

  Copiare i valori dopo **"id":** tra virgolette.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Ottenere l'ID risorsa di VNet4GW e copiare i valori in un editor di testo.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Creare la connessione da TestVNet1 a TestVNet4. In questo passaggio viene creata la connessione da TestVNet1 a TestVNet4. È presente una chiave condivisa a cui si fa riferimento negli esempi. È possibile utilizzare i propri valori specifici per la chiave condivisa. L'importante è che la chiave condivisa corrisponda per entrambe le configurazioni. Il completamento della creazione di una connessione richiede un po' di tempo.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Creare la connessione da TestVNet4 a TestVNet1. Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet4 a TestVNet1. Assicurarsi che le chiavi condivise corrispondano. Per stabilire la connessione, sono necessari alcuni minuti.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Verificare le connessioni. Vedere [Verificare la connessione](#verify).

### <a name="samerg"></a>Per connettere reti virtuali che si trovano nello stesso gruppo di risorse

1. Creare la connessione da TestVNet1 a TestVNet4. In questo passaggio viene creata la connessione da TestVNet1 a TestVNet4. Si noti che i gruppi di risorse sono uguali negli esempi. Viene anche visualizzata una chiave condivisa a cui si fa riferimento negli esempi. È possibile usare i propri valori per la chiave condivisa che però deve essere la stessa per entrambe le connessioni. Il completamento della creazione di una connessione richiede un po' di tempo.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Creare la connessione da TestVNet4 a TestVNet1. Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet4 a TestVNet1. Assicurarsi che le chiavi condivise corrispondano. Per stabilire la connessione, sono necessari alcuni minuti.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Verificare le connessioni. Vedere [Verificare la connessione](#verify).

## <a name="difsub"></a>Connettere reti virtuali che si trovano in sottoscrizioni diverse

In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5, Le reti virtuali si trovano in sottoscrizioni diverse. Non è necessario che le sottoscrizioni siano associate allo stesso tenant di Active Directory. I passaggi di questa configurazione permettono di aggiungere un'altra connessione tra reti virtuali per connettere TestVNet1 e TestVNet5.

### <a name="TestVNet1diff"></a>Passaggio 5: Creare e configurare TestVNet1

Queste istruzioni sono il proseguimento dei passaggi delle sezioni precedenti. È necessario completare il [passaggio 1](#Connect) e il [passaggio 2](#TestVNet1) per creare e configurare TestVNet1 e il gateway VPN per TestVNet1. Per questo configurazione, non è necessario creare TestVNet4 dalla sezione precedente, ma, se è già stata creata, non si verificheranno conflitti con questi passaggi. Al termine, continuare con il passaggio 6 (sotto).

### <a name="verifyranges"></a>Passaggio 6: Verificare gli intervalli di indirizzi IP

Quando si creano connessioni aggiuntive, è importante verificare che lo spazio di indirizzi IP della nuova rete virtuale non si sovrapponga a nessuno degli altri intervalli di rete virtuale o intervalli di gateway di rete locale. Per questo esercizio è possibile usare i valori seguenti per TestVNet5:

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

Questo passaggio deve essere eseguito nel contesto della nuova sottoscrizione, la sottoscrizione 5. Questa parte può essere eseguita dall'amministratore in un'altra organizzazione che possiede la sottoscrizione. Per passare da una sottoscrizione all'altra, usare "az account list --all" per elencare le sottoscrizioni disponibili per l'account, quindi usare "az account set --subscription <subscriptionID>" per passare alla sottoscrizione che si vuole usare.

1. Verificare di essere connessi alla sottoscrizione 5, quindi creare un gruppo di risorse.

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

4. Aggiungere la subnet del gateway.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Richiedere un indirizzo IP pubblico.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Creare il gateway di TestVNet5

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Passaggio 8: Creare le connessioni

Questo passaggio è suddiviso in due sessioni dell'interfaccia della riga di comando, contrassegnate come **[Sottoscrizione 1]** e **[Sottoscrizione 5]**, perché i gateway si trovano in sottoscrizioni diverse. Per passare da una sottoscrizione all'altra, usare "az account list --all" per elencare le sottoscrizioni disponibili per l'account, quindi usare "az account set --subscription <subscriptionID>" per passare alla sottoscrizione che si vuole usare.

1. **[Sottoscrizione 1]** Eseguire l'accesso e connettersi alla sottoscrizione 1. Usare il comando seguente per ottenere il nome e l'ID del gateway dall'output:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copiare l'output per "id:". Inviare l'ID e il nome del gateway della rete virtuale (VNet1GW) all'amministratore della sottoscrizione 5 tramite posta elettronica o un altro metodo.

  Output di esempio:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Sottoscrizione 5]** Eseguire l'accesso e connettersi alla sottoscrizione 5. Usare il comando seguente per ottenere il nome e l'ID del gateway dall'output:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copiare l'output per "id:". Inviare l'ID e il nome del gateway della rete virtuale (VNet5GW) all'amministratore della sottoscrizione 1 tramite posta elettronica o un altro metodo.

3. **[Sottoscrizione 1]** In questo passaggio viene creata la connessione da TestVNet1 a TestVNet5. È possibile usare i propri valori per la chiave condivisa che però deve essere la stessa per entrambe le connessioni. Il completamento della creazione di una connessione può richiedere un po' di tempo. Connettersi alla Sottoscrizione 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Sottoscrizione 5]** Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet5 a TestVNet1. Verificare che le chiavi condivise corrispondano e di essere connessi alla sottoscrizione 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Verificare le connessioni
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-faq-vnet-vnet-include.md)]

## <a name="next-steps"></a>Passaggi successivi

* Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali. Per altre informazioni, vedere la [documentazione sulle macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Per informazioni su BGP, vedere [Panoramica di BGP](vpn-gateway-bgp-overview.md) e [Come configurare BGP](vpn-gateway-bgp-resource-manager-ps.md).