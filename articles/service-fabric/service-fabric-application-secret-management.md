---
title: Gestione dei segreti nelle applicazioni di Service Fabric | Microsoft Docs
description: Questo articolo descrive come proteggere i valori dei segreti in un'applicazione di Service Fabric.
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
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="1bea6-103">Gestione dei segreti nelle applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1bea6-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="1bea6-104">Questa guida descrive la procedura di gestione dei segreti in un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1bea6-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="1bea6-105">I segreti possono essere informazioni riservate, ad esempio le stringhe di connessione di archiviazione, le password o altri valori che non devono essere gestiti in testo normale.</span><span class="sxs-lookup"><span data-stu-id="1bea6-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="1bea6-106">Questa guida usa l'insieme di credenziali delle chiavi di Azure per gestire chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="1bea6-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="1bea6-107">Tuttavia, l' *uso* di segreti in un'applicazione è indipendente dalla piattaforma cloud per consentire alle applicazioni di essere distribuite in un cluster ospitato in un punto qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="1bea6-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="1bea6-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1bea6-108">Overview</span></span>
<span data-ttu-id="1bea6-109">Il metodo consigliato per gestire le impostazioni di configurazione del servizio è tramite i [pacchetti di configurazione del servizio][config-package].</span><span class="sxs-lookup"><span data-stu-id="1bea6-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="1bea6-110">I pacchetti di configurazione dispongono di controllo delle versioni e sono aggiornabili tramite gli aggiornamenti in sequenza gestiti con convalida dell'integrità e rollback automatico.</span><span class="sxs-lookup"><span data-stu-id="1bea6-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="1bea6-111">Questo approccio è da preferire alla configurazione globale in quanto riduce le probabilità di un'interruzione del servizio globale.</span><span class="sxs-lookup"><span data-stu-id="1bea6-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="1bea6-112">I segreti crittografati non rappresentano un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="1bea6-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="1bea6-113">Service Fabric offre funzionalità incorporate per crittografare e decrittografare i valori in un file Settings.xml del pacchetto configurazione tramite la crittografia del certificato.</span><span class="sxs-lookup"><span data-stu-id="1bea6-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="1bea6-114">Il diagramma seguente illustra il flusso di base per la gestione dei segreti in un'applicazione di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="1bea6-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![panoramica della gestione dei segreti][overview]

