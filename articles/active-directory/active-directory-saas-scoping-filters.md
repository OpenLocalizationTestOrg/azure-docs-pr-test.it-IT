---
title: App aaaProvisioning con i filtri di ambito | Documenti Microsoft
description: Informazioni su come ambito toouse Filtra gli oggetti di tooprevent nelle applicazioni che supportano il provisioning utenti automatizzato da effettivamente in corso il provisioning se un oggetto non soddisfa i requisiti aziendali.
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="8b7b4-103">Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito</span><span class="sxs-lookup"><span data-stu-id="8b7b4-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="8b7b4-104">obiettivo di Hello di questa sezione è tooexplain come ambito toouse filtri toodefine basato su attributi regole che determinano quali utenti sono il provisioning dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="8b7b4-105">Clausole e gruppi di ambiti</span><span class="sxs-lookup"><span data-stu-id="8b7b4-105">Clauses and Scope Groups</span></span>
![Filtro per la definizione dell’ambito][1] 

<span data-ttu-id="8b7b4-107">I filtri per la determinazione dell'ambito sono definiti da uno o più **gruppi di ambiti**, ognuno dei quali contiene una o più **clausole**.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="8b7b4-108">clausole hello toosee per un particolare gruppo di ambito, espandere facendo clic a sinistra di hello freccia toohello hello del nome di gruppo.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="8b7b4-109">Oggetto **clausola** determina quali utenti sono autorizzati toopass tramite hello definizione ambito filtro valutando gli attributi di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="8b7b4-110">Ad esempio, potrebbe essere una clausola che richiede che 'state' attributo uguale New York un utente, in modo solo gli utenti di New York vengono effettuato il provisioning in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Nome del gruppo di ambiti][2] 

<span data-ttu-id="8b7b4-112">Ogni **gruppo ambito** inizia con uno obbligatorio **clausola**, come illustrato nella schermata di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="8b7b4-113">Questa clausola indica semplicemente che l'utente hello deve essere assegnato toohello applicazione prima di essere valutato dai filtri di ambito.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="8b7b4-114">Questa clausola non può essere eliminata né modificata.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="8b7b4-115">È possibile aggiungere nuove clausole o nuovi gruppi di ambito premendo l'apposito pulsante hello.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="8b7b4-116">Per assegnare un nome a ogni gruppo di ambiti, modificare la relativa proprietà **Nome del gruppo di ambiti** .</span><span class="sxs-lookup"><span data-stu-id="8b7b4-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="8b7b4-117">Modalità di valutazione dei filtri per la definizione dell'ambito</span><span class="sxs-lookup"><span data-stu-id="8b7b4-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="8b7b4-118">Durante il provisioning, ogni utente assegnato contro l'ambito toodetermine filtri verranno testate se l'applicazione di accesso toohello è idoneo.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="8b7b4-119">È possibile considerare ogni clausola come un test che deve essere passato affinché tooavoid utente hello venga escluso.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="8b7b4-120">Se si dispone di più gruppi di ambito definiti, ogni utente deve passare almeno uno di essi tooaccess applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="8b7b4-121">All'interno di ogni gruppo di ambito, tuttavia, hello utente deve passare toopass ogni clausola tale gruppo di ambito specifico.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="8b7b4-122">In altre parole, è possibile considerare come i gruppi di ambito o correlati con l'operatore e può essere considerato clausole hello al loro interno come AND correlati con l'operatore.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="8b7b4-123">Si consideri ad esempio hello definizione ambito filtro riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8b7b4-123">For example, consider hello scoping filter below:</span></span>

![Nome del gruppo di ambiti][3]  

<span data-ttu-id="8b7b4-125">In base toothis definizione ambito filtro, gli utenti devono soddisfare seguente hello criteri, toobe il provisioning:</span><span class="sxs-lookup"><span data-stu-id="8b7b4-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="8b7b4-126">È necessario assegnare toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="8b7b4-127">Devono lavorare nel reparto Engineering hello</span><span class="sxs-lookup"><span data-stu-id="8b7b4-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="8b7b4-128">La sede di lavoro deve trovarsi a San Francisco o in Canada.</span><span class="sxs-lookup"><span data-stu-id="8b7b4-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="8b7b4-129">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="8b7b4-129">Related Articles</span></span>
* [<span data-ttu-id="8b7b4-130">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b7b4-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8b7b4-131">Automatizzare applicazioni di tooSaaS Provisioning e Deprovisioning</span><span class="sxs-lookup"><span data-stu-id="8b7b4-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="8b7b4-132">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="8b7b4-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="8b7b4-133">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="8b7b4-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="8b7b4-134">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="8b7b4-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="8b7b4-135">Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="8b7b4-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="8b7b4-136">Elenco di esercitazioni sulla tooIntegrate App SaaS</span><span class="sxs-lookup"><span data-stu-id="8b7b4-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
