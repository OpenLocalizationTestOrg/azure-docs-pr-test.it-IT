---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN da sito a sito (versione classica): portale | Documenti Microsoft'
description: Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questi passaggi consentono di creare una connessione Site-to-Site VPN Gateway cross-premise usando il portale di hello.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Creare una connessione Site-to-Site utilizzando hello del portale di Azure (versione classica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Questo articolo illustra come toouse hello toocreate portale Azure una connessione gateway VPN da sito a sito dal toohello di rete locale rete virtuale. passaggi di Hello in questo articolo si applicano al modello di distribuzione classica toohello. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente. Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).

![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Prima di iniziare

Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:

* Verificare che si desidera toowork nel modello di distribuzione classica hello. Se si desidera toowork nel modello di distribuzione di gestione risorse di hello, vedere [creare una connessione da sito a sito (gestione delle risorse)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Se possibile, è consigliabile utilizzare il modello di distribuzione del hello Gestione risorse.
* Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è. Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).
* Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN. L'indirizzo IP non può trovarsi dietro un NAT.
* Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente. Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour. Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.
* Attualmente, PowerShell è una chiave condivisa hello toospecify richiesto e creare una connessione al gateway VPN hello. Installare hello l'ultima versione di hello cmdlet PowerShell di gestione del servizio di Azure (SM). Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Quando si usa PowerShell per questa configurazione, assicurarsi di scegliere l'opzione Esegui come amministratore. 

### <a name="values"></a>Valori di configurazione di esempio per questo esercizio

esempi di Hello in questo articolo utilizzano hello seguenti valori. È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.

* **Nome della rete virtuale:** TestVNet1
* **Spazio di indirizzi:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (facoltativo per questo esercizio)
* **Subnet:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (facoltativo per questo esercizio)
* **GatewaySubnet:** 10.11.255.0/27
* **Gruppo di risorse:** TestRG1
* **Località:** Stati Uniti orientali
* **DNS Server:** 10.11.0.3 (facoltativo per questo esercizio)
* **Nome del sito locale:** Site2
* **Spazio degli indirizzi client:** hello spazio di indirizzi che si trova nel sito locale.

## <a name="CreatVNet"></a>1. Crea rete virtuale

Quando si crea un toouse di rete virtuale per una connessione S2S, è necessario che si sovrapponga spazi degli indirizzi hello specificati con uno qualsiasi degli spazi di indirizzi hello client per i siti locali hello che si desidera tooconnect a toomake. Se sono presenti subnet che si sovrappongono, la connessione non funziona correttamente.

* Se si dispone già di una rete virtuale, verificare che le impostazioni di hello siano compatibili con la progettazione di gateway VPN. Prestare particolare attenzione tooany subnet che si sovrappongano con altre reti. 

* Se non si ha una rete virtuale, crearne una. Gli screenshot sono forniti come esempio. Essere certi tooreplace hello i valori con valori personalizzati.

### <a name="toocreate-a-virtual-network"></a>toocreate una rete virtuale

1. Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account di Azure.
2. Fare clic su **+** In hello **marketplace hello ricerca** , digitare 'Rete virtuale'. Individuare **rete virtuale** hello restituito elenco e fare clic su hello tooopen **rete virtuale** pagina.

  ![pagina di ricerca della rete virtuale](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Nella parte inferiore di hello della pagina rete virtuale hello da hello **selezionare un modello di distribuzione** selezionare nell'elenco a discesa **classico**, quindi fare clic su **crea**.

  ![Selezionare il modello di distribuzione](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. In hello **creare network(classic) virtuale** pagina, configurare le impostazioni di rete virtuale hello. Aggiungere a questa pagina il primo spazio di indirizzi e l'intervallo di indirizzi di una subnet singola. Al termine della creazione hello rete virtuale, è possibile tornare indietro e aggiungere altre subnet e gli spazi degli indirizzi.

  ![Pagina Crea rete virtuale](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Pagina Crea rete virtuale")
5. Verificare che hello **sottoscrizione** è hello corretto. È possibile modificare le sottoscrizioni con elenco a discesa hello.
6. Fare clic su **Gruppo di risorse** e selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Selezionare quindi hello **percorso** le impostazioni per la rete virtuale. posizione di Hello determina in cui risiederà risorse hello distribuire toothis rete virtuale.
8. Se si desidera toofind in grado di toobe facilmente nel dashboard di hello una rete virtuale, selezionare **toodashboard Pin**. Fare clic su **crea** toocreate la rete virtuale.

  ![PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard Pin")
9. Dopo aver fatto clic su 'Crea', viene visualizzato un riquadro nel dashboard di hello che riflette lo stato di avanzamento hello di una rete virtuale. le modifiche apportate al riquadro Hello come hello rete virtuale viene creato.

  ![Riquadro Creazione della rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Creazione della rete virtuale")

Dopo aver creata la rete virtuale, vedere **creato** sotto **stato** nella pagina reti hello hello portale di Azure classico.

## <a name="additionaladdress"></a>2. Aggiungere altri spazi di indirizzi

Dopo aver creato la rete virtuale è possibile aggiungere altri spazi di indirizzi. Aggiunta di ulteriore spazio degli indirizzi non è una parte obbligatoria di una configurazione S2S, ma se è necessaria più spazi degli indirizzi, utilizzare hello alla procedura seguente:

1. Individuare le reti virtuali hello nel portale di hello.
2. Nella pagina di hello per la rete virtuale, in hello **impostazioni** fare clic su **lo spazio degli indirizzi**.
3. Nella pagina di spazio di indirizzo hello, fare clic su **+ Aggiungi** e immettere lo spazio di indirizzi aggiuntivi.

## <a name="dns"></a>3. Specificare un server DNS

Le impostazioni DNS non sono una parte obbligatoria di una configurazione da sito a sito, ma il servizio DNS è necessario per la risoluzione dei nomi. Se si specifica un valore, non verrà creato un nuovo server DNS. Hello indirizzo IP del server DNS specificato deve essere in grado di risolvere nomi hello per le risorse di hello a che ci si connette un server DNS. Per le impostazioni di esempio hello, è stato usato un indirizzo IP privato. indirizzo IP Hello che utilizziamo probabilmente non è in indirizzo IP di hello del server DNS. Essere toouse che i valori personalizzati.

Dopo aver creato la rete virtuale, è possibile aggiungere l'indirizzo IP hello una DNS server toohandle di risoluzione dei nomi. Aprire le impostazioni di hello per la rete virtuale, fare clic su server DNS e aggiungere l'indirizzo IP di hello del server DNS hello che si vuole toouse per la risoluzione dei nomi.

1. Individuare le reti virtuali hello nel portale di hello.
2. Nella pagina di hello per la rete virtuale, in hello **impostazioni** fare clic su **server DNS**.
3. Aggiungere un server DNS.
4. le impostazioni, fare clic su toosave **salvare** nella parte superiore di hello della pagina hello.

## <a name="localsite"></a>4. Configurare il sito locale di hello

percorso locale tooyour si riferisce solitamente da sito locale Hello. Contiene l'indirizzo IP hello del hello VPN dispositivo toowhich che si creerà una connessione e gli intervalli di indirizzi IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway.

1. Nel portale di hello passare toohello rete virtuale per cui si desidera toocreate un gateway.
2. Nella pagina di hello per la rete virtuale, sul hello **Panoramica** pagina, nella sezione relativa alle connessioni VPN hello, fare clic su **Gateway** tooopen hello **nuova connessione VPN** pagina.

  ![Fare clic su impostazioni del gateway tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "fare clic su impostazioni del gateway tooconfigure")
3. In hello **nuova connessione VPN** selezionare **Site-to-site**.
4. Fare clic su **locale del sito - configurare le impostazioni necessarie** tooopen hello **sito locale** pagina. Configurare le impostazioni di hello e quindi fare clic su **OK** impostazioni hello toosave.
  - **Nome:** creare un nome per il sito locale di toomake è più facile per si tooidentify.
  - **Indirizzo IP del gateway VPN:** questo è l'indirizzo IP pubblico hello del dispositivo VPN hello per la rete locale. dispositivo VPN Hello richiede un indirizzo IP pubblico IPv4. Specificare un indirizzo IP pubblico valido per hello toowhich dispositivo VPN desiderato tooconnect. Non può essere protetto da NAT è toobe raggiungibile da Azure. Se non si conosce indirizzo IP di hello del dispositivo VPN, è possibile inserire sempre un valore di segnaposto (fino a quando è in formato hello di un indirizzo IP pubblico valido) e quindi modificarlo in un secondo momento.
  - **Spazio degli indirizzi client:** elenco hello indirizzi IP che si desidera indirizzato toohello di rete locale tramite il gateway. È possibile aggiungere più intervalli di spazi indirizzi. Assicurarsi che non si sovrappongono intervalli hello che è possibile specificare gli intervalli di altre reti in cui a che la rete virtuale si connette o con gli intervalli di indirizzi hello della rete virtuale di hello stesso.

  ![Sito locale](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configurare il sito locale")

## <a name="gatewaysubnet"></a>5. Configurare hello subnet del gateway

È necessario creare una subnet del gateway per il gateway VPN. subnet del gateway Hello contiene indirizzi IP hello utilizzati dai servizi gateway VPN hello.

1. In hello **nuova connessione VPN** pagina, casella di controllo selezionare hello **crea gateway immediatamente**. verrà visualizzata la pagina Hello 'facoltativo configurazione del gateway'. Se non si seleziona la casella di controllo di hello, non verrà visualizzata la subnet gateway hello pagina tooconfigure hello.

  ![Configurazione gateway - Subnet, dimensioni e tipo di routing](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Configurazione gateway - Subnet, dimensioni e tipo di routing")
2. hello tooopen **configurazione del Gateway** pagina, fare clic su **configurazione del gateway facoltativo - Subnet, dimensioni e tipo di routing**.
3. In hello **configurazione del Gateway** pagina, fare clic su **Subnet - configurare le impostazioni necessarie** tooopen hello **aggiungere subnet** pagina.

  ![Configurazione gateway - Subnet gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Configurazione gateway - Subnet gateway")
4. In hello **aggiungere subnet** pagina, aggiungere la subnet gateway hello. dimensioni Hello di subnet del gateway hello specificati dipendono dalla configurazione di gateway VPN hello che si desidera toocreate. Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile utilizzare /27 o /28. In questo modo viene creata una subnet più grande che include più indirizzi. Utilizzando una subnet del gateway più grande consente sufficiente IP indirizzi tooaccommodate future configurazioni possibili.

  ![Aggiungere la subnet del gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Aggiungere la subnet del gateway")

## <a name="sku"></a>6. Specificare hello SKU e il tipo VPN

1. Gateway hello selezionare **dimensioni**. Questo è il gateway di hello SKU utilizzare toocreate il gateway di rete virtuale. Nel portale di hello hello 'Predefinito SKU' = **base**. Gateway VPN classico usare il gateway (legacy) precedente di hello SKU. Per ulteriori informazioni sul gateway legacy hello SKU, vedere [funziona con il gateway di rete virtuale SKU (SKU precedente)](vpn-gateway-about-skus-legacy.md).

  ![Selezionare il tipo SKU e di VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Selezionare il tipo SKU e di VPN")
2. Seleziona hello **tipo di Routing** per il gateway. È anche noto come tipo di VPN hello. È importante tooselect hello del gateway corretti tipo perché non è possibile convertire da un tipo tooanother gateway hello. Il dispositivo VPN deve essere compatibile con tipo di routing hello selezionato. Per altre informazioni sul tipo di VPN, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Si possono vedere gli articoli che fa riferimento too'RouteBased' e 'Basato su criteri' VPN tipi. ' Dynamic 'corrisponde too'RouteBased', 'Static' corrisponde a 'Basato su criteri'.
3. Fare clic su **OK** impostazioni hello toosave.
4. In hello **nuova connessione VPN** pagina, fare clic su **OK** nella parte inferiore di hello di hello pagina toobegin la creazione del gateway di rete virtuale. A seconda hello SKU si seleziona, è possibile richiedere too45 minuti toocreate un gateway di rete virtuale.

## <a name="vpndevice"></a>7. Configurare il dispositivo VPN

Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN. In questo passaggio viene configurato il dispositivo VPN. Quando si configura il dispositivo VPN, è necessario hello segue:

- Chiave condivisa. Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito. In questi esempi viene usata una chiave condivisa semplice. Si consiglia di generare un toouse chiave più complesse.
- Hello indirizzo IP pubblico del gateway di rete virtuale. È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Creare una connessione hello
In questo passaggio, impostare la chiave condivisa hello e creare la connessione hello. chiave di Hello è stata impostata deve essere hello stessa chiave utilizzata nella configurazione del dispositivo VPN.

> [!NOTE]
> Questo passaggio non è attualmente disponibile nel portale di Azure hello. È necessario utilizzare una versione di gestione del servizio (SM) hello di hello cmdlet di Azure PowerShell.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Passaggio 1. Connettersi tooyour account Azure

1. Aprire la console di PowerShell con diritti elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

  ```powershell
  Add-AzureAccount
  ```
2. Controllare le sottoscrizioni di hello per account hello.

  ```powershell
  Get-AzureSubscription
  ```
3. Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Passaggio 2. Impostare la chiave condivisa hello e creare la connessione hello

Quando si utilizza il modello di distribuzione classica PowerShell e hello, talvolta hello nomi di risorse nel portale di hello non sono nomi di hello hello Azure prevede toosee quando si usa PowerShell. Hello passaggi seguenti consentono di esportare hello rete configurazione file tooobtain hello valori esatti per i nomi di hello.

1. Creare una directory sul computer e quindi esportare la directory toohello hello rete configurazione file. In questo esempio, file di configurazione di rete hello è tooC:\AzureNet esportato.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Aprire file di configurazione di rete hello con un editor xml e controllare i valori hello per 'Nome LocalNetworkSite' e 'VirtualNetworkSite name'. Modificare i valori hello tooreflect di esempio hello che è necessario. Quando si specifica un nome che contiene spazi, utilizzare le virgolette singole per racchiudere valori hello.

3. Impostare la chiave condivisa hello e creare hello connessione. Hello '-SharedKey' è un valore che si generano e si specifica. Nell'esempio hello, abbiamo utilizzato "abc123", ma è possibile generare (e consigliabile) utilizzare un nome più complesse. Hello importante cosa è il valore di hello specificato qui deve essere hello che stesso valore specificato quando si configura il dispositivo VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Quando viene creata la connessione hello, hello risulta: **stato: ha esito positivo**.

## <a name="verify"></a>9. Verificare la connessione

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Se si sono verificati problemi di connessione, vedere hello **Troubleshoot** sezione del sommario di hello nel riquadro di sinistra hello.

## <a name="reset"></a>Come tooreset un gateway VPN

La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito. In questo caso, i dispositivi VPN locali sono tutte le funzioni correttamente, ma sono tooestablish non è possibile tunnel IPsec con gateway VPN di Azure hello. Per la procedura da seguire, vedere [Reimpostare un gateway VPN](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Come toochange un SKU di gateway

Per hello passaggi toochange un SKU di gateway, vedere [ridimensionare un gateway SKU](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Passaggi successivi

* Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-about-forced-tunneling.md).