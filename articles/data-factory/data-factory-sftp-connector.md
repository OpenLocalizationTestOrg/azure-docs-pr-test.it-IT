---
title: aaaMove dati dal server SFTP con Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da un locale o un server SFTP cloud con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="7bd72-103">Spostare dati da un server SFTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7bd72-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="7bd72-104">In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da un tooa di server SFTP in locale/cloud supportato archivio dati sink.</span><span class="sxs-lookup"><span data-stu-id="7bd72-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="7bd72-105">In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.</span><span class="sxs-lookup"><span data-stu-id="7bd72-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="7bd72-106">Data factory di supporta attualmente solo lo spostamento di dati da tooother un server SFTP Archivia, ma non per lo spostamento dei dati da altri dati archivia server SFTP tooan.</span><span class="sxs-lookup"><span data-stu-id="7bd72-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="7bd72-107">Supporta i server SFTP locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="7bd72-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd72-108">Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente.</span><span class="sxs-lookup"><span data-stu-id="7bd72-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="7bd72-109">Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="7bd72-110">Scenari supportati e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="7bd72-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="7bd72-111">È possibile utilizzare questo SFTP connettore toocopy dati **entrambi i server SFTP e server SFTP locali cloud**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="7bd72-112">**Base** e **parametri SshPublicKey** tipi di autenticazione sono supportati durante la connessione server SFTP toohello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="7bd72-113">Quando si copiano dati da un server SFTP in locale, è necessario installare un Gateway di gestione di dati nell'ambiente locale hello/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7bd72-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="7bd72-114">Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) per dettagli sul gateway hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="7bd72-115">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per istruzioni dettagliate sulla configurazione di gateway hello e l'uso.</span><span class="sxs-lookup"><span data-stu-id="7bd72-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7bd72-116">introduttiva</span><span class="sxs-lookup"><span data-stu-id="7bd72-116">Getting started</span></span>
<span data-ttu-id="7bd72-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine SFTP usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="7bd72-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="7bd72-118">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="7bd72-119">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="7bd72-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="7bd72-120">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7bd72-121">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="7bd72-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="7bd72-122">Per esempi di JSON dati toocopy tooAzure server SFTP nell'archiviazione Blob, vedere [esempio JSON: copiare i dati da blob di tooAzure server SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7bd72-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7bd72-123">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="7bd72-123">Linked service properties</span></span>
<span data-ttu-id="7bd72-124">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooFTP collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="7bd72-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="7bd72-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bd72-125">Property</span></span> | <span data-ttu-id="7bd72-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bd72-126">Description</span></span> | <span data-ttu-id="7bd72-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7bd72-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7bd72-128">type</span><span class="sxs-lookup"><span data-stu-id="7bd72-128">type</span></span> | <span data-ttu-id="7bd72-129">proprietà di tipo Hello deve essere impostata troppo`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="7bd72-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="7bd72-130">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-130">Yes</span></span> |
| <span data-ttu-id="7bd72-131">host</span><span class="sxs-lookup"><span data-stu-id="7bd72-131">host</span></span> | <span data-ttu-id="7bd72-132">Nome o indirizzo IP del server SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="7bd72-133">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-133">Yes</span></span> |
| <span data-ttu-id="7bd72-134">port</span><span class="sxs-lookup"><span data-stu-id="7bd72-134">port</span></span> |<span data-ttu-id="7bd72-135">Porta su cui hello SFTP server è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="7bd72-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="7bd72-136">valore predefinito di Hello è: 21</span><span class="sxs-lookup"><span data-stu-id="7bd72-136">hello default value is: 21</span></span> |<span data-ttu-id="7bd72-137">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-137">No</span></span> |
| <span data-ttu-id="7bd72-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7bd72-138">authenticationType</span></span> |<span data-ttu-id="7bd72-139">Specificare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7bd72-139">Specify authentication type.</span></span> <span data-ttu-id="7bd72-140">Valori consentiti: **Base**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="7bd72-141">Fare riferimento troppo[tramite l'autenticazione di base](#using-basic-authentication) e [tramite SSH autenticazione a chiave pubblica](#using-ssh-public-key-authentication) sezioni su altre proprietà e gli esempi JSON rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="7bd72-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="7bd72-142">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-142">Yes</span></span> |
| <span data-ttu-id="7bd72-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="7bd72-143">skipHostKeyValidation</span></span> | <span data-ttu-id="7bd72-144">Specificare se tooskip chiave convalida dell'host.</span><span class="sxs-lookup"><span data-stu-id="7bd72-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="7bd72-145">No.</span><span class="sxs-lookup"><span data-stu-id="7bd72-145">No.</span></span> <span data-ttu-id="7bd72-146">Hello valore predefinito: false</span><span class="sxs-lookup"><span data-stu-id="7bd72-146">hello default value: false</span></span> |
| <span data-ttu-id="7bd72-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="7bd72-147">hostKeyFingerprint</span></span> | <span data-ttu-id="7bd72-148">Specificare impronte digitali hello della chiave host hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="7bd72-149">Sì se hello `skipHostKeyValidation` è impostato toofalse.</span><span class="sxs-lookup"><span data-stu-id="7bd72-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="7bd72-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7bd72-150">gatewayName</span></span> |<span data-ttu-id="7bd72-151">Nome di hello Gateway di gestione dati tooconnect tooan locale server SFTP.</span><span class="sxs-lookup"><span data-stu-id="7bd72-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="7bd72-152">Sì se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="7bd72-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="7bd72-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="7bd72-153">encryptedCredential</span></span> | <span data-ttu-id="7bd72-154">Server SFTP hello tooaccess credenziali crittografate.</span><span class="sxs-lookup"><span data-stu-id="7bd72-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="7bd72-155">Generati automaticamente quando si specifica l'autenticazione di base (password e nome utente) o parametri SshPublicKey (nome utente + percorso della chiave privata o contenuto) nella copia guidata o hello ClickOnce finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="7bd72-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="7bd72-156">No.</span><span class="sxs-lookup"><span data-stu-id="7bd72-156">No.</span></span> <span data-ttu-id="7bd72-157">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="7bd72-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="7bd72-158">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="7bd72-158">Using basic authentication</span></span>

