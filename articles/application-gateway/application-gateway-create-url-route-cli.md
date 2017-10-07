---
title: regole di un gateway applicazione utilizzando l'URL di routing - aaaCreate 2.0 CLI di Azure | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure utilizzando le regole di routing di URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Creare un gateway applicazione con il routing basato sul percorso con l'interfaccia della riga di comando di Azure 2.0

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-url-route-cli.md)

Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello di una richiesta Http. Controlla se è presente un pool di back-end tooa route configurati per l'URL di hello presentati in Gateway applicazione hello e invia toohello il traffico di rete hello è definito il pool back-end. Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.

Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola. Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting. Tipo di regola di base fornisce servizio round robin per hello back-end pool inoltre PathBasedRouting durante la distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end hello.

## <a name="scenario"></a>Scenario

Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: un pool di server predefinito e un pool di server di immagine.

Sono richieste per http://contoso.com/image * indirizzato il pool di server tooimage (imagesBackendPool), se hello il modello del percorso non corrisponde, viene selezionato un pool di server predefinito (appGatewayBackendPool).

![route dell'URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Accedi tooAzure

Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso. 

```azurecli
az login -u "username"
```

> [!NOTE]
> È inoltre possibile utilizzare `az login` senza l'opzione per l'accesso di dispositivo che richiede l'immissione di un codice di aka.ms/devicelogin hello.

Una volta digitato hello sopra riportato, viene fornito un codice. Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.

![Comando che illustra l'accesso al dispositivo][1]

Nel browser hello immettere codice hello ricevuto. Si è reindirizzato tooa nella pagina di accesso.

![codice tooenter browser][2]

Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.

![Accesso eseguito][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Aggiungere un gateway di applicazione esistente tooan regola basata sul percorso

Creare un gateway applicazione con una regola di percorso personalizzata

### <a name="create-a-new-back-end-pool"></a>Creare un nuovo pool back-end

Configurare impostazioni del gateway applicazione **imagesBackendPool** hello con bilanciamento del carico del traffico di rete nel pool back-end hello. In questo esempio, configurare le impostazioni del pool back-end diverso per il nuovo pool back-end di hello. Ogni pool back-end può avere un'impostazione del pool back-end dedicata.  Le impostazioni HTTP back-end vengono utilizzate per i membri del pool back-end corretto toohello traffico tooroute regole. Questo parametro determina il protocollo di hello e la porta utilizzata durante l'invio di traffico toohello i membri del pool back-end. Sessioni basate su cookie sono determinate anche dalle impostazioni HTTP back-end di hello.  Se abilitata, l'affinità di sessione basato su cookie invia traffico toohello stesso back-end come richieste precedenti per ogni pacchetto.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Creare una nuova porta front-end

Configurare hello porta front-end per un gateway applicazione. oggetto di configurazione di Hello porta front-end viene utilizzato un toodefine listener cosa porta hello Gateway applicazione è in attesa del traffico listener hello.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Creare un nuovo listener

Configurare il listener di hello. Questo passaggio consente di configurare il listener hello per l'indirizzo IP pubblico hello e la porta utilizzata tooreceive il traffico di rete in ingresso. Hello di esempio seguente accetta la configurazione IP front-end hello configurato in precedenza, la configurazione della porta front-end e un protocollo (http o https) e configura il listener hello. In questo esempio, il listener hello è in ascolto tooHTTP traffico sulla porta 82 hello indirizzo IP pubblico è stato creato in precedenza.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Creare una mappa del percorso Url hello

Configurare i percorsi di regola di URL per il pool di back-end hello. Questo passaggio consente di configurare un percorso di hello utilizzato dal gateway toodefine hello mapping tra il percorso URL e il pool back-end viene assegnato il traffico in ingresso di toohandle hello.

> [!IMPORTANT]
> Ogni percorso deve iniziare con / e hello solo un "\*" è consentita, al fine di hello. Alcuni esempi validi sono /xyz, /xyz* o /xyz/*. Hello stringa inserito toohello matcher di percorso non include alcun testo dopo hello innanzitutto "?" o "#" e tali caratteri non consentiti. 

esempio Hello crea una regola per "/ immagini / *" percorso di routing del traffico tooback-end "imagesBackendPool". Questa regola assicura che il traffico per ciascun set di URL sia indirizzato toohello di back-end. Ad esempio, http://adatum.com/images/figure1.jpg diventa troppo "imagesBackendPool". Se il percorso di hello non corrisponde a una delle regole di percorso predefinito di hello, configurazione della mappa di hello regola percorso consente di configurare anche un pool di indirizzi back-end di predefinito. Ad esempio, http://adatum.com/shoppingcart/test.html passa toopool1 con cui è definito come il pool predefinito hello per il traffico non corrispondente.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera toolearn sull'offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
