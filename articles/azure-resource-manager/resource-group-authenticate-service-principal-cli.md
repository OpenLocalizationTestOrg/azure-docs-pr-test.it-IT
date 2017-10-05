---
title: "Creare un'identità per un'app Azure con l'interfaccia della riga di comando di Azure | Microsoft Docs"
description: "Descrive come utilizzare l'interfaccia della riga di comando di Azure per creare un'applicazione Azure Active Directory e un'entità servizio e concedere l'accesso alle risorse tramite il controllo degli accessi in base al ruolo. Illustra come autenticare l'applicazione con una password o un certificato."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="44cdd-104">Usare l'interfaccia della riga di comando di Azure per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="44cdd-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="44cdd-105">Quando si ha un'app o uno script che deve accedere alle risorse, è possibile configurare un'identità per l'app ed eseguirne l'autenticazione con credenziali specifiche.</span><span class="sxs-lookup"><span data-stu-id="44cdd-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="44cdd-106">Questa identità è nota come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-106">This identity is known as a service principal.</span></span> <span data-ttu-id="44cdd-107">Questo approccio consente di:</span><span class="sxs-lookup"><span data-stu-id="44cdd-107">This approach enables you to:</span></span>

* <span data-ttu-id="44cdd-108">Assegnare all'identità dell'app autorizzazioni diverse rispetto a quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="44cdd-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="44cdd-109">Tali autorizzazioni sono in genere limitate alle specifiche operazioni che devono essere eseguite dall'app.</span><span class="sxs-lookup"><span data-stu-id="44cdd-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="44cdd-110">Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="44cdd-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="44cdd-111">Questo argomento illustra come usare l'[interfaccia della riga di comando di Azure 1.0](../cli-install-nodejs.md) per configurare un'applicazione per l'esecuzione con credenziali e identità proprie.</span><span class="sxs-lookup"><span data-stu-id="44cdd-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="44cdd-112">Installare la versione più recente dell'[interfaccia della riga di comando di Azure 1.0](../cli-install-nodejs.md) per assicurarsi che l'ambiente corrisponda agli esempi presentati nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="44cdd-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="44cdd-113">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="44cdd-113">Required permissions</span></span>
<span data-ttu-id="44cdd-114">Per completare questo argomento è necessario avere autorizzazioni sufficienti sia nell'istanza di Azure Active Directory che nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="44cdd-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="44cdd-115">In particolare, è necessario poter creare un'app in Azure Active Directory e assegnare l'entità servizio a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="44cdd-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="44cdd-116">Il modo più semplice per verificare se l'account dispone delle autorizzazioni appropriate è tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="44cdd-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="44cdd-117">Vedere l'articolo su come [controllare le autorizzazioni necessarie nel portale](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="44cdd-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="44cdd-118">Passare ora alla sezione relativa all'autenticazione della [password](#create-service-principal-with-password) o del [certificato](#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="44cdd-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="44cdd-119">Creare un'entità servizio con password</span><span class="sxs-lookup"><span data-stu-id="44cdd-119">Create service principal with password</span></span>
<span data-ttu-id="44cdd-120">In questa sezione si eseguono i passaggi per creare l'applicazione AD protetta da password e assegnare il ruolo di lettura all'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="44cdd-121">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="44cdd-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="44cdd-122">Per creare un'identità dell'app, specificare il nome dell'app e una password, come illustrato nel comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="44cdd-123">Viene restituita la nuova entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-123">The new service principal is returned.</span></span> <span data-ttu-id="44cdd-124">Quando si concedono autorizzazioni, è necessario l'Id oggetto.</span><span class="sxs-lookup"><span data-stu-id="44cdd-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="44cdd-125">Il GUID indicato in Nomi entità servizio è necessario al momento di eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="44cdd-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="44cdd-126">Si tratta dello stesso valore di ID app.</span><span class="sxs-lookup"><span data-stu-id="44cdd-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="44cdd-127">Nelle applicazioni di esempio, questo valore viene definito `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="44cdd-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="44cdd-128">Concedere le autorizzazioni dell'entità servizio nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="44cdd-129">In questo esempio viene aggiunta l'entità servizio al ruolo Lettore, concedendo così l'autorizzazione per la lettura di tutte le risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="44cdd-130">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="44cdd-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="44cdd-131">Per il parametro Objectid, specificare il valore di ObjectId usato durante la creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="44cdd-132">Prima di eseguire questo comando, è necessario lasciare che la nuova entità servizio si propaghi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44cdd-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="44cdd-133">Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività.</span><span class="sxs-lookup"><span data-stu-id="44cdd-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="44cdd-134">In uno script, è necessario aggiungere un passaggio di sospensione tra i comandi (ad esempio `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="44cdd-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="44cdd-135">Se viene visualizzato un errore indicante che l'entità non esiste nella directory, eseguire nuovamente il comando.</span><span class="sxs-lookup"><span data-stu-id="44cdd-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="44cdd-136">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="44cdd-136">That's it!</span></span> <span data-ttu-id="44cdd-137">L'applicazione AD e l''entità servizio sono così configurate.</span><span class="sxs-lookup"><span data-stu-id="44cdd-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="44cdd-138">La sezione successiva illustra come accedere con le credenziali tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="44cdd-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="44cdd-139">Se si vogliono usare le credenziali nell'applicazione di codice, non è necessario continuare con questo argomento.</span><span class="sxs-lookup"><span data-stu-id="44cdd-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="44cdd-140">È possibile passare ad [Applicazioni di esempio](#sample-applications) per esempi di accesso con l'ID applicazione e la password.</span><span class="sxs-lookup"><span data-stu-id="44cdd-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="44cdd-141">Fornire le credenziali tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="44cdd-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="44cdd-142">A questo punto è necessario accedere come applicazione per eseguire operazioni.</span><span class="sxs-lookup"><span data-stu-id="44cdd-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="44cdd-143">Ogni volta che si accede come un'entità servizio, è necessario fornire l'ID tenant della directory per l'app AD.</span><span class="sxs-lookup"><span data-stu-id="44cdd-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="44cdd-144">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44cdd-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="44cdd-145">Per recuperare l'ID tenant per la sottoscrizione attualmente autenticata, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="44cdd-146">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="44cdd-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="44cdd-147">Se è necessario ottenere l'ID tenant di un'altra sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="44cdd-148">Se è necessario recuperare l'ID client da usare per l'accesso, usare:</span><span class="sxs-lookup"><span data-stu-id="44cdd-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="44cdd-149">Il valore da usare per eseguire l'accesso è il GUID nei nomi dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="44cdd-150">Accedere come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="44cdd-151">Verrà richiesto di specificare la password.</span><span class="sxs-lookup"><span data-stu-id="44cdd-151">You are prompted for the password.</span></span> <span data-ttu-id="44cdd-152">Fornire la password specificata durante la creazione dell'applicazione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44cdd-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="44cdd-153">A questo punto è stata eseguita l'autenticazione come entità servizio per l'entità servizio creata.</span><span class="sxs-lookup"><span data-stu-id="44cdd-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="44cdd-154">In alternativa, è possibile richiamare operazioni REST dalla riga di comando per eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="44cdd-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="44cdd-155">Dalla risposta di autenticazione è possibile recuperare il token di accesso da usare con altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="44cdd-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="44cdd-156">Per un esempio di come recuperare il token di accesso richiamando operazioni REST, vedere [Generazione di un token di accesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="44cdd-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="44cdd-157">Creare un'entità servizio con certificato</span><span class="sxs-lookup"><span data-stu-id="44cdd-157">Create service principal with certificate</span></span>
<span data-ttu-id="44cdd-158">In questa sezione vengono eseguiti i passaggi per:</span><span class="sxs-lookup"><span data-stu-id="44cdd-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="44cdd-159">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="44cdd-159">create a self-signed certificate</span></span>
* <span data-ttu-id="44cdd-160">Creare l'applicazione AD con il certificato e l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="44cdd-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="44cdd-161">Assegnare il ruolo Lettore all'entità servizio</span><span class="sxs-lookup"><span data-stu-id="44cdd-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="44cdd-162">Per completare i passaggi è necessario aver installato [OpenSSL](http://www.openssl.org/) .</span><span class="sxs-lookup"><span data-stu-id="44cdd-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="44cdd-163">Creare un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="44cdd-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="44cdd-164">Nel passaggio precedente sono stati creati due file: privkey.pem e cert.pem.</span><span class="sxs-lookup"><span data-stu-id="44cdd-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="44cdd-165">Combinare le chiavi pubblica e privata in un singolo file.</span><span class="sxs-lookup"><span data-stu-id="44cdd-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="44cdd-166">Aprire il file **examplecert.pem** e cercare la lunga sequenza di caratteri tra **-----BEGIN CERTIFICATE-----** e **-----END CERTIFICATE-----**.</span><span class="sxs-lookup"><span data-stu-id="44cdd-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="44cdd-167">Copiare i dati del certificato.</span><span class="sxs-lookup"><span data-stu-id="44cdd-167">Copy the certificate data.</span></span> <span data-ttu-id="44cdd-168">Questi dati verranno passati come parametri durante la creazione dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="44cdd-169">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="44cdd-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="44cdd-170">Per creare l'entità servizio, fornire il nome dell'app e i dati del certificato, come illustrato nel comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="44cdd-171">Viene restituita la nuova entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-171">The new service principal is returned.</span></span> <span data-ttu-id="44cdd-172">Quando si concedono autorizzazioni, è necessario l'Id oggetto.</span><span class="sxs-lookup"><span data-stu-id="44cdd-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="44cdd-173">Il GUID indicato in Nomi entità servizio è necessario al momento di eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="44cdd-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="44cdd-174">Si tratta dello stesso valore di ID app.</span><span class="sxs-lookup"><span data-stu-id="44cdd-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="44cdd-175">Nelle applicazioni di esempio, questo valore viene definito come ID client.</span><span class="sxs-lookup"><span data-stu-id="44cdd-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="44cdd-176">Concedere le autorizzazioni dell'entità servizio nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="44cdd-177">In questo esempio viene aggiunta l'entità servizio al ruolo Lettore, concedendo così l'autorizzazione per la lettura di tutte le risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="44cdd-178">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="44cdd-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="44cdd-179">Per il parametro Objectid, specificare il valore di ObjectId usato durante la creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="44cdd-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="44cdd-180">Prima di eseguire questo comando, è necessario lasciare che la nuova entità servizio si propaghi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44cdd-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="44cdd-181">Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività.</span><span class="sxs-lookup"><span data-stu-id="44cdd-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="44cdd-182">In uno script, è necessario aggiungere un passaggio di sospensione tra i comandi (ad esempio `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="44cdd-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="44cdd-183">Se viene visualizzato un errore indicante che l'entità non esiste nella directory, eseguire nuovamente il comando.</span><span class="sxs-lookup"><span data-stu-id="44cdd-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="44cdd-184">Fornire il certificato tramite uno script dell'interfaccia della riga di comando di Azure automatizzato</span><span class="sxs-lookup"><span data-stu-id="44cdd-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="44cdd-185">A questo punto è necessario accedere come applicazione per eseguire operazioni.</span><span class="sxs-lookup"><span data-stu-id="44cdd-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="44cdd-186">Ogni volta che si accede come un'entità servizio, è necessario fornire l'ID tenant della directory per l'app AD.</span><span class="sxs-lookup"><span data-stu-id="44cdd-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="44cdd-187">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44cdd-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="44cdd-188">Per recuperare l'ID tenant per la sottoscrizione attualmente autenticata, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="44cdd-189">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="44cdd-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="44cdd-190">Se è necessario ottenere l'ID tenant di un'altra sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44cdd-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="44cdd-191">Per recuperare l'identificazione personale del certificato e rimuovere i caratteri non necessari, usare:</span><span class="sxs-lookup"><span data-stu-id="44cdd-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="44cdd-192">Viene restituito un valore di identificazione personale simile a:</span><span class="sxs-lookup"><span data-stu-id="44cdd-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="44cdd-193">Se è necessario recuperare l'ID client da usare per l'accesso, usare:</span><span class="sxs-lookup"><span data-stu-id="44cdd-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="44cdd-194">Il valore da usare per eseguire l'accesso è il GUID nei nomi dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="44cdd-195">Accedere come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="44cdd-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="44cdd-196">A questo punto, è stata eseguita l'autenticazione come entità servizio per l'applicazione di Azure Active Directory creata.</span><span class="sxs-lookup"><span data-stu-id="44cdd-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="44cdd-197">Modificare le credenziali</span><span class="sxs-lookup"><span data-stu-id="44cdd-197">Change credentials</span></span>

<span data-ttu-id="44cdd-198">Per modificare le credenziali per un'app di Active Directory, a causa di una violazione della protezione o di credenziali scadute, usare `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="44cdd-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="44cdd-199">Per modificare una password, usare:</span><span class="sxs-lookup"><span data-stu-id="44cdd-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="44cdd-200">Per modificare un valore del certificato, usare:</span><span class="sxs-lookup"><span data-stu-id="44cdd-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="44cdd-201">Debug</span><span class="sxs-lookup"><span data-stu-id="44cdd-201">Debug</span></span>

<span data-ttu-id="44cdd-202">Durante la creazione di un'entità servizio, è possibile riscontrare gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="44cdd-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="44cdd-203">**"Authentication_Unauthorized"** o **"Nessuna sottoscrizione trovata nel contesto".**</span><span class="sxs-lookup"><span data-stu-id="44cdd-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="44cdd-204">- Questo errore viene visualizzato quando l'account non ha le [autorizzazioni necessarie](#required-permissions) in Azure Active Directory per registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="44cdd-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="44cdd-205">In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore.</span><span class="sxs-lookup"><span data-stu-id="44cdd-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="44cdd-206">Chiedere all'amministratore di essere assegnati a un ruolo di amministratore oppure di consentire agli utenti di registrare le app.</span><span class="sxs-lookup"><span data-stu-id="44cdd-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="44cdd-207">L'account **"non è autorizzato a eseguire l'azione 'Microsoft.Authorization/roleAssignments/write' nell'ambito '/subscriptions/{guid}'."** - Questo errore viene visualizzato quando l'account non dispone di autorizzazioni sufficienti per assegnare un ruolo a un'identità.</span><span class="sxs-lookup"><span data-stu-id="44cdd-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="44cdd-208">Chiedere all'amministratore della sottoscrizione di essere aggiunti al ruolo Amministratore accessi utente.</span><span class="sxs-lookup"><span data-stu-id="44cdd-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="44cdd-209">Applicazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="44cdd-209">Sample applications</span></span>
<span data-ttu-id="44cdd-210">Per informazioni su come effettuare l'accesso all'applicazione su diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="44cdd-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="44cdd-211">.NET</span><span class="sxs-lookup"><span data-stu-id="44cdd-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="44cdd-212">Java</span><span class="sxs-lookup"><span data-stu-id="44cdd-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="44cdd-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="44cdd-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="44cdd-214">Python</span><span class="sxs-lookup"><span data-stu-id="44cdd-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="44cdd-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="44cdd-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="44cdd-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="44cdd-216">Next steps</span></span>
* <span data-ttu-id="44cdd-217">Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [Guida per gli sviluppatori all'autorizzazione con l'API di Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44cdd-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="44cdd-218">Per altre informazioni sull'uso dei certificati e dell'interfaccia della riga di comando di Azure, vedere [Certificate-based auth with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)(Autenticazione basata su certificati con le entità servizio di Azure dalla riga di comando di Linux).</span><span class="sxs-lookup"><span data-stu-id="44cdd-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="44cdd-219">Per un elenco di azioni disponibili che è possibile concedere o negare agli utenti, vedere [Operazioni di provider di risorse con Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="44cdd-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
