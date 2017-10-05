---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 1: Configurare il dispositivo | Documentazione Microsoft'
description: Questa lezione illustra come configurare Raspberry Pi 3 per il primo uso e installare Raspbian, un sistema operativo gratuito ottimizzato per l'hardware Raspberry Pi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "installare raspbian, scaricare raspbian, come installare raspbian, configurazione di raspbian, raspberry pi - installare raspbian, raspberry pi - installare il sistema operativo, raspberry pi - installazione della scheda sd, connessione raspberry pi, connettersi a raspberry pi, connettività di raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="356ac-104">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="356ac-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="356ac-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="356ac-105">What you will do</span></span>
<span data-ttu-id="356ac-106">Configurare Pi per il primo uso e installare il sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="356ac-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="356ac-107">Raspbian è un sistema operativo gratuito ottimizzato per l'hardware Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="356ac-108">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="356ac-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="356ac-109">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="356ac-109">What you will learn</span></span>
<span data-ttu-id="356ac-110">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="356ac-110">In this article, you will learn:</span></span>

* <span data-ttu-id="356ac-111">Come installare Raspbian in Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="356ac-112">Come accendere Pi tramite un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="356ac-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="356ac-113">Come connettere Pi alla rete tramite un cavo Ethernet o la rete wireless.</span><span class="sxs-lookup"><span data-stu-id="356ac-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="356ac-114">Come aggiungere un LED alla basetta sperimentale e connetterla a Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="356ac-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="356ac-115">What you need</span></span>
<span data-ttu-id="356ac-116">Per completare questa operazione, tenere a portata di mano i componenti seguenti inclusi nello starter kit di Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="356ac-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="356ac-117">Scheda di Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="356ac-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="356ac-118">Scheda microSD da 16 GB</span><span class="sxs-lookup"><span data-stu-id="356ac-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="356ac-119">Alimentatore da 5 V/2 A con cavo micro USB da 1,8 metri</span><span class="sxs-lookup"><span data-stu-id="356ac-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="356ac-120">Basetta sperimentale</span><span class="sxs-lookup"><span data-stu-id="356ac-120">The breadboard</span></span>
* <span data-ttu-id="356ac-121">Cavi del connettore</span><span class="sxs-lookup"><span data-stu-id="356ac-121">Connector wires</span></span>
* <span data-ttu-id="356ac-122">Resistore da 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="356ac-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="356ac-123">LED da 10 mm a luce diffusa</span><span class="sxs-lookup"><span data-stu-id="356ac-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="356ac-124">Cavo Ethernet</span><span class="sxs-lookup"><span data-stu-id="356ac-124">The Ethernet cable</span></span>

