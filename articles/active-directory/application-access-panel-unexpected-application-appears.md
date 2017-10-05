---
title: Come vengono visualizzate le applicazioni nel pannello di accesso | Microsoft Docs
description: Risolvere i problemi relativi alla visualizzazione di un'applicazione nel panello di accesso
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
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="def79-103">Come vengono visualizzate le applicazioni nel pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="def79-103">How applications appear on the access panel</span></span>

<span data-ttu-id="def79-104">Il pannello di accesso è un portale basato sul Web e consente a un utente che ha un account aziendale o dell'istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate su cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="def79-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="def79-105">Queste applicazioni sono configurate per conto dell'utente nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="def79-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="def79-106">L'amministratore può effettuare il provisioning dell'applicazione direttamente per un utente o un gruppo di cui fa parte l'utente. Come risultato di questa operazione, l'applicazione viene visualizzata nel pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="def79-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="def79-107">Problemi generali da verificare prima</span><span class="sxs-lookup"><span data-stu-id="def79-107">General issues to check first</span></span>

-   <span data-ttu-id="def79-108">Se un'applicazione è stata appena rimossa da un utente o da un gruppo di cui l'utente è membro, provare ad accedere e a disconnettersi di nuovo dal pannello di accesso dell'utente dopo alcuni minuti per vedere se l'applicazione è stata rimossa.</span><span class="sxs-lookup"><span data-stu-id="def79-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="def79-109">Se è stata appena rimossa una licenza da un utente o da un gruppo di cui l'utente è membro, l'aggiornamento della visualizzazione potrebbe richiedere molto tempo a seconda delle dimensioni e della complessità del gruppo.</span><span class="sxs-lookup"><span data-stu-id="def79-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="def79-110">Attendere un tempo più lungo prima di accedere al pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="def79-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="def79-111">Problemi relativi all'assegnazione di applicazioni agli utenti</span><span class="sxs-lookup"><span data-stu-id="def79-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="def79-112">Un utente potrebbe vedere un'applicazione nel proprio pannello di accesso perché è stato assegnato precedentemente all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="def79-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="def79-113">Di seguito sono elencate alcuni modi per verificare questa situazione:</span><span class="sxs-lookup"><span data-stu-id="def79-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="def79-114">Controllare se un utente è assegnato all'applicazione</span><span class="sxs-lookup"><span data-stu-id="def79-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="def79-115">Controllare se un utente è incluso nella licenza relativa all'applicazione</span><span class="sxs-lookup"><span data-stu-id="def79-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="def79-116">Controllare se un utente è assegnato all'applicazione</span><span class="sxs-lookup"><span data-stu-id="def79-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="def79-117">Per controllare se un utente è assegnato all'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="def79-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="def79-118">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="def79-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="def79-119">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="def79-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="def79-120">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="def79-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="def79-121">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="def79-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="def79-122">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="def79-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="def79-123">**Cercare** il nome dell'applicazione in questione.</span><span class="sxs-lookup"><span data-stu-id="def79-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="def79-124">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="def79-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="def79-125">Controllare se un utente è assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="def79-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="def79-126">Se si vuole rimuovere l'utente dall'applicazione, **fare clic sulla riga** dell'utente e selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="def79-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="def79-127">Controllare se un utente è incluso nella licenza relativa all'applicazione</span><span class="sxs-lookup"><span data-stu-id="def79-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="def79-128">Per controllare le licenze assegnate a un utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="def79-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="def79-129">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="def79-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="def79-130">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="def79-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="def79-131">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="def79-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="def79-132">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="def79-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="def79-133">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="def79-133">click **All users**.</span></span>

6.  <span data-ttu-id="def79-134">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="def79-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="def79-135">Fare clic su **Licenze** per verificare quali licenze sono assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="def79-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="def79-136">Se l'utente è assegnato a una licenza Office, ciò abilita le applicazioni Office di prima entità ad essere visualizzate nel pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="def79-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="def79-137">Problemi relativi all'assegnazione di applicazioni a gruppi</span><span class="sxs-lookup"><span data-stu-id="def79-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="def79-138">Un utente può visualizzare un'applicazione nel pannello di accesso perché è membro di un gruppo assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="def79-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="def79-139">Alcune procedure per verificare questa situazione sono elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="def79-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="def79-140">Controllare le appartenenze a gruppi dell'utente </span><span class="sxs-lookup"><span data-stu-id="def79-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="def79-141">Controllare se un utente è membro di un gruppo assegnato a una licenza</span><span class="sxs-lookup"><span data-stu-id="def79-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="def79-142">Controllare le appartenenze a gruppi dell'utente</span><span class="sxs-lookup"><span data-stu-id="def79-142">Check a user’s group memberships</span></span>

<span data-ttu-id="def79-143">Per controllare l'appartenenza a un gruppo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="def79-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="def79-144">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="def79-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="def79-145">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="def79-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="def79-146">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="def79-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="def79-147">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="def79-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="def79-148">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="def79-148">click **All users**.</span></span>

6.  <span data-ttu-id="def79-149">**Ricercare** l'utente per cui si vuole verificare la licenza e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="def79-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="def79-150">Fare clic su **gruppi.**</span><span class="sxs-lookup"><span data-stu-id="def79-150">click **Groups.**</span></span>

8.  <span data-ttu-id="def79-151">Controllare se un utente è membro di un gruppo assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="def79-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="def79-152">Se si vuole rimuovere l'utente dal gruppo, **fare clic sulla riga** del gruppo e selezionare Elimina.</span><span class="sxs-lookup"><span data-stu-id="def79-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="def79-153">Controllare se un utente è membro di un gruppo assegnato a una licenza</span><span class="sxs-lookup"><span data-stu-id="def79-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="def79-154">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="def79-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="def79-155">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="def79-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="def79-156">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="def79-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="def79-157">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="def79-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="def79-158">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="def79-158">click **All users**.</span></span>

6.  <span data-ttu-id="def79-159">**Ricercare** l'utente per cui si vuole verificare la licenza e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="def79-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="def79-160">Fare clic su **gruppi.**</span><span class="sxs-lookup"><span data-stu-id="def79-160">click **Groups.**</span></span>

8.  <span data-ttu-id="def79-161">Fare clic sulla riga di un gruppo specifico.</span><span class="sxs-lookup"><span data-stu-id="def79-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="def79-162">Fare clic su **Licenze** per vedere le licenze assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="def79-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="def79-163">Se il gruppo è assegnato a una licenza Office, ciò potrebbe abilitare alcune applicazioni Office di prima entità ad essere visualizzate nel pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="def79-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="def79-164">Se questi passaggi di risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="def79-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="def79-165">aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="def79-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="def79-166">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="def79-166">Correlation error ID</span></span>

-   <span data-ttu-id="def79-167">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="def79-167">UPN (user email address)</span></span>

-   <span data-ttu-id="def79-168">ID tenant</span><span class="sxs-lookup"><span data-stu-id="def79-168">Tenant ID</span></span>

-   <span data-ttu-id="def79-169">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="def79-169">Browser type</span></span>

-   <span data-ttu-id="def79-170">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="def79-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="def79-171">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="def79-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="def79-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="def79-172">Next steps</span></span>
[<span data-ttu-id="def79-173">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="def79-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
