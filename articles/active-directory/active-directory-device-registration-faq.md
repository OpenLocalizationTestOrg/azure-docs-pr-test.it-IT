---
title: Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="395b2-103">Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="395b2-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="395b2-104">**D: Di recente è stato registrato un dispositivo. Perché non viene visualizzato nelle informazioni dell'utente all'interno del portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="395b2-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="395b2-105">**R:** I dispositivi Windows 10 che appartengono a un dominio con la registrazione automatica dei dispositivi non vengono visualizzati nelle informazioni UTENTE.</span><span class="sxs-lookup"><span data-stu-id="395b2-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="395b2-106">È necessario usare PowerShell per visualizzare tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="395b2-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="395b2-107">Nelle informazioni UTENTE vengono elencati solo i dispositivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="395b2-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="395b2-108">Tutti i dispositivi personali non aggiunti a un dominio aziendale</span><span class="sxs-lookup"><span data-stu-id="395b2-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="395b2-109">Tutti i dispositivi non Windows 10/Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="395b2-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="395b2-110">Tutti i dispositivi non Windows</span><span class="sxs-lookup"><span data-stu-id="395b2-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="395b2-111">**D: Perché non vengono visualizzati tutti i dispositivi registrati in Azure Active Directory nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="395b2-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="395b2-112">**R:** Attualmente non è possibile visualizzare tutti i dispositivi registrati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="395b2-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="395b2-113">È possibile usare Azure PowerShell per trovare tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="395b2-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="395b2-114">Per ulteriori informazioni, vedere il cmdlet [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="395b2-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="395b2-115">**D: Come è possibile conoscere lo stato di registrazione del dispositivo client?**</span><span class="sxs-lookup"><span data-stu-id="395b2-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="395b2-116">**R:** Lo stato di registrazione del dispositivo dipende da:</span><span class="sxs-lookup"><span data-stu-id="395b2-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="395b2-117">Tipo di dispositivo</span><span class="sxs-lookup"><span data-stu-id="395b2-117">What the device is</span></span>
- <span data-ttu-id="395b2-118">Modalità di registrazione</span><span class="sxs-lookup"><span data-stu-id="395b2-118">How it was registered</span></span> 
- <span data-ttu-id="395b2-119">Eventuali altri dettagli associati.</span><span class="sxs-lookup"><span data-stu-id="395b2-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="395b2-120">**D: Perché un dispositivo eliminato nel portale di Azure o tramite PowerShell viene comunque elencato come registrato?**</span><span class="sxs-lookup"><span data-stu-id="395b2-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="395b2-121">**A:** Si tratta di un comportamento previsto da progettazione.</span><span class="sxs-lookup"><span data-stu-id="395b2-121">**A:** This is by design.</span></span> <span data-ttu-id="395b2-122">Il dispositivo non avrà accesso alle risorse nel cloud.</span><span class="sxs-lookup"><span data-stu-id="395b2-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="395b2-123">Se si vuole rimuovere e registrare nuovamente il dispositivo, è necessario farlo manualmente da quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="395b2-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="395b2-124">Per i dispositivi Windows 10 e Windows Server 2016 aggiunti a un dominio AD locale:</span><span class="sxs-lookup"><span data-stu-id="395b2-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="395b2-125">Aprire il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="395b2-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="395b2-126">Digitare `dsregcmd.exe /debug /leave`.</span><span class="sxs-lookup"><span data-stu-id="395b2-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="395b2-127">Disconnettersi e accedere per attivare le attività pianificate che registrano nuovamente il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="395b2-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="395b2-128">Per altre piattaforme Windows aggiunte a un dominio AD locale:</span><span class="sxs-lookup"><span data-stu-id="395b2-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="395b2-129">Aprire il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="395b2-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="395b2-130">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="395b2-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="395b2-131">Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="395b2-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="395b2-132">**D: Perché vengono visualizzate voci di dispositivo duplicate nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="395b2-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="395b2-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="395b2-133">**A:**</span></span>

