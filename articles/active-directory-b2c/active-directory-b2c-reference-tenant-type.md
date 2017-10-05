---
title: "Azure Active Directory B2C: aree di disponibilità e residenza dei dati | Microsoft Docs"
description: Un argomento sui tipi di tenant di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="7c5c5-103">Azure Active Directory B2C: aree di disponibilità e residenza dei dati</span><span class="sxs-lookup"><span data-stu-id="7c5c5-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="7c5c5-104">Le aree di disponibilità e la residenza dei dati sono due concetti molto diversi che si applicano in modo diverso ad Azure AD B2C rispetto al resto di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="7c5c5-105">In questo articolo vengono illustrate le differenze tra i due concetti e viene confrontato il modo in cui tali concetti vengono applicati ad Azure e ad Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="7c5c5-106">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7c5c5-106">Summary</span></span>
<span data-ttu-id="7c5c5-107">Azure AD B2C è **in genere disponibile in tutto il mondo** con l'opzione per la **residenza dei dati negli Stati Uniti o in Europa**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="7c5c5-108">Concetti</span><span class="sxs-lookup"><span data-stu-id="7c5c5-108">Concepts</span></span>
* <span data-ttu-id="7c5c5-109">L'**area di disponibilità** si riferisce al paese in cui è possibile usare un servizio.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="7c5c5-110">La **residenza dei dati** si riferisce alla zona in cui i dati utente vengono memorizzati.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="7c5c5-111">Aree di disponibilità</span><span class="sxs-lookup"><span data-stu-id="7c5c5-111">Region availability</span></span>
<span data-ttu-id="7c5c5-112">Azure AD B2C è disponibile in tutto il mondo tramite il cloud pubblico di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="7c5c5-113">Questo approccio è diverso da quello seguito dalla maggior parte degli altri servizi di Azure in cui sono combinate disponibilità e residenza dei dati.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="7c5c5-114">È possibile vedere alcuni esempi di questo tipo di approccio nella pagina [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) e [Prezzi di Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="7c5c5-115">Residenza dei dati</span><span class="sxs-lookup"><span data-stu-id="7c5c5-115">Data residency</span></span>
<span data-ttu-id="7c5c5-116">Azure AD B2C archivia i dati utente negli Stati Uniti o in Europa.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="7c5c5-117">La residenza dei dati viene determinata in base al paese e/o all'area geografica che viene selezionato durante [la creazione di un tenant Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="7c5c5-119">I dati risiedono negli Stati Uniti per i paesi/aree geografiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="7c5c5-120">Stati Uniti, Canada, Costa Rica, Repubblica dominicana, El Salvador, Guatemala, Messico, Panama, Portorico e Trinidad e Tobago</span><span class="sxs-lookup"><span data-stu-id="7c5c5-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="7c5c5-121">I dati risiedono in Europa per i paesi/aree geografiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="7c5c5-122">Algeria, Austria, Azerbaigian, Bahrain, Belarus, Belgio, Bulgaria, Croazia, Cipro, Repubblica ceca, Danimarca, Egitto, Estonia, Finlandia, Francia, Germania, Grecia, Ungheria, Islanda, Irlanda, Israele, Italia, Giordania, Kazakhstan, Kenya, Kuwait, Lettonia, Libano, Liechtenstein, Lituania, Lussemburgo, Ex Repubblica Jugoslava di Macedonia, Malta, Montenegro, Marocco, Paesi Bassi, Nigeria, Norvegia , Oman, Pakistan, Polonia, Portogallo, Qatar, Romania, Russia, Arabia Saudita, Serbia, Slovacchia, Slovenia, Sud Africa, Spagna, Svezia, Svizzera, Tunisia, Turchia, Ucraina, Emirati Arabi Uniti e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="7c5c5-123">I paesi rimanenti saranno aggiunti all'elenco.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="7c5c5-124">Per ora, è comunque possibile usare Azure AD B2C scegliendo uno dei paesi/aree geografiche indicati precedentemente.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="7c5c5-125">Afghanistan, Argentina, Australia, Brasile, Cile, Colombia, Ecuador, Regione amministrativa speciale di Hong Kong, India, Indonesia, Iraq, Giappone, Corea, Malaysia, Nuova Zelanda, Paraguay, Perù, Filippine, Singapore, Sri Lanka, Taiwan, Thailandia, Uruguay e Venezuela.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="7c5c5-126">Tenant di anteprima</span><span class="sxs-lookup"><span data-stu-id="7c5c5-126">Preview tenant</span></span>
<span data-ttu-id="7c5c5-127">Se è stato creato un tenant B2C durante il periodo di anteprima di Azure AD B2C, è probabile che **Tipo di tenant** sia **Tenant di anteprima**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="7c5c5-128">In questo caso, è NECESSARIO usare il tenant solo per scopi di sviluppo e test e non per le app di produzione.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c5c5-129">Non esiste un percorso di migrazione da una versione di anteprima del tenant B2C a un tenant B2C a livello di produzione.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="7c5c5-130">Si noti che si verificano problemi noti quando si elimina un tenant B2C di anteprima e viene creato un tenant B2C a livello di produzione con lo stesso nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="7c5c5-131">È necessario creare un tenant B2C a livello di produzione con un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
