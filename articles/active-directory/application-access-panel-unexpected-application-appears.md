---
title: le applicazioni aaaHow vengono visualizzate nel Pannello di accesso hello | Documenti Microsoft
description: "Risoluzione dei problemi perché un'applicazione viene visualizzato nel Pannello di accesso hello"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="fcda8-103">Modalità di visualizzazione di applicazioni nel Pannello di accesso hello</span><span class="sxs-lookup"><span data-stu-id="fcda8-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="fcda8-104">Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="fcda8-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="fcda8-105">Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="fcda8-106">può eseguire il provisioning salve hello applicazione toohello utente direttamente o tooa gruppo che un utente fa parte di risultante in un'applicazione hello visualizzati nel Pannello di accesso dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="fcda8-107">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="fcda8-107">General issues toocheck first</span></span>

-   <span data-ttu-id="fcda8-108">Se un'applicazione è stata rimossa solo da un utente o gruppo hello utente è membro di, riprovare toosign avanti e indietro nel Pannello di accesso dell'utente hello dopo pochi minuti toosee se un'applicazione hello viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="fcda8-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="fcda8-109">Se una licenza è stata rimossa solo da un utente o gruppo utente hello è che un membro di questo potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello per toobe le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="fcda8-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="fcda8-110">Consentire del tempo aggiuntivo prima della firma in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fcda8-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="fcda8-111">Problemi correlati tooassigning applicazioni toousers</span><span class="sxs-lookup"><span data-stu-id="fcda8-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="fcda8-112">Un utente può essere visualizzata un'applicazione nel proprio pannello di accesso perché che è stata precedentemente assegnate tooit.</span><span class="sxs-lookup"><span data-stu-id="fcda8-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="fcda8-113">Di seguito sono toocheck alcuni modi:</span><span class="sxs-lookup"><span data-stu-id="fcda8-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="fcda8-114">Verificare se un utente è assegnato toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="fcda8-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="fcda8-115">Controllare se un utente è in una licenza correlati toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="fcda8-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="fcda8-116">Verificare se un utente è assegnato toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="fcda8-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="fcda8-117">toocheck se un utente è assegnato toohello applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="fcda8-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="fcda8-118">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fcda8-119">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fcda8-120">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="fcda8-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fcda8-121">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fcda8-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fcda8-122">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="fcda8-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="fcda8-123">**Ricerca** per nome hello dell'applicazione hello in questione.</span><span class="sxs-lookup"><span data-stu-id="fcda8-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="fcda8-124">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="fcda8-125">Controllare toosee se l'utente è assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="fcda8-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="fcda8-126">Se si desidera tooremove hello utente da un'applicazione hello, **fare clic sulla riga hello** dell'utente hello e selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="fcda8-127">Controllare se un utente è in una licenza correlati toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="fcda8-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="fcda8-128">toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="fcda8-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="fcda8-129">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fcda8-130">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fcda8-131">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="fcda8-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fcda8-132">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="fcda8-133">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-133">click **All users**.</span></span>

6.  <span data-ttu-id="fcda8-134">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="fcda8-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="fcda8-135">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="fcda8-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="fcda8-136">Se utente hello viene assegnata una licenza di Office tooan tooappear applicazioni di Office di terze parti prima in questo modo su hello nel Pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fcda8-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="fcda8-137">Problemi correlati tooassigning applicazioni toogroups</span><span class="sxs-lookup"><span data-stu-id="fcda8-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="fcda8-138">Un utente potrebbe contenere un'applicazione nel proprio pannello di accesso perché fanno parte di un gruppo che dispone di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="fcda8-139">Di seguito sono toocheck alcuni modi:</span><span class="sxs-lookup"><span data-stu-id="fcda8-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="fcda8-140">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="fcda8-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="fcda8-141">Controllare se un utente è un membro di un gruppo dispone di licenza tooa</span><span class="sxs-lookup"><span data-stu-id="fcda8-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="fcda8-142">Controllare le appartenenze a gruppi dell'utente</span><span class="sxs-lookup"><span data-stu-id="fcda8-142">Check a user’s group memberships</span></span>

<span data-ttu-id="fcda8-143">toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="fcda8-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="fcda8-144">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fcda8-145">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fcda8-146">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="fcda8-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fcda8-147">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="fcda8-148">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-148">click **All users**.</span></span>

6.  <span data-ttu-id="fcda8-149">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="fcda8-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="fcda8-150">Fare clic su **gruppi.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-150">click **Groups.**</span></span>

8.  <span data-ttu-id="fcda8-151">Controllare toosee se l'utente fa parte di un'applicazione toohello gruppo assegnato.</span><span class="sxs-lookup"><span data-stu-id="fcda8-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="fcda8-152">Se si desidera tooremove hello utente dal gruppo di hello, **fare clic sulla riga hello** del gruppo di hello e seleziona Elimina.</span><span class="sxs-lookup"><span data-stu-id="fcda8-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="fcda8-153">Controllare se un utente è un membro di un gruppo dispone di licenza tooa</span><span class="sxs-lookup"><span data-stu-id="fcda8-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="fcda8-154">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fcda8-155">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fcda8-156">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="fcda8-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fcda8-157">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="fcda8-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="fcda8-158">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-158">click **All users**.</span></span>

6.  <span data-ttu-id="fcda8-159">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="fcda8-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="fcda8-160">Fare clic su **gruppi.**</span><span class="sxs-lookup"><span data-stu-id="fcda8-160">click **Groups.**</span></span>

8.  <span data-ttu-id="fcda8-161">Fare clic sulla riga hello di un gruppo specifico.</span><span class="sxs-lookup"><span data-stu-id="fcda8-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="fcda8-162">Fare clic su **licenze** toosee quale gruppo di licenze hello è assegnato tooit.</span><span class="sxs-lookup"><span data-stu-id="fcda8-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="fcda8-163">Se gruppo hello viene assegnata una licenza di Office tooan in che questo potrebbe rendere determinati tooappear applicazioni di Office di terze parti prima hello nel Pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fcda8-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="fcda8-164">Se questi passaggi di risoluzione dei problemi non hello di risolvere il problema di hello</span><span class="sxs-lookup"><span data-stu-id="fcda8-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="fcda8-165">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="fcda8-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="fcda8-166">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="fcda8-166">Correlation error ID</span></span>

-   <span data-ttu-id="fcda8-167">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="fcda8-167">UPN (user email address)</span></span>

-   <span data-ttu-id="fcda8-168">ID tenant</span><span class="sxs-lookup"><span data-stu-id="fcda8-168">Tenant ID</span></span>

-   <span data-ttu-id="fcda8-169">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="fcda8-169">Browser type</span></span>

-   <span data-ttu-id="fcda8-170">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="fcda8-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="fcda8-171">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="fcda8-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcda8-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fcda8-172">Next steps</span></span>
[<span data-ttu-id="fcda8-173">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcda8-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