![Contenuto dello starter kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="356ac-126">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="356ac-126">You also need:</span></span>

* <span data-ttu-id="356ac-127">Connessione cablata o wireless a cui connettere Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="356ac-128">Scheda USB-SD o mini-SD con cui masterizzare l'immagine del sistema operativo nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="356ac-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="356ac-129">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="356ac-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="356ac-130">Il computer viene usato per installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="356ac-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="356ac-131">Connessione Internet per scaricare gli strumenti e il software necessari.</span><span class="sxs-lookup"><span data-stu-id="356ac-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="356ac-132">Installare Raspbian nella scheda microSD</span><span class="sxs-lookup"><span data-stu-id="356ac-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="356ac-133">Preparare la scheda microSD per l'installazione dell'immagine di Raspbian.</span><span class="sxs-lookup"><span data-stu-id="356ac-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="356ac-134">Scaricare Raspbian.</span><span class="sxs-lookup"><span data-stu-id="356ac-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="356ac-135">[Scaricare](https://www.raspberrypi.org/downloads/raspbian/) il file ZIP per Raspbian Jessie with Pixel.</span><span class="sxs-lookup"><span data-stu-id="356ac-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="356ac-136">Estrarre l'immagine di Raspbian in una cartella nel computer.</span><span class="sxs-lookup"><span data-stu-id="356ac-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="356ac-137">Installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="356ac-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="356ac-138">[Scaricare](https://www.etcher.io) e installare l'utilità di masterizzazione Etcher per schede SD.</span><span class="sxs-lookup"><span data-stu-id="356ac-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="356ac-139">Eseguire Etcher e selezionare l'immagine di Raspbian estratta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="356ac-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="356ac-140">Selezionare l'unità della scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="356ac-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="356ac-141">Si noti che Etcher potrebbe avere già selezionato l'unità corretta.</span><span class="sxs-lookup"><span data-stu-id="356ac-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="356ac-142">Fare clic su **Flash** per installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="356ac-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="356ac-143">Rimuovere la scheda microSD dal computer al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="356ac-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="356ac-144">È possibile rimuovere direttamente la scheda microSD perché viene espulsa o smontata automaticamente da Etcher al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="356ac-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="356ac-145">Inserire la scheda microSD in Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-145">Insert the microSD card into your Pi.</span></span>

![Inserire la scheda SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="356ac-147">Accendere Pi</span><span class="sxs-lookup"><span data-stu-id="356ac-147">Turn on Pi</span></span>
<span data-ttu-id="356ac-148">Accendere Pi usando il cavo micro USB e l'alimentatore.</span><span class="sxs-lookup"><span data-stu-id="356ac-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Accendere](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="356ac-150">È importante usare l'alimentatore da almeno 2 A incluso nel kit per garantire un'alimentazione sufficiente al corretto funzionamento del dispositivo Raspberry.</span><span class="sxs-lookup"><span data-stu-id="356ac-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="356ac-151">Abilitare SSH</span><span class="sxs-lookup"><span data-stu-id="356ac-151">Enable SSH</span></span>
<span data-ttu-id="356ac-152">A partire dalla versione di novembre 2016, Raspbian ha il server SSH disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="356ac-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="356ac-153">È necessario abilitarlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="356ac-153">You need to enable it manually.</span></span> <span data-ttu-id="356ac-154">A tale scopo, fare riferimento alle [istruzioni ufficiali](https://www.raspberrypi.org/documentation/remote-access/ssh/) o collegare un monitor e passare a **Preferences -> Raspberry Pi Configuration** (Preferenze-> Configurazione Raspberry Pi).</span><span class="sxs-lookup"><span data-stu-id="356ac-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="356ac-155">Connettere Raspberry Pi 3 alla rete</span><span class="sxs-lookup"><span data-stu-id="356ac-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="356ac-156">È possibile connettere Pi a una rete cablata oppure a una rete wireless.</span><span class="sxs-lookup"><span data-stu-id="356ac-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="356ac-157">Verificare che Pi sia connesso alla stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="356ac-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="356ac-158">È ad esempio possibile connettere Pi allo stesso commutatore a cui è connesso il computer.</span><span class="sxs-lookup"><span data-stu-id="356ac-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="356ac-159">Connettersi a una rete cablata</span><span class="sxs-lookup"><span data-stu-id="356ac-159">Connect to a wired network</span></span>
<span data-ttu-id="356ac-160">Per connettere Pi alla rete cablata, usare il cavo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="356ac-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="356ac-161">Quando viene stabilita la connessione, i due LED del dispositivo si illuminano.</span><span class="sxs-lookup"><span data-stu-id="356ac-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Connettersi tramite cavo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="356ac-163">Connettersi a una rete wireless</span><span class="sxs-lookup"><span data-stu-id="356ac-163">Connect to a wireless network</span></span>
<span data-ttu-id="356ac-164">Per connettere il dispositivo alla rete wireless, vedere le [istruzioni](https://www.raspberrypi.org/learning/software-guide/wifi/) riportate nella Guida di Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="356ac-165">Per seguire tali istruzioni è prima necessario connettere un monitor e una tastiera al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="356ac-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="356ac-166">Collegare il LED a Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="356ac-166">Connect the LED to Pi</span></span>
<span data-ttu-id="356ac-167">Per completare questa attività, usare la [basetta sperimentale](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), i cavi del connettore, il LED e il resistore.</span><span class="sxs-lookup"><span data-stu-id="356ac-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="356ac-168">Collegarli alle porte GPIO ([General-Purpose Input/Output](https://www.raspberrypi.org/documentation/usage/gpio/)) di Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Basetta sperimentale, LED e resistore](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="356ac-170">Collegare il piedino corto del LED alla porta **GPIO GND (pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="356ac-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="356ac-171">Collegare il piedino lungo del LED a un piedino del resistore.</span><span class="sxs-lookup"><span data-stu-id="356ac-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="356ac-172">Collegare l'altro piedino del resistore alla porta **GPIO 4 (pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="356ac-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="356ac-173">È importante rispettare la polarità del LED,</span><span class="sxs-lookup"><span data-stu-id="356ac-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="356ac-174">generalmente impostata come attiva bassa.</span><span class="sxs-lookup"><span data-stu-id="356ac-174">This polarity setting is commonly known as Active Low.</span></span>

![Piedinatura](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="356ac-176">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="356ac-176">Congratulations!</span></span> <span data-ttu-id="356ac-177">Il dispositivo Raspberry Pi è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="356ac-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="356ac-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="356ac-178">Summary</span></span>
<span data-ttu-id="356ac-179">In questo articolo si è appreso come configurare il dispositivo Raspberry Pi installando Raspbian, connettendo il dispositivo alla rete e collegando un LED al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="356ac-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="356ac-180">Si noti che il LED non si illumina ancora.</span><span class="sxs-lookup"><span data-stu-id="356ac-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="356ac-181">L'attività successiva consiste nell'installazione del software e degli strumenti necessari per preparare l'esecuzione di un'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="356ac-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![L'hardware è pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="356ac-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="356ac-183">Next steps</span></span>
[<span data-ttu-id="356ac-184">Ottenere gli strumenti</span><span class="sxs-lookup"><span data-stu-id="356ac-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

