---
title: un controller di EBOD 8600 StorSimple aaaReplace | Documenti Microsoft
description: Viene illustrato come tooremove e sostituire uno o entrambi i controller EBOD in un dispositivo 8600 StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="f28aa-103">Sostituzione di un controller EBOD nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="f28aa-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="f28aa-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f28aa-104">Overview</span></span>
<span data-ttu-id="f28aa-105">In questa esercitazione viene illustrato come tooreplace un modulo controller EBOD guasto nel dispositivo StorSimple di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f28aa-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="f28aa-106">un modulo controller EBOD tooreplace, è necessario:</span><span class="sxs-lookup"><span data-stu-id="f28aa-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="f28aa-107">Rimuovere i controller EBOD guasto hello</span><span class="sxs-lookup"><span data-stu-id="f28aa-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="f28aa-108">Installare un nuovo controller EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-108">Install a new EBOD controller</span></span>

<span data-ttu-id="f28aa-109">Prendere in considerazione hello prima di iniziare le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="f28aa-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="f28aa-110">In tutti gli slot inutilizzati, è necessario inserire moduli EBOD vuoti.</span><span class="sxs-lookup"><span data-stu-id="f28aa-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="f28aa-111">Hello enclosure non viene raffreddata correttamente se un alloggiamento viene lasciato aperto.</span><span class="sxs-lookup"><span data-stu-id="f28aa-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="f28aa-112">controller EBOD Hello è collegabile a caldo e può essere rimosso o sostituito.</span><span class="sxs-lookup"><span data-stu-id="f28aa-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="f28aa-113">Non rimuovere un modulo guasto finché non si dispone di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="f28aa-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="f28aa-114">Quando si avvia il processo di sostituzione hello, deve essere completato entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f28aa-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f28aa-115">Prima di tentare di tooremove o sostituire qualsiasi componente di StorSimple, verificare che hello [convenzioni delle icone di sicurezza](storsimple-safety.md#safety-icon-conventions) e altri [precauzioni di sicurezza](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="f28aa-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="f28aa-116">Rimozione di un controller EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-116">Remove an EBOD controller</span></span>
<span data-ttu-id="f28aa-117">Prima di sostituire hello Impossibile modulo controller EBOD nel dispositivo StorSimple, assicurarsi che hello altro modulo controller EBOD sia attivo e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f28aa-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="f28aa-118">Hello procedura e la tabella seguente viene illustrato come tooremove hello modulo controller EBOD.</span><span class="sxs-lookup"><span data-stu-id="f28aa-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="f28aa-119">tooremove un modulo EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="f28aa-120">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f28aa-120">Open hello Azure portal.</span></span>
2. <span data-ttu-id="f28aa-121">Passare tooyour dispositivo e passare troppo**impostazioni** > **lo stato di Hardware**e verificare lo stato hello di hello LED per il modulo controller EBOD attivo di hello è verde e hello LED per hello non riuscita Modulo controller EBOD sia di colore rosso.</span><span class="sxs-lookup"><span data-stu-id="f28aa-121">Go tooyour device and navigate too**Settings** > **Hardware health**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="f28aa-122">Posizionate hello parte posteriore dispositivo hello modulo controller EBOD di hello non riuscita.</span><span class="sxs-lookup"><span data-stu-id="f28aa-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="f28aa-123">Rimuovere i cavi di hello che collegano i controller di toohello modulo controller EBOD hello prima di rimuovere il modulo EBOD hello dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="f28aa-124">Prendere nota di hello porta SAS del modulo controller EBOD hello che era connesso toohello controller.</span><span class="sxs-lookup"><span data-stu-id="f28aa-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="f28aa-125">Dopo aver sostituito modulo EBOD hello sarà configurazione toothis del sistema hello toorestore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f28aa-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f28aa-126">In genere, questa sarà la porta A, contrassegnato come **ospitare in** nel seguente diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   
    ![Backplane del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="f28aa-128">**Figura 1** Parte posteriore del modulo EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="f28aa-129">Etichetta</span><span class="sxs-lookup"><span data-stu-id="f28aa-129">Label</span></span> | <span data-ttu-id="f28aa-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f28aa-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f28aa-131">1</span><span class="sxs-lookup"><span data-stu-id="f28aa-131">1</span></span> |<span data-ttu-id="f28aa-132">LED di errore</span><span class="sxs-lookup"><span data-stu-id="f28aa-132">Fault LED</span></span> |
   | <span data-ttu-id="f28aa-133">2</span><span class="sxs-lookup"><span data-stu-id="f28aa-133">2</span></span> |<span data-ttu-id="f28aa-134">LED di alimentazione</span><span class="sxs-lookup"><span data-stu-id="f28aa-134">Power LED</span></span> |
   | <span data-ttu-id="f28aa-135">3</span><span class="sxs-lookup"><span data-stu-id="f28aa-135">3</span></span> |<span data-ttu-id="f28aa-136">Connettori SAS</span><span class="sxs-lookup"><span data-stu-id="f28aa-136">SAS connectors</span></span> |
   | <span data-ttu-id="f28aa-137">4</span><span class="sxs-lookup"><span data-stu-id="f28aa-137">4</span></span> |<span data-ttu-id="f28aa-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="f28aa-138">SAS LEDs</span></span> |
   | <span data-ttu-id="f28aa-139">5</span><span class="sxs-lookup"><span data-stu-id="f28aa-139">5</span></span> |<span data-ttu-id="f28aa-140">Porte seriali solo per l'utilizzo predefinito</span><span class="sxs-lookup"><span data-stu-id="f28aa-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="f28aa-141">6</span><span class="sxs-lookup"><span data-stu-id="f28aa-141">6</span></span> |<span data-ttu-id="f28aa-142">Porta (Host in entrata)</span><span class="sxs-lookup"><span data-stu-id="f28aa-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="f28aa-143">7</span><span class="sxs-lookup"><span data-stu-id="f28aa-143">7</span></span> |<span data-ttu-id="f28aa-144">Porta B (Host in uscita)</span><span class="sxs-lookup"><span data-stu-id="f28aa-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="f28aa-145">8</span><span class="sxs-lookup"><span data-stu-id="f28aa-145">8</span></span> |<span data-ttu-id="f28aa-146">Porta C (solo per utilizzo predefinito)</span><span class="sxs-lookup"><span data-stu-id="f28aa-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="f28aa-147">Installare un nuovo controller EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-147">Install a new EBOD controller</span></span>
<span data-ttu-id="f28aa-148">Hello procedura e la tabella seguente viene illustrato come tooinstall un modulo controller EBOD del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f28aa-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="f28aa-149">tooinstall un controller EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="f28aa-150">Controllare hello EBOD dispositivo siano presenti danneggiamenti, in particolare toohello connettore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="f28aa-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="f28aa-151">Se qualsiasi pin piegati, non installare il nuovo controller di EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="f28aa-152">Aprire posizione, il modulo hello diapositiva in enclosure hello fino a quando non hello scattare latch hello in hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Installazione del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="f28aa-154">**Figura 2** modulo controller EBOD hello di installazione</span><span class="sxs-lookup"><span data-stu-id="f28aa-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="f28aa-155">Latch hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="f28aa-155">Close hello latch.</span></span> <span data-ttu-id="f28aa-156">Quando si attiva il latch hello, si sente un clic.</span><span class="sxs-lookup"><span data-stu-id="f28aa-156">You should hear a click as hello latch engages.</span></span>
   
    ![Rilascio del latch EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="f28aa-158">**Figura 3** chiusura del latch del modulo EBOD hello</span><span class="sxs-lookup"><span data-stu-id="f28aa-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="f28aa-159">Ricollegare i cavi di hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-159">Reconnect hello cables.</span></span> <span data-ttu-id="f28aa-160">Utilizzare configurazione esatta hello che era presente prima della sostituzione hello.</span><span class="sxs-lookup"><span data-stu-id="f28aa-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="f28aa-161">Vedere hello seguente diagramma e tabella per informazioni dettagliate su come cavi hello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f28aa-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="f28aa-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="f28aa-163">**Figure 4**.</span></span> <span data-ttu-id="f28aa-164">Ricollegamento dei cavi</span><span class="sxs-lookup"><span data-stu-id="f28aa-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="f28aa-165">Etichetta</span><span class="sxs-lookup"><span data-stu-id="f28aa-165">Label</span></span> | <span data-ttu-id="f28aa-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f28aa-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f28aa-167">1</span><span class="sxs-lookup"><span data-stu-id="f28aa-167">1</span></span> |<span data-ttu-id="f28aa-168">Enclosure principale</span><span class="sxs-lookup"><span data-stu-id="f28aa-168">Primary enclosure</span></span> |
   | <span data-ttu-id="f28aa-169">2</span><span class="sxs-lookup"><span data-stu-id="f28aa-169">2</span></span> |<span data-ttu-id="f28aa-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="f28aa-170">PCM 0</span></span> |
   | <span data-ttu-id="f28aa-171">3</span><span class="sxs-lookup"><span data-stu-id="f28aa-171">3</span></span> |<span data-ttu-id="f28aa-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="f28aa-172">PCM 1</span></span> |
   | <span data-ttu-id="f28aa-173">4</span><span class="sxs-lookup"><span data-stu-id="f28aa-173">4</span></span> |<span data-ttu-id="f28aa-174">Controller 0</span><span class="sxs-lookup"><span data-stu-id="f28aa-174">Controller 0</span></span> |
   | <span data-ttu-id="f28aa-175">5</span><span class="sxs-lookup"><span data-stu-id="f28aa-175">5</span></span> |<span data-ttu-id="f28aa-176">Controller 1</span><span class="sxs-lookup"><span data-stu-id="f28aa-176">Controller 1</span></span> |
   | <span data-ttu-id="f28aa-177">6</span><span class="sxs-lookup"><span data-stu-id="f28aa-177">6</span></span> |<span data-ttu-id="f28aa-178">Controller 0 EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="f28aa-179">7</span><span class="sxs-lookup"><span data-stu-id="f28aa-179">7</span></span> |<span data-ttu-id="f28aa-180">Controller 1 EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="f28aa-181">8</span><span class="sxs-lookup"><span data-stu-id="f28aa-181">8</span></span> |<span data-ttu-id="f28aa-182">Chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="f28aa-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="f28aa-183">9</span><span class="sxs-lookup"><span data-stu-id="f28aa-183">9</span></span> |<span data-ttu-id="f28aa-184">Unità PDU (Power Distribution Unit)</span><span class="sxs-lookup"><span data-stu-id="f28aa-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f28aa-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f28aa-185">Next steps</span></span>
<span data-ttu-id="f28aa-186">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f28aa-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

