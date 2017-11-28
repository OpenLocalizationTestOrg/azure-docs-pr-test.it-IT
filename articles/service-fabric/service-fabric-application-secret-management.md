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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="6305b-103">Gestione dei segreti nelle applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6305b-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="6305b-104">Questa guida vengono illustrati i passaggi hello della gestione delle informazioni riservate in un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6305b-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="6305b-105">I segreti possono essere informazioni riservate, ad esempio le stringhe di connessione di archiviazione, le password o altri valori che non devono essere gestiti in testo normale.</span><span class="sxs-lookup"><span data-stu-id="6305b-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="6305b-106">Questa Guida Usa i segreti e le chiavi toomanage insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="6305b-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="6305b-107">Tuttavia, *utilizzando* i segreti in un'applicazione è ospitato sul cluster di cloud tooallow indipendente dalla piattaforma applicazioni toobe tooa distribuito ovunque.</span><span class="sxs-lookup"><span data-stu-id="6305b-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="6305b-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6305b-108">Overview</span></span>
<span data-ttu-id="6305b-109">Hello impostazioni di configurazione servizio toomanage consigliato consiste nell'utilizzare [pacchetti di configurazione del servizio][config-package].</span><span class="sxs-lookup"><span data-stu-id="6305b-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="6305b-110">I pacchetti di configurazione dispongono di controllo delle versioni e sono aggiornabili tramite gli aggiornamenti in sequenza gestiti con convalida dell'integrità e rollback automatico.</span><span class="sxs-lookup"><span data-stu-id="6305b-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="6305b-111">Si tratta di Preferiti tooglobal configurazione poiché riduce il possibilità di hello di un'interruzione del servizio globale.</span><span class="sxs-lookup"><span data-stu-id="6305b-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="6305b-112">I segreti crittografati non rappresentano un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="6305b-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="6305b-113">Service Fabric offre funzionalità incorporate per crittografare e decrittografare i valori in un file Settings.xml del pacchetto configurazione tramite la crittografia del certificato.</span><span class="sxs-lookup"><span data-stu-id="6305b-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="6305b-114">Hello seguente diagramma illustra flusso di base per la gestione segreto in un'applicazione di Service Fabric hello:</span><span class="sxs-lookup"><span data-stu-id="6305b-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![panoramica della gestione dei segreti][overview]

