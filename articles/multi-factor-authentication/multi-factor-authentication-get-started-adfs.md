---
title: Verifica in due passaggi e AD FS - Azure MFA | Documentazione Microsoft
description: "Questa è la pagina di Azure Multi-Factor Authentication che descrive come iniziare a usare Azure MFA e ADFS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="ed8e6-103">Introduzione a Azure Multi-Factor Authentication e Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed8e6-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="ed8e6-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="ed8e6-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="ed8e6-105">Se l'organizzazione ha federato l'istanza locale di Active Directory con Azure Active Directory tramite AD FS, sono disponibili due opzioni per l'uso di Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="ed8e6-106">Proteggere le risorse cloud mediante Azure Multi-Factor Authentication o Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed8e6-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="ed8e6-107">Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ed8e6-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="ed8e6-108">Nella tabella seguente viene riepilogata l'esperienza di verifica tra le risorse di protezione con Azure Multi-Factor Authentication e AD FS</span><span class="sxs-lookup"><span data-stu-id="ed8e6-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="ed8e6-109">Esperienza di verifica - App basate su browser</span><span class="sxs-lookup"><span data-stu-id="ed8e6-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="ed8e6-110">Esperienza di verifica - App non basate su browser</span><span class="sxs-lookup"><span data-stu-id="ed8e6-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed8e6-111">Proteggere le risorse Azure AD utilizzando Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ed8e6-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="ed8e6-112">Il primo passaggio di verifica viene eseguito in locale usando AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="ed8e6-113">Il secondo passaggio è un metodo basato su telefono eseguito mediante l'autenticazione cloud.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="ed8e6-114">Proteggere le risorse di Azure AD con Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ed8e6-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="ed8e6-115">Il primo passaggio di verifica viene eseguito in locale usando AD FS.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="ed8e6-116">Il secondo passaggio viene eseguito in locale rispettando l'attestazione.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="ed8e6-117">Avvertenze per le password dell’app rivolte agli utenti federati:</span><span class="sxs-lookup"><span data-stu-id="ed8e6-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="ed8e6-118">Le password dell'app vengono verificate mediante l'autenticazione cloud e di conseguenza ignorano la federazione.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="ed8e6-119">La federazione viene usata attivamente solo durante l'impostazione della password dell'app.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="ed8e6-120">Le impostazioni locali di Controllo di accesso client non vengono rispettate dalle password dell'app.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="ed8e6-121">Si perde la funzionalità di registrazione dell'autenticazione locale per le password dell'app.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="ed8e6-122">La disabilitazione/eliminazione dell'account può richiedere fino a tre ore per la sincronizzazione della directory, ritardando la disabilitazione/eliminazione delle password dell'app nell'identità cloud.</span><span class="sxs-lookup"><span data-stu-id="ed8e6-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed8e6-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed8e6-123">Next steps</span></span>
<span data-ttu-id="ed8e6-124">Per informazioni sulla configurazione di Azure Multi-Factor Authentication o del server Azure Multi-Factor Authentication con AD FS, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="ed8e6-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="ed8e6-125">Proteggere le risorse cloud mediante Azure Multi-Factor Authentication e ADFS</span><span class="sxs-lookup"><span data-stu-id="ed8e6-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="ed8e6-126">Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication con ADFS Server Windows 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ed8e6-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="ed8e6-127">Proteggere le risorse del cloud e locali mediante Server Azure Multi-Factor Authentication con AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="ed8e6-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
