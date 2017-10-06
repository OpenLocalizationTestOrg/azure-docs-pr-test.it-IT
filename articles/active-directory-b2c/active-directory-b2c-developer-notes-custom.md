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
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="1937e-103">Note sulla versione di anteprima pubblica dei criteri personalizzati di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="1937e-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="1937e-104">Hello criterio personalizzato per il set di funzionalità è ora disponibile per la valutazione in un'anteprima pubblica di Azure tutti, B2C Active Directory (Azure AD B2C) clienti.</span><span class="sxs-lookup"><span data-stu-id="1937e-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="1937e-105">Questo set di funzionalità è rivolto agli sviluppatori di identità avanzate la creazione di soluzioni di identità più complesse hello.</span><span class="sxs-lookup"><span data-stu-id="1937e-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="1937e-106">Oggi per questo set di funzionalità necessari agli sviluppatori tooconfigure hello identità esperienza Framework direttamente tramite la modifica di file XML.</span><span class="sxs-lookup"><span data-stu-id="1937e-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="1937e-107">Si tratta di un metodo di configurazione avanzato e complesso.</span><span class="sxs-lookup"><span data-stu-id="1937e-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="1937e-108">Agli sviluppatori di identità usando hello avanzati identità esperienza Framework consigliabile tooinvest del tempo di completamento delle procedure e la lettura dei documenti di riferimento.</span><span class="sxs-lookup"><span data-stu-id="1937e-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="1937e-109">Funzionalità incluse nell'anteprima pubblica</span><span class="sxs-lookup"><span data-stu-id="1937e-109">Features included in this public preview</span></span>
<span data-ttu-id="1937e-110">Con hello nuove funzionalità introdotte in anteprima pubblica di hello, gli sviluppatori possono eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="1937e-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="1937e-111">Creare e caricare percorsi utente di autenticazione personalizzati usando criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1937e-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="1937e-112">Descrivere in modo dettagliato i percorsi utente come scambi tra provider di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="1937e-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="1937e-113">Definire la diramazione condizionale nei percorsi utente.</span><span class="sxs-lookup"><span data-stu-id="1937e-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="1937e-114">Integrare servizi abilitati per API REST nei percorsi utente di autenticazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1937e-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="1937e-115">Aggiungere la federazione con provider di identità che sono conformi a hello OpenIDConnect standard.</span><span class="sxs-lookup"><span data-stu-id="1937e-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="1937e-116">Aggiungere la federazione con provider di identità che rispettano protocollo toohello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1937e-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="1937e-117">Condizioni per l'anteprima pubblica di hello</span><span class="sxs-lookup"><span data-stu-id="1937e-117">Terms of hello public preview</span></span>

* <span data-ttu-id="1937e-118">Si consiglia di nuove funzionalità hello toouse solo a fini di valutazione.</span><span class="sxs-lookup"><span data-stu-id="1937e-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="1937e-119">Le nuove funzionalità non sono destinate all'uso in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1937e-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="1937e-120">Contratti di servizio (SLA) si applicano toohello nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1937e-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="1937e-121">È possibile inviare richieste di supporto tramite i normali canali del supporto.</span><span class="sxs-lookup"><span data-stu-id="1937e-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="1937e-122">Non è stata fissata una data per la disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="1937e-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="1937e-123">Discrezione e per qualsiasi motivo, Microsoft può flag e rifiutare o limitare gli scenari e i percorsi di utente che superano l'ambito di hello di hello Azure Active Directory B2C prodotto fondatore tooserve come una piattaforma di gestione (CIAM) cliente identità e accessi.</span><span class="sxs-lookup"><span data-stu-id="1937e-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="1937e-124">Responsabilità degli sviluppatori che usano il set di funzionalità dei criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="1937e-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="1937e-125">Configurazione manuale dei criteri concede l'accesso di livello inferiore toohello sottostante piattaforma di Azure Active Directory B2C e comporta hello creazione di un framework di trust completamente personalizzabile univoco.</span><span class="sxs-lookup"><span data-stu-id="1937e-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="1937e-126">Le combinazioni possibili di provider di identità personalizzati, le relazioni di trust, integrazioni con servizi esterni e i flussi di lavoro dettagliate inserire le richieste di maggiore su hello avanzate gli sviluppatori che li usano.</span><span class="sxs-lookup"><span data-stu-id="1937e-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="1937e-127">toofully vantaggio dalla versione di anteprima pubblica hello, è consigliabile che gli sviluppatori che usano set di funzionalità di criteri personalizzata hello osservate toohello alle linee guida:</span><span class="sxs-lookup"><span data-stu-id="1937e-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="1937e-128">Acquisire familiarità con il linguaggio di configurazione hello di hello del motore di analisi di identità e la gestione di chiave/i segreti.</span><span class="sxs-lookup"><span data-stu-id="1937e-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="1937e-129">Assumere la proprietà degli scenari e delle integrazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="1937e-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="1937e-130">Eseguire test metodici degli scenari.</span><span class="sxs-lookup"><span data-stu-id="1937e-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="1937e-131">Seguire le procedure consigliate di staging e sviluppo software con almeno un ambiente di sviluppo e testing e un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1937e-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="1937e-132">Essere informati sugli ultimi sviluppi dal provider di identità hello e si integra con servizi.</span><span class="sxs-lookup"><span data-stu-id="1937e-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="1937e-133">Ad esempio, tenere traccia delle modifiche nei segreti e del servizio toohello pianificati e le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1937e-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="1937e-134">Impostare il monitoraggio attivo e monitorare i tempi di risposta hello degli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="1937e-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="1937e-135">Mantenere aggiornati gli indirizzi di posta elettronica di contatto e rimanere messaggi di posta elettronica sito live team Microsoft toohello reattiva.</span><span class="sxs-lookup"><span data-stu-id="1937e-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="1937e-136">Intervento tempestivo quando toodo consigliato in modo che una hello team live-sito Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1937e-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="1937e-137">Queste funzionalità potrebbero essere incluso in criteri predefiniti di Azure AD, rendendoli più accessibile agli sviluppatori di tooall.</span><span class="sxs-lookup"><span data-stu-id="1937e-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1937e-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1937e-138">Next steps</span></span>
<span data-ttu-id="1937e-139">[Introduzione ai criteri personalizzati](active-directory-b2c-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="1937e-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
