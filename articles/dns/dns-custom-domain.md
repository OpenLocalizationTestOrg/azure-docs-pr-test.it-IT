---
title: aaaIntegrate DNS di Azure con le risorse di Azure | Documenti Microsoft
description: Informazioni su come toouse DNS di Azure lungo tooprovide DNS per le risorse di Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Utilizzare le impostazioni di dominio personalizzato tooprovide DNS di Azure per un servizio di Azure

Il servizio DNS di Azure consente di specificare il DNS per un dominio personalizzato per tutte le risorse di Azure che supportano i domini personalizzati o dispongono di un nome di dominio completo (FQDN). Come nel caso si dispone di un'app web di Azure e si desidera il tooaccess gli utenti da uno tramite contoso.com o www.contoso.com come un nome di dominio completo. Questo articolo illustra la configurazione del servizio di Azure con il DNS di Azure per l'uso di domini personalizzati.

## <a name="prerequisites"></a>Prerequisiti

In ordine toouse DNS di Azure per il dominio personalizzato, è innanzitutto necessario delegare il tooAzure di dominio DNS. Visitare [tooAzure un dominio DNS delegato](./dns-delegate-domain-azure-dns.md) per istruzioni su come tooconfigure server dei nomi per la delega. Una volta che il dominio è delegata tooyour zona di DNS di Azure, si è i record DNS di hello in grado di tooconfigure necessari.

