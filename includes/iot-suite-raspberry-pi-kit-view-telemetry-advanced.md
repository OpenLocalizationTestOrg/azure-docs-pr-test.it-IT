## <a name="view-hello-telemetry"></a>Visualizzazione hello telemetria

soluzione di monitoraggio remoto di dati di telemetria toohello ora invia Hello Raspberry Pi. È possibile visualizzare i dati di telemetria hello nel dashboard di soluzione hello. È anche possibile inviare messaggi tooyour Pi Raspberry dal dashboard di soluzione hello.

- Passare il dashboard di soluzione toohello.
- Selezionare il dispositivo in hello **tooView dispositivo** elenco a discesa.
- telemetria Hello da hello Pi Raspberry vengono visualizzati nel dashboard di hello.

![Visualizzare i dati di telemetria da hello Raspberry Pi][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a>Avviare l'aggiornamento del firmware hello

processo di aggiornamento del firmware Hello Scarica e installa una versione aggiornata dell'applicazione client di dispositivo hello nel hello Raspberry Pi. Per ulteriori informazioni sul processo di aggiornamento del firmware hello, vedere la descrizione di hello del criterio di aggiornamento del firmware hello in [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-update-pattern].

Processo di aggiornamento del firmware hello è avviare richiamando un metodo nel dispositivo hello. Questo metodo è asincrono e restituisce appena inizia il processo di aggiornamento hello. utilizza dispositivo Hello segnalate soluzione hello toonotify di proprietà relative stato hello hello aggiornamento.

Per richiamare metodi sulle Pi Raspberry dal dashboard di soluzione hello. Hello Pi Raspberry si connette innanzitutto toohello soluzione di monitoraggio remoto, invia informazioni sui metodi di hello che supporta. 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
