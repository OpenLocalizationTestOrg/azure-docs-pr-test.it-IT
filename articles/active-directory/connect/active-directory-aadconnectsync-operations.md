---
title: "Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni | Documentazione Microsoft"
description: "Questo argomento descrive le attività operative per il servizio di sincronizzazione Azure AD Connect e come prepararsi per il funzionamento di questo componente."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="80c64-103">Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni</span><span class="sxs-lookup"><span data-stu-id="80c64-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="80c64-104">L'obiettivo di questo argomento è descrivere le attività operative per il servizio di sincronizzazione Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="80c64-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="80c64-105">Modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="80c64-105">Staging mode</span></span>
<span data-ttu-id="80c64-106">La modalità di gestione temporanea può essere usata per diversi scenari, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="80c64-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="80c64-107">Disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="80c64-107">High availability.</span></span>
* <span data-ttu-id="80c64-108">Testare e distribuire le nuove modifiche della configurazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="80c64-109">Introdurre un nuovo server e rimuovere quello vecchio.</span><span class="sxs-lookup"><span data-stu-id="80c64-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="80c64-110">Con un server in modalità di gestione temporanea è possibile apportare modifiche alla configurazione e visualizzarle in anteprima prima di attivare il server.</span><span class="sxs-lookup"><span data-stu-id="80c64-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="80c64-111">È anche possibile eseguire operazioni di importazione e sincronizzazione complete per verificare che tutte le modifiche siano previste prima di introdurle nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="80c64-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="80c64-112">Durante l'installazione è possibile selezionare la **modalità di gestione temporanea**per il server.</span><span class="sxs-lookup"><span data-stu-id="80c64-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="80c64-113">In questo modo il server sarà attivo per le operazioni di importazione e sincronizzazione, ma non eseguirà esportazioni.</span><span class="sxs-lookup"><span data-stu-id="80c64-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="80c64-114">Un server in modalità di gestione temporanea non eseguirà la sincronizzazione o il writeback delle password, anche se queste funzionalità sono state selezionate durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="80c64-115">Quando si disabilita la modalità di gestione temporanea, il server avvia l'esportazione e abilita la sincronizzazione e il writeback delle password.</span><span class="sxs-lookup"><span data-stu-id="80c64-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="80c64-116">È comunque possibile forzare un’esportazione utilizzando Synchronization Service Manager.</span><span class="sxs-lookup"><span data-stu-id="80c64-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="80c64-117">Un server in modalità di gestione temporanea continua a ricevere modifiche da Active Directory e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c64-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="80c64-118">Ha sempre una copia delle modifiche più recenti e può così assumere velocemente le funzioni di un altro server.</span><span class="sxs-lookup"><span data-stu-id="80c64-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="80c64-119">Se si apportano modifiche alla configurazione del server primario, è necessario apportare le stesse modifiche al server in modalità di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="80c64-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="80c64-120">Coloro che hanno una conoscenza delle tecnologie di sincronizzazione precedenti tengano presente che la modalità di gestione temporanea è diversa, perché il server ha il proprio database SQL.</span><span class="sxs-lookup"><span data-stu-id="80c64-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="80c64-121">L'architettura consente al server in modalità di gestione temporanea di trovarsi in un altro data center.</span><span class="sxs-lookup"><span data-stu-id="80c64-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="80c64-122">Verificare la configurazione di un server</span><span class="sxs-lookup"><span data-stu-id="80c64-122">Verify the configuration of a server</span></span>
<span data-ttu-id="80c64-123">Per applicare questo metodo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="80c64-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="80c64-124">Preparare</span><span class="sxs-lookup"><span data-stu-id="80c64-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="80c64-125">Configurazione</span><span class="sxs-lookup"><span data-stu-id="80c64-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="80c64-126">Importare e sincronizzare</span><span class="sxs-lookup"><span data-stu-id="80c64-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="80c64-127">Verificare</span><span class="sxs-lookup"><span data-stu-id="80c64-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="80c64-128">Cambiare il server attivo</span><span class="sxs-lookup"><span data-stu-id="80c64-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="80c64-129">Preparazione</span><span class="sxs-lookup"><span data-stu-id="80c64-129">Prepare</span></span>
1. <span data-ttu-id="80c64-130">Installare Azure AD Connect, selezionare **Modalità di gestione temporanea** e deselezionare **Avvia sincronizzazione** nell'ultima pagina dell'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="80c64-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="80c64-131">In questo modo è possibile eseguire manualmente il motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="80c64-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="80c64-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="80c64-133">Disconnettersi e accedere, quindi dal menu Start selezionare **Synchronization Service**(Servizio di sincronizzazione).</span><span class="sxs-lookup"><span data-stu-id="80c64-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="80c64-134">Configurazione</span><span class="sxs-lookup"><span data-stu-id="80c64-134">Configuration</span></span>
<span data-ttu-id="80c64-135">Se si sono apportate modifiche personalizzate al server primario e si desidera confrontare la configurazione con server di gestione temporanea, usare l'[analizzatore di configurazione di Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="80c64-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="80c64-136">Importare e sincronizzare</span><span class="sxs-lookup"><span data-stu-id="80c64-136">Import and Synchronize</span></span>
1. <span data-ttu-id="80c64-137">Selezionare **Connettori** e quindi selezionare il primo connettore con il tipo **Servizi di dominio Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80c64-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="80c64-138">Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="80c64-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="80c64-139">Eseguire questi passaggi per tutti i connettori di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="80c64-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="80c64-140">Selezionare il connettore con il tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="80c64-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="80c64-141">Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="80c64-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="80c64-142">Assicurarsi che la scheda Connectors (Connettori) sia ancora selezionata.</span><span class="sxs-lookup"><span data-stu-id="80c64-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="80c64-143">Per ogni connettore con il tipo **Active Directory Domain Services** fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="80c64-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="80c64-144">Selezionare il connettore con il tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="80c64-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="80c64-145">Fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="80c64-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="80c64-146">È stata eseguita l'esportazione delle modifiche in modalità di gestione temporanea in Azure AD e in AD locale (se si usa una distribuzione ibrida di Exchange).</span><span class="sxs-lookup"><span data-stu-id="80c64-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="80c64-147">I passaggi successivi consentono di ispezionare quali sono gli elementi che stanno per essere modificati prima di avviare effettivamente l'esportazione nelle directory.</span><span class="sxs-lookup"><span data-stu-id="80c64-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="80c64-148">Verificare</span><span class="sxs-lookup"><span data-stu-id="80c64-148">Verify</span></span>
1. <span data-ttu-id="80c64-149">Avviare un prompt dei comandi e passare a `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="80c64-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="80c64-150">Eseguire: `csexport "Name of Connector" %temp%\export.xml /f:x` Il nome del connettore si trova nel servizio di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="80c64-151">Il nome sarà simile a "contoso.com - AAD" per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c64-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="80c64-152">Copiare lo script di PowerShell dalla sezione [CSAnalyzer](#appendix-csanalyzer) in un file denominato `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="80c64-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="80c64-153">Aprire una finestra di PowerShell e passare alla cartella in cui è stato creato lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80c64-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="80c64-154">Eseguire: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="80c64-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="80c64-155">A questo punto si avrà un file denominato **processedusers1.csv**, che può essere esaminato in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="80c64-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="80c64-156">In questo file sono disponibili tutte le modifiche di gestione temporanea da esportare in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c64-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="80c64-157">Apportare le modifiche necessarie ai dati o alla configurazione ed eseguire di nuovo questi passaggi (importazione, sincronizzazione e verifica) finché le modifiche che verranno esportate non saranno quelle previste.</span><span class="sxs-lookup"><span data-stu-id="80c64-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="80c64-158">Cambiare il server attivo</span><span class="sxs-lookup"><span data-stu-id="80c64-158">Switch active server</span></span>
1. <span data-ttu-id="80c64-159">Disattivare il server attualmente attivo (DirSync/FIM/Azure AD Sync), in modo che non esegua l'esportazione in Azure AD oppure impostarlo in modalità di gestione temporanea (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="80c64-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="80c64-160">Eseguire l'installazione guidata nel server in **modalità di gestione temporanea** e disabilitare **questa modalità**.</span><span class="sxs-lookup"><span data-stu-id="80c64-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="80c64-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="80c64-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="80c64-162">Ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="80c64-162">Disaster recovery</span></span>
<span data-ttu-id="80c64-163">Nell'ambito della progettazione dell'implementazione vengono pianificate le operazioni da eseguire nel caso di un'emergenza che causa la perdita del server di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="80c64-164">Ci sono diversi modelli da usare e quello scelto dipende da diversi fattori, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="80c64-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="80c64-165">Qual è la tolleranza per l'impossibilità di apportare modifiche agli oggetti in Azure AD durante il tempo di inattività?</span><span class="sxs-lookup"><span data-stu-id="80c64-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="80c64-166">Se si usa la sincronizzazione delle password, gli utenti accettano di dover usare la vecchia password in Azure AD nel caso la modifichino in locale?</span><span class="sxs-lookup"><span data-stu-id="80c64-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="80c64-167">Si ha una dipendenza dalle operazioni in tempo reale, ad esempio il writeback delle password?</span><span class="sxs-lookup"><span data-stu-id="80c64-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="80c64-168">A seconda delle risposte a queste domande e dei criteri dell'organizzazione, è possibile implementare una delle strategie seguenti:</span><span class="sxs-lookup"><span data-stu-id="80c64-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="80c64-169">Ricompilare quando necessario.</span><span class="sxs-lookup"><span data-stu-id="80c64-169">Rebuild when needed.</span></span>
* <span data-ttu-id="80c64-170">Avere un server di standby di riserva, ovvero in **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="80c64-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="80c64-171">Usare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="80c64-171">Use virtual machines.</span></span>

