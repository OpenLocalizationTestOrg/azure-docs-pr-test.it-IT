---
title: aaaDeploy connesso nel gruppo di Azure IoT gateway factory | Documenti Microsoft
description: "Modalità di connessione delle factory toodeploy un gateway in Windows o Linux toohello connettività tooenable preconfigurato soluzione."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Distribuire un gateway in Windows o Linux per la soluzione factory preconfigurato hello connesso

Hello software necessario toodeploy un gateway per la soluzione factory preconfigurato hello connesso include due componenti:

* Hello *OPC Proxy* stabilisce un tooIoT connessione Hub. Hello *OPC Proxy* quindi attende i messaggi di comando e controllo da hello integrate OPC Browser che viene eseguita nel portale di soluzione hello factory connesso.
* Hello *Publisher OPC* connette tooexisting locale OPC UA server e inoltra i messaggi di dati di telemetria da essi tooIoT Hub.

Entrambi i componenti sono open source e disponibili come origine in GitHub e come contenitori di Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [Server di pubblicazione OPC][lnk-publisher-github] | [Server di pubblicazione OPC][lnk-publisher-docker] |
| [Proxy OPC][lnk-proxy-github] | [Proxy OPC][lnk-proxy-docker] |

Nessun indirizzo IP pubblico o problemi di firewall gateway hello sono necessari per uno dei due componenti. Hello OPC Proxy e server di pubblicazione OPC utilizzare solo le porte in uscita 443, 5671 e 8883.

