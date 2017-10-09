---
title: App del servizio Web App in domande frequenti su Linux aaaAzure | Documenti Microsoft
description: Domande frequenti su App Web del Servizio app di Azure su Linux.
keywords: Servizio app di Azure, app Web, domande frequenti, Linux, OSS
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="2d245-104">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="2d245-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="2d245-105">Con la versione di hello dell'App Web in Linux, si sta lavorando aggiunta di funzionalità e apportando piattaforma tooour miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="2d245-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="2d245-106">Di seguito sono alcune domande frequenti (FAQ) che i clienti hanno richiesto ci su hello ultima mesi.</span><span class="sxs-lookup"><span data-stu-id="2d245-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="2d245-107">Se si dispone di una domanda, un commento per l'articolo hello ed è possibile rispondere appena possibile.</span><span class="sxs-lookup"><span data-stu-id="2d245-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="2d245-108">Immagini predefinite</span><span class="sxs-lookup"><span data-stu-id="2d245-108">Built-in images</span></span>

<span data-ttu-id="2d245-109">**Q:** voglio toofork hello Docker contenitori predefiniti che hello piattaforma fornisce.</span><span class="sxs-lookup"><span data-stu-id="2d245-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="2d245-110">Dove si trovano questi file?</span><span class="sxs-lookup"><span data-stu-id="2d245-110">Where can I find those files?</span></span>

