---
title: Spostare dati da un server SFTP usando Azure Data Factory | Microsoft Docs
description: Informazioni su come spostare dati da un server SFTP locale o cloud mediante Azure Data Factory.
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
ms.openlocfilehash: 3a73311342489af031ed2ea1489e56292ebf2e09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="5e30e-103">Spostare dati da un server SFTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5e30e-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="5e30e-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare dati da un server SFTP locale o cloud a un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="5e30e-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud SFTP server to a supported sink data store.</span></span> <span data-ttu-id="5e30e-105">Questo articolo si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con attività di copia e l'elenco degli archivi dati supportati come origini/sink.</span><span class="sxs-lookup"><span data-stu-id="5e30e-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="5e30e-106">Data Factory supporta attualmente solo lo spostamento di dati da un server SFTP ad altri archivi dati, non da altri archivi dati a un server SFTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-106">Data factory currently supports only moving data from an SFTP server to other data stores, but not for moving data from other data stores to an SFTP server.</span></span> <span data-ttu-id="5e30e-107">Supporta i server SFTP locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="5e30e-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="5e30e-108">L'attività di copia non elimina il file di origine dopo che è stato correttamente copiato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-108">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="5e30e-109">Se è necessario eliminare il file di origine dopo una copia con esito positivo, creare un'attività personalizzata per eliminare il file e usare l'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="5e30e-109">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="5e30e-110">Scenari supportati e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="5e30e-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="5e30e-111">È possibile usare questo connettore SFTP per copiare dati da **server cloud SFTP e SFTP locali**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-111">You can use this SFTP connector to copy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="5e30e-112">Quando ci si connette al server SFTP sono supportati i tipi di chiave di autenticazione **Base** e **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-112">**Basic** and **SshPublicKey** authentication types are supported when connecting to the SFTP server.</span></span>

