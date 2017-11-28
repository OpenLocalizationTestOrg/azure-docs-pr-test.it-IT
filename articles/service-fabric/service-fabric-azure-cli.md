---
title: Introduzione a Azure Service Fabric XPlat CLI aaaGetting
description: Introduzione all'interfaccia della riga di comando XPlat per Azure Service Fabric
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="c72e0-103">Utilizzo di hello XPlat CLI toointeract con un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c72e0-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="c72e0-104">È possibile interagire con i cluster di Service Fabric dai computer Linux usando hello XPlat CLI su Linux.</span><span class="sxs-lookup"><span data-stu-id="c72e0-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="c72e0-105">innanzitutto Hello è ottenere la versione più recente di hello di hello CLI da rep git hello e set, configurarlo nel percorso utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c72e0-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="c72e0-106">Per ogni comando, supporta, è possibile digitare nome hello della Guida in linea hello tooobtain comando hello per quel comando.</span><span class="sxs-lookup"><span data-stu-id="c72e0-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="c72e0-107">Completamento automatico è supportato per i comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="c72e0-108">Ad esempio, hello seguente consente di comando che la Guida per tutti i comandi di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="c72e0-109">È possibile filtrare ulteriormente i comandi specifici tooa Guida hello, come hello esempio illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c72e0-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="c72e0-110">tooenable il completamento automatico in hello CLI, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c72e0-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="c72e0-111">Hello seguenti comandi connettersi toohello cluster e si hello nodi cluster hello Mostra:</span><span class="sxs-lookup"><span data-stu-id="c72e0-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="c72e0-112">toouse parametri denominati e individuare che cosa sono, è possibile digitare - Guida in linea dopo un comando.</span><span class="sxs-lookup"><span data-stu-id="c72e0-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="c72e0-113">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c72e0-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="c72e0-114">Quando ci si connette tooa cluster con più computer da una macchina **che non fanno parte del cluster hello**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="c72e0-115">Sostituire il tag di PublicIPorFQDN hello con hello reale IP o FQDN come appropriato.</span><span class="sxs-lookup"><span data-stu-id="c72e0-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="c72e0-116">Quando ci si connette tooa cluster con più computer da una macchina **che fa parte del cluster hello**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="c72e0-117">È possibile utilizzare PowerShell o toointeract CLI con il Cluster di Service Fabric Linux creato tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c72e0-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="c72e0-118">Questi cluster non sono protetti, pertanto, potrebbe essere aprendo l'unica finestra aggiungendo l'indirizzo IP pubblico hello nel manifesto del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="c72e0-119">Utilizzo di cluster di Service Fabric tooa tooconnect XPlat CLI hello</span><span class="sxs-lookup"><span data-stu-id="c72e0-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="c72e0-120">Hello seguendo i comandi CLI di Azure viene descritto come tooconnect tooa proteggere i cluster.</span><span class="sxs-lookup"><span data-stu-id="c72e0-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="c72e0-121">dettagli del certificato Hello devono corrispondere al certificato sui nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="c72e0-122">Se il certificato dispone di autorità di certificazione (CA), è necessario tooadd hello - ca-cert-parametro come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="c72e0-123">Se si dispone di più autorità di certificazione, è possibile utilizzare la virgola come delimitatore di hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="c72e0-124">Se il nome comune nel certificato hello non corrisponde a endpoint della connessione hello, è possibile utilizzare il parametro hello `--strict-ssl-false` toobypass hello verifica, come illustrato nel comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c72e0-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="c72e0-125">Se si desidera verifica hello CA tooskip, è possibile aggiungere hello - parametro false non autorizzato rifiuta, come illustrato nel comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c72e0-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="c72e0-126">Dopo la connessione, dovrebbe essere in grado di toorun altri toointeract comandi CLI con cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c72e0-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="c72e0-127">Distribuzione dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c72e0-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="c72e0-128">Eseguire i seguenti comandi toocopy, registrare e avviare l'applicazione di service fabric hello hello:</span><span class="sxs-lookup"><span data-stu-id="c72e0-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="c72e0-129">Aggiornamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c72e0-129">Upgrading your application</span></span>

