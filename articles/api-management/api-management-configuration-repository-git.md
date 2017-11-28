---
title: aaaConfigure al servizio Gestione API tramite Git - Azure | Documenti Microsoft
description: Informazioni su come toosave e configurare la configurazione del servizio Gestione API tramite Git.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="9ca24-103">Come toosave e configurare la configurazione del servizio Gestione API tramite Git</span><span class="sxs-lookup"><span data-stu-id="9ca24-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="9ca24-104">Ogni istanza del servizio Gestione API gestisce un database di configurazione che contiene informazioni sulla configurazione di hello e i metadati per l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="9ca24-105">Possibile modificare l'istanza del servizio toohello modificando un'impostazione nel portale di pubblicazione hello, usando un cmdlet di PowerShell o effettua una chiamata API REST.</span><span class="sxs-lookup"><span data-stu-id="9ca24-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="9ca24-106">Inoltre metodi toothese, è inoltre possibile gestire la configurazione di istanza del servizio tramite Git, l'abilitazione di scenari di gestione del servizio, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9ca24-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="9ca24-107">Controllo delle versioni della configurazione: downolad e archiviazione di versioni diverse della configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="9ca24-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="9ca24-108">BULK modifiche di configurazione: l'apportare modifiche toomultiple parti della configurazione del servizio nel repository locale e l'integrazione di server di toohello indietro di hello modifiche con una singola operazione</span><span class="sxs-lookup"><span data-stu-id="9ca24-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="9ca24-109">Toolchain Git e flusso di lavoro - utilizzare gli strumenti Git hello e flussi di lavoro che si ha già familiarità con</span><span class="sxs-lookup"><span data-stu-id="9ca24-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="9ca24-110">Hello seguente diagramma mostra una panoramica di hello modi tooconfigure all'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="9ca24-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Configurare Git][api-management-git-configure]

<span data-ttu-id="9ca24-112">Quando si apportano modifiche tooyour servizio tramite il portale di pubblicazione hello, i cmdlet di PowerShell o hello API REST, si sta gestendo il database di configurazione del servizio usando hello `https://{name}.management.azure-api.net` endpoint, come mostrato sul lato destro hello del diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="9ca24-113">bordo sinistro del diagramma hello Hello viene illustrato come è possibile gestire la configurazione del servizio tramite Git e repository Git per il servizio disponibile all'indirizzo `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="9ca24-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="9ca24-114">Hello alla procedura seguente viene fornita una panoramica di gestione all'istanza del servizio Gestione API tramite Git.</span><span class="sxs-lookup"><span data-stu-id="9ca24-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="9ca24-115">Accedere alla configurazione Git nel servizio</span><span class="sxs-lookup"><span data-stu-id="9ca24-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="9ca24-116">Salvare il repository Git di tooyour database di configurazione di servizio</span><span class="sxs-lookup"><span data-stu-id="9ca24-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="9ca24-117">Clona macchina locale tooyour di hello repository Git</span><span class="sxs-lookup"><span data-stu-id="9ca24-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="9ca24-118">Pull repository più recente di hello verso il basso tooyour di computer locale e il commit e push repository tooyour indietro delle modifiche</span><span class="sxs-lookup"><span data-stu-id="9ca24-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="9ca24-119">Distribuire le modifiche di hello dal repository di in un database di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="9ca24-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="9ca24-120">Questo articolo viene descritto come tooenable e utilizzare Git toomanage la configurazione del servizio e fornisce un riferimento per hello file e cartelle nel repository Git hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="9ca24-121">Accedere alla configurazione Git nel servizio</span><span class="sxs-lookup"><span data-stu-id="9ca24-121">Access Git configuration in your service</span></span>
<span data-ttu-id="9ca24-122">È possibile visualizzare rapidamente lo stato di hello della configurazione di Git visualizzando icona Git hello nell'angolo superiore destro di hello del portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="9ca24-123">In questo esempio, il messaggio di stato hello indica che non vi siano repository toohello le modifiche non salvate.</span><span class="sxs-lookup"><span data-stu-id="9ca24-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="9ca24-124">Questo avviene perché il database di configurazione del servizio Gestione API hello non è ancora stato salvato toohello repository.</span><span class="sxs-lookup"><span data-stu-id="9ca24-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Stato Git][api-management-git-icon-enable]

