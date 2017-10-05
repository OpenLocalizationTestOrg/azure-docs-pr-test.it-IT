---
title: 'Azure AD Connect: autenticazione pass-through - Blocco smart | Microsoft Docs'
description: Questo articolo descrive come l'autenticazione pass-through di Azure Active Directory (Azure AD) consente di proteggere gli account locali da attacchi di forza bruta alla password nel cloud.
services: active-directory
keywords: Autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="07908-104">Autenticazione pass-through di Azure Active Directory: blocco smart</span><span class="sxs-lookup"><span data-stu-id="07908-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="07908-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="07908-105">Overview</span></span>

<span data-ttu-id="07908-106">Azure AD consente di proteggersi dagli attacchi di forza bruta alle password e impedisce il blocco delle applicazioni Office 365 e SaaS degli utenti originali.</span><span class="sxs-lookup"><span data-stu-id="07908-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="07908-107">Questa funzionalità, denominata **blocco smart**, è supportata quando si usa l'autenticazione pass-through come metodo di accesso.</span><span class="sxs-lookup"><span data-stu-id="07908-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="07908-108">Il blocco smart è abilitato per impostazione predefinita per tutti i tenant e protegge costantemente gli account utente. Non è necessario attivarlo.</span><span class="sxs-lookup"><span data-stu-id="07908-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="07908-109">Il blocco smart tiene traccia dei tentativi di accesso non riusciti e dopo una determinata **soglia di blocco**, avvia la **durata del blocco**.</span><span class="sxs-lookup"><span data-stu-id="07908-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="07908-110">Eventuali tentativi di accesso da un utente malintenzionato durante la durata del blocco vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="07908-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="07908-111">Se l'attacco continua, i tentativi successivi di accesso al termine della durata del blocco non riescono e la durata del blocco viene prolungata.</span><span class="sxs-lookup"><span data-stu-id="07908-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="07908-112">Il valore predefinito della Soglia di blocco è 10 tentativi non riusciti, mentre la Durata del blocco predefinita è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="07908-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="07908-113">Il blocco smart consente di distinguere anche tra l'accesso effettuato da utenti originali e da utenti malintenzionati e nella maggior parte dei casi blocca solo gli utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="07908-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="07908-114">Questa funzionalità impedisce agli utenti malintenzionati di bloccare gli utenti veri.</span><span class="sxs-lookup"><span data-stu-id="07908-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="07908-115">Per distinguere tra utenti malintenzionati e utenti veri vengono analizzati il comportamento di accesso, i dispositivi e i browser degli utenti oltre ad altri segnali.</span><span class="sxs-lookup"><span data-stu-id="07908-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="07908-116">Gli algoritmi vengono migliorati costantemente.</span><span class="sxs-lookup"><span data-stu-id="07908-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="07908-117">Poiché l'autenticazione pass-through inoltra le richieste di convalida della password in Active Directory (AD) locale, è necessario impedire ai pirati informatici di bloccare gli account di AD degli utenti.</span><span class="sxs-lookup"><span data-stu-id="07908-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="07908-118">Poiché l'utente dispone di propri criteri di blocco degli account di AD, in particolare [**Soglia di blocchi dell'account**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [ **	Reimposta blocco account dopo**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx), è necessario configurare in modo appropriato i valori di durata del blocco e la soglia di blocco di Azure AD per filtrare gli attacchi nel cloud, prima che raggiungano AD locale.</span><span class="sxs-lookup"><span data-stu-id="07908-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="07908-119">La funzionalità Smart Lockout è gratuita e _attiva_ per impostazione predefinita per tutti i clienti.</span><span class="sxs-lookup"><span data-stu-id="07908-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="07908-120">Tuttavia, per modificare i valori relativi alla soglia di blocco e alla durata del blocco di Azure AD usando l'API Graph, è necessario che il tenant abbia almeno una licenza di Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="07908-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="07908-121">Non è necessaria una licenza di Azure AD Premium P2 _per ogni utente_ per ottenere la funzionalità Smart Lockout con l'autenticazione pass-through.</span><span class="sxs-lookup"><span data-stu-id="07908-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="07908-122">Per garantire che gli account di AD locali degli utenti siano protetti, è necessario assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="07908-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="07908-123">La Soglia di blocco di Azure AD sia _inferiore_ alla soglia di blocco dell'account di AD.</span><span class="sxs-lookup"><span data-stu-id="07908-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="07908-124">È consigliabile impostare i valori in modo che è la soglia di blocco dell'account di AD sia almeno di due o tre volte superiore alla soglia di blocco di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07908-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="07908-125">La durata del blocco di Azure AD, rappresentata in secondi, è _maggiore_ rispetto al valore di Reimposta blocco account dopo di AD, rappresentato in minuti.</span><span class="sxs-lookup"><span data-stu-id="07908-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="07908-126">Verificare i criteri di blocco degli account di AD</span><span class="sxs-lookup"><span data-stu-id="07908-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="07908-127">Usare le istruzioni seguenti per verificare i criteri di blocco degli account di AD:</span><span class="sxs-lookup"><span data-stu-id="07908-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="07908-128">Aprire lo strumento Gestione criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="07908-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="07908-129">Modificare i criteri di gruppo applicati a tutti gli utenti, ad esempio il Criterio dominio predefinito.</span><span class="sxs-lookup"><span data-stu-id="07908-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="07908-130">Passare a Configurazione computer\Criteri\Impostazioni di Windows\Impostazioni di sicurezza\Criteri account\Criterio di blocco account.</span><span class="sxs-lookup"><span data-stu-id="07908-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="07908-131">Verificare i valori di Soglia di blocchi dell'account e Reimposta blocco account dopo.</span><span class="sxs-lookup"><span data-stu-id="07908-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Criteri di blocco degli account di AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="07908-133">Usare l'API Graph per gestire i valori di blocco smart del tenant</span><span class="sxs-lookup"><span data-stu-id="07908-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="07908-134">La modifica dei valori relativi alla soglia di blocco e alla durata del blocco di Azure AD tramite l'API Graph di Azure AD sono funzionalità di Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="07908-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="07908-135">L'utente deve anche essere Amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="07908-136">È possibile usare [Graph explorer](https://developer.microsoft.com/graph/graph-explorer) per leggere, impostare e aggiornare i valori di blocco smart per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07908-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="07908-137">Ma è anche possibile eseguire queste operazioni a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="07908-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="07908-138">Leggere i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="07908-138">Read Smart Lockout values</span></span>

