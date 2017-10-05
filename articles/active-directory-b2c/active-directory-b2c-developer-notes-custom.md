---
title: 'Azure Active Directory B2C: note per gli sviluppatori sull''uso dei criteri personalizzati | Microsoft Docs'
description: Note per gli sviluppatori sulla configurazione e la gestione di Azure AD B2C con criteri personalizzati
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="2839f-103">Note sulla versione di anteprima pubblica dei criteri personalizzati di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="2839f-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="2839f-104">Il set di funzionalità dei criteri personalizzati è ora disponibile per la valutazione in anteprima pubblica per tutti i clienti di Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="2839f-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="2839f-105">Questo set di funzionalità è destinato agli sviluppatori esperti che creano le soluzioni di gestione delle identità più complesse.</span><span class="sxs-lookup"><span data-stu-id="2839f-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="2839f-106">Attualmente, questo set di funzionalità richiede agli sviluppatori di configurare direttamente il framework dell'esperienza di gestione delle identità tramite la modifica di file XML.</span><span class="sxs-lookup"><span data-stu-id="2839f-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="2839f-107">Si tratta di un metodo di configurazione avanzato e complesso.</span><span class="sxs-lookup"><span data-stu-id="2839f-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="2839f-108">Gli sviluppatori esperti di soluzioni di gestione delle identità che usano questo framework dovranno includere nei piani il tempo necessario per completare le procedure dettagliate e leggere i documenti di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2839f-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="2839f-109">Funzionalità incluse nell'anteprima pubblica</span><span class="sxs-lookup"><span data-stu-id="2839f-109">Features included in this public preview</span></span>
<span data-ttu-id="2839f-110">Con le nuove funzionalità introdotte nell'anteprima pubblica, gli sviluppatori possono eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="2839f-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="2839f-111">Creare e caricare percorsi utente di autenticazione personalizzati usando criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2839f-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="2839f-112">Descrivere in modo dettagliato i percorsi utente come scambi tra provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="2839f-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="2839f-113">Definire la diramazione condizionale nei percorsi utente.</span><span class="sxs-lookup"><span data-stu-id="2839f-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="2839f-114">Integrare servizi abilitati per API REST nei percorsi utente di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2839f-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="2839f-115">Aggiungere la federazione con provider di identità conformi allo standard OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2839f-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="2839f-116">Aggiungere la federazione con provider di identità che rispettano il protocollo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="2839f-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="2839f-117">Condizioni per l'anteprima pubblica</span><span class="sxs-lookup"><span data-stu-id="2839f-117">Terms of the public preview</span></span>

* <span data-ttu-id="2839f-118">È consigliabile usare le nuove funzionalità solo a scopo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="2839f-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="2839f-119">Le nuove funzionalità non sono destinate all'uso in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2839f-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="2839f-120">I contratti di servizio non si applicano alle nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2839f-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="2839f-121">È possibile inviare richieste di supporto tramite i normali canali del supporto.</span><span class="sxs-lookup"><span data-stu-id="2839f-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="2839f-122">Non è stata fissata una data per la disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="2839f-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="2839f-123">A propria discrezione e per qualsiasi motivo, Microsoft può contrassegnare e rifiutare o limitare gli scenari e i percorsi utente che esulano dagli obiettivi del prodotto Azure AD B2C di offrire una piattaforma di gestione delle identità e degli accessi per i clienti.</span><span class="sxs-lookup"><span data-stu-id="2839f-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="2839f-124">Responsabilità degli sviluppatori che usano il set di funzionalità dei criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="2839f-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="2839f-125">La configurazione manuale dei criteri garantisce un accesso di livello inferiore alla piattaforma sottostante di Azure AD B2C e determina la creazione di un framework attendibilità interamente personalizzabile e univoco.</span><span class="sxs-lookup"><span data-stu-id="2839f-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="2839f-126">Le possibili permutazioni di provider di identità personalizzati, relazioni di trust, integrazioni con servizi esterni e flussi di lavoro dettagliati risultano particolarmente impegnative per gli sviluppatori esperti da cui vengono utilizzate.</span><span class="sxs-lookup"><span data-stu-id="2839f-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="2839f-127">Per sfruttare appieno l'anteprima pubblica, è consigliabile che gli sviluppatori che utilizzano il set di funzionalità dei criteri personalizzati si attengano alle linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="2839f-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="2839f-128">Acquisire familiarità con il linguaggio di configurazione del motore dell'esperienza di gestione delle identità e con la gestione di chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="2839f-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="2839f-129">Assumere la proprietà degli scenari e delle integrazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="2839f-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="2839f-130">Eseguire test metodici degli scenari.</span><span class="sxs-lookup"><span data-stu-id="2839f-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="2839f-131">Seguire le procedure consigliate di staging e sviluppo software con almeno un ambiente di sviluppo e testing e un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2839f-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="2839f-132">Mantenersi aggiornati sui nuovi sviluppi dei servizi e dei provider di identità con cui viene eseguita l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="2839f-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="2839f-133">Ad esempio, tenere traccia delle modifiche dei segreti e delle modifiche pianificate e non pianificate del servizio.</span><span class="sxs-lookup"><span data-stu-id="2839f-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="2839f-134">Configurare il monitoraggio attivo e monitorare il tempo di risposta degli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="2839f-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="2839f-135">Mantenere aggiornati gli indirizzi di posta elettronica di contatto e prestare attenzione ai messaggi di posta elettronica del team del sito live Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2839f-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="2839f-136">Intervenire tempestivamente quando consigliato del team del sito live Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2839f-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="2839f-137">Queste funzionalità potrebbero essere infine incluse nei criteri predefiniti di Azure AD, diventando così accessibili a tutti gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2839f-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2839f-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2839f-138">Next steps</span></span>
<span data-ttu-id="2839f-139">[Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="2839f-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
