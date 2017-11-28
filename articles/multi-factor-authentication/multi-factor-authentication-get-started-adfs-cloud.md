---
title: risorse del cloud con Azure MFA e AD FS aaaSecure | Documenti Microsoft
description: "Si tratta hello Azure multi-Factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA e AD FS in cloud hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="489b8-103">Protezione delle risorse cloud con Azure Multi-Factor Authentication e AD FS</span><span class="sxs-lookup"><span data-stu-id="489b8-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="489b8-104">Se l'organizzazione è federata con Azure Active Directory, usare Azure multi-Factor Authentication o Active Directory Federation Services (ADFS) toosecure risorse che hanno effettuato l'accesso AD Azure.</span><span class="sxs-lookup"><span data-stu-id="489b8-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="489b8-105">Utilizzare hello seguendo le risorse di Azure Active Directory toosecure procedure con Azure multi-Factor Authentication o Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="489b8-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="489b8-106">Proteggere le risorse Azure AD con ADFS</span><span class="sxs-lookup"><span data-stu-id="489b8-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="489b8-107">toosecure la risorsa cloud, impostare una regola attestazioni, in modo che Active Directory Federation Services genera hello multipleauthn attestazione quando un utente esegue la verifica completata.</span><span class="sxs-lookup"><span data-stu-id="489b8-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="489b8-108">Questa attestazione viene passata in tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="489b8-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="489b8-109">Seguire questa procedura toowalk passaggi hello:</span><span class="sxs-lookup"><span data-stu-id="489b8-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="489b8-110">Aprire il componente di gestione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="489b8-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="489b8-111">A sinistra di hello, selezionare **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="489b8-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="489b8-112">Fare clic con il pulsante destro del mouse su **Piattaforma delle identità di Microsoft Office 365** e selezionare **Modifica regole attestazione**.</span><span class="sxs-lookup"><span data-stu-id="489b8-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="489b8-114">In Regole di trasformazione rilascio fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="489b8-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="489b8-116">In aggiunta guidata regole attestazione trasformare hello, selezionare **Pass Through or Filter an Incoming Claim** hello elenco a discesa e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="489b8-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="489b8-118">Assegnare un nome alla regola.</span><span class="sxs-lookup"><span data-stu-id="489b8-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="489b8-119">Selezionare **riferimenti dei metodi di autenticazione** come hello in arrivo tipo di attestazione.</span><span class="sxs-lookup"><span data-stu-id="489b8-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="489b8-120">Selezionare **Pass-through di tutti i valori attestazione**.</span><span class="sxs-lookup"><span data-stu-id="489b8-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="489b8-121">![Aggiunta guidata regole attestazione di trasformazione](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="489b8-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="489b8-122">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="489b8-122">Click **Finish**.</span></span> <span data-ttu-id="489b8-123">Chiudere la console di gestione di ADFS hello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="489b8-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="489b8-124">Indirizzi IP attendibili per utenti federati</span><span class="sxs-lookup"><span data-stu-id="489b8-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="489b8-125">Indirizzi IP attendibili consente agli amministratori di verifica in due passaggi di tooby passare per gli indirizzi IP specifici o per gli utenti federati con richieste provenienti dalla propria rete intranet.</span><span class="sxs-lookup"><span data-stu-id="489b8-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="489b8-126">Hello nelle sezioni seguenti descrivono come tooconfigure Azure multi-Factor Authentication attendibili gli indirizzi IP con gli utenti federati e verifica in due passaggi di elementi da ignorare quando una richiesta proviene da una rete intranet gli utenti federati.</span><span class="sxs-lookup"><span data-stu-id="489b8-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="489b8-127">Questo risultato viene ottenuto mediante la configurazione di ADFS toouse pass-through o filtro di un modello di attestazione in ingresso con hello il tipo di attestazione all'interno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="489b8-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="489b8-128">Questo esempio usa Office 365 per l'attendibilità del componente.</span><span class="sxs-lookup"><span data-stu-id="489b8-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="489b8-129">Configurare le regole delle attestazioni ADFS hello</span><span class="sxs-lookup"><span data-stu-id="489b8-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="489b8-130">Hello è necessario innanzitutto toodo è tooconfigure hello ADFS attestazioni.</span><span class="sxs-lookup"><span data-stu-id="489b8-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="489b8-131">Creare due regole attestazioni, uno per hello all'interno della rete aziendale attestazione di tipo e un'altra per mantenere gli utenti connessi.</span><span class="sxs-lookup"><span data-stu-id="489b8-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="489b8-132">Aprire il componente di gestione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="489b8-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="489b8-133">A sinistra di hello, selezionare **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="489b8-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="489b8-134">Fare clic con il pulsante destro del mouse su **Piattaforma delle identità di Microsoft Office 365** e selezionare **Modifica regole attestazione...**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="489b8-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="489b8-135">In Regole di trasformazione rilascio fare clic su **Aggiungi regola.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="489b8-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="489b8-136">In aggiunta guidata regole attestazione trasformare hello, selezionare **Pass Through or Filter an Incoming Claim** hello elenco a discesa e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="489b8-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="489b8-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="489b8-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="489b8-138">In hello casella tooClaim regola nome successivo, assegnare alla regola un nome.</span><span class="sxs-lookup"><span data-stu-id="489b8-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="489b8-139">Ad esempio: InternoReteAziend.</span><span class="sxs-lookup"><span data-stu-id="489b8-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="489b8-140">Dall'elenco a discesa hello, tipo di attestazione tooIncoming successivo, selezionare **all'interno della rete aziendale**.</span><span class="sxs-lookup"><span data-stu-id="489b8-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="489b8-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="489b8-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="489b8-142">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="489b8-142">Click **Finish**.</span></span>
9. <span data-ttu-id="489b8-143">In Regole di trasformazione rilascio fare clic su **Aggiungi regola**.</span><span class="sxs-lookup"><span data-stu-id="489b8-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="489b8-144">In aggiunta guidata regole attestazione trasformare hello, selezionare **inviare attestazioni mediante una regola personalizzata** hello elenco a discesa e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="489b8-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="489b8-145">Nella casella hello sotto Nome regola attestazione: immettere *Keep Users Signed In*.</span><span class="sxs-lookup"><span data-stu-id="489b8-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="489b8-146">Nella casella regola personalizzata di hello, immettere:</span><span class="sxs-lookup"><span data-stu-id="489b8-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="489b8-148">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="489b8-148">Click **Finish**.</span></span>
14. <span data-ttu-id="489b8-149">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="489b8-149">Click **Apply**.</span></span>
15. <span data-ttu-id="489b8-150">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="489b8-150">Click **Ok**.</span></span>
16. <span data-ttu-id="489b8-151">Chiudere Gestione ADFS.</span><span class="sxs-lookup"><span data-stu-id="489b8-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="489b8-152">Configurare gli indirizzi IP attendibili di Azure Multi-Factor Authentication con utenti federati</span><span class="sxs-lookup"><span data-stu-id="489b8-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="489b8-153">Ora che le attestazioni hello sono presenti, è possibile configurare indirizzi IP attendibili.</span><span class="sxs-lookup"><span data-stu-id="489b8-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="489b8-154">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="489b8-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="489b8-155">A sinistra di hello, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="489b8-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="489b8-156">Nella Directory, selezionare la directory di hello in cui si desidera tooset di indirizzi IP attendibili.</span><span class="sxs-lookup"><span data-stu-id="489b8-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="489b8-157">Nella Directory selezionata hello, fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="489b8-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="489b8-158">Nella sezione di hello multi-factor authentication, fare clic su **Gestisci impostazioni servizio**.</span><span class="sxs-lookup"><span data-stu-id="489b8-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="489b8-159">Nella pagina Impostazioni servizio hello in indirizzi IP attendibili, selezionare **ignorare multi-factor-autenticazione per le richieste dagli utenti federati nella intranet**.</span><span class="sxs-lookup"><span data-stu-id="489b8-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="489b8-161">Fare clic su **save**.</span><span class="sxs-lookup"><span data-stu-id="489b8-161">Click **save**.</span></span>
8. <span data-ttu-id="489b8-162">Una volta applicati gli aggiornamenti di hello, fare clic su **chiudere**.</span><span class="sxs-lookup"><span data-stu-id="489b8-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="489b8-163">La procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="489b8-163">That’s it!</span></span> <span data-ttu-id="489b8-164">A questo punto, gli utenti federati di Office 365 dovrebbero rimanere solo toouse MFA quando un'attestazione proviene dalla rete intranet aziendale di hello esterno.</span><span class="sxs-lookup"><span data-stu-id="489b8-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
