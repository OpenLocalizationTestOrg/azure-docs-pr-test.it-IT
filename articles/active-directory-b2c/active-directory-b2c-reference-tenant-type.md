---
title: "Azure Active Directory B2C: aree di disponibilità e residenza dei dati | Microsoft Docs"
description: Un argomento sui tipi di hello di tenant di Azure Active Directory B2C
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="57ce8-103">Azure Active Directory B2C: aree di disponibilità e residenza dei dati</span><span class="sxs-lookup"><span data-stu-id="57ce8-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="57ce8-104">La residenza in dati e la disponibilità di area sono due concetti molto diversi che si applicano in modo diverso tooAzure AD B2C dal resto hello di Azure.</span><span class="sxs-lookup"><span data-stu-id="57ce8-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="57ce8-105">In questo articolo verrà illustrano hello differenze tra questi due concetti e confrontare come si applica tooAzure e Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="57ce8-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="57ce8-106">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="57ce8-106">Summary</span></span>
<span data-ttu-id="57ce8-107">Azure Active Directory B2C è **in genere disponibile in tutto il mondo** con l'opzione hello **residenza dati negli Stati Uniti o in Europa**.</span><span class="sxs-lookup"><span data-stu-id="57ce8-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="57ce8-108">Concetti</span><span class="sxs-lookup"><span data-stu-id="57ce8-108">Concepts</span></span>
* <span data-ttu-id="57ce8-109">**Disponibilità area** toowhere di fa riferimento un servizio è disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="57ce8-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="57ce8-110">**La residenza in dati** fa riferimento toowhere utente vengono archiviati.</span><span class="sxs-lookup"><span data-stu-id="57ce8-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="57ce8-111">Aree di disponibilità</span><span class="sxs-lookup"><span data-stu-id="57ce8-111">Region availability</span></span>
<span data-ttu-id="57ce8-112">Azure Active Directory B2C è disponibile in tutto il mondo tramite hello cloud pubblico di Azure.</span><span class="sxs-lookup"><span data-stu-id="57ce8-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="57ce8-113">Questo comportamento è diverso dal modello hello maggior parte degli altri eseguire servizi di Azure cui associare la disponibilità a residenza in dati.</span><span class="sxs-lookup"><span data-stu-id="57ce8-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="57ce8-114">È possibile visualizzare esempi di questo tipo in entrambi Azure [prodotti disponibili per regione](https://azure.microsoft.com/regions/services/) pagina e hello [calcolatore dei costi di Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="57ce8-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="57ce8-115">Residenza dei dati</span><span class="sxs-lookup"><span data-stu-id="57ce8-115">Data residency</span></span>
<span data-ttu-id="57ce8-116">Azure AD B2C archivia i dati utente negli Stati Uniti o in Europa.</span><span class="sxs-lookup"><span data-stu-id="57ce8-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="57ce8-117">La residenza dei dati viene determinata in base al paese e/o all'area geografica che viene selezionato durante [la creazione di un tenant Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="57ce8-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="57ce8-119">Dati si trovano negli Stati Uniti hello per hello seguente paesi/aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="57ce8-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="57ce8-120">Stati Uniti, Canada, Costa Rica, Repubblica dominicana, El Salvador, Guatemala, Messico, Panama, Portorico e Trinidad e Tobago</span><span class="sxs-lookup"><span data-stu-id="57ce8-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="57ce8-121">Dati si trovano in Europa per hello paesi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57ce8-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="57ce8-122">Algeria, Austria, Azerbaigian, Bahrain, Belarus, Belgio, Bulgaria, Croazia, Cipro, Repubblica ceca, Danimarca, Egitto, Estonia, Finlandia, Francia, Germania, Grecia, Ungheria, Islanda, Irlanda, Israele, Italia, Giordania, Kazakhstan, Kenya, Kuwait, Lettonia, Libano, Liechtenstein, Lituania, Lussemburgo, Ex Repubblica Jugoslava di Macedonia, Malta, Montenegro, Marocco, Paesi Bassi, Nigeria, Norvegia , Oman, Pakistan, Polonia, Portogallo, Qatar, Romania, Russia, Arabia Saudita, Serbia, Slovacchia, Slovenia, Sud Africa, Spagna, Svezia, Svizzera, Tunisia, Turchia, Ucraina, Emirati Arabi Uniti e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="57ce8-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="57ce8-123">Hello rimanenti paesi sono nel processo di hello dall'elenco toohello aggiunta.</span><span class="sxs-lookup"><span data-stu-id="57ce8-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="57ce8-124">Per il momento, è possibile utilizzare ancora Azure Active Directory B2C scegliendo hello paesi/aree precedente.</span><span class="sxs-lookup"><span data-stu-id="57ce8-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="57ce8-125">Afghanistan, Argentina, Australia, Brasile, Cile, Colombia, Ecuador, Regione amministrativa speciale di Hong Kong, India, Indonesia, Iraq, Giappone, Corea, Malaysia, Nuova Zelanda, Paraguay, Perù, Filippine, Singapore, Sri Lanka, Taiwan, Thailandia, Uruguay e Venezuela.</span><span class="sxs-lookup"><span data-stu-id="57ce8-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="57ce8-126">Tenant di anteprima</span><span class="sxs-lookup"><span data-stu-id="57ce8-126">Preview tenant</span></span>
<span data-ttu-id="57ce8-127">Se è stato creato un tenant B2C durante il periodo di anteprima di Azure AD B2C, è probabile che **Tipo di tenant** sia **Tenant di anteprima**.</span><span class="sxs-lookup"><span data-stu-id="57ce8-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="57ce8-128">In caso di hello, è necessario utilizzare il tenant solo per scopi di sviluppo e test e non per le applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="57ce8-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57ce8-129">Non è un percorso di migrazione da un'anteprima tenant B2C di B2C tenant tooa scala di produzione.</span><span class="sxs-lookup"><span data-stu-id="57ce8-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="57ce8-130">Si noti che si verificano problemi quando si elimina un tenant di anteprima B2C e ricreare il tenant B2C una scala di produzione hello stesso nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="57ce8-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="57ce8-131">Disporre di toocreate un tenant B2C scala di produzione con un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="57ce8-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
