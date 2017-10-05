---
title: Sicurezza del contenitore di Azure Service Fabric | Microsoft Docs
description: Informazioni su come proteggere i servizi del contenitore.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a>Sicurezza del contenitore

Service Fabric fornisce un meccanismo per i servizi all'interno di un contenitore per accedere a un certificato che viene installato nei nodi in un cluster di Windows o Linux (versione 5.7 o versioni successive). Service Fabric supporta anche gMSA (account del servizio gestito del gruppo) per i contenitori di Windows. 

## <a name="certificate-management-for-containers"></a>Gestione dei certificati per i contenitori

È possibile proteggere i servizi del contenitore specificando un certificato. Questo certificato deve essere installato sui nodi del cluster. Le informazioni del certificato vengono fornite nel manifesto dell'applicazione sotto il tag `ContainerHostPolicies` come illustrato nel frammento di codice seguente:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

All'avvio dell'applicazione, il runtime legge i certificati e genera un file PFX e una password per ogni certificato. Il file PFX e la password sono accessibili all'interno del contenitore usando le variabili di ambiente seguenti: 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

Il servizio del contenitore o del processo è responsabile dell'importazione del file PFX nel contenitore. Per importare il certificato, è possibile usare gli script `setupentrypoint.sh` o il codice personalizzato in esecuzione all'interno del processo del contenitore. Codice di esempio in C# per l'importazione del file PFX seguente:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Questo certificato PFX può essere usato per autenticare l'applicazione o il servizio o per proteggere la comunicazione con altri servizi.


## <a name="set-up-gmsa-for-windows-containers"></a>Configurare gMSA per i contenitori di Windows

Per configurare gMSA (account del servizio gestito del gruppo), un file di specifica delle credenziali (`credspec`) viene posizionato in tutti i nodi del cluster. Il file può essere copiato in tutti i nodi tramite un'estensione della macchina virtuale.  Il file `credspec` deve contenere le informazioni dell'account gMSA. Per altre informazioni sul file `credspec`, vedere [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts) (Account del servizio). La specifica della credenziale e il tag `Hostname` vengono specificati nel manifesto dell'applicazione. Il tag `Hostname` deve corrispondere al nome dell'account gMSA in cui viene eseguito il contenitore.  Il tag `Hostname` consente al contenitore di autenticarsi presso altri servizi nel dominio tramite l'autenticazione Kerberos.  Un esempio per specificare `Hostname` e `credspec` nel manifesto dell'applicazione è illustrato nel frammento seguente:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Passaggi successivi

* [Distribuire un contenitore Windows in Service Fabric su Windows Server 2016](service-fabric-get-started-containers.md)
* [Distribuire un contenitore Docker in Service Fabric su Linux](service-fabric-get-started-containers-linux.md)
