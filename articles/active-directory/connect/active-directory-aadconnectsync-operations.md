---
title: "Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni | Documentazione Microsoft"
description: "In questo argomento vengono descritte le attività operative per la sincronizzazione di Azure AD Connect e come tooprepare per l'uso di questo componente."
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="2f4b9-103">Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni</span><span class="sxs-lookup"><span data-stu-id="2f4b9-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="2f4b9-104">obiettivo di Hello di questo argomento è toodescribe attività operative per la sincronizzazione di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="2f4b9-105">Modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="2f4b9-105">Staging mode</span></span>
<span data-ttu-id="2f4b9-106">La modalità di gestione temporanea può essere usata per diversi scenari, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f4b9-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="2f4b9-107">Disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-107">High availability.</span></span>
* <span data-ttu-id="2f4b9-108">Testare e distribuire le nuove modifiche della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="2f4b9-109">Introduce un nuovo server e rimuovere le autorizzazioni hello precedente.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="2f4b9-110">Con un server in modalità di gestione temporanea, è possibile apportare modifiche toohello configurazione e anteprima hello modifiche prima di apportare active server hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="2f4b9-111">Consente inoltre importazione completa toorun e tooverify sincronizzazione completa che tutte le modifiche sono previsti prima di apportare queste modifiche nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="2f4b9-112">Durante l'installazione, è possibile selezionare hello server toobe in **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="2f4b9-113">Questa azione rende attivo per l'importazione e la sincronizzazione server hello, ma non esegue alcuna esportazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="2f4b9-114">Un server in modalità di gestione temporanea non eseguirà la sincronizzazione o il writeback delle password, anche se queste funzionalità sono state selezionate durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="2f4b9-115">Quando si disattiva modalità di staging, hello server avvia l'esportazione, consente la sincronizzazione della password e abilita il writeback delle password.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="2f4b9-116">È comunque possibile forzare un'esportazione utilizzando Gestione servizio di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="2f4b9-117">Un server in modalità di gestione temporanea continua tooreceive modifiche da Active Directory e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="2f4b9-118">Include sempre una copia delle modifiche più recenti di hello e può essere molto veloci take su responsabilità hello di un altro server.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="2f4b9-119">Se si apportano server primario tooyour modifiche di configurazione, è la responsabilità toomake hello allo stesso server di toohello di modifiche nella modalità di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="2f4b9-120">Per coloro con conoscenza delle tecnologie di sincronizzazione precedenti, hello in modalità di gestione temporanea è diverso dal server hello dispone del proprio database SQL.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="2f4b9-121">Questa architettura consente hello modalità server toobe che si trova in un altro Data Center di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="2f4b9-122">Verificare la configurazione di un server hello</span><span class="sxs-lookup"><span data-stu-id="2f4b9-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="2f4b9-123">tooapply questo metodo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2f4b9-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="2f4b9-124">Preparare</span><span class="sxs-lookup"><span data-stu-id="2f4b9-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="2f4b9-125">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f4b9-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="2f4b9-126">Importare e sincronizzare</span><span class="sxs-lookup"><span data-stu-id="2f4b9-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="2f4b9-127">Verificare</span><span class="sxs-lookup"><span data-stu-id="2f4b9-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="2f4b9-128">Cambiare il server attivo</span><span class="sxs-lookup"><span data-stu-id="2f4b9-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="2f4b9-129">Preparazione</span><span class="sxs-lookup"><span data-stu-id="2f4b9-129">Prepare</span></span>
1. <span data-ttu-id="2f4b9-130">Installare Azure AD Connect, selezionare **modalità di gestione temporanea**e deselezionare **avviare la sincronizzazione** hello ultima pagina nell'installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="2f4b9-131">Questa modalità consente di motore di sincronizzazione hello toorun manualmente.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="2f4b9-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="2f4b9-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="2f4b9-133">Accesso disattivato/sign in e da hello avviare menu selezionare **servizio di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="2f4b9-134">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f4b9-134">Configuration</span></span>
<span data-ttu-id="2f4b9-135">Se sono state apportate modifiche personalizzate toohello primario configurazione server e si desidera toocompare hello con hello server di gestione temporanea, quindi utilizzare [analizzatore di configurazione di Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="2f4b9-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="2f4b9-136">Importare e sincronizzare</span><span class="sxs-lookup"><span data-stu-id="2f4b9-136">Import and Synchronize</span></span>
1. <span data-ttu-id="2f4b9-137">Selezionare **connettori**, e selezionare hello primo connettore con tipo di hello **servizi di dominio Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="2f4b9-138">Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="2f4b9-139">Eseguire questi passaggi per tutti i connettori di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="2f4b9-140">Seleziona hello connettore con tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="2f4b9-141">Fare clic su **Run** (Esegui), selezionare **Full import** (Importazione completa) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="2f4b9-142">Verificare che sia ancora selezionata la scheda hello connettori.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="2f4b9-143">Per ogni connettore con il tipo **Active Directory Domain Services** fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="2f4b9-144">Seleziona hello connettore con tipo **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="2f4b9-145">Fare clic su **Run** (Esegui), selezionare **Delta Synchronization** (Sincronizzazione delta) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="2f4b9-146">È ora esportazione staging cambia tooAzure Active Directory e AD locale (se si utilizza distribuzione ibrida di Exchange).</span><span class="sxs-lookup"><span data-stu-id="2f4b9-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="2f4b9-147">passaggi successivi Hello consentono tooinspect Novità sulla toochange prima di avviare effettivamente directory toohello di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="2f4b9-148">Verificare</span><span class="sxs-lookup"><span data-stu-id="2f4b9-148">Verify</span></span>
1. <span data-ttu-id="2f4b9-149">Avviare un prompt dei comandi e passare troppo`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="2f4b9-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="2f4b9-150">Esegui: `csexport "Name of Connector" %temp%\export.xml /f:x` nome hello del connettore hello è reperibile nel servizio di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="2f4b9-151">Include un too"contoso.com simile nome-AAD" per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="2f4b9-152">Copiare uno script di PowerShell hello dalla sezione hello [CSAnalyzer](#appendix-csanalyzer) tooa file denominato `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="2f4b9-153">Aprire una finestra di PowerShell e Sfoglia cartella toohello in cui è stato creato uno script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="2f4b9-154">Eseguire: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="2f4b9-155">A questo punto si avrà un file denominato **processedusers1.csv**, che può essere esaminato in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="2f4b9-156">Tutte le modifiche inserite toobe esportato tooAzure Active Directory sono riportati in questo file.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="2f4b9-157">Apportare le modifiche necessarie toohello dati o configurazione ed eseguire questi passaggi nuovamente (importazione e sincronizzazione e verifica) finché non sono previste modifiche che stanno toobe esportato hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="2f4b9-158">Cambiare il server attivo</span><span class="sxs-lookup"><span data-stu-id="2f4b9-158">Switch active server</span></span>
1. <span data-ttu-id="2f4b9-159">Nel server attualmente attivo hello, disattivare il server di hello (DirSync/FIM/Azure AD Sync) in modo che non viene esportato tooAzure AD o impostare il valore nella modalità (Azure AD Connect) di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="2f4b9-160">Eseguire l'installazione guidata di hello in server hello **modalità di gestione temporanea** e disabilitare **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="2f4b9-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="2f4b9-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="2f4b9-162">Ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="2f4b9-162">Disaster recovery</span></span>
<span data-ttu-id="2f4b9-163">Parte della progettazione dell'implementazione di hello è tooplan per quali toodo in caso di emergenza in cui si perde il server di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="2f4b9-164">Sono disponibili diversi modelli toouse e quale uno toouse dipende da diversi fattori tra cui:</span><span class="sxs-lookup"><span data-stu-id="2f4b9-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="2f4b9-165">Che cos'è la tolleranza per non è in grado di apportare le modifiche tooobjects in Azure AD durante i tempi di inattività hello?</span><span class="sxs-lookup"><span data-stu-id="2f4b9-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="2f4b9-166">Se si utilizza la sincronizzazione delle password, gli utenti di hello intendesse che hanno una password hello toouse in Azure AD nel caso in cui modificarlo locale?</span><span class="sxs-lookup"><span data-stu-id="2f4b9-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="2f4b9-167">Si ha una dipendenza dalle operazioni in tempo reale, ad esempio il writeback delle password?</span><span class="sxs-lookup"><span data-stu-id="2f4b9-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="2f4b9-168">A seconda hello risposte toothese domande e i criteri dell'organizzazione, una delle seguenti strategie hello può essere implementata:</span><span class="sxs-lookup"><span data-stu-id="2f4b9-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="2f4b9-169">Ricompilare quando necessario.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-169">Rebuild when needed.</span></span>
* <span data-ttu-id="2f4b9-170">Avere un server di standby di riserva, ovvero in **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="2f4b9-171">Usare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-171">Use virtual machines.</span></span>

<span data-ttu-id="2f4b9-172">Se non si utilizza il database di SQL Express incorporati di hello, quindi è inoltre consigliabile esaminare hello [la disponibilità elevata SQL](#sql-high-availability) sezione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="2f4b9-173">Ricompilare quando necessario</span><span class="sxs-lookup"><span data-stu-id="2f4b9-173">Rebuild when needed</span></span>
<span data-ttu-id="2f4b9-174">Una strategia valida è tooplan per una ricompilazione di server, quando necessario.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="2f4b9-175">In genere, l'installazione di hello motore di sincronizzazione e hello importazione iniziale e la sincronizzazione può essere completata entro alcune ore.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="2f4b9-176">Se non esiste un server di riserva non è disponibile, è possibile tootemporarily utilizzare un motore di sincronizzazione hello toohost controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="2f4b9-177">server del motore di sincronizzazione Hello non archivia qualsiasi stato sugli oggetti hello in modo è possibile ricompilare il database di hello dai dati hello in Active Directory e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="2f4b9-178">Hello **sourceAnchor** attributo è usato toojoin hello oggetti locale e cloud hello.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="2f4b9-179">Se si ricompila hello cloud, quindi il motore di sincronizzazione hello associa gli oggetti insieme nuovamente su reinstallazione hello server con gli oggetti locali esistenti.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="2f4b9-180">gli aspetti di Hello è necessario toodocument e salvare sono hello apportate alla configurazione server toohello, ad esempio le regole di filtro e la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="2f4b9-181">Queste configurazioni personalizzate dovranno essere riapplicate prima di avviare la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="2f4b9-182">Avere un server di standby di riserva, in modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="2f4b9-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="2f4b9-183">Nel caso di un ambiente più complesso, è consigliabile avere uno o più server di standby.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="2f4b9-184">Durante l'installazione, è possibile abilitare un server toobe in **modalità di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="2f4b9-185">Per altre informazioni, vedere le [modalità di gestione temporanea](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="2f4b9-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="2f4b9-186">Usare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2f4b9-186">Use virtual machines</span></span>
<span data-ttu-id="2f4b9-187">Un metodo comune e supportato è di tipo motore di sincronizzazione toorun hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="2f4b9-188">Nel caso in cui hello host dispone di un problema, immagine di hello con server hello del motore di sincronizzazione può essere migrato tooanother server.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="2f4b9-189">Disponibilità elevata di SQL</span><span class="sxs-lookup"><span data-stu-id="2f4b9-189">SQL High Availability</span></span>
<span data-ttu-id="2f4b9-190">Se non si utilizza SQL Server Express con Azure AD Connect hello, disponibilità elevata per SQL Server deve inoltre essere considerata.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="2f4b9-191">soluzioni a disponibilità elevata Hello supportate includono il clustering di SQL e AOA (gruppi di disponibilità AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="2f4b9-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="2f4b9-192">mentre il mirroring è una delle soluzioni non supportate.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="2f4b9-193">È stato aggiunto il supporto per SQL AOA tooAzure AD Connect versione 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="2f4b9-194">È necessario abilitare SQL AOA prima di installare Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="2f4b9-195">Durante l'installazione, Azure AD Connect rileva se istanza SQL hello fornita è abilitato per SQL AOA o meno.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="2f4b9-196">Se SQL AOA è abilitata, Azure AD Connect ulteriormente determina se SQL AOA è toouse configurato di replica sincrona o asincrona.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="2f4b9-197">Quando si configurano hello listener del gruppo di disponibilità, è consigliabile impostare hello RegisterAllProvidersIP proprietà too0.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="2f4b9-198">In questo modo Azure AD Connect utilizza attualmente tooSQL tooconnect SQL Native Client e SQL Native Client non supporta l'utilizzo di hello della proprietà MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="2f4b9-199">Appendice CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="2f4b9-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="2f4b9-200">Vedere la sezione hello [verificare](#verify) sulla toouse questo script.</span><span class="sxs-lookup"><span data-stu-id="2f4b9-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="2f4b9-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f4b9-201">Next steps</span></span>
<span data-ttu-id="2f4b9-202">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="2f4b9-202">**Overview topics**</span></span>  

* [<span data-ttu-id="2f4b9-203">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="2f4b9-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="2f4b9-204">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f4b9-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
