---
title: "aaaFederating più Azure AD con ADFS single | Documenti Microsoft"
description: "In questo documento si apprenderà come toofederate più Azure AD con una singola istanza di ADFS."
keywords: "eseguire la federazione, ADFS, AD FS, più tenant, singola istanza di AD FS, unica istanza di AD FS, federazione multi-tenant, ad fs con più foreste, aad connect, federazione, federazione tra tenant"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="b7478-104">Eseguire la federazione di più istanze di Azure AD con una singola istanza di AD FS</span><span class="sxs-lookup"><span data-stu-id="b7478-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="b7478-105">In una singola farm AD FS a disponibilità elevata è possibile eseguire la federazione di più foreste, se tra di esse esiste un trust bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="b7478-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="b7478-106">Più foreste può o potrebbe non corrispondere toohello stesso Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b7478-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="b7478-107">In questo articolo vengono fornite istruzioni su come tooconfigure federazione tra un'unica distribuzione di ADFS e più foreste che toodifferent di sincronizzazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7478-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Federazione multi-tenant con una singola istanza di AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="b7478-109">Il writeback dei dispositivi e l'aggiunta automatica di dispositivi non sono supportati in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="b7478-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="b7478-110">Azure AD Connect non può essere federazione tooconfigure utilizzati in questo scenario, poiché Azure AD Connect è possibile configurare la federazione per i domini in una singola AD Azure.</span><span class="sxs-lookup"><span data-stu-id="b7478-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="b7478-111">Procedura per la federazione di AD FS con più istanze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7478-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="b7478-112">Si consideri che un dominio contoso.com in Azure Active Directory contoso.onmicrosoft.com già è federato con ADFS hello locale installati nell'ambiente di Active Directory locale di contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b7478-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="b7478-113">e che Fabrikam.com sia un dominio nell'istanza di Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b7478-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="b7478-114">Passaggio 1: Stabilire un trust bidirezionale</span><span class="sxs-lookup"><span data-stu-id="b7478-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="b7478-115">Per ADFS in contoso.com toobe tooauthenticate in grado di utenti in fabrikam.com, è necessario un trust bidirezionale tra contoso.com e fabrikam.com. Seguire la linea guida hello in questo [articolo](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello trust bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="b7478-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="b7478-116">Passaggio 2: Modificare le impostazioni di federazione di contoso.com</span><span class="sxs-lookup"><span data-stu-id="b7478-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="b7478-117">Hello autorità di certificazione predefinita impostata per tooAD un singolo dominio federato ADFS è "http://ADFSServiceFQDN/adfs/services/trust", ad esempio, "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="b7478-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="b7478-118">Azure Active Directory richiede un'autorità di certificazione univoca per ogni dominio federato.</span><span class="sxs-lookup"><span data-stu-id="b7478-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="b7478-119">Poiché hello stesso AD FS sta toofederate due domini, il valore di autorità di certificazione hello deve toobe modificato in modo che sia univoco per ogni dominio che ADFS la federazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b7478-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="b7478-120">Nel server AD FS hello, aprire Azure AD PowerShell ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b7478-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="b7478-121">Connettersi toohello Azure Active Directory che contiene hello dominio contoso.com Connect-MsolService aggiornamento hello impostazioni della federazione per contoso.com Update-MsolFederatedDomain - DomainName contoso.com-SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="b7478-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="b7478-122">Autorità emittente di impostazioni di federazione del dominio hello verrà modificato troppo "http://contoso.com/adfs/services/trust" un rilascio di attestazioni e regola sarà aggiunta per hello Azure AD Trust della Relying Party tooissue hello corretto valore issuerId in base al suffisso UPN hello.</span><span class="sxs-lookup"><span data-stu-id="b7478-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="b7478-123">Passaggio 3: Eseguire la federazione di fabrikam.com con AD FS</span><span class="sxs-lookup"><span data-stu-id="b7478-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="b7478-124">Sessione di powershell di Azure AD eseguire l'hello alla procedura seguente: connessione tooAzure Active Directory che contiene hello dominio fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="b7478-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="b7478-125">Convertire toofederated di dominio fabrikam.com gestiti hello:</span><span class="sxs-lookup"><span data-stu-id="b7478-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="b7478-126">Hello sopra operazione effettuerà la federazione hello dominio fabrikam.com con hello stesso AD FS.</span><span class="sxs-lookup"><span data-stu-id="b7478-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="b7478-127">È possibile verificare le impostazioni del dominio hello utilizzando Get-MsolDomainFederationSettings per entrambi i domini.</span><span class="sxs-lookup"><span data-stu-id="b7478-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7478-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7478-128">Next steps</span></span>
[<span data-ttu-id="b7478-129">Connettere Active Directory ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7478-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
