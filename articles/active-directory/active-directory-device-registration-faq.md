---
title: domande frequenti sulla registrazione automatica dei dispositivi di Active Directory aaaAzure | Documenti Microsoft
description: Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory.
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
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="518af-103">Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="518af-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="518af-104">**D: registrazione dispositivo di hello recentemente. Impossibile visualizzare dispositivo hello in mie info di utente nel portale di Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="518af-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="518af-105">**R:** i dispositivi Windows 10 che appartengono a un dominio con la registrazione automatica del dispositivo non vengono visualizzati nelle informazioni utente hello.</span><span class="sxs-lookup"><span data-stu-id="518af-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="518af-106">È necessario toouse PowerShell toosee tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="518af-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="518af-107">Solo hello dispositivi seguenti sono elencati sotto informazioni utente hello:</span><span class="sxs-lookup"><span data-stu-id="518af-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="518af-108">Tutti i dispositivi personali non aggiunti a un dominio aziendale</span><span class="sxs-lookup"><span data-stu-id="518af-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="518af-109">Tutti i dispositivi non Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="518af-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="518af-110">Tutti i dispositivi non Windows</span><span class="sxs-lookup"><span data-stu-id="518af-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="518af-111">**D: perché non visualizzare tutti i dispositivi di hello registrati in Azure Active Directory nel portale di Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="518af-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="518af-112">**R:** attualmente non è disponibile alcun toosee modo tutti i dispositivi registrati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="518af-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="518af-113">È possibile usare Azure PowerShell toofind tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="518af-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="518af-114">Per ulteriori informazioni, vedere hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="518af-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="518af-115">**D: come si capisce quali lo stato di registrazione dispositivo hello del client hello è?**</span><span class="sxs-lookup"><span data-stu-id="518af-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="518af-116">**R:** varia a seconda dello stato di registrazione dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="518af-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="518af-117">Il dispositivo hello è</span><span class="sxs-lookup"><span data-stu-id="518af-117">What hello device is</span></span>
- <span data-ttu-id="518af-118">Modalità di registrazione</span><span class="sxs-lookup"><span data-stu-id="518af-118">How it was registered</span></span> 
- <span data-ttu-id="518af-119">I dettagli correlati tooit.</span><span class="sxs-lookup"><span data-stu-id="518af-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="518af-120">**D: perché è un dispositivo eliminato in hello Azure portal o con Windows PowerShell ancora elencati come registrato?**</span><span class="sxs-lookup"><span data-stu-id="518af-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="518af-121">**A:** Si tratta di un comportamento previsto da progettazione.</span><span class="sxs-lookup"><span data-stu-id="518af-121">**A:** This is by design.</span></span> <span data-ttu-id="518af-122">dispositivo Hello non avranno accesso tooresources nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="518af-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="518af-123">Se si desidera tooremove hello dispositivo e ripetere la registrazione, un'azione manuale deve essere eseguita sul dispositivo hello toobe.</span><span class="sxs-lookup"><span data-stu-id="518af-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="518af-124">Per i dispositivi Windows 10 e Windows Server 2016 aggiunti a un dominio AD locale:</span><span class="sxs-lookup"><span data-stu-id="518af-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="518af-125">Aprire il prompt dei comandi di hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="518af-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="518af-126">Digitare `dsregcmd.exe /debug /leave`.</span><span class="sxs-lookup"><span data-stu-id="518af-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="518af-127">Disconnetti e Accedi tootrigger hello attività pianificata che registra il dispositivo hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="518af-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="518af-128">Per altre piattaforme Windows aggiunte a un dominio AD locale:</span><span class="sxs-lookup"><span data-stu-id="518af-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="518af-129">Aprire il prompt dei comandi di hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="518af-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="518af-130">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="518af-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="518af-131">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="518af-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="518af-132">**D: Perché vengono visualizzate voci di dispositivo duplicate nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="518af-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="518af-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="518af-133">**A:**</span></span>

