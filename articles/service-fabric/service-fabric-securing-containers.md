---
title: sicurezza di Service Fabric contenitore aaaAzure | Documenti Microsoft
description: Informazioni su toosecure ora i servizi di contenitore.
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
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Sicurezza del contenitore

Service Fabric fornisce un meccanismo per i servizi all'interno di un contenitore di tooaccess un certificato installato nei nodi hello in un cluster di Windows o Linux (versione 5.7 o versioni successive). Service Fabric supporta anche gMSA (account del servizio gestito del gruppo) per i contenitori di Windows. 

## <a name="certificate-management-for-containers"></a>Gestione dei certificati per i contenitori

È possibile proteggere i servizi del contenitore specificando un certificato. Hello certificato deve essere installato sui nodi del cluster hello hello. Hello informazioni del certificato viene fornite nel manifesto dell'applicazione hello in hello `ContainerHostPolicies` tag come hello seguente mostra:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Quando si avvia un'applicazione hello, hello runtime legge certificati hello e genera un file PFX e una password per ogni certificato. Il file PFX e la password sono accessibili nel contenitore hello utilizzando hello seguenti variabili di ambiente: 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

il servizio di contenitore Hello o un processo è responsabile per l'importazione di file PFX hello in contenitore hello. certificato di hello tooimport, è possibile utilizzare `setupentrypoint.sh` script o codice personalizzato all'interno di processo del contenitore hello eseguita. Codice di esempio in c# per l'importazione di file PFX hello segue:

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
Questo certificato PFX può essere utilizzato per autenticare un'applicazione hello o servizio oppure commmunication sicuro con altri servizi.


## <a name="set-up-gmsa-for-windows-containers"></a>Configurare gMSA per i contenitori di Windows

tooset backup gMSA (group Managed Service Accounts), un file di specifica delle credenziali (`credspec`) viene inserito in tutti i nodi del cluster di hello. file Hello può essere copiati in tutti i nodi utilizzando un'estensione della macchina virtuale.  Hello `credspec` file deve contenere le informazioni di account gMSA hello. Per ulteriori informazioni su hello `credspec` file, vedere [gli account del servizio](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Specifica credenziali Hello e hello `Hostname` tag specificati nel manifesto dell'applicazione hello. Hello `Hostname` tag deve corrispondere a nome di account gMSA hello che hello contenitore viene eseguito in.  Hello `Hostname` tag consente hello contenitore tooauthenticate stesso tooother servizi nel dominio hello mediante l'autenticazione Kerberos.  Un esempio per la specifica di hello `Hostname` hello e `credspec` in hello manifesto dell'applicazione è illustrato nel seguente frammento di codice hello:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Passaggi successivi

* [Distribuire un tooService di contenitore di Windows Fabric in Windows Server 2016](service-fabric-get-started-containers.md)
* [Distribuire un tooService contenitore Docker dell'infrastruttura in Linux](service-fabric-get-started-containers-linux.md)
