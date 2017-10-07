---
title: Portale di Azure - Gateway applicazione Azure - probe di aaaCreate personalizzato | Documenti Microsoft
description: Informazioni su come toocreate personalizzato probe per il Gateway applicazione tramite il portale di hello
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Crea un probe personalizzato per il Gateway applicazione tramite il portale di hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-probe-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [PowerShell per Azure classico](application-gateway-create-probe-classic-ps.md)

In questo articolo aggiungere un gateway di applicazione esistente probe personalizzato tooan tramite hello portale di Azure. Probe personalizzati sono utili per le applicazioni che dispone di una pagina di controllo di integrità specifico o per le applicazioni che non forniscono una risposta corretta in un'applicazione web predefinita hello.

## <a name="before-you-begin"></a>Prima di iniziare

Se si dispone già di un gateway di applicazioni, visitare [creare un Gateway applicazione](application-gateway-create-gateway-portal.md) toocreate un toowork di gateway applicazione con.

## <a name="createprobe"></a>Creare il probe hello

Probe vengono configurati in un processo in due passaggi tramite il portale di hello. primo passaggio Hello è di tipo probe hello toocreate. Nel secondo passaggio hello, aggiungere le impostazioni hello probe toohello back-end http di gateway applicazione hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com). Se non si dispone già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free)

1. Nel portale di Azure riquadro Preferiti hello, fare clic su tutte le risorse. Fare clic su gateway applicazione hello in hello tutti pannello risorse. Se sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere partners.contoso.net in hello filtro in base al nome... gateway applicazione hello di accesso tooeasily di casella.

1. Fare clic su **probe** e fare clic su hello **Aggiungi** pulsante tooadd un probe.

  ![Pannello Aggiungi probe con informazioni inserite][1]

1. In hello **probe di integrità Aggiungi** pannello, immettere le informazioni di hello necessario per il probe hello e al termine fare clic su **OK**.

  |**Impostazione** | **Valore** | **Dettagli**|
  |---|---|---|
  |**Nome**|customProbe|Questo valore è un probe toohello nome descrittivo che sia accessibile nel portale di hello.|
  |**Protocollo**|HTTP o HTTPS | Usa il protocollo Hello hello probe di integrità.|
  |**Host**|vale a dire contoso.com|Questo valore è nome host hello che viene utilizzato per il probe hello. Applicabile solo quando vengono configurati più siti nel gateway applicazione. In caso contrario, usare "127.0.0.1". Questo valore è diverso dal nome host della macchina virtuale hello.|
  |**Percorso**|/ o un altro percorso|resto Hello di hello l'url completo per il probe personalizzato hello. Un percorso valido inizia con "/". Per il percorso predefinito hello di http://contoso.com semplicemente utilizzare '/' |
  |**Intervallo (sec)**|30|La frequenza con cui hello probe viene eseguito toocheck per l'integrità. Non è consigliabile hello tooset inferiore a 30 secondi.|
  |**Timeout (secondi)**|30|quantità Hello di probe hello tempo di attesa prima del timeout. Hello timeout intervallo esigenze toobe sufficientemente elevato che può essere effettuata una chiamata http pagina di stato tooensure hello back-end è disponibile.|
  |**Soglia non integra**|3|Numero di errori toobe tentativi considerato non integro. Una soglia di 0 significa che se si verifica un errore di un controllo di integrità hello back-end è determinata immediatamente non integro.|

  > [!IMPORTANT]
  > nome host Hello è hello non corrisponde al nome di server. Questo valore è il nome di hello dell'host di hello virtuale in esecuzione nel server di applicazione hello. probe Hello viene inviato toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Aggiungi gateway toohello probe

Ora che hello probe è stato creato, è possibile ora tooadd è toohello gateway. Le impostazioni probe vengono impostate per le impostazioni http back-end di hello del gateway applicazione hello.

1. Fare clic su **impostazioni HTTP** gateway applicazione hello, toobring backup pannello configurazione hello scegliere hello corrente back-end http impostazioni elencate nella finestra hello.

  ![Finestra delle impostazioni HTTP][2]

1. In hello **appGatewayBackEndHttpSettings** pannello impostazioni, controllo hello **probe personalizzato utilizzare** casella di controllo e scegliere probe hello creato in hello [probe hello crea](#createprobe) sezione in hello **probe personalizzato** elenco a discesa...
Al termine, fare clic su **salvare** e vengono applicate le impostazioni di hello.

probe predefinito Hello controlla l'applicazione web di hello predefinita accesso toohello. Ora che è stato creato un probe personalizzato, gateway applicazione hello utilizza hello percorso personalizzato definito toomonitor integrità per i server back-end hello. In base ai criteri hello è definito, il gateway applicazione hello verifica percorso hello specificato in probe hello. Se una chiamata a hello toohost:Port / percorso non viene restituito HTTP 200 399 risposta con stato, il server di hello viene escluso dalla rotazione una volta raggiunta la soglia non integra hello. Individuazione tramite probe continua su hello toodetermine di istanza non integro quando diventa nuovamente integro. Dopo aver aggiunto i pool di server back-toohealthy istanza hello, traffico inizia nuovamente tooit propagazione e probe toohello istanza continuerà nell'intervallo specificato di utente come al solito.

## <a name="next-steps"></a>Passaggi successivi

toolearn tooconfigure offload SSL con Gateway applicazione Azure, vedere [configurare Offload SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

