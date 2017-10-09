---
title: aaaAzure IoT Suite connesso domande frequenti sulla factory | Documenti Microsoft
description: Domande frequenti sulla soluzione di connected factory di IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Domande frequenti sulla soluzione preconfigurata di connected factory di IoT Suite

Vedere anche, hello generale [domande frequenti su](iot-suite-faq.md) per IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Dove trovare il codice sorgente hello per soluzione hello preconfigurato

codice di origine Hello è archiviato in hello repository GitHub seguente:

* [Connected factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) (Soluzione preconfigurata di connected factory)

### <a name="what-is-opc-ua"></a>Che cos'è OPC UA?

OPC Unified Architecture (UA), rilasciato nel 2008, è uno standard di interoperabilità indipendente dalla piattaforma e orientato ai servizi. OPC UA viene anche usato da svariati sistemi e dispositivi di settore, ad esempio PC, PLC e sensori. OPC UA integra la funzionalità di hello specifiche hello OPC classico in un framework estendibile con protezione incorporata. È uno standard che viene gestito dal hello Foundation OPC. Hello [Foundation OPC](http://opcfoundation.org/) è un'organizzazione no profit con più di 440 membri. obiettivo di Hello dell'organizzazione hello è toouse OPC specifiche toofacilitate più fornitori, multipiattaforma, sicura e affidabile interoperabilità tramite:

* Infrastruttura
* Specifiche
* Tecnologia
* Processi

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Perché Microsoft ha scelto di che UA OPC per hello connesso soluzione factory preconfigurato?

Microsoft ha scelto OPC UA perché è uno standard aperto, non proprietario, indipendente dalla piattaforma, riconosciuto nel settore e collaudato. È un requisito per le soluzioni basate sull'architettura di riferimento Industrie 4.0 (RAMI4.0) che assicurano l'interoperabilità tra un'ampia serie di processi e attrezzature di produzione. Microsoft considera richiesta da soluzioni toobuild 4.0 Industrie dei clienti. Supporto per UA OPC consente barriera hello inferiore per i clienti tooachieve gli obiettivi prefissati e toothem valore commerciale immediato.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Aggiunta di una simulazione di toohello indirizzo VM IP pubblica

Si dispone di due opzioni tooadd hello l'indirizzo IP:

* Utilizzare uno script di PowerShell hello `Simulation/Factory/Add-SimulationPublicIp.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory). Passare il nome della distribuzione come parametro. Per una distribuzione locale, usare `<your username>ConnFactoryLocal`. script Hello viene visualizzato un indirizzo IP hello di hello macchina virtuale.

* Nel portale di Azure hello, individuare il gruppo di risorse hello della distribuzione. Ad eccezione di una distribuzione locale, il gruppo di risorse hello ha nome hello che è specificato come soluzione o il nome di distribuzione. Per una distribuzione locale utilizzando uno script di compilazione hello, nome hello hello del gruppo di risorse è `<your username>ConnFactoryLocal`. A questo punto aggiungere un nuovo **indirizzo IP pubblico** toohello gruppo di risorse.

> [!NOTE]
> In entrambi i casi, assicurarsi installare la patch più recenti di hello seguendo le istruzioni di hello nella hello [sito Web Ubuntu](https://wiki.ubuntu.com/Security/Upgrades). Mantenere l'installazione di hello backup toodate per fino a quando la macchina virtuale è possibile accedere tramite un indirizzo IP pubblico.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Come rimuovere hello pubblica IP indirizzo toohello simulazione VM?

Si dispone di due opzioni tooremove hello l'indirizzo IP:

* Usare script di PowerShell hello Simulation/Factory/Remove-SimulationPublicIp.ps1 di hello [repository](https://github.com/Azure/azure-iot-connected-factory). Passare il nome della distribuzione come parametro. Per una distribuzione locale, usare `<your username>ConnFactoryLocal`. script Hello viene visualizzato un indirizzo IP hello di hello macchina virtuale.

* Nel portale di Azure hello, individuare il gruppo di risorse hello della distribuzione. Ad eccezione di una distribuzione locale, il gruppo di risorse hello ha nome hello che è specificato come soluzione o il nome di distribuzione. Per una distribuzione locale utilizzando uno script di compilazione hello, nome hello hello del gruppo di risorse è `<your username>ConnFactoryLocal`. A questo punto, rimuovere hello **indirizzo IP pubblico** risorsa dal gruppo di risorse hello.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Come Accedi toohello simulazione VM?

Firma nella simulazione toohello VM è supportata solo se è stata distribuita la soluzione usando script di PowerShell hello `build.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory).

Se è stata distribuita la soluzione hello da www.azureiotsuite.com, è possibile accedere in toohello macchina virtuale. È possibile accedere, perché la password di hello viene generata in modo casuale e non è possibile reimpostare.

