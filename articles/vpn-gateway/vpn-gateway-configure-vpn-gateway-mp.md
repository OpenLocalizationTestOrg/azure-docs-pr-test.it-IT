---
title: 'Configurare un gateway VPN: portale di Azure classico: Azure| Microsoft Docs'
description: Questo articolo illustra come configurare la rete virtuale del gateway VPN e modificare il tipo di routing VPN del gateway. Questi passaggi sono applicabili toohello distribuzione classica modello e hello classic portale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Configurare un gateway VPN nel portale classico hello 
Se si desidera toocreate una connessione sicura tra più sedi tra Azure e il percorso locale, è necessario toocreate un gateway di rete virtuale. Un gateway VPN è un tipo specifico di gateway di rete virtuale. Nel modello di distribuzione classica hello, un gateway VPN può essere uno dei due tipi di routing VPN: statico o dinamico. Hello tipo VPN scelto dipende sia il piano di progettazione di rete e dispositivo VPN locale di hello da toouse. Per altre informazioni sui dispositivi VPN, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).

**Informazioni sui modelli di distribuzione di AzureAbout Azure deployment models**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Panoramica della configurazione
Hello passaggi seguenti consentono di configurare il gateway VPN nel portale classico hello. Questi passaggi sono applicabili toogateways per le reti virtuali create utilizzando il modello di distribuzione classica hello. Attualmente, non tutte hello impostazioni di configurazione per i gateway sono disponibili nel portale di Azure hello. In questo caso, si creerà un nuovo set di istruzioni valide toohello portale di Azure.

### <a name="before-you-begin"></a>Prima di iniziare
Prima di configurare il gateway, è innanzitutto necessario toocreate la rete virtuale. Per una rete virtuale per la connettività cross-premise toocreate di passaggi, vedere [configurare una rete virtuale con una connessione VPN site-to-site](vpn-gateway-site-to-site-create.md), o [configurare una rete virtuale con una connessione VPN point-to-site](vpn-gateway-point-to-site-create.md). Quindi, utilizzare i seguenti gateway VPN di passaggi tooconfigure hello hello e raccogliere informazioni di hello tooconfigure è necessario il dispositivo VPN. 