<span data-ttu-id="80c64-172">Se non si usa il database di SQL Express predefinito, è opportuno vedere anche la sezione [Disponibilità elevata di SQL](#sql-high-availability) .</span><span class="sxs-lookup"><span data-stu-id="80c64-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="80c64-173">Ricompilare quando necessario</span><span class="sxs-lookup"><span data-stu-id="80c64-173">Rebuild when needed</span></span>
<span data-ttu-id="80c64-174">Una strategia valida consiste nel pianificare la ricompilazione di un server in caso di necessità.</span><span class="sxs-lookup"><span data-stu-id="80c64-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="80c64-175">L'installazione del motore di sincronizzazione e l'esecuzione dell'importazione iniziale e della sincronizzazione possono essere generalmente completate in poche ore.</span><span class="sxs-lookup"><span data-stu-id="80c64-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="80c64-176">Se non è disponibile un server di riserva, è possibile usare temporaneamente un controller di dominio per ospitare il motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="80c64-177">Il server del motore di sincronizzazione non archivia lo stato degli oggetti, quindi il database può essere ricompilato dai dati disponibili in Active Directory e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c64-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="80c64-178">L'attributo **sourceAnchor** viene usato per aggiungere gli oggetti sia locali che dal cloud.</span><span class="sxs-lookup"><span data-stu-id="80c64-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="80c64-179">Se si ricompila il server con gli oggetti esistenti in locale e nel cloud, il motore di sincronizzazione abbinerà di nuovo questi oggetti al momento della reinstallazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="80c64-180">Gli elementi che occorre documentare e salvare sono le modifiche della configurazione apportate al server, ad esempio le regole di filtro e sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="80c64-181">Queste configurazioni personalizzate dovranno essere riapplicate prima di avviare la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="80c64-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="80c64-182">Avere un server di standby di riserva, in modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="80c64-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="80c64-183">Nel caso di un ambiente più complesso, è consigliabile avere uno o più server di standby.</span><span class="sxs-lookup"><span data-stu-id="80c64-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="80c64-184">Durante l'installazione è possibile abilitare un server in **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="80c64-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="80c64-185">Per altre informazioni, vedere le [modalità di gestione temporanea](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="80c64-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="80c64-186">Usare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="80c64-186">Use virtual machines</span></span>
<span data-ttu-id="80c64-187">Un metodo comune e supportato consiste nell'eseguire il motore di sincronizzazione in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="80c64-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="80c64-188">Nel caso di un problema dell'host, è possibile eseguire la migrazione dell'immagine del server del motore di sincronizzazione in un altro server.</span><span class="sxs-lookup"><span data-stu-id="80c64-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="80c64-189">Disponibilità elevata di SQL</span><span class="sxs-lookup"><span data-stu-id="80c64-189">SQL High Availability</span></span>
<span data-ttu-id="80c64-190">Se non si usa SQL Server Express fornito con Azure AD Connect, è necessario prendere in considerazione anche la disponibilità elevata per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="80c64-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="80c64-191">Le soluzioni a disponibilità elevata supportate includono il clustering di SQL e AOA (Gruppi di disponibilità Always On),</span><span class="sxs-lookup"><span data-stu-id="80c64-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="80c64-192">mentre il mirroring è una delle soluzioni non supportate.</span><span class="sxs-lookup"><span data-stu-id="80c64-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="80c64-193">In Azure AD Connect versione 1.1.524.0 è stato aggiunto il supporto per SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="80c64-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="80c64-194">È necessario abilitare SQL AOA prima di installare Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="80c64-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="80c64-195">Durante l'installazione, Azure AD Connect rileva se l'istanza SQL specificata è abilitata per SQL AOA oppure no.</span><span class="sxs-lookup"><span data-stu-id="80c64-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="80c64-196">Se SQL AOA è abilitato, Azure AD Connect rileva quindi se SQL AOA è configurato per usare la replica sincrona o asincrona.</span><span class="sxs-lookup"><span data-stu-id="80c64-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="80c64-197">Quando si configura il listener del gruppo di disponibilità, è consigliabile impostare la proprietà RegisterAllProvidersIP su 0.</span><span class="sxs-lookup"><span data-stu-id="80c64-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="80c64-198">Ciò perché Azure AD Connect usa il client nativo di SQL per connettersi a SQL e il client nativo SQL non supporta l'uso della proprietà MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="80c64-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="80c64-199">Appendice CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="80c64-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="80c64-200">Vedere la sezione [Verificare](#verify) su come usare questo script.</span><span class="sxs-lookup"><span data-stu-id="80c64-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="80c64-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80c64-201">Next steps</span></span>
<span data-ttu-id="80c64-202">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="80c64-202">**Overview topics**</span></span>  

* [<span data-ttu-id="80c64-203">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="80c64-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="80c64-204">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80c64-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
