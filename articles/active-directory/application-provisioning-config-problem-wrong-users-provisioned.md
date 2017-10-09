---
title: aaaWrong set di utenti stanno applicazione raccolta tooan provisioning Azure AD | Documenti Microsoft
description: Informazioni su come toofind il motivo per cui un set diverso di utenti viene effettuato il provisioning tooan applicazione rispetto a quelli previsti
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a><span data-ttu-id="f4a2a-103">Il set corretto di utenti stanno applicazione raccolta tooan provisioning Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a2a-103">Wrong set of users are being provisioned tooan Azure AD Gallery application</span></span>

<span data-ttu-id="f4a2a-104">Gli utenti che sono toohello provisioning app è principalmente dovute quali utenti e gruppi sono stati **assegnato** toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-104">Which users are provisioned toohello app is primarily driven by which users and groups have been **assigned** toohello application.</span></span>

<span data-ttu-id="f4a2a-105">Utilizzare le risorse di hello sotto toolearn come toocheck quali utenti e gruppi assegnati tooan applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-105">Use hello resources below toolearn how toocheck which users and groups have been assigned tooan application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="f4a2a-106">Assegnare un utente direttamente come amministratore</span><span class="sxs-lookup"><span data-stu-id="f4a2a-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="f4a2a-107">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="f4a2a-107">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="f4a2a-108">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="f4a2a-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f4a2a-109">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f4a2a-110">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f4a2a-111">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f4a2a-112">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-112">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f4a2a-113">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="f4a2a-113">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f4a2a-114">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-114">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="f4a2a-115">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-115">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f4a2a-116">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-116">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f4a2a-117">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-117">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f4a2a-118">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-118">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f4a2a-119">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-119">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="f4a2a-120">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-120">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="f4a2a-121">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-121">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="f4a2a-122">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-122">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="f4a2a-123">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-123">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="f4a2a-124">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-124">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="f4a2a-125">Se il provisioning è configurato ed è già in esecuzione per un'app, i nuovi utenti dovranno essere applicazione tooan provisioning in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-125">If provisioning is configured and already running for an app, new users should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="f4a2a-126">Controllare hello **i log di controllo** per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-126">Check hello **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="f4a2a-127">Assegnare un gruppo direttamente tooan applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="f4a2a-127">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="f4a2a-128">tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="f4a2a-128">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="f4a2a-129">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="f4a2a-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f4a2a-130">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f4a2a-131">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f4a2a-132">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f4a2a-133">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-133">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f4a2a-134">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="f4a2a-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f4a2a-135">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-135">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="f4a2a-136">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-136">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f4a2a-137">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-137">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f4a2a-138">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-138">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f4a2a-139">Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-139">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f4a2a-140">Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-140">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="f4a2a-141">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-141">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="f4a2a-142">**Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-142">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="f4a2a-143">Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-143">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="f4a2a-144">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-144">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="f4a2a-145">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-145">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="f4a2a-146">Se il provisioning è configurato ed è già in esecuzione per un'app, nuovi utenti, incluso nel gruppo di hello devono essere sottoposto a provisioning tooan applicazione circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-146">If provisioning is configured and already running for an app, new users contained within hello group should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="f4a2a-147">Controllare hello **i log di controllo** per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-147">Check hello **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f4a2a-148">Provisioning di hello nome del gruppo e gruppo dettagli, nei membri toohello inoltre, se supportato per alcune applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-148">Provisioning of hello group name and group details, in addition toohello members, if supported for some applications.</span></span> <span data-ttu-id="f4a2a-149">È possibile abilitare o disabilitare questa funzionalità abilitando o disabilitando hello **Mapping** per oggetti di gruppo visualizzati nelle hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-149">You can enable or disable this functionality by enabling or disabling hello **Mapping** for group objects shown in hello **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="f4a2a-150">Se è abilitato il provisioning di gruppi, prestare attenzione tooreview hello attributo mapping tooensure un campo appropriato viene utilizzato per hello "corrispondente di ID".</span><span class="sxs-lookup"><span data-stu-id="f4a2a-150">If provisioning groups is enabled, be sure tooreview hello attribute mappings tooensure an appropriate field is being used for hello “matching ID”.</span></span> <span data-ttu-id="f4a2a-151">Può trattarsi di nome visualizzato hello o posta elettronica, alias, come hello gruppo e i relativi membri non essere disponibile se la proprietà corrispondente hello è vuota o non popolata per un gruppo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a2a-151">This can be hello display name or email alias, as hello group and its members not be provisioned if hello matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4a2a-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4a2a-152">Next steps</span></span>
[<span data-ttu-id="f4a2a-153">Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4a2a-153">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
