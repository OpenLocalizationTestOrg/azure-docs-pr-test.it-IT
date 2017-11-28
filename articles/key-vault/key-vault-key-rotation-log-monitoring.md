---
title: aaaSet backup insieme credenziali chiavi Azure con la rotazione della chiave end-to-end e il controllo | Documenti Microsoft
description: Utilizzare questa procedura-tootoohelp che impostare rotazione delle chiavi e i registri di monitoraggio dell'insieme di credenziali chiave.
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="905c1-103">Configurare l'insieme di credenziali delle chiavi di Azure con rotazione e controllo delle chiavi end-to-end</span><span class="sxs-lookup"><span data-stu-id="905c1-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="905c1-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="905c1-104">Introduction</span></span>
<span data-ttu-id="905c1-105">Dopo la creazione di credenziali delle chiavi, sarà in grado di toostart utilizzando toostore tale insieme di credenziali, le chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="905c1-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="905c1-106">Le applicazioni non è più necessitano toopersist le chiavi o i segreti, ma piuttosto verranno richiesti dall'insieme di credenziali chiave hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="905c1-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="905c1-107">Ciò permette tooupdate chiavi e segreti senza influire sul comportamento di hello dell'applicazione, che consente un'ampia gamma di possibilità per la chiave e la gestione di informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="905c1-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="905c1-108">Questo articolo descrive un esempio di utilizzo insieme credenziali chiavi Azure toostore un segreto, in questo caso una chiave dell'Account di archiviazione Azure che si accede da un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="905c1-109">Dimostra anche l'implementazione di una rotazione pianificata della chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="905c1-110">Infine, esamina una dimostrazione di come toomonitor hello i log di controllo dell'insieme di credenziali chiave e generano avvisi quando vengono effettuate le richieste impreviste.</span><span class="sxs-lookup"><span data-stu-id="905c1-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="905c1-111">In questa esercitazione non è previsto tooexplain dettaglio hello la configurazione iniziale di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="905c1-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="905c1-112">Per altre informazioni, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="905c1-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="905c1-113">Per le istruzioni relative all'interfaccia della riga di comando multipiattaforma, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="905c1-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="905c1-114">Configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="905c1-114">Set up Key Vault</span></span>
<span data-ttu-id="905c1-115">tooenable un tooretrieve applicazione un segreto dall'insieme di credenziali chiave, è necessario creare segreto hello e caricarlo tooyour insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="905c1-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="905c1-116">Questo può essere eseguito avviando una sessione di PowerShell di Azure e la firma in tooyour account Azure con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="905c1-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="905c1-117">Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password.</span><span class="sxs-lookup"><span data-stu-id="905c1-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="905c1-118">PowerShell recupera tutte le sottoscrizioni di hello che sono associate a questo account.</span><span class="sxs-lookup"><span data-stu-id="905c1-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="905c1-119">Usa PowerShell hello primo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="905c1-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="905c1-120">Se si dispone di più sottoscrizioni, potrebbe essere toospecify hello che è stato utilizzato toocreate credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="905c1-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="905c1-121">Immettere hello sottoscrizioni hello toosee per l'account di seguito:</span><span class="sxs-lookup"><span data-stu-id="905c1-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="905c1-122">sottoscrizione di hello toospecify è associato alla chiave dell'insieme di credenziali di hello effettuerà l'accesso, immettere:</span><span class="sxs-lookup"><span data-stu-id="905c1-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="905c1-123">Dato che questo articolo illustra l'archiviazione di una chiave dell'account di archiviazione come segreto, è necessario ottenere la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="905c1-124">Dopo aver recuperato il segreto (in questo caso, la chiave di account di archiviazione), è necessario convertire la stringa sicura tooa e quindi creare una chiave privata con tale valore nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="905c1-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="905c1-125">Quindi, è possibile ottenere hello URI per il segreto hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="905c1-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="905c1-126">Quando si chiama hello tooretrieve di insieme di credenziali chiave segreta viene utilizzato in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="905c1-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="905c1-127">Eseguire il comando PowerShell seguente hello e prendere nota del valore di ID hello, ovvero segreto hello URI:</span><span class="sxs-lookup"><span data-stu-id="905c1-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="905c1-128">Configurare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="905c1-128">Set up hello application</span></span>
<span data-ttu-id="905c1-129">Dopo aver creato un segreto archiviato, è possibile utilizzare codice tooretrieve e utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="905c1-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="905c1-130">Esistono alcuni tooachieve necessarie di passaggi questo.</span><span class="sxs-lookup"><span data-stu-id="905c1-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="905c1-131">Hello primo e più importante passaggio è registrazione dell'applicazione con Azure Active Directory e quindi di comunicare le informazioni dell'applicazione insieme di credenziali chiave in modo che questa operazione può consentire le richieste dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="905c1-132">L'applicazione deve essere creato in hello stesso tenant di Azure Active Directory come credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="905c1-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="905c1-133">Aprire scheda applicazioni hello di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-133">Open hello applications tab of Azure Active Directory.</span></span>

