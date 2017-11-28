---
title: aaaTroubleshooting hello-registrazione automatica del dominio di Azure AD aggiunti a un computer per i client legacy di Windows | Documenti Microsoft
description: Risoluzione dei problemi di registrazione automatica hello del dominio di Azure AD aggiunti a un computer per i client legacy di Windows.
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="8a15f-103">Risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows</span><span class="sxs-lookup"><span data-stu-id="8a15f-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="8a15f-104">In questo argomento è applicabile toohello solo i client seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a15f-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="8a15f-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8a15f-105">Windows 7</span></span> 
- <span data-ttu-id="8a15f-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8a15f-106">Windows 8.1</span></span> 
- <span data-ttu-id="8a15f-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="8a15f-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="8a15f-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8a15f-108">Windows Server 2012</span></span> 
- <span data-ttu-id="8a15f-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8a15f-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="8a15f-110">Per Windows 10 o Windows Server 2016, vedere [risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure Active Directory-i computer Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="8a15f-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="8a15f-111">Questo argomento si presuppone di aver configurato la registrazione automatica dei dispositivi appartenenti a un dominio come descritto in descritto in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a15f-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="8a15f-112">In questo argomento fornisce informazioni aggiuntive su come tooresolve potenziali problemi di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="8a15f-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="8a15f-113">Toonote alcune operazioni per i risultati positivi:</span><span class="sxs-lookup"><span data-stu-id="8a15f-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="8a15f-114">La registrazione di questi client su Azure AD è per utente/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a15f-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="8a15f-115">Ad esempio: se jdoe e jharnett Accedi toothis dispositivo, una registrazione separati (DeviceID) viene creata per ciascuno di questi utenti nella scheda informazioni utente di hello.</span><span class="sxs-lookup"><span data-stu-id="8a15f-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="8a15f-116">Registrazione di questi client non viene fornita hello è configurato tootry all'accesso o bloccare/sbloccare e si può verificare che questa azione viene attivata utilizzando un'utilità di pianificazione attività ritardo di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="8a15f-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="8a15f-117">La reinstallazione del sistema operativo hello o annullare la registrazione manuale e ripetere la registrazione potrebbe creare una nuova registrazione in Azure AD e determinerà più voci nella scheda informazioni utente di hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a15f-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="8a15f-118">Passaggio 1: Recuperare lo stato della registrazione hello</span><span class="sxs-lookup"><span data-stu-id="8a15f-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="8a15f-119">**stato della registrazione tooverify hello:**</span><span class="sxs-lookup"><span data-stu-id="8a15f-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="8a15f-120">Hello Apri prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="8a15f-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="8a15f-121">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="8a15f-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="8a15f-122">Questo comando Visualizza una finestra di dialogo che fornisce le informazioni più dettagliate sullo stato di join di hello.</span><span class="sxs-lookup"><span data-stu-id="8a15f-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="8a15f-124">Passaggio 2: Valutare lo stato della registrazione hello</span><span class="sxs-lookup"><span data-stu-id="8a15f-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="8a15f-125">Se il join di hello non ha esito positivo, la finestra di dialogo hello fornisce dettagli sul problema hello che si è verificato.</span><span class="sxs-lookup"><span data-stu-id="8a15f-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="8a15f-126">**Hello i problemi più comuni sono:**</span><span class="sxs-lookup"><span data-stu-id="8a15f-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="8a15f-127">Una configurazione errata di AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a15f-127">A misconfigured AD FS or Azure AD</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="8a15f-129">Non si è connessi come utente di dominio</span><span class="sxs-lookup"><span data-stu-id="8a15f-129">You are not signed on as a domain user</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="8a15f-131">È stata raggiunta una quota</span><span class="sxs-lookup"><span data-stu-id="8a15f-131">A quota has been reached</span></span>

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="8a15f-133">servizio Hello non risponde</span><span class="sxs-lookup"><span data-stu-id="8a15f-133">hello service is not responding</span></span> 

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="8a15f-135">È inoltre possibile trovare informazioni sullo stato hello nel registro eventi di hello in **all'area di lavoro di Log\Microsoft servizi e applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8a15f-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="8a15f-136">**le cause più comuni per una registrazione non riuscita Hello sono:**</span><span class="sxs-lookup"><span data-stu-id="8a15f-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="8a15f-137">Il computer non si trova nella rete interna dell'organizzazione hello o una connessione VPN senza connessione tooan locale controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a15f-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="8a15f-138">Si è connessi in computer tooyour con un account computer locale.</span><span class="sxs-lookup"><span data-stu-id="8a15f-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="8a15f-139">Problemi di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="8a15f-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="8a15f-140">Hello server federativo è stato configurato toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="8a15f-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="8a15f-141">È presente alcun oggetto di punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello.</span><span class="sxs-lookup"><span data-stu-id="8a15f-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="8a15f-142">Un utente ha raggiunto il limite di hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8a15f-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="8a15f-143">Vedere Introduzione a Registrazione dispositivo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a15f-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a15f-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a15f-144">Next steps</span></span>

<span data-ttu-id="8a15f-145">Per ulteriori informazioni, vedere hello [domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="8a15f-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
