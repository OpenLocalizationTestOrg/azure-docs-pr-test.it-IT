---
title: Risolvere i problemi del gateway di gestione dati | Documentazione Microsoft
description: Questo articolo offre suggerimenti per risolvere i problemi correlati al gateway di gestione dati.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="790db-103">Risolvere i problemi nell'uso del gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="790db-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="790db-104">Questo articolo offre informazioni sulla risoluzione dei problemi nell'uso del gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="790db-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="790db-105">Vedere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per informazioni dettagliate sul gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="790db-106">Vedere l'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) per una procedura dettagliata sull'uso del gateway per spostare i dati da un database di SQL Server locale all'Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="790db-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="790db-107">Impossibile installare o registrare il gateway</span><span class="sxs-lookup"><span data-stu-id="790db-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="790db-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-108">1. Problem</span></span>
<span data-ttu-id="790db-109">Questo messaggio di errore viene visualizzato durante l'installazione e la registrazione di un gateway, in particolare durante il download del file di installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="790db-110">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-110">Cause</span></span>
<span data-ttu-id="790db-111">Il computer in cui si prova a installare il gateway non è riuscito a scaricare il file di installazione del gateway più recente dall'area download a causa di un problema di rete.</span><span class="sxs-lookup"><span data-stu-id="790db-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-112">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-112">Resolution</span></span>
<span data-ttu-id="790db-113">Verificare se nel firewall del server proxy sono presenti impostazioni che bloccano la connessione di rete dal computer all'[Area download](https://download.microsoft.com/) e aggiornare le impostazioni di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="790db-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="790db-114">In alternativa, è possibile scaricare il file di installazione del gateway più recente dall'[Area download](https://www.microsoft.com/download/details.aspx?id=39717) su altri computer che possono accedere all'area download.</span><span class="sxs-lookup"><span data-stu-id="790db-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="790db-115">Dopo averlo scaricato, copiare il file di installazione nel computer host del gateway ed eseguirlo manualmente per installare e aggiornare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="790db-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-116">2. Problem</span></span>
<span data-ttu-id="790db-117">Questo errore viene visualizzato quando si prova a installare un gateway facendo clic su **Installa direttamente in questo computer** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="790db-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="790db-118">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-118">Cause</span></span>
<span data-ttu-id="790db-119">È già installato un gateway nel computer.</span><span class="sxs-lookup"><span data-stu-id="790db-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-120">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-120">Resolution</span></span>
<span data-ttu-id="790db-121">Disinstallare il gateway esistente nel computer e fare nuovamente clic sul collegamento **Installa direttamente in questo computer**.</span><span class="sxs-lookup"><span data-stu-id="790db-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="790db-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-122">3. Problem</span></span>
<span data-ttu-id="790db-123">Questo errore può verificarsi quando si registra un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="790db-124">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-124">Cause</span></span>
<span data-ttu-id="790db-125">Il messaggio può essere visualizzato per uno dei motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="790db-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="790db-126">Il formato della chiave del gateway non è valido.</span><span class="sxs-lookup"><span data-stu-id="790db-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="790db-127">La chiave del gateway è stata invalidata.</span><span class="sxs-lookup"><span data-stu-id="790db-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="790db-128">La chiave del gateway è stata rigenerata dal portale.</span><span class="sxs-lookup"><span data-stu-id="790db-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="790db-129">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-129">Resolution</span></span>
<span data-ttu-id="790db-130">Accertarsi che venga usata la chiave del gateway corretta del portale.</span><span class="sxs-lookup"><span data-stu-id="790db-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="790db-131">Se necessario, rigenerare una chiave e usarla per registrare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="790db-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-132">4. Problem</span></span>
<span data-ttu-id="790db-133">Durante la registrazione di un gateway può essere visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Il contenuto o il formato della chiave non è valido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="790db-135">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-135">Cause</span></span>
<span data-ttu-id="790db-136">Il contenuto o il formato della chiave del gateway di input non è corretto.</span><span class="sxs-lookup"><span data-stu-id="790db-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="790db-137">È possibile che sia stata copiata solo una parte della chiave dal portale oppure che la chiave usata non sia valida.</span><span class="sxs-lookup"><span data-stu-id="790db-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-138">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-138">Resolution</span></span>
<span data-ttu-id="790db-139">Generare una chiave del gateway nel portale e usare il pulsante Copia per copiare la chiave intera.</span><span class="sxs-lookup"><span data-stu-id="790db-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="790db-140">Quindi incollarla in questa finestra per registrare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="790db-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-141">5. Problem</span></span>
<span data-ttu-id="790db-142">Durante la registrazione di un gateway può essere visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="790db-144">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-144">Cause</span></span>
<span data-ttu-id="790db-145">La chiave del gateway è stata rigenerata oppure il gateway è stato eliminato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="790db-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="790db-146">Il problema può verificarsi anche quando la versione del programma di installazione del Gateway di gestione dati non è la più recente.</span><span class="sxs-lookup"><span data-stu-id="790db-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-147">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-147">Resolution</span></span>
<span data-ttu-id="790db-148">Controllare che la versione del programma di installazione del Gateway di gestione dati sia la più recente (fare riferimento al [Download Center](https://go.microsoft.com/fwlink/p/?LinkId=271260) di Microsoft).</span><span class="sxs-lookup"><span data-stu-id="790db-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="790db-149">Se la versione del programma di installazione è quella attuale o la più recente e il gateway è ancora presente sul Portale, rigenerare la chiave del gateway nel Portale di Azure e usare il pulsante Copia per copiare l'intera chiave, quindi incollarla in questa finestra per registrare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="790db-150">In caso contrario ricreare il gateway e ricominciare.</span><span class="sxs-lookup"><span data-stu-id="790db-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="790db-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-151">6. Problem</span></span>
<span data-ttu-id="790db-152">Durante la registrazione di un gateway può essere visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="790db-154">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-154">Cause</span></span>
<span data-ttu-id="790db-155">Questo errore può verificarsi perché il gateway è stato eliminato oppure la chiave associata è stata rigenerata.</span><span class="sxs-lookup"><span data-stu-id="790db-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-156">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-156">Resolution</span></span>
<span data-ttu-id="790db-157">Se il gateway è stato eliminato, ricrearlo dal portale, fare clic su **Registra**, copiare la chiave dal portale, incollarla e provare a registrare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="790db-158">Se il gateway è ancora esistente, ma la chiave è stata rigenerata, usare la nuova chiave per registrare il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="790db-159">Se la chiave non è disponibile, rigenerarla nuovamente dal portale.</span><span class="sxs-lookup"><span data-stu-id="790db-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="790db-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-160">7. Problem</span></span>
<span data-ttu-id="790db-161">Quando si registra un gateway, potrebbe essere necessario immettere il percorso e la password di un certificato.</span><span class="sxs-lookup"><span data-stu-id="790db-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="790db-163">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-163">Cause</span></span>
<span data-ttu-id="790db-164">Il gateway è stato registrato in precedenza in altri computer.</span><span class="sxs-lookup"><span data-stu-id="790db-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="790db-165">Durante la registrazione iniziale di un gateway è stato associato un certificato di crittografia al gateway stesso.</span><span class="sxs-lookup"><span data-stu-id="790db-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="790db-166">Il certificato può essere generato automaticamente dal gateway oppure specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="790db-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="790db-167">Questo certificato viene usato per crittografare le credenziali dell'archivio dati (servizio collegato).</span><span class="sxs-lookup"><span data-stu-id="790db-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Esportare il certificato](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="790db-169">Quando si ripristina il gateway in un computer host diverso, la registrazione guidata richiede questo certificato per decrittografare le credenziali crittografate in precedenza con questo certificato.</span><span class="sxs-lookup"><span data-stu-id="790db-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="790db-170">Senza questo certificato, le credenziali non possono essere decrittografate dal nuovo gateway e le successive attività di copia associate al nuovo gateway avranno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="790db-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="790db-171">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-171">Resolution</span></span>
<span data-ttu-id="790db-172">Se il certificato delle credenziali è stato esportato dal computer gateway originale con il pulsante **Esporta** disponibile nella scheda **Impostazioni** di Gestione configurazione di Gateway di gestione dati, usare il certificato in quel computer.</span><span class="sxs-lookup"><span data-stu-id="790db-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="790db-173">Non è possibile ignorare questo passaggio quando si recupera un gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="790db-174">Se il certificato è mancante, è necessario eliminare il gateway dal portale e crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="790db-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="790db-175">Inoltre, tutti i servizi collegati relativi al gateway devono essere aggiornati immettendo di nuovo le credenziali.</span><span class="sxs-lookup"><span data-stu-id="790db-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="790db-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-176">8. Problem</span></span>
<span data-ttu-id="790db-177">È possibile visualizzare il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="790db-178">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-178">Cause</span></span>
<span data-ttu-id="790db-179">Questo errore si verifica quando il gateway si trova in un ambiente che richiede un proxy HTTP per accedere alle risorse Internet oppure quando la password di autenticazione del proxy viene modificata, ma non aggiornata di conseguenza nel gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-180">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-180">Resolution</span></span>
<span data-ttu-id="790db-181">Seguire le istruzioni indicate nella sezione [Considerazioni sui server proxy](#proxy-server-considerations) di questo documento e configurare le impostazioni del proxy con Gestione configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="790db-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="790db-182">Il gateway è online con funzionalità limitate</span><span class="sxs-lookup"><span data-stu-id="790db-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="790db-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-183">1. Problem</span></span>
<span data-ttu-id="790db-184">Lo stato visualizzato per il gateway è online con funzionalità limitata.</span><span class="sxs-lookup"><span data-stu-id="790db-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="790db-185">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-185">Cause</span></span>
<span data-ttu-id="790db-186">Lo stato visualizzato per il gateway è online con funzionalità limitata per uno dei motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="790db-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="790db-187">Il gateway non può connettersi al servizio cloud tramite il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="790db-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="790db-188">Il servizio cloud non può connettersi al gateway tramite il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="790db-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="790db-189">Quando il gateway è online con funzionalità limitate, potrebbe non essere possibile usare la copia guidata di Data Factory per creare pipeline di dati per copiare i dati da e verso archivi dati locali.</span><span class="sxs-lookup"><span data-stu-id="790db-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="790db-190">Come soluzione alternativa, è possibile usare l'editor di Data Factory nel portale, oppure Visual Studio o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="790db-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-191">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-191">Resolution</span></span>
<span data-ttu-id="790db-192">La risoluzione di questo problema (online con funzionalità limitata) dipende dall'eventualità che il gateway non possa connettersi al servizio cloud o viceversa.</span><span class="sxs-lookup"><span data-stu-id="790db-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="790db-193">Le sezioni seguenti illustrano queste risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="790db-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="790db-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-194">2. Problem</span></span>
<span data-ttu-id="790db-195">Viene visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![Il gateway non riesce a connettersi al servizio cloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="790db-197">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-197">Cause</span></span>
<span data-ttu-id="790db-198">Il gateway non può connettersi al servizio cloud tramite il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="790db-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-199">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-199">Resolution</span></span>
<span data-ttu-id="790db-200">Seguire questi passaggi per fare in modo che il gateway torni online:</span><span class="sxs-lookup"><span data-stu-id="790db-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="790db-201">Consentire le regole in uscita degli indirizzi IP nel computer gateway e nel firewall aziendale.</span><span class="sxs-lookup"><span data-stu-id="790db-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="790db-202">È possibile trovare gli indirizzi IP nel registro eventi di Windows (ID == 401): si è verificato un tentativo di accesso a un socket in modalità non consentite dalle relative autorizzazioni di accesso XX.XX.XX.XX:9350.</span><span class="sxs-lookup"><span data-stu-id="790db-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="790db-203">Configurare le impostazioni proxy nel gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="790db-204">Per conoscere i dettagli, vedere la sezione [Considerazioni sui server proxy](#proxy-server-considerations).</span><span class="sxs-lookup"><span data-stu-id="790db-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="790db-205">Abilitare le porte in uscita 5671 e 9350-9354 sia su Windows Firewall nel computer gateway che nel firewall aziendale.</span><span class="sxs-lookup"><span data-stu-id="790db-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="790db-206">Per conoscere i dettagli, vedere la sezione [Porte e firewall](#ports-and-firewall).</span><span class="sxs-lookup"><span data-stu-id="790db-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="790db-207">Questo passaggio è facoltativo, ma consigliato per considerazioni relative alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="790db-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="790db-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="790db-208">3. Problem</span></span>
<span data-ttu-id="790db-209">Viene visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="790db-210">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-210">Cause</span></span>
<span data-ttu-id="790db-211">Errore temporaneo nella connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="790db-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-212">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-212">Resolution</span></span>
<span data-ttu-id="790db-213">Seguire questi passaggi per fare in modo che il gateway torni online:</span><span class="sxs-lookup"><span data-stu-id="790db-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="790db-214">Attendere un paio di minuti; la connettività verrà ripristinata automaticamente quando l'errore non sarà più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="790db-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="790db-215">Se l'errore persiste, riavviare il servizio gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="790db-216">Impossibile creare il servizio collegato</span><span class="sxs-lookup"><span data-stu-id="790db-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="790db-217">Problema</span><span class="sxs-lookup"><span data-stu-id="790db-217">Problem</span></span>
<span data-ttu-id="790db-218">Questo errore può verificarsi quando si prova a usare Gestione credenziali nel portale per inserire le credenziali per un nuovo servizio collegato o aggiornare le credenziali per un servizio collegato esistente.</span><span class="sxs-lookup"><span data-stu-id="790db-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="790db-219">Quando viene visualizzato questo errore, la pagina Impostazioni di Gestione configurazione di Gateway di gestione dati potrebbe essere simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="790db-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Impossibile raggiungere il database](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="790db-221">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-221">Cause</span></span>
<span data-ttu-id="790db-222">È possibile che il certificato SSL sia andato perso nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="790db-223">Il gateway non può caricare il certificato usato attualmente per la crittografia SSL.</span><span class="sxs-lookup"><span data-stu-id="790db-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="790db-224">Nel registro può essere visualizzato un messaggio di errore analogo al seguente.</span><span class="sxs-lookup"><span data-stu-id="790db-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="790db-225">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-225">Resolution</span></span>
<span data-ttu-id="790db-226">Seguire questa procedura per risolvere il problema:</span><span class="sxs-lookup"><span data-stu-id="790db-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="790db-227">Avviare Gestione configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="790db-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="790db-228">Passare alla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="790db-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="790db-229">Fare clic sul pulsante **Cambia** per cambiare il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="790db-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![Pulsate Cambia per cambiare il certificato](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="790db-231">Selezionare un nuovo certificato come certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="790db-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="790db-232">È possibile usare qualsiasi certificato SSL generato dall'utente o da qualsiasi organizzazione.</span><span class="sxs-lookup"><span data-stu-id="790db-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="790db-234">L'attività di copia ha esito negativo</span><span class="sxs-lookup"><span data-stu-id="790db-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="790db-235">Problema</span><span class="sxs-lookup"><span data-stu-id="790db-235">Problem</span></span>
<span data-ttu-id="790db-236">Dopo aver impostato una pipeline nel portale di Azure viene visualizzato l'errore "UserErrorFailedToConnectToSqlserver".</span><span class="sxs-lookup"><span data-stu-id="790db-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="790db-237">Causa</span><span class="sxs-lookup"><span data-stu-id="790db-237">Cause</span></span>
<span data-ttu-id="790db-238">Questo problema può verificarsi per diversi motivi e la mitigazione varia di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="790db-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="790db-239">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="790db-239">Resolution</span></span>
<span data-ttu-id="790db-240">Consentire le connessioni TCP in uscita sulla porta TCP/1433 o sul lato client del gateway di gestione dati prima di connettersi a un database SQL.</span><span class="sxs-lookup"><span data-stu-id="790db-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="790db-241">Se il database di destinazione è un database SQL di Azure, verificare anche le impostazioni del firewall del server SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="790db-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="790db-242">Vedere la sezione seguente per testare la connessione all'archivio dati locale.</span><span class="sxs-lookup"><span data-stu-id="790db-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="790db-243">Errori correlati alla connessione all'archivio dati o al driver</span><span class="sxs-lookup"><span data-stu-id="790db-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="790db-244">Se vengono visualizzati errori relativi alla connessione dell'archivio dati o al driver, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="790db-245">Avviare Gestione configurazione di Gateway di gestione dati sul computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="790db-246">Passare alla scheda **Diagnostica** .</span><span class="sxs-lookup"><span data-stu-id="790db-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="790db-247">In **Test di connessione**, aggiungere i valori del gruppo del gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="790db-248">Fare clic su **Test** per verificare se è possibile connettersi all'origine dati locale dal computer del gateway tramite le informazioni di connessione e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="790db-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="790db-249">Se il test della connessione non riesce dopo aver installato un driver, riavviare il gateway in modo che rilevi la modifica più recente.</span><span class="sxs-lookup"><span data-stu-id="790db-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Test connessione nella scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="790db-251">Log del gateway</span><span class="sxs-lookup"><span data-stu-id="790db-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="790db-252">Inviare i log del gateway a Microsoft</span><span class="sxs-lookup"><span data-stu-id="790db-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="790db-253">Quando si contatta il supporto Microsoft per ricevere assistenza nella risoluzione dei problemi con il gateway, all'utente potrebbe essere richiesto di condividere i log del gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="790db-254">La versione del gateway consente di condividere facilmente i log necessari con pochi clic in Gestione configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="790db-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="790db-255">In Gestione configurazione di Gateway di gestione dati aprire la scheda **Diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="790db-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Gateway di gestione dati - Scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="790db-257">Fare clic sul collegamento **Invia log** per aprire la finestra di dialogo seguente.</span><span class="sxs-lookup"><span data-stu-id="790db-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Gateway di gestione dati - Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="790db-259">(facoltativo) Fare clic su **Visualizza log** per esaminare i log nel visualizzatore eventi.</span><span class="sxs-lookup"><span data-stu-id="790db-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="790db-260">(facoltativo) Fare clic su **Privacy** per esaminare l'informativa sulla privacy per i servizi Web di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="790db-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="790db-261">Quando tutto è pronto per il caricamento, fare clic su **Invia log** per inviare effettivamente i log degli ultimi sette giorni a Microsoft per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="790db-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="790db-262">Lo stato dell'operazione dovrebbe corrispondere a quello mostrato nell'immagine in basso:</span><span class="sxs-lookup"><span data-stu-id="790db-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="790db-264">Al termine dell'operazione viene visualizzata una finestra di dialogo simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="790db-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="790db-266">Annotare l'**ID report** e condividerlo con il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="790db-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="790db-267">L'ID report serve per individuare i log del gateway caricati per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="790db-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="790db-268">Viene anche salvato nel visualizzatore eventi.</span><span class="sxs-lookup"><span data-stu-id="790db-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="790db-269">È possibile trovarlo cercando l'ID evento "25" e verificando la data e l'ora.</span><span class="sxs-lookup"><span data-stu-id="790db-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Gateway di gestione dati - ID report dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="790db-271">Archiviare i log del gateway nel computer host del gateway</span><span class="sxs-lookup"><span data-stu-id="790db-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="790db-272">Esistono dei casi in cui si verificano problemi con il gateway e non è possibile condividere direttamente i log del gateway:</span><span class="sxs-lookup"><span data-stu-id="790db-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="790db-273">quando si installa e registra il gateway manualmente;</span><span class="sxs-lookup"><span data-stu-id="790db-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="790db-274">quando si tenta di registrare il gateway con una chiave rigenerata in Gestione configurazione di Gateway di gestione dati;</span><span class="sxs-lookup"><span data-stu-id="790db-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="790db-275">quando si tenta di inviare i log ma non è possibile connettersi al servizio che ospita il gateway.</span><span class="sxs-lookup"><span data-stu-id="790db-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="790db-276">In questi casi, è possibile salvare i log del gateway come file zip e condividerlo quando si contatta il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="790db-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="790db-277">Ad esempio, se si verifica un errore durante la registrazione del gateway come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="790db-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Gateway di gestione dati - Errore di registrazione](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="790db-279">Fare clic sul collegamento **Archivia log del gateway** per archiviare e salvare i log, quindi condividere il file zip con il supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="790db-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Gateway di gestione dati - Archivia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="790db-281">Trovare i log del gateway</span><span class="sxs-lookup"><span data-stu-id="790db-281">Locate gateway logs</span></span>
<span data-ttu-id="790db-282">Per informazioni dettagliate sui log del gateway, vedere il registro eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="790db-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="790db-283">Avviare il **Visualizzatore eventi** di Windows.</span><span class="sxs-lookup"><span data-stu-id="790db-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="790db-284">Individuare i log nella cartella **Registri applicazioni e servizi** > **Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="790db-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="790db-285">Per risolvere i problemi correlati al gateway, cercare gli eventi a livello di errore nel Visualizzatore eventi.</span><span class="sxs-lookup"><span data-stu-id="790db-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Gateway di gestione dati - Log nel Visualizzatore eventi](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
