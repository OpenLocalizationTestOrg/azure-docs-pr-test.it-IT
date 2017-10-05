---
title: Sostituire un controller EBOD StorSimple | Microsoft Docs
description: Viene illustrato come rimuovere e sostituire uno o entrambi i controller EBOD in un dispositivo StorSimple 8600.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="686fb-103">Sostituzione di un controller EBOD nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="686fb-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="686fb-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="686fb-104">Overview</span></span>
<span data-ttu-id="686fb-105">In questa esercitazione viene illustrato come sostituire un modulo controller EBOD guasto nel dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="686fb-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="686fb-106">Per sostituire un modulo controller EBOD, è necessario:</span><span class="sxs-lookup"><span data-stu-id="686fb-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="686fb-107">Rimuovere il controller EBOD guasto</span><span class="sxs-lookup"><span data-stu-id="686fb-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="686fb-108">Installare un nuovo controller EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-108">Install a new EBOD controller</span></span>

<span data-ttu-id="686fb-109">Prima di iniziare, tenere in considerazione le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="686fb-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="686fb-110">In tutti gli slot inutilizzati, è necessario inserire moduli EBOD vuoti.</span><span class="sxs-lookup"><span data-stu-id="686fb-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="686fb-111">Lo chassis non verrà raffreddato correttamente se uno slot è aperto.</span><span class="sxs-lookup"><span data-stu-id="686fb-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="686fb-112">Il controller EBOD è dispone del supporto per lo swapping a caldo e può essere rimosso o sostituito.</span><span class="sxs-lookup"><span data-stu-id="686fb-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="686fb-113">Non rimuovere un modulo guasto finché non si dispone di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="686fb-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="686fb-114">Quando si avvia il processo di sostituzione, deve essere completato entro 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="686fb-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="686fb-115">Prima di tentare di rimuovere o sostituire qualsiasi componente di StorSimple, leggere le [convenzioni di sicurezza](storsimple-safety.md#safety-icon-conventions) e altre [precauzioni di sicurezza](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="686fb-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="686fb-116">Rimozione di un controller EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-116">Remove an EBOD controller</span></span>
<span data-ttu-id="686fb-117">Prima di sostituire il modulo controller EBOD guasto nel dispositivo StorSimple, assicurarsi che l'altro modulo controller EBOD sia attivo e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="686fb-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="686fb-118">Nella procedura e nella tabella seguenti viene illustrato come rimuovere il modulo controller EBOD.</span><span class="sxs-lookup"><span data-stu-id="686fb-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="686fb-119">Per rimuovere un modulo EBOD:</span><span class="sxs-lookup"><span data-stu-id="686fb-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="686fb-120">Aprire il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="686fb-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="686fb-121">Passare a **Dispositivi** > **Manutenzione** > **Stato hardware**, quindi verificare che lo stato del LED per il modulo controller EBOD sia verde e che il LED per il modulo controller EBOD guasto sia rosso.</span><span class="sxs-lookup"><span data-stu-id="686fb-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="686fb-122">Individuare il modulo controller EBOD guasto nella parte posteriore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="686fb-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="686fb-123">Rimuovere i cavi che collegano il modulo controller EBOD al controller prima di rimuovere il modulo EBOD dal sistema.</span><span class="sxs-lookup"><span data-stu-id="686fb-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="686fb-124">Prendere nota dell'esatta porta SAS del modulo controller EBOD collegata al controller.</span><span class="sxs-lookup"><span data-stu-id="686fb-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="686fb-125">Dopo la sostituzione del modulo EBOD, sarà necessario ripristinare il sistema a questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="686fb-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="686fb-126">In genere, questa sarà la porta A, etichettata come **Host in entrata** nel diagramma seguente.</span><span class="sxs-lookup"><span data-stu-id="686fb-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Backplane del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="686fb-128">**Figura 1** Parte posteriore del modulo EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="686fb-129">Etichetta</span><span class="sxs-lookup"><span data-stu-id="686fb-129">Label</span></span> | <span data-ttu-id="686fb-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="686fb-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="686fb-131">1</span><span class="sxs-lookup"><span data-stu-id="686fb-131">1</span></span> |<span data-ttu-id="686fb-132">LED di errore</span><span class="sxs-lookup"><span data-stu-id="686fb-132">Fault LED</span></span> |
   | <span data-ttu-id="686fb-133">2</span><span class="sxs-lookup"><span data-stu-id="686fb-133">2</span></span> |<span data-ttu-id="686fb-134">LED di alimentazione</span><span class="sxs-lookup"><span data-stu-id="686fb-134">Power LED</span></span> |
   | <span data-ttu-id="686fb-135">3</span><span class="sxs-lookup"><span data-stu-id="686fb-135">3</span></span> |<span data-ttu-id="686fb-136">Connettori SAS</span><span class="sxs-lookup"><span data-stu-id="686fb-136">SAS connectors</span></span> |
   | <span data-ttu-id="686fb-137">4</span><span class="sxs-lookup"><span data-stu-id="686fb-137">4</span></span> |<span data-ttu-id="686fb-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="686fb-138">SAS LEDs</span></span> |
   | <span data-ttu-id="686fb-139">5</span><span class="sxs-lookup"><span data-stu-id="686fb-139">5</span></span> |<span data-ttu-id="686fb-140">Porte seriali solo per l'utilizzo predefinito</span><span class="sxs-lookup"><span data-stu-id="686fb-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="686fb-141">6</span><span class="sxs-lookup"><span data-stu-id="686fb-141">6</span></span> |<span data-ttu-id="686fb-142">Porta (Host in entrata)</span><span class="sxs-lookup"><span data-stu-id="686fb-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="686fb-143">7</span><span class="sxs-lookup"><span data-stu-id="686fb-143">7</span></span> |<span data-ttu-id="686fb-144">Porta B (Host in uscita)</span><span class="sxs-lookup"><span data-stu-id="686fb-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="686fb-145">8</span><span class="sxs-lookup"><span data-stu-id="686fb-145">8</span></span> |<span data-ttu-id="686fb-146">Porta C (solo per utilizzo predefinito)</span><span class="sxs-lookup"><span data-stu-id="686fb-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="686fb-147">Installare un nuovo controller EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-147">Install a new EBOD controller</span></span>
<span data-ttu-id="686fb-148">Nella procedura e nella tabella seguenti viene illustrato come installare un modulo controller EBOD nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="686fb-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="686fb-149">Per installare un controller EBOD:</span><span class="sxs-lookup"><span data-stu-id="686fb-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="686fb-150">Verificare la presenza di danni nel dispositivo EBOD, soprattutto sul connettore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="686fb-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="686fb-151">Non installare il nuovo controller EBOD se sono presenti perni piegati.</span><span class="sxs-lookup"><span data-stu-id="686fb-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="686fb-152">Con i chiavistelli in posizione aperta, far scorrere il modulo nello chassis finché non attiva i chiavistelli.</span><span class="sxs-lookup"><span data-stu-id="686fb-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Installazione del controller EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="686fb-154">**Figura 2** Installazione del modulo controller EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="686fb-155">Chiudere il chiavistello.</span><span class="sxs-lookup"><span data-stu-id="686fb-155">Close the latch.</span></span> <span data-ttu-id="686fb-156">Quando il chiavistello viene attivato si dovrebbe ascoltare un clic.</span><span class="sxs-lookup"><span data-stu-id="686fb-156">You should hear a click as the latch engages.</span></span>
   
    ![Rilascio del latch EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="686fb-158">**Figura 3** Chiusura del chiavistello del modulo EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="686fb-159">Riconnettere i cavi.</span><span class="sxs-lookup"><span data-stu-id="686fb-159">Reconnect the cables.</span></span> <span data-ttu-id="686fb-160">Utilizzare la configurazione esatta presente prima della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="686fb-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="686fb-161">Vedere il diagramma e la tabella seguenti per informazioni dettagliate su come connettere i cavi.</span><span class="sxs-lookup"><span data-stu-id="686fb-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="686fb-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="686fb-163">**Figure 4**.</span></span> <span data-ttu-id="686fb-164">Ricollegamento dei cavi</span><span class="sxs-lookup"><span data-stu-id="686fb-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="686fb-165">Etichetta</span><span class="sxs-lookup"><span data-stu-id="686fb-165">Label</span></span> | <span data-ttu-id="686fb-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="686fb-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="686fb-167">1</span><span class="sxs-lookup"><span data-stu-id="686fb-167">1</span></span> |<span data-ttu-id="686fb-168">Enclosure principale</span><span class="sxs-lookup"><span data-stu-id="686fb-168">Primary enclosure</span></span> |
   | <span data-ttu-id="686fb-169">2</span><span class="sxs-lookup"><span data-stu-id="686fb-169">2</span></span> |<span data-ttu-id="686fb-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="686fb-170">PCM 0</span></span> |
   | <span data-ttu-id="686fb-171">3</span><span class="sxs-lookup"><span data-stu-id="686fb-171">3</span></span> |<span data-ttu-id="686fb-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="686fb-172">PCM 1</span></span> |
   | <span data-ttu-id="686fb-173">4</span><span class="sxs-lookup"><span data-stu-id="686fb-173">4</span></span> |<span data-ttu-id="686fb-174">Controller 0</span><span class="sxs-lookup"><span data-stu-id="686fb-174">Controller 0</span></span> |
   | <span data-ttu-id="686fb-175">5</span><span class="sxs-lookup"><span data-stu-id="686fb-175">5</span></span> |<span data-ttu-id="686fb-176">Controller 1</span><span class="sxs-lookup"><span data-stu-id="686fb-176">Controller 1</span></span> |
   | <span data-ttu-id="686fb-177">6</span><span class="sxs-lookup"><span data-stu-id="686fb-177">6</span></span> |<span data-ttu-id="686fb-178">Controller 0 EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="686fb-179">7</span><span class="sxs-lookup"><span data-stu-id="686fb-179">7</span></span> |<span data-ttu-id="686fb-180">Controller 1 EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="686fb-181">8</span><span class="sxs-lookup"><span data-stu-id="686fb-181">8</span></span> |<span data-ttu-id="686fb-182">Chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="686fb-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="686fb-183">9</span><span class="sxs-lookup"><span data-stu-id="686fb-183">9</span></span> |<span data-ttu-id="686fb-184">Unità PDU (Power Distribution Unit)</span><span class="sxs-lookup"><span data-stu-id="686fb-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="686fb-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="686fb-185">Next steps</span></span>
<span data-ttu-id="686fb-186">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="686fb-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

