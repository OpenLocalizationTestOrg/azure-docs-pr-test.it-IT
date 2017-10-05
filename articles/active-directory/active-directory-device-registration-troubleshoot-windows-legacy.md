---
title: Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows | Documentazione Microsoft
description: Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows.
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="73133-103">Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio in Azure AD per client di livello inferiore di Windows</span><span class="sxs-lookup"><span data-stu-id="73133-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="73133-104">Questo argomento è applicabile solo ai seguenti client:</span><span class="sxs-lookup"><span data-stu-id="73133-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="73133-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="73133-105">Windows 7</span></span> 
- <span data-ttu-id="73133-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="73133-106">Windows 8.1</span></span> 
- <span data-ttu-id="73133-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="73133-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="73133-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="73133-108">Windows Server 2012</span></span> 
- <span data-ttu-id="73133-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="73133-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="73133-110">Per Windows 10 o Windows Server 2016, vedere [Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="73133-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="73133-111">Questo argomento presuppone che la registrazione automatica dei dispositivi aggiunti a un dominio sia stata configurata come descritto in [Come configurare la registrazione automatica dei dispositivi aggiunti al dominio di Windows con Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="73133-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="73133-112">Questo argomento fornisce indicazioni sulla risoluzione di potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="73133-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="73133-113">Alcuni aspetti da tenere presente per risultati positivi:</span><span class="sxs-lookup"><span data-stu-id="73133-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="73133-114">La registrazione di questi client su Azure AD è per utente/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73133-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="73133-115">Ad esempio: se jdoe e jharnett accedono a questo dispositivo, viene creata una registrazione separata (DeviceID) per ciascuno di questi utenti nella scheda Info UTENTE.</span><span class="sxs-lookup"><span data-stu-id="73133-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="73133-116">La registrazione di questi client predefiniti è configurata per essere verificata all'accesso o al blocco/sblocco ed è possibile attivare un ritardo di 5 minuti mediante l'Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="73133-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="73133-117">Una reinstallazione del sistema operativo o l'annullamento e la ripetizione manuale della registrazione potrebbe creare una nuova registrazione in Azure AD e avrà come risultato la presenza di più voci nella scheda Info UTENTE nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="73133-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="73133-118">Passaggio 1: Recuperare lo stato della registrazione</span><span class="sxs-lookup"><span data-stu-id="73133-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="73133-119">**Per verificare lo stato della registrazione**</span><span class="sxs-lookup"><span data-stu-id="73133-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="73133-120">Aprire il prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="73133-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="73133-121">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="73133-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="73133-122">Questo comando consente di visualizzare una finestra di dialogo che fornisce altri dettagli relativi allo stato delle aggiunte.</span><span class="sxs-lookup"><span data-stu-id="73133-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="73133-124">Passaggio 2: Valutare lo stato della registrazione</span><span class="sxs-lookup"><span data-stu-id="73133-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="73133-125">Se l'aggiunta non è avvenuta correttamente, la finestra di dialogo fornisce dettagli sul problema che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="73133-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="73133-126">**I problemi più comuni sono:**</span><span class="sxs-lookup"><span data-stu-id="73133-126">**The most common issues are:**</span></span>

- <span data-ttu-id="73133-127">Una configurazione errata di AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="73133-127">A misconfigured AD FS or Azure AD</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="73133-129">Non si è connessi come utente di dominio</span><span class="sxs-lookup"><span data-stu-id="73133-129">You are not signed on as a domain user</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="73133-131">È stata raggiunta una quota</span><span class="sxs-lookup"><span data-stu-id="73133-131">A quota has been reached</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="73133-133">Il servizio non risponde</span><span class="sxs-lookup"><span data-stu-id="73133-133">The service is not responding</span></span> 

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="73133-135">È inoltre possibile trovare le informazioni sullo stato nel registro eventi in **Registri applicazioni e servizi\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="73133-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="73133-136">**Le cause più comuni di una registrazione non riuscita sono:**</span><span class="sxs-lookup"><span data-stu-id="73133-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="73133-137">Il computer non è presente nella rete interna dell'organizzazione o c'è una VPN senza connessione su un controller di dominio locale AD.</span><span class="sxs-lookup"><span data-stu-id="73133-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="73133-138">Si è connessi al computer con un account computer locale.</span><span class="sxs-lookup"><span data-stu-id="73133-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="73133-139">Problemi di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="73133-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="73133-140">Il server federativo è stato configurato per supportare **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="73133-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="73133-141">Non è presente alcun oggetto Punto di connessione del servizio che punti al nome di dominio verificato in Azure AD nella foresta AD a cui appartiene il computer.</span><span class="sxs-lookup"><span data-stu-id="73133-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="73133-142">Un utente ha raggiunto il limite di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="73133-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="73133-143">Vedere Introduzione a Registrazione dispositivo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73133-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73133-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73133-144">Next steps</span></span>

<span data-ttu-id="73133-145">Per ulteriori informazioni, vedere [Domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="73133-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
