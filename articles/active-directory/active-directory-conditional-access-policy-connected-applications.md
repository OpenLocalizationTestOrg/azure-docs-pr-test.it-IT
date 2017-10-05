---
title: Configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory | Microsoft Docs
description: Informazioni su come configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory.
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
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="009c1-103">Configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="009c1-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="009c1-104">Con l'[accesso condizionale di Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), è possibile ottimizzare la modalità in cui gli utenti autorizzati possono accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="009c1-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="009c1-105">Ad esempio, è possibile limitare l'accesso a determinate risorse a dispositivi attendibili.</span><span class="sxs-lookup"><span data-stu-id="009c1-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="009c1-106">Un criterio di accesso condizionale che richiede un dispositivo attendibile è noto anche come criterio di accesso condizionale basato su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="009c1-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="009c1-107">Questo argomento fornisce informazioni su come configurare i criteri di accesso condizionale basati su dispositivo per le applicazioni connesse ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="009c1-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="009c1-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="009c1-108">Before you begin</span></span>

<span data-ttu-id="009c1-109">Collegamenti di accesso condizionale basato su dispositivo **Accesso condizionale ad Azure AD** e **Gestione dei dispositivi AD Azure insieme**.</span><span class="sxs-lookup"><span data-stu-id="009c1-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="009c1-110">Se non si ha ancora familiarità con una di queste aree, è consigliabile leggere innanzitutto gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="009c1-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="009c1-111">**[Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**: questo argomento offre una panoramica concettuale dell'accesso condizionale e della terminologia correlata.</span><span class="sxs-lookup"><span data-stu-id="009c1-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="009c1-112">**[Introduzione alla gestione dei dispositivi in Azure Active Directory](device-management-introduction.md)**: questo argomento offre una panoramica delle diverse opzioni a disposizione per connettere i dispositivi con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="009c1-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="009c1-113">Dispositivi attendibili</span><span class="sxs-lookup"><span data-stu-id="009c1-113">Trusted devices</span></span>

<span data-ttu-id="009c1-114">In un mondo in cui i dispositivi mobili e il cloud hanno sempre più importanza, Azure Active Directory consente ovunque l'accesso Single Sign-On a dispositivi, app e servizi.</span><span class="sxs-lookup"><span data-stu-id="009c1-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="009c1-115">Per alcune risorse nel proprio ambiente, la concessione dell'accesso agli utenti appropriati potrebbe non essere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="009c1-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="009c1-116">Oltre agli utenti appropriati, potrebbe anche essere necessario l'uso di un dispositivo attendibile per accedere a una risorsa.</span><span class="sxs-lookup"><span data-stu-id="009c1-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="009c1-117">Nell'ambiente in uso, è possibile definire cos'è un dispositivo attendibile sulla base dei componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="009c1-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="009c1-118">Le [piattaforme del dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms)</span><span class="sxs-lookup"><span data-stu-id="009c1-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="009c1-119">Se un dispositivo è conforme</span><span class="sxs-lookup"><span data-stu-id="009c1-119">Whether a device is compliant</span></span>
- <span data-ttu-id="009c1-120">Se un dispositivo è aggiunto al dominio</span><span class="sxs-lookup"><span data-stu-id="009c1-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="009c1-121">Le [piattaforme del dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) sono caratterizzate dal sistema operativo in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="009c1-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="009c1-122">Nei criteri di accesso condizionale basato su dispositivo, è possibile limitare l'accesso a determinate risorse solo a piattaforme specifiche del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="009c1-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="009c1-123">In un criterio di accesso condizionale basato su dispositivo, è possibile richiedere ai dispositivi attendibili di essere contrassegnati come conforme.</span><span class="sxs-lookup"><span data-stu-id="009c1-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="009c1-125">I dispositivi possono essere contrassegnati come conformi nella directory da:</span><span class="sxs-lookup"><span data-stu-id="009c1-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="009c1-126">Intune</span><span class="sxs-lookup"><span data-stu-id="009c1-126">Intune</span></span> 
- <span data-ttu-id="009c1-127">Un sistema di gestione di dispositivi mobili di terze parti che si integra con Azure AD</span><span class="sxs-lookup"><span data-stu-id="009c1-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="009c1-128">Solo i dispositivi connessi ad Azure AD possono essere contrassegnati come conformi.</span><span class="sxs-lookup"><span data-stu-id="009c1-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="009c1-129">Per connettere un dispositivo ad Azure Active Directory, sono disponibili le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="009c1-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="009c1-130">Registrazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="009c1-130">Azure AD registered</span></span>
- <span data-ttu-id="009c1-131">Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="009c1-131">Azure AD joined</span></span>
- <span data-ttu-id="009c1-132">Aggiunta all'identità ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="009c1-132">Hybrid Azure AD joined</span></span>

    ![App cloud](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="009c1-134">Se si dispone di un footprint di Active Directory (AD) locale, è possibile che i dispositivi non connessi ad Azure AD ma che fanno parte di Active Directory devono essere considerati attendibile.</span><span class="sxs-lookup"><span data-stu-id="009c1-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="009c1-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="009c1-136">Next steps</span></span>

<span data-ttu-id="009c1-137">Prima di configurare un criterio di accesso condizionale basato su dispositivo nell'ambiente in uso, è necessario esaminare [Procedure consigliate per l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="009c1-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

