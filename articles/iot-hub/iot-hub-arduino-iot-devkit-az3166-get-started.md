---
title: DevKit di IoT nel cloud - Connettere Devkit di IoT AZ3166 all'hub IoT di Azure | Microsoft Docs
description: Informazioni su come configurare e connettere DevKit di IoT AZ3166 all'hub IoT di Azure in modo che invii i dati alla piattaforma cloud di Azure in questa esercitazione.
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
ms.openlocfilehash: 122fac584ac5b954ef7b33a3121bee2c502ebc63
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="2fcba-103">Connettere DevKit di IoT AZ3166 all'hub IoT di Azure nel cloud</span><span class="sxs-lookup"><span data-stu-id="2fcba-103">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="2fcba-104">[DevKit di IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) può essere usato per sviluppare e creare il prototipo delle soluzioni di Internet delle cose (IoT) sfruttando i servizi di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2fcba-104">The [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used to develop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="2fcba-105">Include una scheda compatibile Arduino con periferiche avanzate e sensori, un pacchetto della scheda open source e un aumento delle dimensioni del [catalogo progetti](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="2fcba-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2fcba-106">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="2fcba-106">What you do</span></span>
<span data-ttu-id="2fcba-107">Connettere [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) a un hub IoT di Azure creato, raccogliere i dati relativi a temperatura e umidità dai sensori e inviare i dati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2fcba-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors and send the data to IoT hub.</span></span>

<span data-ttu-id="2fcba-108">Non hai ancora DevKit?</span><span class="sxs-lookup"><span data-stu-id="2fcba-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="2fcba-109">Ricevine uno nuovo [qui](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="2fcba-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2fcba-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2fcba-110">What you learn</span></span>

* <span data-ttu-id="2fcba-111">Come connettere DevKit di IoT al punto di accesso Wireless e preparare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2fcba-111">How to connect IoT DevKit to Wireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="2fcba-112">Come creare un hub IoT e registrare un dispositivo per DevKit di IoT MXChip.</span><span class="sxs-lookup"><span data-stu-id="2fcba-112">How to create an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="2fcba-113">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in DevKit di IoT MXChip.</span><span class="sxs-lookup"><span data-stu-id="2fcba-113">How to collect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="2fcba-114">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2fcba-114">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2fcba-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2fcba-115">What you need</span></span>

