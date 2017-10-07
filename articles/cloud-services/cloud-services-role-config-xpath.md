---
title: il foglio informativo XPath di aaaCloud ruolo Servizi file config | Documenti Microsoft
description: "Hello varie impostazioni di XPath, che è possibile utilizzare nelle impostazioni del cloud servizio ruolo configurazione tooexpose hello come una variabile di ambiente."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Esporre le impostazioni di configurazione del ruolo come una variabile di ambiente con XPath
Lavoro del servizio cloud di hello o file di definizione del servizio di ruolo web, è possibile esporre i valori di configurazione di runtime come variabili di ambiente. Hello valori XPath seguenti è supportato (che corrispondono a valori tooAPI).

Questi valori XPath sono disponibili anche tramite hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) libreria. 

## <a name="app-running-in-emulator"></a>App in esecuzione nell'emulatore
Indica che app hello è in esecuzione nell'emulatore hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| Codice |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>ID distribuzione
Recupera l'ID distribuzione hello per istanza hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| Codice |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>ID ruolo
Recupera l'ID del ruolo per l'istanza di hello corrente hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| Codice |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Aggiornamento dominio
Recupera il dominio di aggiornamento hello dell'istanza di hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| Codice |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Dominio di errore
Recupera il dominio di errore hello dell'istanza di hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| Codice |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Nome del ruolo
Recupera il nome del ruolo hello di istanze di hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| Codice |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Impostazione di configurazione
Impostazione di configurazione specificato il valore hello recupera hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| Codice |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Percorso di archiviazione locale
Recupera il percorso di archiviazione locale hello per istanza hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| Codice |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>Dimensioni di archiviazione locale
Recupera la dimensione hello di archiviazione locale di hello per istanza hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| Codice |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Protocollo di endpoint
Recupera il protocollo di endpoint hello per istanza hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| Codice |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>IP dell'endpoint
Ottiene hello specificato l'indirizzo IP dell'endpoint.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| Codice |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>Porta dell'endpoint
Recupera una porta dell'endpoint per l'istanza di hello hello.

| Tipo | Esempio |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| Codice |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>Esempio
Di seguito è riportato un esempio di un ruolo di lavoro che crea un'attività di avvio con una variabile di ambiente denominata `TestIsEmulated` impostare toohello [ @emulated valore xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [ServiceConfiguration. cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.

Creare un pacchetto [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .

Abilitare [Desktop remoto](cloud-services-role-enable-remote-desktop.md) per un ruolo.

