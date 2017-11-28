---
title: Conversione di WordPress in un multisito in Servizio app di Azure
description: Informazioni su come accedere a un'app Web WordPress esistente creata tramite la raccolta in Azure e convertirla in un multisito WordPress"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="e074b-103">Conversione di WordPress in un multisito in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e074b-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="e074b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e074b-104">Overview</span></span>
<span data-ttu-id="e074b-105">*Autore: [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="e074b-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="e074b-106">In questa esercitazione si apprenderà come accedere a un'app Web WordPress esistente creata tramite la raccolta in Azure e convertirla in un'installazione multisito WordPress.</span><span class="sxs-lookup"><span data-stu-id="e074b-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="e074b-107">Si apprenderà inoltre come assegnare un dominio personalizzato a ogni sito secondario all'interno dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="e074b-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="e074b-108">Si presuppone che sia già disponibile un'installazione esistente di WordPress.</span><span class="sxs-lookup"><span data-stu-id="e074b-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="e074b-109">In caso contrario, attenersi alle indicazioni fornite in [Creare un sito Web WordPress dalla raccolta in Azure][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="e074b-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="e074b-110">La conversione di un'installazione per singolo sito WordPress esistente in un multisito è in genere un'operazione abbastanza semplice. Alcuni dei passaggi iniziali sono in pratica identici a quelli della pagina [Create A Network][wordpress-codex-create-a-network] (Creare una rete) in [WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="e074b-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="e074b-111">Di seguito sono riportati i requisiti iniziali.</span><span class="sxs-lookup"><span data-stu-id="e074b-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="e074b-112">Abilitare il multisito</span><span class="sxs-lookup"><span data-stu-id="e074b-112">Allow Multisite</span></span>
<span data-ttu-id="e074b-113">È necessario prima abilitare il multisito tramite il file `wp-config.php` con la costante **WP\_ALLOW\_MULTISITE**.</span><span class="sxs-lookup"><span data-stu-id="e074b-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="e074b-114">Per modificare i file dell'app Web sono disponibili due metodi: il primo tramite FTP, il secondo tramite Git.</span><span class="sxs-lookup"><span data-stu-id="e074b-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="e074b-115">Se non si è esperti di configurazione tramite FTP o Git, fare riferimento alle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e074b-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="e074b-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup] (Sito Web PHP con MySQL e FTP)</span><span class="sxs-lookup"><span data-stu-id="e074b-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="e074b-117">[Sito Web PHP con MySQL e Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="e074b-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="e074b-118">Aprire il file `wp-config.php` con l'editor preferito e aggiungere quanto segue sopra la riga `/* That's all, stop editing! Happy blogging. */`.</span><span class="sxs-lookup"><span data-stu-id="e074b-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="e074b-119">Salvare il file e caricarlo di nuovo nel server.</span><span class="sxs-lookup"><span data-stu-id="e074b-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="e074b-120">Configurazione della rete</span><span class="sxs-lookup"><span data-stu-id="e074b-120">Network Setup</span></span>
<span data-ttu-id="e074b-121">Accedere all'area *wp-admin* del sito Web. Si noterà un nuovo elemento **Configurazione di rete** nel menu **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="e074b-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="e074b-122">Fare clic su **Configurazione di rete** e inserire i dettagli relativi alla rete.</span><span class="sxs-lookup"><span data-stu-id="e074b-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Schermata di configurazione della rete][wordpress-network-setup]

<span data-ttu-id="e074b-124">In questa esercitazione viene usato lo schema di sito *Sub-directories* che dovrebbe essere sempre funzionante. I domini personalizzati per ogni sito secondario verranno configurati più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e074b-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="e074b-125">Dovrebbe tuttavia essere possibile configurare un'installazione di sottodominio se si mappa un dominio tramite il [Portale di Azure](https://portal.azure.com) e si configura correttamente il DNS con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="e074b-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="e074b-126">Per altre informazioni sulla differenza tra le configurazioni di sottodomini e sottodirectory, vedere l'articolo [Types of multisite network][wordpress-codex-types-of-networks] (Tipi di rete multisito) in WordPress Codex.</span><span class="sxs-lookup"><span data-stu-id="e074b-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="e074b-127">Abilitare la rete</span><span class="sxs-lookup"><span data-stu-id="e074b-127">Enable the Network</span></span>
<span data-ttu-id="e074b-128">La rete è stata configurata nel database, ma per abilitare la funzionalità di rete è necessario eseguire un ulteriore passaggio.</span><span class="sxs-lookup"><span data-stu-id="e074b-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="e074b-129">Finalizzare le impostazioni di `wp-config.php` e verificare che `web.config` reindirizzi in modo corretto ciascun sito.</span><span class="sxs-lookup"><span data-stu-id="e074b-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="e074b-130">Dopo aver fatto clic sul pulsante **Installa** nella pagina *Configurazione della rete*, WordPress proverà ad aggiornare i file `wp-config.php` e `web.config`.</span><span class="sxs-lookup"><span data-stu-id="e074b-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="e074b-131">È tuttavia consigliabile controllare sempre i file per verificare la riuscita degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="e074b-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="e074b-132">In caso contrario, in questa schermata verranno visualizzati gli aggiornamenti necessari.</span><span class="sxs-lookup"><span data-stu-id="e074b-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="e074b-133">Modificare e salvare i file.</span><span class="sxs-lookup"><span data-stu-id="e074b-133">Edit and save the files.</span></span>

<span data-ttu-id="e074b-134">Dopo aver effettuato gli aggiornamenti, sarà necessario disconnettersi e riconnettersi al dashboard wp-admin.</span><span class="sxs-lookup"><span data-stu-id="e074b-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="e074b-135">Sulla barra di amministrazione dovrebbe ora essere presente un ulteriore menu denominato **My Sites**.</span><span class="sxs-lookup"><span data-stu-id="e074b-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="e074b-136">Tale menu consente di controllare la nuova rete tramite il dashboard **Network Admin** .</span><span class="sxs-lookup"><span data-stu-id="e074b-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="e074b-137">Aggiunta di domini personalizzati</span><span class="sxs-lookup"><span data-stu-id="e074b-137">Adding custom domains</span></span>
<span data-ttu-id="e074b-138">Con il plug-in [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] è semplicissimo aggiungere domini personalizzati a qualsiasi sito della rete.</span><span class="sxs-lookup"><span data-stu-id="e074b-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="e074b-139">Per il corretto funzionamento del plug-in è necessario eseguire alcune operazioni aggiuntive di configurazione sul portale, nonché presso il registrar.</span><span class="sxs-lookup"><span data-stu-id="e074b-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="e074b-140">Abilitare il mapping di dominio all'app Web</span><span class="sxs-lookup"><span data-stu-id="e074b-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="e074b-141">Con il plug-in **gratuito** [Servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) non supporta l'aggiunta di domini ad App Web.</span><span class="sxs-lookup"><span data-stu-id="e074b-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="e074b-142">È quindi necessario passare alla modalità **condivisa** o **standard**.</span><span class="sxs-lookup"><span data-stu-id="e074b-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="e074b-143">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e074b-143">To do this:</span></span>

* <span data-ttu-id="e074b-144">Accedere al portale di Azure e individuare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="e074b-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="e074b-145">Fare clic sulla scheda **Scala verticalmente** in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="e074b-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="e074b-146">In **Generale** selezionare *CONDIVISO* o *STANDARD*</span><span class="sxs-lookup"><span data-stu-id="e074b-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="e074b-147">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="e074b-147">Click **Save**</span></span>

<span data-ttu-id="e074b-148">È possibile che venga ricevuto un messaggio in cui si chiede di verificare la modifica e di accettare che, a seconda dell'utilizzo e delle altre opzioni di configurazione impostate, l'app Web possa comportare costi.</span><span class="sxs-lookup"><span data-stu-id="e074b-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="e074b-149">L'elaborazione delle nuove impostazioni richiede alcuni secondi, pertanto è consigliabile iniziare subito a configurare il dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="e074b-150">Verifica del dominio</span><span class="sxs-lookup"><span data-stu-id="e074b-150">Verify your domain</span></span>
<span data-ttu-id="e074b-151">Prima che App Web di Azure consentano di mappare un dominio al sito, è necessario verificare di disporre dell'autorizzazione per il mapping del dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="e074b-152">A tale scopo, è necessario aggiungere un nuovo record CNAME alla voce DNS.</span><span class="sxs-lookup"><span data-stu-id="e074b-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="e074b-153">Accedere al gestore DNS del dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="e074b-154">Creare un nuovo CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="e074b-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="e074b-155">Impostare *awverify* in modo che punti a *awverify.DOMINIO.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="e074b-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="e074b-156">L'applicazione delle modifiche DNS può richiedere tempo, pertanto se i passaggi seguenti non funzionano immediatamente, attendere qualche minuto prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="e074b-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="e074b-157">Aggiungere il dominio all'app Web</span><span class="sxs-lookup"><span data-stu-id="e074b-157">Add the domain to the web app</span></span>
<span data-ttu-id="e074b-158">Tornare all'app Web tramite il Portale Azure e fare clic su **Impostazioni**, quindi su**Domini personalizzati e SSL**.</span><span class="sxs-lookup"><span data-stu-id="e074b-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="e074b-159">Quando vengono visualizzate le *impostazioni SSL* , appariranno campi in cui immettere tutti i domini a cui si desidera assegnare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="e074b-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="e074b-160">Se un dominio non è incluso nell'elenco, non sarà disponibile per il mapping in WordPress, indipendentemente dalla modalità di configurazione del DNS del dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Finestra di dialogo Manage custom domains][wordpress-manage-domains]

<span data-ttu-id="e074b-162">Dopo aver digitato il dominio nella casella di testo, Azure verificherà il record CNAME creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e074b-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="e074b-163">Se il DNS non è stato completamente propagato, verrà visualizzato un indicatore rosso.</span><span class="sxs-lookup"><span data-stu-id="e074b-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="e074b-164">Se invece l'operazione è riuscita, verrà visualizzato un segno di spunta verde.</span><span class="sxs-lookup"><span data-stu-id="e074b-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="e074b-165">Prendere nota dell'indirizzo IP indicato nella parte inferiore della finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="e074b-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="e074b-166">in quanto sarà necessario per configurare il record A per il dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="e074b-167">Configurare il record A del dominio</span><span class="sxs-lookup"><span data-stu-id="e074b-167">Setup the domain A record</span></span>
<span data-ttu-id="e074b-168">Se gli altri passaggi sono stati completati correttamente, è possibile assegnare il dominio all'app Web di Azure tramite un record A DNS.</span><span class="sxs-lookup"><span data-stu-id="e074b-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="e074b-169">È importante notare che in App Web di Azure vengono accettati sia record CNAME che A, tuttavia è *necessario* utilizzare un record A per abilitare il mapping del dominio corretto.</span><span class="sxs-lookup"><span data-stu-id="e074b-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="e074b-170">Un CNAME non può essere inoltrato a un altro CNAME, ovvero a quello creato da Azure con DOMINIO.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="e074b-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="e074b-171">Se si utilizza l'indirizzo IP del passaggio precedente, tornare al gestore DNS e configurare il record A in modo che punti a tale IP.</span><span class="sxs-lookup"><span data-stu-id="e074b-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="e074b-172">Installare e configurare il plug-in</span><span class="sxs-lookup"><span data-stu-id="e074b-172">Install and setup the plugin</span></span>
<span data-ttu-id="e074b-173">La modalità multisito di WordPress non include al momento un metodo incorporato per mappare i domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e074b-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="e074b-174">Esiste tuttavia un plug-in denominato [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] che consente di aggiungere tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e074b-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="e074b-175">Accedere alla parte Network Admin del sito e installare il plug-in **WordPress MU Domain Mapping** .</span><span class="sxs-lookup"><span data-stu-id="e074b-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="e074b-176">Dopo aver installato e attivato il plug-in, fare clic su **Impostazioni** > **Domain Mapping** per configurarlo.</span><span class="sxs-lookup"><span data-stu-id="e074b-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="e074b-177">Nella prima casella di testo *Server IP Address*immettere l'indirizzo IP utilizzato per configurare il record A per il dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="e074b-178">Impostare le eventuali *opzioni di dominio* desiderate (anche se le impostazioni predefinite sono spesso adeguate), quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e074b-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="e074b-179">Mappare il dominio</span><span class="sxs-lookup"><span data-stu-id="e074b-179">Map the domain</span></span>
<span data-ttu-id="e074b-180">Visualizzare il **Dashboard** relativo al sito a cui mappare il dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="e074b-181">Fare clic su **Tools** > **Domain Mapping** e digitare il nuovo dominio nella casella di testo, quindi fare clic su **Add**.</span><span class="sxs-lookup"><span data-stu-id="e074b-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="e074b-182">Per impostazione predefinita, il nuovo dominio verrà riscritto nel dominio del sito generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e074b-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="e074b-183">Se si desidera che tutto il traffico venga inviato al nuovo dominio, selezionare la casella *Primary domain for this blog* prima di salvare.</span><span class="sxs-lookup"><span data-stu-id="e074b-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="e074b-184">È possibile aggiungere a un sito un numero illimitato di domini, tuttavia solo uno può essere quello primario.</span><span class="sxs-lookup"><span data-stu-id="e074b-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="e074b-185">Ripetere l'operazione</span><span class="sxs-lookup"><span data-stu-id="e074b-185">Do it again</span></span>
<span data-ttu-id="e074b-186">App Web di Azure consente di aggiungere un numero illimitato di domini a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="e074b-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="e074b-187">Per aggiungere altri domini, sarà necessario eseguire per ciascun dominio le operazioni descritte nelle sezioni **Verificare il dominio** e **Configurare il record A** del dominio.</span><span class="sxs-lookup"><span data-stu-id="e074b-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="e074b-188">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="e074b-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e074b-189">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="e074b-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e074b-190">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="e074b-190">What's changed</span></span>
* <span data-ttu-id="e074b-191">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e074b-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


