---
title: "verifica aaaTwo passaggio e AD FS - autenticazione a più fattori di Azure | Documenti Microsoft"
description: "Si tratta hello Azure multi-Factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA e AD FS."
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
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="d86e3-103">Introduzione a Azure Multi-Factor Authentication e Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="d86e3-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="d86e3-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="d86e3-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="d86e3-105">Se l'organizzazione ha federato l'istanza locale di Active Directory con Azure Active Directory tramite AD FS, sono disponibili due opzioni per l'uso di Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="d86e3-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="d86e3-106">Proteggere le risorse cloud mediante Azure Multi-Factor Authentication o Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="d86e3-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="d86e3-107">Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d86e3-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="d86e3-108">Hello nella tabella seguente sono riepilogati hello esperienza di verifica della protezione delle risorse con Azure multi-Factor Authentication e AD FS</span><span class="sxs-lookup"><span data-stu-id="d86e3-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="d86e3-109">Esperienza di verifica - App basate su browser</span><span class="sxs-lookup"><span data-stu-id="d86e3-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="d86e3-110">Esperienza di verifica - App non basate su browser</span><span class="sxs-lookup"><span data-stu-id="d86e3-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d86e3-111">Proteggere le risorse Azure AD utilizzando Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d86e3-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="d86e3-112">il primo passaggio di verifica Hello viene eseguita in locale con ADFS.</span><span class="sxs-lookup"><span data-stu-id="d86e3-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="d86e3-113">secondo passaggio Hello è un metodo basato su telefono eseguito mediante l'autenticazione cloud.</span><span class="sxs-lookup"><span data-stu-id="d86e3-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="d86e3-114">Proteggere le risorse di Azure AD con Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="d86e3-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="d86e3-115">il primo passaggio di verifica Hello viene eseguita in locale con ADFS.</span><span class="sxs-lookup"><span data-stu-id="d86e3-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="d86e3-116">secondo passaggio Hello viene eseguito localmente rispettando l'attestazione hello.</span><span class="sxs-lookup"><span data-stu-id="d86e3-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="d86e3-117">Avvertenze per le password dell’app rivolte agli utenti federati:</span><span class="sxs-lookup"><span data-stu-id="d86e3-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="d86e3-118">Le password dell'app vengono verificate mediante l'autenticazione cloud e di conseguenza ignorano la federazione.</span><span class="sxs-lookup"><span data-stu-id="d86e3-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="d86e3-119">La federazione viene usata attivamente solo durante l'impostazione della password dell'app.</span><span class="sxs-lookup"><span data-stu-id="d86e3-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="d86e3-120">Le impostazioni locali di Controllo di accesso client non vengono rispettate dalle password dell'app.</span><span class="sxs-lookup"><span data-stu-id="d86e3-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="d86e3-121">Si perde la funzionalità di registrazione dell'autenticazione locale per le password dell'app.</span><span class="sxs-lookup"><span data-stu-id="d86e3-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="d86e3-122">Disabilitazione o eliminazione di account potrebbe richiedere ore toothree per la sincronizzazione della directory, ritardando disabilitazione o eliminazione di password di app nell'identità cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d86e3-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d86e3-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d86e3-123">Next steps</span></span>
<span data-ttu-id="d86e3-124">Per informazioni sulla configurazione di Azure multi-Factor Authentication o hello Server Azure multi-Factor Authentication con ADFS, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="d86e3-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="d86e3-125">Proteggere le risorse cloud mediante Azure Multi-Factor Authentication e ADFS</span><span class="sxs-lookup"><span data-stu-id="d86e3-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="d86e3-126">Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication con ADFS Server Windows 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d86e3-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="d86e3-127">Proteggere le risorse del cloud e locali mediante Server Azure Multi-Factor Authentication con AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="d86e3-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