È possibile configurare un dominio personale o personalizzato per le [app per le funzioni di ](#azure-function-app), [Azure IoT](#azure-iot), gli [indirizzi IP pubblici](#public-ip-address), le [app Web del servizio app](#app-service-web-apps), l'[archivio BLOB](#blob-storage) e la [rete CDN di Azure](#azure-cdn).

## <a name="azure-function-app"></a>App per le funzioni di Azure

tooconfigure un dominio personalizzato per le app di Azure (funzione), nonché configurazione hello funzione app stessa cui viene creato un record CNAME.
 
Passare troppo**altri** > **funzione App** e selezionare l'App di funzione. Fare clic su **Funzionalità della piattaforma** e in **RETE** fare clic su **Domini personalizzati**.

![pannello App per le funzioni](./media/dns-custom-domain/functionapp.png)

Prendere nota hello url corrente su hello **i domini personalizzati** pannello, questo indirizzo viene utilizzato come alias hello record DNS hello creato.

![pannello Domini personalizzati](./media/dns-custom-domain/functionshostname.png)

Passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.

|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | myfunctionapp        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per il nome di dominio personalizzato hello.        |
|Tipo     | CNAME        | L'uso di un record CNAME equivale a usare un alias.        |
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Alias     | adatumfunction.azurewebsites.net        | nome DNS Hello si sta creando alias hello, in questo esempio è nome DNS di adatumfunction.azurewebsites.net hello fornito dall'app di funzione toohello predefinita.        |

Spostarsi indietro tooyour funzione app, fare clic su **funzionalità della piattaforma**e in **rete** fare clic su **i domini personalizzati**, quindi in **Hostnames**fare clic su **+ Aggiungi hostname**.

In hello **aggiungere hostname** pannello, immettere i record CNAME hello in hello **hostname** campo di testo e fare clic su **convalida**. Se il record di hello toobe in grado di trovare, hello **aggiungere hostname** pulsante viene visualizzato. Fare clic su **aggiungere hostname** alias hello tooadd.

![pannello Aggiungi il nome host dell'app per le funzioni](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT non dispone di tutte le personalizzazioni necessarie sul servizio hello stesso. è necessario un dominio personalizzato con un IoT Hub toouse solo un record CNAME a cui punta toohello risorse.

Passare troppo**Internet of Things** > **IoT Hub** e selezionare l'hub IoT. In hello **Panoramica** pannello hello nota FQDN dell'hub IoT hello.

![Pannello Hub IoT](./media/dns-custom-domain/iot.png)

Successivamente, passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.


|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | myiothub        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per l'hub IoT hello.        |
|Tipo     | CNAME        | L'uso di un record CNAME equivale a usare un alias.
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Alias     | adatumIOT.azure-devices.net        | nome DNS Hello si sta creando alias hello, in questo esempio è un nome di host adatumIOT.azure devices.net hello fornito dall'hub IoT hello.

Una volta creato il record di hello, verificare la risoluzione dei nomi con record CNAME hello utilizzando`nslookup`

## <a name="public-ip-address"></a>Indirizzo IP pubblico

un dominio personalizzato per i servizi che utilizzano un indirizzo IP pubblico tooconfigure risorse come servizio Cloud Gateway di applicazione, bilanciamento del carico, le macchine virtuali di gestione risorse, e le macchine virtuali classiche, un record CNAME utilizzate.

Passare troppo**rete** > **indirizzo IP pubblico**, selezionare una risorsa indirizzo IP pubblico hello e fare clic su **configurazione**. Tenere traccia dei indirizzo IP hello indicato.

![pannello Indirizzo IP pubblico](./media/dns-custom-domain/publicip.png)

Passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.


|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | mywebserver        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per il nome di dominio personalizzato hello.        |
|Tipo     | Una         | Utilizzare un record come risorsa hello è un indirizzo IP.        |
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Indirizzo IP     | <your ip address>       | indirizzo IP pubblico Hello.|

![creare un record A](./media/dns-custom-domain/arecord.png)

Una volta creato il record A hello, eseguire `nslookup` record hello toovalidate viene risolto.

![ricerca DNS IP pubblico](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Web del servizio app

Hello passaggi seguenti consentono di configurare un dominio personalizzato per un'applicazione del servizio web app.

Passare troppo**Mobile & Web** > **servizio App** selezionare hello risorsa che si sta configurando un nome di dominio personalizzato e fare clic su **i domini personalizzati**.

Prendere nota hello url corrente su hello **i domini personalizzati** pannello, questo indirizzo viene utilizzato come alias hello record DNS hello creato.

![pannello Domini personalizzati](./media/dns-custom-domain/url.png)

Passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.


|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | mywebserver        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per il nome di dominio personalizzato hello.        |
|Tipo     | CNAME        | L'uso di un record CNAME equivale a usare un alias. Se la risorsa hello usato un indirizzo IP, viene utilizzato un record A.        |
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Alias     | webserver.azurewebsites.net        | nome DNS Hello si sta creando alias hello, in questo esempio è un nome DNS di webserver.azurewebsites.net hello fornito dall'applicazione web di toohello predefinito.        |


![creare un record CNAME](./media/dns-custom-domain/createcnamerecord.png)

Spostarsi indietro toohello app service che è configurato per il nome di dominio personalizzato hello. Fare clic su **Domini personalizzati** e quindi su **Nomi host**. record CNAME di hello tooadd creato, fare clic su **+ Aggiungi hostname**.

![Figura 1](./media/dns-custom-domain/figure1.png)

Una volta completato il processo di hello, eseguire **nslookup** toovalidate risoluzione dei nomi funzioni.

![Figura 1](./media/dns-custom-domain/finalnslookup.png)

toolearn ulteriori informazioni sui mapping tooApp un dominio personalizzato del servizio, visitare [mappare un esistente personalizzato DNS nome tooAzure App Web](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Se è necessario un dominio personalizzato toopurchase, visitare [acquistare un nome di dominio personalizzato per le app Web di Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn ulteriori informazioni sui domini di servizio App.

## <a name="blob-storage"></a>Archiviazione BLOB

Hello passaggi seguenti consentono di configurare un record CNAME per un account di archiviazione blob utilizzando il metodo asverify hello. Questo metodo permette di azzerate il tempo di inattività.

Passare troppo**archiviazione** > **gli account di archiviazione**, selezionare l'account di archiviazione e fare clic su **dominio personalizzato**. Tenere traccia dei hello FQDN nel passaggio 2, questo valore viene utilizzato il record CNAME prima di toocreate hello

![dominio personalizzato dell'archivio BLOB](./media/dns-custom-domain/blobcustomdomain.png)

Passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.


|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | asverify.mystorageaccount        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per il nome di dominio personalizzato hello.        |
|Tipo     | CNAME        | L'uso di un record CNAME equivale a usare un alias.        |
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Alias     | asverify.adatumfunctiona9ed.blob.core.windows.net        | nome DNS Hello si sta creando alias hello, in questo esempio è un nome DNS di asverify.adatumfunctiona9ed.blob.core.windows.net hello fornito dall'account di archiviazione predefinito toohello.        |

Passare l'account di archiviazione back-tooyour facendo **archiviazione** > **gli account di archiviazione**, selezionare l'account di archiviazione e fare clic su **dominio personalizzato**. Tipo di alias è creato senza prefisso asverify hello nella casella di testo hello, controllo hello * * Usa convalida CNAME indiretta e fare clic su **salvare**. Una volta completato questo passaggio, tornare tooyour zona DNS e creare un record CNAME senza prefisso asverify hello.  Dopo quel momento, si è sicuri toodelete hello record CNAME prefisso cdnverify hello.

![dominio personalizzato dell'archivio BLOB](./media/dns-custom-domain/indirectvalidate.png)

Per convalidare la risoluzione del DNS, eseguire `nslookup`.

informazioni sul mapping di un endpoint di archiviazione blob tooa dominio personalizzato, visitare toolearn [configurare un nome di dominio personalizzato per l'endpoint di archiviazione Blob](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Rete CDN di Azure

Hello passaggi seguenti consentono di configurare un record CNAME per un endpoint rete CDN tramite il metodo cdnverify hello. Questo metodo permette di azzerate il tempo di inattività.

Passare troppo**rete** > **CDN profili**, selezionare il profilo CDN e fare clic su **endpoint** in **generale**.

Selezionare l'endpoint di hello si lavora con e fare clic su **+ dominio personalizzato**. Hello nota **nome host dell'Endpoint** come questo valore è il record di hello tale record CNAME hello punta a.

![dominio personalizzato della rete CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Passare una zona DNS tooyour e fare clic su **+ registrare set**. Compilare le seguenti informazioni su hello hello **aggiungere set di record** pannello e fare clic su **OK** toocreate è.

|Proprietà  |Valore  |Descrizione  |
|---------|---------|---------|
|Nome     | cdnverify.mycdnendpoint        | Questo valore con l'etichetta del nome di dominio hello è hello FQDN per il nome di dominio personalizzato hello.        |
|Tipo     | CNAME        | L'uso di un record CNAME equivale a usare un alias.        |
|TTL     | 1        | 1 corrisponde a 1 ora        |
|Unità TTL     | Ore        | Ore vengono utilizzate come misura di tempo hello         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.net        | nome DNS Hello si sta creando alias hello, in questo esempio è un nome DNS di cdnverify.adatumcdnendpoint.azureedge.net hello fornito dall'account di archiviazione predefinito toohello.        |

Passare l'endpoint rete CDN tooyour indietro facendo clic su **rete** > **CDN profili**e selezionare il profilo CDN. Fare clic su **+ dominio personalizzato** e immettere l'alias di record CNAME senza prefisso cdnverify hello e fare clic su **Aggiungi**.

Una volta completato questo passaggio, tornare tooyour zona DNS e creare un record CNAME senza prefisso cdnverify hello.  Dopo quel momento, si è sicuri toodelete hello record CNAME prefisso cdnverify hello. Per ulteriori informazioni sulla rete CDN e come tooconfigure un dominio personalizzato senza il passaggio di registrazione intermedio hello visitare [dominio di rete CDN di Azure mappa tooa contenuto personalizzato](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[configurare DNS inversa per i servizi ospitati in Azure](dns-reverse-dns-for-azure-services.md).
