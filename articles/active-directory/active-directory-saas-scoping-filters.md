---
title: Eseguire il provisioning delle app con filtri per la definizione dell'ambito | Documentazione Microsoft
description: Informazioni su come usare i filtri per la definizione dell'ambito per evitare che venga eseguito il provisioning degli oggetti inclusi nelle app che supportano il provisioning automatico degli utenti se un oggetto non soddisfa i requisiti aziendali.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="24cd7-103">Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito</span><span class="sxs-lookup"><span data-stu-id="24cd7-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="24cd7-104">Questa sezione spiega come usare i filtri per la definizione dell'ambito per definire regole basate su attributi per determinare gli utenti per i quali viene eseguito il provisioning nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="24cd7-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="24cd7-105">Clausole e gruppi di ambiti</span><span class="sxs-lookup"><span data-stu-id="24cd7-105">Clauses and Scope Groups</span></span>
![Filtro per la definizione dell’ambito][1] 

<span data-ttu-id="24cd7-107">I filtri per la determinazione dell'ambito sono definiti da uno o più **gruppi di ambiti**, ognuno dei quali contiene una o più **clausole**.</span><span class="sxs-lookup"><span data-stu-id="24cd7-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="24cd7-108">Per visualizzare le clausole per un gruppo di ambiti specifico, espanderlo facendo clic sulla freccia a sinistra del nome del gruppo.</span><span class="sxs-lookup"><span data-stu-id="24cd7-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="24cd7-109">Una **clausola** determina gli utenti che verranno restituiti dal filtro per la definizione dell'ambito valutando gli attributi di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="24cd7-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="24cd7-110">Ad esempio, se una clausola richiede che l'attributo 'state' di un utente sia uguale a New York, nell'applicazione viene eseguito il provisioning solo degli utenti di New York.</span><span class="sxs-lookup"><span data-stu-id="24cd7-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Nome del gruppo di ambiti][2] 

<span data-ttu-id="24cd7-112">Ogni **gruppo di ambiti** inizia con una **clausola** obbligatoria, come mostrato nella schermata.</span><span class="sxs-lookup"><span data-stu-id="24cd7-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="24cd7-113">Questa clausola indica semplicemente che l'utente deve essere assegnato all'applicazione prima di essere valutato dai filtri per la definizione dell'ambito.</span><span class="sxs-lookup"><span data-stu-id="24cd7-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="24cd7-114">Questa clausola non può essere eliminata né modificata.</span><span class="sxs-lookup"><span data-stu-id="24cd7-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="24cd7-115">Per aggiungere nuove clausole o nuovi gruppi di ambiti, fare clic sul pulsante corrispondente.</span><span class="sxs-lookup"><span data-stu-id="24cd7-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="24cd7-116">Per assegnare un nome a ogni gruppo di ambiti, modificare la relativa proprietà **Nome del gruppo di ambiti** .</span><span class="sxs-lookup"><span data-stu-id="24cd7-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="24cd7-117">Modalità di valutazione dei filtri per la definizione dell'ambito</span><span class="sxs-lookup"><span data-stu-id="24cd7-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="24cd7-118">Durante il provisioning, ogni utente assegnato viene verificato in base ai filtri per la definizione dell'ambito per stabilire se l'utente è autorizzato ad accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="24cd7-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="24cd7-119">Si può pensare a una clausola come a un test che deve essere superato affinché l'utente non venga escluso.</span><span class="sxs-lookup"><span data-stu-id="24cd7-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="24cd7-120">Se sono stati definiti più gruppi di ambiti, ogni utente deve superarne almeno uno per poter accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="24cd7-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="24cd7-121">All'interno di ogni gruppo di ambiti, tuttavia, l'utente deve superare la clausola per soddisfare i criteri del gruppo di ambiti specifico.</span><span class="sxs-lookup"><span data-stu-id="24cd7-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="24cd7-122">In altre parole, è come se i gruppi di ambiti fossero collegati tramite operatore OR e le clausole in essi contenute fossero collegate tramite operatore AND.</span><span class="sxs-lookup"><span data-stu-id="24cd7-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="24cd7-123">Vedere ad esempio il filtro per la definizione dell'ambito seguente:</span><span class="sxs-lookup"><span data-stu-id="24cd7-123">For example, consider the scoping filter below:</span></span>

![Nome del gruppo di ambiti][3]  

<span data-ttu-id="24cd7-125">In base a questo filtro per la definizione dell'ambito, affinché sia possibile eseguire il provisioning degli utenti nell'applicazione, questi devono soddisfare i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="24cd7-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="24cd7-126">Devono essere assegnati all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="24cd7-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="24cd7-127">Devono lavorare nel reparto Engineering.</span><span class="sxs-lookup"><span data-stu-id="24cd7-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="24cd7-128">La sede di lavoro deve trovarsi a San Francisco o in Canada.</span><span class="sxs-lookup"><span data-stu-id="24cd7-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="24cd7-129">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="24cd7-129">Related Articles</span></span>
* [<span data-ttu-id="24cd7-130">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24cd7-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="24cd7-131">Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="24cd7-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="24cd7-132">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="24cd7-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="24cd7-133">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="24cd7-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="24cd7-134">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="24cd7-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="24cd7-135">Uso di SCIM per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="24cd7-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="24cd7-136">Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="24cd7-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
