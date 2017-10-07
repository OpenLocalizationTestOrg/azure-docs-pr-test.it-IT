---
title: aaaAzure IoT Suite e logica App | Documenti Microsoft
description: Un'esercitazione sulla toohook di App per la logica tooAzure IoT Suite per il processo di business.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Esercitazione: Connessione logica App tooyour Azure IoT Suite remoto preconfigurato soluzione di monitoraggio
Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] soluzione preconfigurata di monitoraggio remoto è tooget un modo utile per iniziare rapidamente con un set di funzionalità end-to-end per semplificare la soluzione IoT. In questa esercitazione viene illustrato come tooadd logica App tooyour Microsoft Azure IoT Suite monitoraggio remoto preconfigurato soluzione. In questa procedura viene illustrano soluzione IoT ulteriormente connettendola tooa processo di business.

*Se si sta cercando una procedura dettagliata su come un'operazione di monitoraggio remoto tooprovision preconfigurato soluzione, vedere [esercitazione: Introduzione a soluzioni IoT preconfigurato hello][lnk-getstarted].*

Prima di iniziare questa esercitazione, è necessario:

* Monitoraggio remoto di eseguire il provisioning hello preconfigurato soluzione nella sottoscrizione di Azure.
* Creare un tooenable di account di SendGrid è toosend un messaggio di posta elettronica che attiva il processo di business. È possibile richiedere un account di valutazione gratuito accedendo al sito Web [SendGrid](https://sendgrid.com/) e facendo clic su **Try for Free**(Prova gratuitamente). Dopo avere registrato per l'account di valutazione gratuita, è necessario toocreate un [chiave API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid che concede le autorizzazioni di posta elettronica toosend. Questa chiave API è necessario più avanti nell'esercitazione di hello.

toocomplete questa esercitazione, è necessario Visual Studio 2015 o Visual Studio 2017 azioni hello toomodify nel back-end di hello soluzione preconfigurata.

Supponendo che è già stato effettuato il provisioning del monitoraggio remoto preconfigurato soluzione, passare il gruppo di risorse toohello per tale soluzione di hello [portale di Azure][lnk-azureportal]. gruppo di risorse Hello è hello stesso nome come hello soluzione nome scelto quando è stato eseguito il provisioning la soluzione di monitoraggio remota. Nel gruppo di risorse hello, è possibile visualizzare tutti hello il provisioning delle risorse di Azure per la soluzione, ad eccezione dell'applicazione Azure Active Directory che è possibile trovare nel portale di Azure classico hello hello. Hello schermata riportata di seguito viene illustrato un esempio **gruppo di risorse** pannello per un'operazione di monitoraggio remoto preconfigurato soluzione:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, impostare hello logica app toouse con hello preconfigurato soluzione.

## <a name="set-up-hello-logic-app"></a>Impostare hello logica App
1. Fare clic su **Aggiungi** nella parte superiore di hello del Pannello di gruppo risorsa nel portale di Azure hello.
2. Cercare **App per la logica**, farci clic e quindi scegliere **Crea**.
3. Compilare hello **nome** e utilizzare hello stesso **sottoscrizione** e **gruppo di risorse** utilizzato quando è stato effettuato il provisioning la soluzione di monitoraggio remota. Fare clic su **Crea**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. Al termine della distribuzione, è possibile visualizzare hello che App per la logica è elencato come risorsa nel gruppo di risorse.
5. Fare clic su hello logica App toonavigate toohello pannello App logica, seleziona hello **App vuota per la logica** hello tooopen modello **logica App progettazione**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Selezionare **Richiesta**. Questa azione specifica che una richiesta HTTP in ingresso con uno specifico payload in formato JSON agisce come trigger.
7. Incollare hello seguente di codice in hello dello Schema JSON del corpo della richiesta:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > È possibile copiare URL hello per post HTTP hello dopo il salvataggio hello logica app, ma è innanzitutto necessario aggiungere un'azione.
   > 
   > 
8. Fare clic su **+ Nuovo passaggio** nel trigger manuale. Fare quindi clic su **Aggiungi un'azione**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Cercare **SendGrid - Send email** (SendGrid - Invia messaggio di posta elettronica) e fare clic.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Immettere un nome per la connessione hello, ad esempio **SendGridConnection**, immettere hello **chiave API SendGrid** creato quando si imposta l'account di SendGrid e fare clic su **crea**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Aggiungere indirizzi di posta elettronica è proprio tooboth hello **da** e **a** campi. Aggiungere **avviso di monitoraggio remoto [DeviceId]** toohello **soggetto** campo. In hello **corpo del messaggio di posta elettronica** campo, aggiungere **dispositivo [DeviceId] ha segnalato [measurementName] con valore [measuredValue].** È possibile aggiungere **[DeviceId]**, **[measurementName]**, e **[measuredValue]** facendo hello **è possibile inserire i dati nei passaggi precedenti**sezione.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Fare clic su **salvare** nel menu superiore hello.
13. Fare clic su hello **richiesta** hello trigger e copia **Http Post toothis URL** valore. Questo URL sarà necessario più avanti nell'esercitazione.

> [!NOTE]
> Logica App consentono di toorun [molti tipi diversi di azione] [ lnk-logic-apps-actions] incluse azioni in Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Impostare hello processo Web EventProcessor
In questa sezione è connettersi il toohello soluzione preconfigurata logica App è stato creato. toocomplete questa attività, si aggiunge hello tootrigger hello logica App toohello azione URL che viene generato quando un valore del sensore dispositivo supera una soglia.

1. Utilizzare la git client tooclone hello più recente versione di hello [azure iot-remoto monitoraggio repository github][lnk-rmgithub]. ad esempio:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. In Visual Studio, aprire hello **RemoteMonitoring.sln** copia locale di hello del repository hello.
3. Aprire hello **ActionRepository.cs** file hello **infrastruttura\\Repository** cartella.
4. Hello aggiornamento **actionIds** dizionario con hello **Http Post toothis URL** indicato dall'App logica come indicato di seguito:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Salvare le modifiche di hello nella soluzione e uscire da Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Distribuzione dalla riga di comando hello
In questa sezione, si distribuisce la versione aggiornata di hello remoto monitoraggio tooreplace hello versione della soluzione attualmente in esecuzione in Azure.

1. In seguito hello [configurazione dev] [ lnk-devsetup] tooset istruzioni dell'ambiente per la distribuzione.
2. toodeploy in locale, seguire hello [distribuzione locale] [ lnk-localdeploy] istruzioni.
3. toodeploy toohello cloud e aggiornare la distribuzione cloud esistente, seguire hello [distribuzione cloud] [ lnk-clouddeploy] istruzioni. Utilizzare il nome di hello della distribuzione originale come nome della distribuzione hello. Ad esempio se è stata chiamata distribuzione originale hello **demologicapp**, utilizzare hello comando seguente:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Quando viene eseguito lo script di compilazione hello, prestare attenzione toouse hello stesso account Azure, sottoscrizione, area e istanza di Active Directory è utilizzata quando è stato effettuato il provisioning soluzione hello.

## <a name="see-your-logic-app-in-action"></a>App per la logica in azione
Hello soluzione preconfigurata di monitoraggio remoto dispone di due regole impostate per impostazione predefinita quando si esegue il provisioning di una soluzione. Entrambe le regole presenti hello **SampleDevice001** dispositivo:

* Temperature > 38.00
* Humidity > 48.00

regola di temperatura Hello attiva hello **generare allarme** azione e hello regola umidità attiva hello **SendMessage** azione. Presupponendo che utilizzate hello stesso URL per entrambi hello azioni **ActionRepository** classe, i trigger di app logica per una regola. Entrambe le regole di utilizzano SendGrid toosend toohello un messaggio di posta elettronica **a** indirizzo con i dettagli dell'avviso hello.

> [!NOTE]
> Hello logica App continua tootrigger ogni volta che viene raggiunta la soglia di hello. tooavoid email non necessarie, è possibile disattivare le regole di hello nella soluzione portale o disabilitare Ciao logica App hello [portale di Azure][lnk-azureportal].
> 
> 

Inoltre tooreceiving messaggi di posta elettronica, è possibile anche visualizzare quando viene eseguito hello logica App nel portale di hello:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato utilizzato un processo di business tooa logica App tooconnect hello preconfigurato soluzione, è possibile ulteriori informazioni sulle opzioni di hello per personalizzare soluzioni preconfigurata hello:

* [Utilizzare i dati di telemetria dinamico con hello soluzione preconfigurata di monitoraggio remoto][lnk-dynamic]
* [Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
