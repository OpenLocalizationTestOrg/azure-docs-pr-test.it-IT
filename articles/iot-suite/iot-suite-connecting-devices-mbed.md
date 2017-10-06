---
title: aaaConnect un dispositivo utilizzando C su mbed | Documenti Microsoft
description: Viene descritto come tooconnect toohello un dispositivo Azure IoT Suite preconfigurati con un'applicazione scritta in C in esecuzione in un dispositivo mbed soluzione di monitoraggio remoto.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (mbed)

## <a name="scenario-overview"></a>Panoramica dello scenario
In questo scenario, si crea un dispositivo che invia hello seguendo il monitoraggio remoto di dati di telemetria toohello [preconfigurato soluzione][lnk-what-are-preconfig-solutions]:

* Temperatura esterna
* Temperatura interna
* Umidità

Per semplicità, codice hello sul dispositivo hello genera valori di esempio, ma che incoraggia la collaborazione è tooextend: esempio hello connettendosi dispositivo tooyour sensori reale e l'invio di dati di telemetria reale.

dispositivo Hello è anche toomethods toorespond in grado di richiamata dal dashboard di soluzione hello e valori di proprietà impostati in dashboard soluzione hello desiderati.

toocomplete questa esercitazione, è necessario un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].

## <a name="before-you-start"></a>Prima di iniziare
Prima di scrivere un codice per il dispositivo, occorre eseguire la soluzione preconfigurata di monitoraggio remoto e poi effettuare il provisioning di un nuovo dispositivo personalizzato all'interno della soluzione in questione.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Eseguire il provisioning della soluzione preconfigurata per il monitoraggio remoto
dispositivo Hello si creerà in questa esercitazione invia istanza tooan dati hello [monitoraggio remoto] [ lnk-remote-monitoring] preconfigurato soluzione. Se non hai già effettuato il provisioning hello soluzione preconfigurata nell'account di Azure di monitoraggio remoto, utilizzare hello alla procedura seguente:

1. In hello <https://www.azureiotsuite.com/> pagina, fare clic su  **+**  toocreate una soluzione.
2. Fare clic su **selezionare** su hello **monitoraggio remoto** pannello toocreate la soluzione.
3. In hello **creare il monitoraggio remoto soluzione** pagina, immettere un **Nome soluzione** di propria scelta, selezionare hello **area** toodeploy per desiderati e selezionare hello Azure toouse toowant di sottoscrizione. Fare clic su **Crea soluzione**.
4. Attendere il completamento di hello processo di provisioning.

> [!WARNING]
> le soluzioni di Hello preconfigurato utilizzano fatturabili servizi di Azure. Verificare tooremove hello soluzione preconfigurata dalla sottoscrizione di una volta con esso tooavoid eventuali addebiti non necessari. È possibile rimuovere completamente una soluzione preconfigurata dalla sottoscrizione, visitare hello <https://www.azureiotsuite.com/> pagina.
> 
> 

Termine del processo per la soluzione di monitoraggio remoto hello di provisioning hello, fare clic su **avviare** dashboard di soluzione hello tooopen nel browser.

![Dashboard della soluzione][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Eseguire il provisioning del dispositivo nella soluzione di monitoraggio remoto hello
> [!NOTE]
> Se è già stato eseguito il provisioning di un dispositivo nella soluzione, è possibile saltare questo passaggio. Quando si crea un'applicazione client hello, sono necessarie le credenziali di dispositivo di tooknow hello.
> 
> 

Per una soluzione di dispositivo tooconnect toohello preconfigurato, deve identificarsi tooIoT Hub usando credenziali valide. È possibile recuperare le credenziali di dispositivo hello dal dashboard di soluzione hello. Includere le credenziali di dispositivo hello nell'applicazione client più avanti in questa esercitazione.

tooadd una soluzione di monitoraggio remoto tooyour di dispositivo, hello completo seguendo i passaggi nel dashboard di soluzione hello:

1. Hello angolo in basso a sinistra del dashboard hello, fare clic su **aggiunge un dispositivo**.
   
   ![Aggiungere un dispositivo][1]
2. In hello **dispositivo personalizzato** pannello, fare clic su **Aggiungi nuovo**.
   
   ![Aggiungere un dispositivo personalizzato][2]
3. Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo). Immettere un ID dispositivo, ad esempio **mydevice**, fare clic su **ID controllo** tooverify tale nome è già in uso e quindi fare clic su **crea** dispositivo hello tooprovision.
   
   ![Aggiungere un ID dispositivo][3]
4. Rendere un dispositivo di hello nota le credenziali (ID dispositivo, nome host di Hub IoT e chiave del dispositivo). L'applicazione client deve questi toohello tooconnect valori soluzione di monitoraggio remoto. Fare quindi clic su **Done**.
   
    ![Vedere le credenziali del dispositivo][4]
5. Selezionare il dispositivo nell'elenco di dispositivi hello nel dashboard di soluzione hello. Quindi, nel hello **dettagli dispositivo** pannello, fare clic su **Abilita periferica**. lo stato di Hello del dispositivo è ora **esecuzione**. soluzione di monitoraggio remoto Hello possa ora ricevere i dati di telemetria dal dispositivo e richiamare metodi sul dispositivo hello.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Compilare ed eseguire la soluzione di esempio hello C

Hello istruzioni seguenti vengono descritti hello passaggi per la connessione di un [FRDM-K64F abilitato mbed Freescale] [ lnk-mbed-home] toohello dispositivo remoto nella soluzione di monitoraggio.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>La connessione di rete tooyour di hello mbed dispositivi e computer desktop

