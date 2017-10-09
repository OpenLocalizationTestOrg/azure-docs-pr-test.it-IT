> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Questo articolo fornisce una descrizione dettagliata di hello [codice di esempio Hello World] [ lnk-helloworld-sample] tooillustrate componenti fondamentali di hello di hello [Azure IoT Edge] [ lnk-iot-edge] architettura. Hello esempio utilizza hello Azure IoT Edge toobuild un gateway semplice che consente di registrare un file di tooa messaggio "hello world" ogni cinque secondi.

In questa procedura dettagliata verranno trattati i seguenti argomenti:

* **Architettura di esempio World Hello**: descrive come [concetti dell'architettura di Azure IoT Edge] [ lnk-edge-concepts] si applicano all'esempio Hello World toohello e la modalità di interazione fra di hello componenti.
* **Come toobuild hello esempio**: esempio hello toobuild necessari passaggi di hello.
* **Come toorun hello esempio**: esempio hello toorun necessari passaggi di hello. 
* **Output tipico**: un esempio di hello output tooexpect quando si esegue l'esempio hello.
* **Frammenti di codice**: una raccolta di tooshow di frammenti di codice come esempio hello World Hello implementa i componenti di gateway di IoT Edge di chiave.


## <a name="hello-world-sample-architecture"></a>Architettura di esempio Hello World
esempio Hello World Hello illustra i concetti di hello descritti nella sezione precedente hello. esempio Hello World Hello implementa un gateway perimetrale di IoT che dispone di una pipeline costituita da due moduli IoT Edge:

* Hello *HelloWorld* modulo Crea un messaggio ogni cinque secondi e lo passa a modulo logger toohello.
* Hello *logger* modulo scritture hello i messaggi ricevuti tooa file.

![Architettura dell'esempio Hello World compilato con Azure IoT Edge][4]

Come descritto nella sezione precedente di hello, hello World Hello modulo non fa passare messaggi direttamente modulo logger toohello ogni cinque secondi. Al contrario, pubblica un gestore di messaggi toohello ogni cinque secondi.

modulo di logger Hello riceve il messaggio hello dal broker hello e agisce su di esso, scrivere il contenuto del file di tooa hello messaggio hello.

modulo di logger Hello utilizza solo i messaggi da Service broker hello, non pubblicarlo mai broker di toohello nuovi messaggi.

![Come broker hello indirizza i messaggi tra i moduli in Azure IoT Edge][5]

Hello figura precedente hello architettura di esempio hello World Hello e i percorsi relativi hello toohello i file di origine che implementano le parti diverse dell'esempio hello in hello [repository][lnk-iot-edge]. Esplorare il codice hello autonomamente oppure usare frammenti di codice hello seguente come guida.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md