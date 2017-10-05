---
title: Usare un dispositivo fisico con Azure IoT Edge | Microsoft Docs
description: Come usare un dispositivo SensorTag di Texas Instruments per inviare dati a un hub IoT tramite un gateway IoT Edge in esecuzione su un dispositivo Raspberry Pi 3. Il gateway viene creato con Azure IoT Edge.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="a7cdf-104">Usare Azure IoT Edge in Raspberry Pi per inoltrare all'hub IoT messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="a7cdf-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="a7cdf-105">Questa procedura dettagliata relativa all'[esempio Bluetooth Low Energy][lnk-ble-samplecode] illustra come usare [Azure IoT Edge][lnk-sdk] per:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="a7cdf-106">Inoltrare all'hub IoT i dati di telemetria da dispositivo a cloud da un dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="a7cdf-107">Instradare i comandi dall'hub IoT a un dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="a7cdf-108">In questa procedura dettagliata verranno trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-108">This walkthrough covers:</span></span>

* <span data-ttu-id="a7cdf-109">**Architettura**: informazioni importanti sull'architettura relative all'esempio Bluetooth Low Energy.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="a7cdf-110">**Compilazione ed esecuzione**: i passaggi richiesti per compilare ed eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="a7cdf-111">Architettura</span><span class="sxs-lookup"><span data-stu-id="a7cdf-111">Architecture</span></span>

<span data-ttu-id="a7cdf-112">La procedura dettagliata illustra come compilare ed eseguire un gateway IoT Edge in un modulo Raspberry Pi 3 che esegue Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="a7cdf-113">Il gateway viene creato usando IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="a7cdf-114">L'esempio usa un dispositivo SensorTag di Texas Instruments basato su tecnologia Bluetooth Low Energy (BLE) per raccogliere i dati sulla temperatura.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="a7cdf-115">Quando viene eseguito, il gateway IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="a7cdf-116">Si connette a un dispositivo SensorTag usando il protocollo BLE.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="a7cdf-117">Si connette all'hub IoT usando il protocollo HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="a7cdf-118">Inoltra i dati di telemetria dal dispositivo SensorTag all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="a7cdf-119">Instrada i comandi dall'hub IoT al dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="a7cdf-120">Il gateway contiene i moduli IoT Edge seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="a7cdf-121">Un *modulo BLE* che si interfaccia con un dispositivo BLE per ricevere i dati sulla temperatura dal dispositivo e inviare comandi al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="a7cdf-122">Un *modulo BLE da cloud a dispositivo* che converte i messaggi JSON inviati dall'hub IoT in istruzioni BLE per il *modulo BLE*.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="a7cdf-123">Un *modulo logger* che registra tutti i messaggi del gateway in un file locale.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="a7cdf-124">Un *modulo di mapping delle identità* che esegue la conversione tra gli indirizzi MAC del dispositivo BLE e le identità dispositivo dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="a7cdf-125">Un *modulo dell'hub IoT* che carica i dati di telemetria in un hub IoT e riceve i comandi del dispositivo da un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="a7cdf-126">Un *modulo di stampa BLE* che interpreta i dati di telemetria dal dispositivo BLE e stampa i dati formattati sulla console per consentire la risoluzione dei problemi e il debug.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="a7cdf-127">Come avviene il flusso di dati attraverso il gateway</span><span class="sxs-lookup"><span data-stu-id="a7cdf-127">How data flows through the gateway</span></span>