-   <span data-ttu-id="518af-134">Per Windows 10 e Windows Server 2016, se vengono ripetuti tentativi toounjoin e aggiungere nuovamente hello stesso dispositivo, potrebbero essere presenti voci duplicate.</span><span class="sxs-lookup"><span data-stu-id="518af-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="518af-135">Se si utilizza Aggiungi Account aziendale o dell'istituto di istruzione, ogni utente di windows che utilizza Aggiungi Account aziendale o dell'istituto di istruzione verrà creato un nuovo record di dispositivo con hello dello stesso nome dispositivo.</span><span class="sxs-lookup"><span data-stu-id="518af-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="518af-136">Altre piattaforme di Windows che sono locali AD appartenenti a un dominio utilizzando la registrazione automatica verrà creato un nuovo record di dispositivo con hello dello stesso nome di dispositivo per ogni utente di dominio che accede al dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="518af-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="518af-137">Una macchina AADJ che è stata cancellata, reinstallato e nuovamente aggiunti con hello stesso nome, verrà visualizzato come un altro record con hello dello stesso nome dispositivo.</span><span class="sxs-lookup"><span data-stu-id="518af-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="518af-138">**D: perché è un utente ancora accedere alle risorse da un dispositivo che è stato disabilitato in hello portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="518af-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="518af-139">**R:** può richiedere fino a ora tooan per un toobe revoke applicato.</span><span class="sxs-lookup"><span data-stu-id="518af-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="518af-140">Per i dispositivi persi, è consigliabile cancellazione hello dispositivo tooensure che gli utenti non possono accedere dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="518af-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="518af-141">Per altre informazioni, vedere , vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="518af-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="518af-142">**D: Perché viene visualizzato un messaggio che avvisa dell'impossibilità di raggiungere un determinato dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="518af-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="518af-143">**R:** se è stato configurato determinati toorequire di regole di accesso condizionale uno stato di dispositivi specifici e hello dispositivo non soddisfa i criteri di hello, gli utenti vengono bloccati e visualizzare questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="518af-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="518af-144">Valutazione delle regole di hello e verificare che il dispositivo hello è in grado di toomeet hello criteri tooavoid questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="518af-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="518af-145">**D: Vedere record del dispositivo hello nelle informazioni utente hello in hello portale di Azure e visualizzare lo stato di hello registrate nel client hello. La configurazione è corretta per l'uso dell'accesso condizionale?**</span><span class="sxs-lookup"><span data-stu-id="518af-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="518af-146">**R:** record del dispositivo hello (deviceID) e stato nel portale di Azure hello deve corrispondere client hello e soddisfare i criteri di valutazione per l'accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="518af-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="518af-147">Per altre informazioni, vedere [Introduzione a Registrazione dispositivo Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="518af-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="518af-148">**D: perché viene visualizzato un messaggio "nome utente o password non corretta" per un dispositivo è stato appena entrato tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="518af-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="518af-149">**R:** Di seguito vengono elencati alcuni motivi comuni per questo scenario:</span><span class="sxs-lookup"><span data-stu-id="518af-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="518af-150">Le credenziali dell'utente non sono più valide.</span><span class="sxs-lookup"><span data-stu-id="518af-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="518af-151">Il computer è Impossibile toocommunicate con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="518af-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="518af-152">Verificare la presenza di eventuali problemi di connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="518af-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="518af-153">non sono stati soddisfatti i prerequisiti aggiunta ad Azure AD Hello.</span><span class="sxs-lookup"><span data-stu-id="518af-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="518af-154">Verificare di aver eseguito i passaggi di hello per [estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="518af-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="518af-155">Gli account di accesso federato richiede il toosupport server federativo un endpoint attivo WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="518af-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="518af-156">**D: perché vedere hello "... si è verificato un errore!" finestra di dialogo quando si tenta di aggiungere il PC?**</span><span class="sxs-lookup"><span data-stu-id="518af-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="518af-157">**R:** La finestra viene visualizzata quando si registra Azure Active Directory con Intune.</span><span class="sxs-lookup"><span data-stu-id="518af-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="518af-158">Per altri dettagli, vedere [Configurare la gestione dei dispositivi Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="518af-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="518af-159">**D: perché non è stato toojoin il tentativo di un PC non riuscire anche se non ho ricevuto le informazioni di errore?**</span><span class="sxs-lookup"><span data-stu-id="518af-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="518af-160">**R:** una causa probabile è che l'utente hello viene registrato nel dispositivo toohello utilizzando l'account predefinito administrator hello.</span><span class="sxs-lookup"><span data-stu-id="518af-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="518af-161">Creare un account locale diverso prima di usare Azure Active Directory Join toocomplete hello il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="518af-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="518af-162">**D: dove è possibile trovare istruzioni per l'installazione di hello di registrazione automatica dei dispositivi?**</span><span class="sxs-lookup"><span data-stu-id="518af-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="518af-163">**R:** per istruzioni dettagliate, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="518af-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="518af-164">**D: dove posso trovare la risoluzione dei problemi informazioni sulla registrazione automatica dei dispositivi hello?**</span><span class="sxs-lookup"><span data-stu-id="518af-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="518af-165">**R:** Per informazioni sulla risoluzione dei problemi, vedere:</span><span class="sxs-lookup"><span data-stu-id="518af-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="518af-166">Risoluzione dei problemi di registrazione automatica del dominio aggiunti a un computer tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="518af-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="518af-167">Risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows</span><span class="sxs-lookup"><span data-stu-id="518af-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

