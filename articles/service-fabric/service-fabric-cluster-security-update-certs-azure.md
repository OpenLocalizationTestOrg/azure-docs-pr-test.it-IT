---
title: i certificati aaaManage in un cluster di Azure Service Fabric | Documenti Microsoft
description: Viene descritto come tooadd nuovi certificati, il certificato di rollover e Rimuovi certificato tooor da un cluster di Service Fabric.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="739ea-103">Aggiungere o rimuovere certificati per un cluster Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="739ea-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="739ea-104">Si consiglia di acquisire familiarità con l'utilizzo di certificati x. 509 Service Fabric e acquisire familiarità con hello [degli scenari di sicurezza Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="739ea-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="739ea-105">È necessario comprendere cos'è un certificato del cluster e a cosa serve prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="739ea-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="739ea-106">Consente di infrastruttura servizio che specificare che due cluster i certificati, uno primario e secondario, quando si configura certificato di sicurezza durante la creazione del cluster nei certificati tooclient aggiunta.</span><span class="sxs-lookup"><span data-stu-id="739ea-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="739ea-107">Fare riferimento troppo[creazione di un cluster di azure mediante portale](service-fabric-cluster-creation-via-portal.md) o [creazione di un cluster di azure con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) per informazioni dettagliate sulla configurazione al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="739ea-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="739ea-108">Se si specifica un solo certificato cluster al momento della creazione, che viene quindi utilizzato come certificato primario hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="739ea-109">Dopo la creazione del cluster è possibile aggiungere un nuovo certificato come secondario.</span><span class="sxs-lookup"><span data-stu-id="739ea-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="739ea-110">Per un cluster protetto, è sempre necessario certificato almeno un cluster valido (non revocati e non scaduti) (primario o secondario) distribuito (in caso contrario hello cluster si arresterà).</span><span class="sxs-lookup"><span data-stu-id="739ea-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="739ea-111">90 giorni prima della scadenza, di raggiungere tutti i certificati validi sistema hello genera una traccia di avviso e anche un evento di avviso di integrità nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="739ea-112">Attualmente non sono disponibili messaggi di posta elettronica o altre notifiche inviati da Service Fabric su questo argomento.</span><span class="sxs-lookup"><span data-stu-id="739ea-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="739ea-113">Aggiungere un certificato secondario del cluster tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="739ea-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="739ea-114">Impossibile aggiungere il certificato secondario del cluster tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="739ea-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="739ea-115">Hai toouse Azure powershell per tale.</span><span class="sxs-lookup"><span data-stu-id="739ea-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="739ea-116">processo Hello descritta più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="739ea-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="739ea-117">Scambiare certificati cluster hello tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="739ea-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="739ea-118">Dopo avere distribuito correttamente un certificato secondario del cluster, se si desidera tooswap hello primario e secondario, quindi passare pannello sicurezza toohello e selezionare hello 'Swap primario' opzione hello contesto menu tooswap hello secondario cert con certificato primario Hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Scambiare i certificati][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="739ea-120">Rimuovere un certificato di cluster tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="739ea-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="739ea-121">Per un cluster sicura, occorre sempre almeno un valido (non revocato e non scaduto) certificato (primario o secondario) distribuito in caso contrario, hello cluster si arresterà.</span><span class="sxs-lookup"><span data-stu-id="739ea-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="739ea-122">un certificato secondario venga utilizzato per la protezione del cluster, pannello di navigazione toohello sicurezza e selezionare hello 'Delete' opzione dal menu di scelta rapida hello sul certificato secondario hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="739ea-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="739ea-123">Se si intende certificato hello tooremove che è contrassegnato come primario, sarà necessario tooswap con hello secondario prima e quindi eliminare hello secondario dopo il completamento dell'aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="739ea-124">Aggiungere un certificato secondario tramite PowerShell per Resource Manager</span><span class="sxs-lookup"><span data-stu-id="739ea-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="739ea-125">Questi passaggi presuppongono che si ha familiarità con il funzionamento di gestione risorse e avere distribuito almeno un cluster Service Fabric utilizzando un modello di gestione delle risorse e modello hello utilizzato tooset di cluster hello utili.</span><span class="sxs-lookup"><span data-stu-id="739ea-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="739ea-126">Si presuppone anche che si abbia dimestichezza con l'uso di JSON.</span><span class="sxs-lookup"><span data-stu-id="739ea-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="739ea-127">Se si sta cercando un modello di esempio e i parametri che è possibile utilizzare toofollow lungo o come un punto di partenza, quindi scaricarlo da questo [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="739ea-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="739ea-128">Modificare il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="739ea-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="739ea-129">Per facilitare la seguente lungo, esempio 5-VM-1-NodeTypes-Secure_Step2.JSON contiene tutte le modifiche di hello che verrà rilasciato.</span><span class="sxs-lookup"><span data-stu-id="739ea-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="739ea-130">esempio Hello è disponibile in [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="739ea-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="739ea-131">**Verificare che toofollow tutti i passaggi di hello**</span><span class="sxs-lookup"><span data-stu-id="739ea-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="739ea-132">**Passaggio 1:** apre un modello di gestione risorse di hello utilizzato toodeploy del Cluster.</span><span class="sxs-lookup"><span data-stu-id="739ea-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="739ea-133">Se è stato scaricato l'esempio hello da hello sopra repository, quindi utilizzare 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un cluster protetto e quindi aprire il modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="739ea-134">**Passaggio 2:** Aggiungi **due nuovi parametri** "secCertificateThumbprint" e "secCertificateUrlValue" di tipo "stringa" toohello sezione relativa ai parametri del modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="739ea-135">È possibile copiare hello seguente frammento di codice e aggiungerlo toohello modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="739ea-136">A seconda del modello di origine hello si potrebbe già dispone di tali, in tal caso, spostare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="739ea-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="739ea-137">**Passaggio 3:** apportare modifiche toohello **Microsoft.ServiceFabric/clusters** risorse - individuare una definizione di risorsa "Microsoft.ServiceFabric/clusters" hello nel modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="739ea-138">In proprietà di tale definizione, si noterà "Certificato" JSON tag, che dovrebbe essere simile hello frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="739ea-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="739ea-139">Aggiungere un nuovo tag "thumbprintSecondary" e assegnare un valore "[parameters('secCertificateThumbprint')]".</span><span class="sxs-lookup"><span data-stu-id="739ea-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="739ea-140">In tal caso, dopo la definizione di risorsa hello dovrebbe essere simile hello seguente (a seconda dell'origine del modello di hello, potrebbe non essere esattamente come hello frammento di codice riportato di seguito).</span><span class="sxs-lookup"><span data-stu-id="739ea-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="739ea-141">Se si desidera troppo**cert hello rollover**, quindi specificare nuovo certificato hello come database primario corrente hello primario e in movimento come database secondario.</span><span class="sxs-lookup"><span data-stu-id="739ea-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="739ea-142">Di conseguenza il rollover di hello del corrente certificato primario toohello nuovo certificato in un unico passaggio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="739ea-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="739ea-143">**Passaggio 4:** apportare modifiche troppo**tutti** hello **Microsoft.Compute/virtualMachineScaleSets** le definizioni delle risorse - individuare hello Microsoft.Compute/virtualMachineScaleSets risorsa definizione.</span><span class="sxs-lookup"><span data-stu-id="739ea-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="739ea-144">Scorrere toohello "publisher": "Microsoft.Azure.ServiceFabric" in "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="739ea-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="739ea-145">Nelle impostazioni del server di pubblicazione dell'infrastruttura servizio hello, dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="739ea-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="739ea-147">Aggiungere hello nuovo cert voci tooit</span><span class="sxs-lookup"><span data-stu-id="739ea-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="739ea-148">proprietà Hello dovrebbe essere simile al seguente</span><span class="sxs-lookup"><span data-stu-id="739ea-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="739ea-150">Se si desidera troppo**cert hello rollover**, quindi specificare nuovo certificato hello come database primario corrente hello primario e in movimento come database secondario.</span><span class="sxs-lookup"><span data-stu-id="739ea-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="739ea-151">Di conseguenza il rollover di hello del corrente certificato toohello nuovo certificato in un unico passaggio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="739ea-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="739ea-152">proprietà Hello dovrebbe essere simile al seguente</span><span class="sxs-lookup"><span data-stu-id="739ea-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="739ea-154">**Passaggio 5:** apportare modifiche troppo**tutti** hello **Microsoft.Compute/virtualMachineScaleSets** le definizioni delle risorse - individuare hello Microsoft.Compute/virtualMachineScaleSets risorsa definizione.</span><span class="sxs-lookup"><span data-stu-id="739ea-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="739ea-155">Scorrere toohello "vaultCertificates":, in "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="739ea-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="739ea-156">Dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="739ea-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="739ea-158">Aggiungere tooit secCertificateUrlValue hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="739ea-159">Utilizzare hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="739ea-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="739ea-160">Ora hello Json risultante dovrebbe essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="739ea-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="739ea-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="739ea-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="739ea-162">Assicurarsi che nel modello sono ripetuti i passaggi 4 e 5 per tutte le definizioni di risorse Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="739ea-163">Se non è disponibile uno di essi, non verrà installato il certificato di hello in tale VMSS e sarà necessario ottenere risultati imprevisti del cluster, inclusi i cluster hello procedendo verso il basso (se si finisce con nessun certificato valido di che tale cluster hello è possibile utilizzare per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="739ea-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="739ea-164">È quindi importante verificare, prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="739ea-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="739ea-165">Modificare i file tooreflect hello nuovi parametri di modello che è stato aggiunto in precedenza</span><span class="sxs-lookup"><span data-stu-id="739ea-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="739ea-166">Se si utilizza l'esempio hello hello [repository git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow insieme, è possibile avviare le modifiche toomake hello esempio 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="739ea-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="739ea-167">Modifica il parametro di modello di gestione risorse File, aggiungere hello due nuovi parametri per secCertificateThumbprint e secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="739ea-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="739ea-168">Distribuire hello modello tooAzure</span><span class="sxs-lookup"><span data-stu-id="739ea-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="739ea-169">Si sono ora pronti toodeploy tooAzure il modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="739ea-170">Aprire il prompt dei comandi di Azure PowerShell versione 1+.</span><span class="sxs-lookup"><span data-stu-id="739ea-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="739ea-171">Accedi tooyour Account Azure e selezionare la sottoscrizione di azure specifico di hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="739ea-172">Questo è un passaggio importante per gli amministratori che dispongono di accesso toomore rispetto a una sottoscrizione di azure.</span><span class="sxs-lookup"><span data-stu-id="739ea-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="739ea-173">Test hello modello precedente toodeploying è.</span><span class="sxs-lookup"><span data-stu-id="739ea-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="739ea-174">Utilizzare hello stesso gruppo di risorse del cluster attualmente distribuito.</span><span class="sxs-lookup"><span data-stu-id="739ea-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="739ea-175">Distribuire un gruppo di risorse tooyour modello hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="739ea-176">Utilizzare hello stesso gruppo di risorse del cluster attualmente distribuito.</span><span class="sxs-lookup"><span data-stu-id="739ea-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="739ea-177">Eseguire il comando di New-AzureRmResourceGroupDeployment hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="739ea-178">Non è necessaria la modalità di hello toospecify, poiché il valore predefinito di hello è **incrementale**.</span><span class="sxs-lookup"><span data-stu-id="739ea-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="739ea-179">Se si imposta la modalità tooComplete, è possibile eliminare inavvertitamente le risorse che non sono presenti nel modello.</span><span class="sxs-lookup"><span data-stu-id="739ea-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="739ea-180">Non usarla in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="739ea-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="739ea-181">Ecco un riempimento all'esempio di hello powershell stessa.</span><span class="sxs-lookup"><span data-stu-id="739ea-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="739ea-182">Una volta completata la distribuzione di hello, connettersi utilizzando cluster tooyour hello nuovo certificato ed eseguire alcune query.</span><span class="sxs-lookup"><span data-stu-id="739ea-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="739ea-183">Se si è in grado di toodo.</span><span class="sxs-lookup"><span data-stu-id="739ea-183">If you are able toodo.</span></span> <span data-ttu-id="739ea-184">È quindi possibile eliminare il vecchio certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="739ea-185">Se si utilizza un certificato autofirmato, non dimenticare tooimport loro nell'archivio certificati locale TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="739ea-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="739ea-186">Di seguito è cluster sicuro tooa tooconnect comando hello di riferimento rapido</span><span class="sxs-lookup"><span data-stu-id="739ea-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="739ea-187">Di seguito è l'integrità del cluster hello comando tooget di riferimento rapido</span><span class="sxs-lookup"><span data-stu-id="739ea-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="739ea-188">Distribuzione di cluster toohello certificati di applicazione.</span><span class="sxs-lookup"><span data-stu-id="739ea-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="739ea-189">È possibile utilizzare hello stessi passaggi come descritto in 5 passaggi sopra toohave hello certificati distribuiti da un toohello keyvault nodi.</span><span class="sxs-lookup"><span data-stu-id="739ea-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="739ea-190">È sufficiente definire e usare parametri diversi.</span><span class="sxs-lookup"><span data-stu-id="739ea-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="739ea-191">Aggiunta o rimozione di certificati client</span><span class="sxs-lookup"><span data-stu-id="739ea-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="739ea-192">I certificati di addizione toohello cluster, è possibile aggiungere operazioni di gestione tooperform i certificati client in un cluster di service fabric.</span><span class="sxs-lookup"><span data-stu-id="739ea-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="739ea-193">È possibile aggiungere due tipi di certificati client, Amministratore o Sola lettura,</span><span class="sxs-lookup"><span data-stu-id="739ea-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="739ea-194">Quindi possono essere utilizzati toocontrol accesso toohello admin operazioni e le operazioni di Query nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="739ea-195">Per impostazione predefinita, i certificati di hello cluster vengono aggiunti toohello Admin certificati elenco consentito.</span><span class="sxs-lookup"><span data-stu-id="739ea-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="739ea-196">È possibile specificare un numero qualsiasi di certificati client.</span><span class="sxs-lookup"><span data-stu-id="739ea-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="739ea-197">Ogni aggiunta o l'eliminazione di risultati in un cluster di configurazione aggiornamento toohello service fabric</span><span class="sxs-lookup"><span data-stu-id="739ea-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="739ea-198">Aggiunta di certificati client Amministratore o Sola lettura tramite il portale</span><span class="sxs-lookup"><span data-stu-id="739ea-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="739ea-199">Passare a pannello sicurezza toohello e selezionare hello '+ autenticazione' pulsante sopra pannello sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="739ea-200">Nel Pannello di "Aggiungere Authentication" hello, scegliere 'Tipo di autenticazione' - 'Client di sola lettura' o ' Admin' hello</span><span class="sxs-lookup"><span data-stu-id="739ea-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="739ea-201">Scegliere il metodo di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="739ea-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="739ea-202">Se è necessario cercare questo certificato utilizzando il nome di soggetto hello o un'identificazione personale hello indica tooService dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="739ea-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="739ea-203">In generale, non è un metodo di autorizzazione buona pratica toouse hello del nome soggetto.</span><span class="sxs-lookup"><span data-stu-id="739ea-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Aggiungere il certificato client][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="739ea-205">Eliminazione di certificati Client - Admin o sola lettura tramite hello portale</span><span class="sxs-lookup"><span data-stu-id="739ea-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="739ea-206">un certificato secondario venga utilizzato per la protezione del cluster, pannello di navigazione toohello sicurezza e selezionare hello 'Delete' opzione dal menu di scelta rapida hello certificato specifico hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="739ea-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="739ea-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="739ea-207">Next steps</span></span>
<span data-ttu-id="739ea-208">Per ulteriori informazioni sulla gestione del cluster, leggere questi articoli:</span><span class="sxs-lookup"><span data-stu-id="739ea-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="739ea-209">Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente</span><span class="sxs-lookup"><span data-stu-id="739ea-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="739ea-210">Configurare l’accesso in base al ruolo per i client</span><span class="sxs-lookup"><span data-stu-id="739ea-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