<span data-ttu-id="5e30e-113">Quando si copiano dati da un server SFTP locale, è necessario installare un gateway di gestione dati nella VM di Azure o nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="5e30e-114">Per informazioni dettagliate sul gateway, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on the gateway.</span></span> <span data-ttu-id="5e30e-115">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla configurazione e sull'uso del gateway.</span><span class="sxs-lookup"><span data-stu-id="5e30e-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5e30e-116">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5e30e-116">Getting started</span></span>
<span data-ttu-id="5e30e-117">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine SFTP usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="5e30e-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="5e30e-118">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5e30e-119">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="5e30e-120">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5e30e-121">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5e30e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="5e30e-122">Per esempi JSON per copiare dati da server SFTP all'archivio BLOB di Azure, vedere la sezione [Esempio JSON: copiare i dati dal server SFTP in BLOB di Azure](#json-example-copy-data-from-sftp-server-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5e30e-122">For JSON samples to copy data from SFTP server to Azure Blob Storage, see [JSON Example: Copy data from SFTP server to Azure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5e30e-123">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="5e30e-123">Linked service properties</span></span>
<span data-ttu-id="5e30e-124">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato FTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-124">The following table provides description for JSON elements specific to FTP linked service.</span></span>

| <span data-ttu-id="5e30e-125">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e30e-125">Property</span></span> | <span data-ttu-id="5e30e-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e30e-126">Description</span></span> | <span data-ttu-id="5e30e-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5e30e-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e30e-128">type</span><span class="sxs-lookup"><span data-stu-id="5e30e-128">type</span></span> | <span data-ttu-id="5e30e-129">La proprietà type deve essere impostata su `Sftp`.</span><span class="sxs-lookup"><span data-stu-id="5e30e-129">The type property must be set to `Sftp`.</span></span> |<span data-ttu-id="5e30e-130">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-130">Yes</span></span> |
| <span data-ttu-id="5e30e-131">host</span><span class="sxs-lookup"><span data-stu-id="5e30e-131">host</span></span> | <span data-ttu-id="5e30e-132">Nome o indirizzo IP del server SFTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-132">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="5e30e-133">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-133">Yes</span></span> |
| <span data-ttu-id="5e30e-134">port</span><span class="sxs-lookup"><span data-stu-id="5e30e-134">port</span></span> |<span data-ttu-id="5e30e-135">Porta su cui è in ascolto il server SFTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-135">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="5e30e-136">Il valore predefinito è 21</span><span class="sxs-lookup"><span data-stu-id="5e30e-136">The default value is: 21</span></span> |<span data-ttu-id="5e30e-137">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-137">No</span></span> |
| <span data-ttu-id="5e30e-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5e30e-138">authenticationType</span></span> |<span data-ttu-id="5e30e-139">Specificare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-139">Specify authentication type.</span></span> <span data-ttu-id="5e30e-140">Valori consentiti: **Base**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="5e30e-141">Fare riferimento alle sezioni [Uso dell'autenticazione di base](#using-basic-authentication) e [Uso dell'autenticazione con chiave pubblica SSH](#using-ssh-public-key-authentication) rispettivamente per vedere altre proprietà ed esempi JSON.</span><span class="sxs-lookup"><span data-stu-id="5e30e-141">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="5e30e-142">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-142">Yes</span></span> |
| <span data-ttu-id="5e30e-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="5e30e-143">skipHostKeyValidation</span></span> | <span data-ttu-id="5e30e-144">Specificare se si desidera ignorare la convalida tramite della chiave host.</span><span class="sxs-lookup"><span data-stu-id="5e30e-144">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="5e30e-145">No.</span><span class="sxs-lookup"><span data-stu-id="5e30e-145">No.</span></span> <span data-ttu-id="5e30e-146">Il valore predefinito è: falso</span><span class="sxs-lookup"><span data-stu-id="5e30e-146">The default value: false</span></span> |
| <span data-ttu-id="5e30e-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="5e30e-147">hostKeyFingerprint</span></span> | <span data-ttu-id="5e30e-148">Specificare le impronte digitali della chiave host.</span><span class="sxs-lookup"><span data-stu-id="5e30e-148">Specify the finger print of the host key.</span></span> | <span data-ttu-id="5e30e-149">Sì se `skipHostKeyValidation` è impostato su falso.</span><span class="sxs-lookup"><span data-stu-id="5e30e-149">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="5e30e-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5e30e-150">gatewayName</span></span> |<span data-ttu-id="5e30e-151">Nome del gateway di gestione dati per connettersi a un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-151">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="5e30e-152">Sì se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="5e30e-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="5e30e-153">encryptedCredential</span></span> | <span data-ttu-id="5e30e-154">Credenziali crittografate per accedere al server SFTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-154">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="5e30e-155">Generato automaticamente quando si specifica l'autenticazione di base (nome utente e password) o l'autenticazione SshPublicKey (nome utente e percorso della chiave privato o contenuto) nella copia guidata o nella finestra di dialogo popup ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="5e30e-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="5e30e-156">No.</span><span class="sxs-lookup"><span data-stu-id="5e30e-156">No.</span></span> <span data-ttu-id="5e30e-157">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="5e30e-158">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="5e30e-158">Using basic authentication</span></span>

<span data-ttu-id="5e30e-159">Per usare l'autenticazione di base, impostare `authenticationType` come `Basic` e specificare le proprietà seguenti oltre a quelle generiche del connettore SFTP introdotte nell'ultima sezione:</span><span class="sxs-lookup"><span data-stu-id="5e30e-159">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="5e30e-160">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e30e-160">Property</span></span> | <span data-ttu-id="5e30e-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e30e-161">Description</span></span> | <span data-ttu-id="5e30e-162">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5e30e-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e30e-163">username</span><span class="sxs-lookup"><span data-stu-id="5e30e-163">username</span></span> | <span data-ttu-id="5e30e-164">Utente che ha accesso al server SFTP.</span><span class="sxs-lookup"><span data-stu-id="5e30e-164">User who has access to the SFTP server.</span></span> |<span data-ttu-id="5e30e-165">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-165">Yes</span></span> |
| <span data-ttu-id="5e30e-166">password</span><span class="sxs-lookup"><span data-stu-id="5e30e-166">password</span></span> | <span data-ttu-id="5e30e-167">Password per l'utente (nome utente).</span><span class="sxs-lookup"><span data-stu-id="5e30e-167">Password for the user (username).</span></span> | <span data-ttu-id="5e30e-168">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="5e30e-169">Esempio: autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="5e30e-169">Example: Basic authentication</span></span>
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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="5e30e-170">Esempio: autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="5e30e-170">Example: Basic authentication with encrypted credential</span></span>

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

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="5e30e-171">Uso dell'autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="5e30e-171">Using SSH public key authentication</span></span>

<span data-ttu-id="5e30e-172">Per usare l'autenticazione con chiave pubblica SSH, impostare `authenticationType` su `SshPublicKey` e specificare le proprietà seguenti oltre a quelle generiche del connettore SFTP presentate nell'ultima sezione:</span><span class="sxs-lookup"><span data-stu-id="5e30e-172">To use SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="5e30e-173">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e30e-173">Property</span></span> | <span data-ttu-id="5e30e-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e30e-174">Description</span></span> | <span data-ttu-id="5e30e-175">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5e30e-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e30e-176">username</span><span class="sxs-lookup"><span data-stu-id="5e30e-176">username</span></span> |<span data-ttu-id="5e30e-177">Utente che ha accesso al server SFTP</span><span class="sxs-lookup"><span data-stu-id="5e30e-177">User who has access to the SFTP server</span></span> |<span data-ttu-id="5e30e-178">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-178">Yes</span></span> |
| <span data-ttu-id="5e30e-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="5e30e-179">privateKeyPath</span></span> | <span data-ttu-id="5e30e-180">Specificare un percorso assoluto al file di chiave privato a cui il gateway può accedere.</span><span class="sxs-lookup"><span data-stu-id="5e30e-180">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="5e30e-181">Specificare `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="5e30e-181">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="5e30e-182">Applicare solo se si copiano i dati da un server SFTP locale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="5e30e-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="5e30e-183">privateKeyContent</span></span> | <span data-ttu-id="5e30e-184">Una stringa serializzata del contenuto di chiave privata.</span><span class="sxs-lookup"><span data-stu-id="5e30e-184">A serialized string of the private key content.</span></span> <span data-ttu-id="5e30e-185">La copia guidata può leggere il file di chiave privata ed estrarre automaticamente il contenuto della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="5e30e-185">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="5e30e-186">Se si usa un qualsiasi altro strumento/SDK, usare la proprietà privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="5e30e-186">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="5e30e-187">Specificare `privateKeyPath` o `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="5e30e-187">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="5e30e-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="5e30e-188">passPhrase</span></span> | <span data-ttu-id="5e30e-189">Specificare la passphrase o la password per decrittografare la chiave privata se il file della chiave è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="5e30e-189">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="5e30e-190">Sì se il file della chiave privata è protetto da una passphrase.</span><span class="sxs-lookup"><span data-stu-id="5e30e-190">Yes if the private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="5e30e-191">Il connettore SFTP supporta solo chiavi OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="5e30e-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="5e30e-192">Assicurarsi che il file della chiave sia nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="5e30e-192">Make sure your key file is in the proper format.</span></span> <span data-ttu-id="5e30e-193">Per eseguire una conversione dal formato ppk al formato OpenSSH, è possibile usare lo strumento Putty.</span><span class="sxs-lookup"><span data-stu-id="5e30e-193">You can use Putty tool to convert from .ppk to OpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="5e30e-194">Esempio: Autenticazione SshPublicKey con chiave privata filePath</span><span class="sxs-lookup"><span data-stu-id="5e30e-194">Example: SshPublicKey authentication using private key filePath</span></span>

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="5e30e-195">Esempio: Autenticazione SshPublicKey con contenuto della chiave privata</span><span class="sxs-lookup"><span data-stu-id="5e30e-195">Example: SshPublicKey authentication using private key content</span></span>

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
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="5e30e-196">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="5e30e-196">Dataset properties</span></span>
<span data-ttu-id="5e30e-197">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-197">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5e30e-198">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="5e30e-199">La sezione **typeProperties** è diversa per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-199">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="5e30e-200">Fornisce informazioni specifiche del tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-200">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="5e30e-201">La sezione typeProperties per un set di dati di tipo **FileShare** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e30e-201">The typeProperties section for a dataset of type **FileShare** dataset has the following properties:</span></span>

| <span data-ttu-id="5e30e-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5e30e-202">Property</span></span> | <span data-ttu-id="5e30e-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e30e-203">Description</span></span> | <span data-ttu-id="5e30e-204">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5e30e-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e30e-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="5e30e-205">folderPath</span></span> |<span data-ttu-id="5e30e-206">Sottopercorso alla cartella.</span><span class="sxs-lookup"><span data-stu-id="5e30e-206">Sub path to the folder.</span></span> <span data-ttu-id="5e30e-207">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="5e30e-207">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="5e30e-208">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="5e30e-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="5e30e-209">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="5e30e-209">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="5e30e-210">Sì</span><span class="sxs-lookup"><span data-stu-id="5e30e-210">Yes</span></span> |
| <span data-ttu-id="5e30e-211">fileName</span><span class="sxs-lookup"><span data-stu-id="5e30e-211">fileName</span></span> |<span data-ttu-id="5e30e-212">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="5e30e-212">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="5e30e-213">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="5e30e-213">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="5e30e-214">Quando fileName non viene specificato per un set di dati di output, il nome del file generato sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="5e30e-214">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="5e30e-215">Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="5e30e-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="5e30e-216">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-216">No</span></span> |
| <span data-ttu-id="5e30e-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="5e30e-217">fileFilter</span></span> |<span data-ttu-id="5e30e-218">Specificare un filtro da usare per selezionare un sottoinsieme di file in folderPath anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="5e30e-218">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="5e30e-219">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="5e30e-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="5e30e-220">Esempi 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="5e30e-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="5e30e-221">Esempio 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="5e30e-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="5e30e-222">fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="5e30e-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="5e30e-223">Questa proprietà non è supportata con HDFS.</span><span class="sxs-lookup"><span data-stu-id="5e30e-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="5e30e-224">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-224">No</span></span> |
| <span data-ttu-id="5e30e-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="5e30e-225">partitionedBy</span></span> |<span data-ttu-id="5e30e-226">partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-226">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="5e30e-227">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="5e30e-228">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-228">No</span></span> |
| <span data-ttu-id="5e30e-229">format</span><span class="sxs-lookup"><span data-stu-id="5e30e-229">format</span></span> | <span data-ttu-id="5e30e-230">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-230">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="5e30e-231">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="5e30e-231">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="5e30e-232">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="5e30e-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="5e30e-233">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="5e30e-233">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5e30e-234">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-234">No</span></span> |
| <span data-ttu-id="5e30e-235">compressione</span><span class="sxs-lookup"><span data-stu-id="5e30e-235">compression</span></span> | <span data-ttu-id="5e30e-236">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="5e30e-236">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="5e30e-237">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5e30e-238">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5e30e-239">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="5e30e-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5e30e-240">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-240">No</span></span> |
| <span data-ttu-id="5e30e-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="5e30e-241">useBinaryTransfer</span></span> |<span data-ttu-id="5e30e-242">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="5e30e-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="5e30e-243">True per la modalità binaria e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="5e30e-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="5e30e-244">Valore predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="5e30e-244">Default value: True.</span></span> <span data-ttu-id="5e30e-245">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="5e30e-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="5e30e-246">No</span><span class="sxs-lookup"><span data-stu-id="5e30e-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="5e30e-247">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="5e30e-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="5e30e-248">Uso della proprietà partionedBy</span><span class="sxs-lookup"><span data-stu-id="5e30e-248">Using partionedBy property</span></span>
<span data-ttu-id="5e30e-249">Come indicato nella sezione precedente, partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-249">As mentioned in the previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="5e30e-250">È possibile eseguire questa operazione con le macro della data factory e le variabili di sistema SliceStart, SliceEnd, che indicano il periodo di tempo logico per una sezione di dati specificata.</span><span class="sxs-lookup"><span data-stu-id="5e30e-250">You can do so with the Data Factory macros and the system variable SliceStart, SliceEnd that indicate the logical time period for a given data slice.</span></span>

<span data-ttu-id="5e30e-251">Per informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, vedere gli articoli [Creazione di set di dati](data-factory-create-datasets.md), [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) e [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-251">To learn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="5e30e-252">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="5e30e-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="5e30e-253">In questo esempio {Slice} viene sostituito con il valore della variabile di sistema SliceStart di Data Factory nel formato (AAAAMMGGHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="5e30e-253">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="5e30e-254">SliceStart fa riferimento all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-254">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="5e30e-255">La proprietà folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-255">The folderPath is different for each slice.</span></span> <span data-ttu-id="5e30e-256">Esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="5e30e-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="5e30e-257">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="5e30e-257">Sample 2:</span></span>

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
<span data-ttu-id="5e30e-258">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="5e30e-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5e30e-259">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="5e30e-259">Copy activity properties</span></span>
<span data-ttu-id="5e30e-260">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-260">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5e30e-261">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="5e30e-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="5e30e-262">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="5e30e-262">Whereas, the properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="5e30e-263">Per l'attività di copia, le proprietà del tipo variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="5e30e-263">For Copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="5e30e-264">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="5e30e-264">Supported file and compression formats</span></span>
<span data-ttu-id="5e30e-265">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-to-azure-blob"></a><span data-ttu-id="5e30e-266">Esempio JSON: copiare i dati dal server SFTP in BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5e30e-266">JSON Example: Copy data from SFTP server to Azure blob</span></span>
<span data-ttu-id="5e30e-267">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-267">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5e30e-268">Illustrano come copiare dati da un'origine SFTP in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e30e-268">They show how to copy data from SFTP source to Azure Blob Storage.</span></span> <span data-ttu-id="5e30e-269">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e30e-269">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e30e-270">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="5e30e-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="5e30e-271">Non include istruzioni dettagliate per la creazione della data factory.</span><span class="sxs-lookup"><span data-stu-id="5e30e-271">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="5e30e-272">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="5e30e-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="5e30e-273">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e30e-273">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="5e30e-274">Un servizio collegato di tipo [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="5e30e-275">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5e30e-276">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="5e30e-277">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5e30e-278">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5e30e-279">Nell'esempio i dati vengono copiati da un server SFTP a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5e30e-279">The sample copies data from an SFTP server to an Azure blob every hour.</span></span> <span data-ttu-id="5e30e-280">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="5e30e-280">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5e30e-281">**Servizio collegato SFTP**</span><span class="sxs-lookup"><span data-stu-id="5e30e-281">**SFTP linked service**</span></span>

<span data-ttu-id="5e30e-282">Questo esempio usa l'autenticazione di base con il nome utente e la password in testo normale.</span><span class="sxs-lookup"><span data-stu-id="5e30e-282">This example uses the basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="5e30e-283">È possibile anche usare uno dei tre metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e30e-283">You can also use one of the following ways:</span></span>

* <span data-ttu-id="5e30e-284">Autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="5e30e-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="5e30e-285">Autenticazione con chiave pubblica SSH</span><span class="sxs-lookup"><span data-stu-id="5e30e-285">SSH public key authentication</span></span>

<span data-ttu-id="5e30e-286">Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5e30e-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
<span data-ttu-id="5e30e-287">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="5e30e-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="5e30e-288">**Set di dati di input SFTP**</span><span class="sxs-lookup"><span data-stu-id="5e30e-288">**SFTP input dataset**</span></span>

<span data-ttu-id="5e30e-289">Questo set di dati fa riferimento alla cartella FTP `mysharedfolder` e al file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="5e30e-289">This dataset refers to the SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="5e30e-290">La pipeline copia il file nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-290">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="5e30e-291">Impostando "external": "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="5e30e-291">Setting "external": "true" informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="5e30e-292">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="5e30e-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="5e30e-293">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="5e30e-293">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5e30e-294">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5e30e-294">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5e30e-295">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="5e30e-295">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="5e30e-296">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="5e30e-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="5e30e-297">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="5e30e-297">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5e30e-298">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **FileSystemSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5e30e-298">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span>

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

## <a name="performance-and-tuning"></a><span data-ttu-id="5e30e-299">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="5e30e-299">Performance and Tuning</span></span>
<span data-ttu-id="5e30e-300">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="5e30e-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e30e-301">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e30e-301">Next Steps</span></span>
<span data-ttu-id="5e30e-302">Vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e30e-302">See the following articles:</span></span>

* <span data-ttu-id="5e30e-303">[Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="5e30e-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
