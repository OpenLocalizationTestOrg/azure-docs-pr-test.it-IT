---
title: 'Azure AD Connect: Certificato SSL aggiornamento hello per una farm di Active Directory Federation Services (ADFS) | Documenti Microsoft'
description: Questo documento dettagli hello passaggi tooupdate hello certificato SSL di una farm di ADFS con Azure AD Connect.
services: active-directory
keywords: azure ad connect, aggiornamento ssl ad fs, aggiornamento certificato ad fs, modifica certificato ad fs, nuovo certificato ad fs, certificato ad fs, aggiornare certificato ssl ad fs, aggiornare ad fs certificato ssl, configurare certificato ssl ad fs, ad fs, ssl, certificato, certificato comunicazioni di servizio ad fs, aggiornare federazione, configurare federazione, aad connect
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="f423f-104">Aggiorna il certificato SSL di hello per una farm di Active Directory Federation Services (ADFS)</span><span class="sxs-lookup"><span data-stu-id="f423f-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="f423f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f423f-105">Overview</span></span>
<span data-ttu-id="f423f-106">In questo articolo viene descritto come utilizzare certificato SSL di Azure AD Connect tooupdate hello per una farm di Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="f423f-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="f423f-107">È possibile utilizzare un certificato SSL hello Azure AD Connect strumento tooeasily aggiornamento hello per farm ADFS hello AD anche se hello utente metodo di accesso selezionato non è AD FS.</span><span class="sxs-lookup"><span data-stu-id="f423f-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="f423f-108">È possibile eseguire l'intera operazione di hello di aggiornamento certificato SSL per la farm di hello AD FS in tutti i server Proxy applicazione Web (WAP) in tre passaggi semplici e federazione:</span><span class="sxs-lookup"><span data-stu-id="f423f-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Tre passaggi](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="f423f-110">toolearn ulteriori informazioni sui certificati utilizzati da ADFS, vedere [informazioni sui certificati utilizzati da ADFS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="f423f-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f423f-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f423f-111">Prerequisites</span></span>

