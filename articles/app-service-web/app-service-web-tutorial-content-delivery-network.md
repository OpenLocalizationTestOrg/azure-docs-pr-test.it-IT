---
title: aaaAdd tooan una rete CDN Azure App Service | Documenti Microsoft
description: Aggiungere un toocache di servizio App di Azure tooan rete CDN (Content Delivery) e recapitare file statici dal server ai clienti tooyour Chiudi tutto il mondo hello.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Aggiungere un tooan rete CDN (Content Delivery) servizio App di Azure

[Rete di distribuzione Azure contenuti (CDN)](../cdn/cdn-overview.md) memorizza nella cache il contenuto web statico in percorsi strategici tooprovide massima velocità effettiva per il recapito toousers contenuto. Hello CDN riduce anche il carico del server nell'app web. Questa esercitazione viene illustrato come tooadd rete CDN di Azure tooa [app web in Azure App Service](app-service-web-overview.md). 

Ecco hello home page di hello esempio sito HTML statico che è possibile utilizzare:

![Home page dell'app di esempio](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Contenuto dell'esercitazione:

> [!div class="checklist"]
> * Creare un endpoint della rete CDN.
> * Aggiornare gli asset memorizzati nella cache.
> * Versioni di toocontrol memorizzati nella cache delle stringhe di query di utilizzo.
> * Utilizzare un dominio personalizzato per l'endpoint rete CDN hello.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

- [Installare Git](https://git-scm.com/)
- [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Creare l'app web hello

toocreate hello web app che verranno utilizzate, seguire hello [quickstart HTML statico](app-service-web-get-started-html.md) tramite hello **Sfoglia toohello app** passaggio.

### <a name="have-a-custom-domain-ready"></a>Preparare un dominio personalizzato

passaggio di dominio personalizzato hello toocomplete di questa esercitazione, è necessario tooown un dominio personalizzato e dispone del Registro di sistema di accesso tooyour DNS per il provider del dominio (ad esempio GoDaddy). Ad esempio, le voci DNS tooadd per `contoso.com` e `www.contoso.com`, è necessario disporre di impostazioni di accesso tooconfigure hello DNS per hello `contoso.com` dominio radice.

Se si dispone già di un nome di dominio, è consigliabile seguenti hello [esercitazione di dominio di servizio App](custom-dns-web-site-buydomains-web-app.md) toopurchase il dominio utilizzando hello portale di Azure. 

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Aprire un browser e passare toohello [portale di Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Creare un profilo e un endpoint della rete CDN

Nel riquadro di spostamento sinistro di hello, selezionare **servizi App**e quindi selezionare l'applicazione hello creati in hello [quickstart HTML statico](app-service-web-get-started-html.md).

![Selezionare l'applicazione di servizio App nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

In hello **servizio App** hello della pagina **impostazioni** selezionare **rete > rete CDN di Azure configurare per l'app**.

![Selezionare una rete CDN nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

In hello **rete CDN di Azure** fornire hello **nuovo endpoint** impostazioni come specificato nella tabella hello.

![Creare endpoint e del profilo nel portale di hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Impostazione | Valore consigliato | Descrizione |
| ------- | --------------- | ----------- |
| **Profilo CDN** | myCDNProfile | Selezionare **Crea nuovo** toocreate un profilo di rete CDN. Il profilo CDN è una raccolta di endpoint CDN con hello stesso livello di prezzo. |
| **Piano tariffario** | Standard Akamai | Hello [tariffario](../cdn/cdn-overview.md#azure-cdn-features) specifica provider hello e le funzionalità disponibili. In questa esercitazione si userà Akamai standard. |
| **Nome endpoint rete CDN** | Qualsiasi nome che è univoco nel dominio azureedge.net hello | Accedere alle risorse memorizzate nella cache dominio hello  *\<endpointname >. azureedge.net*.

Selezionare **Crea**.

Azure Crea profilo hello e endpoint. viene visualizzata di nuovo endpoint Hello in hello **endpoint** elenco hello stessa pagina, e quando è disponibile lo stato di hello è **esecuzione**.

![Nuovo endpoint nell'elenco](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Hello test endpoint rete CDN

Se è stato selezionato il piano tariffario Verizon, la propagazione dell'endpoint richiede in genere circa 90 minuti. Per Akamai è sufficiente qualche minuto.

applicazione di esempio Hello ha un `index.html` file e *css*, *img*, e *js* cartelle che contengono altre risorse statici. percorsi per tutti i file sono contenuto Hello hello stesso all'endpoint rete CDN hello. Ad esempio, entrambi gli URL seguenti hello accedere hello *bootstrap.css* file hello *css* cartella:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Passare un toohello browser URL seguente:

```
http://<endpointname>.azureedge.net/index.html
```

![Home page dell'app di esempio fornita dalla rete CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Vedrai hello stessa pagina è stata eseguita in precedenza in un'app web di Azure. Rete CDN di Azure ha recuperato asset dell'app web origine di hello e viene utilizzata dall'endpoint rete CDN hello

tooensure che questa pagina memorizzato nella cache di hello CDN, aggiornare la pagina hello. Due richieste hello stesso asset sono talvolta necessarie per toocache CDN hello hello contenuto richiesto.

Per altre informazioni sulla creazione dei profili e degli endpoint della rete CDN di Azure, vedere [Introduzione alla rete CDN di Azure](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Ripulire hello rete CDN

rete CDN Hello Aggiorna periodicamente le risorse da app web di origine hello in base alla configurazione di hello time-to-live (TTL). durata TTL predefinita Hello è sette giorni.

In alcuni casi potrebbe essere necessario toorefresh hello CDN prima della scadenza di TTL: hello, ad esempio, quando si distribuisce l'app web toohello contenuto aggiornato. tootrigger un aggiornamento, è possibile eliminare manualmente le risorse di rete CDN hello. 

In questa sezione dell'esercitazione hello, si distribuisce un'app web toohello di modifica e ripulitura hello CDN tootrigger hello CDN toorefresh la cache.

### <a name="deploy-a-change-toohello-web-app"></a>Distribuire un'app web toohello di modifica

Aprire hello `index.html` file e aggiungere "-V2" intestazione H1 toohello, come illustrato nell'esempio seguente hello: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Eseguire il commit della modifica e distribuirlo toohello web app.

```bash
git commit -am "version 2"
git push azure master
```

Una volta completata la distribuzione, URL dell'app web toohello Sfoglia e visualizzato hello modificare.

```
http://<appname>.azurewebsites.net/index.html
```

!["V2" nel titolo nell'app Web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

URL dell'endpoint rete CDN toohello Sfoglia per hello home page e si non si rilevano hello modificare la versione memorizzata nella cache di hello in hello CDN non è ancora scaduto. 

```
http://<endpointname>.azureedge.net/index.html
```

![Titolo nella rete CDN senza "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Ripulire hello CDN nel portale di hello

tootrigger hello CDN tooupdate la versione memorizzata nella cache, cancellare hello CDN.

Spostamento a sinistra del portale hello, selezionare **gruppi di risorse**, quindi selezionare gruppo di risorse hello creato per l'app web (myResourceGroup).

![Selezionare il gruppo di risorse](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Nell'elenco di hello delle risorse, selezionare l'endpoint CDN.

![Selezionare l'endpoint](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Nella parte superiore di hello di hello **Endpoint** pagina, fare clic su **ripulire**.

![Selezionare Ripulisci](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Immettere i percorsi del contenuto hello desiderato toopurge. È possibile passare un toopurge percorso completo del file, un singolo file o un toopurge segmento di percorso e aggiorna tutto il contenuto in una cartella. Poiché hai cambiato `index.html`, assicurarsi che sia uno dei percorsi di hello.

Nella parte inferiore di hello della pagina hello, selezionare **ripulire**.

![Pagina Ripulisci](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Verificare che hello che viene aggiornata della rete CDN

Attendere che la richiesta di eliminazione hello ha completato l'elaborazione, in genere un paio di minuti. toosee hello lo stato corrente, icona campana hello selezionare nella parte superiore di hello della pagina hello. 

![Notifica di ripulitura](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Individuare l'URL dell'endpoint rete CDN toohello per `index.html`, ed è ora possibile visualizzare hello V2 che è stato aggiunto toohello titolo hello home page. Ciò indica che è stata aggiornata per cache di hello rete CDN.

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" nel titolo nella rete CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Per altre informazioni, vedere [Ripulire un endpoint della rete CDN di Azure](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Utilizzare il contenuto di tooversion stringhe di query

Hello rete CDN di Azure offre hello le opzioni di memorizzazione nella cache comportamento seguenti:

* Ignora stringhe di query
* Disabilita la memorizzazione nella cache per le stringhe di query
* Memorizza nella cache tutti gli URL univoci 

Hello innanzitutto di questi è l'impostazione predefinita di hello, che non esiste un'unica versione memorizzata nella cache di un cespite indipendentemente dalla stringa di query hello hello URL. 

In questa sezione dell'esercitazione hello è modificare hello la memorizzazione nella cache comportamento toocache tutti gli URL univoci.

### <a name="change-hello-cache-behavior"></a>Modificare il comportamento della cache di hello

Nel portale di Azure hello **Endpoint rete CDN** selezionare **Cache**.

Selezionare **memorizzare nella Cache tutti gli URL univoci** da hello **stringa di Query, il comportamento di memorizzazione nella cache** elenco a discesa.

Selezionare **Salva**.

![Selezionare il comportamento di memorizzazione nella cache della stringa di query](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Verificare che gli URL univoci vengano memorizzati nella cache separatamente

In un browser, passare l'endpoint rete CDN hello toohello home page, ma includono una stringa di query: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

rete CDN Hello restituisce hello web app contenuto corrente, ovvero "2" nell'intestazione di hello. 

tooensure che questa pagina memorizzato nella cache di hello CDN, aggiornare la pagina hello. 

Aprire `index.html` e modificare anche "V2" "V3" e distribuire hello modifica. 

```bash
git commit -am "version 3"
git push azure master
```

In un browser, passare l'URL dell'endpoint rete CDN toohello con una nuova stringa di query, ad esempio `q=2`. rete CDN Hello Ottiene hello corrente `index.html` file e visualizza "V3".  Ma se si passa l'endpoint rete CDN toohello con hello `q=1` stringa di query viene visualizzato "V2".

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" nel titolo nella rete CDN, con stringa di query 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" nel titolo nella rete CDN, con stringa di query 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Questo output mostra che ogni stringa di query viene trattata in modo diverso:

* Poiché q=1 è stata usata in precedenza, vengono restituiti i contenuti memorizzati nella cache (V2).
* q = 2 è una novità, in modo più recente contenuto dell'app web hello viene recuperati e restituito (V3).

Per altre informazioni, vedere [Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Eseguire il mapping di un endpoint rete CDN tooa di dominio personalizzato

Viene eseguito il mapping del tooyour dominio personalizzato CDN Endpoint tramite la creazione di un record CNAME. Un record CNAME è una funzionalità DNS che esegue il mapping di un dominio di destinazione tooa di dominio di origine. Ad esempio, è possibile mappare `cdn.contoso.com` o `static.contoso.com` troppo`contoso.azureedge.net`.

Se non si dispone di un dominio personalizzato, prendere in considerazione seguenti hello [esercitazione di dominio di servizio App](custom-dns-web-site-buydomains-web-app.md) toopurchase il dominio utilizzando hello portale di Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Trovare hello hostname toouse con hello CNAME

Nel portale di Azure hello **Endpoint** assicurarsi **Panoramica** è selezionata in hello sinistro spostamento e quindi seleziona hello **+ dominio personalizzato** pulsante nella parte superiore di hello della pagina hello.

![Selezionare l'aggiunta di un dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

In hello **aggiungere un dominio personalizzato** visualizzata hello toouse nome host di endpoint per la creazione di un record CNAME. nome host Hello è derivato dall'URL dell'endpoint rete CDN:  **&lt;EndpointName >. azureedge.net**. 

![Pagina per l'aggiunta di un dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Configurare hello CNAME con il registrar

Sito web del registrar di dominio tooyour passare e individuare la sezione hello per la creazione di record DNS. Queste informazioni possono essere disponibili in una sezione come **Domain Name**, **DNS** o **Name Server Management**.

Trovare la sezione hello per la gestione dei record CNAME. È possibile avere una pagina di impostazioni avanzate tooan toogo e cercare parole hello CNAME, Alias o diversi sottodomini.

Creare un record CNAME che esegue il mapping del sottodominio scelto (ad esempio, **statico** o **cdn**) toohello **nome host dell'Endpoint** illustrato in precedenza nel portale di hello. 

### <a name="enter-hello-custom-domain-in-azure"></a>Immettere dominio personalizzato hello in Azure

Restituire toohello **aggiungere un dominio personalizzato** pagina e immettere il dominio personalizzato, inclusi il sottodominio hello, nella finestra di dialogo hello. Ad esempio, immettere `cdn.contoso.com`.   
   
Azure verifica l'esistenza di record CNAME hello hello nome di dominio immesso. Se hello CNAME è corretto, viene convalidato il dominio personalizzato.

Per i server di tooname toopropagate record CNAME hello in hello Internet può richiedere tempo. Se il dominio non viene convalidato immediatamente, attendere qualche minuto e riprovare.

### <a name="test-hello-custom-domain"></a>Dominio personalizzato hello di test

In un browser, passare toohello `index.html` file utilizzando il dominio personalizzato (ad esempio, `cdn.contoso.com/index.html`) tooverify hello risultato del metodo hello stesso come quando si passa direttamente troppo`<endpointname>azureedge.net/index.html`.

![Home page dell'app di esempio con URL del dominio personalizzato](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Per ulteriori informazioni, vedere [dominio di rete CDN di Azure mappa tooa contenuto personalizzato](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passaggi successivi

Contenuto dell'esercitazione:

> [!div class="checklist"]
> * Creare un endpoint della rete CDN.
> * Aggiornare gli asset memorizzati nella cache.
> * Versioni di toocontrol memorizzati nella cache delle stringhe di query di utilizzo.
> * Utilizzare un dominio personalizzato per l'endpoint rete CDN hello.

Informazioni su come le prestazioni della rete CDN toooptimize hello seguenti articoli:

> [!div class="nextstepaction"]
> [Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Precaricamento di risorse in un endpoint della rete CDN di Azure](../cdn/cdn-preload-endpoint.md)
