---
title: limitazioni di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Panoramica delle limitazioni di Azure Cloud Shell
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="cbc58-103">Limitazioni di Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cbc58-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="cbc58-104">Azure Cloud Shell offre i seguenti di hello limitazioni note:</span><span class="sxs-lookup"><span data-stu-id="cbc58-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="cbc58-105">Persistenza e stato del sistema</span><span class="sxs-lookup"><span data-stu-id="cbc58-105">System state and persistence</span></span>
<span data-ttu-id="cbc58-106">macchina Hello che fornisce la sessione della Shell di Cloud è temporaneo e viene riciclato dopo che la sessione rimane inattiva per 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="cbc58-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="cbc58-107">Shell cloud richiede un toobe condivisione di file montati.</span><span class="sxs-lookup"><span data-stu-id="cbc58-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="cbc58-108">Di conseguenza, la sottoscrizione deve essere in grado di tooset backup tooaccess risorse di archiviazione Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="cbc58-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="cbc58-109">Altre considerazioni di cui tenere conto:</span><span class="sxs-lookup"><span data-stu-id="cbc58-109">Other considerations include:</span></span>
* <span data-ttu-id="cbc58-110">Con l'archiviazione montata vengono conservate soltanto le modifiche apportate all'interno della directory `$Home` o `clouddrive`.</span><span class="sxs-lookup"><span data-stu-id="cbc58-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="cbc58-111">Le condivisioni file possono essere implementate solo dall'interno dell'[area assegnata](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="cbc58-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="cbc58-112">File di Azure supporta solo account di archiviazione con ridondanza locale e account di archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="cbc58-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="cbc58-113">Autorizzazioni utente</span><span class="sxs-lookup"><span data-stu-id="cbc58-113">User permissions</span></span>
<span data-ttu-id="cbc58-114">Le autorizzazioni sono impostate come utenti normali senza accesso SUDO.</span><span class="sxs-lookup"><span data-stu-id="cbc58-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="cbc58-115">Qualsiasi installazione esterna alla directory `$Home` non verrà conservata.</span><span class="sxs-lookup"><span data-stu-id="cbc58-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="cbc58-116">Anche se alcuni comandi all'interno di hello `clouddrive` directory, ad esempio `git clone`, non dispone delle autorizzazioni appropriate, il `$Home` directory dispone di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="cbc58-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="cbc58-117">Supporto browser</span><span class="sxs-lookup"><span data-stu-id="cbc58-117">Browser support</span></span>
<span data-ttu-id="cbc58-118">Shell cloud supporta le versioni più recenti di hello di Microsoft Internet Explorer, Microsoft Edge, Google Chrome, Mozilla Firefox e Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="cbc58-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="cbc58-119">Safari in modalità privata non è supportato.</span><span class="sxs-lookup"><span data-stu-id="cbc58-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="cbc58-120">Copiare e incollare</span><span class="sxs-lookup"><span data-stu-id="cbc58-120">Copy and paste</span></span>
<span data-ttu-id="cbc58-121">CTRL + C e Ctrl + V non funzionano come copiare e incollare collegamenti in Cloud Shell nei computer Windows, utilizzare Ctrl + ins e MAIUSC + INS toocopy e incollare rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="cbc58-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="cbc58-122">Opzioni di copia e Incolla del menu sono anche disponibili, ma pulsante destro del mouse è un accesso agli Appunti toobrowser specifiche dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="cbc58-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="cbc58-123">Modifica di .bashrc</span><span class="sxs-lookup"><span data-stu-id="cbc58-123">Editing .bashrc</span></span>
<span data-ttu-id="cbc58-124">Fare attenzione quando si modifica il file con estensione bashrc, poiché questa operazione può provocare errori imprevisti in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="cbc58-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="cbc58-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="cbc58-125">.bash_history</span></span>
<span data-ttu-id="cbc58-126">È possibile che la cronologia dei comandi bash sia incoerente a causa dell'interruzione della sessione Cloud Shell o di sessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="cbc58-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="cbc58-127">Limiti di consumo</span><span class="sxs-lookup"><span data-stu-id="cbc58-127">Usage limits</span></span>
<span data-ttu-id="cbc58-128">Cloud Shell è pensato per l'uso interattivo</span><span class="sxs-lookup"><span data-stu-id="cbc58-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="cbc58-129">e qualsiasi sessione non interattiva in esecuzione prolungata viene quindi interrotta senza preavviso.</span><span class="sxs-lookup"><span data-stu-id="cbc58-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="cbc58-130">Connettività di rete</span><span class="sxs-lookup"><span data-stu-id="cbc58-130">Network connectivity</span></span>
<span data-ttu-id="cbc58-131">Latenza nella Shell di Cloud è la connessione a internet toolocal soggetto, Cloud Shell continua toocarry tooattempt le eventuali istruzioni inviate.</span><span class="sxs-lookup"><span data-stu-id="cbc58-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbc58-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbc58-132">Next steps</span></span>
[<span data-ttu-id="cbc58-133">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cbc58-133">Cloud Shell Quickstart</span></span>](quickstart.md)
