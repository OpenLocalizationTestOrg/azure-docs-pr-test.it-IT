---
title: aaaDedicated gruppi in Azure Active Directory | Documenti Microsoft
description: Panoramica del funzionamento dei gruppi dedicati in Azure Active Directory e della loro creazione.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="ab30d-103">Gruppi dedicati in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab30d-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="ab30d-104">In Azure Active Directory (Azure AD), funzionalità di gruppi dedicati hello creati e popolati automaticamente l'appartenenza a gruppi di Azure Active Directory predefinito.</span><span class="sxs-lookup"><span data-stu-id="ab30d-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="ab30d-105">Non è possibile aggiungere i membri di gruppi dedicati o rimosso utilizzando hello Azure classico portale, cmdlet di Windows PowerShell, o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="ab30d-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="ab30d-106">I gruppi dedicati richiedono che venga assegnata una licenza Azure AD Premium a:</span><span class="sxs-lookup"><span data-stu-id="ab30d-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="ab30d-107">messaggio per l'amministratore che gestisce la regola hello in un gruppo</span><span class="sxs-lookup"><span data-stu-id="ab30d-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="ab30d-108">tutti gli utenti che sono selezionati per hello regola toobe un membro del gruppo di hello</span><span class="sxs-lookup"><span data-stu-id="ab30d-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="ab30d-109">**gruppi tooenable dedicato**</span><span class="sxs-lookup"><span data-stu-id="ab30d-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="ab30d-110">In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="ab30d-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="ab30d-111">Seleziona hello **gruppi** scheda e quindi aprire hello gruppo tooedit.</span><span class="sxs-lookup"><span data-stu-id="ab30d-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="ab30d-112">Seleziona hello **configura** scheda e quindi impostare **Abilita gruppi dedicati** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="ab30d-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="ab30d-113">Dopo aver impostato troppo hello abilitazione dei gruppi dedicati passare**Sì**, è possibile abilitare hello directory tooautomatically creare gruppo dedicato di hello tutti gli utenti dall'impostazione hello **"tutti gli utenti" gruppo** opzione troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="ab30d-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="ab30d-114">Quindi è possibile inoltre modificare il nome di hello di questo gruppo dedicato digitandolo nel hello **nome visualizzato per "All Users" gruppo** campo.</span><span class="sxs-lookup"><span data-stu-id="ab30d-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="ab30d-115">è possibile utilizzare il gruppo di tutti gli utenti Hello tooassign hello stesso autorizzazioni tooall hello utenti della directory.</span><span class="sxs-lookup"><span data-stu-id="ab30d-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="ab30d-116">Ad esempio, è possibile concedere tutti gli utenti in tooa di accesso la directory applicazione SaaS per l'assegnazione dell'accesso per tutti gli utenti gruppo dedicato toothis applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ab30d-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="ab30d-117">gruppo di tutti gli utenti Hello dedicato include tutti gli utenti nella directory di hello, inclusi i guest e gli utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="ab30d-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="ab30d-118">Se è necessario un gruppo che consente di escludere gli utenti esterni, quindi questo scopo, è possibile la creazione di un gruppo con una regola dinamica basato su attributi quali seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="ab30d-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="ab30d-119">Per un gruppo che esclude tutti i guest, usare una regola, come illustrato di seguito hello:</span><span class="sxs-lookup"><span data-stu-id="ab30d-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="ab30d-120">toolearn sulla toocreate *avanzate* regole, che può contenere più confronti, per l'appartenenza dinamica ai gruppi, vedere [utilizzando attributi toocreate regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="ab30d-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="ab30d-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab30d-121">Next steps</span></span>
<span data-ttu-id="ab30d-122">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab30d-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="ab30d-123">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab30d-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="ab30d-124">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab30d-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ab30d-125">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab30d-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="ab30d-126">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab30d-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