<span data-ttu-id="2d245-111">**R:** È possibile trovare tutti i file Docker su [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="2d245-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="2d245-112">È possibile trovare tutti i contenitori Docker nell'[hub Docker](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="2d245-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="2d245-113">**Q:** quali sono i valori previsti hello per hello sezione del File di avvio quando si configura stack di runtime hello?</span><span class="sxs-lookup"><span data-stu-id="2d245-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="2d245-114">**R:** per Node.Js, specificare il file di configurazione di hello PM2 o il file di script.</span><span class="sxs-lookup"><span data-stu-id="2d245-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="2d245-115">Per .NET Core specificare il nome del file DLL compilato.</span><span class="sxs-lookup"><span data-stu-id="2d245-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="2d245-116">Per Ruby, è possibile specificare hello Ruby script che si desidera tooinitialize dell'app con.</span><span class="sxs-lookup"><span data-stu-id="2d245-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="2d245-117">gestione</span><span class="sxs-lookup"><span data-stu-id="2d245-117">Management</span></span>

<span data-ttu-id="2d245-118">**Q:** cosa accade quando viene premuto il pulsante di riavvio hello nel portale di Azure hello?</span><span class="sxs-lookup"><span data-stu-id="2d245-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="2d245-119">**R:** questo è hello equivalente del riavvio di Docker.</span><span class="sxs-lookup"><span data-stu-id="2d245-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="2d245-120">**Q:** è possibile utilizzare Secure Shell (SSH) tooconnect toohello app contenitore macchina virtuale (VM)?</span><span class="sxs-lookup"><span data-stu-id="2d245-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="2d245-121">**R:** Sì, è possibile eseguire tramite il sito di Gestione controllo servizi hello, seguente hello controllo articolo per altre informazioni [supporto SSH per l'App Web in Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="2d245-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="2d245-122">**Q:** voglio toocreate un piano di Linux App Service tramite SDK o un modello ARM, come è possibile ottenere questo?</span><span class="sxs-lookup"><span data-stu-id="2d245-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="2d245-123">**R:** occorre hello tooset `reserved` campo di applicazione hello service troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="2d245-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="2d245-124">Integrazione/distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="2d245-124">Continuous integration/deployment</span></span>

<span data-ttu-id="2d245-125">**Q:** dell'applicazione web utilizza ancora un'immagine contenitore Docker precedente dopo che è già stato aggiornato immagine hello nell'Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="2d245-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="2d245-126">È supportata l'integrazione/distribuzione continua di contenitori personalizzati?</span><span class="sxs-lookup"><span data-stu-id="2d245-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="2d245-127">**R:** tooset integrazione/distribuzione continua per le immagini del Registro di sistema di Azure contenitore o DockerHub dal controllo hello articolo seguente [distribuzione continua con l'App Web di Azure in Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="2d245-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="2d245-128">Per i registri privati, è possibile aggiornare il contenitore di hello arrestando e riavviando quindi l'app web.</span><span class="sxs-lookup"><span data-stu-id="2d245-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="2d245-129">Oppure è possibile modificare o aggiungere un'applicazione fittizia impostazione tooforce un aggiornamento del contenitore.</span><span class="sxs-lookup"><span data-stu-id="2d245-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="2d245-130">**D:** Gli ambienti di gestione temporanea sono supportati?</span><span class="sxs-lookup"><span data-stu-id="2d245-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="2d245-131">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="2d245-131">**A:** Yes.</span></span>

<span data-ttu-id="2d245-132">**Q:** è possibile utilizzare **distribuzione web** toodeploy dell'app web?</span><span class="sxs-lookup"><span data-stu-id="2d245-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="2d245-133">**R:** Sì, è necessario tooset un'app denominata `WEBSITE_WEBDEPLOY_USE_SCM` troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="2d245-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="2d245-134">Supporto per le lingue</span><span class="sxs-lookup"><span data-stu-id="2d245-134">Language support</span></span>

<span data-ttu-id="2d245-135">**D:** È presente il supporto per le app .NET Core non compilate?</span><span class="sxs-lookup"><span data-stu-id="2d245-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="2d245-136">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="2d245-136">**A:** Yes.</span></span>

<span data-ttu-id="2d245-137">**R:** È previsto il supporto per lo strumento Composer come gestore delle dipendenze per le app PHP?</span><span class="sxs-lookup"><span data-stu-id="2d245-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="2d245-138">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="2d245-138">**A:** Yes.</span></span> <span data-ttu-id="2d245-139">Durante una distribuzione Git, Kudu deve rilevare che si sta distribuendo un'applicazione PHP (grazie toohello presenza di un file composer.json) e verrà attivata un'installazione di creazione per l'utente.</span><span class="sxs-lookup"><span data-stu-id="2d245-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="2d245-140">Contenitori personalizzati</span><span class="sxs-lookup"><span data-stu-id="2d245-140">Custom containers</span></span>

<span data-ttu-id="2d245-141">**D:** Uso un contenitore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2d245-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="2d245-142">L'applicazione si trova in hello `\home\` directory, ma non è possibile trovare i file quando si naviga contenuto hello utilizzando hello [sito SCM](https://github.com/projectkudu/kudu) o un client FTP.</span><span class="sxs-lookup"><span data-stu-id="2d245-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="2d245-143">Dove si trovano i file?</span><span class="sxs-lookup"><span data-stu-id="2d245-143">Where are my files?</span></span>

<span data-ttu-id="2d245-144">**R:** montaggio un toohello condivisione SMB `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="2d245-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="2d245-145">In questo modo viene sostituito qualsiasi contenuto presente.</span><span class="sxs-lookup"><span data-stu-id="2d245-145">This will override any content that's there.</span></span>

<span data-ttu-id="2d245-146">**D:** Uso un contenitore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2d245-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="2d245-147">Non si desidera hello piattaforma toomount un toohello condivisione SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="2d245-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="2d245-148">**R:** scopo è possibile che l'impostazione hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app impostazione troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="2d245-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="2d245-149">**Q:** il contenitore personalizzato accetta un toostart molto tempo e contenitore di hello hello piattaforma riavvio prima che termina l'avvio.</span><span class="sxs-lookup"><span data-stu-id="2d245-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="2d245-150">**R:** è possibile configurare ora hello piattaforma hello attenderà prima di riavviare il contenitore.</span><span class="sxs-lookup"><span data-stu-id="2d245-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="2d245-151">Questa operazione può essere eseguita dall'impostazione hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello impostazione app valore desiderato in secondi.</span><span class="sxs-lookup"><span data-stu-id="2d245-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="2d245-152">valore predefinito di Hello è 230 secondi e hello max è 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="2d245-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="2d245-153">**Q:** che cos'è il formato di hello per l'url del server del Registro di sistema privato?</span><span class="sxs-lookup"><span data-stu-id="2d245-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="2d245-154">**R:** occorre tooprovide hello del Registro di sistema completo url inclusi `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="2d245-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="2d245-155">**Q:** che cos'è il formato di hello per il nome dell'immagine hello nell'opzione del Registro di sistema privato?</span><span class="sxs-lookup"><span data-stu-id="2d245-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="2d245-156">**R:** occorre nome immagine completa di hello tooadd compresi url privato del Registro di sistema di hello (ad es.</span><span class="sxs-lookup"><span data-stu-id="2d245-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="2d245-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="2d245-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="2d245-158">**Q:** desiderato tooexpose più di una porta in immagine contenitore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2d245-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="2d245-159">È possibile?</span><span class="sxs-lookup"><span data-stu-id="2d245-159">Is that possible?</span></span>

<span data-ttu-id="2d245-160">**R:** Attualmente questa operazione non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2d245-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="2d245-161">**D:** È possibile usare la propria archiviazione?</span><span class="sxs-lookup"><span data-stu-id="2d245-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="2d245-162">**R:** Attualmente questa operazione non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2d245-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="2d245-163">**Q:** non è possibile accedere my del contenitore personalizzato file system o in esecuzione processi dal sito SCM hello.</span><span class="sxs-lookup"><span data-stu-id="2d245-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="2d245-164">Perché?</span><span class="sxs-lookup"><span data-stu-id="2d245-164">Why is that?</span></span>

<span data-ttu-id="2d245-165">**R:** sito SCM hello viene eseguito in un contenitore separato.</span><span class="sxs-lookup"><span data-stu-id="2d245-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="2d245-166">Non è possibile controllare il sistema di file hello o in esecuzione processi di contenitore di app hello.</span><span class="sxs-lookup"><span data-stu-id="2d245-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="2d245-167">**Q:** il contenitore personalizzato è in ascolto porta tooa diversa dalla porta 80.</span><span class="sxs-lookup"><span data-stu-id="2d245-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="2d245-168">Come è possibile configurare la porta toothat le richieste di app tooroute hello?</span><span class="sxs-lookup"><span data-stu-id="2d245-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="2d245-169">**R:** abbiamo il rilevamento automatico porta, è anche possibile specificare un'applicazione denominata **WEBSITES_PORT**e assegnare il valore di hello del numero di porta hello previsto.</span><span class="sxs-lookup"><span data-stu-id="2d245-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="2d245-170">In precedenza si utilizzava piattaforma hello `PORT` app impostazione, si intende utilizzare hello toodeprecate questa impostazione di app e spostare toousing `WEBSITES_PORT` in modo esclusivo.</span><span class="sxs-lookup"><span data-stu-id="2d245-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="2d245-171">**Q:** necessario tooimplement HTTPS nel mio contenitore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2d245-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="2d245-172">**R:** No, piattaforma hello gestisce la terminazione HTTPS al server front-end hello condiviso.</span><span class="sxs-lookup"><span data-stu-id="2d245-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="2d245-173">Prezzi e contratto di servizio</span><span class="sxs-lookup"><span data-stu-id="2d245-173">Pricing and SLA</span></span>

<span data-ttu-id="2d245-174">**Q:** che cos'è hello prezzi quando si usa l'anteprima pubblica di hello?</span><span class="sxs-lookup"><span data-stu-id="2d245-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="2d245-175">**R:** vengono addebitati metà hello quante ore che esegue l'app, con prezzi hello normale servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d245-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="2d245-176">Ciò significa che si ottiene uno sconto del 50% sul normale prezzo del Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d245-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="2d245-177">Altre</span><span class="sxs-lookup"><span data-stu-id="2d245-177">Other</span></span>

<span data-ttu-id="2d245-178">**Q:** quali sono i caratteri di hello è supportato nei nomi di impostazioni applicazione?</span><span class="sxs-lookup"><span data-stu-id="2d245-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="2d245-179">**R:** è solo possibile utilizzare A-Z, a-z, 0-9 e hello carattere di sottolineatura per le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d245-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="2d245-180">**D:** Dove è possibile richiedere nuove funzionalità?</span><span class="sxs-lookup"><span data-stu-id="2d245-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="2d245-181">**R:** è possibile inviare l'idea hello [forum sul feedback su applicazioni Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="2d245-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="2d245-182">Aggiungere il titolo toohello "[Linux]" della propria idea.</span><span class="sxs-lookup"><span data-stu-id="2d245-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d245-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d245-183">Next steps</span></span>
* [<span data-ttu-id="2d245-184">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="2d245-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* <span data-ttu-id="2d245-185">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md) (Supporto SSH per App Web di Azure in Linux)</span><span class="sxs-lookup"><span data-stu-id="2d245-185">[SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md)</span></span>
* [<span data-ttu-id="2d245-186">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="2d245-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="2d245-187">Distribuzione continua con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="2d245-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
