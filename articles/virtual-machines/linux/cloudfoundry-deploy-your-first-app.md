---
title: aaaDeploy il primo tooCloud app Foundry in Microsoft Azure | Documenti Microsoft
description: Distribuire un tooCloud applicazione Foundry in Azure
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
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="d8f1c-103">Distribuire il primo tooCloud app Foundry in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d8f1c-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="d8f1c-104">[Cloud Foundry](http://cloudfoundry.org) è una popolare piattaforma di applicazioni open source disponibile in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="d8f1c-105">In questo articolo viene illustrata la modalità toodeploy e gestire un'applicazione in Cloud Foundry in un ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="d8f1c-106">Creare un ambiente Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="d8f1c-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="d8f1c-107">Esistono diverse opzioni per la creazione di un ambiente Cloud Foundry in Azure:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="d8f1c-108">Hello utilizzare [offerta Foundry Cloud fondamentale] [ pcf-azuremarketplace] in hello Azure Marketplace toocreate un ambiente standard che include PCF Operations Manager e hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="d8f1c-109">È possibile trovare [le istruzioni per] [ pcf-azuremarketplace-pivotaldocs] offrire hello documentazione fondamentale per la distribuzione di marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="d8f1c-110">Creare un ambiente personalizzato [distribuendo manualmente Pivotal Cloud Foundry][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="d8f1c-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="d8f1c-111">[Distribuire i pacchetti di hello open-source Foundry Cloud direttamente] [ oss-cf-bosh] impostando un [BOSH](http://bosh.io) director, una macchina virtuale che coordina distribuzione hello dell'ambiente Cloud Foundry hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d8f1c-112">Se si distribuisce PCF hello Azure Marketplace, prendere nota di hello SYSTEMDOMAINURL e richieste di credenziali di amministratore hello tooaccess hello fondamentale Manager di App, di cui sono descritti nella Guida alla distribuzione di hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="d8f1c-113">Essi è toocomplete necessari in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="d8f1c-114">Per le distribuzioni di marketplace, hello SYSTEMDOMAINURL è https://system modulo hello. *indirizzo ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="d8f1c-115">Connettersi toohello Controller del Cloud</span><span class="sxs-lookup"><span data-stu-id="d8f1c-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="d8f1c-116">Hello Controller del Cloud è l'ambiente di Cloud Foundry tooa punto di ingresso principale hello per la distribuzione e la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="d8f1c-117">core Hello Cloud Controller API (CCAPI) è un'API REST, ma è accessibile attraverso vari strumenti.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="d8f1c-118">In questo caso, si interagire con esso tramite hello [Cloud Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="d8f1c-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="d8f1c-119">È possibile installare hello CLI su Linux, MacOS o Windows, ma se si preferisce non tooinstall affatto, è disponibile preinstallato in hello [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="d8f1c-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="d8f1c-120">toolog, anteporre `api` toohello SYSTEMDOMAINURL ottenuti dalla distribuzione marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="d8f1c-121">Poiché la distribuzione di hello predefinito utilizza un certificato autofirmato, è necessario includere anche hello `skip-ssl-validation` passare.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="d8f1c-122">Si è richiesta toolog in toohello Controller del Cloud.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="d8f1c-123">Utilizzare le credenziali dell'account amministratore hello acquisito dalle fasi di distribuzione di hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="d8f1c-124">Cloud Foundry fornisce *organizzazioni* e *spazi* come team hello tooisolate di spazi dei nomi e gli ambienti in una distribuzione condivisa.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="d8f1c-125">distribuzione di marketplace PCF Hello include predefinito hello *sistema* dell'organizzazione e un set di spazi creato toocontain i componenti di base hello, ad esempio servizio di scalabilità automatica hello e hello Azure service broker.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="d8f1c-126">Per il momento, scegliere hello *sistema* spazio.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="d8f1c-127">Creare un'organizzazione e uno spazio</span><span class="sxs-lookup"><span data-stu-id="d8f1c-127">Create an org and space</span></span>

<span data-ttu-id="d8f1c-128">Se si digita `cf apps`, viene visualizzato un set di applicazioni di sistema che sono state distribuite nello spazio di sistema hello all'interno dell'organizzazione sistema hello</span><span class="sxs-lookup"><span data-stu-id="d8f1c-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="d8f1c-129">È consigliabile mantenere hello *sistema* org riservato per le applicazioni di sistema, quindi creare un toohouse org e spazio l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="d8f1c-130">Utilizzare hello destinazione comando tooswitch toohello nuova organizzazione e lo spazio:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="d8f1c-131">A questo punto, quando si distribuisce un'applicazione, viene automaticamente creato nello spazio e hello nuova organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="d8f1c-132">tooconfirm che sono attualmente alcuna App nello spazio/hello nuova organizzazione, non tipo `cf apps` nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="d8f1c-133">Per ulteriori informazioni sulle organizzazioni e gli spazi e come possono essere utilizzati per il controllo di accesso basato sui ruoli (RBAC), vedere hello [documentazione Foundry Cloud][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="d8f1c-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="d8f1c-134">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="d8f1c-134">Deploy an application</span></span>

<span data-ttu-id="d8f1c-135">Consente di usare un'applicazione di esempio Foundry Cloud chiamata Hello Spring Cloud, che viene scritto in linguaggio e in base a hello [Spring Framework](http://spring.io) e [avvio Spring](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="d8f1c-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="d8f1c-136">Clonare il repository di hello Hello Spring Cloud</span><span class="sxs-lookup"><span data-stu-id="d8f1c-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="d8f1c-137">applicazione di esempio Hello Spring Cloud Hello è disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="d8f1c-138">Clonarla ambiente tooyour e modificare nella nuova directory hello:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="d8f1c-139">Compilare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="d8f1c-139">Build hello application</span></span>

<span data-ttu-id="d8f1c-140">Compilazione hello app usando [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="d8f1c-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="d8f1c-141">Distribuire un'applicazione hello con cf push</span><span class="sxs-lookup"><span data-stu-id="d8f1c-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="d8f1c-142">È possibile distribuire la maggior parte delle applicazioni tooCloud Foundry utilizzando hello `push` comando:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="d8f1c-143">Quando si *push* un'applicazione, Cloud Foundry rileva hello tipo di applicazione (in questo caso, un'app Java) e identifica le relative dipendenze (in questo caso, framework di primavera hello).</span><span class="sxs-lookup"><span data-stu-id="d8f1c-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="d8f1c-144">Viene quindi inserito tutto il necessario toorun il codice in un'immagine contenitore autonomo, nota come un *droplet*.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="d8f1c-145">Infine, le pianificazioni di Cloud Foundry hello applicazione su uno dei computer disponibili di hello nell'ambiente in uso e crea un URL in cui è possibile raggiungerli, disponibile nell'output di hello del comando hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Output del comando push cf][cf-push-output]

<span data-ttu-id="d8f1c-147">applicazione hello-spring-cloud hello toosee, aprire hello fornito URL nel browser:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Interfaccia utente predefinita per Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="d8f1c-149">ulteriori informazioni su cosa accade durante toolearn `cf push`, vedere [installazione delle applicazioni] [ cf-push-docs] in hello documentazione Foundry Cloud.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="d8f1c-150">Visualizzare i registri applicazioni</span><span class="sxs-lookup"><span data-stu-id="d8f1c-150">View application logs</span></span>

<span data-ttu-id="d8f1c-151">È possibile utilizzare i log di hello Cloud Foundry CLI tooview per un'applicazione in base al nome:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="d8f1c-152">Per impostazione predefinita, hello Registra comando Usa *della parte finale del*, che mostra i nuovi log man mano che vengono scritte.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="d8f1c-153">toosee nuovi log visualizzati, aggiornare l'applicazione hello-spring-cloud hello nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="d8f1c-154">registri tooview che sono già stati scritti, aggiungere hello `recent` passare:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="d8f1c-155">Applicazione hello scala</span><span class="sxs-lookup"><span data-stu-id="d8f1c-155">Scale hello application</span></span>

<span data-ttu-id="d8f1c-156">Per impostazione predefinita, `cf push` crea solo una singola istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="d8f1c-157">tooensure la disponibilità elevata e scalabilità attiva per una velocità effettiva, in genere si desidera toorun più istanze delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="d8f1c-158">È possibile ridimensionare le applicazioni già distribuite utilizzando hello `scale` comando:</span><span class="sxs-lookup"><span data-stu-id="d8f1c-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="d8f1c-159">In esecuzione hello `cf app` comando in un'applicazione hello mostra che il Cloud è la creazione di un'altra istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="d8f1c-160">Una volta avviata, un'applicazione hello Foundry Cloud avvia automaticamente il bilanciamento del carico del traffico tooit.</span><span class="sxs-lookup"><span data-stu-id="d8f1c-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d8f1c-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8f1c-161">Next steps</span></span>

- <span data-ttu-id="d8f1c-162">[Hello lettura documentazione Cloud Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="d8f1c-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="d8f1c-163">[Impostare i plug-in Visual Studio Team Services hello per Cloud Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="d8f1c-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="d8f1c-164">[Configurare hello prolunga Analitica Log di Microsoft per il Cloud][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="d8f1c-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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