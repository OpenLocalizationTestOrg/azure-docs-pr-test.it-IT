---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: "Installare hello Raspbian del sistema operativo, un sistema operativo gratuito che è ottimizzato per hello hardware Pi Raspberry configurare Raspberry Pi 3 per il primo utilizzo."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "installazione raspbian, raspbian download, la connettività di pi greco, al lampone tooraspberry connettersi come raspbian tooinstall, raspbian l'installazione, al lampone pi installazione raspbian, al lampone pi installazione del sistema operativo, al lampone pi sd card installazione, al lampone pi connect,"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="21883-104">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="21883-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="21883-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="21883-105">What you will do</span></span>
<span data-ttu-id="21883-106">Configurare Pi per il primo utilizzo e installare hello Raspbian del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="21883-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="21883-107">Raspbian è un sistema operativo gratuito che è ottimizzato per hello hardware Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="21883-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="21883-108">Se si verificano problemi, è possibile cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="21883-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="21883-109">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="21883-109">What you will learn</span></span>
<span data-ttu-id="21883-110">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="21883-110">In this article, you will learn:</span></span>

* <span data-ttu-id="21883-111">Come tooinstall Raspbian su Pi.</span><span class="sxs-lookup"><span data-stu-id="21883-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="21883-112">Come toopower backup Pi tramite un cavo USB.</span><span class="sxs-lookup"><span data-stu-id="21883-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="21883-113">Come tooconnect Pi toohello rete tramite un cavo Ethernet o una rete wireless.</span><span class="sxs-lookup"><span data-stu-id="21883-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="21883-114">Come tooadd toohello un LED breadboard e connetterla tooPi.</span><span class="sxs-lookup"><span data-stu-id="21883-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="21883-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="21883-115">What you will need</span></span>
<span data-ttu-id="21883-116">toocomplete questa operazione, è necessario hello dallo Starter Kit di Raspberry Pi 3 le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="21883-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="21883-117">Hello Lavagna Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="21883-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="21883-118">scheda microSD 16 GB Hello</span><span class="sxs-lookup"><span data-stu-id="21883-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="21883-119">Hello 5 volt 2 amp alimentatore con il cavo USB micro di hello 6-ft</span><span class="sxs-lookup"><span data-stu-id="21883-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="21883-120">breadboard Hello</span><span class="sxs-lookup"><span data-stu-id="21883-120">hello breadboard</span></span>
* <span data-ttu-id="21883-121">Cavi del connettore</span><span class="sxs-lookup"><span data-stu-id="21883-121">Connector wires</span></span>
* <span data-ttu-id="21883-122">Resistore da 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="21883-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="21883-123">LED da 10 mm a luce diffusa</span><span class="sxs-lookup"><span data-stu-id="21883-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="21883-124">Hello cavo Ethernet</span><span class="sxs-lookup"><span data-stu-id="21883-124">hello Ethernet cable</span></span>

