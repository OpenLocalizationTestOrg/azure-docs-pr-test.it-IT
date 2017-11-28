---
title: un'app in Azure RemoteApp aaaPublish | Documenti Microsoft
description: Informazioni su come toopublish applicazioni e risorse in Azure RemoteApp.
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
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="1325e-103">Come toopublish un'app in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1325e-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1325e-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="1325e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1325e-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1325e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1325e-106">Dopo aver creato la raccolta RemoteApp, è necessario toopublish hello applicazioni o risorse che si desidera toomake disponibili per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="1325e-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="1325e-107">Hello immagini modello fornite con la sottoscrizione solo con pochi App pubblicato per impostazione predefinita - tooshare hello altre App, è necessario toopublish li.</span><span class="sxs-lookup"><span data-stu-id="1325e-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="1325e-108">È necessario tooupdate un'app?</span><span class="sxs-lookup"><span data-stu-id="1325e-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="1325e-109">È necessario troppo[aggiornamento hello immagine](remoteapp-update.md) prima.</span><span class="sxs-lookup"><span data-stu-id="1325e-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="1325e-110">In hello **pubblicazione** , fare clic nel portale di hello **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="1325e-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="1325e-111">È possibile aggiungere un'app dall'immagine modello **avviare** menu o fornire hello percorso toowhere hello app viene installata in immagine modello hello.</span><span class="sxs-lookup"><span data-stu-id="1325e-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="1325e-112">Se si sceglie tooadd da hello **avviare** menu, scegliere hello app toopublish dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="1325e-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="1325e-113">Se si sceglie tooprovide hello percorso toohello app, immettere un nome per l'applicazione hello e hello percorso toohello app.</span><span class="sxs-lookup"><span data-stu-id="1325e-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="1325e-114">Utilizzare le variabili di percorso hello - ad esempio, "% systemdrive %" invece di "c:\".</span><span class="sxs-lookup"><span data-stu-id="1325e-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="1325e-115">Se si vuole che l'app da hello tooadd **avviare** menu, è necessario toohave *aggiunto tale toohello app **avviare** menu l'immagine modello.*</span><span class="sxs-lookup"><span data-stu-id="1325e-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="1325e-116">In caso contrario, RemoteApp verranno visualizzati solo ciò che *è* su hello **avviare** menu e si verrà confondere.</span><span class="sxs-lookup"><span data-stu-id="1325e-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="1325e-117">toomake che l'app è in hello **avviare** menu, inserire un file di collegamento - **lnk** : hello %systemdrive%\ProgramData\Microsoft\Windows\Start Avvio\Programmi cartella.</span><span class="sxs-lookup"><span data-stu-id="1325e-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="1325e-118">Se si è dimenticato tooadd hello app toohello **avviare** menu quando è stato creato il modello di hello, scegliere tooadd hello percorso toohello app.</span><span class="sxs-lookup"><span data-stu-id="1325e-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="1325e-119">(in alternativa, ricreare l'immagine modello, tuttavia questa procedura è piuttosto complicata).</span><span class="sxs-lookup"><span data-stu-id="1325e-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

