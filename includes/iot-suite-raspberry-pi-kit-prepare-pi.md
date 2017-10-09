## <a name="prepare-your-raspberry-pi"></a>Preparare Raspberry Pi

### <a name="install-raspbian"></a>Installare Raspbian

Se si tratta di hello prima volta che si utilizza l'installazione guidata piattaforma Raspberry, è necessario del sistema operativo Raspbian hello tooinstall utilizzando NOOBS nella scheda SD hello inclusa nel kit di hello. Hello [Raspberry Pi Software Guida] [ lnk-install-raspbian] viene descritto come un sistema operativo nelle Pi Raspberry tooinstall. In questa esercitazione si presuppone che è stato installato hello Raspbian del sistema operativo del Pi Raspberry.

> [!NOTE]
> scheda SD Hello inclusa nella hello [Microsoft Azure IoT Starter Kit per 3 Pi Raspberry] [ lnk-starter-kits] NOOBS installato esiste già. È possibile avviare hello Pi Raspberry da questa scheda e scegliere tooinstall hello Raspbian OS.

### <a name="set-up-hello-hardware"></a>Configurare l'hardware hello

Questa esercitazione viene utilizzato il sensore hello BME280 incluso in hello [Microsoft Azure IoT Starter Kit per 3 Pi Raspberry] [ lnk-starter-kits] toogenerate i dati di telemetria. Usa un tooindicate LED quando hello Pi Raspberry elabora una chiamata al metodo dal dashboard di soluzione hello.

componenti di Hello nella Lavagna Pane hello sono:

- LED rosso
- Resistore da 220 Ohm (rosso, rosso, marrone)
- Sensore BME280

diagramma Hello seguente mostra come tooconnect hardware:

![Configurazione hardware per Raspberry Pi][img-connection-diagram]

Hello nella tabella seguente vengono riepilogate le connessioni hello dai componenti di toohello Raspberry Pi hello in breadboard hello:

| Raspberry Pi            | Breadboard             |Colore         |
| ----------------------- | ---------------------- | ------------- |
| GND (Pin 14)            | LED -ve pin (18A)      | Viola          |
| GPCLK0 (Pin 7)          | Resistore (25A)         | Arancione          |
| SPI_CE0 (Pin 24)        | CS (39A)               | Blu          |
| SPI_SCLK (Pin 23)       | SCK (36A)              | Giallo        |
| SPI_MISO (Pin 21)       | SDO (37A)              | Bianco         |
| SPI_MOSI (Pin 19)       | SDI (38A)              | Verde         |
| GND (Pin 6)             | GND (35A)              | Nero         |
| 3.3 V (Pin 1)           | 3Vo (34A)              | Rosso           |

l'installazione di toocomplete hello hardware, è necessario:

- Collegare l'alimentazione elettrica toohello Raspberry Pi inclusa nel kit di hello.
- Connettere la rete di tooyour Raspberry Pi tramite cavo Ethernet hello incluso con il kit. In alternativa, è possibile configurare la [connettività wireless][lnk-pi-wireless] per Raspberry Pi.

È stata completata l'installazione dell'hardware del pi greco Raspberry hello.

### <a name="sign-in-and-access-hello-terminal"></a>Accesso e terminal hello

Sono presenti due opzioni tooaccess un ambiente terminal le Pi Raspberry:

- Se si dispone di una tastiera e monitorare connesso tooyour Raspberry Pi, è possibile utilizzare hello GUI Raspbian tooaccess una finestra terminale.

- Riga di comando hello accesso con le pi greco Raspberry tramite SSH nel computer desktop.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utilizzare una finestra terminal in hello GUI

le credenziali predefinite Hello per Raspbian sono username **pi** e la password **raspberry**. Nella barra delle applicazioni hello in hello GUI, è possibile avviare hello **Terminal** utilità utilizzando l'icona di hello simile a un monitoraggio.

#### <a name="sign-in-with-ssh"></a>Accedere con SSH

È possibile utilizzare SSH per l'accesso da riga di comando tooyour Raspberry Pi. articolo Hello [SSH (Secure Shell)] [ lnk-pi-ssh] viene descritto come tooconfigure SSH sul pi greco Raspberry e come tooconnect da [Windows] [ lnk-ssh-windows] o [Linux e Mac OS][lnk-ssh-linux].

Accedere con il nome utente **pi** e la password **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Facoltativo: condividere una cartella in Raspberry Pi

Facoltativamente, è opportuno tooshare una cartella con il pi greco Raspberry con l'ambiente desktop. Condivisione di una cartella consente di toouse editor di testo preferito di desktop (ad esempio [codice di Visual Studio](https://code.visualstudio.com/) o [testo Sublime](http://www.sublimetext.com/)) file tooedit le Pi Raspberry anziché `nano` o `vi`.

tooshare una cartella con Windows, configurare un server Samba su hello Raspberry Pi. In alternativa, utilizzare hello incorporato [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server con un client SFTP sul desktop.

### <a name="enable-spi"></a>Abilitare SPI

Prima di eseguire l'applicazione di esempio hello, è necessario abilitare bus seriale periferiche interfaccia SPI () hello hello Raspberry Pi. Hello Pi Raspberry comunica con dispositivo di hello BME280 sensore tramite bus SPI hello. Utilizzare i seguenti file di configurazione di comando tooedit hello hello:

```sh
sudo nano /boot/config.txt
```

Individuare la riga hello:

`#dtparam=spi=on`

- riga hello toouncomment, hello di eliminazione `#` all'inizio di hello.
- Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).
- tooenable SPI, riavviare hello Raspberry Pi. Il riavvio si disconnette terminal hello, è necessario toosign in nuovamente al riavvio di hello Raspberry Pi:

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/