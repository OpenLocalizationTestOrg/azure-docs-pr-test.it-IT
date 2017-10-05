---
title: 'Connettere Arduino (C) ad Azure IoT: lezione 1: Configurare il dispositivo | Documentazione Microsoft'
description: Configurare Adafruit Feather M0 WiFi per il primo utilizzo.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: configurazione di arduino, connessione di arduino al pc, impostazione di arduino, scheda arduino
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="abb7a-104">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="abb7a-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="abb7a-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="abb7a-105">What you will do</span></span>
<span data-ttu-id="abb7a-106">Configurare la scheda Arduino Adafruit Feather M0 WiFi per il primo utilizzo assemblando la scheda e fornendo l'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="abb7a-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="abb7a-107">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="abb7a-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="abb7a-108">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="abb7a-108">What you need</span></span>
<span data-ttu-id="abb7a-109">Per completare questa operazione, tenere a portata di mano i componenti seguenti inclusi nello starter kit di Adafruit Feather M0 WiFi:</span><span class="sxs-lookup"><span data-stu-id="abb7a-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="abb7a-110">Scheda Adafruit Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="abb7a-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="abb7a-111">Cavo USB Micro B/tipo A</span><span class="sxs-lookup"><span data-stu-id="abb7a-111">A Micro B to Type A USB cable</span></span>

![kit][kit]

<span data-ttu-id="abb7a-113">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="abb7a-113">You also need:</span></span>

* <span data-ttu-id="abb7a-114">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="abb7a-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="abb7a-115">Connessione wireless a cui connettere la scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="abb7a-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="abb7a-116">Connessione Internet per scaricare lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="abb7a-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="abb7a-117">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="abb7a-117">What you will learn</span></span>
<span data-ttu-id="abb7a-118">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="abb7a-118">In this article, you will learn:</span></span>

* <span data-ttu-id="abb7a-119">Come assemblare la scheda Arduino e fornire l'alimentazione per le lezioni successive.</span><span class="sxs-lookup"><span data-stu-id="abb7a-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="abb7a-120">Come aggiungere autorizzazioni per la porta seriale in Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="abb7a-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="abb7a-121">Connettere la scheda Arduino al computer</span><span class="sxs-lookup"><span data-stu-id="abb7a-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="abb7a-122">Collegare il cavo micro-USB alla porta micro-USB superiore.</span><span class="sxs-lookup"><span data-stu-id="abb7a-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro-USB superiore][top-micro-usb-port]

2. <span data-ttu-id="abb7a-124">Collegare l'altra estremità del cavo USB al computer.</span><span class="sxs-lookup"><span data-stu-id="abb7a-124">Plug the other end of USB cable into your computer.</span></span>

   ![USB computer][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="abb7a-126">Aggiungere autorizzazioni per la porta seriale in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="abb7a-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="abb7a-127">Se si usa Windows o macOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="abb7a-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="abb7a-128">Per Ubuntu, è necessario attenersi alla seguente procedura per assicurarsi che il normale utente Linux disponga delle autorizzazioni per operare sulla porta USB della scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="abb7a-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="abb7a-129">Come utente normale dal terminale:</span><span class="sxs-lookup"><span data-stu-id="abb7a-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="abb7a-130">Verrà visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="abb7a-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="abb7a-131">Il valore "0" potrebbe essere un numero diverso o potrebbero essere restituite più voci.</span><span class="sxs-lookup"><span data-stu-id="abb7a-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="abb7a-132">Nel primo caso i dati necessari sono `uucp`, nel secondo `dialout`, che è il proprietario del gruppo del file.</span><span class="sxs-lookup"><span data-stu-id="abb7a-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="abb7a-133">Aggiungere l'utente al gruppo:</span><span class="sxs-lookup"><span data-stu-id="abb7a-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="abb7a-134">Dove `group-name` indica i dati trovati nel primo passaggio e `username` è il nome utente Linux.</span><span class="sxs-lookup"><span data-stu-id="abb7a-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="abb7a-135">È necessario eseguire la disconnessione e accedere nuovamente perché questa modifica abbia effetto e per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="abb7a-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="abb7a-136">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="abb7a-136">Summary</span></span>
<span data-ttu-id="abb7a-137">In questo articolo si è appreso come configurare la scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="abb7a-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="abb7a-138">L'attività successiva consiste nell'installazione del software e degli strumenti necessari per preparare l'esecuzione di un'applicazione di esempio nella scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="abb7a-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![L'hardware è pronto][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="abb7a-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abb7a-140">Next steps</span></span>
<span data-ttu-id="abb7a-141">[Ottenere gli strumenti][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="abb7a-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md