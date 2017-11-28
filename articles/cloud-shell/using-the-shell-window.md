---
title: Uso della finestra Azure Cloud Shell (anteprima) | Microsoft Docs
description: Informazioni sulla finestra Azure Cloud Shell.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: a47961dfdaf178a6b793bd68105d9792a9275bb3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-azure-cloud-shell-window"></a><span data-ttu-id="88209-103">Uso della finestra Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="88209-103">Using the Azure Cloud Shell window</span></span>

<span data-ttu-id="88209-104">Questo documento illustra come usare la finestra Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="88209-104">This document explains how to use the Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="88209-105">Sessioni simultanee</span><span class="sxs-lookup"><span data-stu-id="88209-105">Concurrent sessions</span></span>
<span data-ttu-id="88209-106">Cloud Shell abilita l'apertura di più sessioni simultanee nelle schede del browser, consentendo a ogni sessione di essere disponibile come processo Bash separato.</span><span class="sxs-lookup"><span data-stu-id="88209-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.</span></span>
<span data-ttu-id="88209-107">Alla chiusura di una sessione, assicurarsi di chiudere ogni finestra della sessione poiché ogni processo viene eseguito in modo indipendente anche se nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="88209-107">If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="88209-108">Riavviare Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="88209-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="88209-109">Il riavvio della Cloud Shell reimposta lo stato della macchina e qualsiasi file non persistente nella condivisione file andrà perso.</span><span class="sxs-lookup"><span data-stu-id="88209-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="88209-110">Fare clic sull'icona di riavvio sulla barra degli strumenti per ricevere un nuovo ambiente Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="88209-110">Click the restart icon on the toolbar to receive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="88209-111">Ridurre e ingrandire la finestra Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="88209-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="88209-112">Fare clic sull'icona di riduzione nella parte superiore destra della finestra per nasconderla.</span><span class="sxs-lookup"><span data-stu-id="88209-112">Click the minimize icon on the top right of the window to hide it.</span></span> <span data-ttu-id="88209-113">Fare clic di nuovo sull'icona Cloud Shell per riportare in primo piano la finestra.</span><span class="sxs-lookup"><span data-stu-id="88209-113">Click the Cloud Shell icon again to unhide.</span></span>
* <span data-ttu-id="88209-114">Fare clic sull'icona di ingrandimento per aprire la finestra alla grandezza massima.</span><span class="sxs-lookup"><span data-stu-id="88209-114">Click the maximize icon to set window to max height.</span></span> <span data-ttu-id="88209-115">Per ripristinare la dimensioni precedenti, fare clic su Ripristina.</span><span class="sxs-lookup"><span data-stu-id="88209-115">To restore window to previous size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="88209-116">Copiare e incollare</span><span class="sxs-lookup"><span data-stu-id="88209-116">Copy and paste</span></span>
* <span data-ttu-id="88209-117">Windows: `Ctrl-insert` per copiare e `Shift-insert` per incollare.</span><span class="sxs-lookup"><span data-stu-id="88209-117">Windows: `Ctrl-insert` to copy and `Shift-insert` to paste.</span></span> <span data-ttu-id="88209-118">Facendo clic con pulsante destro del mouse sull'elenco a discesa è possibile abilitare Copia e Incolla.</span><span class="sxs-lookup"><span data-stu-id="88209-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="88209-119">FireFox o Internet Explorer potrebbero non supportare correttamente le autorizzazioni per gli appunti.</span><span class="sxs-lookup"><span data-stu-id="88209-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="88209-120">Mac OS: `Cmd-c` per copiare e `Cmd-v` per incollare.</span><span class="sxs-lookup"><span data-stu-id="88209-120">Mac OS: `Cmd-c` to copy and `Cmd-v` to paste.</span></span> <span data-ttu-id="88209-121">Facendo clic con pulsante destro del mouse sull'elenco a discesa è possibile abilitare Copia e Incolla.</span><span class="sxs-lookup"><span data-stu-id="88209-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="88209-122">Ridimensionare la finestra Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="88209-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="88209-123">Fare clic e trascinare il bordo superiore della barra degli strumenti verso l'alto o verso il basso per ridimensionare la finestra Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="88209-123">Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="88209-124">Scorrimento del testo visualizzato</span><span class="sxs-lookup"><span data-stu-id="88209-124">Scrolling text display</span></span>
* <span data-ttu-id="88209-125">Scorrere con il mouse o il touchpad per spostare il testo del terminale.</span><span class="sxs-lookup"><span data-stu-id="88209-125">Scroll with your mouse or touchpad to move terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="88209-126">Comando Exit</span><span class="sxs-lookup"><span data-stu-id="88209-126">Exit command</span></span>
<span data-ttu-id="88209-127">L'esecuzione di `exit` termina la sessione attiva.</span><span class="sxs-lookup"><span data-stu-id="88209-127">Running `exit` terminates the active session.</span></span> <span data-ttu-id="88209-128">Questo comportamento si verifica per impostazione predefinita dopo 20 minuti senza interazione.</span><span class="sxs-lookup"><span data-stu-id="88209-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88209-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88209-129">Next steps</span></span>
[<span data-ttu-id="88209-130">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="88209-130">Cloud Shell Quickstart</span></span>](quickstart.md)
