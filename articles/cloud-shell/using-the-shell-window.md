---
title: finestra della Shell di Cloud di Azure (anteprima) hello aaaUsing | Documenti Microsoft
description: Finestra della Shell di Cloud di Azure hello procedura dettagliata.
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
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="be645-103">Nella finestra della Shell di Cloud di Azure hello</span><span class="sxs-lookup"><span data-stu-id="be645-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="be645-104">Questo documento illustra come toouse hello finestra della Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="be645-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="be645-105">Sessioni simultanee</span><span class="sxs-lookup"><span data-stu-id="be645-105">Concurrent sessions</span></span>
<span data-ttu-id="be645-106">Shell cloud consente più sessioni simultanee in schede del browser consentendo tooexist ogni sessione come processo separato Bash.</span><span class="sxs-lookup"><span data-stu-id="be645-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="be645-107">Se è terminata una sessione, assicurarsi che tooexit da ogni finestra sessione hello stesso come ogni processo viene eseguito in modo indipendente, anche se vengono eseguite in una macchina.</span><span class="sxs-lookup"><span data-stu-id="be645-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="be645-108">Riavviare Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be645-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="be645-109">Il riavvio della Cloud Shell reimposta lo stato della macchina e qualsiasi file non persistente nella condivisione file andrà perso.</span><span class="sxs-lookup"><span data-stu-id="be645-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="be645-110">Fare clic sull'icona di riavvio hello sulla barra degli strumenti di hello tooreceive un nuovo ambiente della Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="be645-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="be645-111">Ridurre e ingrandire la finestra Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be645-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="be645-112">Fare clic su hello ridurre a icona su hello in alto a destra di toohide finestra hello è.</span><span class="sxs-lookup"><span data-stu-id="be645-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="be645-113">Fare clic sull'icona Cloud Shell hello nuovamente toounhide.</span><span class="sxs-lookup"><span data-stu-id="be645-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="be645-114">Fare clic su hello ottimizzare altezza toomax finestra tooset.</span><span class="sxs-lookup"><span data-stu-id="be645-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="be645-115">toorestore finestra tooprevious dimensioni, fare clic su Ripristina.</span><span class="sxs-lookup"><span data-stu-id="be645-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="be645-116">Copiare e incollare</span><span class="sxs-lookup"><span data-stu-id="be645-116">Copy and paste</span></span>
* <span data-ttu-id="be645-117">Windows: `Ctrl-insert` toocopy e `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="be645-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="be645-118">Facendo clic con pulsante destro del mouse sull'elenco a discesa è possibile abilitare Copia e Incolla.</span><span class="sxs-lookup"><span data-stu-id="be645-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="be645-119">FireFox o Internet Explorer potrebbero non supportare correttamente le autorizzazioni per gli appunti.</span><span class="sxs-lookup"><span data-stu-id="be645-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="be645-120">Mac OS: `Cmd-c` toocopy e `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="be645-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="be645-121">Facendo clic con pulsante destro del mouse sull'elenco a discesa è possibile abilitare Copia e Incolla.</span><span class="sxs-lookup"><span data-stu-id="be645-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="be645-122">Ridimensionare la finestra Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be645-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="be645-123">Fare clic e trascinare bordo superiore di hello della barra degli strumenti hello verso l'alto o verso il basso finestra della Shell di Cloud tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="be645-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="be645-124">Scorrimento del testo visualizzato</span><span class="sxs-lookup"><span data-stu-id="be645-124">Scrolling text display</span></span>
* <span data-ttu-id="be645-125">Scorre con il mouse o touchpad toomove terminal testo.</span><span class="sxs-lookup"><span data-stu-id="be645-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="be645-126">Comando Exit</span><span class="sxs-lookup"><span data-stu-id="be645-126">Exit command</span></span>
<span data-ttu-id="be645-127">Esecuzione `exit` termina la sessione attiva hello.</span><span class="sxs-lookup"><span data-stu-id="be645-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="be645-128">Questo comportamento si verifica per impostazione predefinita dopo 20 minuti senza interazione.</span><span class="sxs-lookup"><span data-stu-id="be645-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be645-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be645-129">Next steps</span></span>
[<span data-ttu-id="be645-130">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be645-130">Cloud Shell Quickstart</span></span>](quickstart.md)