* <span data-ttu-id="f423f-112">**Farm AD FS**: assicurarsi che la farm AD FS sia basata su Windows Server 2012 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="f423f-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="f423f-113">**Azure AD Connect**: verificare che hello versione di Azure AD Connect è 1.1.443.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f423f-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="f423f-114">Si userà attività hello **certificato SSL ADFS aggiornamento AD**.</span><span class="sxs-lookup"><span data-stu-id="f423f-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Attività Aggiorna il certificato SSL di AD FS](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="f423f-116">Passaggio 1: Specificare informazioni sulla farm AD FS</span><span class="sxs-lookup"><span data-stu-id="f423f-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="f423f-117">Azure AD Connect tenta automaticamente da tooobtain informazioni farm di hello AD FS:</span><span class="sxs-lookup"><span data-stu-id="f423f-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="f423f-118">Esecuzione di query su informazioni relative alla farm hello da ADFS (Windows Server 2016 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="f423f-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="f423f-119">Un riferimento a informazioni hello esecuzioni precedenti, che vengono archiviate localmente con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f423f-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="f423f-120">È possibile modificare l'elenco di hello del server che vengono visualizzati aggiungendo o rimuovendo hello server tooreflect hello configurazione corrente delle farm di hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="f423f-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="f423f-121">Non appena viene forniti informazioni sul server hello, Azure AD Connect consente di visualizzare la connettività hello e stato corrente del certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="f423f-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Informazioni sui server AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="f423f-123">Se l'elenco di hello contiene un server che non è più parte della farm ADFS hello Active Directory, fare clic su **rimuovere** server hello toodelete dall'elenco di hello del server nella farm ADFS.</span><span class="sxs-lookup"><span data-stu-id="f423f-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Server offline nell'elenco](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="f423f-125">Rimozione di un server dall'elenco di hello del server per AD FS farm in Azure AD Connect è un'operazione locale e aggiornamenti hello informazioni per hello farm ADFS in locale da Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f423f-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="f423f-126">Azure AD Connect non modifica la configurazione hello su ADFS tooreflect hello modifica.</span><span class="sxs-lookup"><span data-stu-id="f423f-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="f423f-127">Passaggio 2: Specificare un nuovo certificato SSL</span><span class="sxs-lookup"><span data-stu-id="f423f-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="f423f-128">Dopo aver verificato informazioni hello sui server della farm di ADFS, Azure AD Connect richiede nuovo certificato SSL di hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="f423f-129">Fornire un'installazione di hello di protetto da password PFX certificato toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f423f-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![Certificato SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="f423f-131">Dopo aver fornito il certificato di hello, Azure AD Connect passa attraverso una serie di prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="f423f-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="f423f-132">Verificare tooensure certificato hello che hello certificato sia corretta per la farm ADFS hello:</span><span class="sxs-lookup"><span data-stu-id="f423f-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="f423f-133">Hello nome soggetto alternativo di nome/soggetto certificato hello è hello stesso come nome del servizio federativo hello oppure è un certificato con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="f423f-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="f423f-134">certificato di Hello è valido per più di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="f423f-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="f423f-135">catena di certificati Hello è valido.</span><span class="sxs-lookup"><span data-stu-id="f423f-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="f423f-136">certificato Hello è protetto da password.</span><span class="sxs-lookup"><span data-stu-id="f423f-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="f423f-137">Passaggio 3: Selezionare i server per l'aggiornamento di hello</span><span class="sxs-lookup"><span data-stu-id="f423f-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="f423f-138">Nel passaggio successivo hello, selezionare Server hello che richiedono i certificati SSL di hello toohave aggiornata.</span><span class="sxs-lookup"><span data-stu-id="f423f-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="f423f-139">Impossibile selezionare i server che non sono in linea per l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-139">Servers that are offline can't be selected for hello update.</span></span>

![Selezionare i server tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="f423f-141">Dopo aver completato la configurazione hello, Azure AD Connect consente di visualizzare il messaggio hello che indica lo stato di hello dell'aggiornamento hello e fornisce un'opzione tooverify hello ADFS Accedi.</span><span class="sxs-lookup"><span data-stu-id="f423f-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Configurazione completata](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="f423f-143">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="f423f-143">FAQs</span></span>

* <span data-ttu-id="f423f-144">**Quale deve essere hello nome del soggetto hello certificato per il certificato SSL di AD FS nuovo hello?**</span><span class="sxs-lookup"><span data-stu-id="f423f-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="f423f-145">Azure AD Connect controlla se hello soggetto alternativo di nome/nome del soggetto hello certificato contiene il nome di servizio federativo hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="f423f-146">Ad esempio, se il nome del servizio federativo è fs.contoso.com, nome soggetto di nome/alternativo del soggetto hello deve essere fs.contoso.com.  Sono accettati anche certificati con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="f423f-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="f423f-147">**Motivo per cui viene chiesto di credenziali nuovamente nella pagina server WAP di hello?**</span><span class="sxs-lookup"><span data-stu-id="f423f-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="f423f-148">Se credenziali hello specificate per la connessione server ADFS tooAD non dispongono anche di server WAP di hello privilegio toomanage hello, Azure AD Connect richiede le credenziali che dispongono di privilegi amministrativi sui server WAP hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="f423f-149">**server Hello viene visualizzato come offline. Cosa devo fare?**</span><span class="sxs-lookup"><span data-stu-id="f423f-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="f423f-150">Azure AD Connect non è possibile eseguire qualsiasi operazione se hello server è offline.</span><span class="sxs-lookup"><span data-stu-id="f423f-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="f423f-151">Se server hello fa parte di hello farm AD FS, controllare server toohello di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="f423f-152">Dopo avere risolto il problema di hello, premere hello aggiornamento icona tooupdate hello dello stato nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="f423f-153">Se il server di hello faceva parte di hello farm in precedenza, ma ora non esiste più, fare clic su **rimuovere** toodelete dall'elenco di hello del server che si connettono AD Azure gestisce.</span><span class="sxs-lookup"><span data-stu-id="f423f-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="f423f-154">Rimozione di server hello dall'elenco di hello in Azure AD Connect non modifica hello stessa configurazione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="f423f-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="f423f-155">Se si usa ADFS in Windows Server 2016 o versione successiva, hello server rimane nelle impostazioni di configurazione hello e verrà visualizzato nuovamente hello successivo hello attività viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="f423f-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="f423f-156">**È possibile aggiornare un sottoinsieme di my Server farm con nuovo certificato SSL di hello?**</span><span class="sxs-lookup"><span data-stu-id="f423f-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="f423f-157">Sì.</span><span class="sxs-lookup"><span data-stu-id="f423f-157">Yes.</span></span> <span data-ttu-id="f423f-158">È sempre possibile eseguire attività di hello **certificato SSL di aggiornamento** nuovamente i hello tooupdate server rimanenti.</span><span class="sxs-lookup"><span data-stu-id="f423f-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="f423f-159">In hello **selezionare i server per SSL certificato aggiornamento** pagina, è possibile ordinare l'elenco di hello del server in **data di scadenza SSL** tooeasily i server di hello di accesso che non sono ancora aggiornati.</span><span class="sxs-lookup"><span data-stu-id="f423f-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="f423f-160">**Rimosso server hello hello precedente esecuzione, ma ancora viene visualizzato come offline ed è elencato nella pagina di annuncio hello server ADFS. Anche dopo che è stato rimosso, perché è ancora presenti server offline hello?**</span><span class="sxs-lookup"><span data-stu-id="f423f-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="f423f-161">Rimozione di server hello dall'elenco di hello in Azure AD Connect non rimuoverlo in hello configurazione di ADFS.</span><span class="sxs-lookup"><span data-stu-id="f423f-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="f423f-162">Azure AD Connect fa riferimento AD FS (Windows Server 2016 o versioni successive) per qualsiasi informazione sulla farm hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="f423f-163">Se il server di hello è ancora presente nella configurazione di ADFS hello, sarà elencato in elenco hello.</span><span class="sxs-lookup"><span data-stu-id="f423f-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f423f-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f423f-164">Next steps</span></span>

- [<span data-ttu-id="f423f-165">Azure AD Connect e federazione</span><span class="sxs-lookup"><span data-stu-id="f423f-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="f423f-166">Gestione e personalizzazione di Active Directory Federation Services con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f423f-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
