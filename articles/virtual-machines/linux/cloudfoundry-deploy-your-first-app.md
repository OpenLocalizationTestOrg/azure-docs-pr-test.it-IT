---
title: Distribuire la prima app a Cloud Foundry in Microsoft Azure | Microsoft Docs
description: Distribuire un'applicazione a Cloud Foundry in Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="21116-103">Distribuire la prima app a Cloud Foundry in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="21116-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="21116-104">[Cloud Foundry](http://cloudfoundry.org) è una popolare piattaforma di applicazioni open source disponibile in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="21116-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="21116-105">In questo articolo viene illustrato come distribuire e gestire un'applicazione in Cloud Foundry in un ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="21116-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="21116-106">Creare un ambiente Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="21116-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="21116-107">Esistono diverse opzioni per la creazione di un ambiente Cloud Foundry in Azure:</span><span class="sxs-lookup"><span data-stu-id="21116-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="21116-108">Usare l'[offerta Pivotal Cloud Foundry][pcf-azuremarketplace] in Azure Marketplace per creare un ambiente standard che include PCF Operations Manager e il Service Broker di Azure.</span><span class="sxs-lookup"><span data-stu-id="21116-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="21116-109">Per le [istruzioni complete][pcf-azuremarketplace-pivotaldocs] per la distribuzione dell'offerta del marketplace, vedere la documentazione di Pivotal.</span><span class="sxs-lookup"><span data-stu-id="21116-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="21116-110">Creare un ambiente personalizzato [distribuendo manualmente Pivotal Cloud Foundry][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="21116-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="21116-111">[Distribuire i pacchetti open source di Cloud Foundry direttamente][oss-cf-bosh] impostando un [BOSH](http://bosh.io) director, una macchina virtuale che coordina la distribuzione dell'ambiente Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="21116-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="21116-112">Se si distribuisce PCF da Azure Marketplace, annotare il SYSTEMDOMAINURL e le credenziali amministratore necessarie per accedere al gestore di app di Pivotal, entrambi descritti nella Guida alla distribuzione dal marketplace.</span><span class="sxs-lookup"><span data-stu-id="21116-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="21116-113">Questi elementi sono necessari per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="21116-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="21116-114">Per le distribuzioni dal marketplace, il SYSTEMDOMAINURL è nel formato https://system.*indirizzo-ip*.cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="21116-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="21116-115">Connettersi al controller del cloud</span><span class="sxs-lookup"><span data-stu-id="21116-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="21116-116">Il controller del cloud è il punto di ingresso principale in un ambiente Cloud Foundry per la distribuzione e la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="21116-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="21116-117">L'API del controller del cloud di base (CCAPI) è un'API REST, ma è accessibile attraverso vari strumenti.</span><span class="sxs-lookup"><span data-stu-id="21116-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="21116-118">In questo caso, si interagisce con essa tramite l'[interfaccia della riga di comando di Cloud Foundry][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="21116-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="21116-119">L'interfaccia della riga di comando può essere installata su Linux, MacOS o Windows, ma se si preferisce non installarla è disponibile preinstallata in [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="21116-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="21116-120">Per eseguire l'accesso, anteporre `api` al SYSTEMDOMAINURL ottenuto dalla distribuzione dal marketplace.</span><span class="sxs-lookup"><span data-stu-id="21116-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="21116-121">Poiché la distribuzione predefinita usa un certificato autofirmato, è necessario includere anche l'istruzione `skip-ssl-validation`.</span><span class="sxs-lookup"><span data-stu-id="21116-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="21116-122">Viene chiesto di accedere al controller del cloud.</span><span class="sxs-lookup"><span data-stu-id="21116-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="21116-123">Usare le credenziali dell'account amministratore acquisite dalle fasi di distribuzione del marketplace.</span><span class="sxs-lookup"><span data-stu-id="21116-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="21116-124">Cloud Foundry offre *organizzazioni* e *spazi* come spazi dei nomi per isolare i team e gli ambienti all'interno di una distribuzione condivisa.</span><span class="sxs-lookup"><span data-stu-id="21116-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="21116-125">La distribuzione dal marketplace PCF include l'organizzazione *sistema* predefinita e un set di spazi creato per contenere i componenti di base, come il servizio di scalabilità automatica e il Service Broker di Azure.</span><span class="sxs-lookup"><span data-stu-id="21116-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="21116-126">Per il momento, scegliere lo spazio *sistema*.</span><span class="sxs-lookup"><span data-stu-id="21116-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="21116-127">Creare un'organizzazione e uno spazio</span><span class="sxs-lookup"><span data-stu-id="21116-127">Create an org and space</span></span>