<span data-ttu-id="6305b-116">In questo flusso sono presenti quattro passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="6305b-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="6305b-117">Ottenere un certificato di crittografia dei dati.</span><span class="sxs-lookup"><span data-stu-id="6305b-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="6305b-118">Installare il certificato di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="6305b-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="6305b-119">Crittografare i valori dei segreti quando si distribuisce un'applicazione con certificato hello e li inserisce nel file di configurazione di un servizio Settings.</span><span class="sxs-lookup"><span data-stu-id="6305b-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="6305b-120">I valori di lettura crittografato fuori Settings decrittografando con hello stesso certificato di crittografia.</span><span class="sxs-lookup"><span data-stu-id="6305b-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="6305b-121">[Insieme di credenziali chiave di Azure] [ key-vault-get-started] è qui utilizzato come un percorso di archiviazione sicura per i certificati e come un modo tooget certificati installati nel cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="6305b-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="6305b-122">Se non si sta distribuendo tooAzure, i segreti toomanage insieme di credenziali chiave di toouse nelle applicazioni di Service Fabric non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="6305b-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="6305b-123">Certificato di crittografia dei dati</span><span class="sxs-lookup"><span data-stu-id="6305b-123">Data encipherment certificate</span></span>
<span data-ttu-id="6305b-124">Il certificato di crittografia dei dati viene usato esclusivamente per la crittografia e decrittografia dei valori di configurazione del file Settings.xml del servizio e non viene impiegato per l'autenticazione o la firma di testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="6305b-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="6305b-125">certificato Hello deve soddisfare i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="6305b-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="6305b-126">certificato di Hello deve contenere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="6305b-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="6305b-127">Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).</span><span class="sxs-lookup"><span data-stu-id="6305b-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="6305b-128">utilizzo dei certificati chiave Hello deve includere la crittografia dei dati (10) e non deve includere l'autenticazione Server o l'autenticazione Client.</span><span class="sxs-lookup"><span data-stu-id="6305b-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="6305b-129">Ad esempio, quando si crea un certificato autofirmato usando PowerShell, hello `KeyUsage` flag deve essere impostato troppo`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="6305b-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="6305b-130">Installare il certificato di hello del cluster</span><span class="sxs-lookup"><span data-stu-id="6305b-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="6305b-131">Questo certificato deve essere installato in ogni nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6305b-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="6305b-132">Verrà utilizzato runtime toodecrypt valori archiviati nel file Settings.xml di un servizio.</span><span class="sxs-lookup"><span data-stu-id="6305b-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="6305b-133">Vedere [come un cluster usando Gestione risorse di Azure toocreate] [ service-fabric-cluster-creation-via-arm] per le istruzioni di installazione.</span><span class="sxs-lookup"><span data-stu-id="6305b-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="6305b-134">Eseguire la crittografia dei segreti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6305b-134">Encrypt application secrets</span></span>
<span data-ttu-id="6305b-135">Hello Service Fabric SDK ha funzioni di crittografia e decrittografia secret predefinite.</span><span class="sxs-lookup"><span data-stu-id="6305b-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="6305b-136">I valori dei segreti possono essere crittografati in fase di compilazione e quindi decrittografati e letti a livello di programmazione nel codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="6305b-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="6305b-137">il comando PowerShell seguente Hello è tooencrypt usato un segreto.</span><span class="sxs-lookup"><span data-stu-id="6305b-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="6305b-138">Questo comando consente di crittografare solo il valore di hello. caso **non** firmare testo crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="6305b-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="6305b-139">È necessario utilizzare hello stesso certificato di crittografia che viene installato nel testo crittografato tooproduce cluster per i valori dei segreti:</span><span class="sxs-lookup"><span data-stu-id="6305b-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="6305b-140">Hello stringa base 64 risultante contiene testo crittografato secret hello nonché a informazioni sul certificato hello che è stato utilizzato tooencrypt è.</span><span class="sxs-lookup"><span data-stu-id="6305b-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="6305b-141">Hello stringa con codifica base 64 può essere inserita in un parametro nel file di configurazione del servizio Settings con hello `IsEncrypted` attributo impostato troppo`true`:</span><span class="sxs-lookup"><span data-stu-id="6305b-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="6305b-142">Inserire i segreti dell'applicazione nelle istanze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6305b-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="6305b-143">In teoria, ambienti di distribuzione toodifferent devono essere automatizzati come possibile.</span><span class="sxs-lookup"><span data-stu-id="6305b-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="6305b-144">Questa operazione può essere eseguita esegue la crittografia segreta in un ambiente di compilazione e fornendo i segreti crittografato hello come parametri durante la creazione di istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6305b-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="6305b-145">Usare parametri sostituibili in Settings.xml</span><span class="sxs-lookup"><span data-stu-id="6305b-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="6305b-146">file di configurazione di Hello Settings consente parametri sostituibili che possono essere forniti al momento della creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6305b-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="6305b-147">Hello utilizzare `MustOverride` attributo invece di fornire un valore per un parametro:</span><span class="sxs-lookup"><span data-stu-id="6305b-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="6305b-148">i valori toooverride nel file Settings.xml, dichiarare un parametro di sostituzione per il servizio di hello in ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="6305b-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="6305b-149">Ora hello valore può essere specificato come un *parametro applicazione* durante la creazione di un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6305b-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="6305b-150">La creazione di un'istanza dell'applicazione può generare uno script con PowerShell o essere scritta in C#, per semplificare l'integrazione in un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6305b-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="6305b-151">Tramite PowerShell, il parametro hello è fornito toohello `New-ServiceFabricApplication` comando come un [tabella hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="6305b-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="6305b-152">Tramite C#, i parametri dell'applicazione vengono specificati in `ApplicationDescription` come `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="6305b-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="6305b-153">Decrittografare i segreti dal codice del servizio</span><span class="sxs-lookup"><span data-stu-id="6305b-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="6305b-154">Servizi di Service Fabric eseguiti nel servizio di rete per impostazione predefinita in Windows e non installato nel nodo hello senza un'ulteriore impostazione toocertificates di accesso.</span><span class="sxs-lookup"><span data-stu-id="6305b-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="6305b-155">Quando si utilizza un certificato di crittografia di dati, è necessario che il servizio di rete o è in esecuzione il servizio di hello account utente disponga di chiave privata del certificato di accesso toohello toomake.</span><span class="sxs-lookup"><span data-stu-id="6305b-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="6305b-156">Service Fabric gestirà la concessione dell'accesso per il servizio automaticamente se è configurarlo toodo così.</span><span class="sxs-lookup"><span data-stu-id="6305b-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="6305b-157">Questa configurazione può essere eseguita in ApplicationManifest definendo utenti e criteri di protezione per i certificati.</span><span class="sxs-lookup"><span data-stu-id="6305b-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="6305b-158">Nell'esempio seguente di hello, hello account servizio di rete viene assegnato l'accesso in lettura tooa certificato definito dalla relativa identificazione personale:</span><span class="sxs-lookup"><span data-stu-id="6305b-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="6305b-159">Quando si copia un'identificazione personale del certificato dal certificato hello archiviare snap-in di Windows, un carattere invisibile viene posizionato all'inizio di hello della stringa di identificazione personale hello.</span><span class="sxs-lookup"><span data-stu-id="6305b-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="6305b-160">Questo carattere invisibile può provocare un errore durante il tentativo di toolocate un certificato con identificazione personale, pertanto è necessario che toodelete questo carattere aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="6305b-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="6305b-161">Usare i segreti dell'applicazione nel codice del servizio</span><span class="sxs-lookup"><span data-stu-id="6305b-161">Use application secrets in service code</span></span>
<span data-ttu-id="6305b-162">Consente di Hello API per l'accesso ai valori di configurazione da Settings in un pacchetto di configurazione per la decrittografia semplice di valori hello `IsEncrypted` attributo impostato troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="6305b-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="6305b-163">Poiché il testo crittografato hello contiene informazioni sul certificato hello utilizzato per la crittografia, certificati di hello toomanually trova non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="6305b-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="6305b-164">certificato Hello deve semplicemente toobe installato nel nodo hello hello servizio sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6305b-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="6305b-165">È sufficiente chiamare hello `DecryptValue()` tooretrieve hello originale secret valore del metodo:</span><span class="sxs-lookup"><span data-stu-id="6305b-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="6305b-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6305b-166">Next Steps</span></span>
<span data-ttu-id="6305b-167">Altre informazioni sull' [esecuzione di applicazioni con autorizzazioni di sicurezza diverse](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="6305b-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
