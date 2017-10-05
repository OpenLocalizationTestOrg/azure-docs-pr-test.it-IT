---
title: "Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory | Microsoft Docs"
description: "Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 715fca79e488ae3759926181c244a42026f4a554
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="19113-103">Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19113-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="19113-104">Questo argomento è applicabile solo ai seguenti dispositivi:</span><span class="sxs-lookup"><span data-stu-id="19113-104">This topic is applicable only to the following devices:</span></span> 

- <span data-ttu-id="19113-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="19113-105">Windows 7</span></span> 
- <span data-ttu-id="19113-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="19113-106">Windows 8.1</span></span> 
- <span data-ttu-id="19113-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="19113-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="19113-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="19113-108">Windows Server 2012</span></span> 
- <span data-ttu-id="19113-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="19113-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="19113-110">Per Windows 10 o Windows Server 2016, vedere [Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="19113-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="19113-111">Questo argomento presuppone che siano stati [configurati dispositivi aggiunti all'identità ibrida di Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) per supportare gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="19113-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="19113-112">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="19113-112">Device-based conditional access</span></span>

- [<span data-ttu-id="19113-113">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="19113-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="19113-114">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="19113-114">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span> 





<span data-ttu-id="19113-115">Questo argomento fornisce indicazioni sulla risoluzione di potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="19113-115">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  

<span data-ttu-id="19113-116">**Informazioni utili:**</span><span class="sxs-lookup"><span data-stu-id="19113-116">**What you should know:**</span></span> 

- <span data-ttu-id="19113-117">Il numero massimo di dispositivi per utente è incentrato sui dispositivi.</span><span class="sxs-lookup"><span data-stu-id="19113-117">The maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="19113-118">Ad esempio: se *jdoe* e *jharnett* accedono a questo dispositivo, viene creata una registrazione separata (DeviceID) per ciascuno di questi utenti nella scheda di informazioni **UTENTE**.</span><span class="sxs-lookup"><span data-stu-id="19113-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span></span>  

- <span data-ttu-id="19113-119">La registrazione/aggiunta iniziale dei dispositivi è configurata in modo da eseguire un tentativo di accesso o blocco/sblocco.</span><span class="sxs-lookup"><span data-stu-id="19113-119">The initial registration / join of devices is configured to perform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="19113-120">Potrebbero esserci 5 minuti di ritardo causati da un'attività dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="19113-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="19113-121">Una reinstallazione del sistema operativo o l'annullamento e la ripetizione manuale della registrazione potrebbe creare una nuova registrazione in Azure AD e causare la presenza di più voci nella scheda Info UTENTE nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19113-121">A reinstall of the operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="19113-122">Passaggio 1: Recuperare lo stato della registrazione</span><span class="sxs-lookup"><span data-stu-id="19113-122">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="19113-123">**Per verificare lo stato della registrazione**</span><span class="sxs-lookup"><span data-stu-id="19113-123">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="19113-124">Aprire il prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="19113-124">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="19113-125">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="19113-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="19113-126">Questo comando consente di visualizzare una finestra di dialogo che fornisce altri dettagli relativi allo stato delle aggiunte.</span><span class="sxs-lookup"><span data-stu-id="19113-126">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a><span data-ttu-id="19113-128">Passaggio 2: Valutare lo stato delle aggiunte all'identità ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19113-128">Step 2: Evaluate the hybrid Azure AD join status</span></span> 

<span data-ttu-id="19113-129">Se l'aggiunta all'identità ibrida di Azure AD non è stata completata correttamente, la finestra di dialogo fornisce dettagli sul problema che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="19113-129">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span></span>

<span data-ttu-id="19113-130">**I problemi più comuni sono:**</span><span class="sxs-lookup"><span data-stu-id="19113-130">**The most common issues are:**</span></span>

- <span data-ttu-id="19113-131">Una configurazione errata di AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="19113-131">A misconfigured AD FS or Azure AD</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="19113-133">Non si è connessi come utente di dominio</span><span class="sxs-lookup"><span data-stu-id="19113-133">You are not signed on as a domain user</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="19113-135">È stata raggiunta una quota</span><span class="sxs-lookup"><span data-stu-id="19113-135">A quota has been reached</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="19113-137">Il servizio non risponde</span><span class="sxs-lookup"><span data-stu-id="19113-137">The service is not responding</span></span> 

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="19113-139">È inoltre possibile trovare le informazioni sullo stato nel registro eventi in **Registri applicazioni e servizi\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="19113-139">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="19113-140">**Le cause più comuni di un'aggiunta all'identità ibrida di Azure AD non riuscita sono:**</span><span class="sxs-lookup"><span data-stu-id="19113-140">**The most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="19113-141">Il computer non è presente nella rete interna dell'organizzazione o c'è una VPN senza connessione su un controller di dominio locale AD.</span><span class="sxs-lookup"><span data-stu-id="19113-141">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="19113-142">Si è connessi al computer con un account computer locale.</span><span class="sxs-lookup"><span data-stu-id="19113-142">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="19113-143">Problemi di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="19113-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="19113-144">Il server federativo è stato configurato per supportare **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="19113-144">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="19113-145">Non è presente alcun oggetto Punto di connessione del servizio che punti al nome di dominio verificato in Azure AD nella foresta AD a cui appartiene il computer.</span><span class="sxs-lookup"><span data-stu-id="19113-145">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="19113-146">Un utente ha raggiunto il limite di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="19113-146">A user has reached the limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="19113-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19113-147">Next steps</span></span>

<span data-ttu-id="19113-148">Per altre informazioni, vedere le [domande frequenti sulla gestione dei dispositivi](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="19113-148">For questions, see the [device management FAQ](device-management-faq.md)</span></span>  
