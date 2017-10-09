---
title: 'Creare una connessione tra reti virtuali: versione classica: portale di Azure | Microsoft Docs'
description: "La modalità di reti di tooconnect virtuali di Azure utilizzando PowerShell e hello portale di Azure classico."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Configurare una connessione da rete virtuale a rete virtuale (versione classica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali. Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni. passaggi di Hello in questo articolo si applicano al modello di distribuzione classica toohello e hello portale di Azure. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connettersi tra modelli di distribuzione diversi - Portale di Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connettersi tra modelli di distribuzione diversi - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Rete virtuale tooVNet diagramma di connettività](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Informazioni sulla connessione da rete virtuale a rete virtuale

La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale nel modello di distribuzione classica hello tramite un gateway VPN è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE.

reti virtuali connesse Hello può trovarsi in diverse sottoscrizioni e aree geografiche diverse. È possibile combinare la comunicazione di rete virtuale tooVNet con configurazioni multisito. Questo permette di definire topologie di rete che consentono di combinare la connettività cross-premise con la connettività tra reti virtuali.

![Rete virtuale tooVNet connessioni](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Perché connettere reti virtuali?

Si consiglia le reti virtuali tooconnect per hello seguenti motivi:

* **Presenza e ridondanza in più aree geografiche**

  * È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.
  * Con Azure Load Balancer e una tecnologia di clustering Microsoft o di terze parti, è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure. Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.
* **Applicazioni multi livello in singole aree geografiche con alto grado di isolamento**

  * Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse, con un isolamento forte e comunicazione tra livelli sicura.
* **Comunicazione tra sottoscrizioni e organizzazioni in Azure**

  * Se si dispone di più sottoscrizioni di Azure, si possono connettere tra loro i carichi di lavoro di sottoscrizioni diverse in modo sicuro tra reti virtuali.
  * Per le aziende o i provider di servizi, è ora possibile abilitare la comunicazione tra organizzazioni con tecnologia VPN sicura in Azure.

Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere [considerazioni per rete virtuale a](#faq) alla fine di hello di questo articolo.

### <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare questo esercizio, scaricare e installare hello l'ultima versione di hello cmdlet PowerShell di gestione del servizio di Azure (SM). Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Utilizziamo portale hello per la maggior parte dei passaggi di hello, ma è necessario utilizzare PowerShell toocreate hello connessioni tra reti virtuali hello. È possibile creare connessioni hello utilizzando hello portale di Azure.

## <a name="plan"></a>Passaggio 1: Pianificare gli intervalli di indirizzi IP

È importante toodecide gli intervalli di hello che userai tooconfigure le reti virtuali. Per questa configurazione, è necessario assicurarsi che nessuno degli intervalli di rete virtuale si sovrappongono reciprocamente o con reti hello locale che si connettono a.

Hello nella tabella seguente viene illustrato un esempio di toodefine le reti virtuali. Usare gli intervalli hello come linea guida solo. Annotare gli intervalli hello per le reti virtuali. Queste informazioni sono necessarie per i passaggi successivi.

**Esempio**

| Rete virtuale | Spazio di indirizzi | Region | Si connette il sito di rete toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Stati Uniti orientali |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Stati Uniti occidentali |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Passaggio 2: creare hello reti virtuali

Creare due reti virtuali in hello [portale di Azure](https://portal.azure.com). Per le reti virtuali classiche toocreate i passaggi hello, vedere [creare una rete virtuale classica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Quando si utilizza hello portale toocreate una rete virtuale classica, è necessario passare il pannello di rete virtuale toohello mediante hello seguendo i passaggi, altrimenti hello opzione toocreate una rete virtuale classica non è presente:

1. Fare clic su hello blade di 'New' hello tooopen '+'.
2. Nel campo "Marketplace hello ricerca" hello, digitare 'Rete virtuale'. Se si seleziona, invece, di rete -> rete virtuale, non sarà possibile ricevere hello opzione toocreate una rete virtuale classica.
3. Individuare 'Rete virtuale' da hello restituito l'elenco e scegliere Pannello di tooopen hello rete virtuale. 
4. Nel Pannello di rete virtuale hello, selezionare 'Classico' toocreate una rete virtuale classica. 

Se si utilizza questo articolo come esercizio, è possibile utilizzare i seguenti valori di esempio hello:

**Valori per TestVNet1**

Nome: TestVNet1<br>
Spazio di indirizzi: 10.11.0.0/16, 10.12.0.0/16 (facoltativo)<br>
Subnet name: predefinito<br>
Intervallo di indirizzi subnet: 10.11.0.1/24<br>
Gruppo di risorse: ClassicRG<br>
Location: Stati Uniti orientali<br>
GatewaySubnet: 10.11.1.0/27

**Valori per TestVNet4**

Nome: TestVNet4<br>
Spazio di indirizzi: 10.41.0.0/16, 10.42.0.0/16 (facoltativo)<br>
Subnet name: predefinito<br>
Intervallo di indirizzi subnet: 10.41.0.1/24<br>
Gruppo di risorse: ClassicRG<br>
Località: Stati Uniti occidentali<br>
GatewaySubnet: 10.41.1.0/27

**Quando si creano le reti virtuali, tenere hello ricordare le impostazioni seguenti:**

* **Spazi di indirizzi di rete virtuale** : nella pagina di spazi di indirizzi di rete virtuale hello, specificare l'intervallo di indirizzi hello che si desidera toouse per la rete virtuale. Si tratta di indirizzi IP dinamici hello che verranno assegnati le macchine virtuali toohello e altre istanze del ruolo da distribuire toothis di rete virtuale.<br>indirizzo Hello spazi selezionato non possono sovrapporsi con spazi degli indirizzi di hello per le hello altre posizioni in locale o le reti virtuali connessi a questa rete virtuale.

* **Indirizzo** : quando si crea una rete virtuale viene associata a una località di Azure (area). Ad esempio, se si desidera che le macchine virtuali che sono distribuiti tooyour toobe di rete virtuale che si trova fisicamente negli Stati Uniti occidentali, selezionare tale posizione. È possibile modificare il percorso di hello associato alla rete virtuale dopo averla creata.

**Dopo aver creato le reti virtuali, è possibile aggiungere hello seguenti impostazioni:**

* **Lo spazio degli indirizzi** : ulteriore spazio degli indirizzi non è necessaria per questa configurazione, ma è possibile aggiungere ulteriore spazio degli indirizzi dopo la creazione di hello rete virtuale.

* **Subnet** : non sono necessarie per la configurazione di altre subnet, ma potrebbe essere necessario toohave le macchine virtuali in una subnet separata dalle altre istanze del ruolo.

* **I server DNS** – immettere nome hello del server DNS e indirizzo IP. Questa impostazione non comporta la creazione di un server DNS. Consente i server DNS di hello toospecify che si vuole toouse per la risoluzione dei nomi per la rete virtuale.

In questa sezione del tipo di connessione di hello sito locale hello, configurare e creare hello gateway.

## <a name="localsite"></a>Passaggio 3: configurare il sito locale di hello

Specificare le impostazioni di hello Azure vengono utilizzati in ogni toodetermine del sito di rete locale come tooroute il traffico tra reti virtuali hello. Ogni rete virtuale deve puntare toohello rispettiva rete locale che si desideri tooroute il traffico. Determinare il nome di hello desiderato toouse toorefer tooeach sito della rete locale. È un nome descrittivo di toouse migliore.

Ad esempio, TestVNet1 connette tooa rete locale di un sito denominato 'VNet4Local'. le impostazioni di Hello per VNet4Local contengono i prefissi di indirizzo hello per TestVNet4.

Hello locale del sito per ogni rete virtuale è hello altra rete virtuale. Hello valori di esempio seguente viene utilizzata per la configurazione:

| Rete virtuale | Spazio di indirizzi | Region | Si connette il sito di rete toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Stati Uniti orientali |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Stati Uniti occidentali |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Individuare TestVNet1 nel portale di Azure hello. In hello **le connessioni VPN** sezione del pannello hello, fare clic su **Gateway**.

    ![Nessun gateway](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. In hello **nuova connessione VPN** selezionare **Site-to-Site**.
3. Fare clic su **sito locale** tooopen hello pagina del sito locale e configurare le impostazioni di hello.
4. In hello **sito locale** pagina, assegnare il nome del sito locale. In questo esempio, si nome sito locale hello 'VNet4Local'.
5. Per **Indirizzo IP del gateway VPN** è possibile usare qualsiasi indirizzo IP desiderato, purché abbia un formato valido. In genere, si utilizzerebbe hello effettivo l'indirizzo IP esterno per un dispositivo VPN. Tuttavia, per una configurazione di rete virtuale a classico, si Usa indirizzo IP pubblico hello assegnato toohello gateway per la rete virtuale. Dato che il gateway di rete virtuale hello non ancora creata, specificare qualsiasi indirizzo IP pubblico valido come segnaposto.<br>Non lasciare vuoto questo campo, poiché per questa configurazione non è un valore facoltativo. In un passaggio successivo, si torna in queste impostazioni e configurare gli indirizzi IP gateway hello corrispondenti rete virtuale dopo Azure che genera l'errore.
6. Per **spazio degli indirizzi Client**, utilizzare lo spazio di indirizzo hello di hello altra rete virtuale. Fare riferimento tooyour pianificazione di esempio. Fare clic su **OK** toosave restituito toohello indietro e impostazioni **nuova connessione VPN** blade.

    ![sito locale](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Passaggio 4: creare il gateway di rete virtuale hello

Ogni rete virtuale deve essere un gateway di rete virtuale. gateway di rete virtuale Hello instrada e crittografa il traffico.

1. In hello **nuova connessione VPN** blade, casella di controllo selezionare hello **crea gateway immediatamente**.
2. Fare clic su **Subnet, dimensioni e tipo di routing**. In hello **configurazione del Gateway** pannello, fare clic su **Subnet**.
3. nome della subnet gateway Hello viene inserito automaticamente con il nome richiesto hello 'GatewaySubnet'. Hello **intervallo di indirizzi** contiene indirizzi IP hello allocati toohello servizi di gateway VPN. Alcune configurazioni consentono una subnet del gateway di /29, ma la migliore toouse un /28 o /27 configurazioni future tooaccommodate che potrebbero richiedere più indirizzi IP per il servizio gateway hello. Nelle impostazioni di esempio viene usato 10.11.1.0/27. Modificare lo spazio degli indirizzi di hello, e quindi fare clic su **OK**.
4. Configurare hello **dimensioni Gateway**. Questa impostazione si riferisce toohello [SKU di Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Configurare hello **tipo di Routing**. Hello il tipo di routing per questa configurazione deve essere **dinamica**. È possibile modificare il tipo di routing hello in un secondo momento, a meno che non si chiudono gateway hello e crearne uno nuovo.
6. Fare clic su **OK**.
7. In hello **nuova connessione VPN** pannello, fare clic su **OK** toobegin creazione gateway della rete virtuale hello. Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU.

## <a name="vnet4settings"></a>Passaggio 5: Configurare le impostazioni di TestVNet4

Ripetere i passaggi di hello troppo[creare un sito locale](#localsite) e [gateway di rete virtuale crea hello](#gw) tooconfigure TestVNet4, sostituendo i valori hello quando necessario. Se si eseguono come esercizio, utilizzare hello [valori di esempio](#vnetvalues).

## <a name="updatelocal"></a>Passaggio 6: aggiornamento di siti locali hello

Dopo aver creato il gateway di rete virtuale per entrambe le reti virtuali, è necessario regolare i siti locali hello **indirizzo IP del gateway VPN** valori.

|Nome della rete virtuale|Sito collegato|Indirizzo IP del gateway|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|Indirizzo IP del gateway VPN per TestVNet4|
|TestVNet4|VNet1Local|Indirizzo IP del gateway VPN per TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Parte 1 - Get hello rete virtuale pubblico indirizzo IP del gateway

1. Individuare la rete virtuale nel portale di Azure hello.
2. Fare clic su tooopen hello rete virtuale **Panoramica** blade. Nel pannello hello in **le connessioni VPN**, è possibile visualizzare l'indirizzo IP hello per il gateway di rete virtuale.

  ![IP pubblico](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Copia l'indirizzo IP hello. Verrà utilizzato nella sezione successiva hello.
4. Ripetere questi passaggi per TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Parte 2: modificare i siti locali hello

1. Individuare la rete virtuale nel portale di Azure hello.
2. Nella rete virtuale hello **Panoramica** pannello, fare clic su sito locale hello.

  ![Sito locale creato](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. In hello **le connessioni VPN da sito a sito** pannello, fare clic sul nome del sito locale di hello che si desidera toomodify hello.

  ![Aprire il sito locale](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Fare clic su hello **sito locale** che si desidera toomodify.

  ![modifica del sito](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Hello aggiornamento **indirizzo IP del gateway VPN** e fare clic su **OK** impostazioni hello toosave.

  ![IP del gateway](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Chiudere hello altri pannelli.
7. Ripetere questi passaggi per TestVNet4.

## <a name="getvalues"></a>Passaggio 7 - recuperare i valori da file di configurazione di rete hello

Quando si creano reti virtuali classiche in hello portale di Azure, non nome hello da visualizzare è nome completo di hello che si usa per PowerShell. Ad esempio, una rete virtuale che viene visualizzato toobe denominato **TestVNet1** nel portale di hello, potrebbe essere un nome molto più nel file di configurazione di rete hello. Hello nome potrebbe essere simile al seguente: **gruppo ClassicRG TestVNet1**. Quando si creano le connessioni, è importante toouse i valori di hello presente nel file di configurazione di rete hello.

In hello alla procedura seguente, verrà effettuata la connessione tooyour account Azure e scaricare e visualizzare hello di tooobtain file di configurazione di hello rete valori che sono necessari per le connessioni.

1. Scaricare e installare una versione più recente di hello di hello cmdlet PowerShell di gestione del servizio di Azure (SM). Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

2. Aprire la console di PowerShell con diritti elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

  ```powershell
  Login-AzureRmAccount
  ```

  Controllare le sottoscrizioni di hello per account hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Successivamente, utilizzare hello seguente cmdlet tooadd tooPowerShell la sottoscrizione di Azure per il modello di distribuzione classica hello.

  ```powershell
  Add-AzureAccount
  ```
3. Esportare e visualizzare file di configurazione di rete hello. Creare una directory sul computer e quindi esportare la directory toohello hello rete configurazione file. In questo esempio, file di configurazione di rete hello esportata troppo**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Aprire il file hello con nomi di hello editor e visualizzare un testo per le reti virtuali e siti. Questi saranno il nome di hello da usare quando si creano le connessioni.<br>I nomi delle reti virtuali sono elencati come **Nome VirtualNetworkSite =**<br>I nomi dei siti sono elencati come **Nome LocalNetworkSiteRef =**

## <a name="createconnections"></a>Passaggio 8 - creare hello connessioni gateway VPN

Dopo aver completati tutti i passaggi precedenti hello, è possibile impostare chiavi hello IPsec/IKE già condivise e creare la connessione hello. Questa procedura usa PowerShell. Le connessioni di rete virtuale a per il modello di distribuzione classica hello non possono essere configurate in hello portale di Azure.

Negli esempi di hello, si noti che hello chiave condivisa è esattamente hello stesso. chiave condivisa Hello deve sempre corrispondere. Essere tooreplace che i valori hello in questi esempi con i nomi esatti hello per le reti virtuali e siti di rete locale.

1. Creare hello TestVNet1 tooTestVNet4 connessione.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Creare hello TestVNet4 tooTestVNet1 connessione.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Attendere tooinitialize connessioni hello. Una volta gateway hello è inizializzato, hello lo stato è 'Riuscito'.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Considerazioni sulle connessioni tra reti virtuali per le reti virtuali classiche
* reti virtuali di Hello possono trovarsi in hello sottoscrizioni uguale o diverse.
* reti virtuali di Hello possono trovarsi in hello uguali o diverse aree di Azure (posizioni).
* Un servizio cloud o un endpoint di bilanciamento del carico non può estendersi tra reti virtuali, anche se sono connesse tra loro.
* Per il collegamento di più reti virtuali non sono necessari dispositivi VPN.
* VNet to VNet supporta la connessione di reti virtuali di Azure. Non supporta le macchine virtuali o servizi cloud che non sono distribuiti tooa di rete virtuale.
* Per la connessione da rete virtuale a rete virtuale sono necessari gateway con routing dinamico. I gateway con routing statico di Azure non sono supportate.
* La connettività di rete virtuale può essere usata contemporaneamente con VPN multisito, È un massimo di 10 tunnel VPN per un gateway VPN di rete virtuale connessione tooeither altre reti virtuali o siti locali.
* Hello spazi degli indirizzi di reti virtuali hello locali e siti di rete locale non devono sovrapporsi. Spazi di indirizzi sovrapposti causerà la creazione di hello di reti virtuali o caricamento toofail di file di configurazione netcfg.
* Non sono supportati tunnel ridondanti tra una coppia di reti virtuali.
* Tutti i tunnel VPN per rete virtuale, tra cui le reti VPN P2S hello hello larghezza di banda per il gateway VPN hello e condividere hello stesso VPN gateway tempi di attività contratto di servizio in Azure.
* Il traffico di rete virtuale a viaggia attraverso hello backbone di Azure.

## <a name="next-steps"></a>Passaggi successivi
Verificare le connessioni. Vedere [Verificare una connessione di Gateway VPN](vpn-gateway-verify-connection-resource-manager.md).