1. Connettere hello mbed dispositivo tooyour rete tramite un cavo Ethernet. Questo passaggio è necessario perché l'applicazione di esempio hello richiede l'accesso a internet.

1. Vedere [introduzione mbed] [ lnk-mbed-getstarted] tooconnect desktop tooyour mbed dispositivo PC.

1. Se il PC è in esecuzione Windows, vedere [configurazione PC] [ lnk-mbed-pcconnect] dispositivo mbed tooyour di tooconfigure porta seriale accesso.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Creare un progetto mbed e importare il codice di esempio hello

Seguire questi passaggi tooadd un progetto di esempio codice tooan mbed. Importare il progetto di avvio di hello remoto monitoraggio e quindi modificare hello toouse di hello progetto protocollo MQTT anziché hello protocollo AMQP. Attualmente, è necessario toouse hello MQTT protocollo toouse hello dispositivo funzionalità di gestione di IoT Hub.

1. Nel web browser, visitare toohello mbed.org [sito per sviluppatori](https://developer.mbed.org/). Se si è ancora iscritti, viene visualizzato un toocreate opzione account (è disponibile). In caso contrario, accedere con le credenziali dell'account. Quindi fare clic su **compilatore** in hello nell'angolo superiore destro della pagina hello. Questa azione consente di toohello *dell'area di lavoro* interfaccia.

1. Assicurarsi che piattaforma hardware hello in uso nella hello nell'angolo superiore destro della finestra hello, oppure fare clic sull'icona di hello in hello nell'angolo destro tooselect la piattaforma hardware.

1. Fare clic su **importazione** nel menu principale di hello. Quindi fare clic su **fare clic qui tooimport dall'URL**.
   
    ![Avviare l'importazione dell'area di lavoro toombed][6]

1. Nella finestra popup hello, immettere il collegamento hello per hello esempio codice https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, quindi fare clic su **importazione**.
   
    ![Importare l'area di lavoro di esempio codice toombed][7]

1. È possibile visualizzare nella finestra di hello mbed del compilatore che l'importazione di questo progetto Importa anche diverse librerie. Alcuni sono forniti e gestiti dal team di Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), mentre altri sono disponibili nel catalogo di librerie mbed hello librerie di terze parti.
   
    ![Visualizzare il progetto mbed][8]

1. In hello **programma dell'area di lavoro**, hello rapida **hub IOT\_amqp\_trasporto** libreria, fare clic su **eliminare**, quindi fare clic su **OK** tooconfirm.

1. In hello **programma dell'area di lavoro**, hello rapida **azure\_amqp\_c** libreria, fare clic su **eliminare**, quindi fare clic su **OK**  tooconfirm.

1. Pulsante destro del mouse hello **remote_monitoring** progetto in hello **programma dell'area di lavoro**selezionare **libreria di importazione**, quindi selezionare **From URL**.
   
    ![Avviare l'area di lavoro toombed importazione libreria][6]

1. Nella finestra popup hello, immettere il collegamento hello per hello MQTT trasporto libreria https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_trasporto / quindi fare clic su **importazione**.
   
    ![Importare l'area di lavoro libreria toombed][12]

1. Hello ripetere il passaggio tooadd hello MQTT libreria precedente da https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. L'area di lavoro è ora simile hello seguenti:

    ![Visualizzare l'area di lavoro mbed][13]

1. Aprire hello remoto\_monitoring\remote_monitoring.c file e sostituire hello esistente `#include` istruzioni con hello seguente codice:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Eliminare tutti hello rimanenti codice hello remoto\_monitoring\remote\_monitoring.c file.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilare ed eseguire l'esempio hello

Aggiungere hello tooinvoke codice **remoto\_monitoraggio\_eseguire** funzione e quindi compilare ed eseguire un'applicazione hello dispositivo.

1. Aggiungere un **principale** funzione con il codice seguente alla fine hello hello remoto\_hello tooinvoke di file monitoring.c **remoto\_monitoraggio\_eseguire** funzione:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Fare clic su **compilare** programma hello toobuild. È possibile in modo sicuro ignorare eventuali avvisi, ma se la compilazione hello genera errori, risolverli prima di procedere.

1. Se la compilazione hello ha esito positivo, sito Web di hello mbed del compilatore genera un file con estensione bin con il nome di hello del progetto e lo scarica tooyour di computer locale. Dispositivo di toohello file con estensione bin hello copia. Il salvataggio di dispositivo toohello di file con estensione bin hello causa toorestart dispositivo hello ed esegue il programma hello contenuto nel file con estensione bin hello. È possibile riavviare manualmente il programma hello in qualsiasi momento premendo il pulsante di reimpostazione hello sul dispositivo mbed hello.

1. Connettere il dispositivo toohello usando un'applicazione client SSH, ad esempio PuTTY. È possibile determinare il dispositivo utilizza controllando Gestione dispositivi di Windows della porta seriale hello.
   
    ![][11]

1. In PuTTY, fare clic su hello **seriale** tipo di connessione. in genere si connette il dispositivo Hello 9600 baud, quindi immettere 9600 hello **velocità** casella. Fare quindi clic su **Apri**.

1. programma Hello avvia l'esecuzione. È possibile che Lavagna hello tooreset (premere CTRL + INTERR o un pulsante di reimpostazione della Lavagna hello premere) se il programma di hello non viene avviato automaticamente quando ci si connette.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
