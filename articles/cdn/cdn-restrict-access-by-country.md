---
title: contenuto della rete CDN di Azure in base al paese aaaRestrict | Documenti Microsoft
description: "Informazioni su come toorestrict accesso tooyour rete CDN di Azure contenuto mediante hello funzionalità filtro geografica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="9d8c0-103">Limitare il contenuto della rete CDN di Azure in base al paese</span><span class="sxs-lookup"><span data-stu-id="9d8c0-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="9d8c0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9d8c0-104">Overview</span></span>
<span data-ttu-id="9d8c0-105">Quando un utente richiede il contenuto, per impostazione predefinita, il contenuto di hello viene servito indipendentemente dalla effettuati di questa richiesta dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="9d8c0-106">In alcuni casi, si consiglia di tooyour toorestrict accedere al contenuto in base al paese.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="9d8c0-107">Questo argomento viene illustrato come hello toouse **filtro geografica** funzionalità in ordine tooconfigure hello servizio tooallow o blocchi l'accesso in base al paese.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d8c0-108">Hello Verizon e Akamai offrono hello stessa funzionalità di filtro geografica ma presentare piccole differenze nei codici paese te supportano.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="9d8c0-109">Per le differenze toohello un collegamento, vedere il passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="9d8c0-110">Per informazioni sulle considerazioni relative tooconfiguring questo tipo di restrizione, vedere hello [considerazioni](cdn-restrict-access-by-country.md#considerations) sezione alla fine di hello di hello argomento.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![filtro di paese](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="9d8c0-112">Passaggio 1: Definire il percorso di directory hello</span><span class="sxs-lookup"><span data-stu-id="9d8c0-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="9d8c0-113">Selezionare l'endpoint nel portale di hello e hello filtro geografica scheda toofind di navigazione a sinistra di hello questa funzionalità è disponibile.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="9d8c0-114">Quando si configura un filtro di paese, è necessario specificare utenti toowhich toohello hello percorso relativo verranno consentiti o negati l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="9d8c0-115">È possibile applicare il filtro geografico a tutti i file con "/" o alle cartelle selezionate specificando i percorsi di directory "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="9d8c0-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="9d8c0-116">È inoltre possibile applicare a file singolo filtro geografica tooa specificando file hello ed escludendo hello barra finale "/ Pictures/City.png".</span><span class="sxs-lookup"><span data-stu-id="9d8c0-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="9d8c0-117">Esempio di filtro di percorso di directory:</span><span class="sxs-lookup"><span data-stu-id="9d8c0-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="9d8c0-118">Passaggio 2: Definire l'azione di hello: bloccare o consentire</span><span class="sxs-lookup"><span data-stu-id="9d8c0-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="9d8c0-119">**Blocco:** agli utenti di hello specificato paesi verranno negati l'accesso tooassets richiesto da tale percorso ricorsiva.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="9d8c0-120">Se non sono state definite altre opzioni di filtro di paese per tale percorso, tutti gli altri utenti saranno autorizzati ad accedere.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="9d8c0-121">**Consenti:** solo gli utenti di hello specificato paesi potrà essere richiesto da tale percorso ricorsiva tooassets di accesso.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="9d8c0-122">Passaggio 3: Definire paesi hello</span><span class="sxs-lookup"><span data-stu-id="9d8c0-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="9d8c0-123">Selezionare hello paesi che desidera tooblock o consentire per il percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="9d8c0-124">Ad esempio, la regola hello di blocco /Photos Strasburgo/filtrerà i file inclusi:</span><span class="sxs-lookup"><span data-stu-id="9d8c0-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="9d8c0-125">Codici paese</span><span class="sxs-lookup"><span data-stu-id="9d8c0-125">Country codes</span></span>
<span data-ttu-id="9d8c0-126">Hello **filtro geografica** funzionalità utilizza paese codici toodefine hello i paesi da cui consentire o bloccare una richiesta per una directory protetta.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="9d8c0-127">Si noterà hello codici paese in [codici paese della rete CDN di Azure](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d8c0-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="9d8c0-128"><a id="considerations"></a>Considerazioni</span><span class="sxs-lookup"><span data-stu-id="9d8c0-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="9d8c0-129">Potrebbe richiedere fino a too90 minuti per Verizon, o un paio di minuti con Akamai, per le modifiche tooyour paese configurazione tootake effetto filtro.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="9d8c0-130">Questa funzionalità non supporta i caratteri jolly (ad esempio, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="9d8c0-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="9d8c0-131">configurazione di filtro geografica Hello associato hello relativo percorso sarà percorso toothat applicate in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="9d8c0-132">Solo una regola può essere applicato toohello stesso percorso relativo (non è possibile creare più filtri paese toohello tale punto stesso percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="9d8c0-133">Tuttavia, una cartella potrebbe avere più filtri di paese.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="9d8c0-134">Questo è dovuto toohello ricorsiva natura dei filtri di paese.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="9d8c0-135">In altre parole, una sottocartella di una cartella configurata in precedenza può essere assegnata a un filtro di paese diverso.</span><span class="sxs-lookup"><span data-stu-id="9d8c0-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

