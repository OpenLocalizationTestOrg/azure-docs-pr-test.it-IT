## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="9cdde-101">Preparare Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9cdde-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="9cdde-102">Installare Raspbian</span><span class="sxs-lookup"><span data-stu-id="9cdde-102">Install Raspbian</span></span>

<span data-ttu-id="9cdde-103">Se si tratta di hello prima volta che si utilizza l'installazione guidata piattaforma Raspberry, è necessario del sistema operativo Raspbian hello tooinstall utilizzando NOOBS nella scheda SD hello inclusa nel kit di hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="9cdde-104">Hello [Raspberry Pi Software Guida] [ lnk-install-raspbian] viene descritto come un sistema operativo nelle Pi Raspberry tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9cdde-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="9cdde-105">In questa esercitazione si presuppone che è stato installato hello Raspbian del sistema operativo del Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="9cdde-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="9cdde-106">scheda SD Hello inclusa nella hello [Microsoft Azure IoT Starter Kit per 3 Pi Raspberry] [ lnk-starter-kits] NOOBS installato esiste già.</span><span class="sxs-lookup"><span data-stu-id="9cdde-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="9cdde-107">È possibile avviare hello Pi Raspberry da questa scheda e scegliere tooinstall hello Raspbian OS.</span><span class="sxs-lookup"><span data-stu-id="9cdde-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="9cdde-108">Configurare l'hardware hello</span><span class="sxs-lookup"><span data-stu-id="9cdde-108">Set up hello hardware</span></span>

<span data-ttu-id="9cdde-109">Questa esercitazione viene utilizzato il sensore hello BME280 incluso in hello [Microsoft Azure IoT Starter Kit per 3 Pi Raspberry] [ lnk-starter-kits] toogenerate i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="9cdde-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="9cdde-110">Usa un tooindicate LED quando hello Pi Raspberry elabora una chiamata al metodo dal dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="9cdde-111">componenti di Hello nella Lavagna Pane hello sono:</span><span class="sxs-lookup"><span data-stu-id="9cdde-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="9cdde-112">LED rosso</span><span class="sxs-lookup"><span data-stu-id="9cdde-112">Red LED</span></span>
- <span data-ttu-id="9cdde-113">Resistore da 220 Ohm (rosso, rosso, marrone)</span><span class="sxs-lookup"><span data-stu-id="9cdde-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="9cdde-114">Sensore BME280</span><span class="sxs-lookup"><span data-stu-id="9cdde-114">BME280 sensor</span></span>

<span data-ttu-id="9cdde-115">diagramma Hello seguente mostra come tooconnect hardware:</span><span class="sxs-lookup"><span data-stu-id="9cdde-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Configurazione hardware per Raspberry Pi][img-connection-diagram]