* <span data-ttu-id="2fcba-116">Una scheda DevKit di IoT MXChip con un cavo USB micro.</span><span class="sxs-lookup"><span data-stu-id="2fcba-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="2fcba-117">Ottienila adesso</span><span class="sxs-lookup"><span data-stu-id="2fcba-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="2fcba-118">Un computer che esegue Windows 10 o macOS 10.10+</span><span class="sxs-lookup"><span data-stu-id="2fcba-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="2fcba-119">Una sottoscrizione di Azure attiva</span><span class="sxs-lookup"><span data-stu-id="2fcba-119">An active Azure subscription</span></span>
  * <span data-ttu-id="2fcba-120">Attivare una [versione di prova gratuita di 30 giorni dell'account di Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="2fcba-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="2fcba-121">Preparare l'hardware</span><span class="sxs-lookup"><span data-stu-id="2fcba-121">Prepare your hardware</span></span>

<span data-ttu-id="2fcba-122">Collegare l'hardware al computer.</span><span class="sxs-lookup"><span data-stu-id="2fcba-122">Hook up the hardware to your computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="2fcba-123">Hardware necessario</span><span class="sxs-lookup"><span data-stu-id="2fcba-123">Hardware you need</span></span>

* <span data-ttu-id="2fcba-124">Scheda DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-124">DevKit board</span></span>
* <span data-ttu-id="2fcba-125">Micro cavo USB</span><span class="sxs-lookup"><span data-stu-id="2fcba-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a><span data-ttu-id="2fcba-127">Connettere DevKit al computer</span><span class="sxs-lookup"><span data-stu-id="2fcba-127">Connect DevKit to your computer</span></span>

1. <span data-ttu-id="2fcba-128">Collegare l'estremità USB al PC</span><span class="sxs-lookup"><span data-stu-id="2fcba-128">Connect USB end to your PC</span></span>
2. <span data-ttu-id="2fcba-129">Collegare l'estremità Micro USB a DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-129">Connect Micro USB end to the DevKit</span></span>
3. <span data-ttu-id="2fcba-130">Il LED verde accanto all'alimentazione conferma la connessione</span><span class="sxs-lookup"><span data-stu-id="2fcba-130">The green LED next to power confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="2fcba-132">Configurare il WiFi</span><span class="sxs-lookup"><span data-stu-id="2fcba-132">Configure WiFi</span></span>

<span data-ttu-id="2fcba-133">I progetti IoT si basano sulla connettività Internet.</span><span class="sxs-lookup"><span data-stu-id="2fcba-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="2fcba-134">Usare le istruzioni seguenti per configurare il DevKit da connettere al WiFi.</span><span class="sxs-lookup"><span data-stu-id="2fcba-134">Use the following instructions to configure the DevKit to connect to WiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="2fcba-135">Passare alla modalità AP</span><span class="sxs-lookup"><span data-stu-id="2fcba-135">Enter AP Mode</span></span>

<span data-ttu-id="2fcba-136">Tenere premuto il pulsante B, poi premere e rilasciare il pulsante di reimpostazione e quindi rilasciare il pulsante B. Il DevKit passerà alla modalità AP per la configurazione del WiFi.</span><span class="sxs-lookup"><span data-stu-id="2fcba-136">Hold down button B, then push and release the reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="2fcba-137">Nella schermata verrà visualizzato l'identificatore SSID del DevKit, nonché l'indirizzo IP del portale di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2fcba-137">The screen will display the Service Set Identifier(SSID) of the DevKit as well as the configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a><span data-ttu-id="2fcba-139">Eseguire la connessione a DevKit AP</span><span class="sxs-lookup"><span data-stu-id="2fcba-139">Connect to DevKit AP</span></span>

<span data-ttu-id="2fcba-140">A questo punto, usare un altro dispositivo con WiFi (PC o telefono cellulare) per connettersi al SSID di DevKit (evidenziato nella schermata precedente) e lasciare vuota la password.</span><span class="sxs-lookup"><span data-stu-id="2fcba-140">Now, use another WiFi enabled device (PC or mobile phone) to connect to the DevKit SSID (highlighted in the screenshot above), leave the password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="2fcba-142">Configurare il WiFi per DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="2fcba-143">Aprire l'indirizzo IP mostrato nella schermata di DevKit nel browser del computer o del telefono cellulare, selezionare la rete WiFi con cui si desidera connettere DevKit, quindi digitare la password.</span><span class="sxs-lookup"><span data-stu-id="2fcba-143">Open the IP address shown on the DevKit screen on your PC or mobile phone browser, select the WiFi network you want the DevKit to connect to, then type the password.</span></span> <span data-ttu-id="2fcba-144">Fare clic su **Connetti** per completare:</span><span class="sxs-lookup"><span data-stu-id="2fcba-144">Click **Connect** to complete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="2fcba-146">Una volta stabilita la connessione, in pochi secondi verrà riavviato il DevKit.</span><span class="sxs-lookup"><span data-stu-id="2fcba-146">Once the connection succeeds, the DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="2fcba-147">In caso di esito positivo, verrà visualizzato il nome del WiFi e l'indirizzo IP sullo schermo:</span><span class="sxs-lookup"><span data-stu-id="2fcba-147">If succeeded, you will see the WiFi name and IP address on the screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="2fcba-149">L'indirizzo IP visualizzato nella foto potrebbe non corrispondere all'indirizzo IP effettivo assegnato e visualizzato sullo schermo di DevKit.</span><span class="sxs-lookup"><span data-stu-id="2fcba-149">The IP address displayed in the photo may not match the actual IP assigned and displayed on the DevKit screen.</span></span> <span data-ttu-id="2fcba-150">Si tratta di un comportamento normale perché il WiFi usa DHCP per assegnare in modo dinamico gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="2fcba-150">This is normal as WiFi uses DHCP to dynamically assign IPs.</span></span>

<span data-ttu-id="2fcba-151">Dopo la configurazione del WiFi, le credenziali verranno mantenute nel dispositivo per tale connessione, anche se scollegato.</span><span class="sxs-lookup"><span data-stu-id="2fcba-151">After WiFi is configured, your credentials will be persisted on the device for that connection, even if unplugged.</span></span> <span data-ttu-id="2fcba-152">Ad esempio, se DevKit è stato configurato per il WiFi di casa e poi si sposta DevKit in ufficio, sarà necessario riconfigurare la modalità AP (a partire dal passaggio **Passare alla modalità AP**) per connettere il DevKit alla rete WiFi dell'ufficio.</span><span class="sxs-lookup"><span data-stu-id="2fcba-152">For example, if you configured the DevKit for WiFi in your home and then took the DevKit to the office, you will need to reconfigure AP mode (starting at step **Enter AP Mode**) to connect the DevKit to your office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="2fcba-153">Iniziare a usare DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-153">Start using DevKit</span></span>

<span data-ttu-id="2fcba-154">L'app predefinita in esecuzione in DevKit controllerà la versione più recente del firmware e visualizzerà alcuni dati di diagnostica del sensore per l'utente.</span><span class="sxs-lookup"><span data-stu-id="2fcba-154">The default app running on DevKit will check the latest version of the firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-to-the-latest-firmware"></a><span data-ttu-id="2fcba-155">Eseguire l'aggiornamento al firmware più recente</span><span class="sxs-lookup"><span data-stu-id="2fcba-155">Upgrade to the latest firmware</span></span>

<span data-ttu-id="2fcba-156">Verranno visualizzate sullo schermo sia la versione attuale sia quella più recente del firmware se è presente un aggiornamento necessario.</span><span class="sxs-lookup"><span data-stu-id="2fcba-156">You will be prompted on the screen both the current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="2fcba-157">Seguire la guida [Aggiorna firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2fcba-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide to upgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="2fcba-159">Si tratta di un'attività una tantum: una volta iniziato lo sviluppo del DevKit e caricata l'app, il firmware più recente sarà fornito con l'app.</span><span class="sxs-lookup"><span data-stu-id="2fcba-159">This is a one-time effort, once you start developing on the DevKit and upload your app, you will have the latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="2fcba-160">Testare i diversi sensori</span><span class="sxs-lookup"><span data-stu-id="2fcba-160">Test various sensors</span></span>

<span data-ttu-id="2fcba-161">Premere il pulsante B per testare i sensori, continuare a premere e rilasciare il pulsante B per scorrere ogni sensore.</span><span class="sxs-lookup"><span data-stu-id="2fcba-161">Press button B to test sensors, continue pressing and releasing the B button to cycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="2fcba-163">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="2fcba-163">Prepare development environment</span></span>

<span data-ttu-id="2fcba-164">Ora è possibile configurare l'ambiente di sviluppo: strumenti e pacchetti per compilare straordinarie applicazioni IoT.</span><span class="sxs-lookup"><span data-stu-id="2fcba-164">Now it's time to set up the development environment: tools and packages for you to build stunning IoT applications.</span></span> <span data-ttu-id="2fcba-165">È possibile scegliere una versione di Windows o macOS in base al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2fcba-165">You can choose Windows or macOS version according to your operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="2fcba-166">Windows</span><span class="sxs-lookup"><span data-stu-id="2fcba-166">Windows</span></span>

<span data-ttu-id="2fcba-167">Si consiglia di usare il pacchetto di installazione per preparare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2fcba-167">We encourage you to use the installation package to prepare the development environment.</span></span> <span data-ttu-id="2fcba-168">Se si verificano problemi, è possibile seguire la [procedura del manuale](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) per risolverli.</span><span class="sxs-lookup"><span data-stu-id="2fcba-168">If you encounter any issues, you can follow the [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) to get it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="2fcba-169">Scaricare il pacchetto più recente</span><span class="sxs-lookup"><span data-stu-id="2fcba-169">Download latest package</span></span>

<span data-ttu-id="2fcba-170">Il file `.zip` scaricato contiene tutti gli strumenti e i pacchetti necessari per lo sviluppo di DevKit.</span><span class="sxs-lookup"><span data-stu-id="2fcba-170">The `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="2fcba-171">Scaricare</span><span class="sxs-lookup"><span data-stu-id="2fcba-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="2fcba-172">Il file `.zip` contiene gli strumenti e i pacchetti seguenti.</span><span class="sxs-lookup"><span data-stu-id="2fcba-172">The `.zip` file contains the following tools and packages.</span></span> <span data-ttu-id="2fcba-173">Se si dispone già di alcuni componenti installati, lo script li rileverà e li ignorerà.</span><span class="sxs-lookup"><span data-stu-id="2fcba-173">If you already have some components installed, the script will detect and skip them.</span></span>
> * <span data-ttu-id="2fcba-174">Node.js e Yarn: runtime per lo script di configurazione e le attività automatizzate</span><span class="sxs-lookup"><span data-stu-id="2fcba-174">Node.js and Yarn: Runtime for the setup script and automated tasks</span></span>
> * <span data-ttu-id="2fcba-175">[Interfaccia della riga di comando di Azure 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows): esperienza della riga di comando multipiattaforma per la gestione delle risorse di Azure, il file MSI contiene Python e pip dipendenti.</span><span class="sxs-lookup"><span data-stu-id="2fcba-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, the MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="2fcba-176">[Visual Studio Code](https://code.visualstudio.com/): editor del codice semplice per lo sviluppo di DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="2fcba-177">[Estensione di Visual Studio Code per Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): abilita lo sviluppo di Arduino in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2fcba-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="2fcba-178">[IDE Arduino](https://www.arduino.cc/en/Main/Software): l'estensione per Arduino si basa su questo strumento</span><span class="sxs-lookup"><span data-stu-id="2fcba-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): The extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="2fcba-179">Pacchetto della scheda DevKit: catene dello strumento, librerie e progetti per il DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-179">DevKit Board Package: Tool chains, libraries and projects for the DevKit</span></span>
> * <span data-ttu-id="2fcba-180">Utilità ST-Link: utilità essenziali e driver</span><span class="sxs-lookup"><span data-stu-id="2fcba-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="2fcba-181">Eseguire lo script di installazione</span><span class="sxs-lookup"><span data-stu-id="2fcba-181">Run installation script</span></span>

<span data-ttu-id="2fcba-182">In Esplora risorse di Windows individuare `.zip` ed estrarlo, trovare `install.cmd`, fare clic on il tasto destro del mouse e selezionare **"Esegui come amministratore"** per iniziare.</span><span class="sxs-lookup"><span data-stu-id="2fcba-182">In Windows File Explorer, locate the `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** to start.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="2fcba-184">Durante l'installazione, si noterà lo stato di avanzamento di ogni strumento o pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2fcba-184">During installation, you will see the progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a><span data-ttu-id="2fcba-186">Confermare per installare i driver</span><span class="sxs-lookup"><span data-stu-id="2fcba-186">Confirm to install drivers</span></span>

<span data-ttu-id="2fcba-187">Il Visual Studio Code per l'estensione di Arduino si basa sull'IDE di Arduino.</span><span class="sxs-lookup"><span data-stu-id="2fcba-187">The VS Code for Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="2fcba-188">Se questa è la prima volta che si sta installando l'IDE di Arduino, viene chiesto di installare i driver corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="2fcba-188">If this is the first time you are installing the Arduino IDE, you will be prompted to install relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="2fcba-190">Il completamento dell'installazione dovrebbe richiedere circa 10 minuti, a seconda della velocità di Internet.</span><span class="sxs-lookup"><span data-stu-id="2fcba-190">It should take around 10 minutes to finish installation depending on your Internet speed.</span></span> <span data-ttu-id="2fcba-191">Al termine dell'installazione, si dovrebbero visualizzare i collegamenti a Visual Studio Code e all'IDE di Arduino sul desktop.</span><span class="sxs-lookup"><span data-stu-id="2fcba-191">Once the installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="2fcba-192">In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati.</span><span class="sxs-lookup"><span data-stu-id="2fcba-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="2fcba-193">Per risolvere l'errore, chiudere Visual Studio Code, avviare una volta l'IDE di Arduino e Visual Studio Code dovrebbe individuare correttamente il percorso dell'IDE di Arduino.</span><span class="sxs-lookup"><span data-stu-id="2fcba-193">To solve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="2fcba-194">macOS (anteprima)</span><span class="sxs-lookup"><span data-stu-id="2fcba-194">macOS (Preview)</span></span>

<span data-ttu-id="2fcba-195">Seguire questa procedura per preparare l'ambiente di sviluppo in macOS.</span><span class="sxs-lookup"><span data-stu-id="2fcba-195">Follow these steps to prepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="2fcba-196">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2fcba-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="2fcba-197">Seguire la [guida ufficiale](https://docs.microsoft.com//cli/azure/install-azure-cli) per installare l'interfaccia della riga di comando di Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="2fcba-197">Follow the [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) to install Azure CLI 2.0:</span></span>

<span data-ttu-id="2fcba-198">Installare l'interfaccia della riga di comando di Azure 2.0 con il solo comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="2fcba-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="2fcba-199">Riavviare quindi la shell dei comandi per rendere effettive le modifiche apportate:</span><span class="sxs-lookup"><span data-stu-id="2fcba-199">And restart your command shell for changes to take effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="2fcba-200">Installare l'IDE di Arduino</span><span class="sxs-lookup"><span data-stu-id="2fcba-200">Install Arduino IDE</span></span>

<span data-ttu-id="2fcba-201">L'estensione di Arduino di Visual Studio Code si basa sull'IDE di Arduino.</span><span class="sxs-lookup"><span data-stu-id="2fcba-201">The Visual Studio Code Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="2fcba-202">Scaricare e installare l'[IDE di Arduino per macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="2fcba-202">Download and install the [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="2fcba-203">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2fcba-203">Install Visual Studio Code</span></span>

<span data-ttu-id="2fcba-204">Scaricar e installare [Visual Studio Code per macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="2fcba-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="2fcba-205">Questo sarà lo strumento di sviluppo primario per la compilazione di applicazioni DevKit di IoT.</span><span class="sxs-lookup"><span data-stu-id="2fcba-205">This will be the primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="2fcba-206">Scaricare il pacchetto più recente</span><span class="sxs-lookup"><span data-stu-id="2fcba-206">Download latest package</span></span>

1. <span data-ttu-id="2fcba-207">Installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="2fcba-207">Install Node.js.</span></span> <span data-ttu-id="2fcba-208">È possibile usare la comune gestione dei pacchetti macOS [Homebrew](https://brew.sh/) o [uno strumento di installazione pre-compilato](https://nodejs.org/en/download/) per installarlo.</span><span class="sxs-lookup"><span data-stu-id="2fcba-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) to install it.</span></span>

2. <span data-ttu-id="2fcba-209">Scaricare il file `.zip` che contiene gli script delle attività necessari per lo sviluppo di DevKit in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2fcba-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="2fcba-210">Scaricare</span><span class="sxs-lookup"><span data-stu-id="2fcba-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="2fcba-211">Individuare `.zip` ed estrarlo.</span><span class="sxs-lookup"><span data-stu-id="2fcba-211">Locate the `.zip` and extract it.</span></span> <span data-ttu-id="2fcba-212">Avviare quindi l'app**Terminal** ed eseguire i comandi seguenti per configurare:</span><span class="sxs-lookup"><span data-stu-id="2fcba-212">Then launch **Terminal** app and run the following commands to configure:</span></span>

   <span data-ttu-id="2fcba-213">Spostare la cartella estratta nella cartella utente macOS:</span><span class="sxs-lookup"><span data-stu-id="2fcba-213">Move extracted folder to your macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="2fcba-214">Installare i pacchetti `npm`:</span><span class="sxs-lookup"><span data-stu-id="2fcba-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="2fcba-215">Installare l'estensione di Visual Studio Code per Arduino</span><span class="sxs-lookup"><span data-stu-id="2fcba-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="2fcba-216">Visual Studio Code consente di installare le estensioni di Marketplace direttamente nello strumento, facendo semplicemente clic sull'icona delle estensioni nel riquadro sinistro e quindi cercando `Arduino` per installare:</span><span class="sxs-lookup"><span data-stu-id="2fcba-216">Visual Studio Code allows you to install Marketplace extensions directly in the tool, simply click the extensions icon in the left menu pane and then search `Arduino` to install:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="2fcba-218">Installare il pacchetto della scheda DevKit</span><span class="sxs-lookup"><span data-stu-id="2fcba-218">Install DevKit board package</span></span>

<span data-ttu-id="2fcba-219">È necessario aggiungere la scheda DevKit tramite Board Manager (Gestione scheda) in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2fcba-219">You will need to add the DevKit board using the Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="2fcba-220">Usare `Cmd+Shift+P` per richiamare il riquadro comandi e digitare **Arduino**, quindi individuare e selezionare **Arduino: Board Manager** (Arduino: Gestione scheda).</span><span class="sxs-lookup"><span data-stu-id="2fcba-220">Use `Cmd+Shift+P` to invoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="2fcba-221">Fare clic su **"Additional URLs"** ("URL aggiuntivi") in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="2fcba-221">Click **'Additional URLs'** at the bottom right.</span></span>
   <span data-ttu-id="2fcba-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="2fcba-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="2fcba-223">Nel file `settings.json` aggiungere una riga nella parte inferiore del riquadro `USER SETTINGS` e salvare.</span><span class="sxs-lookup"><span data-stu-id="2fcba-223">In the `settings.json` file, add a line at the bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="2fcba-225">Ora in Board Manager (Gestione scheda) cercare "az3166" e installare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="2fcba-225">Now in the Board Manager search for 'az3166' and install the latest version.</span></span>
   <span data-ttu-id="2fcba-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="2fcba-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="2fcba-227">Ora si dispone di tutti gli strumenti necessari e dei pacchetti installati per macOS.</span><span class="sxs-lookup"><span data-stu-id="2fcba-227">You now have all the necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="2fcba-228">Aprire la cartella del progetto</span><span class="sxs-lookup"><span data-stu-id="2fcba-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="2fcba-229">Avviare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2fcba-229">Launch VS Code</span></span>

<span data-ttu-id="2fcba-230">Assicurarsi che DevKit non sia connesso.</span><span class="sxs-lookup"><span data-stu-id="2fcba-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="2fcba-231">Innanzitutto avviare Visual Studio Code e collegare il DevKit al computer.</span><span class="sxs-lookup"><span data-stu-id="2fcba-231">Launch VS Code first and connect the DevKit to your computer.</span></span> <span data-ttu-id="2fcba-232">Visual Studio Code lo troverà automaticamente e mostrerà una pagina di introduzione:</span><span class="sxs-lookup"><span data-stu-id="2fcba-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="2fcba-234">In alcuni casi, quando si avvia Visual Studio Code, verrà visualizzato un errore che non è possibile trovare nell'IDE di Arduino o in un pacchetto di scheda correlati.</span><span class="sxs-lookup"><span data-stu-id="2fcba-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="2fcba-235">Per risolvere l'errore, chiudere Visual Studio Code, avviare nuovamente l'IDE di Arduino e Visual Studio Code dovrebbe individuare correttamente il percorso dell'IDE di Arduino.</span><span class="sxs-lookup"><span data-stu-id="2fcba-235">To solve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="2fcba-236">Aprire la cartella degli esempi di Arduino</span><span class="sxs-lookup"><span data-stu-id="2fcba-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="2fcba-237">Passare alla scheda **"Arduino Examples"**("Esempi di Arduino"), procedere con `Examples for MXCHIP AZ3166 > AzureIoT` e fare clic su `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="2fcba-237">Switch to **'Arduino Examples'** tab, navigate to `Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="2fcba-239">Se è capitato di richiudere il pannello, per ricaricarlo, usare `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) per richiamare il riquadro comandi e digitare **Arduino** per individuare e selezionare **Arduino: Examples** (Arduino: esempi).</span><span class="sxs-lookup"><span data-stu-id="2fcba-239">If you happen to close the pane, to reload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** to find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="2fcba-240">Eseguire il provisioning dei servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="2fcba-240">Provision Azure services</span></span>

<span data-ttu-id="2fcba-241">Nella finestra della soluzione eseguire le attività `Ctrl+P` (macOS: `Cmd+P`) digitando "task cloud-provision":</span><span class="sxs-lookup"><span data-stu-id="2fcba-241">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="2fcba-242">Nel terminale di Visual Studio Code una riga di comando interattiva guiderà nel processo di provisioning dei servizi di Azure necessari:</span><span class="sxs-lookup"><span data-stu-id="2fcba-242">In the VS Code terminal, an interactive command line will guide you through provisioning the required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="2fcba-244">Compilare e caricare la definizione di Arduino</span><span class="sxs-lookup"><span data-stu-id="2fcba-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="2fcba-245">Installare la raccolta richiesta</span><span class="sxs-lookup"><span data-stu-id="2fcba-245">Install required library</span></span>

1. <span data-ttu-id="2fcba-246">Premere `F1` o `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) per richiamare il riquadro comandi e digitare **Arduino**, quindi individuare e selezionare **Arduino: Library Manager** (Arduino: Gestione raccolte).</span><span class="sxs-lookup"><span data-stu-id="2fcba-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="2fcba-247">Cercare la raccolta `ArduinoJson` e fare clic su **Install** (Installa)</span><span class="sxs-lookup"><span data-stu-id="2fcba-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-the-device-code"></a><span data-ttu-id="2fcba-248">Compilare e caricare il codice del dispositivo</span><span class="sxs-lookup"><span data-stu-id="2fcba-248">Build and upload the device code</span></span>

<span data-ttu-id="2fcba-249">Usare `Ctrl+P` (macOS: `Cmd+P`) per eseguire di "task device-upload".</span><span class="sxs-lookup"><span data-stu-id="2fcba-249">Use `Ctrl+P` (macOS: `Cmd+P`) to run 'task device-upload'.</span></span> <span data-ttu-id="2fcba-250">Il terminale richiederà di passare alla modalità di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2fcba-250">The terminal will prompt you to enter configuration mode.</span></span> <span data-ttu-id="2fcba-251">A tale scopo, tenere premuto il pulsante A, quindi premere e rilasciare il pulsante di reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="2fcba-251">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="2fcba-252">Nella schermata verrà visualizzato "Configuration" (Configurazione).</span><span class="sxs-lookup"><span data-stu-id="2fcba-252">The screen will display 'Configuration'.</span></span> <span data-ttu-id="2fcba-253">Questa operazione serve per impostare la stringa di connessione che si recupera dal passaggio "task cloud-provision".</span><span class="sxs-lookup"><span data-stu-id="2fcba-253">This is to set the connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="2fcba-254">Quindi è possibile avviare la verifica e il caricamento della definizione di Arduino:</span><span class="sxs-lookup"><span data-stu-id="2fcba-254">Then it will start verifying and uploading the Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="2fcba-256">Il DevKit riavvierà il computer e inizierà l'esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="2fcba-256">The DevKit will reboot and start running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="2fcba-257">Verificare il progetto</span><span class="sxs-lookup"><span data-stu-id="2fcba-257">Test the project</span></span>

<span data-ttu-id="2fcba-258">In Visual Studio Code fare clic sull'icona del plug di accensione sulla barra di stato per aprire Serial Monitor (Monitoraggio seriale).</span><span class="sxs-lookup"><span data-stu-id="2fcba-258">In VS Code, click the power plug icon on the status bar to open the Serial Monitor.</span></span>

<span data-ttu-id="2fcba-259">L'applicazione di esempio viene eseguita correttamente quando vengono visualizzati i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="2fcba-259">The sample application is running successfully when you see the following results:</span></span>

* <span data-ttu-id="2fcba-260">Serial Monitor (Monitoraggio seriale) visualizza le stesse informazioni presenti nel contenuto nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="2fcba-260">The Serial Monitor displays the same information as the content in the screenshot below.</span></span>
* <span data-ttu-id="2fcba-261">Il LED sul DevKit di IoT MXChip lampeggia.</span><span class="sxs-lookup"><span data-stu-id="2fcba-261">The LED on MXChip IoT DevKit is blinking.</span></span>

![Output finale in Visual Studio Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="2fcba-263">Problemi e commenti</span><span class="sxs-lookup"><span data-stu-id="2fcba-263">Problems and feedback</span></span>

<span data-ttu-id="2fcba-264">In caso di problemi, è possibile consultare le [Domande frequenti](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) o contattarci tramite i canali riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="2fcba-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out to us from the channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fcba-265">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fcba-265">Next steps</span></span>

<span data-ttu-id="2fcba-266">La scheda DevKit di IoT MXChip è stata connessa all'hub IoT correttamente e i dati acquisiti dal sensore sono stati inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2fcba-266">You have successfully connected an MXChip IoT DevKit to your IoT Hub, and sent the captured sensor data to your IoT hub.</span></span>

<span data-ttu-id="2fcba-267">Per altre informazioni sulle attività iniziali con l'hub IoT e per esplorare altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="2fcba-267">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="2fcba-268">Gestire la messaggistica dei dispositivi cloud con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="2fcba-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="2fcba-269">Salvare i messaggi dell'hub IoT nell'archivio dati di Azure</span><span class="sxs-lookup"><span data-stu-id="2fcba-269">Save IoT Hub messages to Azure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="2fcba-270">Usare Power BI per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="2fcba-270">Use Power BI to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="2fcba-271">Usare App Web di Azure per visualizzare i dati del sensore in tempo reale dall'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="2fcba-271">Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="2fcba-272">Previsioni meteo usando i dati sensore dell'hub IoT in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2fcba-272">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="2fcba-273">Gestione dei dispositivi con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="2fcba-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="2fcba-274">Monitoraggio remoto e notifiche con App per la logica</span><span class="sxs-lookup"><span data-stu-id="2fcba-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)