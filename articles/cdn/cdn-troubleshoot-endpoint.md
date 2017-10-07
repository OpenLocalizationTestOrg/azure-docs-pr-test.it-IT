---
title: gli endpoint rete CDN di Azure aaaTroubleshooting restituzione di stato 404 | Documenti Microsoft
description: Risolvere i problemi relativi ai codici di risposta 404 con endpoint della rete CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404
Questo articolo consente di risolvere i problemi relativi agli [endpoint della rete CDN](cdn-create-new-endpoint.md) che restituiscono errori 404.

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.

## <a name="symptom"></a>Sintomo
Creato un profilo di rete CDN e un endpoint, ma il contenuto non sembra toobe disponibile in rete CDN hello.  Utenti che tentano di tooaccess il contenuto tramite URL CDN hello ricevere i codici di stato HTTP 404. 

## <a name="cause"></a>Causa
Le cause possono essere diverse, ad esempio:

* Hello origine file non è visibile toohello rete CDN
* endpoint Hello è configurato in modo errato, causando hello CDN toolook nella posizione sbagliata hello
* host Hello sta rifiutando intestazione host hello da hello rete CDN
* endpoint di Hello non sono state toopropagate tempo in tutto hello rete CDN

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi
> [!IMPORTANT]
> Dopo aver creato un endpoint rete CDN, non immediatamente sarà disponibile per l'utilizzo, come il tempo per hello registrazione toopropagate tramite hello CDN.  La propagazione dei profili della <b>rete CDN di Azure fornita da Akamai</b> di solito dura meno di un minuto.  Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.  Se si completano i passaggi di hello in questo documento e si sta ancora ottenere 404 risposte, prendere in considerazione in attesa di poche ore toocheck nuovamente prima di aprire un ticket di supporto.
> 
> 

### <a name="check-hello-origin-file"></a>Controllare il file di origine hello
È necessario verificare innanzitutto hello file hello si vuole memorizzare nella cache è disponibile l'origine ed è accessibile pubblicamente.  Hello toodo modo più rapido che è un browser tooopen in una sessione In privato o Incognito e passare direttamente a file toohello.  Solo digitare o incollare hello URL nella casella Indirizzo hello e visualizzare se risultante nel file hello desiderato.  In questo esempio verrà toouse un file che contiene un account di archiviazione di Azure, accessibile `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Come si può notare, passa correttamente test hello.

