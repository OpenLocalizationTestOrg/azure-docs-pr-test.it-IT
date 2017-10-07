---
title: aaaTroubleshooting dell'appartenenza dinamica per i gruppi | Documenti Microsoft
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="46b12-103">Risoluzione dei problemi di appartenenza dinamica per i gruppi</span><span class="sxs-lookup"><span data-stu-id="46b12-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="46b12-104">**Ho configurato una regola in un gruppo, ma nessuna appartenenza vengono aggiornata nel gruppo hello**</span><span class="sxs-lookup"><span data-stu-id="46b12-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="46b12-105">Verificare che hello **Abilita gestione gruppi delegata** impostazione troppo**Sì** in hello **configura** scheda. Questa impostazione verrà visualizzato solo se si è connessi come viene assegnato un toowhom utente una licenza di Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="46b12-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="46b12-106">Verificare i valori hello per gli attributi utente sulla regola hello: sono presenti utenti che soddisfano la regola hello?</span><span class="sxs-lookup"><span data-stu-id="46b12-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="46b12-107">**Ho configurato una regola, ma ora in cui vengono rimossi i membri esistenti hello della regola hello**</span><span class="sxs-lookup"><span data-stu-id="46b12-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="46b12-108">Si tratta di un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="46b12-108">This is expected behavior.</span></span> <span data-ttu-id="46b12-109">I membri esistenti del gruppo di hello vengono rimossi quando una regola è abilitata o modificata.</span><span class="sxs-lookup"><span data-stu-id="46b12-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="46b12-110">gli utenti di Hello restituiti dalla valutazione della regola hello vengono aggiunti come gruppo toohello membri.</span><span class="sxs-lookup"><span data-stu-id="46b12-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="46b12-111">**Quando si aggiunge o modifica una regola non vengono visualizzate immediatamente le modifiche a livello di appartenenza. Perché?**</span><span class="sxs-lookup"><span data-stu-id="46b12-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="46b12-112">La valutazione dell'appartenenza dedicata viene eseguita periodicamente in un processo asincrono in background.</span><span class="sxs-lookup"><span data-stu-id="46b12-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="46b12-113">Quanto tempo richiede processo hello è determinato dal numero di hello di utenti, le dimensioni di directory e hello del gruppo di hello creato come risultato della regola hello.</span><span class="sxs-lookup"><span data-stu-id="46b12-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="46b12-114">In genere, le directory con un numero limitato di utenti verranno visualizzato modifiche all'appartenenza di gruppo hello in meno di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="46b12-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="46b12-115">Directory con un numero elevato di utenti può richiedere 30 minuti o più toopopulate.</span><span class="sxs-lookup"><span data-stu-id="46b12-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="46b12-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46b12-116">Next steps</span></span>
<span data-ttu-id="46b12-117">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46b12-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="46b12-118">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b12-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="46b12-119">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b12-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="46b12-120">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b12-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="46b12-121">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46b12-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
