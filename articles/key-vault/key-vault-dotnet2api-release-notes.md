---
title: Note sulla versione dell'API .NET 2.x per l'insieme di credenziali delle chiavi | Microsoft Docs
description: Gli sviluppatori .NET useranno questa API per scrivere il codice dell'insieme di credenziali delle chiavi di Azure
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="bad4e-103">Guida alla migrazione e note sulla versione .NET 2.0 per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="bad4e-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="bad4e-104">Le note e le linee guida seguenti sono destinate agli sviluppatori che usano la libreria .NET / C# di Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bad4e-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="bad4e-105">Nel passaggio dalla versione 1.0 alla versione 2.0 sono state apportate alcune modifiche. Per poter però usufruire dei miglioramenti funzionali e delle nuove funzionalità, ad esempio la funzionalità **Certificati Key Vault**, è necessaria un'operazione di migrazione nel codice.</span><span class="sxs-lookup"><span data-stu-id="bad4e-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="bad4e-106">Certificati Key Vault</span><span class="sxs-lookup"><span data-stu-id="bad4e-106">Key Vault certificates</span></span>

<span data-ttu-id="bad4e-107">La funzionalità Certificati dell'insieme di credenziali delle chiavi supporta la gestione di certificati X509 e consente di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bad4e-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="bad4e-108">Il proprietario di un certificato può creare un certificato tramite un processo di creazione dell'insieme di credenziali delle chiavi o tramite l'importazione di un certificato esistente.</span><span class="sxs-lookup"><span data-stu-id="bad4e-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="bad4e-109">Sono inclusi i certificati autofirmati e i certificati generati dall'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="bad4e-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="bad4e-110">Il proprietario di un certificato dell'insieme di credenziali delle chiavi può implementare l'archiviazione sicura e la gestione di certificati X509 senza interagire con materiale della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="bad4e-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="bad4e-111">Il proprietario di un certificato può creare criteri che guidano l'insieme di credenziali delle chiavi nella gestione del ciclo di vita di un certificato.</span><span class="sxs-lookup"><span data-stu-id="bad4e-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="bad4e-112">I proprietari di un certificato possono specificare informazioni sul contatto per notificare eventi sul ciclo di vita di un certificato, come la scadenza e il rinnovo.</span><span class="sxs-lookup"><span data-stu-id="bad4e-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="bad4e-113">Viene supportato il rinnovo automatico con autorità di certificazione selezionate, ad esempio provider di certificati X509 / Autorità di certificazione partner dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="bad4e-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="bad4e-114">NOTA: sono ammessi anche i provider e le autorità di certificazione senza partnership, ma non supportano la funzionalità di rinnovo automatico.</span><span class="sxs-lookup"><span data-stu-id="bad4e-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="bad4e-115">Supporto .NET</span><span class="sxs-lookup"><span data-stu-id="bad4e-115">.NET support</span></span>

* <span data-ttu-id="bad4e-116">**.NET 4.0** non è supportata dalla versione 2.0 della libreria .NET/C# dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="bad4e-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="bad4e-117">**.NET Core** è supportata dalla versione 2.0 della libreria .NET/C# dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="bad4e-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="bad4e-118">Spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="bad4e-118">Namespaces</span></span>

* <span data-ttu-id="bad4e-119">Lo spazio dei nomi per i **modelli** viene cambiato da **Microsoft.Azure.KeyVault** a **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="bad4e-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="bad4e-120">Lo spazio dei nomi **Microsoft.Azure.KeyVault.Internal** viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="bad4e-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="bad4e-121">Lo spazio dei nomi delle dipendenze di Azure SDK viene modificato da **Hyak.Common** e **Hyak.Common.Internals** in **Microsoft.Rest** e **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="bad4e-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="bad4e-122">Modifiche del tipo</span><span class="sxs-lookup"><span data-stu-id="bad4e-122">Type changes</span></span>