-   <span data-ttu-id="395b2-134">Per i dispositivi Windows 10 e Windows Server 2016, se vengono effettuati tentativi ripetuti di rimozione o aggiunta del medesimo dispositivo, potrebbero essere visualizzate voci duplicate.</span><span class="sxs-lookup"><span data-stu-id="395b2-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="395b2-135">Ciascun utente Windows che usa l'opzione Aggiungi account aziendale o dell'istituto di istruzione creerà un nuovo record di dispositivo con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="395b2-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="395b2-136">Per le altre piattaforme Windows aggiunte a domini AD locali che usano la registrazione automatica verrà creato un nuovo record di dispositivo con lo stesso nome per ciascun utente di dominio che accede al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="395b2-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="395b2-137">Un computer AADJ cancellato, reinstallato e aggiunto nuovamente con lo stesso nome verrà visualizzato con un record diverso ma con lo stesso nome dispositivo.</span><span class="sxs-lookup"><span data-stu-id="395b2-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="395b2-138">**D: Perché un utente può comunque accedere alle risorse da un dispositivo disattivato nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="395b2-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="395b2-139">**R:** Potrebbe volerci fino a un'ora per applicare una revoca.</span><span class="sxs-lookup"><span data-stu-id="395b2-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="395b2-140">Se un dispositivo viene perso, è consigliabile cancellarlo per assicurare che gli utenti non possano accedervi.</span><span class="sxs-lookup"><span data-stu-id="395b2-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="395b2-141">Per altre informazioni, vedere , vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="395b2-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="395b2-142">**D: Perché viene visualizzato un messaggio che avvisa dell'impossibilità di raggiungere un determinato dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="395b2-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="395b2-143">**R:** Se sono state configurate determinate regole di accesso condizionale per richiedere uno stato specifico del dispositivo e il dispositivo in questione non soddisfa i criteri, gli utenti vengono bloccati con questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="395b2-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="395b2-144">Esaminare le regole e assicurarsi che il dispositivo soddisfi i criteri per evitare di incorrere in questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="395b2-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="395b2-145">**D: Il record del dispositivo è presente nelle informazioni UTENTE nel portale di Azure e viene indicato come registrato nel client. La configurazione è corretta per l'uso dell'accesso condizionale?**</span><span class="sxs-lookup"><span data-stu-id="395b2-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="395b2-146">**R:** Il record (deviceID) e lo stato del dispositivo nel portale di Azure devono corrispondere al client e soddisfare eventuali criteri di valutazione per l'accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="395b2-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="395b2-147">Per altre informazioni, vedere [Introduzione a Registrazione dispositivo Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="395b2-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="395b2-148">**D: Perché viene visualizzato un messaggio di nome utente o password non corretti per un dispositivo appena aggiunto ad Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="395b2-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="395b2-149">**R:** Di seguito vengono elencati alcuni motivi comuni per questo scenario:</span><span class="sxs-lookup"><span data-stu-id="395b2-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="395b2-150">Le credenziali dell'utente non sono più valide.</span><span class="sxs-lookup"><span data-stu-id="395b2-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="395b2-151">Il computer non riesce a comunicare con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="395b2-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="395b2-152">Verificare la presenza di eventuali problemi di connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="395b2-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="395b2-153">Non sono stati soddisfatti i prerequisiti di aggiunta ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="395b2-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="395b2-154">Assicurarsi di aver seguito i passaggi indicati in [Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="395b2-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="395b2-155">Gli accessi federati richiedono un server di federazione con supporto per endpoint attivi WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="395b2-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="395b2-156">**D: Perché viene visualizzata la finestra di dialogo "Oops… an error occurred!" (Si è verificato un errore) quando si tenta di aggiungere un PC?**</span><span class="sxs-lookup"><span data-stu-id="395b2-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="395b2-157">**R:** La finestra viene visualizzata quando si registra Azure Active Directory con Intune.</span><span class="sxs-lookup"><span data-stu-id="395b2-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="395b2-158">Per altri dettagli, vedere [Configurare la gestione dei dispositivi Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="395b2-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="395b2-159">**D: Perché il tentativo di aggiunta di un PC non è andato a buon fine ma non vengono comunque visualizzate informazioni sull'errore?**</span><span class="sxs-lookup"><span data-stu-id="395b2-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="395b2-160">**R:** È probabile che l'utente abbia effettuato l'accesso al dispositivo con l'account amministratore predefinito.</span><span class="sxs-lookup"><span data-stu-id="395b2-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="395b2-161">Creare un account locale diverso prima di usare l'aggiunta ad Azure Active Directory per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="395b2-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="395b2-162">**D: Dove reperire le istruzioni per la configurazione della registrazione automatica del dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="395b2-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="395b2-163">**R:**Per altre informazioni, vedere [Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="395b2-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="395b2-164">**D: Dove è possibile trovare informazioni sulla risoluzione dei problemi legati alla registrazione automatica del dispositivo?**</span><span class="sxs-lookup"><span data-stu-id="395b2-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="395b2-165">**R:** Per informazioni sulla risoluzione dei problemi, vedere:</span><span class="sxs-lookup"><span data-stu-id="395b2-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="395b2-166">Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio di Azure AD - Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="395b2-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="395b2-167">Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio di Azure AD per client di livello inferiore di Windows</span><span class="sxs-lookup"><span data-stu-id="395b2-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

