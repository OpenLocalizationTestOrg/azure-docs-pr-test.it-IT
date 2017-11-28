---
title: "identità aaaCreate per app di Azure con Azure CLI | Documenti Microsoft"
description: "Viene descritto come controllare toouse CLI di Azure toocreate un'applicazione Azure Active Directory e dell'entità servizio e concedere tooresources accedere tramite l'accesso basato sui ruoli. Viene illustrato come applicazione tooauthenticate con un certificato o la password."
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
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="491d7-104">Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="491d7-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="491d7-105">Quando si dispone di un'app o script che richiede risorse tooaccess, è possibile impostare un'identità per l'applicazione hello e l'applicazione hello con le proprie credenziali di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="491d7-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="491d7-106">Questa identità è nota come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="491d7-106">This identity is known as a service principal.</span></span> <span data-ttu-id="491d7-107">Questo approccio consente di:</span><span class="sxs-lookup"><span data-stu-id="491d7-107">This approach enables you to:</span></span>

* <span data-ttu-id="491d7-108">Assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="491d7-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="491d7-109">In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.</span><span class="sxs-lookup"><span data-stu-id="491d7-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="491d7-110">Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="491d7-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="491d7-111">In questo articolo illustra come toouse [CLI di Azure 1.0](../cli-install-nodejs.md) tooset backup toorun un'applicazione con le proprie credenziali e identità.</span><span class="sxs-lookup"><span data-stu-id="491d7-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="491d7-112">Installare una versione più recente di hello di [CLI di Azure 1.0](../cli-install-nodejs.md) toomake che l'ambiente corrisponda esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="491d7-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="491d7-113">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="491d7-113">Required permissions</span></span>
<span data-ttu-id="491d7-114">toocomplete in questo argomento, è necessario disporre delle autorizzazioni sufficienti in Azure Active Directory sia la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="491d7-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="491d7-115">In particolare, devono essere in grado di toocreate un'app in Azure Active Directory hello e assegnazione di ruolo tooa principale di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="491d7-116">Hello più semplice modo toocheck se l'account disponga delle autorizzazioni appropriate è tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="491d7-117">Vedere l'articolo su come [controllare le autorizzazioni necessarie nel portale](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="491d7-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="491d7-118">A questo punto, procedere sezione tooa per uno [password](#create-service-principal-with-password) o [certificato](#create-service-principal-with-certificate) l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="491d7-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="491d7-119">Creare un'entità servizio con password</span><span class="sxs-lookup"><span data-stu-id="491d7-119">Create service principal with password</span></span>
<span data-ttu-id="491d7-120">In questa sezione, eseguire hello passaggi toocreate hello applicazione Active Directory con una password e assegnare l'entità di servizio toohello ruolo Lettore hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="491d7-121">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="491d7-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="491d7-122">toocreate un'identità di applicazione, specificare nome hello dell'applicazione hello e una password, come illustrato nel comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="491d7-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="491d7-123">viene restituita l'entità servizio nuovo Hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-123">hello new service principal is returned.</span></span> <span data-ttu-id="491d7-124">Id oggetto Hello è necessaria quando si concedono autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="491d7-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="491d7-125">guid Hello elencato con hello nomi dell'entità servizio è necessaria durante l'accesso.</span><span class="sxs-lookup"><span data-stu-id="491d7-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="491d7-126">Questo guid è hello stesso valore di id app hello. Nelle applicazioni di esempio hello, questo valore è hello tooas cui `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="491d7-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="491d7-127">Concedere le autorizzazioni dell'entità hello servizio nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="491d7-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="491d7-128">In questo esempio, aggiungere hello servizio principale toohello ruolo lettura, che concede l'autorizzazione tooread tutte le risorse nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="491d7-129">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="491d7-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="491d7-130">Per il parametro objectid hello, fornire l'Id di oggetto da usare durante la creazione di un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="491d7-131">Prima di eseguire questo comando, è necessario consentire un certo tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="491d7-132">Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività.</span><span class="sxs-lookup"><span data-stu-id="491d7-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="491d7-133">In uno script, è necessario aggiungere un passaggio toosleep tra i comandi di hello (ad esempio `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="491d7-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="491d7-134">Se viene visualizzato che un messaggio hello a errore principale non esiste nella directory di hello, eseguire di nuovo il comando hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="491d7-135">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="491d7-135">That's it!</span></span> <span data-ttu-id="491d7-136">L'applicazione AD e l''entità servizio sono così configurate.</span><span class="sxs-lookup"><span data-stu-id="491d7-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="491d7-137">Nella sezione successiva Hello viene illustrato come toolog con hello credenziali tramite l'interfaccia CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="491d7-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="491d7-138">Se si desiderano credenziali hello toouse codice nell'applicazione in uso, non è necessario toocontinue con questo argomento.</span><span class="sxs-lookup"><span data-stu-id="491d7-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="491d7-139">È possibile passare toohello [applicazioni di esempio](#sample-applications) per esempi di accesso con l'id dell'applicazione e la password.</span><span class="sxs-lookup"><span data-stu-id="491d7-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="491d7-140">Fornire le credenziali tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="491d7-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="491d7-141">A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="491d7-142">Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="491d7-143">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="491d7-144">id tenant di hello tooretrieve per la sottoscrizione attualmente autenticata, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="491d7-145">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="491d7-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="491d7-146">Se è necessario l'id tenant di hello tooget di un'altra sottoscrizione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="491d7-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="491d7-147">Se è necessario tooretrieve hello client id toouse per l'accesso, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="491d7-148">Hello valore toouse per l'accesso è il guid di hello elencato in nomi dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="491d7-149">Accedi come servizio hello principale.</span><span class="sxs-lookup"><span data-stu-id="491d7-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="491d7-150">Viene chiesto di immettere la password di hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-150">You are prompted for hello password.</span></span> <span data-ttu-id="491d7-151">Specificare la password di hello specificata durante la creazione di un'applicazione hello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="491d7-152">Ora vengono autenticate come entità servizio hello per entità di servizio hello creato.</span><span class="sxs-lookup"><span data-stu-id="491d7-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="491d7-153">In alternativa, è possibile richiamare le operazioni REST da toolog riga di comando hello in.</span><span class="sxs-lookup"><span data-stu-id="491d7-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="491d7-154">Dalla risposta di autenticazione hello, è possibile recuperare il token di accesso hello per l'utilizzo con altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="491d7-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="491d7-155">Per un esempio di recupero dei token di accesso hello richiamando operazioni REST, vedere [la generazione di un Token di accesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="491d7-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="491d7-156">Creare un'entità servizio con certificato</span><span class="sxs-lookup"><span data-stu-id="491d7-156">Create service principal with certificate</span></span>
<span data-ttu-id="491d7-157">In questa sezione, eseguire passaggi di hello per:</span><span class="sxs-lookup"><span data-stu-id="491d7-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="491d7-158">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="491d7-158">create a self-signed certificate</span></span>
* <span data-ttu-id="491d7-159">creare applicazione AD hello con certificato hello e l'entità servizio hello</span><span class="sxs-lookup"><span data-stu-id="491d7-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="491d7-160">assegnare l'entità di servizio toohello ruolo Lettore hello</span><span class="sxs-lookup"><span data-stu-id="491d7-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="491d7-161">toocomplete questi passaggi, è necessario disporre di [OpenSSL](http://www.openssl.org/) installato.</span><span class="sxs-lookup"><span data-stu-id="491d7-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="491d7-162">Creare un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="491d7-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="491d7-163">Hello precedente passaggio creato due file - privkey.pem e cert.pem.</span><span class="sxs-lookup"><span data-stu-id="491d7-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="491d7-164">Combinare le chiavi pubbliche e private hello in un singolo file.</span><span class="sxs-lookup"><span data-stu-id="491d7-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="491d7-165">Aprire hello **examplecert.pem** file e cercare di sequenza di caratteri tra lunga hello **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---**.</span><span class="sxs-lookup"><span data-stu-id="491d7-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="491d7-166">Copiare i dati del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-166">Copy hello certificate data.</span></span> <span data-ttu-id="491d7-167">Passare questi dati come parametro durante la creazione di un'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="491d7-168">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="491d7-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="491d7-169">entità di servizio toocreate hello, specificare il nome di hello hello app e dei dati del certificato hello, come illustrato nel comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="491d7-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="491d7-170">viene restituita l'entità servizio nuovo Hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-170">hello new service principal is returned.</span></span> <span data-ttu-id="491d7-171">Id oggetto Hello è necessaria quando si concedono autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="491d7-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="491d7-172">guid Hello elencato con hello nomi dell'entità servizio è necessaria durante l'accesso.</span><span class="sxs-lookup"><span data-stu-id="491d7-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="491d7-173">Questo guid è hello stesso valore di id app hello. Nelle applicazioni di esempio hello, questo valore è hello tooas cui ID Client.</span><span class="sxs-lookup"><span data-stu-id="491d7-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="491d7-174">Concedere le autorizzazioni dell'entità hello servizio nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="491d7-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="491d7-175">In questo esempio, aggiungere hello servizio principale toohello ruolo lettura, che concede l'autorizzazione tooread tutte le risorse nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="491d7-176">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="491d7-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="491d7-177">Per il parametro objectid hello, fornire l'Id di oggetto da usare durante la creazione di un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="491d7-178">Prima di eseguire questo comando, è necessario consentire un certo tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="491d7-179">Quando si eseguono questi comandi manualmente, in genere trascorre tempo sufficiente tra le attività.</span><span class="sxs-lookup"><span data-stu-id="491d7-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="491d7-180">In uno script, è necessario aggiungere un passaggio toosleep tra i comandi di hello (ad esempio `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="491d7-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="491d7-181">Se viene visualizzato che un messaggio hello a errore principale non esiste nella directory di hello, eseguire di nuovo il comando hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="491d7-182">Fornire il certificato tramite uno script dell'interfaccia della riga di comando di Azure automatizzato</span><span class="sxs-lookup"><span data-stu-id="491d7-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="491d7-183">A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="491d7-184">Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="491d7-185">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="491d7-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="491d7-186">id tenant di hello tooretrieve per la sottoscrizione attualmente autenticata, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="491d7-187">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="491d7-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="491d7-188">Se è necessario l'id tenant di hello tooget di un'altra sottoscrizione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="491d7-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="491d7-189">tooretrieve hello identificazione personale del certificato e rimuovere i caratteri non necessari, usare:</span><span class="sxs-lookup"><span data-stu-id="491d7-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="491d7-190">Viene restituito un valore di identificazione personale simile a:</span><span class="sxs-lookup"><span data-stu-id="491d7-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="491d7-191">Se è necessario tooretrieve hello client id toouse per l'accesso, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="491d7-192">Hello valore toouse per l'accesso è il guid di hello elencato in nomi dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="491d7-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="491d7-193">Accedi come servizio hello principale.</span><span class="sxs-lookup"><span data-stu-id="491d7-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="491d7-194">Ora vengono autenticate come entità servizio hello per hello applicazione Azure Active Directory creato.</span><span class="sxs-lookup"><span data-stu-id="491d7-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="491d7-195">Modificare le credenziali</span><span class="sxs-lookup"><span data-stu-id="491d7-195">Change credentials</span></span>

<span data-ttu-id="491d7-196">utilizzano le credenziali di hello toochange per un'app di Active Directory, a causa una compromissione della sicurezza o la scadenza di una credenziale, `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="491d7-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="491d7-197">toochange una password, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="491d7-198">toochange un valore del certificato, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="491d7-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="491d7-199">Debug</span><span class="sxs-lookup"><span data-stu-id="491d7-199">Debug</span></span>

<span data-ttu-id="491d7-200">È possibile riscontrare hello gli errori seguenti durante la creazione di un'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="491d7-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="491d7-201">**"Authentication_Unauthorized"** o **"alcuna sottoscrizione non trovato nel contesto di hello".**</span><span class="sxs-lookup"><span data-stu-id="491d7-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="491d7-202">-Viene visualizzato questo errore quando l'account non dispone di hello [delle autorizzazioni necessarie](#required-permissions) su hello Azure Active Directory tooregister un'app.</span><span class="sxs-lookup"><span data-stu-id="491d7-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="491d7-203">In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore. Chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.</span><span class="sxs-lookup"><span data-stu-id="491d7-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="491d7-204">L'account **"ha azione tooperform autorizzazione 'Microsoft.Authorization/roleAssignments/write' su"sottoscrizioni / {guid}"ambito".**  -Questo errore viene visualizzato quando l'account non dispone di sufficienti autorizzazioni tooassign un'identità tooan ruolo.</span><span class="sxs-lookup"><span data-stu-id="491d7-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="491d7-205">Chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore.</span><span class="sxs-lookup"><span data-stu-id="491d7-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="491d7-206">Applicazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="491d7-206">Sample applications</span></span>
<span data-ttu-id="491d7-207">Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="491d7-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="491d7-208">.NET</span><span class="sxs-lookup"><span data-stu-id="491d7-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="491d7-209">Java</span><span class="sxs-lookup"><span data-stu-id="491d7-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="491d7-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="491d7-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="491d7-211">Python</span><span class="sxs-lookup"><span data-stu-id="491d7-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="491d7-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="491d7-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="491d7-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="491d7-213">Next steps</span></span>
* <span data-ttu-id="491d7-214">Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="491d7-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="491d7-215">tooget ulteriori informazioni sull'utilizzo di certificati e CLI di Azure, vedere [l'autenticazione basata su certificati con le entità servizio di Azure dalla riga di comando Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="491d7-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="491d7-216">Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="491d7-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
