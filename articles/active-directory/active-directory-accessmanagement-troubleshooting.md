---
title: Risoluzione dei problemi di appartenenza dinamica per i gruppi | Documentazione Microsoft
description: Suggerimenti per la risoluzione dei problemi di appartenenza dinamica per i gruppi di Azure AD.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="bc5da-103">Risoluzione dei problemi di appartenenza dinamica per i gruppi</span><span class="sxs-lookup"><span data-stu-id="bc5da-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="bc5da-104">**È stata configurata una regola su un gruppo, ma nessuna appartenenza viene aggiornata nel gruppo**</span><span class="sxs-lookup"><span data-stu-id="bc5da-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="bc5da-105">Verificare che l'opzione **Abilita gestione gruppi delegata** sia impostata su **Sì** nella scheda **Configura**.</span><span class="sxs-lookup"><span data-stu-id="bc5da-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="bc5da-106">Questa impostazione verrà visualizzato solo se si è connessi come utente a cui è assegnata una licenza di Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="bc5da-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="bc5da-107">Verificare i valori degli attributi utente della regola: sono presenti utenti che soddisfano la regola?</span><span class="sxs-lookup"><span data-stu-id="bc5da-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="bc5da-108">**È stata configurata una regola, ma i membri esistenti della regola sono stati rimossi**</span><span class="sxs-lookup"><span data-stu-id="bc5da-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="bc5da-109">Si tratta di un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="bc5da-109">This is expected behavior.</span></span> <span data-ttu-id="bc5da-110">I membri esistenti del gruppo vengono rimosse quando una regola viene abilitata o modificata.</span><span class="sxs-lookup"><span data-stu-id="bc5da-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="bc5da-111">Gli utenti restituiti dalla valutazione della regola vengono aggiunti come membri al gruppo.</span><span class="sxs-lookup"><span data-stu-id="bc5da-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="bc5da-112">**Quando si aggiunge o modifica una regola non vengono visualizzate immediatamente le modifiche a livello di appartenenza. Perché?**</span><span class="sxs-lookup"><span data-stu-id="bc5da-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="bc5da-113">La valutazione dell'appartenenza dedicata viene eseguita periodicamente in un processo asincrono in background.</span><span class="sxs-lookup"><span data-stu-id="bc5da-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="bc5da-114">La durata del processo è determinata dal numero di utenti nella directory e dalle dimensioni del gruppo creato in base alla regola.</span><span class="sxs-lookup"><span data-stu-id="bc5da-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="bc5da-115">In genere, per le directory con un numero limitato di utenti le modifiche a livello di appartenenza al gruppo verranno visualizzate nell'arco di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bc5da-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="bc5da-116">L'inserimento dei dati per le directory con un numero elevato di utenti può richiedere intervalli maggiori o uguali a 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="bc5da-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="bc5da-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc5da-117">Next steps</span></span>
<span data-ttu-id="bc5da-118">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc5da-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bc5da-119">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc5da-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="bc5da-120">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc5da-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="bc5da-121">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc5da-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="bc5da-122">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc5da-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
