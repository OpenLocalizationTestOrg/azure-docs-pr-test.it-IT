---
title: Connettersi al database SQL usando SQL Server Management Studio in Azure RemoteApp | Documentazione Microsoft
description: Questa esercitazione spiega come imparare a usare SQL Server Management Studio in Azure RemoteApp per la sicurezza e le prestazioni durante la connessione al database SQL
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="07119-103">Usare SQL Server Management Studio in Azure RemoteApp per connettersi al database SQL</span><span class="sxs-lookup"><span data-stu-id="07119-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07119-104">Azure RemoteApp sta per essere sospeso.</span><span class="sxs-lookup"><span data-stu-id="07119-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="07119-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="07119-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="07119-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="07119-106">Introduction</span></span>
<span data-ttu-id="07119-107">Questa esercitazione illustra come usare SQL Server Management Studio (SSMS) in Azure RemoteApp per connettersi al database SQL.</span><span class="sxs-lookup"><span data-stu-id="07119-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="07119-108">Descrive il processo di installazione di SQL Server Management Studio in Azure RemoteApp, ne spiega i vantaggi e illustra le funzionalità di sicurezza che è possibile usare in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07119-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="07119-109">**Tempo previsto per il completamento:** 45 minuti</span><span class="sxs-lookup"><span data-stu-id="07119-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="07119-110">SSMS in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="07119-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="07119-111">Azure RemoteApp è un servizio di Servizi desktop remoto di Azure che fornisce applicazioni.</span><span class="sxs-lookup"><span data-stu-id="07119-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="07119-112">Per altre informazioni, vedere: [Informazioni su Azure RemoteApp](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="07119-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="07119-113">SSMS eseguito in Azure RemoteApp offre la stessa esperienza dell'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="07119-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Schermata di SSMS in esecuzione in Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="07119-115">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="07119-115">Benefits</span></span>
<span data-ttu-id="07119-116">Ecco alcuni dei molti vantaggi che derivano dall'uso di SSMS in Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="07119-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="07119-117">La porta 1433 sul server SQL di Azure non deve essere esposta esternamente (all'esterno di Azure).</span><span class="sxs-lookup"><span data-stu-id="07119-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="07119-118">Non è necessario continuare ad aggiungere e rimuovere indirizzi IP nel firewall del server SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="07119-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="07119-119">Tutte le connessioni di Azure RemoteApp avvengono tramite HTTPS sulla porta 443 con Remote Desktop Protocol crittografato.</span><span class="sxs-lookup"><span data-stu-id="07119-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="07119-120">È multiutente e scalabile.</span><span class="sxs-lookup"><span data-stu-id="07119-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="07119-121">Offre un miglioramento delle prestazioni grazie all'esecuzione di SSMS nella stessa area del database SQL.</span><span class="sxs-lookup"><span data-stu-id="07119-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="07119-122">È possibile controllare l'uso di Azure RemoteApp con la Premium Edition di Azure Active Directory che include report sull'attività utente.</span><span class="sxs-lookup"><span data-stu-id="07119-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="07119-123">È possibile abilitare Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="07119-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="07119-124">Possibilità di accesso a SSMS ovunque, usando uno dei client di Azure RemoteApp supportati che include iOS, Android, Mac, Windows Phone e PC Windows.</span><span class="sxs-lookup"><span data-stu-id="07119-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="07119-125">Creare la raccolta di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="07119-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="07119-126">Ecco i passaggi per creare la raccolta Azure RemoteApp con SSMS:</span><span class="sxs-lookup"><span data-stu-id="07119-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="07119-127">1. Creare una nuova VM Windows da immagine</span><span class="sxs-lookup"><span data-stu-id="07119-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="07119-128">Per creare la nuova VM, usare l'immagine "Host sessione Desktop remoto di Windows Server 2012 R2" dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="07119-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="07119-129">2. Installare SSMS da SQL Express</span><span class="sxs-lookup"><span data-stu-id="07119-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="07119-130">Nella nuova VM passare alla pagina di download: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="07119-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="07119-131">È disponibile un'opzione per scaricare solo SSMS.</span><span class="sxs-lookup"><span data-stu-id="07119-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="07119-132">Dopo il download, passare alla directory di installazione ed eseguire il programma di installazione di SSMS.</span><span class="sxs-lookup"><span data-stu-id="07119-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="07119-133">È necessario installare anche SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="07119-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="07119-134">Scaricarlo qui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="07119-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="07119-135">SQL Server 2014 Service Pack 1 include le funzionalità essenziali per l'utilizzo del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="07119-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="07119-136">3. Eseguire lo script di convalida e Sysprep</span><span class="sxs-lookup"><span data-stu-id="07119-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="07119-137">Sul desktop della VM è disponibile uno script di PowerShell denominato Validate.</span><span class="sxs-lookup"><span data-stu-id="07119-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="07119-138">Fare doppio clic sullo script per eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="07119-138">Run this by double-clicking.</span></span> <span data-ttu-id="07119-139">Verificherà che la VM è pronta all'uso per l'hosting remoto di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="07119-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="07119-140">Una volta completata la verifica, verrà richiesto di eseguire sysprep. Scegliere di eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="07119-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="07119-141">Al termine dell'esecuzione di sysprep, la VM viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="07119-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="07119-142">Per altre informazioni sulla creazione di un'immagine di Azure RemoteApp, vedere l'articolo relativo alla [creazione di un'immagine modello di RemoteApp in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="07119-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="07119-143">4. Acquisire l'immagine</span><span class="sxs-lookup"><span data-stu-id="07119-143">4. Capture image</span></span>
<span data-ttu-id="07119-144">Una volta interrotta l'esecuzione della VM, trovarla nel portale corrente e acquisirla.</span><span class="sxs-lookup"><span data-stu-id="07119-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="07119-145">Per altre informazioni sull'acquisizione di un'immagine, vedere [Acquisire un'immagine di una macchina virtuale Windows di Azure creata con il modello di distribuzione classica](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="07119-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="07119-146">5. Aggiungere immagini modello di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="07119-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="07119-147">Nella sezione Azure RemoteApp del portale corrente passare alla scheda Immagini modello e fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="07119-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="07119-148">Nella finestra popup selezionare "Importare un'immagine dalla raccolta di macchine virtuali" e quindi scegliere l'immagine appena creata.</span><span class="sxs-lookup"><span data-stu-id="07119-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="07119-149">6. Creare una raccolta nel cloud</span><span class="sxs-lookup"><span data-stu-id="07119-149">6. Create cloud collection</span></span>
<span data-ttu-id="07119-150">Nel portale corrente creare una nuova raccolta nel cloud di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="07119-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="07119-151">Scegliere l'immagine modello appena importata con installato SSMS.</span><span class="sxs-lookup"><span data-stu-id="07119-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Creare una nuova raccolta nel cloud][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="07119-153">7. Pubblicare SSMS</span><span class="sxs-lookup"><span data-stu-id="07119-153">7. Publish SSMS</span></span>
<span data-ttu-id="07119-154">Nella scheda Pubblicazione della nuova raccolta nel cloud selezionare l'opzione per pubblicare un'applicazione dal menu Start e quindi scegliere SSMS dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="07119-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Pubblicare l'app][5]

### <a name="8-add-users"></a><span data-ttu-id="07119-156">8. Aggiungere utenti</span><span class="sxs-lookup"><span data-stu-id="07119-156">8. Add users</span></span>
<span data-ttu-id="07119-157">Nella scheda Accesso utente è possibile selezionare gli utenti che avranno accesso a questa raccolta di Azure RemoteApp che include solo SSMS.</span><span class="sxs-lookup"><span data-stu-id="07119-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Aggiunta di un utente][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="07119-159">9. Installare l'applicazione client Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="07119-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="07119-160">Scaricare e installare un client di Azure RemoteApp qui: [Scaricare | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="07119-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="07119-161">Configurare il server SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="07119-161">Configure Azure SQL server</span></span>
<span data-ttu-id="07119-162">La sola configurazione necessaria consiste nel verificare che Servizi di Azure sia abilitato per il firewall.</span><span class="sxs-lookup"><span data-stu-id="07119-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="07119-163">Se si usa questa soluzione, non è necessario aggiungere alcun indirizzo IP per aprire il firewall.</span><span class="sxs-lookup"><span data-stu-id="07119-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="07119-164">Il traffico di rete per SQL Server è consentito solo da altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="07119-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Consentire Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="07119-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="07119-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="07119-167">MFA può essere abilitata appositamente per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="07119-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="07119-168">Passare alla scheda Applicazioni di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07119-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="07119-169">È disponibile una voce per Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="07119-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="07119-170">Se si fa clic su questa applicazione e quindi la si configura, verrà visualizzata la pagina seguente in cui è possibile abilitare MFA per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07119-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Abilitare MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="07119-172">Controllare l'attività utente con Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="07119-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="07119-173">Se non è disponibile Azure AD Premium, è necessario attivarlo nella sezione Licenze della directory.</span><span class="sxs-lookup"><span data-stu-id="07119-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="07119-174">Con la versione Premium abilitata, è possibile assegnare utenti al livello Premium.</span><span class="sxs-lookup"><span data-stu-id="07119-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="07119-175">Passando a un utente in Azure Active Directory, si potrà quindi passare alla scheda Attività per visualizzare informazioni di accesso ad Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="07119-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07119-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07119-176">Next steps</span></span>
<span data-ttu-id="07119-177">Dopo aver completato i passaggi precedenti, si sarà in grado di eseguire il client di Azure RemoteApp e l'accesso con un account utente assegnato.</span><span class="sxs-lookup"><span data-stu-id="07119-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="07119-178">SSMS verrà visualizzato tra le applicazioni disponibili e si potrà eseguirlo come se fosse installato nel computer locale con accesso al server SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="07119-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="07119-179">Per altre informazioni su come stabilire la connessione al database SQL, vedere [Connettersi al database SQL con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="07119-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="07119-180">È tutto per ora.</span><span class="sxs-lookup"><span data-stu-id="07119-180">That's everything for now.</span></span> <span data-ttu-id="07119-181">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="07119-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png