<span data-ttu-id="9cdde-117">Hello nella tabella seguente vengono riepilogate le connessioni hello dai componenti di toohello Raspberry Pi hello in breadboard hello:</span><span class="sxs-lookup"><span data-stu-id="9cdde-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="9cdde-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9cdde-118">Raspberry Pi</span></span>            | <span data-ttu-id="9cdde-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="9cdde-119">Breadboard</span></span>             |<span data-ttu-id="9cdde-120">Colore</span><span class="sxs-lookup"><span data-stu-id="9cdde-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="9cdde-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="9cdde-121">GND (Pin 14)</span></span>            | <span data-ttu-id="9cdde-122">LED -ve pin (18A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="9cdde-123">Viola</span><span class="sxs-lookup"><span data-stu-id="9cdde-123">Purple</span></span>          |
| <span data-ttu-id="9cdde-124">GPCLK0 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="9cdde-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="9cdde-125">Resistore (25A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-125">Resistor (25A)</span></span>         | <span data-ttu-id="9cdde-126">Arancione</span><span class="sxs-lookup"><span data-stu-id="9cdde-126">Orange</span></span>          |
| <span data-ttu-id="9cdde-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="9cdde-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="9cdde-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-128">CS (39A)</span></span>               | <span data-ttu-id="9cdde-129">Blu</span><span class="sxs-lookup"><span data-stu-id="9cdde-129">Blue</span></span>          |
| <span data-ttu-id="9cdde-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="9cdde-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="9cdde-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-131">SCK (36A)</span></span>              | <span data-ttu-id="9cdde-132">Giallo</span><span class="sxs-lookup"><span data-stu-id="9cdde-132">Yellow</span></span>        |
| <span data-ttu-id="9cdde-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="9cdde-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="9cdde-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-134">SDO (37A)</span></span>              | <span data-ttu-id="9cdde-135">Bianco</span><span class="sxs-lookup"><span data-stu-id="9cdde-135">White</span></span>         |
| <span data-ttu-id="9cdde-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="9cdde-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="9cdde-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-137">SDI (38A)</span></span>              | <span data-ttu-id="9cdde-138">Verde</span><span class="sxs-lookup"><span data-stu-id="9cdde-138">Green</span></span>         |
| <span data-ttu-id="9cdde-139">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="9cdde-139">GND (Pin 6)</span></span>             | <span data-ttu-id="9cdde-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-140">GND (35A)</span></span>              | <span data-ttu-id="9cdde-141">Nero</span><span class="sxs-lookup"><span data-stu-id="9cdde-141">Black</span></span>         |
| <span data-ttu-id="9cdde-142">3.3 V (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="9cdde-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="9cdde-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="9cdde-143">3Vo (34A)</span></span>              | <span data-ttu-id="9cdde-144">Rosso</span><span class="sxs-lookup"><span data-stu-id="9cdde-144">Red</span></span>           |

<span data-ttu-id="9cdde-145">l'installazione di toocomplete hello hardware, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9cdde-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="9cdde-146">Collegare l'alimentazione elettrica toohello Raspberry Pi inclusa nel kit di hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="9cdde-147">Connettere la rete di tooyour Raspberry Pi tramite cavo Ethernet hello incluso con il kit.</span><span class="sxs-lookup"><span data-stu-id="9cdde-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="9cdde-148">In alternativa, è possibile configurare la [connettività wireless][lnk-pi-wireless] per Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9cdde-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="9cdde-149">È stata completata l'installazione dell'hardware del pi greco Raspberry hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="9cdde-150">Accesso e terminal hello</span><span class="sxs-lookup"><span data-stu-id="9cdde-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="9cdde-151">Sono presenti due opzioni tooaccess un ambiente terminal le Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="9cdde-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="9cdde-152">Se si dispone di una tastiera e monitorare connesso tooyour Raspberry Pi, è possibile utilizzare hello GUI Raspbian tooaccess una finestra terminale.</span><span class="sxs-lookup"><span data-stu-id="9cdde-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="9cdde-153">Riga di comando hello accesso con le pi greco Raspberry tramite SSH nel computer desktop.</span><span class="sxs-lookup"><span data-stu-id="9cdde-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="9cdde-154">Utilizzare una finestra terminal in hello GUI</span><span class="sxs-lookup"><span data-stu-id="9cdde-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="9cdde-155">le credenziali predefinite Hello per Raspbian sono username **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="9cdde-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="9cdde-156">Nella barra delle applicazioni hello in hello GUI, è possibile avviare hello **Terminal** utilità utilizzando l'icona di hello simile a un monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="9cdde-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="9cdde-157">Accedere con SSH</span><span class="sxs-lookup"><span data-stu-id="9cdde-157">Sign in with SSH</span></span>

<span data-ttu-id="9cdde-158">È possibile utilizzare SSH per l'accesso da riga di comando tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9cdde-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="9cdde-159">articolo Hello [SSH (Secure Shell)] [ lnk-pi-ssh] viene descritto come tooconfigure SSH sul pi greco Raspberry e come tooconnect da [Windows] [ lnk-ssh-windows] o [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="9cdde-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="9cdde-160">Accedere con il nome utente **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="9cdde-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="9cdde-161">Facoltativo: condividere una cartella in Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9cdde-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="9cdde-162">Facoltativamente, è opportuno tooshare una cartella con il pi greco Raspberry con l'ambiente desktop.</span><span class="sxs-lookup"><span data-stu-id="9cdde-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="9cdde-163">Condivisione di una cartella consente di toouse editor di testo preferito di desktop (ad esempio [codice di Visual Studio](https://code.visualstudio.com/) o [testo Sublime](http://www.sublimetext.com/)) file tooedit le Pi Raspberry anziché `nano` o `vi`.</span><span class="sxs-lookup"><span data-stu-id="9cdde-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="9cdde-164">tooshare una cartella con Windows, configurare un server Samba su hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9cdde-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="9cdde-165">In alternativa, utilizzare hello incorporato [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server con un client SFTP sul desktop.</span><span class="sxs-lookup"><span data-stu-id="9cdde-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="9cdde-166">Abilitare SPI</span><span class="sxs-lookup"><span data-stu-id="9cdde-166">Enable SPI</span></span>

<span data-ttu-id="9cdde-167">Prima di eseguire l'applicazione di esempio hello, è necessario abilitare bus seriale periferiche interfaccia SPI () hello hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9cdde-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="9cdde-168">Hello Pi Raspberry comunica con dispositivo di hello BME280 sensore tramite bus SPI hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="9cdde-169">Utilizzare i seguenti file di configurazione di comando tooedit hello hello:</span><span class="sxs-lookup"><span data-stu-id="9cdde-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="9cdde-170">Individuare la riga hello:</span><span class="sxs-lookup"><span data-stu-id="9cdde-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="9cdde-171">riga hello toouncomment, hello di eliminazione `#` all'inizio di hello.</span><span class="sxs-lookup"><span data-stu-id="9cdde-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="9cdde-172">Salvare le modifiche (**Ctrl O**, **invio**) e uscire dall'editor hello (**Ctrl + X**).</span><span class="sxs-lookup"><span data-stu-id="9cdde-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="9cdde-173">tooenable SPI, riavviare hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9cdde-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="9cdde-174">Il riavvio si disconnette terminal hello, è necessario toosign in nuovamente al riavvio di hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="9cdde-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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