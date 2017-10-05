---
title: Assegnare licenze per Azure MFA | Documentazione Microsoft
description: Informazioni su come assegnare licenze agli utenti per Microsoft Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="eb554-103">Assegnazione di una licenza di Azure MFA, Azure AD Premium o Enterprise Mobility Suite agli utenti</span><span class="sxs-lookup"><span data-stu-id="eb554-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="eb554-104">Se sono state acquistate licenze di Azure MFA, Azure AD Premium o Enterprise Mobility Suite, non è necessario creare un provider di Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="eb554-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="eb554-105">Dopo aver assegnato le licenze agli utenti, è possibile abilitarli al servizio MFA.</span><span class="sxs-lookup"><span data-stu-id="eb554-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="eb554-106">Per assegnare una licenza</span><span class="sxs-lookup"><span data-stu-id="eb554-106">To assign a license</span></span>
1. <span data-ttu-id="eb554-107">Accedere al [portale di Azure classico](https://manage.windowsazure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="eb554-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="eb554-108">A sinistra, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb554-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="eb554-109">Nella pagina Active Directory fare doppio clic sulla directory con gli utenti da abilitare.</span><span class="sxs-lookup"><span data-stu-id="eb554-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="eb554-110">Nella parte superiore della pagina della directory selezionare **Licenses**.</span><span class="sxs-lookup"><span data-stu-id="eb554-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="eb554-111">![Assegnare licenze](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="eb554-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="eb554-112">Nella pagina Licenze selezionare **Azure Multi-Factor Authentication**, **Active Directory Premium** o **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="eb554-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="eb554-113">Se è presente una sola opzione, risulterà selezionata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="eb554-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="eb554-114">Nella parte inferiore della pagina fare clic su **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="eb554-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="eb554-115">![Assegnare licenze](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="eb554-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="eb554-116">Nella casella visualizzata fare clic accanto agli utenti o ai gruppi a cui si vogliono assegnare le licenze.</span><span class="sxs-lookup"><span data-stu-id="eb554-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="eb554-117">Verrà visualizzato un segno di spunta verde .</span><span class="sxs-lookup"><span data-stu-id="eb554-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="eb554-118">Fare clic sul segno di spunta per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="eb554-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="eb554-119">![Assegnare licenze](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="eb554-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="eb554-120">Verrà visualizzato un messaggio che indica quante licenze sono state assegnate e quante non sono riuscite.</span><span class="sxs-lookup"><span data-stu-id="eb554-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="eb554-121">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb554-121">Click **Ok**.</span></span>
   <span data-ttu-id="eb554-122">![Assegnare licenze](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="eb554-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb554-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb554-123">Next steps</span></span>

- <span data-ttu-id="eb554-124">Per altre informazioni, vedere [Che cosa sono le licenze di Microsoft Azure Active Directory?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="eb554-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