![Completamento della procedura](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Mentre questo è più rapido hello e tooverify modo più semplice il file è disponibile pubblicamente, può fornire alcune configurazioni di rete nell'organizzazione si hello illusione che questo file è disponibile pubblicamente quando è, infatti, solo visibile toousers di (la rete anche se è ospitato in Azure).  Se si dispone di un browser esterno da cui è possibile verificare, ad esempio un dispositivo mobile che non è connesso in rete dell'organizzazione tooyour o una macchina virtuale in Azure, che potrebbe essere più appropriata.
> 
> 

### <a name="check-hello-origin-settings"></a>Controllare le impostazioni dell'origine hello
È stata verificata file hello è disponibile pubblicamente su internet di hello, è necessario verificare le impostazioni di origine.  In hello [portale Azure](https://portal.azure.com), individuare il profilo CDN tooyour e fare clic sull'endpoint hello si sta cercando di risolvere.  Nella finestra hello **Endpoint** pannello, fare clic su origine hello.  

![Pannello Endpoint con origine evidenziata](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Hello **origine** pannello viene visualizzato. 

![Pannello Origine](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Tipo di origine e nome host
Verificare hello **tipo di origine** sia corretto e verificare hello **nome host dell'origine**.  In questo esempio, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, porzione hostname di hello di hello URL `cdndocdemo.blob.core.windows.net`.  Come si può vedere nella schermata di hello, il valore è corretto.  Per l'archiviazione di Azure, App Web e le origini di servizio Cloud, hello **nome host dell'origine** campo è un elenco a discesa, è necessario tooworry su cui stato digitato correttamente.  Tuttavia, se si usa un'origine personalizzata, è *assolutamente fondamentale* che l'ortografia del nome host sia corretta.

#### <a name="http-and-https-ports"></a>Porte HTTP e HTTPS
è Hello altri toocheck cosa qui il **HTTP** e **porte HTTPS**.  Nella maggior parte dei casi, 80 e 443 sono corrette e non saranno necessarie modifiche.  Tuttavia, se il server di origine hello è in ascolto su una porta diversa, che sarà necessario toobe rappresentato qui.  Se non si è certi, osservare hello URL per il file di origine.  specifiche di HTTPS e HTTP Hello specificano porte 80 e 443 come impostazioni predefinite di hello. L'URL, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, una porta non è specificata, in modo hello 443 predefinita è e le impostazioni sono corrette.  

Tuttavia, ad esempio hello URL per il file di origine che verificato in precedenza è `http://www.contoso.com:8080/file.txt`.  Hello nota `:8080` alla fine di hello del segmento hostname hello.  Che indica la porta di hello browser toouse `8080` tooconnect toohello server web `www.contoso.com`, pertanto sarà necessario tooenter 8080 in hello **porta HTTP** campo.  È importante toonote che queste impostazioni porta influiscono solo sull'endpoint di hello quale porta utilizza le informazioni tooretrieve origine hello.

> [!NOTE]
> **Rete CDN di Azure da Akamai** endpoint non consentano hello completo TCP intervallo di porte per le origini.  Per un elenco delle porte di origine non consentite, vedere l'articolo relativo ai [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Porte di origine consentite in Rete CDN di Azure da Akamai).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Controllare le impostazioni di endpoint hello
In hello **Endpoint** pannello, fare clic su hello **configura** pulsante.

![Pannello Endpoint con il pulsante Configura evidenziato](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Hello dell'endpoint **configura** pannello viene visualizzato.

![Pannello Configura](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocolli
Per **protocolli**, verificare che sia selezionato il protocollo di hello utilizzato dai client hello.  Hello stesso protocollo utilizzato dal client hello sarà utilizzato uno origine hello tooaccess, pertanto è importante toohave hello origine le porte configurate correttamente nella sezione precedente hello hello.  endpoint Hello in ascolto solo su hello predefinito porte HTTP e HTTPS (80 e 443), indipendentemente dalle porte di origine hello.

Torniamo tooour esempio ipotetico con `http://www.contoso.com:8080/file.txt`.  Come si ricorderà, per Contoso è stato specificato `8080` come porta HTTP, ma si supponga anche che sia stato specificato `44300` come porta HTTPS.  Se è stato creato un endpoint denominato `contoso`, il nome host dell'endpoint di rete CDN sarà `contoso.azureedge.net`.  Una richiesta per `http://contoso.azureedge.net/file.txt` è una richiesta HTTP, endpoint hello potrebbe usare HTTP sulla porta 8080 tooretrieve dall'origine hello.  Una richiesta protetta tramite HTTPS, `https://contoso.azureedge.net/file.txt`, causerebbe hello endpoint toouse HTTPS sulla porta 44300 quando durante il recupero della hello file dall'origine hello.

#### <a name="origin-host-header"></a>Intestazione host di origine
Hello **intestazione host di origine** è il valore di intestazione host hello inviato origine toohello con ogni richiesta.  Nella maggior parte dei casi, questo deve essere hello stesso come hello **nome host dell'origine** abbiamo verificato in precedenza.  Un valore non corretto in questo campo non è in genere provocheranno 404 stati, ma è probabile toocause altri Stati 4xx, a seconda di quale origine hello prevista.

#### <a name="origin-path"></a>Percorso dell'origine
Infine è necessario verificare il **Percorso dell'origine**.  Per impostazione predefinita è vuoto.  È consigliabile utilizzare questo campo solo se si desidera toonarrow hello ambito delle risorse basati su origine hello desiderato toomake disponibile in rete CDN hello.  

Ad esempio, l'endpoint, vorrei tutte le risorse in my toobe di account di archiviazione disponibile, pertanto lasciato **il percorso di origine** vuoto.  Ciò significa che una richiesta troppo`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` risultati in una connessione da my endpoint troppo`cdndocdemo.core.windows.net` che richiede `/publicblob/lorem.txt`.  Analogamente, una richiesta per `https://cdndocdemo.azureedge.net/donotcache/status.png` comporta la richiesta di hello endpoint `/donotcache/status.png` dall'origine hello.

Ma cosa accade se si desidera toouse hello CDN per ogni percorso l'origine?  Ad esempio I voleva solo hello tooexpose `publicblob` percorso.  Se immette */publicblob* in my **il percorso di origine** campo, che causa hello endpoint tooinsert */publicblob* prima di ogni richiesta effettuata toohello origine.  Ciò significa che la richiesta di hello per `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` effettivamente visualizzata parte richiesta hello dell'URL di hello, `/publicblob/lorem.txt`e aggiungere `/publicblob` toohello inizio. Di conseguenza, una richiesta per `/publicblob/publicblob/lorem.txt` dall'origine hello.  Se tale percorso non viene risolto tooan effettive del file, origine hello verrà restituito uno stato 404.  Hello corretto URL tooretrieve lorem.txt in questo esempio sarebbe effettivamente `https://cdndocdemo.azureedge.net/lorem.txt`.  Si noti che non includono hello */publicblob* percorso, in quanto parte richiesta hello di hello URL è `/lorem.txt` e consente di aggiungere endpoint hello `/publicblob`, con conseguente `/publicblob/lorem.txt` richiesta hello passati toohello origine .

