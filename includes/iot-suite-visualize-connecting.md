## <a name="view-device-telemetry-in-hello-dashboard"></a>Telemetria di dispositivo di visualizzazione nel dashboard di hello
dashboard di Hello in hello Abilita soluzione si tooview hello telemetria tooIoT Hub di inviare i dispositivi di monitoraggio remoto.

1. Nel browser, toohello restituito remoto soluzione dashboard di monitoraggio, fare clic su **dispositivi** in hello pannello sinistro toonavigate toohello **elenco dispositivi**.
2. In hello **elenco dispositivi**, si dovrebbe essere stato hello del dispositivo **esecuzione**. In caso contrario, fare clic su **abilitare dispositivo** in hello **dettagli dispositivo** pannello.
   
    ![Visualizzare lo stato dei dispositivi][18]
3. Fare clic su **Dashboard** tooreturn toohello dashboard, selezionare il dispositivo in hello **dispositivo tooView** tooview elenco a discesa la telemetria. la telemetria Hello dall'applicazione di esempio hello è 50 unità per la temperatura, 55 unità esterne temperatura e 50 unità per umidità.
   
    ![Visualizzare la telemetria dei dispositivi][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>Richiamare un metodo sul dispositivo
dashboard Hello nella soluzione di monitoraggio remoto hello consente metodi tooinvoke nei dispositivi tramite IoT Hub. Nella soluzione di monitoraggio remoto hello, ad esempio, è possibile richiamare un metodo toosimulate il riavvio di un dispositivo.

1. In hello remoto soluzione dashboard di monitoraggio, fare clic su **dispositivi** in hello pannello sinistro toonavigate toohello **elenco dispositivi**.
2. Fare clic su **ID dispositivo** per il dispositivo in hello **elenco dispositivi**.
3. In hello **dettagli dispositivo** pannello, fare clic su **metodi**.
   
    ![Metodi per il dispositivo][13]
4. In hello **metodo** elenco a discesa, selezionare **InitiateFirmwareUpdate**, quindi nel **FWPACKAGEURI** immettere un URL fittizio. Fare clic su **Richiama metodo** metodo hello toocall sul dispositivo hello.
   
    ![Richiamare un metodo per il dispositivo][14]
   

5. Viene visualizzato un messaggio nella console di hello in esecuzione il codice del dispositivo quando il dispositivo hello gestisce metodo hello. risultati di Hello del metodo hello vengono aggiunti toohello cronologia nel portale di soluzione hello:

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="next-steps"></a>Passaggi successivi
articolo Hello [personalizzazione preconfigurato soluzioni] [ lnk-customize] vengono descritte alcune differenze, è possibile estendere questo esempio. Le estensioni possibili comprendono l'utilizzo di sensori reali e implementazione di comandi aggiuntivi.

È possibile approfondire hello [le autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
