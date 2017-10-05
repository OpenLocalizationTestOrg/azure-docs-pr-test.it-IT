---
title: Gruppi dedicati in Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="c9d59-103">Gruppi dedicati in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d59-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="c9d59-104">In Azure Active Directory (Azure AD), la funzionalità gruppi dedicati crea e popola automaticamente l'appartenenza per gruppi di Azure AD predefiniti.</span><span class="sxs-lookup"><span data-stu-id="c9d59-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="c9d59-105">Non è possibile aggiungere o rimuovere membri nei gruppi dedicati tramite il portale di Azure classico, i cmdlet di Windows PowerShell oppure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="c9d59-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d59-106">I gruppi dedicati richiedono che venga assegnata una licenza Azure AD Premium a:</span><span class="sxs-lookup"><span data-stu-id="c9d59-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="c9d59-107">l'amministratore che gestisce la regola in un gruppo</span><span class="sxs-lookup"><span data-stu-id="c9d59-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="c9d59-108">tutti gli utenti che vengono selezionati in base alla regola come membro del gruppo</span><span class="sxs-lookup"><span data-stu-id="c9d59-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="c9d59-109">**Per abilitare i gruppi dedicati**</span><span class="sxs-lookup"><span data-stu-id="c9d59-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="c9d59-110">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c9d59-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="c9d59-111">Selezionare la scheda **Gruppi** e aprire il gruppo da modificare.</span><span class="sxs-lookup"><span data-stu-id="c9d59-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="c9d59-112">Selezionare la scheda **Configura** e impostare **Abilita gruppi dedicati** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c9d59-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="c9d59-113">Dopo aver impostato l'opzione Abilita gruppi dedicati su **Sì**, è anche possibile consentire alla directory di creare automaticamente il gruppo dedicato Tutti gli utenti impostando l'opzione **Abilita il gruppo "Tutti gli utenti"** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c9d59-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="c9d59-114">È quindi possibile modificare il nome di questo gruppo dedicato digitando il nuovo nome nel campo **Nome visualizzato per il gruppo “Tutti gli utenti”** .</span><span class="sxs-lookup"><span data-stu-id="c9d59-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="c9d59-115">Il gruppo Tutti gli utenti può essere usato per assegnare le stesse autorizzazioni a tutti gli utenti in una directory.</span><span class="sxs-lookup"><span data-stu-id="c9d59-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="c9d59-116">Ad esempio, è possibile consentire a tutti gli utenti di una directory di accedere a un'applicazione SaaS tramite l'assegnazione dell'accesso a tale applicazione al gruppo dedicato Tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c9d59-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="c9d59-117">Il gruppo Tutti gli utenti include tutti gli utenti della directory, compresi gli utenti guest e gli utenti esterni.</span><span class="sxs-lookup"><span data-stu-id="c9d59-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="c9d59-118">Se è necessario un gruppo che esclude gli utenti esterni, è possibile creare un gruppo con una regola dinamica basata su attributi come la seguente:</span><span class="sxs-lookup"><span data-stu-id="c9d59-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="c9d59-119">Per un gruppo che esclude tutti gli utenti guest, usare una regola come la seguente:</span><span class="sxs-lookup"><span data-stu-id="c9d59-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="c9d59-120">Per informazioni su come creare regole *avanzate* (ovvero regole che possono contenere più confronti) per l'appartenenza dinamica ai gruppi, vedere [Uso di attributi per la creazione di regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c9d59-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="c9d59-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9d59-121">Next steps</span></span>
<span data-ttu-id="c9d59-122">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9d59-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c9d59-123">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d59-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c9d59-124">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d59-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c9d59-125">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d59-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c9d59-126">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9d59-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
