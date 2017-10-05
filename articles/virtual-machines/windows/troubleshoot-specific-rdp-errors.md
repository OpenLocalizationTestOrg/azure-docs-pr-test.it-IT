---
title: Specifici messaggi di errore RDP per VM di Azure | Documentazione Microsoft
description: Comprendere specifici messaggi di errore che possono essere visualizzati quando si tenta di usare una connessione Desktop remoto a una macchina virtuale Windows in Azure
keywords: Errore di desktop remoto, errore di connessione al desktop remoto, impossibile connettersi alla macchina virtuale, risoluzione dei problemi di desktop remoto
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: e7c049106726a15e96d4ebe7c7c0388a29c546c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="65704-104">Risoluzione dei problemi relativi a specifici messaggi di errore RDP inviati a una VM Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="65704-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="65704-105">Quando si usa una connessione Desktop remoto a una macchina virtuale (VM) Windows in Azure, è possibile ricevere uno specifico messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="65704-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="65704-106">Questo articolo illustra nei dettagli alcuni dei più comuni messaggi di errore visualizzati e spiega le procedure per la risoluzione dei problemi relativi a tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="65704-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="65704-107">Se si verificano problemi di connessione alla VM mediante RDP ma non viene visualizzato un messaggio di errore specifico, vedere la [guida alla risoluzione dei problemi relativi a Desktop remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65704-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="65704-108">Per informazioni su messaggi di errore specifici, vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="65704-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="65704-109"><seg>
  [La sessione remota è stata disconnessa perché non sono disponibili server licenze di Desktop remoto per il rilascio della licenza](#rdplicense).</seg></span><span class="sxs-lookup"><span data-stu-id="65704-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="65704-110">[Desktop remoto: impossibile rilevare il "nome" del computer](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="65704-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="65704-111">[Si è verificato un errore di autenticazione. Impossibile contattare l'autorità di sicurezza locale](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="65704-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="65704-112">[Errore di sicurezza di Windows: Le credenziali specificate non funzionano](#wincred).</span><span class="sxs-lookup"><span data-stu-id="65704-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="65704-113">[Il computer non è in grado di connettersi al computer remoto](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="65704-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="65704-114">La sessione remota è stata disconnessa perché non sono disponibili server licenze di Desktop remoto per il rilascio della licenza.</span><span class="sxs-lookup"><span data-stu-id="65704-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="65704-115">Causa: il periodo di prova di 120 giorni delle licenza per il ruolo Server Desktop remoto è scaduto ed è necessario installare le licenze.</span><span class="sxs-lookup"><span data-stu-id="65704-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="65704-116">Per risolvere il problema, salvare una copia locale del file RDP dal portale e al prompt dei comandi di PowerShell eseguire questo comando per avviare la connessione.</span><span class="sxs-lookup"><span data-stu-id="65704-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="65704-117">Questo passaggio disabilita la licenza solo per la connessione in oggetto:</span><span class="sxs-lookup"><span data-stu-id="65704-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="65704-118">Se in realtà non sono necessarie più di due connessioni di desktop remoto contemporanee nella VM, è possibile usare Gestione server per rimuovere il ruolo server desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="65704-119">Per altre informazioni, vedere il post di blog relativo all' [errore della VM di Azure "Non sono disponibili server licenze di Desktop remoto"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="65704-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="65704-120">Desktop remoto: impossibile rilevare il "nome" del computer.</span><span class="sxs-lookup"><span data-stu-id="65704-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="65704-121">Causa: il client Desktop remoto del computer non è in grado di risolvere il nome del computer nelle impostazioni del file RDP.</span><span class="sxs-lookup"><span data-stu-id="65704-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="65704-122">Possibili soluzioni:</span><span class="sxs-lookup"><span data-stu-id="65704-122">Possible solutions:</span></span>

* <span data-ttu-id="65704-123">Se si usa una rete Intranet aziendale, assicurarsi che il computer abbia accesso al server proxy e sia in grado di inviare a quest'ultimo traffico HTTPS.</span><span class="sxs-lookup"><span data-stu-id="65704-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="65704-124">Se si usa un file RDP archiviato localmente, provare a usare il file generato dal portale.</span><span class="sxs-lookup"><span data-stu-id="65704-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="65704-125">Questo passaggio consente di verificare di usare il nome DNS corretto per la macchina virtuale o il servizio cloud e la porta dell'endpoint della VM.</span><span class="sxs-lookup"><span data-stu-id="65704-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="65704-126">Di seguito viene riportato un esempio di file RDP generato dal portale:</span><span class="sxs-lookup"><span data-stu-id="65704-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="65704-127">La parte dell'indirizzo del file RDP contiene:</span><span class="sxs-lookup"><span data-stu-id="65704-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="65704-128">Il nome di dominio completo del servizio cloud contenente la macchina virtuale ("tailspin-azdatatier.cloudapp.net" in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="65704-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="65704-129">La porta TCP esterna dell'endpoint per il traffico di Desktop remoto (55919).</span><span class="sxs-lookup"><span data-stu-id="65704-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="65704-130">Si è verificato un errore di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="65704-130">An authentication error has occurred.</span></span> <span data-ttu-id="65704-131">Impossibile contattare l'autorità di sicurezza locale.</span><span class="sxs-lookup"><span data-stu-id="65704-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="65704-132">Causa: la macchina virtuale di destinazione non è in grado di individuare l'autorità di sicurezza nella porzione di nome utente delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="65704-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="65704-133">Quando il nome utente è nel formato *AutoritàSicurezza*\\*NomeUtente* (esempio: CORP\Utente1), la parte *AutoritàSicurezza* indica o il nome del computer della VM (per l'autorità di protezione locale) o un nome di dominio di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="65704-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="65704-134">Possibili soluzioni:</span><span class="sxs-lookup"><span data-stu-id="65704-134">Possible solutions:</span></span>

