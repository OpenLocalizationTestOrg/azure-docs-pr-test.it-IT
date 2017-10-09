## <a name="view-hello-telemetry"></a>Visualizzazione hello telemetria

soluzione di monitoraggio remoto di dati di telemetria toohello ora invia Hello Raspberry Pi. È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello. È anche possibile inviare messaggi tooyour Pi Raspberry dal dashboard di soluzione hello.

- Passare il dashboard di soluzione toohello.
- Selezionare il dispositivo in hello **tooView dispositivo** elenco a discesa.
- telemetria Hello da hello Pi Raspberry vengono visualizzati nel dashboard di hello.

![Visualizzare i dati di telemetria da hello Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a>Agire sul dispositivo hello

Dal dashboard di soluzione hello, è possibile richiamare metodi sulle Pi Raspberry. Quando hello Pi Raspberry si connette toohello soluzione di monitoraggio remoto, invia informazioni sui metodi di hello che supporta.

- Nel dashboard di soluzione hello, fare clic su **dispositivi** toovisit hello **dispositivi** pagina. Selezionare le Pi Raspberry hello **elenco dei dispositivi**. Quindi scegliere **Metodi**:

    ![Elencare i dispositivi nel dashboard][img-list-devices]

- In hello **Richiama metodo** pagina, scegliere **LightBlink** in hello **metodo** elenco a discesa.

- Scegliere **InvokeMethod**. simulatore Hello viene stampato un messaggio nella console di hello in hello Raspberry Pi. app Hello in hello Pi Raspberry invia un dashboard di soluzione toohello indietro riconoscimento:

    ![Visualizzare la cronologia del metodo][img-method-history]

- È possibile passare il LED di hello e disattivare utilizzando hello **ChangeLightStatus** metodo con un **LightStatusValue** impostare troppo**1** per su o **0** per disattivare.

> [!WARNING]
> Se si lascia in esecuzione nell'account di Azure di soluzione di monitoraggio remoto hello, verrà addebitato per volta hello che è in esecuzione. Per ulteriori informazioni sulla riduzione del consumo durante l'esecuzione di soluzioni di monitoraggio remoto hello, vedere [configurazione Azure IoT Suite preconfigurato soluzioni per scopi dimostrativi][lnk-demo-config]. Eliminare la soluzione hello preconfigurato dall'account di Azure al termine dell'utilizzo.


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md