Hello passaggi in questo articolo viene illustrato come toodeploy un gateway uno usando Docker [Windows](#windows-deployment) o [Linux](#linux-deployment). gateway di Hello consente soluzione di connettività toohello connesso factory preconfigurato.

> [!NOTE]
> il software gateway Hello viene eseguita nel contenitore Docker hello è [Azure IoT Edge].

## <a name="windows-deployment"></a>Distribuzione in Windows

> [!NOTE]
> Se non si ha ancora un dispositivo gateway, Microsoft consiglia di acquistare un gateway commerciale da uno dei partner. Visitare hello [catalogo dispositivi Azure IoT] per un elenco di dispositivi gateway compatibili con hello connesso soluzione factory. Seguire le istruzioni di hello forniti con hello dispositivo tooset di gateway hello. In alternativa, utilizzare hello seguendo le istruzioni toomanually impostare uno dei gateway esistente.

### <a name="install-docker"></a>Installare Docker

Installare [Docker per Windows] nel dispositivo gateway basato su Windows. Durante l'installazione di Docker di Windows, selezionare un'unità il tooshare macchina host con Docker. Hello seguente schermata mostra la condivisione di unità D hello sul sistema di Windows:

![Installare Docker][img-install-docker]

Quindi creare una cartella denominata **docker** nella radice di hello di hello le unità condivise.
È anche possibile eseguire questo passaggio dopo l'installazione di docker da hello **impostazioni** menu.

### <a name="configure-hello-gateway"></a>Configurare il gateway hello

1. È necessario hello **iothubowner** stringa di connessione del gruppo di IoT di Azure connessa factory distribuzione toocomplete hello gateway distribuzione. In hello [portale di Azure], passare tooyour IoT Hub nel gruppo di risorse hello creato per la distribuzione di soluzioni factory hello connesso. Fare clic su **criteri di accesso condiviso** tooaccess hello **iothubowner** stringa di connessione:

    ![Trovare la stringa di connessione IoT Hub hello][img-hub-connection]

    Hello copia **stringa di connessione - chiave primaria** valore.

1. Configurare il gateway di hello per l'IoT Hub eseguendo i moduli di hello due gateway **una volta** da un prompt dei comandi con:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  è hello Nome toogive tooyour OPC UA Publisher in formato hello **server di pubblicazione.&lt; il nome di dominio completo&gt;**. Ad esempio, se la rete factory viene chiamata **myfactorynetwork.com**, hello **ApplicationName** valore **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  è hello **iothubowner** stringa di connessione è stato copiato nel passaggio precedente hello. La stringa di connessione viene utilizzata solo in questo passaggio, non è necessario in hello alla procedura seguente:

    Utilizzare hello mappato d:\\cartella docker (hello `-v` argomento) toopersist successive hello due certificati x. 509 che utilizzano moduli di hello gateway.

### <a name="run-hello-gateway"></a>Eseguire hello gateway

1. Riavviare il gateway di hello tramite hello seguenti comandi:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Per motivi di sicurezza, i certificati x. 509 hello due persistente nell'unità d: hello\\cartella docker contiene la chiave privata di hello. Limitare le credenziali di accesso toothis cartella toohello (in genere **amministratori**) si utilizza toorun hello Docker contenitore. Pulsante destro del mouse hello d:\\cartella docker, scegliere **proprietà**, quindi **sicurezza**e quindi **modifica**. Assegnare ad **Administrators** (Amministratori) il controllo completo e rimuovere tutti gli altri utenti:

    ![Condivisione di concedere autorizzazioni tooDocker][img-docker-share]

1. Verificare la connettività di rete. Da un prompt dei comandi, immettere il comando di hello `ping publisher.<your fully qualified domain name>` tooping il gateway. Se la destinazione hello è raggiungibile, aggiungere l'indirizzo IP hello e il nome del file host gateway toohello sul gateway. file hosts di Hello è disponibile in hello **Windows\\System32\\driver\\via** cartella.

1. Successivamente, provare a tooconnect toohello server di pubblicazione utilizzando un client OPC UA locale che esegue gateway hello. Hello OPC UA URL dell'endpoint è `opc.tcp://publisher.<your fully qualified domain name>:62222`. Se non si ha un client OPC UA, è possibile scaricare e usare un [client OPC UA open source].

1. Quando questi test locali è stata completata, passare toohello **connettere il proprio Server UA OPC** hello factory connesso soluzione portale. Immettere l'URL dell'endpoint server di pubblicazione hello (`tcp://publisher.<your fully qualified domain name>:62222`) e fare clic su **Connetti**. Viene visualizzato un avviso relativo al certificato. Fare clic su **Proceed** (Continua). Successivamente si verifica un errore che hello server di pubblicazione non ritiene attendibile hello Client Web agente utente. tooresolve questo errore, hello copia **Client Web UA** certificato da hello **unità d:\\docker\\rifiutato certificati\\certificati** cartella toohello **Unità d:\\docker\\applicazioni UA\\certificati** cartella gateway hello. Non è necessario toorestart del gateway hello. Ripetere questo passaggio. È ora possibile connettersi toohello gateway dal cloud hello e si è pronti tooadd soluzione di toohello server UA OPC.

### <a name="add-your-opc-ua-servers"></a>Aggiungere i server OPC UA

1. Sfoglia toohello **connettere il proprio Server UA OPC** hello factory connesso soluzione portale. Attenersi alla stessa procedura come esempio hello precedente sezione tooestablish attendibilità tra hello portale factory connesso e hello server OPC UA hello. Questo passaggio stabilisce una relazione di trust reciproca dei certificati hello da hello connesso portale factory e i server OPC UA hello e crea una connessione.

1. Sfoglia hello albero di nodi OPC UA del server OPC UA, nodi OPC hello e scegliere **pubblicare**. Per pubblicazione toowork in questo modo, i server OPC UA hello e publisher hello deve trovarsi in hello stessa rete. In altre parole, se hello completo il nome di dominio del server di pubblicazione hello è **publisher.mydomain.com** il nome di dominio completo di hello di hello OPC UA server deve essere, ad esempio, **myopcuaserver.mydomain.com**. Se il programma di installazione è diversa, è possibile aggiungere manualmente i nodi toohello publishesnodes.json file nel hello **unità d:\\docker** cartella. Hello publishesnodes.json file viene generato automaticamente in hello innanzitutto corretta pubblicazione di un nodo OPC.

1. Dati di telemetria passerà da dispositivo gateway hello. È possibile visualizzare i dati di telemetria hello in hello **percorsi Factory** Visualizza del portale di factory connesso hello in **nuova Factory**.

## <a name="linux-deployment"></a>Distribuzione in Linux

> [!NOTE]
> Se non si ha ancora un dispositivo gateway, Microsoft consiglia di acquistare un gateway commerciale da uno dei partner. Visitare hello [catalogo dispositivi Azure IoT] per un elenco di dispositivi gateway compatibili con hello connesso soluzione factory. Seguire le istruzioni di hello forniti con hello dispositivo tooset di gateway hello. In alternativa, utilizzare hello seguendo le istruzioni toomanually impostare uno dei gateway esistente.

[Installare Docker] nel dispositivo gateway Linux.

### <a name="configure-hello-gateway"></a>Configurare il gateway hello

1. È necessario hello **iothubowner** stringa di connessione del gruppo di IoT di Azure connessa factory distribuzione toocomplete hello gateway distribuzione. In hello [portale di Azure], passare tooyour IoT Hub nel gruppo di risorse hello creato per la distribuzione di soluzioni factory hello connesso. Fare clic su **criteri di accesso condiviso** tooaccess hello **iothubowner** stringa di connessione:

    ![Trovare la stringa di connessione IoT Hub hello][img-hub-connection]

    Hello copia **stringa di connessione - chiave primaria** valore.

1. Configurare il gateway di hello per l'IoT Hub eseguendo i moduli di hello due gateway **una volta** da una shell con:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  è il nome di hello del gateway di OPC UA applicazione hello viene creato nel formato di hello hello **server di pubblicazione.&lt; il nome di dominio completo&gt;**. Ad esempio, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  è hello **iothubowner** stringa di connessione è stato copiato nel passaggio precedente hello. La stringa di connessione viene utilizzata solo in questo passaggio, non è necessario in hello alla procedura seguente:

    Utilizzare hello **/ condiviso** cartella (hello `-v` argomento) toopersist successive hello due certificati x. 509 che utilizzano moduli di hello gateway.

### <a name="run-hello-gateway"></a>Eseguire hello gateway

1. Riavviare il gateway di hello tramite hello seguenti comandi:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Per motivi di sicurezza, i certificati x. 509 hello due persistente in hello **/ condiviso** cartella contiene la chiave privata di hello. Limite toothis cartella toohello le credenziali di accesso è utilizzare toorun hello contenitore Docker. le autorizzazioni di hello tooset per **radice** solo, utilizzare hello `chmod` comando nella cartella hello della shell.

1. Verificare la connettività di rete. Da una shell, immettere il comando hello `ping publisher.<your fully qualified domain name>` tooping il gateway. Se la destinazione hello è raggiungibile, aggiungere l'indirizzo IP hello e il nome del file host gateway tooyour sul gateway. file hosts di Hello è disponibile in hello **e così via** cartella.

1. Successivamente, provare a tooconnect toohello server di pubblicazione utilizzando un client OPC UA locale che esegue gateway hello. Hello OPC UA URL dell'endpoint è `opc.tcp://publisher.<your fully qualified domain name>:62222`. Se non si ha un client OPC UA, è possibile scaricare e usare un [client OPC UA open source].

1. Quando questi test locali è stata completata, passare toohello **connettere il proprio Server UA OPC** hello factory connesso soluzione portale. Immettere l'URL dell'endpoint server di pubblicazione hello (`tcp://publisher.<your fully qualified domain name>:62222`) e fare clic su **Connetti**. Viene visualizzato un avviso relativo al certificato. Fare clic su **Proceed** (Continua). Successivamente si verifica un errore che hello server di pubblicazione non ritiene attendibile hello Client Web agente utente. tooresolve questo errore, hello copia **Client Web UA** certificato da hello **/shared/rifiutato con certificati/certificati** cartella toohello **/shared/UA applicazioni/certificati** cartella gateway hello. Non è necessario toorestart del gateway hello. Ripetere questo passaggio. È ora possibile connettersi toohello gateway dal cloud hello e si è pronti tooadd soluzione di toohello server UA OPC.

### <a name="add-your-opc-ua-servers"></a>Aggiungere i server OPC UA

1. Sfoglia toohello **connettere il proprio Server UA OPC** hello factory connesso soluzione portale. Attenersi alla stessa procedura come esempio hello precedente sezione tooestablish attendibilità tra hello portale factory connesso e hello server OPC UA hello. Questo passaggio stabilisce una relazione di trust reciproca dei certificati hello da hello connesso portale factory e i server OPC UA hello e crea una connessione.

1. Sfoglia hello albero di nodi OPC UA del server OPC UA, nodi OPC hello e scegliere **pubblicare**. Per pubblicazione toowork in questo modo, i server OPC UA hello e publisher hello deve trovarsi in hello stessa rete. In altre parole, se hello completo il nome di dominio del server di pubblicazione hello è **publisher.mydomain.com** il nome di dominio completo di hello di hello OPC UA server deve essere, ad esempio, **myopcuaserver.mydomain.com**. Se il programma di installazione è diversa, è possibile aggiungere manualmente i nodi toohello publishesnodes.json file nel hello **/ condiviso** cartella. Hello publishesnodes.json viene generato automaticamente in hello innanzitutto corretta pubblicazione di un nodo OPC.

1. Dati di telemetria passerà da dispositivo gateway hello. È possibile visualizzare i dati di telemetria hello in hello **percorsi Factory** Visualizza del portale di factory connesso hello in **nuova Factory**.

## <a name="next-steps"></a>Passaggi successivi

toolearn più informazioni sull'architettura di hello della factory connesso hello preconfigurato soluzione, vedere [factory connesso preconfigurato procedura dettagliata sulla soluzione][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker per Windows]: https://www.docker.com/docker-windows
[catalogo dispositivi Azure IoT]: https://catalog.azureiotsuite.com/?q=opc
[portale di Azure]: http://portal.azure.com/
[client OPC UA open source]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Installare Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy