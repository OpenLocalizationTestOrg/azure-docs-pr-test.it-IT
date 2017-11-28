---
title: aaaConnect tooSQL Database utilizzando SQL Server Management Studio in Azure RemoteApp | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come toouse SQL Server Management Studio in Azure RemoteApp per la sicurezza e le prestazioni durante la connessione di Database tooSQL
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
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="477bc-103">Utilizzare SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="477bc-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="477bc-104">Azure RemoteApp sta per essere sospeso.</span><span class="sxs-lookup"><span data-stu-id="477bc-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="477bc-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="477bc-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="477bc-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="477bc-106">Introduction</span></span>
<span data-ttu-id="477bc-107">In questa esercitazione illustra come toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="477bc-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="477bc-108">Viene illustrato il processo di hello di configurazione di SQL Server Management Studio in Azure RemoteApp, vengono illustrati i vantaggi di hello e illustra le funzionalità di sicurezza che è possibile utilizzare in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="477bc-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="477bc-109">**Toocomplete tempo stimato:** 45 minuti</span><span class="sxs-lookup"><span data-stu-id="477bc-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="477bc-110">SSMS in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="477bc-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="477bc-111">Azure RemoteApp è un servizio di Servizi desktop remoto di Azure che fornisce applicazioni.</span><span class="sxs-lookup"><span data-stu-id="477bc-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="477bc-112">Per altre informazioni, vedere: [Informazioni su Azure RemoteApp](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="477bc-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="477bc-113">SQL Server Management Studio in esecuzione in Azure RemoteApp consente hello stessa esperienza di esecuzione in locale di SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="477bc-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Schermata di SSMS in esecuzione in Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="477bc-115">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="477bc-115">Benefits</span></span>
<span data-ttu-id="477bc-116">Esistono molti vantaggi toousing SSMS in Azure RemoteApp, tra cui:</span><span class="sxs-lookup"><span data-stu-id="477bc-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="477bc-117">La porta 1433 sul server SQL di Azure non dispone di toobe esposta esternamente (all'esterno di Azure).</span><span class="sxs-lookup"><span data-stu-id="477bc-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="477bc-118">Nessuna necessità tookeep aggiunta e rimozione di indirizzi IP in firewall hello del server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="477bc-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="477bc-119">Tutte le connessioni di Azure RemoteApp avvengono tramite HTTPS sulla porta 443 con Remote Desktop Protocol crittografato.</span><span class="sxs-lookup"><span data-stu-id="477bc-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="477bc-120">È multiutente e scalabile.</span><span class="sxs-lookup"><span data-stu-id="477bc-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="477bc-121">È un miglioramento delle prestazioni dalla presenza di SQL Server Management Studio in hello stessa area hello Database SQL.</span><span class="sxs-lookup"><span data-stu-id="477bc-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="477bc-122">È possibile controllare l'utilizzo di Azure RemoteApp con hello Premium edition di Azure Active Directory che contiene il report attività utente.</span><span class="sxs-lookup"><span data-stu-id="477bc-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="477bc-123">È possibile abilitare Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="477bc-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="477bc-124">Client di Azure RemoteApp di accesso SQL Server Management Studio in qualsiasi punto quando si utilizza uno di hello supportati che include iOS, Android, Mac, Windows Phone e PC Windows.</span><span class="sxs-lookup"><span data-stu-id="477bc-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="477bc-125">Creare una raccolta di hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="477bc-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="477bc-126">Di seguito è hello passaggi toocreate la raccolta RemoteApp di Azure con SQL Server Management Studio:</span><span class="sxs-lookup"><span data-stu-id="477bc-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="477bc-127">1. Creare una nuova VM Windows da immagine</span><span class="sxs-lookup"><span data-stu-id="477bc-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="477bc-128">Utilizzare hello immagine "Windows Server Remote Desktop sessione Host Windows Server 2012 R2" da hello raccolta toomake la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="477bc-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="477bc-129">2. Installare SSMS da SQL Express</span><span class="sxs-lookup"><span data-stu-id="477bc-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="477bc-130">Andare nella nuova macchina virtuale hello e passare la pagina di download toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="477bc-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="477bc-131">È un download tooonly opzione SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="477bc-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="477bc-132">Dopo il download, passare alla directory di installazione hello ed eseguire il programma di installazione tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="477bc-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="477bc-133">È inoltre necessario tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="477bc-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="477bc-134">Scaricarlo qui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="477bc-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="477bc-135">SQL Server 2014 Service Pack 1 include le funzionalità essenziali per l'utilizzo del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="477bc-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="477bc-136">3. Eseguire lo script di convalida e Sysprep</span><span class="sxs-lookup"><span data-stu-id="477bc-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="477bc-137">In hello desktop della macchina virtuale hello è uno script di PowerShell denominato convalida.</span><span class="sxs-lookup"><span data-stu-id="477bc-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="477bc-138">Fare doppio clic sullo script per eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="477bc-138">Run this by double-clicking.</span></span> <span data-ttu-id="477bc-139">Verificherà che hello macchina virtuale è pronta toobe utilizzato per l'hosting remoto di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="477bc-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="477bc-140">Quando si verifica è completa, viene chiesto di sysprep toorun - scegliere toorun è.</span><span class="sxs-lookup"><span data-stu-id="477bc-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="477bc-141">Al termine, sysprep viene chiuso hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="477bc-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="477bc-142">toolearn informazioni sulla creazione di un'immagine di Azure RemoteApp, vedere: [come immagine di un modello di RemoteApp toocreate in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="477bc-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="477bc-143">4. Acquisire l'immagine</span><span class="sxs-lookup"><span data-stu-id="477bc-143">4. Capture image</span></span>
<span data-ttu-id="477bc-144">Quando hello VM ha smesso di funzionare, individuarlo nel portale corrente hello e acquisirlo.</span><span class="sxs-lookup"><span data-stu-id="477bc-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="477bc-145">toolearn più informazioni sull'acquisizione di un'immagine, vedere [acquisire un'immagine di una macchina virtuale Windows Azure creata con il modello di distribuzione classica hello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="477bc-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="477bc-146">5. Aggiungere immagini modello RemoteApp tooAzure</span><span class="sxs-lookup"><span data-stu-id="477bc-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="477bc-147">Nella sezione di Azure RemoteApp del portale corrente hello hello, andare scheda immagini modello toohello e fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="477bc-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="477bc-148">Nella finestra popup hello, selezionare "Importare un'immagine dalla raccolta di macchine virtuali", quindi scegliere hello immagine appena creato.</span><span class="sxs-lookup"><span data-stu-id="477bc-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="477bc-149">6. Creare una raccolta nel cloud</span><span class="sxs-lookup"><span data-stu-id="477bc-149">6. Create cloud collection</span></span>
<span data-ttu-id="477bc-150">Nel portale corrente hello, creare una nuova raccolta Cloud di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="477bc-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="477bc-151">Scegliere hello immagine modello appena importata con SQL Server Management Studio è installato.</span><span class="sxs-lookup"><span data-stu-id="477bc-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Creare una nuova raccolta nel cloud][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="477bc-153">7. Pubblicare SSMS</span><span class="sxs-lookup"><span data-stu-id="477bc-153">7. Publish SSMS</span></span>
<span data-ttu-id="477bc-154">Nella pubblicazione di un'applicazione dalla scheda della finestra il nuovo insieme di cloud, seleziona pubblica hello hello Menu Start e quindi scegliere SQL Server Management Studio elenco hello.</span><span class="sxs-lookup"><span data-stu-id="477bc-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Pubblicare l'app][5]

