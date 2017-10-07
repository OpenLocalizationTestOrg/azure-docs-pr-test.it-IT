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
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Che cos'è il modello di servizio Cloud hello e come pacchetto?
Viene creato un servizio cloud da tre componenti, la definizione di servizio hello *(con estensione csdef)*, hello configurazione del servizio *(. cscfg)*, un pacchetto del servizio e *(con estensione cspkg)*. Entrambi hello **Servicedefinition** e **ServiceConfig.cscfg** file sono basati su XML e descrivono la struttura hello del servizio cloud hello e come è configurato; collettivamente denominati modello hello. Hello **ServicePackage.cspkg** è un file zip che viene generato da hello **Servicedefinition** e tra le altre cose, contiene tutte le dipendenze basate su file binario hello necessario. Azure crea un servizio cloud da entrambi hello **ServicePackage.cspkg** hello e **ServiceConfig.cscfg**.

Servizio cloud hello in esecuzione in Azure, è possibile riconfigurare tramite hello **ServiceConfig.cscfg** file, ma non è possibile modificare la definizione di hello.

## <a name="what-would-you-like-tooknow-more-about"></a>Ciò che si desidera tooknow ulteriori informazioni.
* Si desidera approfondire hello tooknow [Servicedefinition](#csdef) e [ServiceConfig.cscfg](#cscfg) file.
* Si hanno già informazioni in proposito, ma sono necessari [alcuni esempi](#next-steps) sugli elementi configurabili.
* Voglio hello toocreate [ServicePackage.cspkg](#cspkg).
* Si sta usando Visual Studio e si vuole...
  * [Creare un servizio cloud][vs_create]
  * [Riconfigurare un servizio cloud esistente][vs_reconfigure]
  * [Distribuire un progetto di servizio cloud][vs_deploy]
  * [Desktop remoto in un'istanza del servizio cloud][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Hello **Servicedefinition** file specifica le impostazioni di hello usati da Azure tooconfigure un servizio cloud. Hello [dello Schema di definizione del servizio di Azure (File con estensione csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornisce formato consentito di hello per un file di definizione del servizio. Hello riportato di seguito le impostazioni di hello che possono essere definite per hello Web e ruoli di lavoro:

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

È possibile fare riferimento toohello [dello Schema di definizione del servizio](https://msdn.microsoft.com/library/azure/ee758711.aspx) per una migliore comprensione di hello XML schema utilizzato in questo caso, tuttavia, viene fornita una rapida spiegazione di alcuni degli elementi di hello:

**Sites**  
Contiene le definizioni di hello per siti o applicazioni web ospitate in IIS7.

**InputEndpoints**  
Contiene le definizioni di hello per gli endpoint servizio cloud di hello toocontact utilizzato.

**InternalEndpoints**  
Contiene le definizioni di hello per gli endpoint utilizzati dal ruolo istanze toocommunicate tra loro.

**ConfigurationSettings**  
Contiene le definizioni di impostazione hello per le funzionalità di un ruolo specifico.

**Certificates**  
Contiene le definizioni di hello per i certificati necessari per un ruolo. esempio di codice Hello precedente mostra un certificato utilizzato per la configurazione di Azure Connect hello.

**LocalResources**  
Contiene le definizioni di hello per le risorse di archiviazione locale. Una risorsa di archiviazione locale è una directory riservata nel file system di hello della macchina virtuale hello in cui è in esecuzione un'istanza di un ruolo.

**Imports**  
Contiene le definizioni di hello per i moduli importati. esempio di codice precedente Hello i moduli di hello per connessione Desktop remoto e Azure Connect.

**Startup**  
Contiene le attività eseguite all'avvio ruolo hello. Hello attività sono definite in un file eseguibile o di cmd.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
Hello configurazione delle impostazioni di hello per il servizio cloud è determinata dai valori hello hello **ServiceConfiguration. cscfg** file. Specificare il numero di hello di istanze che si desidera toodeploy per ogni ruolo in questo file. i valori Hello per le impostazioni di configurazione hello è definito nel file di definizione del servizio hello vengono aggiunti file di configurazione del servizio toohello. identificazioni personali di Hello per i certificati di gestione che sono associati al servizio cloud hello vengono aggiunti anche file toohello. Hello [dello Schema di configurazione del servizio di Azure (File con estensione cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornisce formato consentito di hello per un file di configurazione del servizio.

Hello file di configurazione del servizio non è incluso in un'applicazione hello, ma è tooAzure caricato come file separato e viene utilizzato tooconfigure hello servizio cloud. È possibile caricare un nuovo file di configurazione del servizio senza ridistribuire il servizio cloud. i valori di configurazione Hello per il servizio cloud hello possono essere modificati mentre è in esecuzione il servizio di cloud hello. Hello riportato di seguito le impostazioni di configurazione hello che possono essere definite per hello Web e ruoli di lavoro:

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

È possibile fare riferimento toohello [dello Schema di configurazione del servizio](https://msdn.microsoft.com/library/azure/ee758710.aspx) per una migliore comprensione hello XML schema utilizzato qui, tuttavia, viene fornita una rapida spiegazione degli elementi di hello:

**Istanze**  
Configura hello numero di istanze per ruolo hello in esecuzione. tooprevent del servizio cloud diventi potenzialmente non disponibile durante gli aggiornamenti, è consigliabile distribuire più istanze dei ruoli basata sul web. La distribuzione di più di un'istanza, si rispettano le linee guida toohello in hello [Azure Compute livello di contratto di servizio](http://azure.microsoft.com/support/legal/sla/), che garantisce una connettività esterna pari al 99,95% per i ruoli con connessione Internet quando due o più ruoli le istanze vengono distribuite per un servizio.

**ConfigurationSettings**  
Configura le impostazioni di hello per hello istanze in esecuzione per un ruolo. nome Hello di hello `<Setting>` elementi devono corrispondere relative definizioni nel file di definizione del servizio hello hello.

**Certificates**  
Consente di configurare i certificati di hello utilizzati dal servizio hello. esempio di codice Hello precedente viene illustrato come toodefine hello certificato per il modulo RemoteAccess hello. valore di hello Hello *identificazione personale* attributo deve essere impostato l'identificazione personale toohello del toouse certificato hello.

<p/>

> [!NOTE]
> identificazione digitale certificato hello Hello possibile aggiungere file di configurazione toohello utilizzando un editor di testo. O, hello valore può essere aggiunto in hello **certificati** scheda di hello **proprietà** pagina del ruolo di hello in Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Definizione delle porte per le istanze del ruolo
Azure consente un solo ruolo web tooa punto di ingresso. Ciò significa che tutto il traffico viene gestito tramite un solo indirizzo IP. È possibile configurare il tooshare di siti Web, una porta configurando hello host intestazione toodirect hello richiesta toohello posizione corretta. È inoltre possibile configurare le porte di applicazioni toolisten toowell note sull'indirizzo IP hello.

Hello esempio seguente viene illustrata hello configurazione per un ruolo web con un'applicazione web e il sito Web. sito Web di Hello è configurato come hello posizione predefinita di ingresso sulla porta 80 e applicazioni web hello sono configurati tooreceive richieste da un'intestazione host alternativa denominata "mail.mysite.cloudapp.net".

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


## <a name="changing-hello-configuration-of-a-role"></a>La modifica della configurazione di un ruolo hello
È possibile aggiornare la configurazione hello del servizio cloud mentre è in esecuzione in Azure, senza portare offline il servizio di hello. toochange le informazioni di configurazione, è possibile caricare un nuovo file di configurazione, oppure Modifica file di configurazione hello in posizionare e applicarlo tooyour in esecuzione del servizio. Hello seguenti è possibile apportare modifiche toohello configurazione di un servizio:

* **Modifica di valori hello delle impostazioni di configurazione**  
  Quando una configurazione impostando le modifiche, un'istanza del ruolo possa scegliere tooapply hello modifica mentre hello istanza è online o istanza hello toorecycle normalmente e applicare modifiche hello mentre istanza hello è offline.
* **Modifica della topologia di hello servizio delle istanze del ruolo**  
  Le modifiche di topologia non influiscono sulle istanze in esecuzione, a eccezione del caso di rimozione di un'istanza. Tutte le istanze rimanenti, in genere, non è necessario toobe riciclato; Tuttavia, è possibile scegliere toorecycle le istanze del ruolo nella modifica di topologia tooa di risposta.
* **Modifica l'identificazione personale del certificato hello**  
  È possibile aggiornare un certificato solo quando un'istanza del ruolo è offline. Se un certificato viene aggiunto, eliminato o modificato mentre un'istanza del ruolo è online, Azure normalmente accetta certificato hello tooupdate offline di istanza hello e riportarlo online dopo aver completato la modifica hello.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Gestione delle modifiche di configurazione con gli eventi di runtime del servizio
Hello [libreria di Runtime Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) include hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) spazio dei nomi, che fornisce le classi per l'interazione con hello ambiente Azure da un ruolo. Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe definisce hello dopo gli eventi generati prima e dopo una modifica della configurazione:

* **Evento [Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**  
  Ciò si verifica prima della modifica della configurazione hello tooa applicato istanza specificata di un ruolo è una possibilità tootake verso il basso le istanze del ruolo hello se necessario.
* **Evento [Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**  
  Si verifica dopo la modifica della configurazione hello è applicato tooa istanza specificata di un ruolo.

> [!NOTE]
> Poiché non in linea delle modifiche al certificato hanno sempre istanze hello di un ruolo, non generano eventi roleenvironment. Changing o Roleenvironment di hello.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy un'applicazione come servizio cloud in Azure, è necessario prima applicazione hello del pacchetto nel formato appropriato hello. È possibile utilizzare hello **CSPack** strumento da riga di comando (installato con hello [Azure SDK](https://azure.microsoft.com/downloads/)) file del pacchetto toocreate hello come un'alternativa tooVisual Studio.

**CSPack** utilizza hello contenuto di hello servizio definizione servizi file e configurazione toodefine hello contenuto del file del pacchetto di hello. **CSPack** genera un file di pacchetto di applicazione (con estensione cspkg) che è possibile caricare tooAzure utilizzando hello [portale di Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Per impostazione predefinita, viene denominato pacchetto hello `[ServiceDefinitionFileName].cspkg`, ma è possibile specificare un nome diverso utilizzando hello `/out` opzione di **CSPack**.

**CSPack** si trova in  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (in windows) è disponibile eseguendo hello **prompt dei comandi di Microsoft Azure** scelta rapida che viene installato con hello SDK.  
> 
> Esecuzione programma CSPack.exe hello toosee documentazione su tutti i comandi e le opzioni possibili hello.
> 
> 

<p />

> [!TIP]
> Eseguire il servizio cloud localmente in hello **emulatore di calcolo di Microsoft Azure**, utilizzare hello **/copyonly** opzione. Questa opzione consente di copiare i file binari di hello per layout di hello applicazione tooa directory da cui possono essere eseguiti nell'emulatore di calcolo hello.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Comando di esempio toopackage un servizio cloud
Hello seguente viene creato un pacchetto di applicazione che contiene informazioni di hello per un ruolo web. comando Hello specifica hello servizio definizione file toouse, trovato directory hello in cui possono essere i file binari e nome del file di pacchetto hello hello.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Se un'applicazione hello contiene sia un ruolo web e un ruolo di lavoro, hello comando riportato di seguito viene utilizzato:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Le variabili di hello in cui sono definite come segue:

| Variabile | Valore |
| --- | --- |
| \[DirectoryName\] |Hello sottodirectory nella directory di progetto hello radice che contiene il file con estensione csdef hello di hello progetto Azure. |
| \[ServiceDefinition\] |nome Hello del file di definizione del servizio hello. Per impostazione predefinita, il file è denominato ServiceDefinition.csdef. |
| \[OutputFileName\] |nome Hello per hello ha generato il file di pacchetto. In genere, viene impostato toohello nome di un'applicazione hello. Se viene specificato alcun nome di file, il pacchetto di applicazione hello viene creato come \[ApplicationName\]con estensione cspkg. |
| \[RoleName\] |nome Hello del ruolo di hello come definito nel file di definizione del servizio hello. |
| \[RoleBinariesDirectory] |percorso di Hello dei file binari di hello per ruolo hello. |
| \[VirtualPath\] |directory fisiche di Hello per ogni percorso virtuale definito nella sezione Sites hello della definizione di servizio hello. |
| \[PhysicalPath\] |Hello directory fisiche del contenuto di hello per ogni percorso virtuale definito nel nodo di sito hello della definizione del servizio hello. |
| \[RoleAssemblyName\] |nome Hello del file binario di hello per ruolo hello. |

## <a name="next-steps"></a>Passaggi successivi
Si sta creando un pacchetto del servizio cloud e si vuole...

* [Configurare il desktop remoto per un'istanza del servizio cloud][remotedesktop]
* [Distribuire un progetto di servizio cloud][deploy]

Si sta usando Visual Studio e si vuole...

* [Creare un nuovo servizio cloud][vs_create]
* [Riconfigurare un servizio cloud esistente][vs_reconfigure]
* [Distribuire un progetto di servizio cloud][vs_deploy]
* [Configurare il desktop remoto per un'istanza del servizio cloud][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