<span data-ttu-id="1bea6-116">In questo flusso sono presenti quattro passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="1bea6-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="1bea6-117">Ottenere un certificato di crittografia dei dati.</span><span class="sxs-lookup"><span data-stu-id="1bea6-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="1bea6-118">Installare il certificato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1bea6-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="1bea6-119">Crittografare i valori dei segreti quando si distribuisce un'applicazione con il certificato e inserirli nel file di configurazione Settings.xml del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bea6-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="1bea6-120">Leggere i valori crittografati risultati da Settings. XML eseguendo la decrittografia con lo stesso certificato di crittografia.</span><span class="sxs-lookup"><span data-stu-id="1bea6-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="1bea6-121">[Azure Key Vault][key-vault-get-started] viene usato come percorso di archiviazione sicuro per i certificati e come un modo per ottenere i certificati installati nei cluster Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="1bea6-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="1bea6-122">Se non si esegue la distribuzione in Azure, non è necessario usare l'insieme di credenziali delle chiavi per gestire i segreti nelle applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1bea6-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="1bea6-123">Certificato di crittografia dei dati</span><span class="sxs-lookup"><span data-stu-id="1bea6-123">Data encipherment certificate</span></span>
<span data-ttu-id="1bea6-124">Il certificato di crittografia dei dati viene usato esclusivamente per la crittografia e decrittografia dei valori di configurazione del file Settings.xml del servizio e non viene impiegato per l'autenticazione o la firma di testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="1bea6-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="1bea6-125">Il certificato deve soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bea6-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="1bea6-126">Il certificato deve includere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="1bea6-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="1bea6-127">Il certificato deve essere stato creato per lo scambio di chiave, esportabile in un file con estensione pfx (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="1bea6-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="1bea6-128">L'uso delle chiavi del certificato deve includere la crittografia dei dati (10) e non deve includere l'autenticazione del server o del client.</span><span class="sxs-lookup"><span data-stu-id="1bea6-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="1bea6-129">Ad esempio, quando si crea un certificato autofirmato tramite PowerShell, il flag `KeyUsage` deve essere impostato su `DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="1bea6-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="1bea6-130">Installare il certificato nel cluster</span><span class="sxs-lookup"><span data-stu-id="1bea6-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="1bea6-131">Questo certificato deve essere installato su ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="1bea6-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="1bea6-132">Verrà usato in fase di esecuzione per decrittografare i valori archiviati in nel file Settings.xml del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bea6-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="1bea6-133">Per le istruzioni di installazione, vedere l'articolo che spiega [come creare un cluster con Azure Resource Manager][service-fabric-cluster-creation-via-arm].</span><span class="sxs-lookup"><span data-stu-id="1bea6-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="1bea6-134">Eseguire la crittografia dei segreti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1bea6-134">Encrypt application secrets</span></span>
<span data-ttu-id="1bea6-135">L'SDK di Service Fabric ha funzioni di crittografia e decrittografia dei segreti predefinite.</span><span class="sxs-lookup"><span data-stu-id="1bea6-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="1bea6-136">I valori dei segreti possono essere crittografati in fase di compilazione e quindi decrittografati e letti a livello di programmazione nel codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bea6-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="1bea6-137">Il comando PowerShell seguente viene usato per crittografare un segreto.</span><span class="sxs-lookup"><span data-stu-id="1bea6-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="1bea6-138">Questo comando consente unicamente di crittografare il valore e **non** firma il testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="1bea6-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="1bea6-139">È necessario usare lo stesso certificato di crittografia installato nel cluster per produrre il testo crittografato per i valori del segreto:</span><span class="sxs-lookup"><span data-stu-id="1bea6-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="1bea6-140">La stringa Base 64 risultante contiene sia il testo crittografato dei segreti che le informazioni relative al certificato usato per crittografarlo.</span><span class="sxs-lookup"><span data-stu-id="1bea6-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="1bea6-141">La stringa con codifica Base 64 può essere inserita in un parametro nel file di configurazione Settings.xml del servizio con l'attributo `IsEncrypted` impostato su `true`:</span><span class="sxs-lookup"><span data-stu-id="1bea6-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="1bea6-142">Inserire i segreti dell'applicazione nelle istanze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1bea6-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="1bea6-143">Idealmente, la distribuzione in ambienti diversi dovrebbe essere il più possibile automatizzata.</span><span class="sxs-lookup"><span data-stu-id="1bea6-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="1bea6-144">Questo può essere ottenuto tramite l'esecuzione della crittografia dei segreti in un ambiente di compilazione e l'uso dei segreti crittografati come parametri durante la creazione delle istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bea6-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="1bea6-145">Usare parametri sostituibili in Settings.xml</span><span class="sxs-lookup"><span data-stu-id="1bea6-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="1bea6-146">Il file di configurazione Settings.xml consente di usare parametri sostituibili che possono essere forniti al momento della creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bea6-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="1bea6-147">Usare l'attributo `MustOverride` invece di fornire un valore per un parametro:</span><span class="sxs-lookup"><span data-stu-id="1bea6-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="1bea6-148">Per sostituire i valori in Settings.xml, dichiarare un parametro di sostituzione per il servizio in ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="1bea6-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="1bea6-149">A questo punto, il valore può essere specificato come un *parametro dell'applicazione* quando si crea un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bea6-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="1bea6-150">La creazione di un'istanza dell'applicazione può generare uno script con PowerShell o essere scritta in C#, per semplificare l'integrazione in un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1bea6-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="1bea6-151">Tramite PowerShell, viene fornito il parametro del comando `New-ServiceFabricApplication` come [tabella hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="1bea6-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="1bea6-152">Tramite C#, i parametri dell'applicazione vengono specificati in `ApplicationDescription` come `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="1bea6-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="1bea6-153">Decrittografare i segreti dal codice del servizio</span><span class="sxs-lookup"><span data-stu-id="1bea6-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="1bea6-154">I servizi di Service Fabric vengono eseguiti in NETWORK SERVICE per impostazione predefinita su Windows e non hanno accesso ai certificati installati nel nodo senza un'impostazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="1bea6-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="1bea6-155">Quando si usa un certificato di crittografia dati, è necessario assicurarsi che NETWORK SERVICE o qualsiasi account utente sia in esecuzione nel servizio disponga dell'accesso alla chiave privata del certificato.</span><span class="sxs-lookup"><span data-stu-id="1bea6-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="1bea6-156">Service Fabric gestirà automaticamente la concessione dell'accesso per il servizio se viene configurato a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="1bea6-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="1bea6-157">Questa configurazione può essere eseguita in ApplicationManifest definendo utenti e criteri di protezione per i certificati.</span><span class="sxs-lookup"><span data-stu-id="1bea6-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="1bea6-158">Nell'esempio seguente, all'account NETWORK SERVICE viene concesso l'accesso in lettura a un certificato definito dalla relativa identificazione personale:</span><span class="sxs-lookup"><span data-stu-id="1bea6-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="1bea6-159">Quando si copia un'identificazione personale di un certificato dallo snap-in dell'archivio dei certificati su Windows, viene inserito un carattere invisibile all'inizio della stringa di identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="1bea6-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="1bea6-160">Questo carattere invisibile può causare un errore durante il tentativo di individuare un certificato tramite identificazione personale. Accertarsi di eliminare questo carattere aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="1bea6-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="1bea6-161">Usare i segreti dell'applicazione nel codice del servizio</span><span class="sxs-lookup"><span data-stu-id="1bea6-161">Use application secrets in service code</span></span>
<span data-ttu-id="1bea6-162">L'API per accedere ai valori di configurazione da Settings.xml in un pacchetto di configurazione consente di decrittografare facilmente i valori con l'attributo `IsEncrypted` impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="1bea6-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="1bea6-163">Poiché il testo crittografato contiene informazioni sul certificato usato per la crittografia, non è necessario individuare manualmente il certificato.</span><span class="sxs-lookup"><span data-stu-id="1bea6-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="1bea6-164">Il certificato deve essere solo installato sul nodo su cui è in esecuzione il servizio.</span><span class="sxs-lookup"><span data-stu-id="1bea6-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="1bea6-165">È sufficiente chiamare il metodo `DecryptValue()` per recuperare il valore del segreto originale:</span><span class="sxs-lookup"><span data-stu-id="1bea6-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="1bea6-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bea6-166">Next Steps</span></span>
<span data-ttu-id="1bea6-167">Altre informazioni sull' [esecuzione di applicazioni con autorizzazioni di sicurezza diverse](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="1bea6-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
