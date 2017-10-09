---
title: note sulla versione di .NET insieme di credenziali 2. x API aaaKey | Documenti Microsoft
description: Gli sviluppatori .NET utilizzeranno questo toocode API per insieme credenziali chiavi Azure
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
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="ddbfd-103">Guida alla migrazione e note sulla versione .NET 2.0 per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="ddbfd-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="ddbfd-104">Hello note e linee guida seguenti sono per gli sviluppatori che utilizzano .NET insieme di credenziali chiave di Azure / libreria di c#.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="ddbfd-105">In fase di transizione hello dalla versione di hello 1.0 versione toohello 2.0, un numero di aggiornamenti è stato apportato che richiedono operazioni di migrazione del codice affinché toobenefit dai miglioramenti funzionali hello e funzionalità aggiunte come **insieme di credenziali chiave i certificati** supportano.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="ddbfd-106">Certificati Key Vault</span><span class="sxs-lookup"><span data-stu-id="ddbfd-106">Key Vault certificates</span></span>

<span data-ttu-id="ddbfd-107">Fornisce il supporto di certificati di chiave dell'insieme di credenziali per la gestione del x509 certificati e hello comportamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ddbfd-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="ddbfd-108">Consente un toocreate di proprietario del certificato a un certificato tramite un processo di creazione dell'insieme di credenziali chiave o importazione di hello di un certificato esistente.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="ddbfd-109">Sono inclusi i certificati autofirmati e i certificati generati dall'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="ddbfd-110">Consente il proprietario di un certificato di chiave dell'insieme di credenziali di archiviazione protetta tooimplement e la gestione di X509 certificati senza l'interazione con materiale della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="ddbfd-111">Consente un toocreate di proprietario del certificato di un criterio che indirizza l'insieme di credenziali chiave toomanage hello del ciclo di vita di un certificato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="ddbfd-112">Consente ai proprietari di certificato tooprovide informazioni di contatto per la notifica sugli eventi del ciclo di vita di scadenza e il rinnovo del certificato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="ddbfd-113">Viene supportato il rinnovo automatico con autorità di certificazione selezionate, ad esempio provider di certificati X509 / Autorità di certificazione partner dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="ddbfd-114">Nota: Non collaborato provider/autorità sono inoltre consentite ma non supporta funzionalità di rinnovo automatico hello.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="ddbfd-115">Supporto .NET</span><span class="sxs-lookup"><span data-stu-id="ddbfd-115">.NET support</span></span>

* <span data-ttu-id="ddbfd-116">**.NET 4.0** non è supportata dalla versione di hello 2.0 di .NET insieme credenziali chiavi Azure hello / libreria di c#</span><span class="sxs-lookup"><span data-stu-id="ddbfd-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="ddbfd-117">**.NET core** è supportata dalla versione di hello 2.0 di .NET insieme credenziali chiavi Azure hello / libreria di c#</span><span class="sxs-lookup"><span data-stu-id="ddbfd-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="ddbfd-118">Spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="ddbfd-118">Namespaces</span></span>

* <span data-ttu-id="ddbfd-119">spazio dei nomi per Hello **modelli** viene modificato da **Microsoft.Azure.KeyVault** troppo**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="ddbfd-120">Hello **Microsoft.Azure.KeyVault.Internal** dello spazio dei nomi viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="ddbfd-121">spazio dei nomi di Hello Azure SDK le dipendenze vengono modificate da **Hyak.Common** e **Hyak.Common.Internals** troppo**Microsoft.Rest** e  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="ddbfd-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="ddbfd-122">Modifiche del tipo</span><span class="sxs-lookup"><span data-stu-id="ddbfd-122">Type changes</span></span>

* <span data-ttu-id="ddbfd-123">*Segreto* modificato troppo*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="ddbfd-124">*Dizionario* modificato troppo*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="ddbfd-125">*Elenco<T>, string []* modificato troppo*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="ddbfd-126">*NextList* modificato troppo *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="ddbfd-127">Tipi restituiti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-127">Return types</span></span>

* <span data-ttu-id="ddbfd-128">**KeyList** e **SecretList** restituiranno *IPage<T>* anziché *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="ddbfd-129">Hello generato **BackupKeyAsync** restituirà *BackupKeyResult* contenente *valore* (blob di backup).</span><span class="sxs-lookup"><span data-stu-id="ddbfd-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="ddbfd-130">Prima di hello metodo è stato sottoposto a wrapping e restituire unico valore hello.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="ddbfd-131">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="ddbfd-131">Exceptions</span></span>

* <span data-ttu-id="ddbfd-132">*KeyVaultClientException* è stato modificato anche*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="ddbfd-133">Errore del servizio Hello viene modificato da *eccezione. Errore* troppo*eccezione. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="ddbfd-134">Rimuovere informazioni aggiuntive nel messaggio di errore hello per **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="ddbfd-135">Costruttori</span><span class="sxs-lookup"><span data-stu-id="ddbfd-135">Constructors</span></span>

* <span data-ttu-id="ddbfd-136">Invece di accettare un *HttpClient* come un argomento del costruttore, hello costruttore accetta solo *HttpClientHandler* o *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="ddbfd-137">Pacchetti scaricati</span><span class="sxs-lookup"><span data-stu-id="ddbfd-137">Downloaded packages</span></span>

<span data-ttu-id="ddbfd-138">Quando un client viene elaborata una dipendenza in seguito hello insieme di credenziali chiave sono stati scaricati</span><span class="sxs-lookup"><span data-stu-id="ddbfd-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="ddbfd-139">Elenco dei pacchetti precedenti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-139">Previous package list</span></span>

* <span data-ttu-id="ddbfd-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="ddbfd-148">Elenco dei pacchetti correnti</span><span class="sxs-lookup"><span data-stu-id="ddbfd-148">Current package list</span></span>

* <span data-ttu-id="ddbfd-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="ddbfd-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="ddbfd-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="ddbfd-152">Modifiche alle classi</span><span class="sxs-lookup"><span data-stu-id="ddbfd-152">Class changes</span></span>

* <span data-ttu-id="ddbfd-153">La **UnixEpoch** è stata rimossa</span><span class="sxs-lookup"><span data-stu-id="ddbfd-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="ddbfd-154">**Base64UrlConverter** classe viene rinominata troppo**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="ddbfd-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="ddbfd-155">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="ddbfd-155">Other changes</span></span>

* <span data-ttu-id="ddbfd-156">È stato aggiunto supporto per la configurazione di hello del criterio di ripetizione KV operazione nel caso di errori temporanei versione toothis di hello API.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="ddbfd-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="ddbfd-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="ddbfd-158">Per le operazioni di hello che ha restituito un *insieme di credenziali*, tipo restituito di hello è una classe che contiene una proprietà dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="ddbfd-159">Hello tipo restituito è ora *insieme di credenziali*.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="ddbfd-160">*PermissionsToKeys* e *PermissionsToSecrets* ora sono *Permissions.Keys* e *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="ddbfd-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="ddbfd-161">Alcune di hello restituiscono toohello Pannello di controllo anche di applicare le modifiche di tipi.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="ddbfd-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="ddbfd-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="ddbfd-163">pacchetto di Hello viene suddivisa in troppo**Microsoft.Azure.KeyVault.Extensions** e **Microsoft.Azure.KeyVault.Cryptography** per le operazioni di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="ddbfd-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

