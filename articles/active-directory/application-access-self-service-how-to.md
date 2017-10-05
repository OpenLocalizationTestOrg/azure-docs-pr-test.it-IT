---
title: Come configurare l'assegnazione di applicazioni self-service| Microsoft Docs
description: Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni
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
ms.openlocfilehash: 7991dc19d41c5eb8e149c3ee08069e1a162929cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-self-service-application-assignment"></a><span data-ttu-id="43947-103">Come configurare un'assegnazione di applicazioni self-service</span><span class="sxs-lookup"><span data-stu-id="43947-103">How to configure self-service application assignment</span></span>

<span data-ttu-id="43947-104">Prima che gli utenti possano da soli individuare le applicazioni dal pannello di accesso, è necessario abilitare l'**accesso alle applicazioni self-service** per tutte le applicazioni per cui si vuole consentire l'individuazione e l'accesso da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="43947-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="43947-105">Questa funzionalità è un modo efficace per consentire di risparmiare tempo e denaro al gruppo IT ed è altamente consigliata come parte di una distribuzione moderna di applicazioni con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43947-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="43947-106">Questa funzionalità permette di:</span><span class="sxs-lookup"><span data-stu-id="43947-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="43947-107">Consentire agli utenti di individuare da soli le applicazioni dal [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) senza dover contattare il gruppo IT.</span><span class="sxs-lookup"><span data-stu-id="43947-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="43947-108">Aggiungere gli utenti a un gruppo pre-configurato in modo che sia possibile verificare chi ha richiesto l'accesso, rimuovere l'accesso e gestire i ruoli assegnati.</span><span class="sxs-lookup"><span data-stu-id="43947-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="43947-109">Facoltativamente, consentire al revisore aziendale di approvare l'accesso alle applicazioni in modo da rimuovere questa azione dalle operazioni del gruppo IT.</span><span class="sxs-lookup"><span data-stu-id="43947-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="43947-110">Facoltativamente, configurare un massimo di 10 persone che possono approvare l'accesso a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="43947-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="43947-111">Facoltativamente consentire al revisore aziendale di impostare le password usate dagli utenti per accedere all'applicazione, direttamente dal [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) del revisore aziendale.</span><span class="sxs-lookup"><span data-stu-id="43947-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="43947-112">Facoltativamente, assegnare automaticamente gli utenti dell'accesso self-service direttamente a un ruolo applicazione.</span><span class="sxs-lookup"><span data-stu-id="43947-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="43947-113">Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="43947-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="43947-114">L'accesso alle applicazioni self-service è un modo efficace per consentire agli utenti di individuare da soli le applicazioni e, facoltativamente, al gruppo aziendale di approvare l'accesso a tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="43947-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="43947-115">È possibile consentire al gruppo aziendale di gestire le credenziali assegnate agli utenti per il diritto di accesso alle applicazioni Single Sign-On tramite password dal pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="43947-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="43947-116">Per abilitare l'accesso self-service per un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="43947-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="43947-117">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="43947-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="43947-118">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="43947-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="43947-119">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43947-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="43947-120">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43947-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="43947-121">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="43947-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="43947-122">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="43947-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="43947-123">Selezionare l'applicazione per cui si desidera abilitare l'accesso self-service dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="43947-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="43947-124">Dopo il caricamento dell'applicazione, fare clic su **Self-service** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43947-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="43947-125">Per abilitare l'accesso self-service per questa applicazione, impostare l'opzione **Consentire agli utenti di richiedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="43947-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="43947-126">Successivamente, per selezionare il gruppo al quale devono essere aggiunti gli utenti che richiedono l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Gruppo a cui devono essere aggiunti gli utenti assegnati** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="43947-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="43947-127">**Facoltativo:** se si desidera richiedere un'approvazione aziendale prima che venga consentito l'accesso agli utenti, impostare l'opzione **Richiedere l'approvazione prima di concedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="43947-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="43947-128">**Facoltativo: per applicazioni che usano solo l'accesso Single Sign-On tramite password,** se si desidera consentire ai responsabili approvazione aziendali di specificare le password inviate a questa applicazione per gli utenti approvati, impostare l'opzione **Consentire ai responsabili approvazione di impostare le password utente per questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="43947-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="43947-129">**Facoltativo:** per specificare i responsabili approvazione aziendali che possono approvare l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Utenti autorizzati ad approvare l'accesso a questa applicazione** per selezionare un massimo di 10 singoli responsabili approvazione aziendali.</span><span class="sxs-lookup"><span data-stu-id="43947-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   >[!NOTE]
   ><span data-ttu-id="43947-130">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="43947-130">Groups are not supported.</span></span>
   >
   >

13. <span data-ttu-id="43947-131">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera assegnare un ruolo agli utenti approvati self-service, fare clic sul selettore accanto all'opzione **A quale ruolo è necessario assegnare gli utenti in questa applicazione?** per selezionare il ruolo a cui devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="43947-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="43947-132">Per terminare, fare clic sul pulsante **Salva** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="43947-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="43947-133">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono accedere al [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic sul pulsante **+Aggiungi** per trovare le app per cui è stato abilitato l'accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="43947-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="43947-134">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="43947-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="43947-135">È possibile abilitare un messaggio di posta elettronica per informare i responsabili dell'approvazione quando un utente richiede l'accesso a un'applicazione per cui è necessaria l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="43947-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="43947-136">Tali approvazioni supportano solo flussi di lavoro di approvazione individuali. Se si specificano pertanto più responsabili approvazione, uno qualsiasi di esso potrà approvare l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43947-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43947-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43947-137">Next steps</span></span>
[<span data-ttu-id="43947-138">Configurazione di Azure Active Directory per la gestione self-service dei gruppi</span><span class="sxs-lookup"><span data-stu-id="43947-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