<span data-ttu-id="9ca24-126">tooview e configurare le impostazioni di configurazione di Git, è possibile fare clic sull'icona Git hello o fare clic su hello **sicurezza** menu e passare toohello **repository di configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="9ca24-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Abilitare GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="9ca24-128">Le informazioni riservate che non sono definiti come proprietà verranno archiviate nel repository di hello e rimarranno nella cronologia di finché non si disabilitare e riabilitare l'accesso di Git.</span><span class="sxs-lookup"><span data-stu-id="9ca24-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="9ca24-129">Proprietà forniscono toomanage un luogo sicuro i valori di stringa costante, inclusi i segreti, in tutte le API criteri di configurazione e, pertanto non è toostore loro direttamente nelle istruzioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="9ca24-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="9ca24-130">Per ulteriori informazioni, vedere [come proprietà toouse nei criteri di gestione API di Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="9ca24-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="9ca24-131">Per informazioni sull'attivazione e disabilitazione dell'accesso Git utilizzando hello API REST, vedere [abilitare o disabilitare l'accesso di Git utilizzando l'API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="9ca24-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="9ca24-132">repository Git di toosave hello servizio configurazione toohello</span><span class="sxs-lookup"><span data-stu-id="9ca24-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="9ca24-133">innanzitutto Hello prima della clonazione del repository hello è stato corrente di hello toosave del repository di toohello hello servizio configurazione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="9ca24-134">Fare clic su **Salva configurazione toorepository**.</span><span class="sxs-lookup"><span data-stu-id="9ca24-134">Click **Save configuration toorepository**.</span></span>

![Salvare la configurazione][api-management-save-configuration]

<span data-ttu-id="9ca24-136">Apportare le modifiche desiderate nella schermata di conferma hello e fare clic su **Ok** toosave.</span><span class="sxs-lookup"><span data-stu-id="9ca24-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Salvare la configurazione][api-management-save-configuration-confirm]

<span data-ttu-id="9ca24-138">Dopo alcuni istanti configurazione hello viene salvato e viene visualizzato lo stato configurazione hello repository hello, tra cui hello data e ora dell'ultima modifica della configurazione hello e l'ultima sincronizzazione di hello tra la configurazione del servizio hello e hello repository.</span><span class="sxs-lookup"><span data-stu-id="9ca24-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Stato della configurazione][api-management-configuration-status]

<span data-ttu-id="9ca24-140">Dopo aver salvata la configurazione hello toohello repository, possono essere clonato.</span><span class="sxs-lookup"><span data-stu-id="9ca24-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="9ca24-141">Per informazioni su come eseguire questa operazione utilizzando hello API REST, vedere [configurazione Commit snapshot utilizzando l'API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="9ca24-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="9ca24-142">computer locale tooyour tooclone hello repository</span><span class="sxs-lookup"><span data-stu-id="9ca24-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="9ca24-143">tooclone un repository, è necessario repository tooyour di hello URL, un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="9ca24-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="9ca24-144">Hello nome utente e l'URL vengono visualizzati parte superiore di hello di hello **repository di configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="9ca24-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Clonare in Git][api-management-configuration-git-clone]

<span data-ttu-id="9ca24-146">password Hello viene generata nella parte inferiore di hello di hello **repository di configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="9ca24-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Generare password][api-management-generate-password]

<span data-ttu-id="9ca24-148">toogenerate una password, verificare innanzitutto che hello **scadenza** toohello desiderato data di scadenza e l'ora di impostare e quindi fare clic su **genera Token**.</span><span class="sxs-lookup"><span data-stu-id="9ca24-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Password][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="9ca24-150">Prendere nota della password.</span><span class="sxs-lookup"><span data-stu-id="9ca24-150">Make a note of this password.</span></span> <span data-ttu-id="9ca24-151">Dopo avere chiuso la password di hello pagina non essere visualizzata nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9ca24-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="9ca24-152">strumento Hello seguono esempi di utilizzo hello Git Bash da [Git per Windows](http://www.git-scm.com/downloads) ma è possibile utilizzare qualsiasi strumento Git che si ha familiarità con.</span><span class="sxs-lookup"><span data-stu-id="9ca24-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="9ca24-153">Aprire lo strumento di Git nella cartella desiderata hello ed eseguire hello successivo comando tooclone hello git repository tooyour locale, utilizzando il comando hello fornito dal portale di server di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9ca24-154">Fornire nome utente hello e una password quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="9ca24-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="9ca24-155">Se si ricevono errori, provare a modificare il `git clone` comando tooinclude hello utente nome e una password, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9ca24-156">Se si fornisce un errore, provare a parte password hello del comando hello di codifica degli URL.</span><span class="sxs-lookup"><span data-stu-id="9ca24-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="9ca24-157">Un modo rapido toodo tratta tooopen Visual Studio e il comando seguente di hello di problema in hello **finestra controllo immediato**.</span><span class="sxs-lookup"><span data-stu-id="9ca24-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="9ca24-158">hello tooopen **finestra controllo immediato**, aprire qualsiasi soluzione o progetto in Visual Studio oppure creare una nuova applicazione console vuota, scegliere **Windows**, **immediato** da Hello **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="9ca24-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="9ca24-159">Utilizzare password hello codificato con il nome e del repository percorso tooconstruct hello git comando utente.</span><span class="sxs-lookup"><span data-stu-id="9ca24-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="9ca24-160">Una volta è clonazione del repository hello è possibile visualizzare e utilizzarlo nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="9ca24-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="9ca24-161">Per altre informazioni, vedere [Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="9ca24-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="9ca24-162">tooupdate il repository locale con una configurazione dell'istanza del servizio più recente hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="9ca24-163">Se l'istanza del servizio Gestione API tooyour le modifiche apportate nel portale di pubblicazione hello oppure utilizzando hello API REST, è necessario salvare questi repository toohello modifiche prima di aggiornare il repository locale con le modifiche più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="9ca24-164">toodo, fare clic su **Salva configurazione toorepository** su hello **repository di configurazioni** scheda nel portale di pubblicazione hello e quindi rilasciare hello seguente comando nel repository locale.</span><span class="sxs-lookup"><span data-stu-id="9ca24-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="9ca24-165">Prima di eseguire `git pull` assicurarsi che sia nella cartella hello per il repository locale.</span><span class="sxs-lookup"><span data-stu-id="9ca24-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="9ca24-166">Se è stato completato hello `git clone` comando, è necessario modificare i repository di hello directory tooyour eseguendo un comando simile hello seguente.</span><span class="sxs-lookup"><span data-stu-id="9ca24-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="9ca24-167">modifiche toopush dal repository di server toohello di repository locale</span><span class="sxs-lookup"><span data-stu-id="9ca24-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="9ca24-168">toopush cambia dall'archivio locale del repository toohello server, è necessario eseguire il commit delle modifiche e quindi inviarli toohello repository del server.</span><span class="sxs-lookup"><span data-stu-id="9ca24-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="9ca24-169">toocommit le modifiche, aprire lo strumento di comando Git, switch toohello directory del repository locale e hello problema i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9ca24-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="9ca24-170">toopush tutti hello viene eseguito il commit toohello server, eseguire hello il seguente comando.</span><span class="sxs-lookup"><span data-stu-id="9ca24-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="9ca24-171">toodeploy qualsiasi istanza del servizio Gestione API servizio configurazione modifiche toohello</span><span class="sxs-lookup"><span data-stu-id="9ca24-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="9ca24-172">Dopo aver eseguito il commit e push toohello repository del server le modifiche locali, è possibile distribuirli tooyour istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="9ca24-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Distribuire][api-management-configuration-deploy]

