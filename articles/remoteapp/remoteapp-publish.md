---
title: Pubblicare un'app in Azure RemoteApp | Microsoft Docs
description: Informazioni su come pubblicare app e risorse in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="85fe1-103">Come pubblicare un'app in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="85fe1-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="85fe1-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="85fe1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="85fe1-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="85fe1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="85fe1-106">Dopo aver creato la raccolta RemoteApp, è necessario pubblicare le app o le risorse che si desidera rendere disponibili agli utenti.</span><span class="sxs-lookup"><span data-stu-id="85fe1-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="85fe1-107">Nelle immagini modello fornite con la sottoscrizione sono pubblicate solo alcune app per impostazione predefinita. Per condividere le altre app, è necessario pubblicarle.</span><span class="sxs-lookup"><span data-stu-id="85fe1-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="85fe1-108">È necessario aggiornare un'app?</span><span class="sxs-lookup"><span data-stu-id="85fe1-108">Do you need to update an app?</span></span> <span data-ttu-id="85fe1-109">È prima necessario [aggiornare l'immagine](remoteapp-update.md) .</span><span class="sxs-lookup"><span data-stu-id="85fe1-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="85fe1-110">Nella scheda **Publishing** (Pubblicazione) del portale fare clic su **Publish** (Pubblica).</span><span class="sxs-lookup"><span data-stu-id="85fe1-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="85fe1-111">È possibile aggiungere un'app dal menu **Start** dell'immagine modello oppure specificare il percorso in cui è installata l'app nell'immagine modello.</span><span class="sxs-lookup"><span data-stu-id="85fe1-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="85fe1-112">Se si decide di aggiungere l'app dal menu **Start** , scegliere l'app da pubblicare dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="85fe1-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="85fe1-113">Se si decide di fornire il percorso dell'app, specificare il nome e il percorso dell'app.</span><span class="sxs-lookup"><span data-stu-id="85fe1-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="85fe1-114">Usare le variabili nel percorso, ad esempio "%systemdrive%" anziché "c:\".</span><span class="sxs-lookup"><span data-stu-id="85fe1-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="85fe1-115">Per aggiungere l'app dal menu **Start**, è necessario aver *aggiunto l'app al menu **Start** nell'immagine modello*.</span><span class="sxs-lookup"><span data-stu-id="85fe1-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="85fe1-116">In caso contrario, RemoteApp visualizzerà solo gli elementi *presenti* nel menu **Start**, creando confusione.</span><span class="sxs-lookup"><span data-stu-id="85fe1-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="85fe1-117">Per assicurarsi che l'applicazione venga visualizzata nel menu **Start**, inserire un file di collegamento **.Ink** nella cartella %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programmi.</span><span class="sxs-lookup"><span data-stu-id="85fe1-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="85fe1-118">Se si dimentica di aggiungere l'app al menu **Start** al momento della creazione del modello, aggiungere il percorso all'app</span><span class="sxs-lookup"><span data-stu-id="85fe1-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="85fe1-119">(in alternativa, ricreare l'immagine modello, tuttavia questa procedura è piuttosto complicata).</span><span class="sxs-lookup"><span data-stu-id="85fe1-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

