---
title: un dispositivo fisico con Azure IoT Edge aaaUse | Documenti Microsoft
description: Come toouse un hub IoT tooan di Texas strumenti SensorTag dispositivo toosend dati tramite un gateway perimetrale IoT in esecuzione in un dispositivo Raspberry Pi 3. gateway Hello viene creato utilizzando Azure IoT Edge.
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="1fa68-104">Utilizzare Azure IoT Edge su un tooIoT di messaggi da dispositivo a cloud tooforward Pi Raspberry Hub</span><span class="sxs-lookup"><span data-stu-id="1fa68-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="1fa68-105">Questa procedura dettagliata di hello [esempio consumo energetico Bluetooth] [ lnk-ble-samplecode] illustra come toouse [Azure IoT Edge] [ lnk-sdk] per:</span><span class="sxs-lookup"><span data-stu-id="1fa68-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="1fa68-106">Inoltrare i dati di telemetria da dispositivo a cloud tooIoT Hub da un dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="1fa68-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="1fa68-107">Inviare i comandi dal dispositivo fisico tooa di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="1fa68-108">In questa procedura dettagliata verranno trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="1fa68-108">This walkthrough covers:</span></span>

* <span data-ttu-id="1fa68-109">**Architettura**: importanti informazioni architetturale: esempio hello Bluetooth consumo energetico.</span><span class="sxs-lookup"><span data-stu-id="1fa68-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="1fa68-110">**Compilare ed eseguire**: esempio di esecuzione hello e toobuild necessari passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="1fa68-111">Architettura</span><span class="sxs-lookup"><span data-stu-id="1fa68-111">Architecture</span></span>

<span data-ttu-id="1fa68-112">Hello dettagliata mostra come toobuild ed eseguire un gateway esterno IoT su 3 Pi Raspberry che esegue Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="1fa68-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="1fa68-113">gateway Hello viene compilato utilizzando IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1fa68-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="1fa68-114">esempio Hello utilizza una data di temperatura toocollect dispositivo Texas strumenti SensorTag Bluetooth bassa energia (disattiva).</span><span class="sxs-lookup"><span data-stu-id="1fa68-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="1fa68-115">Quando si esegue hello gateway perimetrale IoT è:</span><span class="sxs-lookup"><span data-stu-id="1fa68-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="1fa68-116">Connette il dispositivo di SensorTag tooa utilizzando il protocollo di energia bassa Bluetooth (disattiva) hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="1fa68-117">Si connette tooIoT Hub utilizzando il protocollo HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="1fa68-118">Inoltra i dati di telemetria da hello SensorTag dispositivo tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="1fa68-119">Invia i comandi dal dispositivo di SensorTag toohello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="1fa68-120">gateway Hello contiene i seguenti moduli IoT Edge hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="1fa68-121">Oggetto *modulo BILITA* che interagisce con i dati di temperatura tooreceive dispositivo un BILITA da dispositivi hello e invia i comandi toohello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="1fa68-122">Oggetto *modulo toodevice di cloud BILITA* che converte i messaggi JSON inviati dall'IoT Hub in istruzioni BILE per hello *modulo BILITA*.</span><span class="sxs-lookup"><span data-stu-id="1fa68-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="1fa68-123">Oggetto *modulo logger* che registra tutti i gateway messaggi tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="1fa68-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="1fa68-124">Un *modulo di mapping delle identità* che esegue la conversione tra gli indirizzi MAC del dispositivo BLE e le identità dispositivo dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fa68-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="1fa68-125">Un *modulo IoT Hub* che consente di caricare hub IoT tooan dati di telemetria e riceve i comandi di dispositivo da un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fa68-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="1fa68-126">Oggetto *modulo stampante BILITA* che viene interpretata la telemetria dal dispositivo BILITA hello e stampa dati formattati toohello console tooenable risoluzione e il debug.</span><span class="sxs-lookup"><span data-stu-id="1fa68-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="1fa68-127">Il flusso dei dati tramite il gateway hello</span><span class="sxs-lookup"><span data-stu-id="1fa68-127">How data flows through hello gateway</span></span>