<span data-ttu-id="c72e0-130">il processo di Hello è simile toohello [processo Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="c72e0-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="c72e0-131">Compilare, copiare, registrare e creare l'applicazione dalla directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="c72e0-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="c72e0-132">Se l'istanza dell'applicazione è denominato `fabric:/MySFApp`e il tipo di hello è MySFApp, comandi hello sarebbe come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c72e0-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="c72e0-133">Apportare hello Modifica applicazione tooyour e ricompilare il servizio hello modificato.</span><span class="sxs-lookup"><span data-stu-id="c72e0-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="c72e0-134">Hello aggiornamento modificate file manifesto del servizio (ServiceManifest.xml) con le versioni aggiornata di hello per hello servizio (e codice o configurazione o dati come appropriato).</span><span class="sxs-lookup"><span data-stu-id="c72e0-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="c72e0-135">Inoltre modificare il manifesto dell'applicazione hello (ApplicationManifest.xml) con numero di versione di hello aggiornato per un'applicazione hello e hello servizio modificato.</span><span class="sxs-lookup"><span data-stu-id="c72e0-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="c72e0-136">A questo punto, copiare e registrare l'applicazione aggiornata utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c72e0-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="c72e0-137">A questo punto, è possibile avviare l'aggiornamento dell'applicazione hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="c72e0-138">Ora è possibile monitorare l'aggiornamento di applicazione hello utilizzando SFX.</span><span class="sxs-lookup"><span data-stu-id="c72e0-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="c72e0-139">In pochi minuti, un'applicazione hello sarebbe sono stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="c72e0-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="c72e0-140">È anche possibile provare una versione aggiornata dell'app con un errore e verificare la funzionalità di rollback automatico hello nell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="c72e0-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="c72e0-141">La conversione dal file PFX tooPEM e viceversa</span><span class="sxs-lookup"><span data-stu-id="c72e0-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="c72e0-142">Potrebbe essere necessario tooinstall un certificato nel computer locale (con Windows o Linux) tooaccess sicura cluster che potrebbero essere in un ambiente diverso.</span><span class="sxs-lookup"><span data-stu-id="c72e0-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="c72e0-143">Ad esempio, durante l'accesso a un cluster Linux protetto da un computer Windows e viceversa potrebbe essere tooconvert il certificato dal file PFX tooPEM e viceversa.</span><span class="sxs-lookup"><span data-stu-id="c72e0-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="c72e0-144">tooconvert da un file PFX tooa di file PEM, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="c72e0-145">tooconvert da un file PEM tooa di file PFX, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="c72e0-146">Fare riferimento troppo[OpenSSL documentazione](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="c72e0-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="c72e0-147">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c72e0-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="c72e0-148">Copia del pacchetto di applicazione hello non riesce</span><span class="sxs-lookup"><span data-stu-id="c72e0-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="c72e0-149">Controllare se `openssh` è installato.</span><span class="sxs-lookup"><span data-stu-id="c72e0-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="c72e0-150">Per impostazione predefinita, in Ubuntu Desktop non è installato.</span><span class="sxs-lookup"><span data-stu-id="c72e0-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="c72e0-151">L'installazione utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c72e0-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="c72e0-152">Se hello problema persiste, provare a disabilitare PAM per ssh modificando hello `sshd_config` file utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c72e0-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="c72e0-153">Se hello problema persiste, provare a numero crescente di hello di ssh sessioni eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c72e0-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="c72e0-154">Utilizzo di chiavi per ssh autenticazione (come anziché toopasswords) non è ancora supportata (poiché hello piattaforma Usa ssh toocopy pacchetti), quindi utilizzare l'autenticazione di password.</span><span class="sxs-lookup"><span data-stu-id="c72e0-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c72e0-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c72e0-155">Next steps</span></span>

[<span data-ttu-id="c72e0-156">Configurare un ambiente di sviluppo hello e distribuire un cluster di Service Fabric applicazione tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="c72e0-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="c72e0-157">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="c72e0-157">Related articles</span></span>

* [<span data-ttu-id="c72e0-158">Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c72e0-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
