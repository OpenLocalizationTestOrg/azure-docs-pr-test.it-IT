---
title: 'Connect Arduino (C) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: Configurare Adafruit Feather M0 WiFi per il primo utilizzo.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino impostato, connettersi arduino toopc, il programma di installazione arduino, arduino Lavagna
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="a7e0e-104">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="a7e0e-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a7e0e-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a7e0e-105">What you will do</span></span>
<span data-ttu-id="a7e0e-106">Configurare la Lavagna Adafruit sfumatura M0 Wi-Fi Arduino per primo utilizzo assemblando Lavagna hello, l'accensione.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="a7e0e-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a7e0e-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7e0e-108">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="a7e0e-108">What you need</span></span>
<span data-ttu-id="a7e0e-109">toocomplete questa operazione, è necessario hello seguenti parti per lo Starter Kit Adafruit sfumatura M0 Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="a7e0e-110">Hello Adafruit sfumatura M0 WiFi Lavagna</span><span class="sxs-lookup"><span data-stu-id="a7e0e-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="a7e0e-111">Un cavo USB A di tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="a7e0e-111">A Micro B tooType A USB cable</span></span>

![kit][kit]

<span data-ttu-id="a7e0e-113">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-113">You also need:</span></span>

* <span data-ttu-id="a7e0e-114">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="a7e0e-115">Una connessione wireless per i tooconnect Lavagna Arduino per.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="a7e0e-116">Strumento di configurazione toodownload connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7e0e-117">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a7e0e-117">What you will learn</span></span>
<span data-ttu-id="a7e0e-118">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-118">In this article, you will learn:</span></span>

* <span data-ttu-id="a7e0e-119">Come tooassemble la Lavagna Arduino e potenza, per hello seguenti lezioni.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="a7e0e-120">Come le autorizzazioni di porta seriale tooadd per Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="a7e0e-121">Connettere il computer di tooyour Arduino Lavagna</span><span class="sxs-lookup"><span data-stu-id="a7e0e-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="a7e0e-122">Collegare il cavo USB micro di hello superiore porta USB micro hello.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro-USB superiore][top-micro-usb-port]

2. <span data-ttu-id="a7e0e-124">Plug hello altra estremità del cavo USB nel computer.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-124">Plug hello other end of USB cable into your computer.</span></span>

   ![USB computer][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="a7e0e-126">Aggiungere autorizzazioni per la porta seriale in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a7e0e-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="a7e0e-127">Se si usa Windows o macOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="a7e0e-128">Per Ubuntu, è necessario hello seguendo i passaggi toomake hello linux normale utente che disponga hello autorizzazioni toooperate sulla porta USB hello la Lavagna Arduino.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="a7e0e-129">Come utente normale dal terminale:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="a7e0e-130">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="a7e0e-131">Hello "0" potrebbe essere un numero diverso oppure potrebbero essere restituite più voci.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="a7e0e-132">In dati hello case primo hello dobbiamo `uucp`, hello in secondo luogo è `dialout`, che è proprietario del gruppo di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="a7e0e-133">Aggiungi utente toohello toohello gruppo:</span><span class="sxs-lookup"><span data-stu-id="a7e0e-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="a7e0e-134">Dove `group-name` dati hello trovato nel primo passaggio hello e `username` è il nome utente di linux.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="a7e0e-135">È necessario toolog e nuovamente per questo effetto tootake modifica e l'installazione completa di hello.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="a7e0e-136">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a7e0e-136">Summary</span></span>
<span data-ttu-id="a7e0e-137">In questo articolo, si è appreso come tooconfigure la Lavagna Arduino.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="a7e0e-138">attività successiva Hello è software in preparazione per l'esecuzione di un'applicazione di esempio sulla Lavagna Arduino e gli strumenti necessari di tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="a7e0e-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![L'hardware è pronto][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="a7e0e-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7e0e-140">Next steps</span></span>
<span data-ttu-id="a7e0e-141">[Ottenere strumenti hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="a7e0e-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md