## <a name="customize-and-extend-hello-device-management-actions"></a>Personalizzare ed estendere le azioni di gestione dispositivo hello

Le soluzioni IoT possono espandere hello definito set di modelli di gestione di dispositivi o abilitare modelli personalizzati utilizzando un doppio dispositivo hello e primitive metodo cloud a dispositivo. Altri esempi di operazioni di gestione dei dispositivi includono il ripristino delle informazioni predefinite, l'aggiornamento del firmware, l'aggiornamento del software, il risparmio energia, la gestione di rete e connettività e la crittografia dei dati.

## <a name="device-maintenance-windows"></a>Finestre di manutenzione del dispositivo

In genere, configurare azioni tooperform dispositivi in una fase che riduce al minimo le interruzioni e tempi di inattività. Finestre di manutenzione di dispositivo sono un modello di uso comune toodefine hello quando un dispositivo deve aggiornare la configurazione. Le soluzioni di back-end possono utilizzare le proprietà di hello desiderato di hello dispositivo doppi toodefine e attivare un criterio del dispositivo che consente una finestra di manutenzione. Quando un dispositivo riceve i criteri di finestra di manutenzione hello, può utilizzare hello segnalati proprietà hello doppi tooreport hello dello stato dei dispositivi di criteri di hello. app di back-end Hello è quindi possibile utilizzare dispositivo doppi query tooattest toocompliance di dispositivi e tutti i criteri.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato utilizzato un tootrigger dirette del metodo, riavviare il computer remoto in un dispositivo. È utilizzato hello proprietà segnalati tooreport hello riavviare ultima volta da dispositivo hello e hello toodiscover gemelli di hello richiesto dispositivo riavviare ultima ora del dispositivo hello dal cloud hello.

toocontinue introduzione IoT Hub e modelli di gestione di dispositivi, ad esempio remoto tramite l'aggiornamento del firmware di hello air, vedere:

[Esercitazione: Come toodo un aggiornamento firmware][lnk-fwupdate]

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

Introduzione a IoT Hub, toocontinue vedere [Guida introduttiva a bordo IoT][lnk-iot-edge].

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md