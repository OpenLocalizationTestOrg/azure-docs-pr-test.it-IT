> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Introduzione

In [introduzione gemelli dispositivo IoT Hub][lnk-twin-tutorial], si è appreso come metadati del dispositivo tooset dalla soluzione nuovamente comporta l'utilizzo di *tag*, segnalare le condizioni di dispositivo da un'app del dispositivo utilizzando *segnalati proprietà*ed eseguire query su queste informazioni tramite un linguaggio simile a SQL.

In questa esercitazione si apprenderà come toouse hello del doppi dispositivo hello *le proprietà desiderate* insieme a *segnalati proprietà*, tooremotely configurare App per dispositivi. In particolare, questa esercitazione viene illustrato come una coppia di dispositivo segnalati e le proprietà desiderate abilitare una configurazione di più passaggi di un'applicazione per dispositivi e forniscano hello visibilità toohello soluzione back-end di stato hello di questa operazione in tutti i dispositivi. È possibile trovare ulteriori informazioni sul ruolo hello di configurazioni di dispositivo in [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-dm-overview].

In generale, l'utilizzo di gemelli dispositivo consente hello soluzione back-end toospecify hello configurazione desiderata per i dispositivi gestito hello, anziché inviare comandi specifici. In questo modo il dispositivo hello responsabile della configurazione tooupdate modo migliore hello relativa configurazione (molto importante in scenari IoT in condizioni di dispositivo specifico influire sul hello possibilità tooimmediately eseguire determinati comandi) durante la restituzione continuamente toohello stato corrente di hello e potenziali condizioni di errore del processo di aggiornamento hello di fine soluzione nuovamente. Questo modello è strumentale toohello gestione di grandi set di dispositivi, poiché consente hello soluzione back-end toohave completa visibilità dello stato di hello del processo di configurazione hello in tutti i dispositivi.

> [!NOTE]
> Negli scenari in cui i dispositivi sono controllati in modo più interattivo (come nel caso dell'attivazione di una ventola da un'app controllata dall'utente), può essere opportuno usare [metodi diretti][lnk-methods].
> 
> 

In questa esercitazione, modifiche di back-end di soluzione hello configurazione di telemetria hello di un dispositivo di destinazione e, in seguito che app per dispositivi hello segue tooapply un processo in più passaggi una configurazione di aggiornamento (ad esempio, che richiedono il riavvio modulo software, quale l'oggetto esercitazione simula con un ritardo semplice).

back-end di Hello soluzione memorizza la configurazione di hello nelle proprietà desiderato del doppi dispositivo hello hello seguente modo:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Poiché le configurazioni possono essere oggetti complessi, in genere vengono assegnati un ID univoco (hash o [GUID][lnk-guid]) toosimplify i confronti.
> 
> 

app per dispositivi Hello segnala la configurazione corrente del mirroring proprietà hello desiderato **telemetryConfig** in hello segnalati proprietà:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Si noti la modalità di segnalazione hello **telemetryConfig** ha una proprietà aggiuntiva **stato**, stato hello tooreport del processo di aggiornamento configurazione hello utilizzato.

Quando viene ricevuta una nuova configurazione desiderata, hello dispositivo app segnala una configurazione in sospeso modificando hello informazioni:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Quindi, in un secondo momento, hello dispositivo app segnalerà hello riuscita o meno dell'operazione aggiornando hello di sopra di proprietà.
Si noti come back-end di hello soluzione è in grado di, in qualsiasi momento, lo stato di hello tooquery del processo di configurazione hello in tutti i dispositivi di hello.

Questa esercitazione illustra come:

* Creare un'app dispositivo simulato che riceve gli aggiornamenti della configurazione dal back-end di soluzione hello e report più aggiornamenti come *segnalati proprietà* configurazione hello processo di aggiornamento.
* Creare un'app di back-end che gli aggiornamenti hello configurazione desiderata di un dispositivo e quindi query hello il processo di aggiornamento di configurazione.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
