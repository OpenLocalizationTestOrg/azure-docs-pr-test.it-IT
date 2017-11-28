---
title: "aaaAzure AD connettersi più domini"
description: "Questo documento descrive l'impostazione e la configurazione di più domini di primo livello con Office 365 e Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="2a9d1-103">Supporto di più domini per la federazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a9d1-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="2a9d1-104">Hello documentazione riportata di seguito vengono fornite indicazioni su come toouse più domini di primo livello e i sottodomini quando la federazione con Office 365 o Azure AD domini.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="2a9d1-105">Supporto di più domini di primo livello</span><span class="sxs-lookup"><span data-stu-id="2a9d1-105">Multiple top-level domain support</span></span>
<span data-ttu-id="2a9d1-106">Per la federazione di più domini di primo livello con Azure AD sono necessarie alcune operazioni di configurazione aggiuntive che non sono obbligatorie per la federazione con un dominio di primo livello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="2a9d1-107">Quando un dominio è federato con Azure AD, vengono impostate diverse proprietà dominio hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="2a9d1-108">Una proprietà importante è IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="2a9d1-109">Si tratta di un URI che viene usato in Azure AD tooidentify dominio hello hello token è associato.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="2a9d1-110">Hello URI non è necessario tooresolve tooanything ma deve essere un URI valido.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="2a9d1-111">Per impostazione predefinita, Azure AD questo valore viene impostato toohello dell'identificatore del servizio federativo hello in locale ADFS configurazione.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="2a9d1-112">Identificatore del servizio federativo Hello è un URI che identifica in modo univoco un servizio federativo.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="2a9d1-113">servizio federativo Hello è un'istanza di AD FS che funziona come servizio token di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="2a9d1-114">È possibile visualizzare IssuerUri usando il comando di PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="2a9d1-116">Si verifica un problema quando si desidera tooadd più di un dominio di primo livello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="2a9d1-117">Ad esempio, si supponga di avere configurato la federazione tra Azure AD e l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="2a9d1-118">Per questo documento si usa bmcontoso.com.  Viene quindi aggiunto un secondo dominio di primo livello, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domini](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="2a9d1-120">Quando si tenta di tooconvert nostri toobe dominio bmfabrikam.com federata, è visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="2a9d1-121">Hello questo accade, Azure AD con un vincolo che non consente hello hello toohave di proprietà IssuerUri stesso valore per più di un dominio.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Errore della federazione](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="2a9d1-123">Parametro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="2a9d1-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="2a9d1-124">tooworkaround, è necessario un IssuerUri diversi che possono essere eseguiti utilizzando hello tooadd `-SupportMultipleDomain` parametro.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="2a9d1-125">Questo parametro viene utilizzato con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="2a9d1-126">Questo parametro consente AD Azure configurare hello IssuerUri in modo che è basato su nome hello del dominio di hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="2a9d1-127">Questo valore sarà univoco nelle directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="2a9d1-128">Utilizzando il parametro hello consente hello PowerShell comando toocomplete correttamente.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="2a9d1-130">Esaminano impostazioni hello del nuovo dominio bmfabrikam.com si può vedere seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="2a9d1-132">Si noti che `-SupportMultipleDomain` invariato di hello altri endpoint che sono ancora configurate servizio federativo di toopoint tooour nella adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="2a9d1-133">Un altro aspetto che `-SupportMultipleDomain` does che assicura che sistema di hello AD FS include il valore dell'autorità di certificazione corretta di hello nel token rilasciato per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="2a9d1-134">A tale scopo eseguire parte di utenti hello UPN di dominio hello e questa impostazione come dominio hello in hello IssuerUri, vale a dire https://{upn suffisso} / adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="2a9d1-135">In questo modo durante l'autenticazione tooAzure AD o Office 365, hello IssuerUri elemento token dell'utente hello è dominio hello toolocate usato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="2a9d1-136">Se non è possibile trovare una corrispondenza hello autenticazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="2a9d1-137">Ad esempio, se un utente UPN è bsimon@bmcontoso.com, elemento IssuerUri hello in problemi relativi AD ADFS token hello imposterà toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="2a9d1-138">La configurazione di Azure AD hello verrà trovata corrispondenza e l'autenticazione avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="2a9d1-139">di seguito Hello è regola attestazione personalizzata hello che implementa questa logica:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="2a9d1-140">In ordine toouse hello - SupportMultipleDomain passare quando si tenta di nuovo tooadd o convertire già aggiunti domini, è necessario toohave toosupport la relazione di trust federativa del programma di installazione li originariamente.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="2a9d1-141">Come tooupdate hello trust tra ADFS e Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a9d1-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="2a9d1-142">Se hello federata trust tra ADFS e l'istanza di Azure AD non è stata configurata, potrebbe essere necessario toore-creare il trust.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="2a9d1-143">Questo avviene perché, quando è originariamente il programma di installazione senza hello `-SupportMultipleDomain` parametro hello IssuerUri è impostato con il valore predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="2a9d1-144">In hello schermata seguente è possibile visualizzare hello IssuerUri impostata toohttps://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="2a9d1-145">In questo momento, se è stato aggiunto correttamente un nuovo dominio nel portale di Azure AD hello e quindi tentare tooconvert utilizzando `Convert-MsolDomaintoFederated -DomainName <your domain>`, si ottiene hello errore seguente.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="2a9d1-147">Se si tenta di hello tooadd `-SupportMultipleDomain` commutatore verranno inviati hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="2a9d1-149">Durante il tentativo semplicemente toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` su hello dominio originale inoltre genererà un errore.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="2a9d1-151">Attenersi alla procedura hello sotto tooadd un dominio di primo livello aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="2a9d1-152">Se si dispone già aggiunto un dominio e non è stata utilizzata hello `-SupportMultipleDomain` parametro start con passaggi hello per eliminare e aggiornare il dominio originale.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="2a9d1-153">Se non è stato aggiunto un dominio di primo livello ancora è possibile iniziare con la procedura di hello per aggiungere un dominio con PowerShell di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="2a9d1-154">Utilizzare hello seguendo i passaggi tooremove hello Microsoft Online trust e aggiornare il dominio originale.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="2a9d1-155">Nel server federativo di AD FS aprire **Gestione AD FS**</span><span class="sxs-lookup"><span data-stu-id="2a9d1-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="2a9d1-156">A sinistra di hello, espandere **relazioni di Trust** e **Relying Party Trusts**</span><span class="sxs-lookup"><span data-stu-id="2a9d1-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="2a9d1-157">In hello destra, l'eliminazione di hello **piattaforma delle identità di Microsoft Office 365** voce.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="2a9d1-158">![Rimozione di Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="2a9d1-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="2a9d1-159">In un computer dotato di [modulo di Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installato eseguire hello seguente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="2a9d1-160">Immettere hello username e password di un amministratore globale per il dominio di Azure AD hello che con federazione</span><span class="sxs-lookup"><span data-stu-id="2a9d1-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="2a9d1-161">In PowerShell immettere `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="2a9d1-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="2a9d1-162">In PowerShell immettere `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="2a9d1-163">Si tratta di dominio originale hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-163">This is for hello original domain.</span></span>  <span data-ttu-id="2a9d1-164">Quindi l'uso di hello precedente domini che sarebbe:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="2a9d1-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="2a9d1-165">Utilizzare hello seguendo i passaggi tooadd hello nuovo dominio di primo livello con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a9d1-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="2a9d1-166">In un computer dotato di [modulo di Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installato eseguire hello seguente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="2a9d1-167">Immettere hello username e password di un amministratore globale per il dominio di Azure AD hello che con federazione</span><span class="sxs-lookup"><span data-stu-id="2a9d1-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="2a9d1-168">In PowerShell immettere `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="2a9d1-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="2a9d1-169">In PowerShell immettere `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="2a9d1-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="2a9d1-170">Utilizzare hello seguendo i passaggi tooadd hello nuovo dominio di primo livello con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="2a9d1-171">Avvio di Azure AD Connect, da desktop hello o menu start</span><span class="sxs-lookup"><span data-stu-id="2a9d1-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="2a9d1-172">Scegliere "Aggiunta di un altro dominio di Azure AD" ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="2a9d1-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="2a9d1-173">Immettere le credenziali di Azure AD e Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="2a9d1-174">Selezionare il dominio di secondo hello desiderato tooconfigure per la federazione.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="2a9d1-175">![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="2a9d1-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="2a9d1-176">Fare clic su Installa.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="2a9d1-177">Verificare il dominio di primo livello nuovo hello</span><span class="sxs-lookup"><span data-stu-id="2a9d1-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="2a9d1-178">Tramite il comando di PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`è possibile visualizzare hello aggiornato IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="2a9d1-179">Hello schermata riportata di seguito viene illustrato l'aggiornamento delle impostazioni di federazione hello nel nostro http://bmcontoso.com/adfs/services/trust dominio originale</span><span class="sxs-lookup"><span data-stu-id="2a9d1-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="2a9d1-181">E hello IssuerUri nel nuovo dominio è stato impostato toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="2a9d1-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="2a9d1-183">Supporto per sottodomini</span><span class="sxs-lookup"><span data-stu-id="2a9d1-183">Support for Sub-domains</span></span>
<span data-ttu-id="2a9d1-184">Quando si aggiunge un sottodominio, a causa di hello modo Azure AD gestite domini, erediterà le impostazioni di hello del padre hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="2a9d1-185">Ciò significa che hello IssuerUri deve padri hello toomatch.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="2a9d1-186">Si supponga ad esempio che sia presente il dominio bmcontoso.com e che quindi si aggiunga corp.bmcontoso.com.  Ciò significa che hello IssuerUri per un utente da corp.bmcontoso.com necessario toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="2a9d1-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="2a9d1-187">Tuttavia la regola standard hello implementato sopra per Azure AD, verrà generato un token con un emittente come **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="2a9d1-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="2a9d1-188">valore obbligatorio del dominio hello che non corrispondono e l'autenticazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="2a9d1-189">La modalità di supporto tooenable per i sottodomini</span><span class="sxs-lookup"><span data-stu-id="2a9d1-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="2a9d1-190">In ordine toowork attorno a questa hello ADFS trust della relying party per Microsoft Online deve toobe aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="2a9d1-191">toodo, è necessario configurare una regola attestazioni personalizzata in modo che rimuove tutti i sottodomini dal suffisso UPN dell'utente hello durante la costruzione di valore dell'autorità di certificazione personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="2a9d1-192">Hello seguente attestazione eseguirà questo:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="2a9d1-193">ultimo numero di Hello nell'espressione regolare hello imposta hello il numero di domini padre è presente nel dominio radice.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="2a9d1-194">In bmcontoso.com sono necessari due domini padre.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="2a9d1-195">Se tre padre domini sono stati mantenuti toobe (ad esempio: corp.bmcontoso.com), quindi il numero di hello sarebbe stata tre.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="2a9d1-196">Eventualy un intervallo possono essere indicati, corrispondenza hello verrà sempre effettuato massimo hello toomatch dei domini.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="2a9d1-197">"{2,3}", verranno restituiti due domini toothree (ad esempio: bmfabrikam.com e corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="2a9d1-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="2a9d1-198">Questa procedura hello utilizzare tooadd un'attestazione personalizzata toosupport i sottodomini.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="2a9d1-199">Aprire Gestione AD FS.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-199">Open AD FS Management</span></span>
2. <span data-ttu-id="2a9d1-200">Fare clic con il pulsante destro trust relying Party Online Microsoft hello e scegliere regole attestazione di modifica</span><span class="sxs-lookup"><span data-stu-id="2a9d1-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="2a9d1-201">Selezionare una regola attestazioni terzo hello e sostituire ![richiesta di modifica](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="2a9d1-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="2a9d1-202">Sostituire attestazioni corrente hello:</span><span class="sxs-lookup"><span data-stu-id="2a9d1-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Sostituzione dell'attestazione](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="2a9d1-204">Fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-204">Click Ok.</span></span>  <span data-ttu-id="2a9d1-205">Fare clic su Applica.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-205">Click Apply.</span></span>  <span data-ttu-id="2a9d1-206">Fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-206">Click Ok.</span></span>  <span data-ttu-id="2a9d1-207">Chiudere Gestione ADFS.</span><span class="sxs-lookup"><span data-stu-id="2a9d1-207">Close AD FS Management.</span></span>

