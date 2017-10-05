---
title: Report Utilizzo senza licenza | Microsoft Docs
description: "Il report Utilizzo senza licenza semplifica l'identificazione di utenti senza licenza che usano funzionalità a pagamento di Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="7935f-103">Report Utilizzo senza licenza</span><span class="sxs-lookup"><span data-stu-id="7935f-103">Unlicensed usage report</span></span>
<span data-ttu-id="7935f-104">Il report Utilizzo senza licenza semplifica l'identificazione di utenti senza licenza che usano funzionalità a pagamento di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7935f-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="7935f-105">Ciò consente di usare in modo ottimale le licenze acquistate e di identificare le situazioni in cui potrebbero essere necessarie licenze aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="7935f-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="7935f-106">Il report mostra l'utilizzo attivo effettivo delle funzionalità a pagamento negli ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="7935f-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="7935f-107">Struttura del report</span><span class="sxs-lookup"><span data-stu-id="7935f-107">Report structure</span></span>
| <span data-ttu-id="7935f-108">Nome colonna</span><span class="sxs-lookup"><span data-stu-id="7935f-108">Column name</span></span> | <span data-ttu-id="7935f-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7935f-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7935f-110">Utente senza licenza</span><span class="sxs-lookup"><span data-stu-id="7935f-110">Unlicensed User</span></span> |<span data-ttu-id="7935f-111">Nome dell'utente</span><span class="sxs-lookup"><span data-stu-id="7935f-111">Name of the user</span></span> |
| <span data-ttu-id="7935f-112">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="7935f-112">Feature</span></span> |<span data-ttu-id="7935f-113">Nome della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7935f-113">The feature name.</span></span> <span data-ttu-id="7935f-114">Ad esempio: accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="7935f-114">For example: conditional access</span></span> |
| <span data-ttu-id="7935f-115">Applicazioni a cui è stato eseguito l'accesso</span><span class="sxs-lookup"><span data-stu-id="7935f-115">Application Accessed</span></span> |<span data-ttu-id="7935f-116">Nome dell'applicazione a cui viene eseguito l'accesso con la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7935f-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="7935f-117">Ad esempio: Office 365 SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="7935f-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="7935f-118">Se l'account utente è stato eliminato, la colonna "Utente senza licenza" verrò popolata con un ID, ad esempio 1003000090D8B285.</span><span class="sxs-lookup"><span data-stu-id="7935f-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="7935f-119">Funzionalità di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="7935f-119">Conditional access feature</span></span>
<span data-ttu-id="7935f-120">Gli utenti senza licenza verranno contrassegnati quando accedono a un servizio a cui sono applicati criteri di accesso, se non hanno una licenza di Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="7935f-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="7935f-121">Questo approccio viene applicato ai criteri di MFA e di posizione, oltre ai dispositivi dei criteri che usano Intune.</span><span class="sxs-lookup"><span data-stu-id="7935f-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="7935f-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7935f-122">See also</span></span>
* [<span data-ttu-id="7935f-123">Protezione dell'accesso a Office 365 e ad altre app connesse ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7935f-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="7935f-124">Guida introduttiva all'accesso condizionale ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="7935f-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

