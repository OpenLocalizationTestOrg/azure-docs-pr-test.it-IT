---
title: "Risoluzione dei problemi: Elemento \"Active Directory\" è mancante o non disponibile | Documenti Microsoft"
description: Operazioni da eseguire quando la voce di menu Active Directory non viene visualizzata nel portale di gestione di Azure.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="1dd9e-103">Risoluzione dei problemi: Voce "Active Directory" mancante o non disponibile</span><span class="sxs-lookup"><span data-stu-id="1dd9e-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="1dd9e-104">Per la maggior parte delle istruzioni relative all'uso delle funzionalità di Azure Active Directory è necessario accedere al portale di gestione di Azure e fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="1dd9e-105">Come procedere però se la voce di menu Active Directory non viene visualizzata o è contrassegnata come **Non disponibile**?</span><span class="sxs-lookup"><span data-stu-id="1dd9e-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="1dd9e-106">Questo argomento illustra come risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-106">This topic is designed to help.</span></span> <span data-ttu-id="1dd9e-107">Descrive inoltre le condizioni per cui la voce di menu **Active Directory** non viene visualizzata o non è disponibile e illustra le procedure da eseguire.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="1dd9e-108">Active Directory non disponibile</span><span class="sxs-lookup"><span data-stu-id="1dd9e-108">Active Directory is missing</span></span>
<span data-ttu-id="1dd9e-109">In genere la voce **Active Directory** viene visualizzata nel menu di navigazione sinistro.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="1dd9e-110">Le istruzioni relative alle procedure di Azure Active Directory presuppongono che questa voce sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Schermata: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="1dd9e-112">La voce Active Directory viene visualizzata nel menu di navigazione sinistro se si verifica una delle condizioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="1dd9e-113">In caso contrario, la voce non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="1dd9e-114">L'utente corrente ha effettuato l'accesso con un account Microsoft (in precedenza Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="1dd9e-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="1dd9e-115">OPPURE</span><span class="sxs-lookup"><span data-stu-id="1dd9e-115">OR</span></span>
* <span data-ttu-id="1dd9e-116">Il tenant di Azure ha una directory e l'account corrente è di tipo amministratore di directory.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="1dd9e-117">OPPURE</span><span class="sxs-lookup"><span data-stu-id="1dd9e-117">OR</span></span>
* <span data-ttu-id="1dd9e-118">Il tenant di Azure ha almeno uno spazio dei nomi di Azure AD Access Control (ACS).</span><span class="sxs-lookup"><span data-stu-id="1dd9e-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="1dd9e-119">Per altre informazioni, vedere [Spazio dei nomi di Access Control](https://msdn.microsoft.com/library/azure/gg185908.aspx)</span><span class="sxs-lookup"><span data-stu-id="1dd9e-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="1dd9e-120">OPPURE</span><span class="sxs-lookup"><span data-stu-id="1dd9e-120">OR</span></span>
* <span data-ttu-id="1dd9e-121">Il tenant di Azure ha almeno un provider di Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="1dd9e-122">Per altre informazioni, vedere [Amministrazione dei provider di Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1dd9e-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="1dd9e-123">Per creare uno spazio dei nomi di Access Control o un provider Multi-Factor Authentication, fare clic su **+Nuovo** > **Servizi app** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="1dd9e-124">Per ottenere diritti amministrativi per una directory, chiedere a un amministratore di assegnare un ruolo di amministratore al proprio account.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="1dd9e-125">Per informazioni dettagliate, vedere [Assegnazione dei ruoli di amministratore in Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1dd9e-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="1dd9e-126">Active Directory non è disponibile</span><span class="sxs-lookup"><span data-stu-id="1dd9e-126">Active Directory is not available</span></span>
<span data-ttu-id="1dd9e-127">Quando si fa clic su **+Nuovo** > **Servizi app**, viene visualizzata la voce **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="1dd9e-128">In particolare, questa voce viene visualizzata quando per l'utente corrente sono disponibili funzionalità di Active Directory, ad esempio Directory, Access Control o provider di Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="1dd9e-129">Tuttavia, durante il caricamento della pagina, la voce viene visualizzata in grigio ed è contrassegnata come **Non disponibile**.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="1dd9e-130">Questo stato è temporaneo.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-130">This is a temporary state.</span></span> <span data-ttu-id="1dd9e-131">Dopo alcuni secondi, la voce diventerà disponibile.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="1dd9e-132">Se il ritardo è prolungato, spesso il problema si risolve aggiornando la pagina Web.</span><span class="sxs-lookup"><span data-stu-id="1dd9e-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Schermata: Active Directory non disponibile](./media/active-directory-troubleshooting/not-available.png)