<span data-ttu-id="a7cdf-128">Il diagramma a blocchi seguente illustra la pipeline del flusso di caricamento dei dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Pipeline di caricamento dei dati di telemetria attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="a7cdf-130">Il passaggio di un elemento di telemetria da un dispositivo BLE all'hub IoT prevede le fasi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="a7cdf-131">Il dispositivo BLE genera un esempio relativo alla temperatura e lo invia tramite Bluetooth al modulo BLE nel gateway.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="a7cdf-132">Il modulo BLE riceve l'esempio e lo pubblica sul broker insieme all'indirizzo MAC del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="a7cdf-133">Il modulo di mapping delle identità preleva il messaggio e usa una tabella interna per convertire l'indirizzo MAC del dispositivo in un'identità dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="a7cdf-134">Un'identità dispositivo dell'hub IoT è costituita da un ID di dispositivo e una chiave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="a7cdf-135">Il modulo di mapping delle identità pubblica un nuovo messaggio contenente i dati di esempio relativi alla temperatura, nonché l'indirizzo MAC, l'ID e la chiave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="a7cdf-136">Il modulo dell'hub IoT riceve questo nuovo messaggio (generato dal modulo di mapping delle identità) e lo pubblica nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="a7cdf-137">Il modulo logger registra tutti i messaggi provenienti dal broker in un file locale.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="a7cdf-138">Il diagramma a blocchi seguente illustra la pipeline del flusso di invio dei comandi del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Pipeline dell'invio dei comandi del dispositivo attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="a7cdf-140">Il modulo dell'hub IoT esegue periodicamente il polling dell'hub IoT per rilevare la presenza di nuovi messaggi di comando.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="a7cdf-141">Quando il modulo dell'hub IoT riceve un nuovo messaggio di comando, lo pubblica sul broker.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="a7cdf-142">Il modulo di mapping delle identità preleva il messaggio di comando e usa una tabella interna per convertire l'ID dispositivo dell'hub IoT in un indirizzo MAC di dispositivo,</span><span class="sxs-lookup"><span data-stu-id="a7cdf-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="a7cdf-143">quindi pubblica un nuovo messaggio che include l'indirizzo MAC del dispositivo di destinazione nella mappa delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="a7cdf-144">Il modulo BLE da cloud a dispositivo preleva il messaggio e lo converte nell'istruzione BLE appropriata per il modulo BLE.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="a7cdf-145">Dopodiché pubblica un nuovo messaggio.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="a7cdf-146">Il modulo BLE preleva il messaggio ed esegue l'istruzione di I/O comunicando con il dispositivo BLE.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="a7cdf-147">Il modulo logger registra tutti i messaggi provenienti dal broker in un file su disco.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7cdf-148">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a7cdf-148">Prerequisites</span></span>

<span data-ttu-id="a7cdf-149">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a7cdf-150">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a7cdf-151">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="a7cdf-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="a7cdf-152">È necessario un client SSH nel computer desktop per poter accedere in remoto alla riga di comando in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="a7cdf-153">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="a7cdf-154">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a7cdf-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a7cdf-155">La maggior parte delle distribuzioni Linux e Mac OS includono l'utilità SSH della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="a7cdf-156">Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="a7cdf-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="a7cdf-157">Preparare l'hardware</span><span class="sxs-lookup"><span data-stu-id="a7cdf-157">Prepare your hardware</span></span>

<span data-ttu-id="a7cdf-158">Questa esercitazione presuppone che si usi un dispositivo [SensorTag di Texas Instruments](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) connesso a un modulo Raspberry Pi 3 che esegue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="a7cdf-159">Installare Raspbian</span><span class="sxs-lookup"><span data-stu-id="a7cdf-159">Install Raspbian</span></span>

<span data-ttu-id="a7cdf-160">È possibile usare una delle opzioni seguenti per installare Raspbian nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="a7cdf-161">Per installare la versione più recente di Raspbian, usare l'interfaccia utente grafica [NOOBS][lnk-noobs].</span><span class="sxs-lookup"><span data-stu-id="a7cdf-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="a7cdf-162">[Scaricare][lnk-raspbian] manualmente l'immagine più recente del sistema operativo Raspbian e scriverla in una scheda SD.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="a7cdf-163">Accedere al terminale</span><span class="sxs-lookup"><span data-stu-id="a7cdf-163">Sign in and access the terminal</span></span>

<span data-ttu-id="a7cdf-164">Esistono due opzioni per accedere all'ambiente di un terminale in Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="a7cdf-165">Se a Raspberry Pi sono connessi una tastiera e un monitor, è possibile usare l'interfaccia utente grafica di Raspbian per accedere a una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="a7cdf-166">Accedere alla riga di comando in Raspberry Pi usando SSH dal computer desktop.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="a7cdf-167">Usare una finestra del terminale nell'interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="a7cdf-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="a7cdf-168">Le credenziali predefinite per Raspbian sono il nome utente **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="a7cdf-169">Nella barra della applicazioni dell'interfaccia utente grafica è possibile avviare l'utilità **Terminal** (Terminale) usando l'icona del monitor.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="a7cdf-170">Accedere con SSH</span><span class="sxs-lookup"><span data-stu-id="a7cdf-170">Sign in with SSH</span></span>