Se si dispone già di un gateway VPN e si desidera che il tipo di routing VPN hello toochange, vedere [come toochange hello tipo per il gateway di routing VPN](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Creare un gateway VPN
1. In hello [portale di Azure classico](https://manage.windowsazure.com), su hello **reti** pagina, verificare che la colonna Stato hello per la rete virtuale è **creato**.
2. In hello **nome** colonna, fare clic sul nome della rete virtuale hello.
3. In hello **Dashboard** pagina, si noti che questa rete virtuale non ha ancora un gateway configurato. Questo stato verrà visualizzato man mano che procede hello passaggi tooconfigure il gateway.

![Gateway non creato](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Nella parte inferiore di hello della pagina hello, quindi fare clic su **crea Gateway**. È possibile selezionare *Routing statico* o *Routing dinamico*. si seleziona il tipo di routing VPN Hello dipende da alcuni fattori. Se è necessario connessioni point-to-site toosupport, ad esempio, ciò che supporta il dispositivo VPN. Controllare [informazioni sui dispositivi VPN per la connettività di rete virtuale](vpn-gateway-about-vpn-devices.md) tooverify hello tipo di routing VPN che è necessario. Dopo aver creato il gateway di hello, è possibile modificare tra tipi di routing VPN gateway senza eliminare e ricreare il gateway hello. Quando il sistema hello chiede tooconfirm che si desidera hello gateway creato, fare clic su **Sì**.

![Tipo di routing VPN del gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Quando viene creato il gateway, si noti grafico gateway hello nella pagina hello modifiche tooyellow e afferma *creazione Gateway*. Potrebbe richiedere fino a too45 minuti per toocreate gateway hello. Attendere che il gateway hello è stato completato prima di poter proseguire con altre impostazioni di configurazione.

![Creazione del gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Quando hello modifiche gateway troppo*connessione*, è possibile raccogliere informazioni hello è necessario per il dispositivo VPN.

![Connessione del gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Connessioni Site-to-site

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Passaggio 1. Raccogliere informazioni per la configurazione del dispositivo VPN
Se si sta creando una connessione Site-to-Site, dopo aver creato il gateway di hello, raccogliere informazioni per la configurazione del dispositivo VPN. Queste informazioni si trovano in hello **Dashboard** pagina per la rete virtuale:

1. **Indirizzo IP del gateway -** indirizzo IP hello è reperibile in hello **Dashboard** pagina. Non sarà in grado di toosee fino a dopo il gateway ha terminato la creazione.
2. **Chiave condivisa -** fare clic su **Gestisci chiave** in basso hello hello. Fare clic su hello icona Avanti toohello chiave toocopy è tooyour Appunti, quindi incollare e salvare la chiave di hello. Questo pulsante funziona solo quando è presente un solo tunnel VPN Site-to-Site. Se si dispone di più tunnel VPN S2S, utilizzare hello *Get Virtual Network Gateway Shared Key* API o il cmdlet PowerShell.

![Gestisci chiave](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Passaggio 2.  Configurare il dispositivo VPN
Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN. Anche se è non fornisce i passaggi di configurazione per tutti i dispositivi VPN, è possibile trovare informazioni hello hello seguenti collegamenti utili:

- Per informazioni sui dispositivi VPN compatibili, vedere l'articolo relativo ai [dispositivi VPN](vpn-gateway-about-vpn-devices.md). 
- Per le impostazioni di configurazione toodevice di collegamenti, vedere [i dispositivi VPN convalidati](vpn-gateway-about-vpn-devices.md#devicetable). I collegamenti forniti rappresentano i migliori possibili. È sempre toocheck migliore con il produttore del dispositivo per le informazioni di configurazione più recente hello.
- Per informazioni sulla modifica degli esempi, vedere [Modifica degli esempi di configurazione di dispositivo](vpn-gateway-about-vpn-devices.md#editing).
- Per informazioni sui parametri IPsec/IKE, vedere [Parametri](vpn-gateway-about-vpn-devices.md#ipsec).
- Prima di configurare il dispositivo VPN, verificare la presenza di [noti problemi di compatibilità dei dispositivi](vpn-gateway-about-vpn-devices.md#known) per dispositivo VPN hello che si desidera toouse.

Quando si configura il dispositivo VPN, è necessario hello seguenti elementi:

- Hello indirizzo IP pubblico del gateway di rete virtuale. È possibile individuare questo accade toohello **Panoramica** pannello per la rete virtuale.
- Chiave condivisa. Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito. In questi esempi viene usata una chiave condivisa molto semplice. È necessario generare un toouse chiave più complesse.

Dopo la configurazione di dispositivo VPN hello, è possibile visualizzare le informazioni di connessione aggiornate nella pagina Dashboard hello per la rete virtuale.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Passaggio 3. Verificare gli intervalli della rete locale e l'indirizzo IP del gateway VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Verificare l'indirizzo IP del gateway VPN
Per gateway tooconnect correttamente, hello indirizzo IP per il dispositivo VPN deve essere correttamente configurato per hello rete locale specificati per la configurazione di più sedi locali. In genere, questa viene configurata durante il processo di configurazione da sito a sito hello. Tuttavia, se è usato in precedenza la rete locale con un altro dispositivo o indirizzo IP di hello è stato modificato per la rete locale, modificare hello impostazioni toospecify hello corretto indirizzo IP del Gateway.

1. tooverify l'indirizzo IP del gateway, fare clic su **reti** hello riquadro sinistro del portale e quindi selezionare **reti locali** nella parte superiore di hello della pagina hello. Si noterà hello indirizzo del Gateway VPN per ogni rete locale in cui è stato creato. indirizzo IP di hello tooedit, selezionare hello rete virtuale e fare clic su **modifica** nella parte inferiore di hello della pagina hello.
2. In hello **specificare i dettagli della rete locale** pagina, modificare l'indirizzo IP hello e fare clic sulla freccia avanti hello nella parte inferiore di hello della pagina hello.
3. In hello **specificare lo spazio degli indirizzi hello** pagina, fare clic su segno di spunta hello toosave destro inferiore hello le impostazioni.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Verificare gli intervalli di indirizzi hello per le reti locali
Per tooflow traffico corretto di hello tramite una sede hello gateway tooyour locale, è necessario tooverify che ogni intervallo di indirizzi IP sia specificato. Ciascun intervallo deve essere elencato nella configurazione delle **reti locali** di Azure. A seconda della configurazione di rete hello del percorso locale, può trattarsi di un'attività piuttosto grande. Verrà inviato il traffico associato a un indirizzo IP all'interno di intervalli hello elencato tramite gateway VPN della rete virtuale hello. gli intervalli di Hello che elencati non dispone di intervalli privati toobe, anche se sarà necessario tooverify in grado di ricevere la configurazione di on-premise hello il traffico in ingresso.

gli intervalli di hello tooadd o di modifica per una rete locale, utilizzare hello alla procedura seguente:

1. intervalli di indirizzi IP hello tooedit per una rete locale, fare clic su **reti** hello riquadro sinistro del portale e quindi selezionare **reti locali** nella parte superiore di hello della pagina hello. Nel portale di hello hello più semplice modo tooview hello intervalli elencati è hello **modifica** pagina. toosee gli intervalli, selezionare hello rete virtuale e fare clic su **modifica** nella parte inferiore di hello della pagina hello.
2. In hello **specificare i dettagli della rete locale** pagina, non apportare alcuna modifica. Fare clic sulla freccia avanti hello nella parte inferiore di hello della pagina hello.
3. In hello **specificare lo spazio degli indirizzi hello** pagina, apportare le modifiche di spazio di indirizzo di rete. Fare clic su hello segno di spunta toosave la configurazione.

## <a name="how-tooview-gateway-traffic"></a>Il traffico gateway tooview
È possibile visualizzare il gateway e il relativo traffico dalla pagina **Dashboard** della rete virtuale.

In hello **Dashboard** pagina è possibile visualizzare hello seguenti:

* quantità di Hello di dati che passano attraverso il gateway sia i dati in dati in uscita.
* nomi di Hello del server DNS hello specificati per la rete virtuale.
* connessione Hello tra il gateway e il dispositivo VPN.
* chiave che viene utilizzato tooconfigure Hello condivisa il dispositivo gateway VPN tooyour della connessione.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Come toochange hello tipo per il gateway di routing VPN
Poiché alcune configurazioni di connettività sono disponibili solo per determinati tipi di routing del gateway, è possibile che è necessario toochange hello gateway VPN tipo di routing di un gateway VPN esistente. Ad esempio, è consigliabile tooadd connettività point-to-site tooan già site-to-site connessione esistente con un gateway statico. Le connessioni Point-to-Site richiedono un gateway dinamico. Ciò significa tooconfigure una connessione P2S, è necessario toochange il tipo di routing VPN gateway da toodynamic statico.

Se è necessario un tipo di routing VPN gateway toochange, si sarà eliminare il gateway esistente hello e quindi creare un nuovo gateway con nuovo tipo di routing hello. Non è necessario toodelete hello tutta la rete virtuale toochange hello gateway tipo di routing.

Prima di modificare il tipo di routing VPN del gateway, essere tooverify assicurarsi che il dispositivo VPN supporti il tipo di routing hello che si desidera toouse. nuovi esempi configurazione routing toodownload e controllo requisiti del dispositivo VPN, vedere [informazioni sui dispositivi VPN per la connettività di rete virtuale](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Quando si elimina un gateway VPN di rete virtuale, viene rilasciata hello indirizzo VIP assegnato toohello gateway. Quando si ricrea il gateway di hello, un nuovo VIP viene assegnato tooit.
> 
> 

1. **Eliminare il gateway VPN esistente di hello.**
   
    In hello **Dashboard** pagina per la rete virtuale, passare toohello parte inferiore della pagina hello e fare clic su **Delete Gateway**. Attesa per una notifica hello hello gateway è stato eliminato. Dopo aver ricevuto la notifica di hello nella schermata di hello che il gateway è stato eliminato, è possibile creare un nuovo gateway.
2. **Creare un nuovo gateway VPN.**
   
    Utilizzare procedura hello in cima a hello hello pagina toocreate un nuovo gateway: [creare un gateway VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Passaggi successivi
È possibile aggiungere una rete virtuale tooyour di macchine virtuali. Vedere [come una macchina virtuale personalizzata toocreate](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se si desidera una connessione VPN tooconfigure una point-to-site, vedere [configurare una connessione VPN point-to-site](vpn-gateway-point-to-site-create.md).