* <span data-ttu-id="bad4e-123">*Secret* modificato in *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="bad4e-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="bad4e-124">*Dictionary* modificato in *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="bad4e-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="bad4e-125">*List<T>, string []* modificato in *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="bad4e-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="bad4e-126">*NextList* modificato in *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="bad4e-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="bad4e-127">Tipi restituiti</span><span class="sxs-lookup"><span data-stu-id="bad4e-127">Return types</span></span>

* <span data-ttu-id="bad4e-128">**KeyList** e **SecretList** restituiranno *IPage<T>* anziché *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="bad4e-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="bad4e-129">L'oggetto **BackupKeyAsync** generato restituirà *BackupKeyResult* che contiene *Value* (BLOB di backup).</span><span class="sxs-lookup"><span data-stu-id="bad4e-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="bad4e-130">Prima veniva eseguito il wrapping del metodo e veniva restituito solo il valore.</span><span class="sxs-lookup"><span data-stu-id="bad4e-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="bad4e-131">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="bad4e-131">Exceptions</span></span>

* <span data-ttu-id="bad4e-132">*KeyVaultClientException* viene modificato in *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="bad4e-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="bad4e-133">L'errore del servizio viene modificato da *exception.Error* in *exception.Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="bad4e-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="bad4e-134">Le informazioni aggiuntive sono rimosse dal messaggio di errore per **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="bad4e-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="bad4e-135">Costruttori</span><span class="sxs-lookup"><span data-stu-id="bad4e-135">Constructors</span></span>

* <span data-ttu-id="bad4e-136">Invece di accettare *HttpClient* come argomento del costruttore, il costruttore accetta solo *HttpClientHandler* o *DelegatingHandler[]*.</span><span class="sxs-lookup"><span data-stu-id="bad4e-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="bad4e-137">Pacchetti scaricati</span><span class="sxs-lookup"><span data-stu-id="bad4e-137">Downloaded packages</span></span>

<span data-ttu-id="bad4e-138">Durante l'elaborazione di una dipendenza dall'insieme di credenziali delle chiavi da parte del client, venivano scaricati i pacchetti seguenti</span><span class="sxs-lookup"><span data-stu-id="bad4e-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="bad4e-139">Elenco dei pacchetti precedenti</span><span class="sxs-lookup"><span data-stu-id="bad4e-139">Previous package list</span></span>

* <span data-ttu-id="bad4e-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="bad4e-148">Elenco dei pacchetti correnti</span><span class="sxs-lookup"><span data-stu-id="bad4e-148">Current package list</span></span>

* <span data-ttu-id="bad4e-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="bad4e-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="bad4e-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="bad4e-152">Modifiche alle classi</span><span class="sxs-lookup"><span data-stu-id="bad4e-152">Class changes</span></span>

* <span data-ttu-id="bad4e-153">La **UnixEpoch** è stata rimossa</span><span class="sxs-lookup"><span data-stu-id="bad4e-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="bad4e-154">La classe **Base64UrlConverter** viene rinominata in **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="bad4e-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="bad4e-155">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="bad4e-155">Other changes</span></span>

* <span data-ttu-id="bad4e-156">A questa versione dell'API è stato aggiunto il supporto per la configurazione dei criteri per i tentativi dell'operazione insieme di credenziali delle chiavi su errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="bad4e-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="bad4e-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="bad4e-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="bad4e-158">Per le operazioni che restituivano un *insieme di credenziali*, il tipo restituito era una classe che conteneva una proprietà Vault.</span><span class="sxs-lookup"><span data-stu-id="bad4e-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="bad4e-159">Il tipo restituito è ora *Vault*.</span><span class="sxs-lookup"><span data-stu-id="bad4e-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="bad4e-160">*PermissionsToKeys* e *PermissionsToSecrets* ora sono *Permissions.Keys* e *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="bad4e-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="bad4e-161">Alcune delle modifiche che riguardano i tipi restituiti si applicano anche al piano di controllo.</span><span class="sxs-lookup"><span data-stu-id="bad4e-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="bad4e-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="bad4e-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="bad4e-163">Il pacchetto viene interrotto a **Microsoft.Azure.KeyVault.Extensions** e **Microsoft.Azure.KeyVault.Cryptography** per le operazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="bad4e-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

