> [!div class="op_single_selector"]
> * [C su Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C su Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.JS](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

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

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/