<span data-ttu-id="9ca24-174">Per informazioni su come eseguire questa operazione utilizzando hello API REST, vedere [distribuire Git Cambia database tooconfiguration utilizzando l'API REST di hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="9ca24-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="9ca24-175">Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale</span><span class="sxs-lookup"><span data-stu-id="9ca24-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="9ca24-176">Hello file e cartelle nel repository git locale hello contengono informazioni di configurazione hello sull'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="9ca24-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="9ca24-177">Item</span></span> | <span data-ttu-id="9ca24-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9ca24-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9ca24-179">Cartella api-management radice</span><span class="sxs-lookup"><span data-stu-id="9ca24-179">root api-management folder</span></span> |<span data-ttu-id="9ca24-180">Contiene una configurazione di livello principale per l'istanza del servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="9ca24-181">Cartella apis</span><span class="sxs-lookup"><span data-stu-id="9ca24-181">apis folder</span></span> |<span data-ttu-id="9ca24-182">Contiene la configurazione hello hello API nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="9ca24-183">Cartella groups</span><span class="sxs-lookup"><span data-stu-id="9ca24-183">groups folder</span></span> |<span data-ttu-id="9ca24-184">Contiene la configurazione hello gruppi hello nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="9ca24-185">Cartella policies</span><span class="sxs-lookup"><span data-stu-id="9ca24-185">policies folder</span></span> |<span data-ttu-id="9ca24-186">Contiene i criteri di hello nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="9ca24-187">Cartella portalStyles</span><span class="sxs-lookup"><span data-stu-id="9ca24-187">portalStyles folder</span></span> |<span data-ttu-id="9ca24-188">Contiene configurazione hello per le personalizzazioni del portale per sviluppatori di hello nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="9ca24-189">Cartella products</span><span class="sxs-lookup"><span data-stu-id="9ca24-189">products folder</span></span> |<span data-ttu-id="9ca24-190">Contiene la configurazione hello prodotti hello nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="9ca24-191">Cartella templates</span><span class="sxs-lookup"><span data-stu-id="9ca24-191">templates folder</span></span> |<span data-ttu-id="9ca24-192">Contiene configurazione hello per i modelli di messaggio di posta elettronica hello nell'istanza di servizio hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="9ca24-193">Ogni cartella può contenere uno o più file e in alcuni casi una o più cartelle, ad esempio una cartella per ogni API, prodotto o gruppo.</span><span class="sxs-lookup"><span data-stu-id="9ca24-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="9ca24-194">file Hello all'interno di ogni cartella sono specifici per il tipo di entità hello descritto dal nome della cartella hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="9ca24-195">Tipo file</span><span class="sxs-lookup"><span data-stu-id="9ca24-195">File type</span></span> | <span data-ttu-id="9ca24-196">Scopo</span><span class="sxs-lookup"><span data-stu-id="9ca24-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="9ca24-197">json</span><span class="sxs-lookup"><span data-stu-id="9ca24-197">json</span></span> |<span data-ttu-id="9ca24-198">Informazioni di configurazione di entità corrispondente di hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="9ca24-199">html</span><span class="sxs-lookup"><span data-stu-id="9ca24-199">html</span></span> |<span data-ttu-id="9ca24-200">Descrizioni relative entità hello, spesso visualizzato nel portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="9ca24-201">xml</span><span class="sxs-lookup"><span data-stu-id="9ca24-201">xml</span></span> |<span data-ttu-id="9ca24-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="9ca24-202">Policy statements</span></span> |
| <span data-ttu-id="9ca24-203">css</span><span class="sxs-lookup"><span data-stu-id="9ca24-203">css</span></span> |<span data-ttu-id="9ca24-204">Fogli di stile per la personalizzazione del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="9ca24-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="9ca24-205">Questi file possono essere creati, eliminati, modificati e gestiti nel file system locale e modifiche hello distribuiti toohello indietro all'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="9ca24-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca24-206">Hello entità seguenti non sono contenute nel repository Git hello e non può essere configurata tramite Git.</span><span class="sxs-lookup"><span data-stu-id="9ca24-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="9ca24-207">Utenti</span><span class="sxs-lookup"><span data-stu-id="9ca24-207">Users</span></span>
> * <span data-ttu-id="9ca24-208">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="9ca24-208">Subscriptions</span></span>
> * <span data-ttu-id="9ca24-209">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9ca24-209">Properties</span></span>
> * <span data-ttu-id="9ca24-210">Entità del portale per sviluppatori diverse dagli stili</span><span class="sxs-lookup"><span data-stu-id="9ca24-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="9ca24-211">Cartella api-management radice</span><span class="sxs-lookup"><span data-stu-id="9ca24-211">Root api-management folder</span></span>
<span data-ttu-id="9ca24-212">radice Hello `api-management` cartella contiene un `configuration.json` file che contiene informazioni sull'istanza del servizio hello in hello seguente formato di livello principale.</span><span class="sxs-lookup"><span data-stu-id="9ca24-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="9ca24-213">Hello primi quattro impostazioni (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, e `UserRegistrationTermsConsentRequired`) eseguire il mapping toohello seguendo le impostazioni di hello **identità** scheda hello **sicurezza** sezione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="9ca24-214">Impostazione</span><span class="sxs-lookup"><span data-stu-id="9ca24-214">Identity setting</span></span> | <span data-ttu-id="9ca24-215">Esegue il mapping troppo</span><span class="sxs-lookup"><span data-stu-id="9ca24-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="9ca24-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="9ca24-216">RegistrationEnabled</span></span> |<span data-ttu-id="9ca24-217">**Reindirizzare gli utenti anonimi toosign-pagina** casella di controllo</span><span class="sxs-lookup"><span data-stu-id="9ca24-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="9ca24-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="9ca24-218">UserRegistrationTerms</span></span> |<span data-ttu-id="9ca24-219">**Terms of use on user signup** </span><span class="sxs-lookup"><span data-stu-id="9ca24-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="9ca24-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="9ca24-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="9ca24-221">**Show terms of use on signup page**</span><span class="sxs-lookup"><span data-stu-id="9ca24-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="9ca24-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="9ca24-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="9ca24-223">**Richiedi consenso** </span><span class="sxs-lookup"><span data-stu-id="9ca24-223">**Require consent** checkbox</span></span> |

![Impostazioni di identità][api-management-identity-settings]

<span data-ttu-id="9ca24-225">Hello quattro impostazioni (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, e `DelegationValidationKey`) eseguire il mapping toohello seguendo le impostazioni di hello **delega** scheda hello **sicurezza** sezione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="9ca24-226">Impostazione</span><span class="sxs-lookup"><span data-stu-id="9ca24-226">Delegation setting</span></span> | <span data-ttu-id="9ca24-227">Esegue il mapping troppo</span><span class="sxs-lookup"><span data-stu-id="9ca24-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="9ca24-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="9ca24-228">DelegationEnabled</span></span> |<span data-ttu-id="9ca24-229">Casella di controllo **Delegate sign-in & sign-up** (Delega accesso e iscrizione)</span><span class="sxs-lookup"><span data-stu-id="9ca24-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="9ca24-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="9ca24-230">DelegationUrl</span></span> |<span data-ttu-id="9ca24-231">**Delegation endpoint URL**</span><span class="sxs-lookup"><span data-stu-id="9ca24-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="9ca24-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="9ca24-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="9ca24-233">**Delegate product subscription**</span><span class="sxs-lookup"><span data-stu-id="9ca24-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="9ca24-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="9ca24-234">DelegationValidationKey</span></span> |<span data-ttu-id="9ca24-235">**Delegate Validation Key**</span><span class="sxs-lookup"><span data-stu-id="9ca24-235">**Delegate Validation Key** textbox</span></span> |

![Impostazioni di delega][api-management-delegation-settings]

<span data-ttu-id="9ca24-237">impostazione finale, Hello `$ref-policy`, esegue il mapping di file di istruzioni toohello criteri globali per l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="9ca24-238">Cartella apis</span><span class="sxs-lookup"><span data-stu-id="9ca24-238">apis folder</span></span>
<span data-ttu-id="9ca24-239">Hello `apis` cartella contiene una cartella per ciascuna API nell'istanza di servizio hello che contiene i seguenti elementi hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="9ca24-240">`apis\<api name>\configuration.json`-Questa configurazione hello per hello API e contiene informazioni sull'URL del servizio back-end hello e operazioni hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="9ca24-241">Si tratta di hello stesse informazioni che verrebbero restituite se fosse toocall [ottenere un'API specifica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` in `application/json` formato.</span><span class="sxs-lookup"><span data-stu-id="9ca24-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="9ca24-242">`apis\<api name>\api.description.html`-si tratta di descrizione hello di hello API e corrispondono toohello `description` proprietà di hello [entità API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="9ca24-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="9ca24-243">`apis\<api name>\operations\`-Questa cartella contiene `<operation name>.description.html` file toohello operazioni mappa in hello API.</span><span class="sxs-lookup"><span data-stu-id="9ca24-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="9ca24-244">Ogni file contiene la descrizione hello di una singola operazione di hello API che consente di associare toohello `description` proprietà di hello [entità operation](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello API REST.</span><span class="sxs-lookup"><span data-stu-id="9ca24-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="9ca24-245">Cartella groups</span><span class="sxs-lookup"><span data-stu-id="9ca24-245">groups folder</span></span>
<span data-ttu-id="9ca24-246">Hello `groups` cartella contiene una cartella per ogni gruppo definito nell'istanza di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="9ca24-247">`groups\<group name>\configuration.json`-si tratta di hello configurazione per il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="9ca24-248">Si tratta di hello stesse informazioni che verrebbero restituite se fosse hello toocall [ottenere un gruppo specifico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operazione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="9ca24-249">`groups\<group name>\description.html`-si tratta di descrizione hello del gruppo di hello e corrispondono toohello `description` proprietà di hello [gruppo entità](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="9ca24-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="9ca24-250">Cartella policies</span><span class="sxs-lookup"><span data-stu-id="9ca24-250">policies folder</span></span>
<span data-ttu-id="9ca24-251">Hello `policies` cartella contiene le istruzioni dei criteri di hello per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="9ca24-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="9ca24-252">`policies\global.xml` : contiene i criteri definiti in ambito globale per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="9ca24-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="9ca24-253">`policies\apis\<api name>\`: se sono presenti criteri definiti nell'ambito delle API, tali criteri sono contenuti in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="9ca24-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="9ca24-254">`policies\apis\<api name>\<operation name>\`cartella - se si dispone di tutti i criteri definiti nell'ambito di operazione, sono contenuti in questa cartella `<operation name>.xml` file che eseguono il mapping toohello istruzioni dei criteri per ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="9ca24-255">`policies\products\`-Se si dispone di tutti i criteri definiti nell'ambito del prodotto, sono contenuti in questa cartella contiene `<product name>.xml` file che eseguono il mapping toohello istruzioni dei criteri per ogni prodotto.</span><span class="sxs-lookup"><span data-stu-id="9ca24-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="9ca24-256">Cartella portalStyles</span><span class="sxs-lookup"><span data-stu-id="9ca24-256">portalStyles folder</span></span>
<span data-ttu-id="9ca24-257">Hello `portalStyles` cartella contiene i fogli di stile e di configurazione per le personalizzazioni del portale per sviluppatori per l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="9ca24-258">`portalStyles\configuration.json`-contiene i nomi di hello hello dei fogli di stile utilizzati dal portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="9ca24-259">`portalStyles\<style name>.css`-ogni `<style name>.css` file contiene gli stili per il portale per sviluppatori di hello (`Preview.css` e `Production.css` per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="9ca24-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="9ca24-260">Cartella products</span><span class="sxs-lookup"><span data-stu-id="9ca24-260">products folder</span></span>
<span data-ttu-id="9ca24-261">Hello `products` cartella contiene una cartella per ogni prodotto definito nell'istanza di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="9ca24-262">`products\<product name>\configuration.json`-si tratta di configurazione hello hello prodotto.</span><span class="sxs-lookup"><span data-stu-id="9ca24-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="9ca24-263">Si tratta di hello stesse informazioni che verrebbero restituite se fosse hello toocall [ottenere un prodotto specifico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operazione.</span><span class="sxs-lookup"><span data-stu-id="9ca24-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="9ca24-264">`products\<product name>\product.description.html`-si tratta di descrizione hello del prodotto di hello e corrispondono toohello `description` proprietà di hello [entità product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello API REST.</span><span class="sxs-lookup"><span data-stu-id="9ca24-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="9ca24-265">Modelli</span><span class="sxs-lookup"><span data-stu-id="9ca24-265">templates</span></span>
<span data-ttu-id="9ca24-266">Hello `templates` cartella contiene la configurazione hello [modelli di posta elettronica](api-management-howto-configure-notifications.md) hello di istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="9ca24-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="9ca24-267">`<template name>\configuration.json`-si tratta di hello configurazione per il modello di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="9ca24-268">`<template name>\body.html`-si tratta corpo hello del modello di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="9ca24-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ca24-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ca24-269">Next steps</span></span>
<span data-ttu-id="9ca24-270">Per informazioni su altri modi di toomanage all'istanza del servizio, vedere:</span><span class="sxs-lookup"><span data-stu-id="9ca24-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="9ca24-271">Gestire l'istanza di servizio utilizzando i cmdlet di PowerShell seguente hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="9ca24-272">Informazioni di riferimento sui cmdlet di PowerShell per la distribuzione dei servizi</span><span class="sxs-lookup"><span data-stu-id="9ca24-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="9ca24-273">Informazioni di riferimento sui cmdlet di PowerShell per la gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="9ca24-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="9ca24-274">Gestire l'istanza di servizio nel portale di pubblicazione hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="9ca24-275">Gestire la prima API in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="9ca24-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="9ca24-276">Gestire l'istanza di servizio utilizzando l'API REST hello</span><span class="sxs-lookup"><span data-stu-id="9ca24-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="9ca24-277">Informazioni di riferimento sull'API REST di Gestione API</span><span class="sxs-lookup"><span data-stu-id="9ca24-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="9ca24-278">Guardare un video introduttivo</span><span class="sxs-lookup"><span data-stu-id="9ca24-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