<span data-ttu-id="a7cdf-171">È possibile usare la riga di comando SSH per accedere a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="a7cdf-172">L'articolo [SSH (Secure Shell)][lnk-pi-ssh] (SSH - Secure Shell) descrive come configurare SSH in Raspberry Pi e come connettersi da [Windows][lnk-ssh-windows] o [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="a7cdf-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="a7cdf-173">Accedere con il nome utente **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="a7cdf-174">Installare BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="a7cdf-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="a7cdf-175">I moduli BLE comunicano con l'hardware Bluetooth tramite lo stack BlueZ.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="a7cdf-176">Per il corretto funzionamento dei moduli è necessaria la versione 5.37 di BlueZ.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="a7cdf-177">Queste istruzioni consentono di verificare che sia installata la versione corretta di BlueZ.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="a7cdf-178">Arrestare il daemon Bluetooth corrente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="a7cdf-179">Installare le dipendenze BlueZ:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="a7cdf-180">Scaricare il codice sorgente BlueZ da bluez.org:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a7cdf-181">Decomprimere il codice sorgente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="a7cdf-182">Passare alla cartella appena creata:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="a7cdf-183">Configurare il codice BlueZ da compilare:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="a7cdf-184">Compilare BlueZ:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="a7cdf-185">Al termine, installare BlueZ:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="a7cdf-186">Cambiare la configurazione del servizio systemd per bluetooth in modo che punti al nuovo daemon Bluetooth nel file `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="a7cdf-187">Sostituire la riga 'ExecStart' con il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="a7cdf-188">Abilitare la connettività al dispositivo SensorTag dal dispositivo Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a7cdf-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="a7cdf-189">Prima di eseguire l'esempio è necessario verificare che il dispositivo Raspberry Pi 3 possa connettersi al dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="a7cdf-190">Assicurarsi che l'utilità `rfkill` sia installata:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="a7cdf-191">Sbloccare Bluetooth sul dispositivo Raspberry Pi 3 e verificare che il numero di versione sia **5.37**:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="a7cdf-192">Per accedere a una shell del Bluetooth interattiva, avviare il servizio Bluetooth ed eseguire il comando **bluetoothctl**:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="a7cdf-193">Immettere il comando **power on** per accendere il controller bluetooth.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="a7cdf-194">L'output restituito dal comando è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="a7cdf-195">Nella shell Bluetooth interattiva immettere il comando **scan on** per cercare i dispositivi Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="a7cdf-196">L'output restituito dal comando è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="a7cdf-197">Rendere individuabile il dispositivo SensorTag premendo il pulsante piccolo (il LED verde dovrebbe lampeggiare).</span><span class="sxs-lookup"><span data-stu-id="a7cdf-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="a7cdf-198">Il modulo Raspberry Pi 3 dovrebbe individuare il dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="a7cdf-199">In questo esempio è possibile notare che l'indirizzo MAC del dispositivo SensorTag è **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="a7cdf-200">Disattivare la scansione immettendo il comando **scan off**:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="a7cdf-201">Connettersi al dispositivo SensorTag tramite il relativo indirizzo MAC immettendo**connect \<indirizzo MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="a7cdf-202">L'output di esempio seguente è abbreviato per maggiore chiarezza:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="a7cdf-203">È possibile elencare di nuovo le caratteristiche GATT del dispositivo usando il comando **list-attributes**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="a7cdf-204">È ora possibile disconnettersi dal dispositivo usando il comando **disconnect** e quindi uscire dalla shell Bluetooth con il comando **quit**:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="a7cdf-205">A questo punto si è pronti a eseguire l'esempio di IoT Edge BLE nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="a7cdf-206">Eseguire l'esempio di IoT Edge BLE</span><span class="sxs-lookup"><span data-stu-id="a7cdf-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="a7cdf-207">Per eseguire l'esempio IoT Edge BLE è necessario completare tre attività:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="a7cdf-208">Configurare due dispositivi di esempio nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="a7cdf-209">Compilare IoT Edge sul dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="a7cdf-210">Configurare ed eseguire l'esempio BLE sul dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="a7cdf-211">Al momento della redazione di questo documento, IoT Edge supporta solo moduli BLE in gateway che vengono eseguiti in Linux.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="a7cdf-212">Configurare due dispositivi di esempio nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a7cdf-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="a7cdf-213">[Creare un hub IoT][lnk-create-hub] nella sottoscrizione di Azure. Per completare questa procedura, è necessario disporre del nome dell'hub.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="a7cdf-214">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a7cdf-215">Aggiungere un dispositivo chiamato **SensorTag_01** all'hub IoT e prendere nota del relativo ID e della chiave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="a7cdf-216">È possibile usare lo strumento per [Esplora dispositivi o iothub-explorer][lnk-explorer-tools] per aggiungere il dispositivo all'hub IoT creato nel passaggio precedente e recuperarne la chiave.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="a7cdf-217">Il mapping del dispositivo al SensorTag avviene quando si configura il gateway.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="a7cdf-218">Compilare Azure IoT Edge su Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a7cdf-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="a7cdf-219">Installare le dipendenze per Azure IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="a7cdf-220">Usare i comandi seguenti per clonare IoT Edge e tutti i relativi moduli secondari nella directory home:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="a7cdf-221">Quando si ha una copia completa del repository di IoT Edge nel dispositivo Raspberry Pi 3, è possibile procedere alla compilazione usando il comando seguente dalla cartella contenente l'SDK:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="a7cdf-222">Configurare ed eseguire l'esempio BLE sul dispositivo Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a7cdf-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="a7cdf-223">Per avviare ed eseguire l'esempio, è necessario configurare ogni modulo IoT Edge coinvolto nell'attività del gateway.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="a7cdf-224">La configurazione viene definita in un file JSON ed è necessario configurare tutti e cinque i moduli IoT Edge coinvolti.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="a7cdf-225">Nell'archivio chiamato **gateway\_sample.json** è presente un file JSON di esempio che è possibile usare come base per creare il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="a7cdf-226">Il file si trova nella cartella **samples/ble_gateway_hl/src** della copia locale del repository IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="a7cdf-227">Le sezioni seguenti descrivono come modificare il file di configurazione per l'esempio BLE, supponendo che il repository IoT Edge si trovi nella cartella **/home/pi/iot-edge/** del dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="a7cdf-228">Se l'archivio si trova in un'altra posizione, modificare i percorsi di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="a7cdf-229">Configurazione del modulo logger</span><span class="sxs-lookup"><span data-stu-id="a7cdf-229">Logger configuration</span></span>

<span data-ttu-id="a7cdf-230">Se l'archivio del gateway si trova nella cartella **/home/pi/iot-edge/**, configurare il modulo logger nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="a7cdf-231">Configurazione del modulo BLE</span><span class="sxs-lookup"><span data-stu-id="a7cdf-231">BLE module configuration</span></span>

<span data-ttu-id="a7cdf-232">La configurazione di esempio per il dispositivo BLE presuppone che venga usato un dispositivo SensorTag di Texas Instruments.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="a7cdf-233">Dovrebbe essere possibile usare qualsiasi dispositivo BLE standard in grado di funzionare come periferica GATT, ma in tal caso sarà necessario aggiornare i dati e gli ID delle caratteristiche GATT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="a7cdf-234">Aggiungere l'indirizzo MAC del dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="a7cdf-235">Se non si usa un dispositivo SensorTag, esaminare la documentazione del dispositivo BLE per determinare se è necessario aggiornare i dati e gli ID delle caratteristiche GATT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="a7cdf-236">modulo dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="a7cdf-236">IoT Hub module</span></span>

<span data-ttu-id="a7cdf-237">Aggiungere il nome dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="a7cdf-238">Il valore del suffisso è in genere **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="a7cdf-239">Configurazione del modulo di mapping delle identità</span><span class="sxs-lookup"><span data-stu-id="a7cdf-239">Identity mapping module configuration</span></span>

<span data-ttu-id="a7cdf-240">Aggiungere l'indirizzo MAC del dispositivo SensorTag, nonché l'ID e la chiave del dispositivo **SensorTag_01** che è stato aggiunto all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="a7cdf-241">Configurazione del modulo di stampa BLE</span><span class="sxs-lookup"><span data-stu-id="a7cdf-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="a7cdf-242">Configurazione del modulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="a7cdf-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="a7cdf-243">Configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="a7cdf-243">Routing Configuration</span></span>

<span data-ttu-id="a7cdf-244">La configurazione seguente garantisce che i moduli IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="a7cdf-245">Il modulo **Logger** riceva e registri tutti i messaggi.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="a7cdf-246">Il modulo **SensorTag** invii i messaggi a entrambi i moduli **mapping** e **BLE Printer**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="a7cdf-247">Il modulo **mapping** invii i messaggi al modulo **IoTHub** per farli recapitare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="a7cdf-248">Il modulo **IoTHub** invii di nuovo i messaggi al modulo **mapping**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="a7cdf-249">Il modulo **mapping** invii i messaggi al modulo **BLEC2D**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="a7cdf-250">Il modulo **BLEC2D** invii di nuovo i messaggi al modulo **SensorTag**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="a7cdf-251">Per eseguire l'esempio, passare il percorso del file di configurazione JSON come parametro al codice binario **ble\_gateway**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="a7cdf-252">Il comando seguente assume che si stia usano il file di configurazione **gateway_sample.json**.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="a7cdf-253">Eseguire questo comando dalla cartella **iot-edge** in Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="a7cdf-254">Prima di eseguire l'esempio, potrebbe essere necessario premere il pulsante piccolo sul dispositivo SensorTag per renderlo individuabile.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="a7cdf-255">Durante l'esecuzione dell'esempio è possibile usare lo strumento [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o [iothub-explorer](https://github.com/Azure/iothub-explorer) per monitorare i messaggi che il gateway IoT Edge inoltra dal dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="a7cdf-256">Ad esempio, tramite iothub-explorer è possibile monitorare i messaggi da dispositivo a cloud usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="a7cdf-257">Inviare messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="a7cdf-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="a7cdf-258">Il modulo BLE supporta anche l'invio di comandi dall'hub IoT al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="a7cdf-259">È possibile usare lo strumento [Esplora dispositivi](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o [iothub-explorer](https://github.com/Azure/iothub-explorer) per inviare i messaggi JSON che il modulo BLE del gateway inoltra al dispositivo BLE.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="a7cdf-260">Se si usa il dispositivo SensorTag di Texas Instruments, è possibile attivare il LED rosso, il LED verde o il segnalatore acustico inviando comandi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="a7cdf-261">Prima dell'invio dei comandi dall'hub IoT, occorre tuttavia inviare i due messaggi JSON seguenti nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="a7cdf-262">Sarà quindi possibile inviare i comandi per attivare i LED o il segnalatore acustico.</span><span class="sxs-lookup"><span data-stu-id="a7cdf-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="a7cdf-263">Reimpostare tutti i LED e il segnalatore acustico (spegnerli):</span><span class="sxs-lookup"><span data-stu-id="a7cdf-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="a7cdf-264">Configurare l'I/O come "remote":</span><span class="sxs-lookup"><span data-stu-id="a7cdf-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="a7cdf-265">È possibile a questo punto inviare i comandi seguenti per attivare i LED o il segnalatore acustico sul dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="a7cdf-266">Accendere il LED rosso:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="a7cdf-267">Accendere il LED verde:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="a7cdf-268">Accendere il segnalatore acustico:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="a7cdf-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7cdf-269">Next Steps</span></span>

<span data-ttu-id="a7cdf-270">Per ottenere informazioni più avanzate su IoT Edge e provare alcuni esempi di codice, vedere le seguenti risorse ed esercitazioni per gli sviluppatori:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="a7cdf-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="a7cdf-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="a7cdf-272">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="a7cdf-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a7cdf-273">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a7cdf-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
