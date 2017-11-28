---
title: raccolte di cloud di RemoteApp aaaTroubleshoot - creazione | Documenti Microsoft
description: Informazioni su come tootroubleshoot RemoteApp cloud errori nella creazione di raccolta
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="8440c-103">Risoluzione dei problemi di creazione di raccolte di cloud di RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8440c-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8440c-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="8440c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8440c-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="8440c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8440c-106">Se si riscontrano problemi durante la creazione di una raccolta nel cloud, controllare hello le seguenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="8440c-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="8440c-107">L'immagine non è valida</span><span class="sxs-lookup"><span data-stu-id="8440c-107">Your image is invalid</span></span>
<span data-ttu-id="8440c-108">Se viene visualizzato un messaggio ad esempio, "GoldImageInvalid" quando si resta in attesa per Azure tooprovision la raccolta, significa che l'immagine modello non soddisfa hello [definito requisiti immagine](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="8440c-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="8440c-109">In tal caso, passare a leggere quelli [requisiti](remoteapp-imagereqs.md), correggere l'immagine e si tenta di toocreate nuovamente la raccolta.</span><span class="sxs-lookup"><span data-stu-id="8440c-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="8440c-110">Errori comuni visualizzati nel portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="8440c-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="8440c-111">La creazione di raccolte cloud spesso non riesce perché si usano immagini personalizzate.</span><span class="sxs-lookup"><span data-stu-id="8440c-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="8440c-112">Se si verifica uno di hello sopra gli errori e si utilizza una raccolta di hello toocreate immagine personalizzata, verificare hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="8440c-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="8440c-113">Assicurarsi che immagine personalizzata hello caricato soddisfi i requisiti di immagine.</span><span class="sxs-lookup"><span data-stu-id="8440c-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="8440c-114">In genere hello problema comune è che l'immagine hello non è stato correttamente preparata con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8440c-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="8440c-115">Verificare immagine hello possibile avvio all'interno di Hyper-V o provare a creare una VM IAAS direttamente nella sottoscrizione di Azure utilizzando l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="8440c-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="8440c-116">Se hello macchina virtuale non riesce tooboot e non avviare, quindi questo indica in genere che tale immagine personalizzata hello non è stato preparato correttamente.</span><span class="sxs-lookup"><span data-stu-id="8440c-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="8440c-117">Verificare l'immagine personalizzata hello è stato compilato in seguito hello come toocreate immagine di un modello personalizzato per RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8440c-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="8440c-118">Se si utilizza una delle immagini di Microsoft hello incluse con la sottoscrizione, provare di nuovo insieme di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8440c-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="8440c-119">Se hello problema persiste, contattare il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8440c-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="8440c-120">Se questo errore viene visualizzato in genere significa che è stato aggiornato tooa pagato account ma che si sta tentando di toouse un'immagine forniti da Microsoft che è valida solo durante la modalità di valutazione del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="8440c-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="8440c-121">In questo caso, provare a ripetere la raccolta cloud toocreate, ma essere toospecify che l'immagine corretta hello.</span><span class="sxs-lookup"><span data-stu-id="8440c-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

