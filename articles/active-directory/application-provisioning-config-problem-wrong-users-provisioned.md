---
title: "È in corso il provisioning di un set errato di utenti per un'applicazione della raccolta di Azure AD | Microsoft Docs"
description: "Informazioni su come individuare i motivi per cui è in corso il provisioning di un set di utenti per un'applicazione diverso da quello previsto"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="5dc96-103">È in corso il provisioning di un set errato di utenti per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5dc96-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="5dc96-104">Il provisioning degli utenti dell'app è principalmente basato su quali utenti e gruppi sono stati **assegnati** all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="5dc96-105">Usare le risorse seguenti per informazioni su come verificare quali utenti e gruppi sono stati assegnati a un'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dc96-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="5dc96-106">Assegnare un utente direttamente come amministratore</span><span class="sxs-lookup"><span data-stu-id="5dc96-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="5dc96-107">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5dc96-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5dc96-108">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dc96-109">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5dc96-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dc96-110">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dc96-111">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dc96-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dc96-112">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5dc96-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5dc96-113">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5dc96-114">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="5dc96-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5dc96-115">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dc96-116">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5dc96-117">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5dc96-118">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5dc96-119">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5dc96-120">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5dc96-121">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="5dc96-122">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5dc96-123">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="5dc96-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="5dc96-124">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="5dc96-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="5dc96-125">Se il provisioning è configurato e già in esecuzione per un'app, il provisioning di nuovi utenti per un'applicazione dovrebbe essere eseguito dopo circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="5dc96-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="5dc96-126">Controllare i **registri di controllo** per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="5dc96-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="5dc96-127">Assegnare un gruppo direttamente a un'applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="5dc96-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="5dc96-128">Per assegnare uno o più gruppi direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5dc96-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5dc96-129">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dc96-130">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5dc96-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dc96-131">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dc96-132">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dc96-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5dc96-133">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5dc96-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5dc96-134">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5dc96-135">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="5dc96-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5dc96-136">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5dc96-137">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5dc96-138">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5dc96-139">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo del gruppo** a cui si vuole eseguire l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5dc96-140">Posizionare il puntatore sul **gruppo** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5dc96-141">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo del gruppo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5dc96-142">**Facoltativo:** se si vuole **aggiungere più di un gruppo**, digitare un altro **nome completo di gruppo** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="5dc96-143">Dopo avere selezionato i gruppi, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5dc96-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5dc96-144">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="5dc96-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="5dc96-145">Fare clic sul pulsante **Assegna** per assegnare l'applicazione ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="5dc96-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="5dc96-146">Se il provisioning è configurato e già in esecuzione per un'app, il provisioning dei nuovi utenti inclusi nel gruppo dovrebbe essere eseguito per un'applicazione dopo circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="5dc96-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="5dc96-147">Controllare i **registri di controllo** per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="5dc96-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5dc96-148">Eseguire il provisioning dei dettagli del gruppo e del nome del gruppo, oltre ai membri, se supportato per alcune applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5dc96-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="5dc96-149">È possibile abilitare o disabilitare questa funzionalità attivando o disattivando il **mapping** per gli oggetti di gruppo visualizzati nella scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="5dc96-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="5dc96-150">Se il provisioning di gruppi è abilitato, assicurarsi di verificare i mapping degli attributi per garantire che viene usato un campo appropriato per il "corrispondente ID".</span><span class="sxs-lookup"><span data-stu-id="5dc96-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="5dc96-151">Questo può essere il nome visualizzato o l'alias di posta elettronica, poiché il provisioning del gruppo e dei relativi membri non viene effettuato se la proprietà corrispondente è vuota o non popolata per un gruppo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dc96-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dc96-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5dc96-152">Next steps</span></span>
[<span data-ttu-id="5dc96-153">Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dc96-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