### <a name="8-add-users"></a><span data-ttu-id="477bc-156">8. Aggiungi utenti</span><span class="sxs-lookup"><span data-stu-id="477bc-156">8. Add users</span></span>
<span data-ttu-id="477bc-157">Nella scheda accesso utente hello è possibile selezionare gli utenti di hello che disporranno di accesso toothis Azure RemoteApp raccolta che include solo SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="477bc-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Aggiunta di un utente][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="477bc-159">9. Installare un'applicazione client hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="477bc-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="477bc-160">Scaricare e installare un client di Azure RemoteApp qui: [Scaricare | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="477bc-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="477bc-161">Configurare il server SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="477bc-161">Configure Azure SQL server</span></span>
<span data-ttu-id="477bc-162">Hello configurazione necessaria è tooensure che servizi di Azure è abilitato per il firewall hello.</span><span class="sxs-lookup"><span data-stu-id="477bc-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="477bc-163">Se si utilizza questa soluzione, quindi non è necessario tooadd qualsiasi firewall di hello tooopen gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="477bc-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="477bc-164">traffico di rete Hello consentito toohello SQL Server è da altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="477bc-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Consentire Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="477bc-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="477bc-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="477bc-167">MFA può essere abilitata appositamente per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="477bc-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="477bc-168">Andare nella scheda applicazioni toohello di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="477bc-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="477bc-169">È disponibile una voce per Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="477bc-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="477bc-170">Se si sceglie di tale applicazione e quindi configurare, si noterà hello pagina in cui è possibile abilitare l'autenticazione a più fattori per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="477bc-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Abilitare MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="477bc-172">Controllare l'attività utente con Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="477bc-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="477bc-173">Se non è Azure AD Premium, è necessario tooturn in su hello sezione licenze della directory.</span><span class="sxs-lookup"><span data-stu-id="477bc-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="477bc-174">Con Premium abilitato, è possibile assegnare agli utenti di livello Premium toohello.</span><span class="sxs-lookup"><span data-stu-id="477bc-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="477bc-175">Quando si passa tooa utente in Azure Active Directory, sarà quindi possibile passare toohello attività scheda toosee accesso informazioni tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="477bc-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="477bc-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="477bc-176">Next steps</span></span>
<span data-ttu-id="477bc-177">Dopo aver completato tutti hello sopra passaggi, verrà client di Azure RemoteApp in grado di toorun hello e Accedi con un utente assegnato.</span><span class="sxs-lookup"><span data-stu-id="477bc-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="477bc-178">Verrà visualizzata con SQL Server Management Studio come una delle applicazioni ed è possibile eseguire come se fosse installato in computer con accesso tooAzure a SQL server.</span><span class="sxs-lookup"><span data-stu-id="477bc-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="477bc-179">Per ulteriori informazioni su come toomake hello tooSQL connessione Database, vedere [connettersi tooSQL Database con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="477bc-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="477bc-180">È tutto per ora.</span><span class="sxs-lookup"><span data-stu-id="477bc-180">That's everything for now.</span></span> <span data-ttu-id="477bc-181">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="477bc-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png