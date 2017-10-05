---
title: Configurare il servizio Gestione API tramite Git - Azure | Documentazione Microsoft
description: Informazioni su come salvare e configurare la configurazione del servizio Gestione API tramite Git
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
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="336ca-103">Come salvare e configurare la configurazione del servizio Gestione API tramite Git</span><span class="sxs-lookup"><span data-stu-id="336ca-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="336ca-104">Ogni istanza del servizio Gestione API gestisce un database di configurazione che contiene informazioni sulla configurazione e i metadati dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="336ca-105">Per apportare modifiche all'istanza del servizio è possibile modificare un'impostazione nel portale di pubblicazione, usare un cmdlet di PowerShell o eseguire una chiamata all'API REST.</span><span class="sxs-lookup"><span data-stu-id="336ca-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="336ca-106">Oltre a questi metodi, è possibile gestire la configurazione dell'istanza del servizio tramite Git. Ciò consente scenari di gestione del servizio diversi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="336ca-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="336ca-107">Controllo delle versioni della configurazione: downolad e archiviazione di versioni diverse della configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="336ca-108">Modifiche in blocco alla configurazione: esecuzione di modifiche in più punti della configurazione del servizio all'interno del repository locale e integrazione delle modifiche nel server con un'unica operazione</span><span class="sxs-lookup"><span data-stu-id="336ca-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="336ca-109">Serie di strumenti e flussi di lavoro Git familiari: possibilità di usare gli strumenti e i flussi di lavoro Git con cui si ha familiarità</span><span class="sxs-lookup"><span data-stu-id="336ca-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="336ca-110">Il diagramma seguente offre una panoramica dei diversi modi in cui è possibile configurare un'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="336ca-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Configurare Git][api-management-git-configure]

<span data-ttu-id="336ca-112">Quando si apportano modifiche al servizio tramite il portale di pubblicazione, i cmdlet di PowerShell o l'API REST, la gestione del database di configurazione del servizio avviene tramite l'endpoint `https://{name}.management.azure-api.net` , come mostrato nella parte destra del diagramma.</span><span class="sxs-lookup"><span data-stu-id="336ca-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="336ca-113">Il lato sinistro del diagramma illustra come gestire la configurazione del servizio tramite Git e il repository Git per il servizio, disponibile all'indirizzo `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="336ca-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="336ca-114">I passaggi seguenti offrono una panoramica della gestione dell'istanza del servizio Gestione API tramite Git.</span><span class="sxs-lookup"><span data-stu-id="336ca-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="336ca-115">Accedere alla configurazione Git nel servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="336ca-116">Salvare il database di configurazione del servizio nel repository Git</span><span class="sxs-lookup"><span data-stu-id="336ca-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="336ca-117">Clonare il repository Git nel computer locale</span><span class="sxs-lookup"><span data-stu-id="336ca-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="336ca-118">Estrarre il repository più recente nel computer locale ed eseguire il commit e il push delle modifiche nel repository</span><span class="sxs-lookup"><span data-stu-id="336ca-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="336ca-119">Distribuire le modifiche dal repository nel database di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="336ca-120">Questo articolo descrive come abilitare e usare Git per gestire la configurazione del servizio e costituisce un riferimento per i file e le cartelle nel repository Git.</span><span class="sxs-lookup"><span data-stu-id="336ca-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="336ca-121">Accedere alla configurazione Git nel servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-121">Access Git configuration in your service</span></span>
<span data-ttu-id="336ca-122">È possibile visualizzare rapidamente lo stato della configurazione di Git visualizzando l'icona Git nell'angolo superiore destro del portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="336ca-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="336ca-123">In questo esempio, il messaggio di stato indica che ci sono modifiche non salvate nel repository.</span><span class="sxs-lookup"><span data-stu-id="336ca-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="336ca-124">Questo avviene perché il database di configurazione del servizio Gestione API non è ancora stato salvato nel repository.</span><span class="sxs-lookup"><span data-stu-id="336ca-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Stato Git][api-management-git-icon-enable]