<span data-ttu-id="7bd72-159">impostare l'autenticazione di base toouse, `authenticationType` come `Basic`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:</span><span class="sxs-lookup"><span data-stu-id="7bd72-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="7bd72-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bd72-160">Property</span></span> | <span data-ttu-id="7bd72-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bd72-161">Description</span></span> | <span data-ttu-id="7bd72-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7bd72-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7bd72-163">username</span><span class="sxs-lookup"><span data-stu-id="7bd72-163">username</span></span> | <span data-ttu-id="7bd72-164">Utente che dispone di server di accesso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="7bd72-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="7bd72-165">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-165">Yes</span></span> |
| <span data-ttu-id="7bd72-166">password</span><span class="sxs-lookup"><span data-stu-id="7bd72-166">password</span></span> | <span data-ttu-id="7bd72-167">Password per l'utente di hello (nomeutente).</span><span class="sxs-lookup"><span data-stu-id="7bd72-167">Password for hello user (username).</span></span> | <span data-ttu-id="7bd72-168">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="7bd72-169">Esempio: autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="7bd72-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="7bd72-170">Esempio: autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="7bd72-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="7bd72-171">Uso dell'autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="7bd72-171">Using SSH public key authentication</span></span>

<span data-ttu-id="7bd72-172">impostare toouse SSH autenticazione a chiave pubblica, `authenticationType` come `SshPublicKey`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:</span><span class="sxs-lookup"><span data-stu-id="7bd72-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="7bd72-173">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bd72-173">Property</span></span> | <span data-ttu-id="7bd72-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bd72-174">Description</span></span> | <span data-ttu-id="7bd72-175">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7bd72-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7bd72-176">username</span><span class="sxs-lookup"><span data-stu-id="7bd72-176">username</span></span> |<span data-ttu-id="7bd72-177">Utente che dispone di server di accesso toohello SFTP</span><span class="sxs-lookup"><span data-stu-id="7bd72-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="7bd72-178">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-178">Yes</span></span> |
| <span data-ttu-id="7bd72-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="7bd72-179">privateKeyPath</span></span> | <span data-ttu-id="7bd72-180">Specificare un percorso assoluto toohello file di chiave privata accessibile tale gateway.</span><span class="sxs-lookup"><span data-stu-id="7bd72-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="7bd72-181">Specificare entrambi hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="7bd72-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="7bd72-182">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="7bd72-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="7bd72-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="7bd72-183">privateKeyContent</span></span> | <span data-ttu-id="7bd72-184">Una stringa serializzata del contenuto di chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="7bd72-185">Hello Copia guidata è possibile leggere il file di chiave privata di hello ed estrarre automaticamente il contenuto di chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="7bd72-186">Se si utilizza qualsiasi altro strumento o SDK, è possibile utilizzare proprietà privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="7bd72-187">Specificare entrambi hello `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="7bd72-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="7bd72-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="7bd72-188">passPhrase</span></span> | <span data-ttu-id="7bd72-189">Specificare hello frase/password toodecrypt hello privati passkey se i file di chiave hello è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="7bd72-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="7bd72-190">Sì se il file di chiave privata di hello è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="7bd72-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="7bd72-191">Il connettore SFTP supporta solo chiavi OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="7bd72-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="7bd72-192">Assicurarsi che il file di chiave sia nel formato corretto hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="7bd72-193">È possibile utilizzare lo strumento Putty tooconvert dal formato tooOpenSSH *.ppk.</span><span class="sxs-lookup"><span data-stu-id="7bd72-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="7bd72-194">Esempio: Autenticazione SshPublicKey con chiave privata filePath</span><span class="sxs-lookup"><span data-stu-id="7bd72-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="7bd72-195">Esempio: Autenticazione SshPublicKey con contenuto della chiave privata</span><span class="sxs-lookup"><span data-stu-id="7bd72-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="7bd72-196">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="7bd72-196">Dataset properties</span></span>
<span data-ttu-id="7bd72-197">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="7bd72-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7bd72-198">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="7bd72-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="7bd72-199">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="7bd72-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="7bd72-200">Fornisce informazioni che sono il tipo di set di dati toohello specifico.</span><span class="sxs-lookup"><span data-stu-id="7bd72-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="7bd72-201">sezione Hello typeProperties per un set di dati di tipo **FileShare** set di dati è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd72-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="7bd72-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7bd72-202">Property</span></span> | <span data-ttu-id="7bd72-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bd72-203">Description</span></span> | <span data-ttu-id="7bd72-204">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7bd72-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bd72-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="7bd72-205">folderPath</span></span> |<span data-ttu-id="7bd72-206">Toohello sottocartella percorso.</span><span class="sxs-lookup"><span data-stu-id="7bd72-206">Sub path toohello folder.</span></span> <span data-ttu-id="7bd72-207">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="7bd72-208">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="7bd72-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="7bd72-209">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="7bd72-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="7bd72-210">Sì</span><span class="sxs-lookup"><span data-stu-id="7bd72-210">Yes</span></span> |
| <span data-ttu-id="7bd72-211">fileName</span><span class="sxs-lookup"><span data-stu-id="7bd72-211">fileName</span></span> |<span data-ttu-id="7bd72-212">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="7bd72-213">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="7bd72-214">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato:</span><span class="sxs-lookup"><span data-stu-id="7bd72-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="7bd72-215">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="7bd72-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="7bd72-216">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-216">No</span></span> |
| <span data-ttu-id="7bd72-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="7bd72-217">fileFilter</span></span> |<span data-ttu-id="7bd72-218">Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="7bd72-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="7bd72-219">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="7bd72-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="7bd72-220">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="7bd72-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="7bd72-221">Esempio 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="7bd72-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="7bd72-222">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="7bd72-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="7bd72-223">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="7bd72-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="7bd72-224">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-224">No</span></span> |
| <span data-ttu-id="7bd72-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="7bd72-225">partitionedBy</span></span> |<span data-ttu-id="7bd72-226">partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="7bd72-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="7bd72-227">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="7bd72-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="7bd72-228">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-228">No</span></span> |
| <span data-ttu-id="7bd72-229">format</span><span class="sxs-lookup"><span data-stu-id="7bd72-229">format</span></span> | <span data-ttu-id="7bd72-230">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7bd72-231">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="7bd72-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="7bd72-232">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="7bd72-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="7bd72-233">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="7bd72-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="7bd72-234">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-234">No</span></span> |
| <span data-ttu-id="7bd72-235">compressione</span><span class="sxs-lookup"><span data-stu-id="7bd72-235">compression</span></span> | <span data-ttu-id="7bd72-236">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="7bd72-237">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7bd72-238">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7bd72-239">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7bd72-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7bd72-240">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-240">No</span></span> |
| <span data-ttu-id="7bd72-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="7bd72-241">useBinaryTransfer</span></span> |<span data-ttu-id="7bd72-242">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="7bd72-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="7bd72-243">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="7bd72-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="7bd72-244">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="7bd72-244">Default value: True.</span></span> <span data-ttu-id="7bd72-245">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="7bd72-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="7bd72-246">No</span><span class="sxs-lookup"><span data-stu-id="7bd72-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="7bd72-247">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7bd72-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="7bd72-248">Uso della proprietà partionedBy</span><span class="sxs-lookup"><span data-stu-id="7bd72-248">Using partionedBy property</span></span>
<span data-ttu-id="7bd72-249">Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamica, il nome file per i dati della serie temporale con partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="7bd72-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="7bd72-250">È possibile farlo con le macro Data Factory di hello e variabile di sistema hello SliceStart, SliceEnd che indicano hello periodo di tempo logico per una sezione di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="7bd72-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="7bd72-251">toolearn sui set di dati serie ora, la pianificazione e le sezioni, vedere [la creazione di DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [la creazione di pipeline](data-factory-create-pipelines.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="7bd72-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="7bd72-252">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="7bd72-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="7bd72-253">In questo esempio {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="7bd72-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="7bd72-254">Hello SliceStart fa riferimento l'ora toostart sezione hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="7bd72-255">Hello folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="7bd72-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="7bd72-256">Esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="7bd72-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="7bd72-257">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="7bd72-257">Sample 2:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="7bd72-258">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="7bd72-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="7bd72-259">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="7bd72-259">Copy activity properties</span></span>
<span data-ttu-id="7bd72-260">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="7bd72-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7bd72-261">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="7bd72-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="7bd72-262">Mentre le proprietà di hello disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="7bd72-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="7bd72-263">Per attività di copia, le proprietà del tipo hello variano a seconda di hello tipi di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="7bd72-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7bd72-264">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="7bd72-264">Supported file and compression formats</span></span>
<span data-ttu-id="7bd72-265">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="7bd72-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="7bd72-266">Esempio JSON: Copiare i dati da blob di tooAzure server SFTP</span><span class="sxs-lookup"><span data-stu-id="7bd72-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="7bd72-267">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7bd72-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7bd72-268">Visualizzano come origine dei dati di toocopy da SFTP tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="7bd72-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="7bd72-269">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7bd72-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bd72-270">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="7bd72-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="7bd72-271">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="7bd72-272">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7bd72-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="7bd72-273">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd72-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="7bd72-274">Un servizio collegato di tipo [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="7bd72-275">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="7bd72-276">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="7bd72-277">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="7bd72-278">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7bd72-279">esempio Hello copia dati da un tooan server SFTP blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="7bd72-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="7bd72-280">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="7bd72-281">**Servizio collegato SFTP**</span><span class="sxs-lookup"><span data-stu-id="7bd72-281">**SFTP linked service**</span></span>

<span data-ttu-id="7bd72-282">Nell'esempio viene utilizzata l'autenticazione di base hello con nome utente e password in testo normale.</span><span class="sxs-lookup"><span data-stu-id="7bd72-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="7bd72-283">È inoltre possibile utilizzare uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="7bd72-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="7bd72-284">Autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="7bd72-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="7bd72-285">Autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="7bd72-285">SSH public key authentication</span></span>

<span data-ttu-id="7bd72-286">Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7bd72-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="7bd72-287">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="7bd72-287">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="7bd72-288">**Set di dati di input SFTP**</span><span class="sxs-lookup"><span data-stu-id="7bd72-288">**SFTP input dataset**</span></span>

<span data-ttu-id="7bd72-289">Questo set di dati si riferisce cartella SFTP toohello `mysharedfolder` e file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="7bd72-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="7bd72-290">Hello pipeline copie hello toohello destinazione file.</span><span class="sxs-lookup"><span data-stu-id="7bd72-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="7bd72-291">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="7bd72-292">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="7bd72-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="7bd72-293">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="7bd72-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7bd72-294">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="7bd72-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="7bd72-295">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bd72-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="7bd72-296">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="7bd72-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="7bd72-297">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="7bd72-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="7bd72-298">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7bd72-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="7bd72-299">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7bd72-299">Performance and Tuning</span></span>
<span data-ttu-id="7bd72-300">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="7bd72-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bd72-301">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bd72-301">Next Steps</span></span>
<span data-ttu-id="7bd72-302">Vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7bd72-302">See hello following articles:</span></span>

* <span data-ttu-id="7bd72-303">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="7bd72-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