1. Aggiungere un toohello di indirizzo IP pubblico macchina virtuale. Vedere [come aggiungere una simulazione di toohello indirizzo VM IP pubblica?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Creare un tooyour sessione SSH VM utilizzando l'indirizzo IP hello di hello macchina virtuale.
1. è Hello username toouse: `docker`.
1. Hello password toouse dipende dalla versione di hello utilizzato toodeploy:
    * Per le soluzioni distribuite mediante script build.ps1 hello prima 1 giugno 2017, password hello è: `Passw0rd`.
    * Per le soluzioni distribuite mediante script build.ps1 hello dopo il 1 giugno 2017, è possibile trovare la password di hello in hello `<name of your deployment>.config.user` file. Hello password viene archiviata in hello **VmAdminPassword** impostazione. Hello password viene generata in modo casuale in fase di distribuzione se non si specifica utilizzando hello `build.ps1` parametro di script`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Come arrestare e avviare tutti i processi di docker nella macchina virtuale di simulazione di hello?

1. Accedi simulazione toohello macchina virtuale. Vedere [come effettuare l'accesso nella simulazione toohello macchina virtuale?](#how-do-i-sign-in-to-the-simulation-vm)
1. eseguire i contenitori sono attivi, toocheck: `docker ps`.
1. eseguire tutti i contenitori di simulazione, toostop: `./stopsimulation`.
1. toostart tutti i contenitori di simulazione:
    * Esportare una variabile della shell con nome hello **IOTHUB_CONNECTIONSTRING**. Utilizzare il valore di hello di hello **IotHubOwnerConnectionString** impostazione hello `<name of your deployment>.config.user` file. ad esempio:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Eseguire `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Come posso aggiornare simulazione hello nella VM hello?

Se sono state apportate modifiche toohello simulazione, è possibile utilizzare script di PowerShell hello `build.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory) utilizzando hello `updatedimulation` comando. Questo script compila tutti i componenti di simulazione hello, la simulazione di hello in hello VM si interrompe, caricamenti, installa e avviarle.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Come scoprire la stringa di connessione hello dell'hub IoT hello utilizzato dalla soluzione?

Se è stata distribuita la soluzione con hello `build.ps1` script hello [repository](https://github.com/Azure/azure-iot-connected-factory), la stringa di connessione hello è il valore di hello di **IotHubOwnerConnectionString** in hello `<name of your deployment>.config.user` file.

È inoltre possibile trovare stringa di connessione di hello utilizzando hello portale di Azure. In hello risorsa IoT Hub nel gruppo di risorse hello della distribuzione, individuare le impostazioni della stringa di connessione hello.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Quali dispositivi IoT Hub hello utilizzare simulazione factory connessi?

Hello simulazione self registra hello seguenti dispositivi:

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Utilizzando hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o [l'hub IOT Esplora](https://github.com/azure/iothub-explorer) strumento, è possibile controllare quali dispositivi sono registrati con l'hub IoT hello utilizza la soluzione. toouse questi strumenti, è necessario stringa di connessione hello per l'hub IoT hello nella distribuzione.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Come è possibile ottenere dati di log dai componenti di simulazione hello?

Tutti i componenti nella simulazione di hello registrare informazioni nei file toolog. Questi file sono reperibile in hello VM nella cartella hello `home/docker/Logs`. log di hello tooretrieve, è possibile utilizzare script di PowerShell hello `Simulation/Factory/Get-SimulationLogs.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory).

Questo script deve toosign in toohello macchina virtuale. Potrebbe essere necessario tooprovide credenziali per l'accesso hello. Vedere [come effettuare l'accesso nella simulazione toohello VM?](#how-do-i-sign-in-to-the-simulation-vm) credenziali hello toofind.

script Hello aggiunge o rimuove un toohello di indirizzo IP pubblico macchina virtuale, se non dispone ancora di uno e lo rimuove. script Hello inserisce tutti i file di log in un archivio e scarica workstation di sviluppo tooyour archivio hello.

In alternativa, accedere toohello VM tramite SSH, esaminare i file di log hello in fase di esecuzione.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Come è possibile controllare se la simulazione hello sta inviando dati toohello nel cloud?

Con hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) o hello [l'hub IOT Esplora](https://github.com/azure/iothub-explorer) strumento, è possibile controllare i dati di hello inviati tooIoT Hub da alcuni dispositivi. toouse questi strumenti, è necessario stringa di connessione hello tooknow per l'hub IoT hello nella distribuzione. Vedere [come è possibile individuare la stringa di connessione hello dell'hub IoT hello utilizzato dalla soluzione?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Controllare i dati di hello inviati da uno dei dispositivi di server di pubblicazione hello:

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Se viene non visualizzato alcun dato inviato tooIoT Hub, quindi si verifica un problema con una simulazione hello. Come primo passaggio di analisi è consigliabile analizzare i file di log hello dei componenti di simulazione hello. Vedere [come è possibile ottenere dati di log da hello componenti simulazione?](#how-can-i-get-log-data-from-the-simulation-components) Provare toostop e avviare la simulazione hello e se non sono ancora presenti dati inviati, aggiornare la simulazione hello completamente. Vedere [come aggiornare simulazione hello nella VM hello?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Passaggi successivi

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva](iot-suite-predictive-overview.md)
* [Panoramica della soluzione preconfigurata di connected factory](iot-suite-connected-factory-overview.md)
* [Sicurezza di IoT da hello messa a terra](securing-iot-ground-up.md)
