---
title: Errore durante l'accesso alle applicazioni self-service | Microsoft Docs
description: Risoluzione dei problemi relativi all'accesso alle applicazioni self-service
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
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="6c8b8-103">Errore durante l'accesso alle applicazioni self-service</span><span class="sxs-lookup"><span data-stu-id="6c8b8-103">Problem using self-service application access</span></span>

<span data-ttu-id="6c8b8-104">L'accesso alle applicazioni self-service è un modo efficace per consentire agli utenti di individuare da soli le applicazioni e, facoltativamente, al gruppo aziendale di approvare l'accesso a tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="6c8b8-105">È possibile consentire al gruppo aziendale di gestire le credenziali assegnate agli utenti per il diritto di accesso alle applicazioni Single Sign-On tramite password dal pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="6c8b8-106">Prima che gli utenti possano da soli individuare le applicazioni dal pannello di accesso, è necessario abilitare l'**accesso alle applicazioni self-service** per tutte le applicazioni per cui si desidera consentire l'individuazione e l'accesso da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="6c8b8-107">Problemi generali da verificare inizialmente</span><span class="sxs-lookup"><span data-stu-id="6c8b8-107">General issues to check first</span></span>

-   <span data-ttu-id="6c8b8-108">Assicurarsi che l'accesso alle applicazioni self-service sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="6c8b8-109">Consultare "Come configurare l'accesso alle applicazioni self-service".</span><span class="sxs-lookup"><span data-stu-id="6c8b8-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="6c8b8-110">Assicurarsi che l'utente o il gruppo sia stato abilitato per richiedere l'accesso alle applicazioni self-service.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="6c8b8-111">Assicurarsi che l'utente stia visitando la posizione corretta per l'accesso alle applicazioni self-service.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="6c8b8-112">Gli utenti possono accedere al [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic sul pulsante **+Aggiungi** per trovare le app per cui è stato abilitato l'accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="6c8b8-113">Se di recente è stato configurato l'accesso alle applicazioni self-service, provare ad accedere e a uscire nuovamente dal Pannello di accesso dell'utente dopo alcuni minuti per vedere se le modifiche dell'accesso self-service vengono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="6c8b8-114">Come configurare l'accesso alle applicazioni self-service</span><span class="sxs-lookup"><span data-stu-id="6c8b8-114">How to configure self-service application access</span></span>

<span data-ttu-id="6c8b8-115">Per abilitare l'accesso self-service per un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6c8b8-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="6c8b8-116">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6c8b8-117">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6c8b8-118">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6c8b8-119">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6c8b8-120">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="6c8b8-121">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6c8b8-122">Selezionare l'applicazione per cui si desidera abilitare l'accesso self-service dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="6c8b8-123">Dopo il caricamento dell'applicazione, fare clic su **Self-service** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6c8b8-124">Per abilitare l'accesso self-service per questa applicazione, impostare l'opzione **Consentire agli utenti di richiedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="6c8b8-125">Successivamente, per selezionare il gruppo al quale devono essere aggiunti gli utenti che richiedono l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Gruppo a cui devono essere aggiunti gli utenti assegnati** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="6c8b8-126">**Facoltativo:** se si desidera richiedere un'approvazione aziendale prima che venga consentito l'accesso agli utenti, impostare l'opzione **Richiedere l'approvazione prima di concedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="6c8b8-127">**Facoltativo: per applicazioni che usano solo l'accesso Single Sign-On tramite password,** se si desidera consentire ai responsabili approvazione aziendali di specificare le password inviate a questa applicazione per gli utenti approvati, impostare l'opzione **Consentire ai responsabili approvazione di impostare le password utente per questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="6c8b8-128">**Facoltativo:** per specificare i responsabili approvazione aziendali che possono approvare l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Utenti autorizzati ad approvare l'accesso a questa applicazione** per selezionare un massimo di 10 singoli responsabili approvazione aziendali.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="6c8b8-129">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="6c8b8-130">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera assegnare un ruolo agli utenti approvati self-service, fare clic sul selettore accanto all'opzione **A quale ruolo è necessario assegnare gli utenti in questa applicazione?** per selezionare il ruolo a cui devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="6c8b8-131">Per terminare, fare clic sul pulsante **Salva** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="6c8b8-132">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono accedere al [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic sul pulsante **+Aggiungi** per trovare le app per cui è stato abilitato l'accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="6c8b8-133">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6c8b8-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="6c8b8-134">È possibile abilitare un messaggio di posta elettronica per informare i responsabili dell'approvazione quando un utente richiede l'accesso a un'applicazione per cui è necessaria l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="6c8b8-135">Tali approvazioni supportano solo flussi di lavoro di approvazione individuali. Se si specificano pertanto più responsabili approvazione, uno qualsiasi di essi potrà approvare l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c8b8-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="6c8b8-136">Se questi passaggi per la risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="6c8b8-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="6c8b8-137">Aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="6c8b8-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="6c8b8-138">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="6c8b8-138">Correlation error ID</span></span>

-   <span data-ttu-id="6c8b8-139">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="6c8b8-139">UPN (user email address)</span></span>

-   <span data-ttu-id="6c8b8-140">ID tenant</span><span class="sxs-lookup"><span data-stu-id="6c8b8-140">TenantID</span></span>

-   <span data-ttu-id="6c8b8-141">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="6c8b8-141">Browser type</span></span>

-   <span data-ttu-id="6c8b8-142">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="6c8b8-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="6c8b8-143">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="6c8b8-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c8b8-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c8b8-144">Next steps</span></span>
[<span data-ttu-id="6c8b8-145">Configurazione di Azure Active Directory per la gestione self-service dei gruppi</span><span class="sxs-lookup"><span data-stu-id="6c8b8-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
