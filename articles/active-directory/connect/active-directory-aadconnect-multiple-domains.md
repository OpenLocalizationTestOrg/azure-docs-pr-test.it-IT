---
title: Domini multipli di Azure AD Connect
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="ac30a-103">Supporto di più domini per la federazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac30a-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="ac30a-104">La documentazione seguente fornisce indicazioni su come usare più domini di primo livello e sottodomini durante la federazione con domini di Office 365 o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac30a-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="ac30a-105">Supporto di più domini di primo livello</span><span class="sxs-lookup"><span data-stu-id="ac30a-105">Multiple top-level domain support</span></span>
<span data-ttu-id="ac30a-106">Per la federazione di più domini di primo livello con Azure AD sono necessarie alcune operazioni di configurazione aggiuntive che non sono obbligatorie per la federazione con un dominio di primo livello.</span><span class="sxs-lookup"><span data-stu-id="ac30a-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="ac30a-107">Quando un dominio è federato con Azure AD, alcune proprietà vengono impostate nel dominio in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac30a-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="ac30a-108">Una proprietà importante è IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="ac30a-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="ac30a-109">Si tratta di un URI usato da Azure AD per identificare il dominio a cui è associato il token.</span><span class="sxs-lookup"><span data-stu-id="ac30a-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="ac30a-110">Non è necessario che l'URI venga risolto, ma deve essere un URI valido.</span><span class="sxs-lookup"><span data-stu-id="ac30a-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="ac30a-111">Per impostazione predefinita, Azure AD lo imposta sul valore dell'identificatore del servizio federativo nella configurazione locale di AD FS.</span><span class="sxs-lookup"><span data-stu-id="ac30a-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="ac30a-112">L'identificatore del servizio federativo è un URI che identifica in modo univoco un servizio federativo.</span><span class="sxs-lookup"><span data-stu-id="ac30a-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="ac30a-113">Il servizio federativo è un'istanza di AD FS che funge da servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ac30a-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="ac30a-114">È possibile visualizzare IssuerUri usando il comando `Get-MsolDomainFederationSettings -DomainName <your domain>`di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac30a-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="ac30a-116">Si verifica un problema quando si vogliono aggiungere più domini di primo livello.</span><span class="sxs-lookup"><span data-stu-id="ac30a-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="ac30a-117">Ad esempio, si supponga di avere configurato la federazione tra Azure AD e l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="ac30a-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="ac30a-118">Per questo documento si usa bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ac30a-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="ac30a-119">Viene quindi aggiunto un secondo dominio di primo livello, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="ac30a-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domini](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="ac30a-121">Quando si prova a convertire il dominio bmfabrikam.com in modo che sia federato, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="ac30a-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="ac30a-122">La causa dell'errore è un vincolo di Azure AD che non consente alla proprietà IssuerUri di avere lo stesso valore per più di un dominio.</span><span class="sxs-lookup"><span data-stu-id="ac30a-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Errore della federazione](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="ac30a-124">Parametro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="ac30a-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="ac30a-125">Per risolvere il problema, è necessario aggiungere una proprietà IssuerUri diversa, usando il parametro `-SupportMultipleDomain` .</span><span class="sxs-lookup"><span data-stu-id="ac30a-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="ac30a-126">Questo parametro viene usato con i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac30a-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="ac30a-127">Questo parametro consente ad Azure AD di configurare IssuerUri in modo che sia basata sul nome del dominio.</span><span class="sxs-lookup"><span data-stu-id="ac30a-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="ac30a-128">Questo valore sarà univoco nelle directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac30a-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="ac30a-129">L'uso del parametro consente il completamento corretto del comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac30a-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="ac30a-131">Se si esaminano le impostazioni del nuovo dominio bmfabrikam.com, si può notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ac30a-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="ac30a-133">Si noti che `-SupportMultipleDomain` non modifica gli altri endpoint, che sono ancora configurati in modo da fare riferimento al servizio federativo su adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ac30a-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="ac30a-134">`-SupportMultipleDomain` consente anche di assicurare che il sistema AD FS includa il valore Issuer appropriato nei token emessi per Azure AD,</span><span class="sxs-lookup"><span data-stu-id="ac30a-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="ac30a-135">selezionando la porzione relativa al dominio del valore UPN degli utenti e impostandola come dominio in IssuerUri, ovvero https://{upn suffix}/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ac30a-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="ac30a-136">In questo modo durante l'autenticazione in Azure AD oppure Office 365 l'elemento IssuerUri nel token dell'utente viene usato per individuare il dominio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac30a-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="ac30a-137">Se non viene rilevata una corrispondenza, l'autenticazione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="ac30a-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="ac30a-138">Ad esempio, se un utente UPN è bsimon@bmcontoso.com, l'elemento IssuerUri i problemi di token AD FS verrà impostato su http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ac30a-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="ac30a-139">Se questo corrisponde alla configurazione di Azure AD, l'autenticazione avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ac30a-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="ac30a-140">Di seguito è riportata la regola attestazioni personalizzata che implementa questa logica:</span><span class="sxs-lookup"><span data-stu-id="ac30a-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="ac30a-141">Per usare l'opzione -SupportMultipleDomain quando si prova ad aggiungere o convertire domini già aggiunti, è necessario che il trust federativo sia stato configurato per supportarli in origine.</span><span class="sxs-lookup"><span data-stu-id="ac30a-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="ac30a-142">Come aggiornare il trust tra AD FS e Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac30a-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="ac30a-143">Se il trust federativo non è stato configurato tra AD FS e l'istanza di Azure AD, potrebbe essere necessario crearlo di nuovo,</span><span class="sxs-lookup"><span data-stu-id="ac30a-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="ac30a-144">perché, quando viene configurato in origine senza il parametro `-SupportMultipleDomain`, il valore IssuerUri viene impostato con il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="ac30a-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="ac30a-145">Nella schermata seguente è possibile vedere che IssuerUri è impostato su https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ac30a-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="ac30a-146">Se un nuovo dominio è stato aggiunto correttamente al portale di Azure AD e si prova a convertirlo usando `Convert-MsolDomaintoFederated -DomainName <your domain>`, verrà visualizzato l'errore seguente.</span><span class="sxs-lookup"><span data-stu-id="ac30a-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="ac30a-148">Se si prova ad aggiungere l'opzione `-SupportMultipleDomain` , verrà visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="ac30a-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="ac30a-150">Se si prova semplicemente a eseguire `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` nel dominio originale, verrà visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="ac30a-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Errore della federazione](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="ac30a-152">Usare la procedura seguente per aggiungere un dominio di primo livello aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="ac30a-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="ac30a-153">Se è già stato aggiunto un dominio e non è stato usato il parametro `-SupportMultipleDomain` , iniziare dalla procedura per la rimozione e l'aggiornamento del dominio originale.</span><span class="sxs-lookup"><span data-stu-id="ac30a-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="ac30a-154">Se il dominio di primo livello non è stato ancora aggiunto, è possibile iniziare dalla procedura per l'aggiunta di un dominio usando comandi PowerShell di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ac30a-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="ac30a-155">Usare la procedura seguente per rimuovere il trust di Microsoft Online e aggiornare il dominio originale.</span><span class="sxs-lookup"><span data-stu-id="ac30a-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="ac30a-156">Nel server federativo di AD FS aprire **Gestione AD FS**</span><span class="sxs-lookup"><span data-stu-id="ac30a-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="ac30a-157">Sulla sinistra espandere **Relazioni di attendibilità** e **Attendibilità componente**</span><span class="sxs-lookup"><span data-stu-id="ac30a-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="ac30a-158">Sulla destra eliminare la voce **Piattaforma delle identità di Microsoft Office 365** .</span><span class="sxs-lookup"><span data-stu-id="ac30a-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="ac30a-159">![Rimozione di Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="ac30a-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="ac30a-160">Nel computer in cui è installato il [Modulo di Microsoft Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) eseguire il comando seguente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="ac30a-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="ac30a-161">Immettere il nome utente e la password di un amministratore globale di Azure AD con cui si esegue la federazione.</span><span class="sxs-lookup"><span data-stu-id="ac30a-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="ac30a-162">In PowerShell immettere `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="ac30a-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="ac30a-163">In PowerShell immettere `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="ac30a-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="ac30a-164">Questa impostazione è relativa al dominio originale.</span><span class="sxs-lookup"><span data-stu-id="ac30a-164">This is for the original domain.</span></span>  <span data-ttu-id="ac30a-165">Usando i domini precedenti, si ottiene quindi: `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="ac30a-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="ac30a-166">Usare la procedura seguente per aggiungere il nuovo dominio di primo livello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac30a-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="ac30a-167">Nel computer in cui è installato il [Modulo di Microsoft Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) eseguire il comando seguente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="ac30a-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="ac30a-168">Immettere il nome utente e la password di un amministratore globale di Azure AD con cui si esegue la federazione.</span><span class="sxs-lookup"><span data-stu-id="ac30a-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="ac30a-169">In PowerShell immettere `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="ac30a-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="ac30a-170">In PowerShell immettere `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="ac30a-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="ac30a-171">Usare la procedura seguente per aggiungere il nuovo dominio di primo livello tramite Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ac30a-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="ac30a-172">Avviare Azure AD Connect dal desktop o dal menu Start.</span><span class="sxs-lookup"><span data-stu-id="ac30a-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="ac30a-173">Scegliere "Aggiunta di un altro dominio di Azure AD" ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="ac30a-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="ac30a-174">Immettere le credenziali di Azure AD e Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac30a-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="ac30a-175">Selezionare il secondo dominio da configurare per la federazione.</span><span class="sxs-lookup"><span data-stu-id="ac30a-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="ac30a-176">![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="ac30a-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="ac30a-177">Fare clic su Installa.</span><span class="sxs-lookup"><span data-stu-id="ac30a-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="ac30a-178">Verificare il nuovo dominio di primo livello</span><span class="sxs-lookup"><span data-stu-id="ac30a-178">Verify the new top-level domain</span></span>
<span data-ttu-id="ac30a-179">Usando il comando `Get-MsolDomainFederationSettings -DomainName <your domain>`di PowerShell, è possibile visualizzare la proprietà IssuerUri aggiornata.</span><span class="sxs-lookup"><span data-stu-id="ac30a-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="ac30a-180">La schermata seguente mostra le impostazioni di federazione aggiornate sul dominio originale http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="ac30a-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="ac30a-182">E IssuerUri sul nuovo dominio è stato impostato su https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="ac30a-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="ac30a-184">Supporto per sottodomini</span><span class="sxs-lookup"><span data-stu-id="ac30a-184">Support for Sub-domains</span></span>
<span data-ttu-id="ac30a-185">A causa della modalità di gestione dei domini in Azure AD, eventuali sottodomini aggiunti erediteranno le impostazioni del dominio padre.</span><span class="sxs-lookup"><span data-stu-id="ac30a-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="ac30a-186">La proprietà IssuerUri deve quindi corrispondere a quella degli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="ac30a-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="ac30a-187">Si supponga ad esempio che sia presente il dominio bmcontoso.com e che quindi si aggiunga corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ac30a-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="ac30a-188">Ciò significa che IssuerUri per un utente di corp.bmcontoso.com dovrà essere **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="ac30a-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="ac30a-189">Tuttavia la regola standard implementata sopra per Azure AD genererà un token con un emittente come **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="ac30a-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="ac30a-190">che non corrisponderà al valore di dominio obbligatorio e l'autenticazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ac30a-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="ac30a-191">Come abilitare il supporto per sottodomini</span><span class="sxs-lookup"><span data-stu-id="ac30a-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="ac30a-192">Per risolvere questo problema, è necessario che il trust della relying party di AD FS per Microsoft Online venga aggiornato.</span><span class="sxs-lookup"><span data-stu-id="ac30a-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="ac30a-193">Per eseguire questa operazione, è necessario configurare una regola attestazioni personalizzata, in modo che vengano rimossi tutti i sottodomini dal suffisso UPN di un utente durante la creazione del valore Issuer personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ac30a-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="ac30a-194">L'attestazione seguente consente di eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="ac30a-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="ac30a-195">L'ultimo numero dell'espressione regolare imposta il numero di domini padre presente nel dominio radice.</span><span class="sxs-lookup"><span data-stu-id="ac30a-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="ac30a-196">In bmcontoso.com sono necessari due domini padre.</span><span class="sxs-lookup"><span data-stu-id="ac30a-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="ac30a-197">Se fossero necessari tre domini padre (ad esempio: corp.bmcontoso.com), il numero sarebbe tre.</span><span class="sxs-lookup"><span data-stu-id="ac30a-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="ac30a-198">È possibile indicare un intervallo, la corrispondenza sarà sempre in base al massimo dei domini.</span><span class="sxs-lookup"><span data-stu-id="ac30a-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="ac30a-199">"{2,3}" corrisponde a due o tre domini (ad esempio: bmfabrikam.com e corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="ac30a-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="ac30a-200">Usare la procedura seguente per aggiungere un'attestazione personalizzata per il supporto dei sottodomini.</span><span class="sxs-lookup"><span data-stu-id="ac30a-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="ac30a-201">Aprire Gestione AD FS.</span><span class="sxs-lookup"><span data-stu-id="ac30a-201">Open AD FS Management</span></span>
2. <span data-ttu-id="ac30a-202">Fare clic con il pulsante destro del mouse sul trust della relying party di Microsoft Online RP quindi scegliere Modifica regole attestazione.</span><span class="sxs-lookup"><span data-stu-id="ac30a-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="ac30a-203">Selezionare la terza regola attestazioni e sostituire ![Modifica dell'attestazione](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="ac30a-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="ac30a-204">Sostituire l'attestazione corrente:</span><span class="sxs-lookup"><span data-stu-id="ac30a-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Sostituzione dell'attestazione](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="ac30a-206">Fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="ac30a-206">Click Ok.</span></span>  <span data-ttu-id="ac30a-207">Fare clic su Applica.</span><span class="sxs-lookup"><span data-stu-id="ac30a-207">Click Apply.</span></span>  <span data-ttu-id="ac30a-208">Fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="ac30a-208">Click Ok.</span></span>  <span data-ttu-id="ac30a-209">Chiudere Gestione ADFS.</span><span class="sxs-lookup"><span data-stu-id="ac30a-209">Close AD FS Management.</span></span>

