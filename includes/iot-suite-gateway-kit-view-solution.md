## <a name="view-hello-solution-dashboard"></a>Dashboard di soluzione hello View

dashboard di soluzione Hello consente soluzione hello distribuito toomanage. Ad esempio, è possibile visualizzare dati di telemetria, aggiungere dispositivi e richiamare metodi.

1. Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen il portale soluzione di monitoraggio remoto in una nuova scheda.

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*. Passare tooother aree del portale di soluzione hello utilizzando il menu di hello nella parte sinistra della pagina hello hello.

    ![Dashboard della soluzione preconfigurata per il monitoraggio remoto][img-menu]

## <a name="add-a-device"></a>Aggiungere un dispositivo

Per una soluzione di dispositivo tooconnect toohello preconfigurato, deve identificarsi tooIoT Hub usando credenziali valide. È possibile recuperare le credenziali di dispositivo hello dal dashboard di soluzione hello. Includere le credenziali di dispositivo hello nell'applicazione client più avanti in questa esercitazione.

tooadd una soluzione di monitoraggio remoto tooyour di dispositivo, hello completo seguendo i passaggi nel dashboard di soluzione hello:

1. Hello angolo in basso a sinistra del dashboard hello, fare clic su **aggiunge un dispositivo**.

   ![Aggiungere un dispositivo][1]

1. In hello **dispositivo personalizzato** pannello, fare clic su **Aggiungi nuovo**.

   ![Aggiungere un dispositivo personalizzato][2]

1. Scegliere **Let me define my own Device ID** (Desidero definire il mio ID dispositivo). Immettere un ID dispositivo, ad esempio **device01**, fare clic su **ID controllo** tooverify nome hello non hai già utilizzato nella soluzione e quindi fare clic su **crea** dispositivo hello tooprovision.

   ![Aggiungere un ID dispositivo][3]

1. Rendere le credenziali di un dispositivo di hello nota (**ID dispositivo**, **Hostname Hub IoT**, e **chiave dispositivo**). L'applicazione client in hello NUC Intel deve questi toohello tooconnect valori soluzione di monitoraggio remoto. Fare quindi clic su **Done**.

    ![Vedere le credenziali del dispositivo][4]

1. Selezionare il dispositivo nell'elenco di dispositivi hello nel dashboard di soluzione hello. Quindi, nel hello **dettagli dispositivo** pannello, fare clic su **Abilita periferica**. lo stato di Hello del dispositivo è ora **esecuzione**. soluzione di monitoraggio remoto Hello possa ora ricevere i dati di telemetria dal dispositivo e richiamare metodi sul dispositivo hello.

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png