* <span data-ttu-id="65704-135">Se l'account è locale nella macchina virtuale, verificare che il nome della macchina virtuale sia stato digitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="65704-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="65704-136">Se l'account è in un dominio di Active Directory, controllare l'ortografia del nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="65704-137">Se è un account di dominio di Active Directory e il nome di dominio è stato digitato correttamente, verificare che in tale dominio sia disponibile un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="65704-138">Nelle reti virtuali di Azure che contengono controller di dominio, è un problema comune che un controller di dominio non sia disponibile perché non è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="65704-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="65704-139">Per risolvere il problema, è possibile usare un account amministratore locale anziché un account di dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="65704-140">Errore di sicurezza di Windows: Le credenziali specificate non funzionano.</span><span class="sxs-lookup"><span data-stu-id="65704-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="65704-141">Causa: la macchina virtuale di destinazione non può convalidare il nome e la password dell'account.</span><span class="sxs-lookup"><span data-stu-id="65704-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="65704-142">Un computer basato su Windows può convalidare le credenziali di un account locale o di un account di dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="65704-143">Per gli account locali, usare la sintassi *NomeComputer*\\*NomeUtente* (ad esempio: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="65704-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="65704-144">Per gli account di dominio usare la sintassi *NomeDominio*\\*NomeUtente* (ad esempio: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="65704-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="65704-145">Se la VM è stata innalzata al livello di controller di dominio in una nuova foresta Active Directory, l'account amministratore locale con il quale è stato eseguito l'accesso viene convertito in un account equivalente con la stessa password nella nuova foresta e nel nuovo dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="65704-146">L'account locale viene quindi eliminato.</span><span class="sxs-lookup"><span data-stu-id="65704-146">The local account is then deleted.</span></span>

<span data-ttu-id="65704-147">Ad esempio, se è stato eseguito l'accesso con l'account locale DC1\DCAdmin e la macchina virtuale è stata innalzata al livello di controller di dominio in una nuova foresta per il dominio corp.contoso.com, l'account locale DC1\DCAdmin viene eliminato e viene creato un nuovo account di dominio (CORP\DCAdmin) con la stessa password.</span><span class="sxs-lookup"><span data-stu-id="65704-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="65704-148">Assicurarsi che il nome dell'account sia un nome che possa essere verificato come account valido dalla macchina virtuale e che la password sia corretta.</span><span class="sxs-lookup"><span data-stu-id="65704-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="65704-149">Se è necessario modificare la password dell'account amministratore locale, vedere [Come reimpostare una password o il servizio Desktop remoto per le macchine virtuali Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65704-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="65704-150">Il computer non è in grado di connettersi al computer remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="65704-151">Causa: l'account usato per la connessione non dispone dei diritti di accesso Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="65704-152">Ogni computer Windows dispone di un gruppo locale Utenti desktop remoto, che contiene gli account e i gruppi che hanno il diritto di accedere in remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="65704-153">Anche i membri del gruppo Administrators locale dispongono dell'accesso, sebbene tali account non siano elencati nel gruppo locale Utenti Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="65704-154">Per le macchine appartenenti a un dominio, il gruppo Administrators locale contiene anche gli amministratori di dominio per il dominio.</span><span class="sxs-lookup"><span data-stu-id="65704-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="65704-155">Assicurarsi che l'account che si usa per la connessione disponga dei diritti di accesso a Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="65704-156">Come soluzione alternativa, usare un account amministratore locale o di dominio per connettersi tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="65704-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="65704-157">Per aggiungere l'account desiderato al gruppo locale Utenti desktop remoto, usare quindi lo snap-in Microsoft Management Console (**Utilità di sistema > Utenti e gruppi locali > Gruppi > Utenti desktop remoto**).</span><span class="sxs-lookup"><span data-stu-id="65704-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65704-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65704-158">Next steps</span></span>
<span data-ttu-id="65704-159">Se non è stato visualizzato alcuno di questi messaggi ma si verifica un errore sconosciuto riguardo alla connessione mediante RDP, vedere la [guida alla risoluzione dei problemi relativi a Desktop remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65704-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="65704-160">Per la risoluzione dei problemi di accesso alle applicazioni in esecuzione in una VM, vedere [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Risolvere i problemi di accesso a un'applicazione in esecuzione in una macchina virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="65704-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="65704-161">Se si verificano problemi relativi all'uso di SSH (Secure Shell) per la connessione a una VM Linux in Azure, vedere [Risoluzione dei problemi di connessione SSH a una macchina virtuale Linux di Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65704-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