<span data-ttu-id="21116-128">Se si digita `cf apps`, viene visualizzato un set di applicazioni di sistema che sono state distribuite nello spazio di sistema all'interno dell'organizzazione sistema.</span><span class="sxs-lookup"><span data-stu-id="21116-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="21116-129">È consigliabile mantenere l'organizzazione *sistema* riservata per le applicazioni di sistema, pertanto creare un'organizzazione e uno spazio per ospitare l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="21116-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="21116-130">Usare il comando di destinazione per passare alla nuova organizzazione e al nuovo spazio:</span><span class="sxs-lookup"><span data-stu-id="21116-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="21116-131">A questo punto, quando si distribuisce un'applicazione essa viene automaticamente creata nella nuova organizzazione e nel nuovo spazio.</span><span class="sxs-lookup"><span data-stu-id="21116-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="21116-132">Per confermare che non sono attualmente presenti app nella nuova organizzazione/spazio, digitare nuovamente `cf apps`.</span><span class="sxs-lookup"><span data-stu-id="21116-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="21116-133">Per altre informazioni sulle organizzazioni e gli spazi e su come possono essere usati per il controllo degli accessi in base al ruolo, vedere la [documentazione di Cloud Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="21116-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="21116-134">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="21116-134">Deploy an application</span></span>

<span data-ttu-id="21116-135">Usiamo un'applicazione Cloud Foundry di esempio chiamata Hello Spring Cloud, che viene scritta in Java ed è basata sul [framework Spring](http://spring.io) e su [Spring Boot](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="21116-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="21116-136">Clonare il repository Hello Spring Cloud</span><span class="sxs-lookup"><span data-stu-id="21116-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="21116-137">L'applicazione di esempio Hello Spring Cloud è disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="21116-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="21116-138">Clonarla nel proprio ambiente e modificarla nella nuova directory:</span><span class="sxs-lookup"><span data-stu-id="21116-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="21116-139">Compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21116-139">Build the application</span></span>

<span data-ttu-id="21116-140">Compilare l'app mediante [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="21116-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="21116-141">Distribuire l'applicazione con cf push</span><span class="sxs-lookup"><span data-stu-id="21116-141">Deploy the application with cf push</span></span>

<span data-ttu-id="21116-142">È possibile distribuire la maggior parte delle applicazioni per Cloud Foundry tramite il comando `push`:</span><span class="sxs-lookup"><span data-stu-id="21116-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="21116-143">Quando si *effettua il push* di un'applicazione, Cloud Foundry rileva il tipo di applicazione (in questo caso, un'app Java) e identifica le relative dipendenze (in questo caso, il framework Spring).</span><span class="sxs-lookup"><span data-stu-id="21116-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="21116-144">Inserisce quindi in un pacchetto tutti gli elementi necessari per eseguire il codice in un'immagine del contenitore autonoma, denominata *droplet*.</span><span class="sxs-lookup"><span data-stu-id="21116-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="21116-145">Infine, Cloud Foundry pianifica l'applicazione in uno dei computer disponibili nell'ambiente e crea un URL in cui è possibile raggiungerla, disponibile nell'output del comando.</span><span class="sxs-lookup"><span data-stu-id="21116-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![Output del comando push cf][cf-push-output]

<span data-ttu-id="21116-147">Per visualizzare l'applicazione hello-spring-cloud, aprire l'URL specificato nel browser:</span><span class="sxs-lookup"><span data-stu-id="21116-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Interfaccia utente predefinita per Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="21116-149">Per altre informazioni su cosa accade durante `cf push`, vedere [How Applications Are Staged][cf-push-docs] (Come vengono gestite temporaneamente le applicazioni) nella documentazione di Cloud Foundry.</span><span class="sxs-lookup"><span data-stu-id="21116-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="21116-150">Visualizzare i registri applicazioni</span><span class="sxs-lookup"><span data-stu-id="21116-150">View application logs</span></span>

<span data-ttu-id="21116-151">Per visualizzare i registri di un'applicazione in base al nome, è possibile usare l'interfaccia della riga di comando di Cloud Foundry:</span><span class="sxs-lookup"><span data-stu-id="21116-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="21116-152">Per impostazione predefinita, il comando registri usa *tail*, che visualizza i nuovi registri man mano che vengono scritti.</span><span class="sxs-lookup"><span data-stu-id="21116-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="21116-153">Per visualizzare i nuovi registri, aggiornare l'applicazione hello-spring-cloud nel browser.</span><span class="sxs-lookup"><span data-stu-id="21116-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="21116-154">Per visualizzare i log che sono già stati scritti, aggiungere l'istruzione `recent`:</span><span class="sxs-lookup"><span data-stu-id="21116-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="21116-155">Scalare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="21116-155">Scale the application</span></span>

<span data-ttu-id="21116-156">Per impostazione predefinita, `cf push` crea solo una singola istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21116-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="21116-157">Per garantire la disponibilità elevata e consentire la scalabilità orizzontale per una velocità effettiva superiore, in genere è consigliabile eseguire più istanze delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="21116-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="21116-158">È possibile scalare orizzontalmente le applicazioni già distribuite tramite il comando `scale`:</span><span class="sxs-lookup"><span data-stu-id="21116-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="21116-159">L'esecuzione del comando `cf app` nell'applicazione indica che Cloud Foundry sta creando un'altra istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21116-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="21116-160">Dopo che l'applicazione è stata avviata, Cloud Foundry avvia automaticamente il bilanciamento del carico del traffico.</span><span class="sxs-lookup"><span data-stu-id="21116-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="21116-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21116-161">Next steps</span></span>

- <span data-ttu-id="21116-162">[Leggere la documentazione di Cloud Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="21116-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="21116-163">[Configurare il plug-in Visual Studio Team Services per Cloud Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="21116-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="21116-164">[Configurare il nozzle di Microsoft Log Analytics per Cloud Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="21116-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png