![Aprire applicazioni in Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="905c1-135">Scegliere **aggiungere** tooadd un tooyour applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Scegliere Aggiungi](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="905c1-137">Lasciare il tipo di applicazione hello come **applicazione WEB, e/o API WEB** e assegnare un nome di applicazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Applicazione hello nome](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="905c1-139">Immettere **URL accesso** e **URI ID app** per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="905c1-140">È possibile usare qualsiasi valore per questa demo. Sarà comunque possibile modificarli in un secondo momento se necessario.</span><span class="sxs-lookup"><span data-stu-id="905c1-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Specificare gli URI necessari](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="905c1-142">Dopo l'aggiunta di un'applicazione hello tooAzure Active Directory, verrà inserito nella pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="905c1-143">Fare clic su hello **configura** scheda e quindi individuare e copiare hello **ID Client** valore.</span><span class="sxs-lookup"><span data-stu-id="905c1-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="905c1-144">Prendere nota dell'ID client hello per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="905c1-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="905c1-145">Generare quindi una chiave per l'applicazione in modo che possa interagire con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="905c1-146">È possibile creare questo in hello **chiavi** sezione hello **configurazione** scheda. Prendere nota della chiave di hello appena generato dall'applicazione Azure Active Directory per l'utilizzo in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="905c1-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Chiavi delle applicazioni di Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="905c1-148">Prima di stabilire tutte le chiamate dall'applicazione in insieme di credenziali chiave di hello, è necessario indicare l'insieme di credenziali chiave hello sull'applicazione e le relative autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="905c1-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="905c1-149">Hello comando seguente accetta hello insieme di credenziali nome e ID client hello da app di Azure Active Directory e concede **ottenere** accesso tooyour chiave dell'insieme di credenziali per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="905c1-150">A questo punto, si è pronti toostart compilazione l'applicazione chiama.</span><span class="sxs-lookup"><span data-stu-id="905c1-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="905c1-151">Nell'applicazione, è necessario installare hello NuGet pacchetti necessari toointeract con l'insieme di credenziali chiave di Azure e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="905c1-152">Dalla console di gestione di pacchetti di Visual Studio hello, immettere hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="905c1-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="905c1-153">Al momento della stesura di hello di questo articolo, versione corrente di hello del pacchetto di Azure Active Directory hello è 3.10.305231913, pertanto si tooconfirm versione più recente di hello e aggiornare di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="905c1-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="905c1-154">Nel codice dell'applicazione, creare un metodo della classe toohold hello per l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="905c1-155">In questo esempio, la classe è denominata **Utils**.</span><span class="sxs-lookup"><span data-stu-id="905c1-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="905c1-156">Aggiungere hello seguente istruzione using:</span><span class="sxs-lookup"><span data-stu-id="905c1-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="905c1-157">Successivamente, aggiungere hello seguente token di metodo tooretrieve hello JWT da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="905c1-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="905c1-158">Per manutenzione, è consigliabile valori stringa hardcoded di hello toomove alla configurazione del web o applicazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="905c1-159">Aggiungere hello codice necessario toocall insieme di credenziali chiave e recuperare il valore segreto.</span><span class="sxs-lookup"><span data-stu-id="905c1-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="905c1-160">È innanzitutto necessario aggiungere il seguente hello istruzione using:</span><span class="sxs-lookup"><span data-stu-id="905c1-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="905c1-161">Aggiungere tooinvoke chiamate di metodo hello insieme di credenziali chiave e recuperare il segreto.</span><span class="sxs-lookup"><span data-stu-id="905c1-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="905c1-162">In questo metodo, fornire il segreto hello URI che è stato salvato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="905c1-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="905c1-163">Si noti utilizzo hello di hello **GetToken** metodo hello **Utils** classe creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="905c1-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="905c1-164">Quando si esegue l'applicazione, si dovrebbe ora autenticazione tooAzure Active Directory e quindi recuperare il valore segreto dall'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="905c1-165">Rotazione delle chiavi con Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="905c1-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="905c1-166">Sono disponibili diverse opzioni per l'implementazione di una strategia di rotazione per i valori memorizzati come segreti dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="905c1-167">La rotazione dei segreti può essere eseguita nell'ambito di un processo manuale, a livello di codice usando chiamate API oppure con uno script di automazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="905c1-168">Ai fini di hello di questo articolo, sarà con Azure PowerShell combinato con automazione di Azure toochange una chiave di accesso di Account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="905c1-169">Verrà quindi aggiornato un segreto dell'insieme di credenziali delle chiavi con la nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="905c1-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="905c1-170">tooallow automazione di Azure tooset i valori dei segreti nell'insieme di credenziali chiave, è necessario ottenere l'ID client hello per connessione hello denominato AzureRunAsConnection, che è stata creata quando è stata stabilita l'istanza di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="905c1-171">È possibile trovare l'ID scegliendo **Asset** dall'istanza di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="905c1-172">Da qui, si sceglie **connessioni** e quindi selezionare hello **AzureRunAsConnection** principio del servizio.</span><span class="sxs-lookup"><span data-stu-id="905c1-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="905c1-173">Prendere nota di hello **ID applicazione**.</span><span class="sxs-lookup"><span data-stu-id="905c1-173">Take note of hello **Application ID**.</span></span>

![ID client di Automazione di Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="905c1-175">In **Asset** scegliere **Moduli**.</span><span class="sxs-lookup"><span data-stu-id="905c1-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="905c1-176">Da **moduli**selezionare **raccolta**e quindi cercare e **importazione** le versioni aggiornate di ciascuno dei seguenti moduli hello:</span><span class="sxs-lookup"><span data-stu-id="905c1-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="905c1-177">Al momento della stesura di hello di questo articolo, hello indicato in precedenza i moduli necessari toobe aggiornata solo per lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="905c1-178">Se si verificano errori nel processo di automazione, verificare di avere importato tutti i moduli necessari e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="905c1-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="905c1-179">Dopo avere recuperato ID applicazione hello per la connessione di automazione di Azure, è necessario che l'insieme di credenziali chiave che l'applicazione disponga di accesso tooupdate segreti nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="905c1-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="905c1-180">Questo può essere eseguita con hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="905c1-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="905c1-181">Selezionare quindi **Runbook** nell'istanza di Automazione di Azure e quindi selezionare **Aggiungi runbook**.</span><span class="sxs-lookup"><span data-stu-id="905c1-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="905c1-182">Selezionare **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="905c1-182">Select **Quick Create**.</span></span> <span data-ttu-id="905c1-183">Nome del runbook, quindi selezionare **PowerShell** come tipo di runbook hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="905c1-184">È necessario hello opzione tooadd una descrizione.</span><span class="sxs-lookup"><span data-stu-id="905c1-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="905c1-185">Fare infine clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="905c1-185">Finally, click **Create**.</span></span>

![Creare un runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="905c1-187">Incollare lo script di PowerShell nel riquadro dell'editor per il nuovo runbook hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="905c1-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="905c1-188">Riquadro editor hello scegliere **riquadro Test** tootest lo script.</span><span class="sxs-lookup"><span data-stu-id="905c1-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="905c1-189">Hello script viene eseguito senza errori, è possibile selezionarlo **pubblica**, ed è quindi possibile applicare una pianificazione per hello runbook nel riquadro di configurazione del runbook hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="905c1-190">Pipeline di controllo dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="905c1-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="905c1-191">Quando si configura un insieme di credenziali chiave, è possibile attivare il controllo toocollect accede toohello chiave insieme di credenziali di accesso richieste.</span><span class="sxs-lookup"><span data-stu-id="905c1-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="905c1-192">Questi log vengono archiviati in un apposito account di archiviazione di Azure e possono essere estratti, monitorati e analizzati.</span><span class="sxs-lookup"><span data-stu-id="905c1-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="905c1-193">Hello nello scenario seguente Usa funzioni di Azure, App per la logica di Azure e insieme di credenziali chiave audit log toocreate toosend una pipeline tramite posta elettronica quando un'app che corrisponde a hello app ID dell'app web hello recupera i segreti dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="905c1-194">È prima di tutto necessario abilitare la registrazione per l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="905c1-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="905c1-195">Questa operazione può essere eseguita tramite i seguenti comandi PowerShell hello (è possibile visualizzare i dettagli completi [chiave dell'insieme di credenziali-registrazione](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="905c1-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="905c1-196">Dopo questa opzione è abilitata, i log di controllo Avvia la raccolta in hello designato account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="905c1-197">Questi log contengono eventi relativi alla modalità di accesso all'insieme di credenziali delle chiavi, a quando avviene l'accesso e a chi lo esegue.</span><span class="sxs-lookup"><span data-stu-id="905c1-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="905c1-198">È possibile accedere a informazioni di registrazione 10 minuti dopo l'operazione di insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="905c1-199">ma in genere saranno disponibili anche prima.</span><span class="sxs-lookup"><span data-stu-id="905c1-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="905c1-200">passaggio successivo Hello è troppo[creare una coda di Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="905c1-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="905c1-201">Questa è la posizione in cui verrà eseguito il push dei log di controllo dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="905c1-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="905c1-202">Quando i messaggi di log di controllo hello presenti nella coda di hello, hello logica app li preleva e interviene su di essi.</span><span class="sxs-lookup"><span data-stu-id="905c1-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="905c1-203">Creare un bus di servizio con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="905c1-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="905c1-204">Creare uno spazio dei nomi del Bus di servizio (se si dispone già di quello che si desidera toouse a tale scopo, ignorare tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="905c1-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="905c1-205">Selezionare il bus di servizio toohello hello portale di Azure e spazio dei nomi selezionare hello coda hello toocreate in.</span><span class="sxs-lookup"><span data-stu-id="905c1-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="905c1-206">Selezionare **New** e scegliere **Service Bus > coda** e immettere i dettagli di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="905c1-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="905c1-207">Selezionare informazioni di connessione del Bus di servizio hello scegliendo hello dello spazio dei nomi e fare clic su **informazioni di connessione**.</span><span class="sxs-lookup"><span data-stu-id="905c1-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="905c1-208">Queste informazioni è necessario per la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="905c1-209">Successivamente, [creare una funzione Azure](../azure-functions/functions-create-first-azure-function.md) toopoll insieme di credenziali chiave interno hello account di archiviazione e registri prelevati nuovi eventi.</span><span class="sxs-lookup"><span data-stu-id="905c1-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="905c1-210">Questa funzione verrà attivata in base alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="905c1-211">toocreate una funzione di Azure, scegliere **nuovo > funzione App** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="905c1-212">Durante la creazione è possibile usare un piano di hosting esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="905c1-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="905c1-213">È anche possibile optare per l'hosting dinamico.</span><span class="sxs-lookup"><span data-stu-id="905c1-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="905c1-214">Ulteriori informazioni sulla funzione Opzioni di hosting sono reperibile in [come tooscale Azure funzioni](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="905c1-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="905c1-215">Quando viene creato hello funzione Azure, passare tooit e scegliere un timer di funzione e C\#.</span><span class="sxs-lookup"><span data-stu-id="905c1-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="905c1-216">quindi fare clic su **Creare questa funzione**.</span><span class="sxs-lookup"><span data-stu-id="905c1-216">Then click **Create this function**.</span></span>

![Pannello iniziale di Funzioni di Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="905c1-218">In hello **sviluppare** scheda, sostituire il codice di run.csx hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="905c1-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="905c1-219">Le variabili di hello tooreplace che all'hello precedente account di archiviazione tooyour toopoint codice in cui vengono scritti i log di insieme di credenziali chiave di hello, creato in precedenza, il bus di servizio hello e hello registri del percorso specifico toohello insieme di credenziali chiave di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="905c1-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="905c1-220">funzione Hello preleva hello ultimo file di log dall'account di archiviazione hello in cui vengono scritti i log dell'insieme di credenziali chiave di hello, acrobazie hello gli eventi più recenti da tale file, e li inserisce tooa della coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="905c1-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="905c1-221">Un singolo file potrebbero essere più eventi, è necessario creare un file sync.txt funzione hello prende in considerazione anche toodetermine hello timestamp dell'hello ultimo evento che è stato prelevato.</span><span class="sxs-lookup"><span data-stu-id="905c1-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="905c1-222">In questo modo si garantisce che non push hello stesso evento più volte.</span><span class="sxs-lookup"><span data-stu-id="905c1-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="905c1-223">Questo file sync.txt contiene un timestamp per l'evento è stato rilevato ultimo hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="905c1-224">i registri, quando caricati, Hello hanno toobe ordinati in base a hello timestamp tooensure vengono ordinati correttamente.</span><span class="sxs-lookup"><span data-stu-id="905c1-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="905c1-225">Per questa funzione è fare riferimento a un paio di librerie aggiuntive che non sono disponibili predefinito hello nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="905c1-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="905c1-226">tooinclude, abbiamo bisogno di funzioni di Azure toopull loro tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="905c1-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="905c1-227">Scegliere hello **Visualizza file** opzione.</span><span class="sxs-lookup"><span data-stu-id="905c1-227">Choose hello **View Files** option.</span></span>

![Opzione Visualizza file](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="905c1-229">Aggiungere poi un file denominato project.json con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="905c1-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="905c1-230">Al momento **salvare**, le funzioni di Azure verranno scaricati i file binari hello necessario.</span><span class="sxs-lookup"><span data-stu-id="905c1-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="905c1-231">Passare toohello **integrazione** scheda e assegnare il parametro di timer hello toouse un nome significativo all'interno di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="905c1-232">In hello codice precedente, è previsto che hello timer toobe chiamato *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="905c1-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="905c1-233">Specificare un [espressione CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) nel modo seguente: 0 \* \* \* \* \* di timer hello che causerà toorun funzione hello una volta al minuto.</span><span class="sxs-lookup"><span data-stu-id="905c1-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="905c1-234">Hello nella stessa **integrazione** scheda, aggiungere un input di tipo hello **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="905c1-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="905c1-235">Questo punterà toohello sync.txt file che contiene il timestamp di hello dell'ultimo evento hello esaminato dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="905c1-236">Questo sarà disponibile nell'ambito di funzione hello in base al nome di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="905c1-237">Nel codice precedente di hello, hello input di archiviazione Blob di Azure prevede hello parametro nome toobe *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="905c1-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="905c1-238">Scegliere l'account di archiviazione hello in cui risiederà file sync.txt hello (potrebbe essere hello stesso o in un altro account di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="905c1-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="905c1-239">Nel campo percorso hello, specificare il percorso di hello in cui si trova il file hello in formato hello {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="905c1-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="905c1-240">Aggiungere un output di tipo hello *archiviazione Blob di Azure* output.</span><span class="sxs-lookup"><span data-stu-id="905c1-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="905c1-241">Questo punterà toohello sync.txt file definito nell'input hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="905c1-242">Viene utilizzato da hello funzione toowrite hello timestamp dell'ultimo evento hello esaminato.</span><span class="sxs-lookup"><span data-stu-id="905c1-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="905c1-243">il codice precedente Hello prevede toobe questo parametro chiamato *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="905c1-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="905c1-244">A questo punto, la funzione hello è pronta.</span><span class="sxs-lookup"><span data-stu-id="905c1-244">At this point, hello function is ready.</span></span> <span data-ttu-id="905c1-245">Verificare che tooswitch indietro toohello **sviluppare** scheda e salvare il codice hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="905c1-246">Esaminare la finestra di output di hello per gli errori di compilazione e correggerle di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="905c1-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="905c1-247">Se il codice hello viene compilato, codice hello deve ora controllare i registri di insieme di credenziali chiave hello ogni minuto e inserendo nuovi eventi in hello definita coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="905c1-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="905c1-248">Dovrebbe essere informazioni di registrazione scrivono finestra log toohello ogni volta che viene attivata la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="905c1-249">App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="905c1-249">Azure logic app</span></span>
<span data-ttu-id="905c1-250">Successivamente è necessario creare un'app di Azure logica che preleva eventi hello funzione hello è push toohello della coda del Bus di servizio, analizza il contenuto di hello e invia un messaggio di posta elettronica in base a una condizione viene cercata la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="905c1-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="905c1-251">[Creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md) passando troppo**nuovo > App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="905c1-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="905c1-252">Una volta creato, hello logica app passare tooit e scegliere **modifica**.</span><span class="sxs-lookup"><span data-stu-id="905c1-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="905c1-253">Nell'editor di hello logica app scegliere **coda di Service Bus** e immettere tooconnect di credenziali del Bus di servizio è toohello coda.</span><span class="sxs-lookup"><span data-stu-id="905c1-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Bus di servizio dell'app per la logica di Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="905c1-255">Scegliere quindi **Aggiungi una condizione**.</span><span class="sxs-lookup"><span data-stu-id="905c1-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="905c1-256">Nella condizione di hello, passare toohello editor avanzato e immettere hello nel codice seguente, sostituendo APP_ID con hello APP_ID effettivo dell'app web:</span><span class="sxs-lookup"><span data-stu-id="905c1-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="905c1-257">Questa espressione restituisce essenzialmente **false** se hello *appid* da hello evento in entrata (ovvero il corpo di hello del messaggio hello del Bus di servizio) è non hello *appid* di hello app.</span><span class="sxs-lookup"><span data-stu-id="905c1-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="905c1-258">Creare ora un'azione in **Se no, non fare nulla** .</span><span class="sxs-lookup"><span data-stu-id="905c1-258">Now, create an action under **If no, do nothing**.</span></span>

![Scelta dell'azione per l'app per la logica di Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="905c1-260">Per l'azione di hello, scegliere **Office 365 - invio di email**.</span><span class="sxs-lookup"><span data-stu-id="905c1-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="905c1-261">Compilare hello campi toocreate toosend un messaggio di posta elettronica quando hello definito condizione restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="905c1-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="905c1-262">Se non si dispone di Office 365, da prendere in considerazione alternative tooachieve hello stessi risultati.</span><span class="sxs-lookup"><span data-stu-id="905c1-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="905c1-263">A questo punto, si dispone di una pipeline tooend fine che cerca i log di controllo nuovo insieme di credenziali chiave di una volta al minuto.</span><span class="sxs-lookup"><span data-stu-id="905c1-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="905c1-264">Inserisce nuovi registri trova tooa coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="905c1-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="905c1-265">app per la logica Hello viene attivata quando un nuovo messaggio inserita nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="905c1-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="905c1-266">Se hello *appid* all'interno di hello evento non corrisponde all'ID di app hello di hello applicazione chiamante, invia un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="905c1-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