<span data-ttu-id="07908-139">Seguire questa procedura per leggere i valori di blocco smart del tenant:</span><span class="sxs-lookup"><span data-stu-id="07908-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="07908-140">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="07908-141">Se richiesto, concedere l'accesso per le autorizzazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="07908-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="07908-142">Fare clic su "Autorizzazioni di modifica" e selezionare l'autorizzazione "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="07908-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="07908-143">Configurare la richiesta dell'API Graph nel modo seguente: impostare la versione su "BETA", il tipo di richiesta su "GET" e l'URL su `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="07908-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="07908-144">Fare clic su "Esegui query" per visualizzare i valori di blocco smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="07908-145">Se i valori del tenant non sono stati mai impostati, viene visualizzato un insieme vuoto.</span><span class="sxs-lookup"><span data-stu-id="07908-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="07908-146">Impostare i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="07908-146">Set Smart Lockout values</span></span>

<span data-ttu-id="07908-147">Attenersi alla procedura seguente per impostare i valori di blocco smart del tenant. Eseguire questa procedura solo la prima volta.</span><span class="sxs-lookup"><span data-stu-id="07908-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="07908-148">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="07908-149">Se richiesto, concedere l'accesso per le autorizzazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="07908-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="07908-150">Fare clic su "Autorizzazioni di modifica" e selezionare l'autorizzazione "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="07908-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="07908-151">Configurare la richiesta dell'API Graph nel modo seguente: impostare la versione su "BETA", il tipo di richiesta su "POST" e l'URL su `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="07908-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="07908-152">Copiare e incollare la richiesta JSON seguente nel campo "Corpo della richiesta".</span><span class="sxs-lookup"><span data-stu-id="07908-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="07908-153">Modificare i valori di blocco smart in base alle necessità e usare un GUID casuale per `templateId`.</span><span class="sxs-lookup"><span data-stu-id="07908-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="07908-154">Fare clic su "Esegui query" per impostare i valori di blocco smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="07908-155">Se l'utente non li sta usando, è possibile lasciare i valori di **BannedPasswordList** e **EnableBannedPasswordCheck** i vuoto ("") e "false" rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="07908-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="07908-156">Verificare di aver impostato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="07908-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="07908-157">Aggiornare i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="07908-157">Update Smart Lockout values</span></span>

<span data-ttu-id="07908-158">Seguire questa procedura per aggiornare i valori di blocco smart del tenant, se questi sono già stati impostati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="07908-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="07908-159">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="07908-160">Se richiesto, concedere l'accesso per le autorizzazioni richieste.</span><span class="sxs-lookup"><span data-stu-id="07908-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="07908-161">Fare clic su "Autorizzazioni di modifica" e selezionare l'autorizzazione "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="07908-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="07908-162">[Seguire questa procedura per leggere i valori di blocco smart del tenant](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="07908-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="07908-163">Copia il valore `id` , ovvero un GUID dell'elemento con "displayName" come "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="07908-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="07908-164">Configurare la richiesta dell'API Graph nel modo seguente: impostare la versione su "BETA", il tipo di richiesta su "PATCH" e l'URL su `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>`. Usare il GUID dal passaggio 3 per `<id>`.</span><span class="sxs-lookup"><span data-stu-id="07908-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="07908-165">Copiare e incollare la richiesta JSON seguente nel campo "Corpo della richiesta".</span><span class="sxs-lookup"><span data-stu-id="07908-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="07908-166">Modificare i valori di blocco smart in base alle necessità.</span><span class="sxs-lookup"><span data-stu-id="07908-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="07908-167">Fare clic su "Esegui query" per aggiornare i valori di blocco smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="07908-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="07908-168">Verificare di aver aggiornato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="07908-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07908-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07908-169">Next steps</span></span>
- <span data-ttu-id="07908-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07908-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
