---
title: Risolvere i problemi delle raccolte cloud di RemoteApp - Creazione | Documentazione Microsoft
description: Informazioni su come risolvere i problemi relativi agli errori di creazione delle raccolte cloud di RemoteApp
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
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="3a035-103">Risoluzione dei problemi di creazione di raccolte di cloud di RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3a035-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a035-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="3a035-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3a035-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="3a035-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3a035-106">Se si riscontrano problemi durante la creazione di una raccolta di cloud, consultare le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="3a035-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="3a035-107">L'immagine non è valida</span><span class="sxs-lookup"><span data-stu-id="3a035-107">Your image is invalid</span></span>
<span data-ttu-id="3a035-108">Se viene visualizzato un messaggio del tipo "GoldImageInvalid" quando si è in attesa di Azure per eseguire il provisioning per la raccolta, significa che l'immagine del modello non soddisfa i [requisiti definiti per l’immagine](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="3a035-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="3a035-109">Quindi, leggere quei [requisiti](remoteapp-imagereqs.md), correggere l'immagine e cercare di creare nuovamente la raccolta.</span><span class="sxs-lookup"><span data-stu-id="3a035-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="3a035-110">Errori più frequenti visualizzati nel portale di gestione di Azure:</span><span class="sxs-lookup"><span data-stu-id="3a035-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="3a035-111">La creazione di raccolte cloud spesso non riesce perché si usano immagini personalizzate.</span><span class="sxs-lookup"><span data-stu-id="3a035-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="3a035-112">Se si verifica uno degli errori precedenti e si usa un'immagine personalizzata per creare la raccolta, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3a035-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="3a035-113">Assicurarsi che l'immagine personalizzata che è stata caricata soddisfi i requisiti relativi all'immagine.</span><span class="sxs-lookup"><span data-stu-id="3a035-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="3a035-114">Molto spesso il problema risiede nel fatto che l'immagine non è stata preparata correttamente con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3a035-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="3a035-115">Verificare l'immagine di avvio all'interno di Hyper-V o provare a creare una VM IAAS direttamente nella sottoscrizione di Azure usando l'immagine.</span><span class="sxs-lookup"><span data-stu-id="3a035-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="3a035-116">Gli errori nell'avvio della macchina virtuale indicano, in genere, che l'immagine personalizzata non è stata preparata correttamente ed è necessario correggerla.</span><span class="sxs-lookup"><span data-stu-id="3a035-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="3a035-117">Verificare che l'immagine personalizzata sia stata creata seguendo la procedura per la creazione di un'immagine modello personalizzata per RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3a035-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="3a035-118">Se si usa una delle immagini Microsoft incluse nella sottoscrizione, provare a creare nuovamente la raccolta.</span><span class="sxs-lookup"><span data-stu-id="3a035-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="3a035-119">Se il problema persiste, contattare il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a035-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="3a035-120">Se viene visualizzato questo errore in genere significa che è stato effettuato l'aggiornamento a un account a pagamento, ma si sta tentando di usare un'immagine fornita da Microsoft che è valida solo durante la modalità di valutazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="3a035-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="3a035-121">In questo caso, provare a creare nuovamente la raccolta cloud, ma assicurarsi di specificare l'immagine corretta.</span><span class="sxs-lookup"><span data-stu-id="3a035-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

