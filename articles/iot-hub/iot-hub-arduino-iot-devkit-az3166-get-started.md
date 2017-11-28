---
title: aaaIoT Kit toocloud - tooAzure connettersi AZ3166 Kit di IoT IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi tooAzure AZ3166 Kit IoT IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="82979-103">Connettersi tooAzure AZ3166 Kit IoT IoT Hub nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="82979-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="82979-104">Hello [MXChip IoT Kit](https://microsoft.github.io/azure-iot-developer-kit/) può essere utilizzato toodevelop e prototipo soluzioni Internet delle cose (IoT) sfruttando i servizi di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82979-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="82979-105">Include una scheda compatibile Arduino con periferiche avanzate e sensori, un pacchetto della scheda open source e un aumento delle dimensioni del [catalogo progetti](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="82979-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="82979-106">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="82979-106">What you do</span></span>
<span data-ttu-id="82979-107">Connettersi [Kit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub di creare, dati di temperatura e umidità hello raccogliere da sensori e inviare l'hub di tooIoT dati hello.</span><span class="sxs-lookup"><span data-stu-id="82979-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="82979-108">Non hai ancora DevKit?</span><span class="sxs-lookup"><span data-stu-id="82979-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="82979-109">Ricevine uno nuovo [qui](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="82979-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="82979-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="82979-110">What you learn</span></span>

* <span data-ttu-id="82979-111">La modalità tooconnect IoT DevKit tooWireless accesso scegliere e preparare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="82979-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="82979-112">Come toocreate un hub IoT e registrare un dispositivo per MXChip IoT Kit.</span><span class="sxs-lookup"><span data-stu-id="82979-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="82979-113">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su MXChip IoT Kit.</span><span class="sxs-lookup"><span data-stu-id="82979-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="82979-114">Come toosend hello hub IoT tooyour di dati del sensore.</span><span class="sxs-lookup"><span data-stu-id="82979-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82979-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="82979-115">What you need</span></span>

* <span data-ttu-id="82979-116">Una scheda DevKit di IoT MXChip con un cavo USB micro.</span><span class="sxs-lookup"><span data-stu-id="82979-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="82979-117">Ottienila adesso</span><span class="sxs-lookup"><span data-stu-id="82979-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="82979-118">Un computer che esegue Windows 10 o macOS 10.10+</span><span class="sxs-lookup"><span data-stu-id="82979-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="82979-119">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="82979-119">An active Azure subscription</span></span>
  * <span data-ttu-id="82979-120">Attivare una [versione di prova gratuita di 30 giorni dell'account di Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="82979-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="82979-121">Preparare l'hardware</span><span class="sxs-lookup"><span data-stu-id="82979-121">Prepare your hardware</span></span>

<span data-ttu-id="82979-122">Collegare il computer di tooyour hello hardware.</span><span class="sxs-lookup"><span data-stu-id="82979-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="82979-123">Hardware necessario</span><span class="sxs-lookup"><span data-stu-id="82979-123">Hardware you need</span></span>

* <span data-ttu-id="82979-124">Scheda DevKit</span><span class="sxs-lookup"><span data-stu-id="82979-124">DevKit board</span></span>
* <span data-ttu-id="82979-125">Micro cavo USB</span><span class="sxs-lookup"><span data-stu-id="82979-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="82979-127">Connettere computer tooyour Kit</span><span class="sxs-lookup"><span data-stu-id="82979-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="82979-128">La connessione USB fine tooyour PC</span><span class="sxs-lookup"><span data-stu-id="82979-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="82979-129">La connessione USB Micro fine toohello Kit</span><span class="sxs-lookup"><span data-stu-id="82979-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="82979-130">Hello verde LED Avanti toopower Conferma connessione</span><span class="sxs-lookup"><span data-stu-id="82979-130">hello green LED next toopower confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="82979-132">Configurare il WiFi</span><span class="sxs-lookup"><span data-stu-id="82979-132">Configure WiFi</span></span>

<span data-ttu-id="82979-133">I progetti IoT si basano sulla connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="82979-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="82979-134">Utilizzare hello seguendo le istruzioni tooconfigure hello Kit tooconnect tooWiFi.</span><span class="sxs-lookup"><span data-stu-id="82979-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="82979-135">Passare alla modalità AP</span><span class="sxs-lookup"><span data-stu-id="82979-135">Enter AP Mode</span></span>

<span data-ttu-id="82979-136">Tenere premuto il pulsante B, quindi si reimposta hello push e la versione, quindi il tasto versione B. Il kit passerà alla modalità punto di accesso per la configurazione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="82979-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="82979-137">schermata Ciao visualizzerà hello servizio impostare Identifier(SSID) di hello Kit, così come indirizzo IP del portale di hello configurazione:</span><span class="sxs-lookup"><span data-stu-id="82979-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="82979-139">Asia Pacifico tooDevKit connettersi</span><span class="sxs-lookup"><span data-stu-id="82979-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="82979-140">A questo punto, usare un altro Wi-Fi abilitato dispositivi (PC o telefono cellulare) tooconnect toohello DevKit SSID (evidenziato nella schermata di hello precedente), lasciare vuota la password hello.</span><span class="sxs-lookup"><span data-stu-id="82979-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="82979-142">Configurare il WiFi per DevKit</span><span class="sxs-lookup"><span data-stu-id="82979-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="82979-143">Indirizzo IP hello aprire visualizzato sullo schermo Kit hello sul proprio PC o un browser di telefono cellulare, selezionare hello Wi-Fi rete hello Kit tooconnect per, quindi digitare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="82979-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="82979-144">Fare clic su **Connetti** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="82979-144">Click **Connect** toocomplete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="82979-146">Al termine della connessione di hello, hello Kit verrà riavviato in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="82979-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="82979-147">Se ha avuto esito positivo, verrà visualizzato hello Wi-Fi nome e indirizzo IP nella schermata di hello:</span><span class="sxs-lookup"><span data-stu-id="82979-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="82979-149">l'indirizzo IP Hello foto hello potrebbe non corrispondere hello IP effettivo assegnato e visualizzati sullo schermo Kit hello.</span><span class="sxs-lookup"><span data-stu-id="82979-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="82979-150">Questo è normale come Wi-Fi utilizza DHCP toodynamically assegnare indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="82979-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="82979-151">Dopo la configurazione Wi-Fi, le credenziali verranno rese persistenti nel dispositivo hello per tale connessione, anche se scollegato.</span><span class="sxs-lookup"><span data-stu-id="82979-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="82979-152">Ad esempio, se configurato hello Kit per Wi-Fi in casa e ha quindi office toohello Kit di hello, occorrerà modalità tooreconfigure PA (a partire dal passaggio **immettere modalità PA**) tooconnect hello Kit tooyour office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="82979-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="82979-153">Iniziare a usare DevKit</span><span class="sxs-lookup"><span data-stu-id="82979-153">Start using DevKit</span></span>

<span data-ttu-id="82979-154">applicazione predefinita Hello in esecuzione nel Kit verrà controllare hello la versione più recente del firmware hello e visualizzare alcuni dati di diagnostica sensore automaticamente.</span><span class="sxs-lookup"><span data-stu-id="82979-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="82979-155">Aggiornare il firmware più recente di toohello</span><span class="sxs-lookup"><span data-stu-id="82979-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="82979-156">Verrà richiesto nella schermata di hello che entrambi hello versione più recente del firmware se è presente un aggiornamento Necessito.</span><span class="sxs-lookup"><span data-stu-id="82979-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="82979-157">Seguire [aggiornare il firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade della Guida è.</span><span class="sxs-lookup"><span data-stu-id="82979-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="82979-159">Si tratta di un impegno monouso, dopo aver iniziato lo sviluppo di hello Kit e caricare l'app, sarà necessario firmware più recente di hello forniti con l'app.</span><span class="sxs-lookup"><span data-stu-id="82979-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="82979-160">Testare i diversi sensori</span><span class="sxs-lookup"><span data-stu-id="82979-160">Test various sensors</span></span>

<span data-ttu-id="82979-161">Premere sensori tootest pulsante B, continuare premendo e rilasciando toocycle pulsante hello B tramite ogni sensore.</span><span class="sxs-lookup"><span data-stu-id="82979-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="82979-163">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="82979-163">Prepare development environment</span></span>

<span data-ttu-id="82979-164">Ora è ora tooset hello ambiente di sviluppo: strumenti e i pacchetti per toobuild IoT applicazioni sorprendenti.</span><span class="sxs-lookup"><span data-stu-id="82979-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="82979-165">È possibile scegliere una versione Windows o macOS tooyour del sistema operativo di base.</span><span class="sxs-lookup"><span data-stu-id="82979-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="82979-166">Windows</span><span class="sxs-lookup"><span data-stu-id="82979-166">Windows</span></span>

<span data-ttu-id="82979-167">Invita i clienti si toouse hello installazione pacchetto tooprepare hello ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="82979-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="82979-168">Se si verificano problemi, è possibile seguire hello [passaggi manuali](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget eseguito.</span><span class="sxs-lookup"><span data-stu-id="82979-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="82979-169">Scaricare il pacchetto più recente</span><span class="sxs-lookup"><span data-stu-id="82979-169">Download latest package</span></span>

<span data-ttu-id="82979-170">Hello `.zip` file scaricato contiene tutti i pacchetti necessari per lo sviluppo di Kit e strumenti necessari.</span><span class="sxs-lookup"><span data-stu-id="82979-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="82979-171">Scaricare</span><span class="sxs-lookup"><span data-stu-id="82979-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="82979-172">Hello `.zip` hello siano contenuti file strumenti e i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="82979-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="82979-173">Se si dispone già di alcuni componenti installati, script hello rileverà e ignorarli.</span><span class="sxs-lookup"><span data-stu-id="82979-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="82979-174">Node.js e Yarn: Runtime per lo script di installazione di hello e attività automatizzate</span><span class="sxs-lookup"><span data-stu-id="82979-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="82979-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -multipiattaforma esperienza della riga di comando per la gestione delle risorse di Azure, hello MSI contiene Python e pip dipendenti.</span><span class="sxs-lookup"><span data-stu-id="82979-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="82979-176">[Visual Studio Code](https://code.visualstudio.com/): editor del codice semplice per lo sviluppo di DevKit</span><span class="sxs-lookup"><span data-stu-id="82979-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="82979-177">[Estensione di Visual Studio Code per Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): abilita lo sviluppo di Arduino in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="82979-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="82979-178">[IDE Arduino](https://www.arduino.cc/en/Main/Software): estensione hello per Arduino si basa su questo strumento</span><span class="sxs-lookup"><span data-stu-id="82979-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="82979-179">Pacchetto Kit Lavagna: Strumento catene, librerie e progetti per hello Kit</span><span class="sxs-lookup"><span data-stu-id="82979-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="82979-180">Utilità ST-Link: utilità essenziali e driver</span><span class="sxs-lookup"><span data-stu-id="82979-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="82979-181">Eseguire lo script di installazione</span><span class="sxs-lookup"><span data-stu-id="82979-181">Run installation script</span></span>

<span data-ttu-id="82979-182">In Esplora File individuare hello `.zip` e decomprimerlo, trovare `install.cmd`del mouse e scegliere **"Esegui come amministratore"** toostart.</span><span class="sxs-lookup"><span data-stu-id="82979-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="82979-184">Durante l'installazione, verrà visualizzato lo stato di avanzamento hello di ogni strumento o un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="82979-184">During installation, you will see hello progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="82979-186">Verificare i driver tooinstall</span><span class="sxs-lookup"><span data-stu-id="82979-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="82979-187">Hello Visual Studio Code per l'estensione Arduino si basa su hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="82979-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="82979-188">Se si tratta di hello prima volta che si sta installando hello Arduino IDE, sarà richiesta tooinstall rilevanti driver:</span><span class="sxs-lookup"><span data-stu-id="82979-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="82979-190">Occorrere installazione toofinish circa 10 minuti a seconda della velocità di Internet.</span><span class="sxs-lookup"><span data-stu-id="82979-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="82979-191">Al termine dell'installazione di hello, dovrebbe essere codice e Visual Studio IDE Arduino collegamenti sul desktop.</span><span class="sxs-lookup"><span data-stu-id="82979-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="82979-192">In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati.</span><span class="sxs-lookup"><span data-stu-id="82979-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="82979-193">toosolve chiudere Visual Studio Code, avviare una volta Arduino IDE e Visual Studio Code deve individuare il percorso di IDE Arduino correttamente.</span><span class="sxs-lookup"><span data-stu-id="82979-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="82979-194">macOS (anteprima)</span><span class="sxs-lookup"><span data-stu-id="82979-194">macOS (Preview)</span></span>

<span data-ttu-id="82979-195">Seguire questi ambiente di sviluppo tooprepare passaggi macOS.</span><span class="sxs-lookup"><span data-stu-id="82979-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="82979-196">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="82979-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="82979-197">Seguire hello [guida ufficiale](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall CLI di Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="82979-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="82979-198">Installare l'interfaccia della riga di comando di Azure 2.0 con il solo comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="82979-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="82979-199">E riavviare la shell dei comandi per effetto di tootake modifiche:</span><span class="sxs-lookup"><span data-stu-id="82979-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="82979-200">Installare l'IDE di Arduino</span><span class="sxs-lookup"><span data-stu-id="82979-200">Install Arduino IDE</span></span>

<span data-ttu-id="82979-201">estensione di Visual Studio codice Arduino Hello si basa su hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="82979-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="82979-202">Scaricare e installare hello [Arduino IDE per macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="82979-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="82979-203">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="82979-203">Install Visual Studio Code</span></span>

<span data-ttu-id="82979-204">Scaricar e installare [Visual Studio Code per macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="82979-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="82979-205">Questo sarà lo strumento di sviluppo primario hello per la creazione di applicazioni DevKit IoT.</span><span class="sxs-lookup"><span data-stu-id="82979-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="82979-206">Scaricare il pacchetto più recente</span><span class="sxs-lookup"><span data-stu-id="82979-206">Download latest package</span></span>

1. <span data-ttu-id="82979-207">Installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="82979-207">Install Node.js.</span></span> <span data-ttu-id="82979-208">È possibile usare Gestione pacchetti macOS diffusi [Homebrew](https://brew.sh/) o [pre-compilato installazione](https://nodejs.org/en/download/) tooinstall è.</span><span class="sxs-lookup"><span data-stu-id="82979-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="82979-209">Scaricare il file `.zip` che contiene gli script delle attività necessari per lo sviluppo di DevKit in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="82979-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="82979-210">Scaricare</span><span class="sxs-lookup"><span data-stu-id="82979-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="82979-211">Individuare hello `.zip` ed estrarre i file.</span><span class="sxs-lookup"><span data-stu-id="82979-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="82979-212">Avviare quindi **Terminal** app e l'esecuzione hello tooconfigure i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="82979-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="82979-213">Spostare estratti tooyour macOS utente una cartella:</span><span class="sxs-lookup"><span data-stu-id="82979-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="82979-214">Installare i pacchetti `npm`:</span><span class="sxs-lookup"><span data-stu-id="82979-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="82979-215">Installare l'estensione di Visual Studio Code per Arduino</span><span class="sxs-lookup"><span data-stu-id="82979-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="82979-216">Codice di Visual Studio consente le estensioni di Marketplace tooinstall direttamente nello strumento di hello, semplicemente fare clic sull'icona di estensioni hello nel riquadro di hello menu a sinistra e quindi cercare `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="82979-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="82979-218">Installare il pacchetto della scheda DevKit</span><span class="sxs-lookup"><span data-stu-id="82979-218">Install DevKit board package</span></span>

<span data-ttu-id="82979-219">Sarà necessario Lavagna Kit di hello tooadd utilizzando hello Manager scheda in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="82979-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="82979-220">Utilizzare `Cmd+Shift+P` tooinvoke comando tavolozza e digitare **Arduino** quindi individuare e selezionare **Arduino: scheda Gestione**.</span><span class="sxs-lookup"><span data-stu-id="82979-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="82979-221">Fare clic su **'URL aggiuntivi'** in basso a destra hello.</span><span class="sxs-lookup"><span data-stu-id="82979-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="82979-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="82979-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="82979-223">In hello `settings.json` file, aggiungere una riga in fondo hello `USER SETTINGS` riquadro e salvare.</span><span class="sxs-lookup"><span data-stu-id="82979-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="82979-225">Ora cercare 'az3166' hello Lavagna Manager e installare la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="82979-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="82979-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="82979-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="82979-227">È ora tutti i pacchetti installati per macOS e gli strumenti necessari hello.</span><span class="sxs-lookup"><span data-stu-id="82979-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="82979-228">Aprire la cartella del progetto</span><span class="sxs-lookup"><span data-stu-id="82979-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="82979-229">Avviare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="82979-229">Launch VS Code</span></span>

<span data-ttu-id="82979-230">Assicurarsi che DevKit non sia connesso.</span><span class="sxs-lookup"><span data-stu-id="82979-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="82979-231">Avviare innanzitutto il codice di Visual Studio e connettere hello Kit tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="82979-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="82979-232">Visual Studio Code lo troverà automaticamente e mostrerà una pagina di introduzione:</span><span class="sxs-lookup"><span data-stu-id="82979-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="82979-234">In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati.</span><span class="sxs-lookup"><span data-stu-id="82979-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="82979-235">toosolve chiudere Visual Studio Code, avviare nuovamente Arduino IDE e Visual Studio Code deve individuare il percorso di IDE Arduino correttamente.</span><span class="sxs-lookup"><span data-stu-id="82979-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="82979-236">Aprire la cartella degli esempi di Arduino</span><span class="sxs-lookup"><span data-stu-id="82979-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="82979-237">Opzione troppo**'Arduino esempi'** scheda, passare troppo`Examples for MXCHIP AZ3166 > AzureIoT` e fare clic su `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="82979-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="82979-239">Se si è verificata riquadro hello tooclose tooreload, utilizzare `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tavolozza e il tipo di comando tooinvoke **Arduino** toofind e selezionare **Arduino: esempi**.</span><span class="sxs-lookup"><span data-stu-id="82979-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="82979-240">Eseguire il provisioning dei servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="82979-240">Provision Azure services</span></span>

<span data-ttu-id="82979-241">Nella finestra di soluzione hello, eseguire le attività `Ctrl+P` (macOS: `Cmd+P`) digitando 'task il provisioning di cloud':</span><span class="sxs-lookup"><span data-stu-id="82979-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="82979-242">In hello Visual Studio Code terminale, che una riga di comando interattiva guiderà hello provisioning necessari servizi di Azure:</span><span class="sxs-lookup"><span data-stu-id="82979-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="82979-244">Compilare e caricare la definizione di Arduino</span><span class="sxs-lookup"><span data-stu-id="82979-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="82979-245">Installare la raccolta richiesta</span><span class="sxs-lookup"><span data-stu-id="82979-245">Install required library</span></span>

1. <span data-ttu-id="82979-246">Premere `F1` o `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tavolozza e il tipo di comando tooinvoke **Arduino** quindi individuare e selezionare **Arduino: Gestione librerie**.</span><span class="sxs-lookup"><span data-stu-id="82979-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="82979-247">Cercare la raccolta `ArduinoJson` e fare clic su **Install** (Installa)</span><span class="sxs-lookup"><span data-stu-id="82979-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="82979-248">Creare e caricare codice dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="82979-248">Build and upload hello device code</span></span>

<span data-ttu-id="82979-249">Utilizzare `Ctrl+P` (macOS: `Cmd+P`) toorun 'attività di dispositivo upload'.</span><span class="sxs-lookup"><span data-stu-id="82979-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="82979-250">Hello terminal richiederà si tooenter modalità di configurazione.</span><span class="sxs-lookup"><span data-stu-id="82979-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="82979-251">toodo in tal caso, tenere premuto un pulsante, quindi push e la versione di hello pulsante Reimposta.</span><span class="sxs-lookup"><span data-stu-id="82979-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="82979-252">schermata Ciao visualizzerà 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="82979-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="82979-253">Si tratta di stringa di connessione hello tooset che recupera dal passaggio di 'cloud-provisioning di attività'.</span><span class="sxs-lookup"><span data-stu-id="82979-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="82979-254">Quindi è possibile avviare la verifica e caricamento sketch Arduino hello:</span><span class="sxs-lookup"><span data-stu-id="82979-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="82979-256">Hello Kit verrà riavviato e avviarne l'esecuzione di codice hello.</span><span class="sxs-lookup"><span data-stu-id="82979-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="82979-257">Progetto di test hello</span><span class="sxs-lookup"><span data-stu-id="82979-257">Test hello project</span></span>

<span data-ttu-id="82979-258">Nel codice di Visual Studio, fare clic sul hello power plug sulla barra tooopen hello seriale di monitoraggio di stato hello.</span><span class="sxs-lookup"><span data-stu-id="82979-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="82979-259">applicazione di esempio Hello è in esecuzione correttamente quando viene visualizzato hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="82979-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="82979-260">Hello Visualizza monitoraggio seriale hello stesse informazioni di contenuto di hello hello schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="82979-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="82979-261">LED sul kit IoT MXChip Hello è lampeggiante.</span><span class="sxs-lookup"><span data-stu-id="82979-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Output finale in Visual Studio Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="82979-263">Problemi e commenti</span><span class="sxs-lookup"><span data-stu-id="82979-263">Problems and feedback</span></span>

<span data-ttu-id="82979-264">È possibile trovare [FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) se si verificano problemi o raggiungere toous dai canali hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="82979-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82979-265">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82979-265">Next steps</span></span>

<span data-ttu-id="82979-266">Si è connessi un tooyour MXChip Kit di IoT IoT Hub e hello inviato acquisita l'hub IoT sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="82979-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="82979-267">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="82979-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="82979-268">Gestire la messaggistica dei dispositivi cloud con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="82979-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="82979-269">Salvare i messaggi di IoT Hub tooAzure archiviazione dei dati</span><span class="sxs-lookup"><span data-stu-id="82979-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="82979-270">Usare Power BI toovisualize sensore in tempo reale dati provenienti dall'IoT Hub Azure</span><span class="sxs-lookup"><span data-stu-id="82979-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="82979-271">Utilizzare le app Web di Azure toovisualize sensore in tempo reale dati provenienti dall'IoT Hub Azure</span><span class="sxs-lookup"><span data-stu-id="82979-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="82979-272">Previsioni meteorologiche utilizzando i dati del sensore hello dall'hub IoT in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="82979-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="82979-273">Gestione dei dispositivi con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="82979-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="82979-274">Monitoraggio remoto e notifiche con App per la logica</span><span class="sxs-lookup"><span data-stu-id="82979-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)