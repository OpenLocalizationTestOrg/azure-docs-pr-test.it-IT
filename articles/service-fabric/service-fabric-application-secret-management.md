---
title: i segreti aaaManaging nelle applicazioni di Service Fabric | Documenti Microsoft
description: In questo articolo viene descritto come segreto toosecure valori in un'applicazione di Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Gestione dei segreti nelle applicazioni di Service Fabric
Questa guida vengono illustrati i passaggi hello della gestione delle informazioni riservate in un'applicazione di Service Fabric. I segreti possono essere informazioni riservate, ad esempio le stringhe di connessione di archiviazione, le password o altri valori che non devono essere gestiti in testo normale.

Questa Guida Usa i segreti e le chiavi toomanage insieme credenziali chiavi Azure. Tuttavia, *utilizzando* i segreti in un'applicazione è ospitato sul cluster di cloud tooallow indipendente dalla piattaforma applicazioni toobe tooa distribuito ovunque. 

## <a name="overview"></a>Panoramica
Hello impostazioni di configurazione servizio toomanage consigliato consiste nell'utilizzare [pacchetti di configurazione del servizio][config-package]. I pacchetti di configurazione dispongono di controllo delle versioni e sono aggiornabili tramite gli aggiornamenti in sequenza gestiti con convalida dell'integrità e rollback automatico. Si tratta di Preferiti tooglobal configurazione poiché riduce il possibilità di hello di un'interruzione del servizio globale. I segreti crittografati non rappresentano un'eccezione. Service Fabric offre funzionalità incorporate per crittografare e decrittografare i valori in un file Settings.xml del pacchetto configurazione tramite la crittografia del certificato.

Hello seguente diagramma illustra flusso di base per la gestione segreto in un'applicazione di Service Fabric hello:

![panoramica della gestione dei segreti][overview]

In questo flusso sono presenti quattro passaggi principali:

1. Ottenere un certificato di crittografia dei dati.
2. Installare il certificato di hello del cluster.
3. Crittografare i valori dei segreti quando si distribuisce un'applicazione con certificato hello e li inserisce nel file di configurazione di un servizio Settings.
4. I valori di lettura crittografato fuori Settings decrittografando con hello stesso certificato di crittografia. 

[Insieme di credenziali chiave di Azure] [ key-vault-get-started] è qui utilizzato come un percorso di archiviazione sicura per i certificati e come un modo tooget certificati installati nel cluster di Service Fabric in Azure. Se non si sta distribuendo tooAzure, i segreti toomanage insieme di credenziali chiave di toouse nelle applicazioni di Service Fabric non è necessaria.

## <a name="data-encipherment-certificate"></a>Certificato di crittografia dei dati
Il certificato di crittografia dei dati viene usato esclusivamente per la crittografia e decrittografia dei valori di configurazione del file Settings.xml del servizio e non viene impiegato per l'autenticazione o la firma di testo crittografato. certificato Hello deve soddisfare i seguenti requisiti hello:

* certificato di Hello deve contenere una chiave privata.
* Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).
* utilizzo dei certificati chiave Hello deve includere la crittografia dei dati (10) e non deve includere l'autenticazione Server o l'autenticazione Client. 
  
  Ad esempio, quando si crea un certificato autofirmato usando PowerShell, hello `KeyUsage` flag deve essere impostato troppo`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Installare il certificato di hello del cluster
Questo certificato deve essere installato in ogni nodo cluster hello. Verrà utilizzato runtime toodecrypt valori archiviati nel file Settings.xml di un servizio. Vedere [come un cluster usando Gestione risorse di Azure toocreate] [ service-fabric-cluster-creation-via-arm] per le istruzioni di installazione. 

## <a name="encrypt-application-secrets"></a>Eseguire la crittografia dei segreti dell'applicazione
Hello Service Fabric SDK ha funzioni di crittografia e decrittografia secret predefinite. I valori dei segreti possono essere crittografati in fase di compilazione e quindi decrittografati e letti a livello di programmazione nel codice del servizio. 

il comando PowerShell seguente Hello è tooencrypt usato un segreto. Questo comando consente di crittografare solo il valore di hello. caso **non** firmare testo crittografato hello. È necessario utilizzare hello stesso certificato di crittografia che viene installato nel testo crittografato tooproduce cluster per i valori dei segreti:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Hello stringa base 64 risultante contiene testo crittografato secret hello nonché a informazioni sul certificato hello che è stato utilizzato tooencrypt è.  Hello stringa con codifica base 64 può essere inserita in un parametro nel file di configurazione del servizio Settings con hello `IsEncrypted` attributo impostato troppo`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Inserire i segreti dell'applicazione nelle istanze dell'applicazione
In teoria, ambienti di distribuzione toodifferent devono essere automatizzati come possibile. Questa operazione può essere eseguita esegue la crittografia segreta in un ambiente di compilazione e fornendo i segreti crittografato hello come parametri durante la creazione di istanze dell'applicazione.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Usare parametri sostituibili in Settings.xml
file di configurazione di Hello Settings consente parametri sostituibili che possono essere forniti al momento della creazione dell'applicazione. Hello utilizzare `MustOverride` attributo invece di fornire un valore per un parametro:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

i valori toooverride nel file Settings.xml, dichiarare un parametro di sostituzione per il servizio di hello in ApplicationManifest.xml:

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Ora hello valore può essere specificato come un *parametro applicazione* durante la creazione di un'istanza di un'applicazione hello. La creazione di un'istanza dell'applicazione può generare uno script con PowerShell o essere scritta in C#, per semplificare l'integrazione in un processo di compilazione.

Tramite PowerShell, il parametro hello è fornito toohello `New-ServiceFabricApplication` comando come un [tabella hash](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Tramite C#, i parametri dell'applicazione vengono specificati in `ApplicationDescription` come `NameValueCollection`:

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Decrittografare i segreti dal codice del servizio
Servizi di Service Fabric eseguiti nel servizio di rete per impostazione predefinita in Windows e non installato nel nodo hello senza un'ulteriore impostazione toocertificates di accesso.

Quando si utilizza un certificato di crittografia di dati, è necessario che il servizio di rete o è in esecuzione il servizio di hello account utente disponga di chiave privata del certificato di accesso toohello toomake. Service Fabric gestirà la concessione dell'accesso per il servizio automaticamente se è configurarlo toodo così. Questa configurazione può essere eseguita in ApplicationManifest definendo utenti e criteri di protezione per i certificati. Nell'esempio seguente di hello, hello account servizio di rete viene assegnato l'accesso in lettura tooa certificato definito dalla relativa identificazione personale:

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> Quando si copia un'identificazione personale del certificato dal certificato hello archiviare snap-in di Windows, un carattere invisibile viene posizionato all'inizio di hello della stringa di identificazione personale hello. Questo carattere invisibile può provocare un errore durante il tentativo di toolocate un certificato con identificazione personale, pertanto è necessario che toodelete questo carattere aggiuntivo.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Usare i segreti dell'applicazione nel codice del servizio
Consente di Hello API per l'accesso ai valori di configurazione da Settings in un pacchetto di configurazione per la decrittografia semplice di valori hello `IsEncrypted` attributo impostato troppo`true`. Poiché il testo crittografato hello contiene informazioni sul certificato hello utilizzato per la crittografia, certificati di hello toomanually trova non è necessaria. certificato Hello deve semplicemente toobe installato nel nodo hello hello servizio sia in esecuzione. È sufficiente chiamare hello `DecryptValue()` tooretrieve hello originale secret valore del metodo:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sull' [esecuzione di applicazioni con autorizzazioni di sicurezza diverse](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
