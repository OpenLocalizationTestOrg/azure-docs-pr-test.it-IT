---
title: la compressione dei file aaaTroubleshooting nella rete CDN di Azure | Documenti Microsoft
description: Risolvere i problemi relativi alla compressione di file nella rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Risoluzione dei problemi della compressione dei file CDN
Questo articolo consente di risolvere i problemi relativi alla [compressione dei file CDN](cdn-improve-performance.md).

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.

## <a name="symptom"></a>Sintomo
La compressione per l'endpoint è abilitata, ma i file vengono restituiti non compressi.

> [!TIP]
> toocheck se vengono restituiti i file compressi, è necessario uno strumento come toouse [Fiddler](http://www.telerik.com/fiddler) del browser o [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Intestazioni della risposta HTTP hello controllo restituito con memorizzati nella cache della rete CDN in contenuto.  Se è presente un'intestazione denominata `Content-Encoding` con un valore **gzip**, **bzip2** o **deflate**, il contenuto è compresso.
> 
> ![Intestazione Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Causa
Le cause possono essere diverse, ad esempio:

* Hello richiesto contenuto non è idoneo per la compressione.
* La compressione non è abilitata per hello il tipo di file richiesto.
* Hello HTTP richiesta non include un'intestazione di richiesta di un tipo di compressione valido.

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi
> [!TIP]
> Come distribuire i nuovi endpoint, le modifiche alla configurazione della rete CDN richiedere alcune toopropagate ora tramite rete hello.  In genere, le modifiche vengono applicate entro 90 minuti.  Se si tratta di hello prima di che aver configurato la compressione per l'endpoint CDN, è consigliabile in attesa che le impostazioni di compressione hello siano propagate POP toohello toobe di 1-2 ore. 
> 
> 

### <a name="verify-hello-request"></a>Verificare una richiesta di hello
In primo luogo, eseguire una verifica dell'integrità di rapido su richiesta hello.  È possibile utilizzare il browser [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) hello tooview le richieste effettuate.

* Verificare che la richiesta hello viene inviata tooyour URL dell'endpoint, `<endpointname>.azureedge.net`e non all'origine.
* Verificare che la richiesta di hello contiene un **Accept-Encoding** intestazione, hello e il valore per l'intestazione contiene **gzip**, **deflate**, o **bzip2** .

> [!NOTE]
> I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.
> 
> 

![Intestazioni di richiesta CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Verificare le impostazioni di compressione (profilo di rete CDN Standard)
> [!NOTE]
> Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Standard di Azure fornita da Verizon** o di **rete CDN Standard di Azure fornita da Akamai**. 
> 
> 

Passare l'endpoint tooyour hello [portale di Azure](https://portal.azure.com) e fare clic su hello **configura** pulsante.

* Verificare se la compressione è abilitata.
* Verificare il tipo MIME hello per hello contenuto toobe compresso è incluso nell'elenco di hello dei formati compressi.

![Impostazioni di compressione CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Verificare le impostazioni di compressione (profilo di rete CDN Premium)
> [!NOTE]
> Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Premium di Azure fornita da Verizon** .
> 
> 

Passare l'endpoint tooyour hello [portale di Azure](https://portal.azure.com) e fare clic su hello **Gestisci** pulsante.  verrà aperto il portale supplementare di Hello.  Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.  Fare clic su **Compressione**. 

* Verificare se la compressione è abilitata.
* Verificare hello **tipi di File** elenco contiene un elenco delimitato da virgole (senza spazi) di tipi MIME.
* Verificare il tipo MIME hello per hello contenuto toobe compresso è incluso nell'elenco di hello dei formati compressi.

![Impostazioni di compressione CDN premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Verificare il contenuto di hello è memorizzato nella cache
> [!NOTE]
> Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).
> 
> 

Utilizzando gli strumenti di sviluppo del browser, verificare hello risposta intestazioni tooensure hello memorizzato nell'area di hello in cui viene richiesto.

* Controllare hello **Server** intestazione della risposta.  intestazione Hello deve avere il formato di hello **piattaforma (POP/Server ID)**, come illustrato nell'esempio seguente hello.
* Controllare hello **X Cache** intestazione della risposta.  intestazione Hello dovrebbe essere **HIT**.  

![Intestazioni di risposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Verificare il file hello soddisfi i requisiti di dimensione hello
> [!NOTE]
> Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).
> 
> 

toobe idonee per la compressione, un file deve soddisfare hello seguenti requisiti di dimensione:

* Maggiore di 128 byte.
* Minore di 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Controllo hello richiesta al server di origine hello un **tramite** intestazione
Hello **tramite** intestazione HTTP indica i server web toohello che hello richiesta viene passato da un server proxy.  Server web IIS Microsoft per impostazione predefinita non comprimere le risposte quando hello richiesta contiene un **tramite** intestazione.  toooverride questo comportamento, eseguire l'esempio hello:

* **IIS 6**: [impostare HcNoCompressionForProxies = "FALSE" nelle proprietà della Metabase di IIS hello](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 e successive**: [impostare sia **noCompressionForHttp10** e **noCompressionForProxies** tooFalse in configurazione server hello](http://www.iis.net/configreference/system.webserver/httpcompression)

