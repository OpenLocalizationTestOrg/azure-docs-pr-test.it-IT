---
title: Cosa sono un modello del servizio cloud e un pacchetto | Documentazione Microsoft
description: Descrive il modello del servizio cloud (csdef, cscfg) e il pacchetto (cspkg) in Azure
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="6dd13-103">Cos'è il modello del servizio cloud e come è possibile crearne il pacchetto?</span><span class="sxs-lookup"><span data-stu-id="6dd13-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="6dd13-104">Un servizio cloud viene creato da tre componenti: la definizione del servizio *(.csdef)*, la configurazione del servizio *(.cscfg)* e un pacchetto servizio *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="6dd13-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="6dd13-105">Entrambi i file **ServiceDefinition.csdef** e **ServiceConfig.cscfg** sono basati su XML e descrivono la struttura e la configurazione del servizio cloud. Insieme costituiscono il modello.</span><span class="sxs-lookup"><span data-stu-id="6dd13-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="6dd13-106">**ServicePackage.cspkg** è un file ZIP generato da **ServiceDefinition.csdef** e contiene, oltre ad altri elementi, tutte le dipendenze necessarie basate su file binari.</span><span class="sxs-lookup"><span data-stu-id="6dd13-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="6dd13-107">Azure crea un servizio cloud sia da **ServicePackage.cspkg** che da **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="6dd13-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="6dd13-108">Una volta che il servizio cloud è in esecuzione in Azure, è possibile riconfigurarlo tramite il file **ServiceConfig.cscfg** , ma non è possibile modificare la definizione.</span><span class="sxs-lookup"><span data-stu-id="6dd13-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="6dd13-109">Quali altre informazioni sono necessarie?</span><span class="sxs-lookup"><span data-stu-id="6dd13-109">What would you like to know more about?</span></span>
* <span data-ttu-id="6dd13-110">Si vuole sapere di più sui file [ServiceDefinition.csdef](#csdef) e [ServiceConfig.cscfg](#cscfg).</span><span class="sxs-lookup"><span data-stu-id="6dd13-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="6dd13-111">Si hanno già informazioni in proposito, ma sono necessari [alcuni esempi](#next-steps) sugli elementi configurabili.</span><span class="sxs-lookup"><span data-stu-id="6dd13-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="6dd13-112">Si vuole crea [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="6dd13-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="6dd13-113">Si sta usando Visual Studio e si vuole...</span><span class="sxs-lookup"><span data-stu-id="6dd13-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="6dd13-114">[Creare un servizio cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="6dd13-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="6dd13-115">[Riconfigurare un servizio cloud esistente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="6dd13-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="6dd13-116">[Distribuire un progetto di servizio cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="6dd13-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="6dd13-117">[Desktop remoto in un'istanza del servizio cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="6dd13-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="6dd13-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="6dd13-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="6dd13-119">Il file **ServiceDefinition.csdef** specifica le impostazioni usate da Azure per configurare un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6dd13-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="6dd13-120">Lo [schema di definizione dei servizi di Azure (file .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornisce il formato consentito per un file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="6dd13-121">L'esempio seguente mostra le impostazioni che possono essere definite per i ruoli Web e di lavoro:</span><span class="sxs-lookup"><span data-stu-id="6dd13-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="6dd13-122">È possibile fare riferimento allo [schema di definizione dei servizi](https://msdn.microsoft.com/library/azure/ee758711.aspx) per comprendere meglio lo schema XML usato qui, ma viene indicata anche una breve spiegazione di alcuni elementi:</span><span class="sxs-lookup"><span data-stu-id="6dd13-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="6dd13-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="6dd13-123">**Sites**</span></span>  
<span data-ttu-id="6dd13-124">Contiene le definizioni per i siti Web o per le applicazioni Web ospitate in IIS7.</span><span class="sxs-lookup"><span data-stu-id="6dd13-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="6dd13-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="6dd13-125">**InputEndpoints**</span></span>  
<span data-ttu-id="6dd13-126">Contiene le definizioni per gli endpoint usati per contattare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6dd13-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="6dd13-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="6dd13-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="6dd13-128">Contiene le definizioni per gli endpoint usati dalle istanze del ruolo per comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="6dd13-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="6dd13-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="6dd13-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="6dd13-130">Contiene le definizioni delle impostazioni per le funzionalità di un ruolo specifico.</span><span class="sxs-lookup"><span data-stu-id="6dd13-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="6dd13-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="6dd13-131">**Certificates**</span></span>  
<span data-ttu-id="6dd13-132">Contiene le definizioni dei certificati necessari per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="6dd13-133">L'esempio di codice precedente mostra un certificato usato per la configurazione di Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="6dd13-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="6dd13-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="6dd13-134">**LocalResources**</span></span>  
<span data-ttu-id="6dd13-135">Contiene le definizioni per le risorse di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="6dd13-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="6dd13-136">Una risorsa di archiviazione locale è una directory riservata nel file system della macchina virtuale in cui è in esecuzione un'istanza di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="6dd13-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="6dd13-137">**Imports**</span></span>  
<span data-ttu-id="6dd13-138">Contiene le definizioni per i moduli importati.</span><span class="sxs-lookup"><span data-stu-id="6dd13-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="6dd13-139">L'esempio di codice precedente mostra i moduli per la connessione Desktop remoto e Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="6dd13-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="6dd13-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="6dd13-140">**Startup**</span></span>  
<span data-ttu-id="6dd13-141">Contiene le attività eseguite all'avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="6dd13-142">Le attività vengono definite in un file eseguibile o con estensione cmd.</span><span class="sxs-lookup"><span data-stu-id="6dd13-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="6dd13-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="6dd13-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="6dd13-144">La configurazione delle impostazioni per il servizio cloud è determinata dai valori nel file **ServiceConfiguration.cscfg** .</span><span class="sxs-lookup"><span data-stu-id="6dd13-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="6dd13-145">Si specifica il numero di istanze che si vuole distribuire per ogni ruolo in questo file.</span><span class="sxs-lookup"><span data-stu-id="6dd13-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="6dd13-146">I valori per le impostazioni di configurazione definite nel file di definizione del servizio vengono aggiunti al file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="6dd13-147">Vengono aggiunte al file anche le identificazioni personali per eventuali certificati di gestione associati al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6dd13-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="6dd13-148">Lo [schema di configurazione dei servizi di Azure (file .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornisce il formato consentito per un file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="6dd13-149">Il file di configurazione del servizio non viene incluso nel pacchetto con l'applicazione, ma viene caricato in Azure come file separato e viene usato per configurare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6dd13-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="6dd13-150">È possibile caricare un nuovo file di configurazione del servizio senza ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6dd13-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="6dd13-151">I valori di configurazione per il servizio cloud possono essere modificati mentre il servizio cloud è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6dd13-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="6dd13-152">L'esempio seguente mostra le impostazioni di configurazione che possono essere definite per i ruoli Web e di lavoro:</span><span class="sxs-lookup"><span data-stu-id="6dd13-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="6dd13-153">È possibile fare riferimento allo [schema di configurazione dei servizi](https://msdn.microsoft.com/library/azure/ee758710.aspx) per comprendere meglio lo schema XML usato qui, ma ecco anche una rapida spiegazione degli elementi:</span><span class="sxs-lookup"><span data-stu-id="6dd13-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="6dd13-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="6dd13-154">**Instances**</span></span>  
<span data-ttu-id="6dd13-155">Configura il numero di istanze in esecuzione per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="6dd13-156">Per evitare che il servizio cloud diventi potenzialmente non disponibile durante gli aggiornamenti, è consigliabile distribuire più istanze dei ruoli esposti al Web.</span><span class="sxs-lookup"><span data-stu-id="6dd13-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="6dd13-157">In questo modo si rispettano le linee guida del [contratto di servizio (SLA, Service Level Agreement) per il servizio di calcolo di Azure](http://azure.microsoft.com/support/legal/sla/), che garantisce una connettività esterna pari al 99,95% per i ruoli esposti a Internet quando due o più istanze dei ruoli vengono distribuite per un servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="6dd13-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="6dd13-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="6dd13-159">Configura le impostazioni per le istanze in esecuzione di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="6dd13-160">Il nome degli elementi `<Setting>` deve corrispondere alle definizioni delle impostazioni nel file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="6dd13-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="6dd13-161">**Certificates**</span></span>  
<span data-ttu-id="6dd13-162">Configura i certificati usati dal servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="6dd13-163">L'esempio di codice precedente mostra come definire il certificato per il modulo RemoteAccess.</span><span class="sxs-lookup"><span data-stu-id="6dd13-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="6dd13-164">Il valore dell'attributo *thumbprint* deve essere impostato sull'identificazione personale del certificato da usare.</span><span class="sxs-lookup"><span data-stu-id="6dd13-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="6dd13-165">L'identificazione personale del certificato può essere aggiunta al file di configurazione usando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="6dd13-166">In alternativa, il valore può essere aggiunto nella scheda **Certificati** della pagina **Proprietà** relativa la ruolo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="6dd13-167">Definizione delle porte per le istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="6dd13-167">Defining ports for role instances</span></span>
<span data-ttu-id="6dd13-168">Azure consente solo un punto di ingresso a un ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="6dd13-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="6dd13-169">Ciò significa che tutto il traffico viene gestito tramite un solo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6dd13-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="6dd13-170">È possibile configurare la condivisione di una porta per i siti Web configurando l'intestazione host in modo da indirizzare la richiesta al percorso corretto.</span><span class="sxs-lookup"><span data-stu-id="6dd13-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="6dd13-171">Si possono anche configurare le applicazioni in modo che siano in ascolto di porte note sull'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6dd13-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="6dd13-172">L'esempio seguente illustra la configurazione di un ruolo Web con un sito Web e un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="6dd13-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="6dd13-173">Il sito Web è configurato come percorso di ingresso predefinito sulla porta 80 e le applicazioni Web sono configurate in modo da ricevere le richieste da un'intestazione host alternativa denominata "mail.mysite.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="6dd13-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="6dd13-174">Modifica della configurazione di un ruolo</span><span class="sxs-lookup"><span data-stu-id="6dd13-174">Changing the configuration of a role</span></span>
<span data-ttu-id="6dd13-175">È possibile aggiornare la configurazione del servizio cloud mentre è in esecuzione in Azure, senza portare il servizio offline.</span><span class="sxs-lookup"><span data-stu-id="6dd13-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="6dd13-176">Per modificare le informazioni di configurazione, è possibile caricare un nuovo file di configurazione o modificare il file di configurazione sul posto e applicarlo al servizio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6dd13-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="6dd13-177">Alla configurazione di un servizio possono essere apportate le seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="6dd13-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="6dd13-178">**Modifica dei valori delle impostazioni di configurazione**</span><span class="sxs-lookup"><span data-stu-id="6dd13-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="6dd13-179">Quando un'impostazione di configurazione viene modificata, è possibile applicare la modifica a un'istanza del ruolo mentre l'istanza è online oppure è possibile riciclare normalmente l'istanza e applicare la modifica mentre si trova offline.</span><span class="sxs-lookup"><span data-stu-id="6dd13-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="6dd13-180">**Modifica della topologia del servizio delle istanze del ruolo**</span><span class="sxs-lookup"><span data-stu-id="6dd13-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="6dd13-181">Le modifiche di topologia non influiscono sulle istanze in esecuzione, a eccezione del caso di rimozione di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="6dd13-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="6dd13-182">Non è in genere necessario riciclare tutte le istanze rimanenti; tuttavia, è possibile scegliere di riciclare le istanze del ruolo in risposta a una modifica di topologia.</span><span class="sxs-lookup"><span data-stu-id="6dd13-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="6dd13-183">**Modifica dell'identificazione personale del certificato**</span><span class="sxs-lookup"><span data-stu-id="6dd13-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="6dd13-184">È possibile aggiornare un certificato solo quando un'istanza del ruolo è offline.</span><span class="sxs-lookup"><span data-stu-id="6dd13-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="6dd13-185">Se un certificato viene aggiunto, eliminato o modificato mentre un'istanza del ruolo è online, in Azure l'istanza viene portata offline normalmente per aggiornare il certificato e riportata online dopo il completamento della modifica.</span><span class="sxs-lookup"><span data-stu-id="6dd13-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="6dd13-186">Gestione delle modifiche di configurazione con gli eventi di runtime del servizio</span><span class="sxs-lookup"><span data-stu-id="6dd13-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="6dd13-187">La [libreria di runtime di Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) include lo spazio dei nomi [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx), che fornisce le classi per l'interazione di un ruolo con l'ambiente di Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd13-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="6dd13-188">La classe [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) definisce gli eventi seguenti generati prima e dopo una modifica di configurazione:</span><span class="sxs-lookup"><span data-stu-id="6dd13-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="6dd13-189">**Evento [Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**</span><span class="sxs-lookup"><span data-stu-id="6dd13-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="6dd13-190">Si verifica prima che la modifica di configurazione venga applicata a un'istanza specificata di un ruolo, offrendo la possibilità di interrompere il funzionamento delle istanze del ruolo, se necessario.</span><span class="sxs-lookup"><span data-stu-id="6dd13-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="6dd13-191">**Evento [Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**</span><span class="sxs-lookup"><span data-stu-id="6dd13-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="6dd13-192">Si verifica dopo che la modifica della configurazione è stata applicata a un'istanza specificata di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="6dd13-193">Poiché le modifiche ai certificati richiedono sempre che le istanze di un ruolo siano portate offline, non generano eventi RoleEnvironment.Changing o RoleEnvironment.Changed.</span><span class="sxs-lookup"><span data-stu-id="6dd13-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="6dd13-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="6dd13-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="6dd13-195">Per distribuire un'applicazione come servizio cloud in Azure, è necessario prima creare un pacchetto dell'applicazione nel formato appropriato.</span><span class="sxs-lookup"><span data-stu-id="6dd13-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="6dd13-196">È possibile usare lo strumento da riga di comando **CSPack** (installato con [Azure SDK](https://azure.microsoft.com/downloads/)) per creare il file del pacchetto come alternativa a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="6dd13-197">**CSPack** usa il contenuto del file di definizione del servizio e del file di configurazione del servizio per definire il contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6dd13-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="6dd13-198">**CSPack** genera un file del pacchetto dell’applicazione (con estensione .cspkg) che è possibile caricare su Azure utilizzando il [portale di Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="6dd13-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="6dd13-199">Per impostazione predefinita, il pacchetto viene denominato `[ServiceDefinitionFileName].cspkg`, ma è possibile specificare un nome diverso usando l'opzione `/out` di **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="6dd13-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="6dd13-200">**CSPack** si trova in</span><span class="sxs-lookup"><span data-stu-id="6dd13-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="6dd13-201">CSPack.exe (in Windows) è disponibile eseguendo il collegamento del **prompt dei comandi di Microsoft Azure** installato con l'SDK.</span><span class="sxs-lookup"><span data-stu-id="6dd13-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="6dd13-202">Eseguire il programma CSPack.exe da solo per visualizzare la documentazione su tutti i comandi e le opzioni possibili.</span><span class="sxs-lookup"><span data-stu-id="6dd13-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="6dd13-203">Eseguire il servizio cloud in locale nell' **emulatore di calcolo di Microsoft Azure**, usando l'opzione **/copyonly**.</span><span class="sxs-lookup"><span data-stu-id="6dd13-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="6dd13-204">Questa opzione consente di copiare i file binari per l'applicazione in una struttura di directory da cui possono essere eseguiti nell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="6dd13-205">Comando di esempio per creare un pacchetto di un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="6dd13-205">Example command to package a cloud service</span></span>
<span data-ttu-id="6dd13-206">L'esempio seguente crea un pacchetto dell'applicazione che contiene le informazioni per un ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="6dd13-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="6dd13-207">Nel comando vengono specificati il file di definizione del servizio da utilizzare, la directory in cui trovare i file binari e il nome del file del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6dd13-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="6dd13-208">Se l'applicazione contiene sia un ruolo Web che un ruolo di lavoro, viene usato il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6dd13-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="6dd13-209">Dove le variabili vengono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6dd13-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="6dd13-210">Variabile</span><span class="sxs-lookup"><span data-stu-id="6dd13-210">Variable</span></span> | <span data-ttu-id="6dd13-211">Valore</span><span class="sxs-lookup"><span data-stu-id="6dd13-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6dd13-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-212">\[DirectoryName\]</span></span> |<span data-ttu-id="6dd13-213">Sottodirectory della directory radice del progetto contenente il file csdef del progetto Azure.</span><span class="sxs-lookup"><span data-stu-id="6dd13-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="6dd13-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="6dd13-215">Nome del file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-215">The name of the service definition file.</span></span> <span data-ttu-id="6dd13-216">Per impostazione predefinita, il file è denominato ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="6dd13-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="6dd13-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-217">\[OutputFileName\]</span></span> |<span data-ttu-id="6dd13-218">Nome del file del pacchetto generato.</span><span class="sxs-lookup"><span data-stu-id="6dd13-218">The name for the generated package file.</span></span> <span data-ttu-id="6dd13-219">Viene in genere impostato sul nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6dd13-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="6dd13-220">Se non viene specificato alcun nome file, il pacchetto dell'applicazione viene creato con il nome \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="6dd13-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="6dd13-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-221">\[RoleName\]</span></span> |<span data-ttu-id="6dd13-222">Nome del ruolo definito nel file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="6dd13-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="6dd13-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="6dd13-224">Percorso dei file binari del ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="6dd13-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-225">\[VirtualPath\]</span></span> |<span data-ttu-id="6dd13-226">Directory fisiche per ogni percorso virtuale definito nella sezione Sites della definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="6dd13-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="6dd13-228">Directory fisiche dei contenuti per ogni percorso virtuale definito nel nodo del sito della definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6dd13-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="6dd13-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="6dd13-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="6dd13-230">Nome del file binario del ruolo.</span><span class="sxs-lookup"><span data-stu-id="6dd13-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6dd13-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6dd13-231">Next steps</span></span>
<span data-ttu-id="6dd13-232">Si sta creando un pacchetto del servizio cloud e si vuole...</span><span class="sxs-lookup"><span data-stu-id="6dd13-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="6dd13-233">[Configurare il desktop remoto per un'istanza del servizio cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="6dd13-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="6dd13-234">[Distribuire un progetto di servizio cloud][deploy]</span><span class="sxs-lookup"><span data-stu-id="6dd13-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="6dd13-235">Si sta usando Visual Studio e si vuole...</span><span class="sxs-lookup"><span data-stu-id="6dd13-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="6dd13-236">[Creare un nuovo servizio cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="6dd13-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="6dd13-237">[Riconfigurare un servizio cloud esistente][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="6dd13-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="6dd13-238">[Distribuire un progetto di servizio cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="6dd13-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="6dd13-239">[Configurare il desktop remoto per un'istanza del servizio cloud][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="6dd13-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
