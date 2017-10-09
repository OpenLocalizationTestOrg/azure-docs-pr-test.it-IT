---
title: 'Connettere le reti virtuali classiche tooAzure VNets Gestione risorse: portale | Documenti Microsoft'
description: Informazioni su come toocreate una connessione VPN tra classico reti virtuali e Gestione risorse VNets tramite Gateway VPN e del portale hello
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Connettere reti virtuali da modelli di distribuzione diversi tramite il portale di hello

Questo articolo illustra come tooconnect tooResource di reti virtuali classiche tooallow Manager VNets hello risorse che si trovano in toocommunicate di modelli di distribuzione separata hello tra loro. passaggi di Hello in questo articolo usano principalmente hello portale di Azure, ma è anche possibile creare questa configurazione tramite PowerShell hello selezionando articolo hello da questo elenco.

> [!div class="op_single_selector"]
> * [Portale](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

La connessione di un classico tooa di rete virtuale VNet Gestione risorse è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. È possibile creare una connessione tra reti virtuali in sottoscrizioni diverse e in aree diverse. È inoltre possibile connettersi reti virtuali che dispone già di reti locali tooon di connessioni, come gateway hello che sono stati configurati con è dinamico o basato su route. Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo. 

Se le reti virtuali si trovano in hello stessa area, è opportuno prendere in considerazione tooinstead collegarli tramite Peering reti virtuali. Peering reti virtuali non usa un gateway VPN. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Prerequisiti

* Questa procedura presuppone che entrambe le reti virtuali siano già state create. Se si utilizza questo articolo come un esercizio e non le reti virtuali, sono disponibili collegamenti in hello passaggi toohelp sono stati creati.
* Verificare che gli intervalli di indirizzi hello per le reti virtuali non si sovrappongono reciprocamente hello o gli intervalli si sovrappongono con i hello per le altre connessioni che hello gateway potrebbero essere connessa alla.
* Installare i cmdlet di PowerShell più recenti hello per Gestione risorse e gestione dei servizi (classica). In questo articolo vengono utilizzati sia hello portale di Azure e PowerShell. PowerShell è obbligatorio toocreate hello connessione hello toohello di rete virtuale classica VNet Gestione risorse. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Impostazioni di esempio

È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.

**Rete virtuale classica**

Nome rete virtuale = ClassicVNet <br>
Spazio indirizzi = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
Gruppo di risorse = ClassicRG <br>
Località = Stati Uniti occidentali <br>
GatewaySubnet: 10.0.0.32/28 <br>
Sito locale = RMVNetLocal <br>

**Rete virtuale di Resource Manager**

Nome della rete virtuale = RMVNet <br>
Spazio indirizzi = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Gruppo di risorse= RG1 <br>
Località = Stati Uniti orientali <br>
Nome gateway di rete virtuale = RMGateway <br>
Tipo di gateway = VPN <br>
Tipo VPN= Basato su route <br>
Nome indirizzo IP pubblico del gateway = rmgwpip <br>
Gateway di rete locale = ClassicVNetLocal <br>
Nome della connessione = RMtoClassic

### <a name="connection-overview"></a>Panoramica sulla connessione

Per questa configurazione, si crea una connessione gateway VPN tramite un tunnel VPN IPsec/IKE tra reti virtuali hello. Assicurarsi che nessuno degli intervalli di rete virtuale si sovrappongono reciprocamente o con reti hello locale che si connettono a.

Hello nella tabella seguente viene illustrato un esempio di come sono definiti hello esempio le reti virtuali e siti locali:

| Rete virtuale | Spazio di indirizzi | Region | Si connette il sito di rete toolocal |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Stati Uniti occidentali | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Stati Uniti orientali |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Configurare le impostazioni di rete virtuale classiche hello

In questa sezione si crea hello locale (sito locale) di rete e gateway di rete virtuale hello per una rete virtuale classica. Se si dispone di una rete virtuale classica e si eseguono questi passaggi come esercizio, è possibile creare una rete virtuale utilizzando [questo articolo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) hello e [esempio](#values) i valori delle impostazioni dall'alto.

Quando si utilizza hello portale toocreate una rete virtuale classica, è necessario passare il pannello di rete virtuale toohello mediante hello seguendo i passaggi, altrimenti hello opzione toocreate una rete virtuale classica non è presente:

1. Fare clic su hello blade di 'New' hello tooopen '+'.
2. Nel campo "Marketplace hello ricerca" hello, digitare 'Rete virtuale'. Se si seleziona, invece, di rete -> rete virtuale, non sarà possibile ricevere hello opzione toocreate una rete virtuale classica.
3. Individuare 'Rete virtuale' da hello restituito l'elenco e scegliere Pannello di tooopen hello rete virtuale. 
4. Nel Pannello di rete virtuale hello, selezionare 'Classico' toocreate una rete virtuale classica. 

Se si dispone già di una rete virtuale con un gateway VPN, verificare che gateway hello è dinamica. Se è statico, è innanzitutto necessario eliminare il gateway VPN hello, quindi continuare.

Gli screenshot sono forniti come esempio. Essere tooreplace che i valori hello con valori personalizzati oppure utilizzare hello [esempio](#values) valori.

### <a name="part-1---configure-hello-local-site"></a>Parte 1 - configurare il sito locale hello

Aprire hello [portale di Azure](https://ms.portal.azure.com) e accedere con l'account di Azure.

1. Passare troppo**tutte le risorse** e individuare hello **ClassicVNet** nell'elenco di hello.
2. In hello **Panoramica** pannello in hello **le connessioni VPN** fare clic su hello **Gateway** toocreate grafica un gateway.

    ![Configurare un gateway VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configurare un gateway VPN")
3. In hello **nuova connessione VPN** pannello per **tipo di connessione**selezionare **Site-to-site**.
4. In **Sito locale** fare clic su **Configurare le impostazioni necessarie**. Verrà visualizzata hello **sito locale** blade.
5. In hello **sito locale** pannello, creare un toohello toorefer nome VNet Gestione risorse. ad esempio "RMVNetLocal".
6. Se il gateway VPN hello per Gestione risorse VNet hello dispone già di un indirizzo IP pubblico, è possibile utilizzare il valore di hello per hello **indirizzo IP del gateway VPN** campo. Se si stanno eseguendo questi passaggi come esercizio o non si dispone ancora di un gateway di rete virtuale per la rete virtuale di Resource Manager, è possibile creare un indirizzo IP segnaposto. Verificare che l'indirizzo IP segnaposto hello venga utilizzato un formato valido. In un secondo momento, sostituire l'indirizzo IP segnaposto hello con indirizzo IP pubblico del gateway di rete virtuale di gestione risorse hello hello.
7. Per **spazio degli indirizzi Client**, utilizzare i valori hello per spazi di indirizzi IP di rete virtuale di hello per hello VNet Gestione risorse. Questa impostazione è utilizzata toospecify hello indirizzo spazi tooroute toohello Gestione risorse rete virtuale.
8. Fare clic su **OK** toosave hello valori e restituiscono toohello **nuova connessione VPN** blade.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Parte 2 - creare un gateway di rete virtuale hello

1. In hello **nuova connessione VPN** blade, seleziona hello **crea gateway immediatamente** casella di controllo e fare clic su **configurazione del gateway facoltativo** tooopen hello  **Configurazione del gateway** blade. 

    ![Aprire il pannello Configurazione gateway](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Aprire il pannello Configurazione gateway")
2. Fare clic su **Subnet - configurare le impostazioni necessarie** tooopen hello **aggiungere subnet** blade. Hello **nome** è già configurato con il valore richiesto hello **GatewaySubnet**.
3. Hello **intervallo di indirizzi** fa riferimento toohello intervallo per la subnet del gateway hello. Sebbene sia possibile creare una subnet del gateway con un intervallo di indirizzi /29 (3 indirizzi), è consigliabile creare una subnet del gateway che contiene più indirizzi IP. Questo la rende compatibile con configurazioni future che potrebbero richiedere più indirizzi IP disponibili. Se possibile, usare /27 o /28. Se si utilizza questa procedura come esercizio, è possibile fare riferimento toohello [esempio](#values) valori. Fare clic su **OK** subnet del gateway toocreate hello.
4. In hello **configurazione del Gateway** pannello **dimensioni** fa riferimento il gateway toohello SKU. Selezionare il gateway hello SKU per il gateway VPN.
5. Verificare hello **tipo di Routing** è **dinamica**, quindi fare clic su **OK** tooreturn toohello **nuova connessione VPN** blade.
6. In hello **nuova connessione VPN** pannello, fare clic su **OK** toobegin creazione gateway VPN. Creazione di un gateway VPN può richiedere too45 minuti toocomplete.

### <a name="ip"></a>Parte 3 - gateway di rete virtuale hello copia indirizzo IP pubblico

Dopo aver creato il gateway di rete virtuale hello, è possibile visualizzare l'indirizzo IP del gateway hello. 

1. Passare tooyour classico rete virtuale e fare clic su **Panoramica**.
2. Fare clic su **le connessioni VPN** blade di connessioni VPN hello tooopen. Nel Pannello di connessioni VPN hello, è possibile visualizzare l'indirizzo IP pubblico hello. Questo è l'indirizzo IP pubblico hello assegnato tooyour gateway di rete virtuale. 
3. Annotare o copiare l'indirizzo IP hello. Sarà necessario nei passaggi successivi quando si useranno le impostazioni di configurazione del gateway di rete locale di Resource Manager. È anche possibile visualizzare lo stato di hello le connessioni di gateway di. Sito di rete locale hello di notifica creato viene elencato come 'Connessione'. Hello stato viene modificato dopo aver creato le connessioni.
4. Chiudere il pannello di hello dopo la copia di indirizzo IP del gateway hello.

## <a name="rmvnet"></a>2. Configurare le impostazioni di rete virtuale di gestione risorse di hello

In questa sezione viene creato il gateway di rete virtuale hello e gateway di rete locale hello per VNet il gestore delle risorse. Se si dispone di un gestore delle risorse di VNet e si eseguono questi passaggi come esercizio, è possibile creare una rete virtuale utilizzando [questo articolo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) hello e [esempio](#values) i valori delle impostazioni dall'alto.

Gli screenshot sono forniti come esempio. Essere tooreplace che i valori hello con valori personalizzati oppure utilizzare hello [esempio](#values) valori.

### <a name="part-1---create-a-gateway-subnet"></a>Parte 1 - Creare una subnet del gateway

Prima di creare un gateway di rete virtuale, è necessario innanzitutto subnet del gateway toocreate hello. Creare una subnet del gateway con conteggio CIDR /28 o superiore, ad esempio /27, /26 e così via.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Parte 2 - Creare un gateway di rete virtuale

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Parte 3: Creare un gateway di rete locale

gateway di rete locale Hello specifica l'intervallo di indirizzi hello e indirizzo IP pubblico hello associata a una rete virtuale classica e il gateway di rete virtuale.

Se si siano eseguendo questi passaggi come esercizio, vedere Impostazioni toothese:

| Rete virtuale | Spazio di indirizzi | Region | Si connette il sito di rete toolocal |Indirizzo IP pubblico del gateway|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Stati Uniti occidentali | RMVNetLocal (192.168.0.0/16) |indirizzo IP pubblico assegnato toohello ClassicVNet gateway Hello|
| RMVNet | (192.168.0.0/16) |Stati Uniti orientali |ClassicVNetLocal (10.0.0.0/24) |indirizzo IP pubblico assegnato toohello RMVNet gateway Hello.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Modificare le impostazioni di hello classiche rete virtuale del sito locale

In questa sezione è sostituire l'indirizzo IP di segnaposto hello utilizzato quando si specificano le impostazioni di sito locale di hello, con l'indirizzo IP del gateway VPN di gestione risorse di hello. Questa sezione Usa i cmdlet di PowerShell (SM) classici hello.

1. Nel portale di Azure hello, passare rete virtuale classica toohello.
2. Nel Pannello di hello per la rete virtuale, fare clic su **Panoramica**.
3. In hello **le connessioni VPN** sezione, fare clic sul nome del sito locale nell'elemento grafico hello hello.

    ![Connessioni VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "Connessioni VPN")
4. In hello **le connessioni VPN da sito a sito** pannello, fare clic sul nome del sito hello hello.

    ![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Nome del sito locale")
5. Nel Pannello di connessione hello per sito locale, fare clic sul nome hello di hello tooopen sito locale di hello **sito locale** blade.

    ![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Aprire il sito locale")
6. In hello **sito locale** blade, sostituire hello **indirizzo IP del gateway VPN** con indirizzo IP di hello del gateway di gestione risorse di hello.

    ![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Indirizzo IP del gateway")
7. Fare clic su **OK** tooupdate l'indirizzo IP hello.

## <a name="RMtoclassic"></a>4. Creare una connessione tooclassic Gestione risorse

In questa procedura configurare la connessione di hello da hello VNet Gestione risorse tramite rete virtuale classica toohello hello portale di Azure.

1. In **tutte le risorse**, individuare il gateway di rete locale hello. In questo esempio, il gateway di rete locale hello è **ClassicVNetLocal**.
2. Fare clic su **configurazione** e verificare che il gateway VPN hello per hello valore dell'indirizzo IP hello classic rete virtuale. Se necessario, aggiornare e quindi fare clic su **Salva**. Pannello hello Chiudi.
3. In **tutte le risorse**, fare clic su hello gateway di rete locale.
4. Fare clic su **connessioni** blade di connessioni tooopen hello.
5. In hello **connessioni** pannello, fare clic su  **+**  tooadd una connessione.
6. In hello **Aggiungi connessione** blade, connessione hello al nome. ad esempio "RMtoClassic".
7. **Da sito a sito** è già selezionato nel pannello.
8. Selezionare il gateway di rete virtuale hello che si desidera tooassociate con questo sito.
9. Creare una **chiave condivisa**. Questa chiave viene utilizzata anche nella connessione hello create dalle hello toohello di rete virtuale classica VNet Gestione risorse. È possibile generare la chiave hello o costituiscono uno. Per questo esempio è stato usato "abc123", ma è possibile e consigliabile usare un elemento più complesso.
10. Fare clic su **OK** connessione hello toocreate.

##<a name="classictoRM"></a>5. Creare connection Manager tooResource classico

Nei passaggi seguenti configurare la connessione hello da hello toohello di rete virtuale classica VNet Gestione risorse. Per questa procedura è necessario PowerShell. È possibile creare la connessione nel portale di hello. Assicurarsi di aver scaricato e installato sia hello classic (SM) e i cmdlet PowerShell di gestione risorse (RM).

### <a name="1-connect-tooyour-azure-account"></a>1. Connettersi tooyour account Azure

Aprire la console di PowerShell hello con diritti elevati e accedere tooyour account Azure. Hello seguente cmdlet richiede hello le credenziali di accesso per l'Account di Azure. Dopo l'accesso, le impostazioni dell'account vengono scaricate in modo che siano disponibili tooAzure PowerShell.

```powershell
Login-AzureRmAccount
```
   
Ottenere un elenco delle sottoscrizioni di Azure se si dispone di più di una sottoscrizione.

```powershell
Get-AzureRmSubscription
```

Specificare una sottoscrizione di hello che si desidera toouse. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Aggiungere l'Account di Azure toouse hello classic i cmdlet di PowerShell (SM). toodo in tal caso, è possibile utilizzare hello comando seguente:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Visualizzare i valori del file di configurazione rete hello

Quando si crea una rete virtuale nel portale di Azure hello, nome completo di hello utilizzato da Azure non è visibile nel portale di Azure hello. Ad esempio, una rete virtuale denominata 'ClassicVNet' nel portale di Azure hello toobe visualizzato potrebbe essere un nome molto più nel file di configurazione di rete hello. Hello nome potrebbe essere simile al seguente: 'Gruppo ClassicRG ClassicVNet'. In questa procedura è scaricare hello rete file e Visualizza hello i valori di configurazione.

Creare una directory sul computer e quindi esportare la directory toohello hello rete configurazione file. In questo esempio, file di configurazione di rete hello è tooC:\AzureNet esportato.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Aprire il file hello con un nome di hello editor e visualizzare il testo per una rete virtuale classica. Utilizzare nomi di hello nel file di configurazione di rete hello durante l'esecuzione dei cmdlet di PowerShell.

- I nomi delle reti virtuali sono elencati come **Nome VirtualNetworkSite =**
- I nomi dei siti sono elencati come **Nome LocalNetworkSite =**

### <a name="3-create-hello-connection"></a>3. Creare una connessione hello

Impostare la chiave condivisa hello e creare la connessione hello da hello toohello di rete virtuale classica VNet Gestione risorse. È possibile impostare una chiave condivisa di hello tramite il portale di hello. Assicurarsi di eseguire questi passaggi mentre si è connessi con versione classica di hello di hello i cmdlet di PowerShell. toodo in tal caso, utilizzare **Add-AzureAccount**. In caso contrario, non sarà in grado di tooset hello '-AzureVNetGatewayKey'.

- In questo esempio, **- VNetName** nome hello di hello classic rete virtuale come trovato nel file di configurazione di rete. 
- Hello **- LocalNetworkSiteName** viene specificato per il sito locale hello, come nome di hello trovato nel file di configurazione di rete.
- Hello **- SharedKey** è un valore che si generano e si specifica. Per questo esempio è stato usato *abc123*, ma è possibile generare un elemento più complesso. Hello importante cosa è il valore di hello specificato qui deve essere hello che stesso valore specificato durante la creazione della connessione tooclassic Gestione risorse.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Verificare le connessioni

È possibile verificare che le connessioni utilizzando hello portale di Azure o PowerShell. Quando si verifica, potrebbe essere necessario toowait uno o due minuti come connessione hello viene creato. Quando una connessione ha esito positivo, lo stato di connettività hello cambia da too'Connected 'Connessione' '.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>connessione hello tooverify il classico tooyour di rete virtuale VNet Gestione risorse

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>connessione hello tooverify il tooyour VNet Gestione risorse di rete virtuale classica

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