![Contenuto dello starter kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="21883-126">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="21883-126">You also need:</span></span>

* <span data-ttu-id="21883-127">Una connessione cablata o wireless per Pi tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="21883-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="21883-128">Un USB SD adapter o miniSD card tooburn hello immagine del sistema operativo nella scheda microSD hello.</span><span class="sxs-lookup"><span data-stu-id="21883-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="21883-129">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="21883-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="21883-130">computer Hello è usato tooinstall Raspbian scheda microSD hello.</span><span class="sxs-lookup"><span data-stu-id="21883-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="21883-131">Un toodownload connessione Internet hello software e gli strumenti necessari.</span><span class="sxs-lookup"><span data-stu-id="21883-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="21883-132">Installare Raspbian scheda microSD hello</span><span class="sxs-lookup"><span data-stu-id="21883-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="21883-133">Preparare una scheda microSD hello per l'installazione dell'immagine Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="21883-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="21883-134">Scaricare Raspbian.</span><span class="sxs-lookup"><span data-stu-id="21883-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="21883-135">[Scaricare](https://www.raspberrypi.org/downloads/raspbian/) file con estensione zip hello per Raspbian Jessie con Pixel.</span><span class="sxs-lookup"><span data-stu-id="21883-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="21883-136">Estrarre la cartella di hello Raspbian immagine tooa nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="21883-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="21883-137">Installare una scheda microSD di Raspbian toohello.</span><span class="sxs-lookup"><span data-stu-id="21883-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="21883-138">[Scaricare](https://www.etcher.io) e installare hello Etcher SD card masterizzatore utilità.</span><span class="sxs-lookup"><span data-stu-id="21883-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="21883-139">Eseguire Etcher e selezionare l'immagine Raspbian hello estratta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="21883-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="21883-140">Selezionare un'unità scheda microSD hello.</span><span class="sxs-lookup"><span data-stu-id="21883-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="21883-141">Si noti che Etcher potrebbe essere stata già selezionata unità corretta hello.</span><span class="sxs-lookup"><span data-stu-id="21883-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="21883-142">Fare clic su **Flash** tooinstall Raspbian toohello microSD scheda.</span><span class="sxs-lookup"><span data-stu-id="21883-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="21883-143">Rimuovi scheda microSD hello dal computer al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="21883-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="21883-144">Scheda microSD di hello tooremove provvisoria è direttamente perché Etcher Smonta scheda microSD hello dopo il completamento o rimuove automaticamente.</span><span class="sxs-lookup"><span data-stu-id="21883-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="21883-145">Inserire scheda microSD hello Pi.</span><span class="sxs-lookup"><span data-stu-id="21883-145">Insert hello microSD card into Pi.</span></span>

![Inserire hello SD card](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="21883-147">Accendere Pi</span><span class="sxs-lookup"><span data-stu-id="21883-147">Turn on Pi</span></span>
<span data-ttu-id="21883-148">Attivare Pi tramite cavo USB micro hello e alimentatore hello.</span><span class="sxs-lookup"><span data-stu-id="21883-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Accendere](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="21883-150">È importante toouse hello alimentatore nel kit di hello almeno toomake 2A che sia il Raspberry sufficiente toowork power correttamente.</span><span class="sxs-lookup"><span data-stu-id="21883-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="21883-151">Abilitare SSH</span><span class="sxs-lookup"><span data-stu-id="21883-151">Enable SSH</span></span>
<span data-ttu-id="21883-152">A partire dalla versione di novembre 2016 hello, Raspbian ha server SSH hello disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="21883-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="21883-153">È necessario tooenable è manualmente.</span><span class="sxs-lookup"><span data-stu-id="21883-153">You need tooenable it manually.</span></span> <span data-ttu-id="21883-154">È possibile fare riferimento toohello [istruzioni ufficiale](https://www.raspberrypi.org/documentation/remote-access/ssh/) o collegare un monitor e andare troppo**Preferenze -> configurazione Pi Raspberry** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="21883-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="21883-155">Connessione di rete toohello Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="21883-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="21883-156">È possibile connettersi tooa Pi cablata tooa di rete wireless o di rete.</span><span class="sxs-lookup"><span data-stu-id="21883-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="21883-157">Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="21883-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="21883-158">Ad esempio, è possibile connettersi toohello Pi che stesso commutatore che il computer è connesso.</span><span class="sxs-lookup"><span data-stu-id="21883-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="21883-159">La connessione di rete cablata tooa</span><span class="sxs-lookup"><span data-stu-id="21883-159">Connect tooa wired network</span></span>
<span data-ttu-id="21883-160">Utilizzare hello Ethernet via cavo tooconnect tooyour Pi rete cablata.</span><span class="sxs-lookup"><span data-stu-id="21883-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="21883-161">Hello due LED Pi accendere se hello connessione viene stabilita.</span><span class="sxs-lookup"><span data-stu-id="21883-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Connettersi tramite cavo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="21883-163">Connessione rete wireless tooa</span><span class="sxs-lookup"><span data-stu-id="21883-163">Connect tooa wireless network</span></span>
<span data-ttu-id="21883-164">Seguire hello [istruzioni](https://www.raspberrypi.org/learning/software-guide/wifi/) dalla rete wireless di hello Raspberry Pi Foundation tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="21883-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="21883-165">Queste istruzioni richiedono toofirst connettere un monitoraggio e tooPi una tastiera.</span><span class="sxs-lookup"><span data-stu-id="21883-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="21883-166">Connettersi tooPi hello LED</span><span class="sxs-lookup"><span data-stu-id="21883-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="21883-167">toocomplete questa attività, utilizzare hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello cavi connettore, hello LED e hello resistenza.</span><span class="sxs-lookup"><span data-stu-id="21883-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="21883-168">Connetterle toohello [input/output generico](https://www.raspberrypi.org/documentation/usage/gpio/) porte (GPIO) di pi greco.</span><span class="sxs-lookup"><span data-stu-id="21883-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Basetta sperimentale, LED e resistore](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="21883-170">Connettersi segmento più breve di hello del LED hello troppo**GPIO GND (6 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="21883-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="21883-171">Connettersi segmento più lungo di hello del segmento tooone LED di resistenza hello hello.</span><span class="sxs-lookup"><span data-stu-id="21883-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="21883-172">Connettersi hello altro segmento di resistenza hello troppo**GPIO 4 (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="21883-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="21883-173">Si noti che è importante polarità hello LED.</span><span class="sxs-lookup"><span data-stu-id="21883-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="21883-174">generalmente impostata come attiva bassa.</span><span class="sxs-lookup"><span data-stu-id="21883-174">This polarity setting is commonly known as Active Low.</span></span>

![Piedinatura](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="21883-176">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="21883-176">Congratulations!</span></span> <span data-ttu-id="21883-177">Il dispositivo Raspberry Pi è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="21883-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="21883-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="21883-178">Summary</span></span>
<span data-ttu-id="21883-179">In questo articolo, si è appreso come tooconfigure pi greco, installando Raspbian, connessione rete tooa di pi greco, e la connessione a un tooPi LED.</span><span class="sxs-lookup"><span data-stu-id="21883-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="21883-180">Si noti che hello che LED non ancora accendersi.</span><span class="sxs-lookup"><span data-stu-id="21883-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="21883-181">attività successiva Hello è tooinstall hello strumenti e necessari software in preparazione per l'esecuzione di un'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="21883-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![L'hardware è pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="21883-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21883-183">Next steps</span></span>
[<span data-ttu-id="21883-184">Ottenere strumenti hello</span><span class="sxs-lookup"><span data-stu-id="21883-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