<span data-ttu-id="336ca-126">Per visualizzare e configurare le impostazioni di configurazione di Git, è possibile fare clic sull'icona Git oppure fare clic sul menu **Security** (Sicurezza) e passare alla scheda **Configuration repository** (Repository configurazioni).</span><span class="sxs-lookup"><span data-stu-id="336ca-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Abilitare GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="336ca-128">Eventuali segreti non definiti come proprietà verranno archiviati nel repository e rimarranno nella cronologia di questo finché non si disabilita e riabilita l'accesso a Git.</span><span class="sxs-lookup"><span data-stu-id="336ca-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="336ca-129">Le proprietà rappresentano un luogo sicuro per gestire i valori stringa costanti, segreti inclusi, attraverso tutte le configurazioni e tutti i criteri per le API. Non è quindi necessario archiviarli direttamente nelle istruzioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="336ca-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="336ca-130">Per altre informazioni, vedere [Come usare le proprietà nei criteri di Gestione API di Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="336ca-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="336ca-131">Per informazioni sull'abilitazione o la disabilitazione dell'accesso a Git mediante l'API REST, vedere la [pagina relativa a questo argomento](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="336ca-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="336ca-132">Per salvare la configurazione del servizio nel repository Git</span><span class="sxs-lookup"><span data-stu-id="336ca-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="336ca-133">Il primo passaggio prima della clonazione del repository corrisponde al salvataggio dello stato corrente della configurazione del servizio nel repository.</span><span class="sxs-lookup"><span data-stu-id="336ca-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="336ca-134">Fare clic su **Save configuration to repository**.</span><span class="sxs-lookup"><span data-stu-id="336ca-134">Click **Save configuration to repository**.</span></span>

![Salvare la configurazione][api-management-save-configuration]

<span data-ttu-id="336ca-136">Apportare le modifiche desiderate nella schermata di conferma e fare clic su **Ok** per salvare.</span><span class="sxs-lookup"><span data-stu-id="336ca-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Salvare la configurazione][api-management-save-configuration-confirm]

<span data-ttu-id="336ca-138">Dopo qualche secondo la configurazione viene salvata e viene visualizzato lo stato della configurazione del repository, con la data e l'ora dell'ultima modifica alla configurazione e l'ultima sincronizzazione tra la configurazione del servizio e il repository.</span><span class="sxs-lookup"><span data-stu-id="336ca-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Stato della configurazione][api-management-configuration-status]

<span data-ttu-id="336ca-140">Dopo che la configurazione è stata salvata nel repository, può essere clonata.</span><span class="sxs-lookup"><span data-stu-id="336ca-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="336ca-141">Per informazioni sull'esecuzione di questa operazione tramite l'API REST, vedere la [pagina relativa all'esecuzione del commit di uno snapshot della configurazione tramite l'API REST](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="336ca-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="336ca-142">Per clonare il repository nel computer locale</span><span class="sxs-lookup"><span data-stu-id="336ca-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="336ca-143">Per clonare un repository, sono necessari l'URL del repository, un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="336ca-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="336ca-144">Il nome utente e l'URL sono visualizzati nella parte superiore della scheda **Configuration repository** .</span><span class="sxs-lookup"><span data-stu-id="336ca-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Clonare in Git][api-management-configuration-git-clone]

<span data-ttu-id="336ca-146">La password viene generata nella parte inferiore della scheda **Configuration repository** .</span><span class="sxs-lookup"><span data-stu-id="336ca-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Generare password][api-management-generate-password]

<span data-ttu-id="336ca-148">Per generare una password, verificare prima di tutto che il campo **Expiry** (Scadenza) sia impostato sulla data e sull'ora di scadenza desiderate e quindi fare clic su **Generate Token** (Genera token).</span><span class="sxs-lookup"><span data-stu-id="336ca-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Password][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="336ca-150">Prendere nota della password.</span><span class="sxs-lookup"><span data-stu-id="336ca-150">Make a note of this password.</span></span> <span data-ttu-id="336ca-151">Una volta chiusa questa pagina, la password non verrà più visualizzata.</span><span class="sxs-lookup"><span data-stu-id="336ca-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="336ca-152">Gli esempi seguenti usano lo strumento Git Bash di [Git per Windows](http://www.git-scm.com/downloads) ma è possibile usare qualsiasi strumento Git con cui si abbia familiarità.</span><span class="sxs-lookup"><span data-stu-id="336ca-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="336ca-153">Aprire lo strumento Git nella cartella desiderata ed eseguire il comando seguente per clonare il repository Git nel computer locale, usando il comando fornito dal portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="336ca-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="336ca-154">Quando richiesto,specificare il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="336ca-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="336ca-155">Se si ricevono errori, provare a modificare il comando `git clone` includendo il nome utente e password, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="336ca-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="336ca-156">Se viene generato un errore, provare a codificare con URL la parte della password del comando.</span><span class="sxs-lookup"><span data-stu-id="336ca-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="336ca-157">Un metodo rapido per eseguire questa operazione consiste nell'aprire Visual Studio, eseguendo il comando seguente nella **finestra di controllo immediato**.</span><span class="sxs-lookup"><span data-stu-id="336ca-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="336ca-158">Per aprire la **finestra di controllo immediato**, aprire qualsiasi soluzione o progetto in Visual Studio oppure creare una nuova applicazione console vuota e quindi **Finestre** e quindi **Controllo immediato** dal menu **Debug**.</span><span class="sxs-lookup"><span data-stu-id="336ca-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="336ca-159">Per creare il comando git, usare la password codificata con il nome utente e il percorso del repository.</span><span class="sxs-lookup"><span data-stu-id="336ca-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="336ca-160">Una volta clonato il repository, è possibile visualizzarlo e usarlo nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="336ca-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="336ca-161">Per altre informazioni, vedere [Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="336ca-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="336ca-162">Per aggiornare il repository locale con la configurazione dell'istanza del servizio più recente</span><span class="sxs-lookup"><span data-stu-id="336ca-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="336ca-163">Se si apportano modifiche all'istanza del servizio Gestione API nel portale di pubblicazione o tramite l'API REST, è necessario salvare le modifiche nel repository prima di aggiornare il repository locale con le modifiche più recenti.</span><span class="sxs-lookup"><span data-stu-id="336ca-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="336ca-164">A tale scopo, fare clic su **Save configuration to repository** (Salva configurazione in repository) nella scheda **Configuration repository** (Repository configurazioni) del portale di pubblicazione e quindi eseguire questo comando nel repository locale.</span><span class="sxs-lookup"><span data-stu-id="336ca-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="336ca-165">Prima di eseguire `git pull` assicurarsi di trovarsi nella cartella del repository locale.</span><span class="sxs-lookup"><span data-stu-id="336ca-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="336ca-166">Se è appena stato eseguito il comando `git clone` , è necessario modificare la directory con quella del repository tramite un comando simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="336ca-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="336ca-167">Per eseguire il push delle modifiche dal repository locale al repository del server</span><span class="sxs-lookup"><span data-stu-id="336ca-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="336ca-168">Per eseguire il push delle modifiche dal repository locale al repository del server, è prima necessario eseguire il commit delle modifiche stesse.</span><span class="sxs-lookup"><span data-stu-id="336ca-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="336ca-169">Per eseguire il commit delle modifiche, aprire lo strumento dei comandi Git, passare alla directory del repository locale ed eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="336ca-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="336ca-170">Per eseguire il push di tutti i commit nel server, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="336ca-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="336ca-171">Per distribuire le modifiche alla configurazione del servizio all'istanza del servizio Gestione API</span><span class="sxs-lookup"><span data-stu-id="336ca-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="336ca-172">Dopo il commit e il push delle modifiche locali nel repository del server, è possibile distribuire le modifiche all'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="336ca-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Distribuisci][api-management-configuration-deploy]

<span data-ttu-id="336ca-174">Per informazioni sull'esecuzione di questa operazione tramite l'API REST, vedere la [pagina relativa alla distribuzione delle modifiche al database di configurazione tramite l'API REST](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="336ca-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="336ca-175">Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale</span><span class="sxs-lookup"><span data-stu-id="336ca-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="336ca-176">I file e cartelle nel repository Git locale contengono le informazioni di configurazione dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="336ca-177">Item</span><span class="sxs-lookup"><span data-stu-id="336ca-177">Item</span></span> | <span data-ttu-id="336ca-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="336ca-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="336ca-179">Cartella api-management radice</span><span class="sxs-lookup"><span data-stu-id="336ca-179">root api-management folder</span></span> |<span data-ttu-id="336ca-180">Contiene la configurazione di livello superiore per l'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="336ca-181">Cartella apis</span><span class="sxs-lookup"><span data-stu-id="336ca-181">apis folder</span></span> |<span data-ttu-id="336ca-182">Contiene la configurazione per le API nell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="336ca-183">Cartella groups</span><span class="sxs-lookup"><span data-stu-id="336ca-183">groups folder</span></span> |<span data-ttu-id="336ca-184">Contiene la configurazione per i gruppi nell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="336ca-185">Cartella policies</span><span class="sxs-lookup"><span data-stu-id="336ca-185">policies folder</span></span> |<span data-ttu-id="336ca-186">Contiene i criteri dell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="336ca-187">Cartella portalStyles</span><span class="sxs-lookup"><span data-stu-id="336ca-187">portalStyles folder</span></span> |<span data-ttu-id="336ca-188">Contiene la configurazione delle personalizzazioni del portale per sviluppatori nell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="336ca-189">Cartella products</span><span class="sxs-lookup"><span data-stu-id="336ca-189">products folder</span></span> |<span data-ttu-id="336ca-190">Contiene la configurazione per i prodotti nell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="336ca-191">Cartella templates</span><span class="sxs-lookup"><span data-stu-id="336ca-191">templates folder</span></span> |<span data-ttu-id="336ca-192">Contiene la configurazione per i modelli nell'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="336ca-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="336ca-193">Ogni cartella può contenere uno o più file e in alcuni casi una o più cartelle, ad esempio una cartella per ogni API, prodotto o gruppo.</span><span class="sxs-lookup"><span data-stu-id="336ca-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="336ca-194">I file all'interno di ogni cartella sono specifici per il tipo di entità descritto dal nome della cartella.</span><span class="sxs-lookup"><span data-stu-id="336ca-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="336ca-195">Tipo file</span><span class="sxs-lookup"><span data-stu-id="336ca-195">File type</span></span> | <span data-ttu-id="336ca-196">Scopo</span><span class="sxs-lookup"><span data-stu-id="336ca-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="336ca-197">json</span><span class="sxs-lookup"><span data-stu-id="336ca-197">json</span></span> |<span data-ttu-id="336ca-198">Informazioni di configurazione dell'entità corrispondente</span><span class="sxs-lookup"><span data-stu-id="336ca-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="336ca-199">html</span><span class="sxs-lookup"><span data-stu-id="336ca-199">html</span></span> |<span data-ttu-id="336ca-200">Descrizioni delle entità, spesso visualizzate nel portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="336ca-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="336ca-201">xml</span><span class="sxs-lookup"><span data-stu-id="336ca-201">xml</span></span> |<span data-ttu-id="336ca-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="336ca-202">Policy statements</span></span> |
| <span data-ttu-id="336ca-203">css</span><span class="sxs-lookup"><span data-stu-id="336ca-203">css</span></span> |<span data-ttu-id="336ca-204">Fogli di stile per la personalizzazione del portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="336ca-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="336ca-205">Questi file possono essere creati, eliminati, modificati e gestiti nel file system locale e le modifiche possono essere ridistribuite nell'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="336ca-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="336ca-206">Le entità seguenti non sono contenute nel repository Git e non possono essere configurate tramite Git.</span><span class="sxs-lookup"><span data-stu-id="336ca-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="336ca-207">Utenti</span><span class="sxs-lookup"><span data-stu-id="336ca-207">Users</span></span>
> * <span data-ttu-id="336ca-208">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="336ca-208">Subscriptions</span></span>
> * <span data-ttu-id="336ca-209">Proprietà</span><span class="sxs-lookup"><span data-stu-id="336ca-209">Properties</span></span>
> * <span data-ttu-id="336ca-210">Entità del portale per sviluppatori diverse dagli stili</span><span class="sxs-lookup"><span data-stu-id="336ca-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="336ca-211">Cartella api-management radice</span><span class="sxs-lookup"><span data-stu-id="336ca-211">Root api-management folder</span></span>
<span data-ttu-id="336ca-212">La cartella `api-management` radice contiene un file `configuration.json` che a propria volta contiene informazioni di livello superiore relative all'istanza del servizio nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="336ca-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="336ca-213">Le prime quattro impostazioni (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` e `UserRegistrationTermsConsentRequired`) sono mappate alle impostazioni seguenti della scheda **Identities** (Identità) della sezione **Security** (Sicurezza).</span><span class="sxs-lookup"><span data-stu-id="336ca-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="336ca-214">Impostazione</span><span class="sxs-lookup"><span data-stu-id="336ca-214">Identity setting</span></span> | <span data-ttu-id="336ca-215">Mapping a</span><span class="sxs-lookup"><span data-stu-id="336ca-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="336ca-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="336ca-216">RegistrationEnabled</span></span> |<span data-ttu-id="336ca-217">**Redirect anonymous users to** </span><span class="sxs-lookup"><span data-stu-id="336ca-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="336ca-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="336ca-218">UserRegistrationTerms</span></span> |<span data-ttu-id="336ca-219">**Terms of use on user signup** </span><span class="sxs-lookup"><span data-stu-id="336ca-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="336ca-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="336ca-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="336ca-221">**Show terms of use on signup page** </span><span class="sxs-lookup"><span data-stu-id="336ca-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="336ca-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="336ca-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="336ca-223">**Richiedi consenso** </span><span class="sxs-lookup"><span data-stu-id="336ca-223">**Require consent** checkbox</span></span> |

![Impostazioni di identità][api-management-identity-settings]

<span data-ttu-id="336ca-225">Le quattro impostazioni successive (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` e `DelegationValidationKey`) sono mappate alle impostazioni seguenti della scheda **Delegation** (Delega) della sezione **Security** (Sicurezza).</span><span class="sxs-lookup"><span data-stu-id="336ca-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="336ca-226">Impostazione</span><span class="sxs-lookup"><span data-stu-id="336ca-226">Delegation setting</span></span> | <span data-ttu-id="336ca-227">Mapping a</span><span class="sxs-lookup"><span data-stu-id="336ca-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="336ca-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="336ca-228">DelegationEnabled</span></span> |<span data-ttu-id="336ca-229">Casella di controllo **Delegate sign-in & sign-up** (Delega accesso e iscrizione)</span><span class="sxs-lookup"><span data-stu-id="336ca-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="336ca-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="336ca-230">DelegationUrl</span></span> |<span data-ttu-id="336ca-231">**Delegation endpoint URL** </span><span class="sxs-lookup"><span data-stu-id="336ca-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="336ca-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="336ca-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="336ca-233">**Delegate product subscription** </span><span class="sxs-lookup"><span data-stu-id="336ca-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="336ca-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="336ca-234">DelegationValidationKey</span></span> |<span data-ttu-id="336ca-235">**Delegate Validation Key** </span><span class="sxs-lookup"><span data-stu-id="336ca-235">**Delegate Validation Key** textbox</span></span> |

![Impostazioni di delega][api-management-delegation-settings]

<span data-ttu-id="336ca-237">L'impostazione finale, `$ref-policy`, esegue il mapping al file di istruzioni dei criteri globali per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="336ca-238">Cartella apis</span><span class="sxs-lookup"><span data-stu-id="336ca-238">apis folder</span></span>
<span data-ttu-id="336ca-239">La cartella `apis` contiene, per ogni API nell'istanza del servizio, una cartella contenente a sua volta gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="336ca-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="336ca-240">`apis\<api name>\configuration.json`: configurazione dell'API. Contiene informazioni relative all'URL del servizio back-end e alle operazioni.</span><span class="sxs-lookup"><span data-stu-id="336ca-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="336ca-241">Si tratta delle stesse informazioni che verrebbero restituite se fosse necessario [ottenere un'API specifica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` nel formato `application/json`.</span><span class="sxs-lookup"><span data-stu-id="336ca-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="336ca-242">`apis\<api name>\api.description.html`: descrizione dell'API. Corrisponde alla proprietà `description` dell'[entità relativa all'API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="336ca-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="336ca-243">`apis\<api name>\operations\`: questa cartella contiene i file `<operation name>.description.html` mappati alle operazioni nell'API.</span><span class="sxs-lookup"><span data-stu-id="336ca-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="336ca-244">Ogni file contiene la descrizione di una singola operazione dell'API che esegue il mapping alla proprietà `description` dell' [entità relativa all'operazione](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="336ca-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="336ca-245">Cartella groups</span><span class="sxs-lookup"><span data-stu-id="336ca-245">groups folder</span></span>
<span data-ttu-id="336ca-246">La cartella `groups` contiene una cartella per ogni gruppo definito nell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="336ca-247">`groups\<group name>\configuration.json`: configurazione del gruppo.</span><span class="sxs-lookup"><span data-stu-id="336ca-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="336ca-248">Si tratta delle stesse informazioni che verrebbero restituite se fosse necessario chiamare l'operazione per [ottenere un gruppo specifico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .</span><span class="sxs-lookup"><span data-stu-id="336ca-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="336ca-249">`groups\<group name>\description.html`: descrizione del gruppo. Corrisponde alla proprietà `description` dell'[entità relativa al gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="336ca-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="336ca-250">Cartella policies</span><span class="sxs-lookup"><span data-stu-id="336ca-250">policies folder</span></span>
<span data-ttu-id="336ca-251">La cartella `policies` contiene le istruzioni dei criteri per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="336ca-252">`policies\global.xml` : contiene i criteri definiti in ambito globale per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="336ca-253">`policies\apis\<api name>\`: se sono presenti criteri definiti nell'ambito delle API, tali criteri sono contenuti in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="336ca-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="336ca-254">Cartella `policies\apis\<api name>\<operation name>\`: se sono presenti criteri definiti nell'ambito delle operazioni, tali criteri sono contenuti in questa cartella all'interno dei file `<operation name>.xml` mappati alle istruzioni dei criteri per ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="336ca-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="336ca-255">`policies\products\`: se sono presenti criteri definiti nell'ambito dei prodotti, tali criteri sono contenuti in questa cartella, contenente file `<product name>.xml` mappati alle istruzioni dei criteri per ogni prodotto.</span><span class="sxs-lookup"><span data-stu-id="336ca-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="336ca-256">Cartella portalStyles</span><span class="sxs-lookup"><span data-stu-id="336ca-256">portalStyles folder</span></span>
<span data-ttu-id="336ca-257">La cartella `portalStyles` contiene la configurazione e i fogli di stile delle personalizzazioni del portale per sviluppatori per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="336ca-258">`portalStyles\configuration.json` : contiene i nomi dei fogli di stile usati dal portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="336ca-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="336ca-259">`portalStyles\<style name>.css`: ogni file `<style name>.css` contiene stili per il portale per sviluppatori (per impostazione predefinita, `Preview.css` e `Production.css`).</span><span class="sxs-lookup"><span data-stu-id="336ca-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="336ca-260">Cartella products</span><span class="sxs-lookup"><span data-stu-id="336ca-260">products folder</span></span>
<span data-ttu-id="336ca-261">La cartella `products` contiene una cartella per ogni prodotto definito nell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="336ca-262">`products\<product name>\configuration.json`: configurazione del prodotto.</span><span class="sxs-lookup"><span data-stu-id="336ca-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="336ca-263">Si tratta delle stesse informazioni che verrebbero restituite se fosse necessario chiamare l'operazione per [ottenere un prodotto specifico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .</span><span class="sxs-lookup"><span data-stu-id="336ca-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="336ca-264">`products\<product name>\product.description.html`: descrizione del prodotto. Corrisponde alla proprietà `description` dell'[entità relativa al prodotto](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="336ca-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="336ca-265">Modelli</span><span class="sxs-lookup"><span data-stu-id="336ca-265">templates</span></span>
<span data-ttu-id="336ca-266">La cartella `templates` contiene la configurazione per i [modelli di posta elettronica](api-management-howto-configure-notifications.md) dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="336ca-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="336ca-267">`<template name>\configuration.json` : configurazione del modello di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="336ca-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="336ca-268">`<template name>\body.html` : corpo del modello di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="336ca-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="336ca-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="336ca-269">Next steps</span></span>
<span data-ttu-id="336ca-270">Per informazioni su altri metodi di gestione dell'istanza del servizio, vedere:</span><span class="sxs-lookup"><span data-stu-id="336ca-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="336ca-271">Gestire l'istanza del servizio con i cmdlet di PowerShell seguenti</span><span class="sxs-lookup"><span data-stu-id="336ca-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="336ca-272">Informazioni di riferimento sui cmdlet di PowerShell per la distribuzione dei servizi</span><span class="sxs-lookup"><span data-stu-id="336ca-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="336ca-273">Informazioni di riferimento sui cmdlet di PowerShell per la gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="336ca-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="336ca-274">Gestire l'istanza del servizio nel portale di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="336ca-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="336ca-275">Gestire la prima API</span><span class="sxs-lookup"><span data-stu-id="336ca-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="336ca-276">Gestire l'istanza del servizio tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="336ca-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="336ca-277">Informazioni di riferimento sull'API REST di Gestione API</span><span class="sxs-lookup"><span data-stu-id="336ca-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="336ca-278">Guardare un video introduttivo</span><span class="sxs-lookup"><span data-stu-id="336ca-278">Watch a video overview</span></span>
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