<span data-ttu-id="1fa68-128">Hello seguente diagramma a blocchi di seguito viene illustrato come pipeline di flusso dati di caricamento di hello telemetria.</span><span class="sxs-lookup"><span data-stu-id="1fa68-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Pipeline di caricamento dei dati di telemetria attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="1fa68-130">passaggi di Hello che un elemento di dati di telemetria accetta gli spostamenti da un tooIoT dispositivo BILITA Hub sono:</span><span class="sxs-lookup"><span data-stu-id="1fa68-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="1fa68-131">dispositivo BILITA Hello genera un campione di temperatura e lo invia tramite Bluetooth toohello BILITA modulo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="1fa68-132">modulo BILITA Hello riceve l'esempio hello e pubblica broker toohello con indirizzo MAC hello del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="1fa68-133">modulo di mapping identità Hello preleva il messaggio e utilizza un hello tootranslate tabella interna indirizzo MAC del dispositivo hello in un'identità del dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="1fa68-134">Un'identità dispositivo dell'hub IoT è costituita da un ID di dispositivo e una chiave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="1fa68-135">modulo di mapping identità Hello pubblica un nuovo messaggio che contiene dati di esempio hello temperatura, l'indirizzo MAC di hello del dispositivo hello e ID dispositivo hello chiave hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="1fa68-136">modulo di IoT Hub Hello riceve questo messaggio nuovo (generato dal modulo di mapping identità hello) e pubblica tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="1fa68-137">modulo di logger Hello registra tutti i messaggi da file di hello broker tooa locale.</span><span class="sxs-lookup"><span data-stu-id="1fa68-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="1fa68-138">Hello seguente diagramma a blocchi di seguito viene illustrato come pipeline di flusso dati di hello dispositivo comando:</span><span class="sxs-lookup"><span data-stu-id="1fa68-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Pipeline dell'invio dei comandi del dispositivo attraverso il gateway](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="1fa68-140">IoT Hub modulo esegue periodicamente il polling di Hello hello hub IoT per i nuovi messaggi di comando.</span><span class="sxs-lookup"><span data-stu-id="1fa68-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="1fa68-141">Quando il modulo di IoT Hub hello riceve un nuovo messaggio di comando, vengono pubblicati toohello broker.</span><span class="sxs-lookup"><span data-stu-id="1fa68-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="1fa68-142">modulo di mapping identità Hello preleva il messaggio di comando hello e utilizza un hello tootranslate tabella interna IoT Hub ID tooa dispositivo indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="1fa68-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="1fa68-143">Quindi, vengono pubblicati un nuovo messaggio che include l'indirizzo MAC di hello hello per dispositivo di destinazione nel mapping di proprietà hello del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="1fa68-144">modulo BILITA Cloud a dispositivo Hello preleva il messaggio e lo converte in istruzione BILITA corretta di hello per il modulo BILITA hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="1fa68-145">Dopodiché pubblica un nuovo messaggio.</span><span class="sxs-lookup"><span data-stu-id="1fa68-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="1fa68-146">modulo BILITA Hello preleva il messaggio ed esegue istruzioni dei / o hello comunicando con dispositivo BILITA hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="1fa68-147">modulo di logger Hello registra tutti i messaggi dal file di disco tooa broker hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fa68-148">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1fa68-148">Prerequisites</span></span>

<span data-ttu-id="1fa68-149">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="1fa68-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1fa68-150">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1fa68-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1fa68-151">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="1fa68-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="1fa68-152">È necessario client SSH nel tooenable computer desktop è tooremotely accesso hello della riga di comando in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="1fa68-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="1fa68-153">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="1fa68-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="1fa68-154">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="1fa68-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="1fa68-155">La maggior parte delle distribuzioni di Linux e Mac OS includono hello della riga di comando SSH utilità.</span><span class="sxs-lookup"><span data-stu-id="1fa68-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="1fa68-156">Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="1fa68-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="1fa68-157">Preparare l'hardware</span><span class="sxs-lookup"><span data-stu-id="1fa68-157">Prepare your hardware</span></span>

<span data-ttu-id="1fa68-158">In questa esercitazione si presuppone l'uso un [SensorTag strumenti Texas](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo connesso tooa Raspberry Pi 3 Raspbian di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1fa68-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="1fa68-159">Installare Raspbian</span><span class="sxs-lookup"><span data-stu-id="1fa68-159">Install Raspbian</span></span>

<span data-ttu-id="1fa68-160">È possibile utilizzare una delle seguenti opzioni tooinstall Raspbian sul dispositivo Raspberry Pi 3 hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="1fa68-161">versione più recente di hello tooinstall di Raspbian, utilizzare hello [NOOBS] [ lnk-noobs] interfaccia utente grafica.</span><span class="sxs-lookup"><span data-stu-id="1fa68-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="1fa68-162">Manualmente [scaricare] [ lnk-raspbian] e scrivere hello immagine più recente della scheda hello Raspbian del sistema operativo tooan SD.</span><span class="sxs-lookup"><span data-stu-id="1fa68-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="1fa68-163">Accesso e terminal hello</span><span class="sxs-lookup"><span data-stu-id="1fa68-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="1fa68-164">Sono presenti due opzioni tooaccess un ambiente terminal le Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="1fa68-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="1fa68-165">Se si dispone di una tastiera e monitorare connesso tooyour Raspberry Pi, è possibile utilizzare hello GUI Raspbian tooaccess una finestra terminale.</span><span class="sxs-lookup"><span data-stu-id="1fa68-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="1fa68-166">Riga di comando hello accesso con le pi greco Raspberry tramite SSH nel computer desktop.</span><span class="sxs-lookup"><span data-stu-id="1fa68-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="1fa68-167">Utilizzare una finestra terminal in hello GUI</span><span class="sxs-lookup"><span data-stu-id="1fa68-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="1fa68-168">le credenziali predefinite Hello per Raspbian sono username **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="1fa68-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="1fa68-169">Nella barra delle applicazioni hello in hello GUI, è possibile avviare hello **Terminal** utilità utilizzando l'icona di hello simile a un monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="1fa68-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="1fa68-170">Accedere con SSH</span><span class="sxs-lookup"><span data-stu-id="1fa68-170">Sign in with SSH</span></span>

<span data-ttu-id="1fa68-171">È possibile utilizzare SSH per l'accesso da riga di comando tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="1fa68-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="1fa68-172">articolo Hello [SSH (Secure Shell)] [ lnk-pi-ssh] viene descritto come tooconfigure SSH sul pi greco Raspberry e come tooconnect da [Windows] [ lnk-ssh-windows] o [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="1fa68-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="1fa68-173">Accedere con il nome utente **pi** e la password **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="1fa68-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="1fa68-174">Installare BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="1fa68-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="1fa68-175">i moduli BILITA Hello comunicare toohello Bluetooth hardware tramite stack BlueZ hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="1fa68-176">È necessario versione 5.37 di BlueZ per hello moduli toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="1fa68-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="1fa68-177">Queste istruzioni assicurarsi che sia installata hello versione corretta di BlueZ.</span><span class="sxs-lookup"><span data-stu-id="1fa68-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="1fa68-178">Arrestare il daemon bluetooth corrente di hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="1fa68-179">Installare le dipendenze BlueZ hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="1fa68-180">Scaricare il codice sorgente di hello BlueZ da bluez.org:</span><span class="sxs-lookup"><span data-stu-id="1fa68-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="1fa68-181">Decomprimere il codice sorgente hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="1fa68-182">Cambia cartella toohello appena creato di directory:</span><span class="sxs-lookup"><span data-stu-id="1fa68-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="1fa68-183">Configurare hello BlueZ codice toobe compilato:</span><span class="sxs-lookup"><span data-stu-id="1fa68-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="1fa68-184">Compilare BlueZ:</span><span class="sxs-lookup"><span data-stu-id="1fa68-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="1fa68-185">Al termine, installare BlueZ:</span><span class="sxs-lookup"><span data-stu-id="1fa68-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="1fa68-186">Modificare la configurazione di servizio per bluetooth in modo che punti toohello nuovo daemon bluetooth nel file hello systemd `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="1fa68-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="1fa68-187">Sostituire riga 'ExecStart' hello con hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="1fa68-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="1fa68-188">Abilitazione del dispositivo SensorTag toohello connettività dal dispositivo Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1fa68-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="1fa68-189">Prima di esempio hello in esecuzione, è necessario che il Pi 3 Raspberry possano connettersi dispositivo SensorTag toohello tooverify.</span><span class="sxs-lookup"><span data-stu-id="1fa68-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="1fa68-190">Assicurarsi di hello `rfkill` utilità è installata:</span><span class="sxs-lookup"><span data-stu-id="1fa68-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="1fa68-191">Sbloccare bluetooth su hello Raspberry Pi 3, verificare che il numero di versione di hello **5.37**:</span><span class="sxs-lookup"><span data-stu-id="1fa68-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="1fa68-192">shell interattiva bluetooth di hello tooenter, avviare il servizio bluetooth hello ed eseguire hello **bluetoothctl** comando:</span><span class="sxs-lookup"><span data-stu-id="1fa68-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="1fa68-193">Immettere il comando hello **accensione** toopower controller bluetooth hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="1fa68-194">comando Hello restituisce seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="1fa68-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="1fa68-195">Nella shell interattiva bluetooth hello, immettere il comando hello **analisi** tooscan per i dispositivi bluetooth.</span><span class="sxs-lookup"><span data-stu-id="1fa68-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="1fa68-196">comando Hello restituisce seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="1fa68-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="1fa68-197">Rendere individuabile un dispositivo SensorTag hello premendo hello piccolo pulsante (Buongiorno lampeggiamento LED verde).</span><span class="sxs-lookup"><span data-stu-id="1fa68-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="1fa68-198">Hello Raspberry Pi 3 deve individuare dispositivi SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="1fa68-199">In questo esempio, è possibile visualizzare tale indirizzo MAC di hello SensorTag dispositivo hello **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="1fa68-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="1fa68-200">Disattivare l'analisi immettendo hello **analisi** comando:</span><span class="sxs-lookup"><span data-stu-id="1fa68-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="1fa68-201">Connettere il dispositivo di SensorTag tooyour tramite il relativo indirizzo MAC immettendo **connettersi \<indirizzo MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="1fa68-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="1fa68-202">Per maggiore chiarezza, è abbreviato Hello seguente esempio di output:</span><span class="sxs-lookup"><span data-stu-id="1fa68-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="1fa68-203">È possibile elencare le caratteristiche di GATT hello del dispositivo hello utilizzando hello **elenco attributi** comando.</span><span class="sxs-lookup"><span data-stu-id="1fa68-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="1fa68-204">È ora possibile disconnettersi dal dispositivo hello utilizzando hello **disconnettere** comando e uscire dalla shell bluetooth hello utilizzando hello **chiudere** comando:</span><span class="sxs-lookup"><span data-stu-id="1fa68-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="1fa68-205">A questo punto è pronto toorun: esempio hello IoT Edge disattiva il 3 Pi Raspberry.</span><span class="sxs-lookup"><span data-stu-id="1fa68-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="1fa68-206">Eseguire l'esempio IoT Edge BILITA hello</span><span class="sxs-lookup"><span data-stu-id="1fa68-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="1fa68-207">esempio di IoT Edge BILITA toorun hello, è necessario toocomplete tre attività:</span><span class="sxs-lookup"><span data-stu-id="1fa68-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="1fa68-208">Configurare due dispositivi di esempio nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fa68-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="1fa68-209">Compilare IoT Edge sul dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1fa68-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="1fa68-210">Configurare ed eseguire l'esempio BILITA hello sul dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1fa68-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="1fa68-211">Al momento della scrittura hello IoT Edge supporta solo i moduli BILITA gateway su Linux.</span><span class="sxs-lookup"><span data-stu-id="1fa68-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="1fa68-212">Configurare due dispositivi di esempio nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="1fa68-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="1fa68-213">[Creazione di un hub IoT] [ lnk-create-hub] nella sottoscrizione di Azure, è necessario il nome di hello di toocomplete l'hub in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="1fa68-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="1fa68-214">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1fa68-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1fa68-215">Aggiungere un dispositivo chiamato **SensorTag_01** tooyour IoT hub e prendere nota della chiave id e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="1fa68-216">È possibile utilizzare hello [Esplora dispositivo o l'hub IOT-Esplora] [ lnk-explorer-tools] strumenti tooadd l'hub IoT toohello di dispositivi creata nel passaggio precedente hello e tooretrieve la relativa chiave.</span><span class="sxs-lookup"><span data-stu-id="1fa68-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="1fa68-217">Eseguire il mapping in questo dispositivo toohello SensorTag dispositivo quando si configura gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="1fa68-218">Compilare Azure IoT Edge su Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1fa68-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="1fa68-219">Installare le dipendenze per Azure IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="1fa68-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="1fa68-220">I comandi seguenti di hello utilizzare, tooclone IoT Edge e tutti i relativi dei Sottomoduli tooyour home directory:</span><span class="sxs-lookup"><span data-stu-id="1fa68-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="1fa68-221">Quando si dispone di una copia completa di hello repository IoT bordo il 3 Pi Raspberry, è possibile compilare utilizzando hello comando seguente dalla cartella hello contenente hello SDK:</span><span class="sxs-lookup"><span data-stu-id="1fa68-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="1fa68-222">Configurare ed eseguire l'esempio BILITA hello il 3 Pi Raspberry</span><span class="sxs-lookup"><span data-stu-id="1fa68-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="1fa68-223">toobootstrap e l'esempio hello esecuzione, è necessario configurare ogni modulo IoT Edge che partecipa nel gateway hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="1fa68-224">La configurazione viene definita in un file JSON ed è necessario configurare tutti e cinque i moduli IoT Edge coinvolti.</span><span class="sxs-lookup"><span data-stu-id="1fa68-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="1fa68-225">È un file JSON di esempio in repository hello denominato **gateway\_sample.json** che è possibile utilizzare come punto di partenza per la creazione di un file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="1fa68-226">Questo file è hello **ble_gateway/samples/src** cartella nella copia locale di hello repository IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1fa68-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="1fa68-227">Hello nelle sezioni seguenti descrivono come tooedit questa configurazione del file di esempio BILITA hello e si presuppone che hello repository IoT Edge è hello **/home/pi/iot-edge /** cartella il Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1fa68-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="1fa68-228">Se il repository di hello è altrove, regolare i percorsi di hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="1fa68-229">Configurazione del modulo logger</span><span class="sxs-lookup"><span data-stu-id="1fa68-229">Logger configuration</span></span>

<span data-ttu-id="1fa68-230">Presupponendo che si trova il repository di gateway hello in hello **/home/pi/iot-edge /** cartella, configurare il modulo di logger hello come segue:</span><span class="sxs-lookup"><span data-stu-id="1fa68-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="1fa68-231">Configurazione del modulo BLE</span><span class="sxs-lookup"><span data-stu-id="1fa68-231">BLE module configuration</span></span>

<span data-ttu-id="1fa68-232">configurazione di esempio Hello per dispositivo BILITA hello presuppone un dispositivo SensorTag strumenti Texas.</span><span class="sxs-lookup"><span data-stu-id="1fa68-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="1fa68-233">Qualsiasi dispositivo BILITA standard che può operare come un GATT periferiche dovrebbero funzionare, ma potrebbe essere necessario tooupdate hello GATT caratteristica ID e dati.</span><span class="sxs-lookup"><span data-stu-id="1fa68-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="1fa68-234">Aggiungere l'indirizzo MAC hello del dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="1fa68-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="1fa68-235">Se non si utilizza un dispositivo SensorTag, vedere documentazione di hello per le toodetermine dispositivo BILITA se è necessario tooupdate hello GATT caratteristica ID e i valori dei dati.</span><span class="sxs-lookup"><span data-stu-id="1fa68-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="1fa68-236">modulo dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="1fa68-236">IoT Hub module</span></span>

<span data-ttu-id="1fa68-237">Aggiungere il nome di hello dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="1fa68-238">valore suffisso Hello è in genere **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="1fa68-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="1fa68-239">Configurazione del modulo di mapping delle identità</span><span class="sxs-lookup"><span data-stu-id="1fa68-239">Identity mapping module configuration</span></span>

<span data-ttu-id="1fa68-240">Aggiungere l'indirizzo MAC di hello del dispositivo SensorTag e hello dispositivo chiave e ID di hello **SensorTag_01** dispositivo tooyour IoT Hub è stato aggiunto:</span><span class="sxs-lookup"><span data-stu-id="1fa68-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="1fa68-241">Configurazione del modulo di stampa BLE</span><span class="sxs-lookup"><span data-stu-id="1fa68-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="1fa68-242">Configurazione del modulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="1fa68-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="1fa68-243">Configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="1fa68-243">Routing Configuration</span></span>

<span data-ttu-id="1fa68-244">la configurazione seguente Hello assicura seguente hello routing tra i moduli di IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="1fa68-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="1fa68-245">Hello **Logger** modulo riceve e registra tutti i messaggi.</span><span class="sxs-lookup"><span data-stu-id="1fa68-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="1fa68-246">Hello **SensorTag** modulo Invia hello tooboth messaggi **mapping** e **stampante BILITA** moduli.</span><span class="sxs-lookup"><span data-stu-id="1fa68-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="1fa68-247">Hello **mapping** modulo Invia messaggi toohello **l'hub IOT** toobe modulo inviato tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="1fa68-248">Hello **l'hub IOT** modulo Invia messaggi di risposta toohello **mapping** modulo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="1fa68-249">Hello **mapping** modulo Invia messaggi toohello **BLEC2D** modulo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="1fa68-250">Hello **BLEC2D** modulo Invia messaggi di risposta toohello **Tag sensore** modulo.</span><span class="sxs-lookup"><span data-stu-id="1fa68-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="1fa68-251">esempio hello toorun, file di configurazione JSON per la toohello percorso pass hello come un parametro di toohello **bilita\_gateway** binario.</span><span class="sxs-lookup"><span data-stu-id="1fa68-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="1fa68-252">Hello comando riportato di seguito si presuppone l'uso hello **gateway_sample.json** file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1fa68-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="1fa68-253">Eseguire il comando seguente da hello **iot edge** cartella hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="1fa68-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="1fa68-254">Potrebbe essere necessario toopress hello piccolo pulsante hello SensorTag dispositivo toomake è individuabile prima di eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="1fa68-255">Quando si esegue l'esempio hello, è possibile utilizzare hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) hello messaggi hello toomonitor di strumento gateway perimetrale IoT inoltra dal dispositivo SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="1fa68-256">Ad esempio, tramite l'hub IOT explorer è possibile monitorare i messaggi da dispositivo a cloud utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1fa68-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="1fa68-257">Inviare messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="1fa68-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="1fa68-258">modulo BILITA Hello supporta anche l'invio di comandi dal dispositivo toohello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="1fa68-259">È possibile utilizzare hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) i messaggi JSON di strumento toosend modulo hello BILITA gateway inoltra sul dispositivo BILITA toohello.</span><span class="sxs-lookup"><span data-stu-id="1fa68-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="1fa68-260">Se si usa hello Texas strumenti SensorTag dispositivo, è possibile attivare il LED di colore rosso hello, LED verde o cicalino inviando i comandi da IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1fa68-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="1fa68-261">Prima di inviare comandi dall'IoT Hub, inviare innanzitutto hello due messaggi JSON nell'ordine seguente.</span><span class="sxs-lookup"><span data-stu-id="1fa68-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="1fa68-262">È quindi possibile inviare qualsiasi hello comandi tooturn luci hello o cicalino.</span><span class="sxs-lookup"><span data-stu-id="1fa68-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="1fa68-263">Reimposta tutti i LED e cicalino hello (spegnerli):</span><span class="sxs-lookup"><span data-stu-id="1fa68-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="1fa68-264">Configurare l'I/O come "remote":</span><span class="sxs-lookup"><span data-stu-id="1fa68-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="1fa68-265">È ora possibile inviare uno qualsiasi dei seguenti comandi tooturn luci hello o cicalino sul dispositivo SensorTag hello hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="1fa68-266">Attiva il LED di colore rosso hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="1fa68-267">Attiva il LED verde hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="1fa68-268">Attivare cicalino hello:</span><span class="sxs-lookup"><span data-stu-id="1fa68-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="1fa68-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fa68-269">Next Steps</span></span>

<span data-ttu-id="1fa68-270">Se si desidera toogain conoscenze più avanzate del bordo IoT e sperimentare alcuni esempi di codice, visitare hello esercitazioni per sviluppatori e risorse:</span><span class="sxs-lookup"><span data-stu-id="1fa68-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="1fa68-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="1fa68-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="1fa68-272">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="1fa68-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1fa68-273">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="1fa68-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
