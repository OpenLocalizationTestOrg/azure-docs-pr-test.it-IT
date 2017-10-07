---
title: Report utilizzo aaaUnlicensed | Documenti Microsoft
description: "salve le funzionalità di Azure AD a pagamento consente di che identificare gli utenti senza licenza che usano report di utilizzo senza licenza."
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
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="1d4c3-103">Report Utilizzo senza licenza</span><span class="sxs-lookup"><span data-stu-id="1d4c3-103">Unlicensed usage report</span></span>
<span data-ttu-id="1d4c3-104">salve le funzionalità di Azure AD a pagamento consente di che identificare gli utenti senza licenza che usano report di utilizzo senza licenza.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="1d4c3-105">In questo modo toomake un migliore utilizzo delle licenze acquistate e tooidentify si conosce quando potrebbe essere necessario ottenere licenze aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="1d4c3-106">report di Hello Mostra utilizzo attivo di hello le funzionalità a pagamento in hello ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="1d4c3-107">Struttura del report</span><span class="sxs-lookup"><span data-stu-id="1d4c3-107">Report structure</span></span>
| <span data-ttu-id="1d4c3-108">Nome colonna</span><span class="sxs-lookup"><span data-stu-id="1d4c3-108">Column name</span></span> | <span data-ttu-id="1d4c3-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d4c3-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d4c3-110">Utente senza licenza</span><span class="sxs-lookup"><span data-stu-id="1d4c3-110">Unlicensed User</span></span> |<span data-ttu-id="1d4c3-111">Nome dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="1d4c3-111">Name of hello user</span></span> |
| <span data-ttu-id="1d4c3-112">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="1d4c3-112">Feature</span></span> |<span data-ttu-id="1d4c3-113">nome della funzionalità Hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-113">hello feature name.</span></span> <span data-ttu-id="1d4c3-114">Ad esempio: accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-114">For example: conditional access</span></span> |
| <span data-ttu-id="1d4c3-115">Applicazioni a cui è stato eseguito l'accesso</span><span class="sxs-lookup"><span data-stu-id="1d4c3-115">Application Accessed</span></span> |<span data-ttu-id="1d4c3-116">nome di Hello dell'applicazione hello cui si accede con funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="1d4c3-117">Ad esempio: Office 365 SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="1d4c3-118">Se è stato eliminato un account utente hello 'Senza licenza utente' colonna verrà popolata con un ID, ad esempio 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="1d4c3-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="1d4c3-119">Funzionalità di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="1d4c3-119">Conditional access feature</span></span>
<span data-ttu-id="1d4c3-120">Gli utenti senza licenza verranno contrassegnati quando accedono a un servizio a cui sono applicati criteri di accesso, se non hanno una licenza di Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="1d4c3-121">Si applica tooMFA / criteri di posizione, nonché dispositivi criteri che utilizzano Intune.</span><span class="sxs-lookup"><span data-stu-id="1d4c3-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="1d4c3-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1d4c3-122">See also</span></span>
* [<span data-ttu-id="1d4c3-123">Protezione dell'accesso a Office 365 e ad altre app connesse ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d4c3-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="1d4c3-124">Guida introduttiva con accesso condizionale tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="1d4c3-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

