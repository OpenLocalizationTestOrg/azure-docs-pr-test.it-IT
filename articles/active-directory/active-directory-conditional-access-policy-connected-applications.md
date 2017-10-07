---
title: criteri di accesso condizionale basato su dispositivo di Azure Active Directory aaaConfigure | Documenti Microsoft
description: Informazioni su come criteri di accesso condizionale basato su dispositivi di tooconfigure Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="7a0e4-103">Configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a0e4-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="7a0e4-104">Con l'[accesso condizionale di Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), è possibile ottimizzare la modalità in cui gli utenti autorizzati possono accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="7a0e4-105">Ad esempio, si limita hello accedere toocertain risorse tootrusted ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="7a0e4-106">Un criterio di accesso condizionale che richiede un dispositivo attendibile è noto anche come criterio di accesso condizionale basato su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="7a0e4-107">In questo argomento fornisce informazioni su come criteri per le applicazioni connessi AD Azure di accesso condizionale basato su dispositivi tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="7a0e4-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7a0e4-108">Before you begin</span></span>

<span data-ttu-id="7a0e4-109">L'accesso condizionale basato su dispositivo lega l'**accesso condizionale di Azure AD** e la **gestione dei dispositivi di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="7a0e4-110">Se non si ha familiarità con una di queste aree, è consigliabile leggere i seguenti argomenti, innanzitutto hello:</span><span class="sxs-lookup"><span data-stu-id="7a0e4-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="7a0e4-111">**[Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -questo argomento offre una panoramica concettuale di condizionale accedere e hello la terminologia correlata.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="7a0e4-112">**[Gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)**  -questo argomento viene fornita una panoramica di hello varie opzioni sono tooconnect dispositivi con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="7a0e4-113">Dispositivi attendibili</span><span class="sxs-lookup"><span data-stu-id="7a0e4-113">Trusted devices</span></span>

<span data-ttu-id="7a0e4-114">In un ambiente mobile-first, prima di cloud, Azure Active Directory consente di single sign-on toodevices, applicazioni e servizi da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="7a0e4-115">Per alcune risorse nel proprio ambiente, concessione dell'accesso di utenti appropriati toohello potrebbero non essere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="7a0e4-116">Inoltre toohello utenti appropriati, si potrebbero anche richiedere che un toobe attendibile di dispositivo utilizzato tooaccess una risorsa.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="7a0e4-117">Nell'ambiente in uso, è possibile definire un dispositivo attendibile ciò che si basa su hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="7a0e4-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="7a0e4-118">Hello [piattaforme per dispositivi](active-directory-conditional-access-azure-portal.md#device-platforms) in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="7a0e4-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="7a0e4-119">Se un dispositivo è conforme</span><span class="sxs-lookup"><span data-stu-id="7a0e4-119">Whether a device is compliant</span></span>
- <span data-ttu-id="7a0e4-120">Se un dispositivo è aggiunto al dominio</span><span class="sxs-lookup"><span data-stu-id="7a0e4-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="7a0e4-121">Hello [piattaforme per dispositivi](active-directory-conditional-access-azure-portal.md#device-platforms) è caratterizzato dal sistema operativo hello che è in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="7a0e4-122">Nei criteri di accesso condizionale basato su dispositivo, è possibile limitare l'accesso toocertain toospecific risorse piattaforme del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="7a0e4-123">In un criterio di accesso condizionale basato su dispositivo, è possibile richiedere toobe dispositivi attendibili segnato come conforme.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="7a0e4-125">I dispositivi possono essere contrassegnati come conformi nella directory hello da:</span><span class="sxs-lookup"><span data-stu-id="7a0e4-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="7a0e4-126">Intune</span><span class="sxs-lookup"><span data-stu-id="7a0e4-126">Intune</span></span> 
- <span data-ttu-id="7a0e4-127">Un sistema di gestione di dispositivi mobili di terze parti che si integra con Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a0e4-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="7a0e4-128">Solo i dispositivi che sono connessi tooAzure Active Directory possono essere contrassegnati come conformi.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="7a0e4-129">tooconnect tooAzure un dispositivo Active Directory, è necessario hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7a0e4-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="7a0e4-130">Registrazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a0e4-130">Azure AD registered</span></span>
- <span data-ttu-id="7a0e4-131">Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a0e4-131">Azure AD joined</span></span>
- <span data-ttu-id="7a0e4-132">Aggiunta all'identità ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a0e4-132">Hybrid Azure AD joined</span></span>

    ![App cloud](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="7a0e4-134">Se si dispone di un footprint di Active Directory (AD) locale, è possibile i dispositivi che non sono connessi tooAzure AD ma toobe tooyour aggiunti a un Active Directory trusted.</span><span class="sxs-lookup"><span data-stu-id="7a0e4-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="7a0e4-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7a0e4-136">Next steps</span></span>

<span data-ttu-id="7a0e4-137">Prima di configurare un criterio di accesso condizionale basato su dispositivi nell'ambiente in uso, è consigliabile dare un'occhiata hello [procedure consigliate per l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7a0e4-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

