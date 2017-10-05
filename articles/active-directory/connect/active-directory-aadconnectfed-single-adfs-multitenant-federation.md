---
title: "Federazione di più istanze di Azure AD con una singola istanza di AD FS | Microsoft Docs"
description: "Questo documento illustra come eseguire la federazione di più istanze di Azure AD con una singola istanza di AD FS."
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
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="7f707-104">Eseguire la federazione di più istanze di Azure AD con una singola istanza di AD FS</span><span class="sxs-lookup"><span data-stu-id="7f707-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="7f707-105">In una singola farm AD FS a disponibilità elevata è possibile eseguire la federazione di più foreste, se tra di esse esiste un trust bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="7f707-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="7f707-106">Queste diverse foreste possono corrispondere o meno alla stessa istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f707-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="7f707-107">Questo articolo contiene istruzioni su come configurare la federazione tra una singola distribuzione di AD FS e più foreste con sincronizzazione in istanze diverse di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f707-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Federazione multi-tenant con una singola istanza di AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="7f707-109">Il writeback dei dispositivi e l'aggiunta automatica di dispositivi non sono supportati in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="7f707-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="7f707-110">Non è possibile usare Azure AD Connect per configurare la federazione in questo scenario perché Azure AD Connect può configurare la federazione per domini in una singola istanza di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f707-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="7f707-111">Procedura per la federazione di AD FS con più istanze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f707-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="7f707-112">Si supponga che il dominio contoso.com nell'istanza di Azure Active Directory contoso.onmicrosoft.com sia già federato con l'istanza locale di AD FS installata nell'ambiente Active Directory locale contoso.com</span><span class="sxs-lookup"><span data-stu-id="7f707-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="7f707-113">e che Fabrikam.com sia un dominio nell'istanza di Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7f707-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="7f707-114">Passaggio 1: Stabilire un trust bidirezionale</span><span class="sxs-lookup"><span data-stu-id="7f707-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="7f707-115">Per consentire all'istanza di AD FS in contoso.com di autenticare gli utenti in fabrikam.com, è necessario un trust bidirezionale tra contoso.com e fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="7f707-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="7f707-116">Per creare il trust bidirezionale, seguire le linee guida contenute in questo [articolo](https://technet.microsoft.com/library/cc816590.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f707-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="7f707-117">Passaggio 2: Modificare le impostazioni di federazione di contoso.com</span><span class="sxs-lookup"><span data-stu-id="7f707-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="7f707-118">L'autorità di certificazione predefinita per un singolo dominio federato ad AD FS è "http://FQDNServizioADFS/adfs/services/trust", ad esempio "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="7f707-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="7f707-119">Azure Active Directory richiede un'autorità di certificazione univoca per ogni dominio federato.</span><span class="sxs-lookup"><span data-stu-id="7f707-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="7f707-120">Dato che la stessa istanza di AD FS eseguirà la federazione di due domini, il valore dell'autorità di certificazione deve essere modificato in modo che sia univoco per ogni dominio federato con Azure Active Directory da AD FS.</span><span class="sxs-lookup"><span data-stu-id="7f707-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="7f707-121">Nel server AD FS aprire Azure AD PowerShell e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7f707-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="7f707-122">Connettersi all'istanza di Azure Active Directory contenente il dominio contoso.com: Connect-MsolService. Aggiornare le impostazioni di federazione per contoso.com: Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain.</span><span class="sxs-lookup"><span data-stu-id="7f707-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="7f707-123">L'autorità di certificazione nell'impostazione di federazione del dominio verrà modificata in "http://contoso.com/adfs/services/trust" e verrà aggiunta una regola attestazioni di rilascio per il trust della relying party di Azure AD per rilasciare il valore issuerId corretto in base al suffisso UPN.</span><span class="sxs-lookup"><span data-stu-id="7f707-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="7f707-124">Passaggio 3: Eseguire la federazione di fabrikam.com con AD FS</span><span class="sxs-lookup"><span data-stu-id="7f707-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="7f707-125">Nella sessione di Azure AD PowerShell seguire questa procedura: connettersi all'istanza di Azure Active Directory contenente il dominio fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="7f707-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="7f707-126">Convertire il dominio gestito fabrikam.com in federato:</span><span class="sxs-lookup"><span data-stu-id="7f707-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="7f707-127">L'operazione riportata sopra eseguirà la federazione del dominio fabrikam.com con la stessa istanza di AD FS.</span><span class="sxs-lookup"><span data-stu-id="7f707-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="7f707-128">È possibile verificare le impostazioni di dominio usando Get-MsolDomainFederationSettings per entrambi i domini.</span><span class="sxs-lookup"><span data-stu-id="7f707-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f707-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f707-129">Next steps</span></span>
[<span data-ttu-id="7f707-130">Connettere Active Directory ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f707-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
