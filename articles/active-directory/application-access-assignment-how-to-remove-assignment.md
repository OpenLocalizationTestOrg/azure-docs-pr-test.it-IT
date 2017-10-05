---
title: Come rimuovere l'accesso di un utente a un'applicazione | Microsoft Docs
description: Comprendere come rimuovere l'accesso di un utente a un'applicazione
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="9f309-103">Come rimuovere l'accesso di un utente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="9f309-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="9f309-104">Questo articolo consente di comprendere come rimuovere l'accesso di un utente a un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9f309-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="9f309-105">Si desidera rimuovere un'assegnazione specifica di un utente o gruppo a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="9f309-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="9f309-106">Per rimuovere un'assegnazione di un utente o di un gruppo da un'applicazione, seguire la procedura indicata nell'articolo [Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9f309-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="9f309-107">Si desidera disabilitare tutti gli accessi a un'applicazione per tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="9f309-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="9f309-108">Per disabilitare tutti gli accessi utente a un'applicazione, seguire la procedura indicata nell'articolo [Disabilitare gli accessi utente per un'app aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9f309-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="9f309-109">Si vuole eliminare completamente un'applicazione</span><span class="sxs-lookup"><span data-stu-id="9f309-109">I want to delete an application entirely</span></span>

<span data-ttu-id="9f309-110">Per **eliminare un'applicazione**, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="9f309-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="9f309-111">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="9f309-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f309-112">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9f309-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f309-113">Digitare **"Azure Active Directory"** nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f309-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f309-114">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f309-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f309-115">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9f309-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9f309-116">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9f309-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f309-117">Selezionare l'applicazione che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="9f309-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="9f309-118">Dopo il caricamento dell'applicazione, fare clic sull'icona **Elimina** che si trova nella parte superiore del pannello **Panoramica** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9f309-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="9f309-119">Si vuole disabilitare tutte le operazioni future di consenso da parte dell'utente a tutte le applicazioni</span><span class="sxs-lookup"><span data-stu-id="9f309-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="9f309-120">La disabilitazione di consenso da parte dell'utente per l'intera directory impedisce agli utenti finali di consentire l'accesso a qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="9f309-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="9f309-121">Gli amministratori possono sempre dare consenso per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9f309-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="9f309-122">Per informazioni sul consenso alle applicazioni e sui motivi per cui si desideri dare o meno consenso, leggere [Informazioni sul consenso dell'utente e dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="9f309-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="9f309-123">Per **disabilitare tutte le operazioni future di consenso degli utenti nella directory intera**, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="9f309-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="9f309-124">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="9f309-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9f309-125">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9f309-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f309-126">Digitare **"Azure Active Directory"** nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f309-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f309-127">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="9f309-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9f309-128">Fare clic su **Impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="9f309-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="9f309-129">Disabilitare tutte le future operazioni di consenso degli utenti impostando l'opzione **Gli utenti possono consentire alle app di accedere ai propri dati** su **No**, quindi fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9f309-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="9f309-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f309-130">Next steps</span></span>
[<span data-ttu-id="9f309-131">Gestione dell'accesso alle app</span><span class="sxs-lookup"><span data-stu-id="9f309-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
