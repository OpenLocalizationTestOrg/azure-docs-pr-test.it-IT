---
title: Assegnare gruppi alle app Azure AD | Documentazione Microsoft
description: Come implementare l'assegnazione di gruppo per le applicazioni Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="17f02-103">Assegnare gruppi di Azure Active Directory a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="17f02-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="17f02-104">Prima di assegnare utenti e gruppi a un'applicazione, è necessario richiedere l'assegnazione dell’utente.</span><span class="sxs-lookup"><span data-stu-id="17f02-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="17f02-105">Per informazioni su come richiedere l'assegnazione dell'utente, vedere l'articolo [Richiedere l'assegnazione utente](active-directory-applications-guiding-developers-requiring-user-assignment.md) .</span><span class="sxs-lookup"><span data-stu-id="17f02-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="17f02-106">In questo articolo si presuppone che siano già stati creati gruppi nella active directory che si utilizza per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="17f02-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="17f02-107">Assegnazione dei gruppi a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="17f02-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="17f02-108">Accedere al portale di Azure con un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="17f02-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="17f02-109">Fare clic sulla voce **Tutti gli elementi** del menu principale.</span><span class="sxs-lookup"><span data-stu-id="17f02-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="17f02-110">Scegliere la directory utilizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17f02-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="17f02-111">Fare clic sulla scheda **APPLICAZIONI** .</span><span class="sxs-lookup"><span data-stu-id="17f02-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="17f02-112">Selezionare l'applicazione dall'elenco di applicazioni associate a questa directory.</span><span class="sxs-lookup"><span data-stu-id="17f02-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="17f02-113">Fare clic sulla scheda **UTENTI E GRUPPI** .</span><span class="sxs-lookup"><span data-stu-id="17f02-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="17f02-114">Filtrare l'elenco dei gruppi nella active directory utilizzando l’elenco a discesa **Gruppi** .</span><span class="sxs-lookup"><span data-stu-id="17f02-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="17f02-115">Selezionare il gruppo.</span><span class="sxs-lookup"><span data-stu-id="17f02-115">Select the group.</span></span>
9. <span data-ttu-id="17f02-116">Fare clic su **ASSEGNARE**.</span><span class="sxs-lookup"><span data-stu-id="17f02-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="17f02-117">Fare clic su **sì** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="17f02-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17f02-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17f02-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
