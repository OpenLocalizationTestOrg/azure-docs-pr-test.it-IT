---
title: "aaaWhat è un modello di servizio Cloud e di un pacchetto | Documenti Microsoft"
description: Viene descritto il modello del servizio cloud hello (con estensione csdef, con estensione cscfg) e il pacchetto (con estensione cspkg) in Azure
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="a1ad6-103">Che cos'è il modello di servizio Cloud hello e come pacchetto?</span><span class="sxs-lookup"><span data-stu-id="a1ad6-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="a1ad6-104">Viene creato un servizio cloud da tre componenti, la definizione di servizio hello *(con estensione csdef)*, hello configurazione del servizio *(. cscfg)*, un pacchetto del servizio e *(con estensione cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="a1ad6-105">Entrambi hello **Servicedefinition** e **ServiceConfig.cscfg** file sono basati su XML e descrivono la struttura hello del servizio cloud hello e come è configurato; collettivamente denominati modello hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="a1ad6-106">Hello **ServicePackage.cspkg** è un file zip che viene generato da hello **Servicedefinition** e tra le altre cose, contiene tutte le dipendenze basate su file binario hello necessario.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="a1ad6-107">Azure crea un servizio cloud da entrambi hello **ServicePackage.cspkg** hello e **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="a1ad6-108">Servizio cloud hello in esecuzione in Azure, è possibile riconfigurare tramite hello **ServiceConfig.cscfg** file, ma non è possibile modificare la definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="a1ad6-109">Ciò che si desidera tooknow ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="a1ad6-110">Si desidera approfondire hello tooknow [Servicedefinition](#csdef) e [ServiceConfig.cscfg](#cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="a1ad6-111">Si hanno già informazioni in proposito, ma sono necessari [alcuni esempi](#next-steps) sugli elementi configurabili.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="a1ad6-112">Voglio hello toocreate [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="a1ad6-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="a1ad6-113">Si sta usando Visual Studio e si vuole...</span><span class="sxs-lookup"><span data-stu-id="a1ad6-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="a1ad6-114">[Creare un servizio cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="a1ad6-115">[Riconfigurare un servizio cloud esistente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="a1ad6-116">[Distribuire un progetto di servizio cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="a1ad6-117">[Desktop remoto in un'istanza del servizio cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="a1ad6-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="a1ad6-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="a1ad6-119">Hello **Servicedefinition** file specifica le impostazioni di hello usati da Azure tooconfigure un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="a1ad6-120">Hello [dello Schema di definizione del servizio di Azure (File con estensione csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornisce formato consentito di hello per un file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="a1ad6-121">Hello riportato di seguito le impostazioni di hello che possono essere definite per hello Web e ruoli di lavoro:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="a1ad6-122">È possibile fare riferimento toohello [dello Schema di definizione del servizio](https://msdn.microsoft.com/library/azure/ee758711.aspx) per una migliore comprensione di hello XML schema utilizzato in questo caso, tuttavia, viene fornita una rapida spiegazione di alcuni degli elementi di hello:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="a1ad6-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-123">**Sites**</span></span>  
<span data-ttu-id="a1ad6-124">Contiene le definizioni di hello per siti o applicazioni web ospitate in IIS7.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="a1ad6-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-125">**InputEndpoints**</span></span>  
<span data-ttu-id="a1ad6-126">Contiene le definizioni di hello per gli endpoint servizio cloud di hello toocontact utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="a1ad6-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="a1ad6-128">Contiene le definizioni di hello per gli endpoint utilizzati dal ruolo istanze toocommunicate tra loro.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="a1ad6-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="a1ad6-130">Contiene le definizioni di impostazione hello per le funzionalità di un ruolo specifico.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="a1ad6-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-131">**Certificates**</span></span>  
<span data-ttu-id="a1ad6-132">Contiene le definizioni di hello per i certificati necessari per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="a1ad6-133">esempio di codice Hello precedente mostra un certificato utilizzato per la configurazione di Azure Connect hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="a1ad6-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-134">**LocalResources**</span></span>  
<span data-ttu-id="a1ad6-135">Contiene le definizioni di hello per le risorse di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="a1ad6-136">Una risorsa di archiviazione locale è una directory riservata nel file system di hello della macchina virtuale hello in cui è in esecuzione un'istanza di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="a1ad6-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-137">**Imports**</span></span>  
<span data-ttu-id="a1ad6-138">Contiene le definizioni di hello per i moduli importati.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="a1ad6-139">esempio di codice precedente Hello i moduli di hello per connessione Desktop remoto e Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="a1ad6-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-140">**Startup**</span></span>  
<span data-ttu-id="a1ad6-141">Contiene le attività eseguite all'avvio ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="a1ad6-142">Hello attività sono definite in un file eseguibile o di cmd.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="a1ad6-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="a1ad6-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="a1ad6-144">Hello configurazione delle impostazioni di hello per il servizio cloud è determinata dai valori hello hello **ServiceConfiguration. cscfg** file.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="a1ad6-145">Specificare il numero di hello di istanze che si desidera toodeploy per ogni ruolo in questo file.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="a1ad6-146">i valori Hello per le impostazioni di configurazione hello è definito nel file di definizione del servizio hello vengono aggiunti file di configurazione del servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="a1ad6-147">identificazioni personali di Hello per i certificati di gestione che sono associati al servizio cloud hello vengono aggiunti anche file toohello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="a1ad6-148">Hello [dello Schema di configurazione del servizio di Azure (File con estensione cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornisce formato consentito di hello per un file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="a1ad6-149">Hello file di configurazione del servizio non è incluso in un'applicazione hello, ma è tooAzure caricato come file separato e viene utilizzato tooconfigure hello servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="a1ad6-150">È possibile caricare un nuovo file di configurazione del servizio senza ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="a1ad6-151">i valori di configurazione Hello per il servizio cloud hello possono essere modificati mentre è in esecuzione il servizio di cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="a1ad6-152">Hello riportato di seguito le impostazioni di configurazione hello che possono essere definite per hello Web e ruoli di lavoro:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="a1ad6-153">È possibile fare riferimento toohello [dello Schema di configurazione del servizio](https://msdn.microsoft.com/library/azure/ee758710.aspx) per una migliore comprensione hello XML schema utilizzato qui, tuttavia, viene fornita una rapida spiegazione degli elementi di hello:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="a1ad6-154">**Istanze**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-154">**Instances**</span></span>  
<span data-ttu-id="a1ad6-155">Configura hello numero di istanze per ruolo hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="a1ad6-156">tooprevent del servizio cloud diventi potenzialmente non disponibile durante gli aggiornamenti, è consigliabile distribuire più istanze dei ruoli basata sul web.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="a1ad6-157">La distribuzione di più di un'istanza, si rispettano le linee guida toohello in hello [Azure Compute livello di contratto di servizio](http://azure.microsoft.com/support/legal/sla/), che garantisce una connettività esterna pari al 99,95% per i ruoli con connessione Internet quando due o più ruoli le istanze vengono distribuite per un servizio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="a1ad6-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="a1ad6-159">Configura le impostazioni di hello per hello istanze in esecuzione per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="a1ad6-160">nome Hello di hello `<Setting>` elementi devono corrispondere relative definizioni nel file di definizione del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="a1ad6-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-161">**Certificates**</span></span>  
<span data-ttu-id="a1ad6-162">Consente di configurare i certificati di hello utilizzati dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="a1ad6-163">esempio di codice Hello precedente viene illustrato come toodefine hello certificato per il modulo RemoteAccess hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="a1ad6-164">valore di hello Hello *identificazione personale* attributo deve essere impostato l'identificazione personale toohello del toouse certificato hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="a1ad6-165">identificazione digitale certificato hello Hello possibile aggiungere file di configurazione toohello utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="a1ad6-166">O, hello valore può essere aggiunto in hello **certificati** scheda di hello **proprietà** pagina del ruolo di hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="a1ad6-167">Definizione delle porte per le istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="a1ad6-167">Defining ports for role instances</span></span>
<span data-ttu-id="a1ad6-168">Azure consente un solo ruolo web tooa punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="a1ad6-169">Ciò significa che tutto il traffico viene gestito tramite un solo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="a1ad6-170">È possibile configurare il tooshare di siti Web, una porta configurando hello host intestazione toodirect hello richiesta toohello posizione corretta.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="a1ad6-171">È inoltre possibile configurare le porte di applicazioni toolisten toowell note sull'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="a1ad6-172">Hello esempio seguente viene illustrata hello configurazione per un ruolo web con un'applicazione web e il sito Web.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="a1ad6-173">sito Web di Hello è configurato come hello posizione predefinita di ingresso sulla porta 80 e applicazioni web hello sono configurati tooreceive richieste da un'intestazione host alternativa denominata "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="a1ad6-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="a1ad6-174">La modifica della configurazione di un ruolo hello</span><span class="sxs-lookup"><span data-stu-id="a1ad6-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="a1ad6-175">È possibile aggiornare la configurazione hello del servizio cloud mentre è in esecuzione in Azure, senza portare offline il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="a1ad6-176">toochange le informazioni di configurazione, è possibile caricare un nuovo file di configurazione, oppure Modifica file di configurazione hello in posizionare e applicarlo tooyour in esecuzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="a1ad6-177">Hello seguenti è possibile apportare modifiche toohello configurazione di un servizio:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="a1ad6-178">**Modifica di valori hello delle impostazioni di configurazione**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="a1ad6-179">Quando una configurazione impostando le modifiche, un'istanza del ruolo possa scegliere tooapply hello modifica mentre hello istanza è online o istanza hello toorecycle normalmente e applicare modifiche hello mentre istanza hello è offline.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="a1ad6-180">**Modifica della topologia di hello servizio delle istanze del ruolo**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="a1ad6-181">Le modifiche di topologia non influiscono sulle istanze in esecuzione, a eccezione del caso di rimozione di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="a1ad6-182">Tutte le istanze rimanenti, in genere, non è necessario toobe riciclato; Tuttavia, è possibile scegliere toorecycle le istanze del ruolo nella modifica di topologia tooa di risposta.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="a1ad6-183">**Modifica l'identificazione personale del certificato hello**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="a1ad6-184">È possibile aggiornare un certificato solo quando un'istanza del ruolo è offline.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="a1ad6-185">Se un certificato viene aggiunto, eliminato o modificato mentre un'istanza del ruolo è online, Azure normalmente accetta certificato hello tooupdate offline di istanza hello e riportarlo online dopo aver completato la modifica hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="a1ad6-186">Gestione delle modifiche di configurazione con gli eventi di runtime del servizio</span><span class="sxs-lookup"><span data-stu-id="a1ad6-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="a1ad6-187">Hello [libreria di Runtime Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) include hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) spazio dei nomi, che fornisce le classi per l'interazione con hello ambiente Azure da un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="a1ad6-188">Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe definisce hello dopo gli eventi generati prima e dopo una modifica della configurazione:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="a1ad6-189">**Evento [Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="a1ad6-190">Ciò si verifica prima della modifica della configurazione hello tooa applicato istanza specificata di un ruolo è una possibilità tootake verso il basso le istanze del ruolo hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="a1ad6-191">**Evento [Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**</span><span class="sxs-lookup"><span data-stu-id="a1ad6-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="a1ad6-192">Si verifica dopo la modifica della configurazione hello è applicato tooa istanza specificata di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ad6-193">Poiché non in linea delle modifiche al certificato hanno sempre istanze hello di un ruolo, non generano eventi roleenvironment. Changing o Roleenvironment di hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="a1ad6-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="a1ad6-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="a1ad6-195">toodeploy un'applicazione come servizio cloud in Azure, è necessario prima applicazione hello del pacchetto nel formato appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="a1ad6-196">È possibile utilizzare hello **CSPack** strumento da riga di comando (installato con hello [Azure SDK](https://azure.microsoft.com/downloads/)) file del pacchetto toocreate hello come un'alternativa tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="a1ad6-197">**CSPack** utilizza hello contenuto di hello servizio definizione servizi file e configurazione toodefine hello contenuto del file del pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="a1ad6-198">**CSPack** genera un file di pacchetto di applicazione (con estensione cspkg) che è possibile caricare tooAzure utilizzando hello [portale di Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="a1ad6-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="a1ad6-199">Per impostazione predefinita, viene denominato pacchetto hello `[ServiceDefinitionFileName].cspkg`, ma è possibile specificare un nome diverso utilizzando hello `/out` opzione di **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="a1ad6-200">**CSPack** si trova in</span><span class="sxs-lookup"><span data-stu-id="a1ad6-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="a1ad6-201">CSPack.exe (in windows) è disponibile eseguendo hello **prompt dei comandi di Microsoft Azure** scelta rapida che viene installato con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="a1ad6-202">Esecuzione programma CSPack.exe hello toosee documentazione su tutti i comandi e le opzioni possibili hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="a1ad6-203">Eseguire il servizio cloud localmente in hello **emulatore di calcolo di Microsoft Azure**, utilizzare hello **/copyonly** opzione.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="a1ad6-204">Questa opzione consente di copiare i file binari di hello per layout di hello applicazione tooa directory da cui possono essere eseguiti nell'emulatore di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="a1ad6-205">Comando di esempio toopackage un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="a1ad6-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="a1ad6-206">Hello seguente viene creato un pacchetto di applicazione che contiene informazioni di hello per un ruolo web.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="a1ad6-207">comando Hello specifica hello servizio definizione file toouse, trovato directory hello in cui possono essere i file binari e nome del file di pacchetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="a1ad6-208">Se un'applicazione hello contiene sia un ruolo web e un ruolo di lavoro, hello comando riportato di seguito viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="a1ad6-209">Le variabili di hello in cui sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="a1ad6-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="a1ad6-210">Variabile</span><span class="sxs-lookup"><span data-stu-id="a1ad6-210">Variable</span></span> | <span data-ttu-id="a1ad6-211">Valore</span><span class="sxs-lookup"><span data-stu-id="a1ad6-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1ad6-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-212">\[DirectoryName\]</span></span> |<span data-ttu-id="a1ad6-213">Hello sottodirectory nella directory di progetto hello radice che contiene il file con estensione csdef hello di hello progetto Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="a1ad6-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="a1ad6-215">nome Hello del file di definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-215">hello name of hello service definition file.</span></span> <span data-ttu-id="a1ad6-216">Per impostazione predefinita, il file è denominato ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="a1ad6-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-217">\[OutputFileName\]</span></span> |<span data-ttu-id="a1ad6-218">nome Hello per hello ha generato il file di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-218">hello name for hello generated package file.</span></span> <span data-ttu-id="a1ad6-219">In genere, viene impostato toohello nome di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="a1ad6-220">Se viene specificato alcun nome di file, il pacchetto di applicazione hello viene creato come \[ApplicationName\]con estensione cspkg.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="a1ad6-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-221">\[RoleName\]</span></span> |<span data-ttu-id="a1ad6-222">nome Hello del ruolo di hello come definito nel file di definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="a1ad6-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="a1ad6-224">percorso di Hello dei file binari di hello per ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="a1ad6-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-225">\[VirtualPath\]</span></span> |<span data-ttu-id="a1ad6-226">directory fisiche di Hello per ogni percorso virtuale definito nella sezione Sites hello della definizione di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="a1ad6-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="a1ad6-228">Hello directory fisiche del contenuto di hello per ogni percorso virtuale definito nel nodo di sito hello della definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="a1ad6-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="a1ad6-230">nome Hello del file binario di hello per ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="a1ad6-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a1ad6-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1ad6-231">Next steps</span></span>
<span data-ttu-id="a1ad6-232">Si sta creando un pacchetto del servizio cloud e si vuole...</span><span class="sxs-lookup"><span data-stu-id="a1ad6-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="a1ad6-233">[Configurare il desktop remoto per un'istanza del servizio cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="a1ad6-234">[Distribuire un progetto di servizio cloud][deploy]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="a1ad6-235">Si sta usando Visual Studio e si vuole...</span><span class="sxs-lookup"><span data-stu-id="a1ad6-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="a1ad6-236">[Creare un nuovo servizio cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="a1ad6-237">[Riconfigurare un servizio cloud esistente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="a1ad6-238">[Distribuire un progetto di servizio cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="a1ad6-239">[Configurare il desktop remoto per un'istanza del servizio cloud][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="a1ad6-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
