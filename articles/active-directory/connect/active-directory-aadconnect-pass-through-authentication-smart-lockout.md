---
title: 'Azure AD Connect: autenticazione pass-through - Blocco smart | Microsoft Docs'
description: In questo articolo viene descritto come l'autenticazione pass-through di Azure Active Directory (Azure AD) consente di proteggere gli account locali da attacchi di forza bruta password nel cloud hello.
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
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="01f72-104">Autenticazione pass-through di Azure Active Directory: blocco smart</span><span class="sxs-lookup"><span data-stu-id="01f72-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="01f72-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="01f72-105">Overview</span></span>

<span data-ttu-id="01f72-106">Azure AD consente di proteggersi dagli attacchi di forza bruta alle password e impedisce il blocco delle applicazioni Office 365 e SaaS degli utenti originali.</span><span class="sxs-lookup"><span data-stu-id="01f72-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="01f72-107">Questa funzionalità, denominata **blocco smart**, è supportata quando si usa l'autenticazione pass-through come metodo di accesso.</span><span class="sxs-lookup"><span data-stu-id="01f72-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="01f72-108">Blocco intelligente è abilitato per impostazione predefinita per tutti i tenant e proteggere tutti i tempi di hello; gli account utente non è alcuna necessità tooturn sul.</span><span class="sxs-lookup"><span data-stu-id="01f72-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="01f72-109">Il blocco smart tiene traccia dei tentativi di accesso non riusciti e dopo una determinata **soglia di blocco**, avvia la **durata del blocco**.</span><span class="sxs-lookup"><span data-stu-id="01f72-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="01f72-110">Eventuali tentativi di accesso da attacchi di hello durante la durata del blocco hello vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="01f72-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="01f72-111">Se l'attacco hello continua, hello successivi tentativi di accesso scadenza hello durata del blocco del risultato in più intervalli di blocco.</span><span class="sxs-lookup"><span data-stu-id="01f72-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="01f72-112">Hello valore predefinito di soglia di blocco è 10 tentativi non riusciti e default hello che durata del blocco è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="01f72-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="01f72-113">Blocco smart anche distingue tra l'accesso degli utenti originali e da utenti malintenzionati e solo i blocchi out gli utenti malintenzionati hello nella maggior parte dei casi.</span><span class="sxs-lookup"><span data-stu-id="01f72-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="01f72-114">Questa funzionalità impedisce agli utenti malintenzionati di bloccare gli utenti veri.</span><span class="sxs-lookup"><span data-stu-id="01f72-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="01f72-115">Utilizziamo Accedi il comportamento passato, i dispositivi degli utenti & browser e altre toodistinguish segnali tra originali e utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="01f72-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="01f72-116">Gli algoritmi vengono migliorati costantemente.</span><span class="sxs-lookup"><span data-stu-id="01f72-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="01f72-117">Poiché l'autenticazione pass-through inoltra le richieste di convalida di password in locale Active Directory (AD), è necessario ai pirati informatici tooprevent di blocco degli account di Active Directory degli utenti.</span><span class="sxs-lookup"><span data-stu-id="01f72-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="01f72-118">Poiché si dispone di propri criteri di blocco degli Account di Active Directory (in particolare, [ **soglia blocco Account** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [ **Reimposta Account blocco contatore dopo aver criteri** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), è necessario soglia di blocco tooconfigure Azure AD e blocca i valori in modo appropriato toofilter attacchi nel cloud hello prima che raggiungano locale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01f72-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="01f72-119">funzionalità di blocco Smart Hello è gratuita ed _su_ per impostazione predefinita per tutti i clienti.</span><span class="sxs-lookup"><span data-stu-id="01f72-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="01f72-120">Modifica di soglia di blocco e i valori di durata del blocco usando l'API Graph di Azure AD deve, tuttavia, la licenza di P2 Premium toohave Azure AD almeno un tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="01f72-121">Non occorre una licenza Azure AD Premium P2 _per ogni utente_ funzionalità di blocco Smart hello tooget con l'autenticazione pass-through.</span><span class="sxs-lookup"><span data-stu-id="01f72-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="01f72-122">tooensure che degli utenti AD account locali siano ben protetti, è necessario tooensure che:</span><span class="sxs-lookup"><span data-stu-id="01f72-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="01f72-123">La Soglia di blocco di Azure AD sia _inferiore_ alla soglia di blocco dell'account di AD.</span><span class="sxs-lookup"><span data-stu-id="01f72-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="01f72-124">È consigliabile impostare valori hello tale soglia blocco Account di Active Directory è almeno due o tre volte la soglia di blocco di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f72-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="01f72-125">La durata del blocco di Azure AD, rappresentata in secondi, è _maggiore_ rispetto al valore di Reimposta blocco account dopo di AD, rappresentato in minuti.</span><span class="sxs-lookup"><span data-stu-id="01f72-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="01f72-126">Verificare i criteri di blocco degli account di AD</span><span class="sxs-lookup"><span data-stu-id="01f72-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="01f72-127">Utilizzare hello seguendo le istruzioni tooverify i criteri di blocco degli Account di Active Directory:</span><span class="sxs-lookup"><span data-stu-id="01f72-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="01f72-128">Aprire lo strumento di gestione criteri di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="01f72-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="01f72-129">Modificare hello criteri di gruppo applicati tooall utenti, ad esempio, hello criterio dominio predefinito.</span><span class="sxs-lookup"><span data-stu-id="01f72-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="01f72-130">Passare tooComputer Configurazione computer\Criteri\Impostazioni di Windows\Impostazioni protezione\Criteri account\Criterio blocco criteri.</span><span class="sxs-lookup"><span data-stu-id="01f72-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="01f72-131">Verificare i valori di Soglia di blocchi dell'account e Reimposta blocco account dopo.</span><span class="sxs-lookup"><span data-stu-id="01f72-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Criteri di blocco degli account di AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="01f72-133">Utilizzare hello API Graph toomanage valori blocco Smart del tenant</span><span class="sxs-lookup"><span data-stu-id="01f72-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="01f72-134">La modifica dei valori relativi alla soglia di blocco e alla durata del blocco di Azure AD tramite l'API Graph di Azure AD sono funzionalità di Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="01f72-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="01f72-135">Richiede inoltre toobe un amministratore globale per il tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="01f72-136">È possibile utilizzare [Esplora grafico](https://developer.microsoft.com/graph/graph-explorer) tooread, impostare e aggiornare i valori di blocco Smart di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f72-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="01f72-137">Ma è anche possibile eseguire queste operazioni a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="01f72-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="01f72-138">Leggere i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="01f72-138">Read Smart Lockout values</span></span>

<span data-ttu-id="01f72-139">Seguire questi tooread passaggi valori blocco Smart del tenant:</span><span class="sxs-lookup"><span data-stu-id="01f72-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="01f72-140">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="01f72-141">Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="01f72-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="01f72-142">Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".</span><span class="sxs-lookup"><span data-stu-id="01f72-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="01f72-143">Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "GET" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="01f72-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="01f72-144">Fare clic su "Esegui Query" toosee valori blocco Smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="01f72-145">Se i valori del tenant non sono stati mai impostati, viene visualizzato un insieme vuoto.</span><span class="sxs-lookup"><span data-stu-id="01f72-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="01f72-146">Impostare i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="01f72-146">Set Smart Lockout values</span></span>

<span data-ttu-id="01f72-147">Seguire questi tooset passaggi valori blocco Smart del tenant (per hello solo la prima volta):</span><span class="sxs-lookup"><span data-stu-id="01f72-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="01f72-148">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="01f72-149">Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="01f72-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="01f72-150">Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".</span><span class="sxs-lookup"><span data-stu-id="01f72-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="01f72-151">Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "POST" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="01f72-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="01f72-152">Copiare e incollare hello seguente richiesta JSON nel campo "Corpo della richiesta" hello.</span><span class="sxs-lookup"><span data-stu-id="01f72-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="01f72-153">Modificare valori blocco Smart hello in modo appropriato e usare un GUID casuale per `templateId`.</span><span class="sxs-lookup"><span data-stu-id="01f72-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="01f72-154">Fare clic su "Esegui Query" tooset valori blocco Smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="01f72-155">Se non vengono utilizzati, è possibile lasciare hello **BannedPasswordList** e **EnableBannedPasswordCheck** i valori come vuoto ("") e "false" rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="01f72-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="01f72-156">Verificare di aver impostato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="01f72-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="01f72-157">Aggiornare i valori di blocco smart</span><span class="sxs-lookup"><span data-stu-id="01f72-157">Update Smart Lockout values</span></span>

<span data-ttu-id="01f72-158">Seguire questi tooupdate passaggi valori blocco Smart del tenant (se è già stato impostato in precedenza):</span><span class="sxs-lookup"><span data-stu-id="01f72-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="01f72-159">Accedere a Graph explorer come amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="01f72-160">Se richiesto, concedere l'accesso per hello richiesta delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="01f72-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="01f72-161">Selezionare l'autorizzazione "Directory.ReadWrite.All" hello "Autorizzazioni di modifica".</span><span class="sxs-lookup"><span data-stu-id="01f72-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="01f72-162">[Seguire questi tooread passaggi valori blocco Smart del tenant](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="01f72-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="01f72-163">Hello copia `id` valore (GUID) dell'elemento hello con "displayName" come "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="01f72-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="01f72-164">Configurare richiesta all'API Graph hello come segue: Set versione troppo "BETA", tipo di richiesta troppo "PATCH" e l'URL troppo`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -utilizzare hello GUID dal passaggio 3 per `<id>`.</span><span class="sxs-lookup"><span data-stu-id="01f72-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="01f72-165">Copiare e incollare hello seguente richiesta JSON nel campo "Corpo della richiesta" hello.</span><span class="sxs-lookup"><span data-stu-id="01f72-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="01f72-166">Modificare i valori di blocco Smart hello come appropriato.</span><span class="sxs-lookup"><span data-stu-id="01f72-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="01f72-167">Fare clic su "Esegui Query" tooupdate valori blocco Smart del tenant.</span><span class="sxs-lookup"><span data-stu-id="01f72-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="01f72-168">Verificare di aver aggiornato i valori di blocco smart del tenant correttamente tramite [questa procedura](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="01f72-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f72-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01f72-169">Next steps</span></span>
- <span data-ttu-id="01f72-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="01f72-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
