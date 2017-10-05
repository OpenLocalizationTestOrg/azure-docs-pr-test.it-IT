---
title: Limitare il contenuto della rete CDN di Azure in base al paese | Documentazione Microsoft
description: "Informazioni su come limitare l'accesso al contenuto della rete CDN di Azure con la funzionalità Filtro geografico."
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
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="1f578-103">Limitare il contenuto della rete CDN di Azure in base al paese</span><span class="sxs-lookup"><span data-stu-id="1f578-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="1f578-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1f578-104">Overview</span></span>
<span data-ttu-id="1f578-105">Quando un utente richiede il contenuto, per impostazione predefinita il contenuto viene servito indipendentemente dalla località dell'utente che effettua la richiesta.</span><span class="sxs-lookup"><span data-stu-id="1f578-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="1f578-106">In alcuni casi, è possibile limitare l'accesso al contenuto in base al paese.</span><span class="sxs-lookup"><span data-stu-id="1f578-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="1f578-107">Questo argomento illustra come usare la funzionalità **Filtro geografico** per configurare il servizio in modo da consentire o bloccare l'accesso in base al paese.</span><span class="sxs-lookup"><span data-stu-id="1f578-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f578-108">I prodotti Verizon e Akamai forniscono la stessa funzionalità di filtro geografico, ma con una lieve differenza a livello di indicativi paese supportati.</span><span class="sxs-lookup"><span data-stu-id="1f578-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="1f578-109">Per un collegamento relativo alle differenze, vedere il Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="1f578-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="1f578-110">Per informazioni su considerazioni relative alla configurazione di questo tipo di restrizioni, vedere la sezione [Considerazioni](cdn-restrict-access-by-country.md#considerations) alla fine dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="1f578-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![filtro di paese](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="1f578-112">Passaggio 1: definire il percorso di directory</span><span class="sxs-lookup"><span data-stu-id="1f578-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="1f578-113">Per trovare questa funzionalità, selezionare l'endpoint all'interno del portale e individuare la scheda Filtro geografico nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1f578-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="1f578-114">Quando si configura un filtro di paese, è necessario specificare il percorso relativo della posizione a cui gli utenti potranno o meno accedere.</span><span class="sxs-lookup"><span data-stu-id="1f578-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="1f578-115">È possibile applicare il filtro geografico a tutti i file con "/" o alle cartelle selezionate specificando i percorsi di directory "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="1f578-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="1f578-116">È inoltre possibile applicare il filtro geografico a un singolo file specificando il file ed escludendo la barra finale "/pictures/city.png".</span><span class="sxs-lookup"><span data-stu-id="1f578-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="1f578-117">Esempio di filtro di percorso di directory:</span><span class="sxs-lookup"><span data-stu-id="1f578-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="1f578-118">Passaggio 2: definire l'azione Blocca o Consenti</span><span class="sxs-lookup"><span data-stu-id="1f578-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="1f578-119">**Blocca** : agli utenti dei paesi specificati verrà negato l'accesso alle risorse richieste da quel percorso ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="1f578-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="1f578-120">Se non sono state definite altre opzioni di filtro di paese per tale percorso, tutti gli altri utenti saranno autorizzati ad accedere.</span><span class="sxs-lookup"><span data-stu-id="1f578-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="1f578-121">**Consenti** : solo agli utenti dei paesi specificati verrà autorizzato l'accesso alle risorse richieste da quel percorso ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="1f578-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="1f578-122">Passaggio 3: definire i paesi</span><span class="sxs-lookup"><span data-stu-id="1f578-122">Step 3: Define the countries</span></span>
<span data-ttu-id="1f578-123">Selezionare i paesi che si desidera bloccare o consentire per il percorso.</span><span class="sxs-lookup"><span data-stu-id="1f578-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="1f578-124">Per esempio, la regola di blocco /Photos/Strasbourg/ filtrerà i file tra cui:</span><span class="sxs-lookup"><span data-stu-id="1f578-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="1f578-125">Codici paese</span><span class="sxs-lookup"><span data-stu-id="1f578-125">Country codes</span></span>
<span data-ttu-id="1f578-126">La funzionalità **Filtro geografico** usa i codici paese per definire i paesi da cui una richiesta viene consentita o bloccata per una directory protetta.</span><span class="sxs-lookup"><span data-stu-id="1f578-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="1f578-127">Gli indicativi paese sono disponibili nella pagina [Azure CDN Country Codes](https://msdn.microsoft.com/library/mt761717.aspx) (Indicativi paese della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="1f578-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="1f578-128"><a id="considerations"></a>Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1f578-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="1f578-129">Per rendere effettive le modifiche alla configurazione del filtro geografico possono essere necessari fino a 90 minuti per Verizon o un paio di minuti con Akamai.</span><span class="sxs-lookup"><span data-stu-id="1f578-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="1f578-130">Questa funzionalità non supporta i caratteri jolly (ad esempio, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="1f578-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="1f578-131">La configurazione del filtro geografico associata al percorso relativo viene applicata in modo ricorsivo a tale percorso.</span><span class="sxs-lookup"><span data-stu-id="1f578-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="1f578-132">Può essere applicata solo una regola allo stesso percorso relativo (non è possibile creare più filtri di paese che puntano allo stesso percorso relativo).</span><span class="sxs-lookup"><span data-stu-id="1f578-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="1f578-133">Tuttavia, una cartella potrebbe avere più filtri di paese.</span><span class="sxs-lookup"><span data-stu-id="1f578-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="1f578-134">Ciò è dovuto alla natura ricorsiva dei filtri di paese.</span><span class="sxs-lookup"><span data-stu-id="1f578-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="1f578-135">In altre parole, una sottocartella di una cartella configurata in precedenza può essere assegnata a un filtro di paese diverso.</span><span class="sxs-lookup"><span data-stu-id="1f578-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

