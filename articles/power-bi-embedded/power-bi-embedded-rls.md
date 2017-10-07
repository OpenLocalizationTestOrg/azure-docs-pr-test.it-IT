---
title: sicurezza a livello di aaaRow con Power BI Embedded
description: Informazioni dettagliate sulla sicurezza a livello di riga con Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="a78d3-103">Sicurezza a livello di riga con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a78d3-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="a78d3-104">Sicurezza a livello di riga (RLS) può essere utilizzato toorestrict utente accesso tooparticular dati all'interno di un report o un set di dati, consentendo di più utenti diversi toouse hello stesso report durante tutti vedere dati diversi.</span><span class="sxs-lookup"><span data-stu-id="a78d3-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="a78d3-105">Power BI Embedded supporta ora i set di dati configurati con la sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="a78d3-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="a78d3-106">In ordine tootake sfruttare di riga, è importante che comprendere i concetti principali tre; Gli utenti, ruoli e regole.</span><span class="sxs-lookup"><span data-stu-id="a78d3-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="a78d3-107">Ecco informazioni più approfondite su ogni concetto:</span><span class="sxs-lookup"><span data-stu-id="a78d3-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="a78d3-108">**Gli utenti** : questi sono gli utenti finali effettivo hello la visualizzazione dei report.</span><span class="sxs-lookup"><span data-stu-id="a78d3-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="a78d3-109">In Power BI Embedded, gli utenti vengono identificati dalle proprietà username hello in un Token di App.</span><span class="sxs-lookup"><span data-stu-id="a78d3-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="a78d3-110">**Ruoli** – tooroles appartengono gli utenti.</span><span class="sxs-lookup"><span data-stu-id="a78d3-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="a78d3-111">Un ruolo è un contenitore di regole e può essere denominato ad esempio "Responsabile vendite" o "Rappresentante".</span><span class="sxs-lookup"><span data-stu-id="a78d3-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="a78d3-112">In Power BI Embedded, gli utenti vengano identificati dalla proprietà ruoli hello in un Token di App.</span><span class="sxs-lookup"><span data-stu-id="a78d3-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="a78d3-113">**Regole** : ruoli dispongono di regole e le regole sono filtri effettivo hello che verranno applicati toobe toohello dati.</span><span class="sxs-lookup"><span data-stu-id="a78d3-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="a78d3-114">È ad esempio possibile usare un filtro semplice come "Paese = USA" o un filtro più dinamico.</span><span class="sxs-lookup"><span data-stu-id="a78d3-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="a78d3-115">Esempio</span><span class="sxs-lookup"><span data-stu-id="a78d3-115">Example</span></span>

<span data-ttu-id="a78d3-116">Per rest hello di questo articolo, verrà suggerito un esempio di creazione di riga e quindi che l'utilizzo all'interno di un'applicazione incorporata.</span><span class="sxs-lookup"><span data-stu-id="a78d3-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="a78d3-117">Questo esempio utilizza hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) file PBIX.</span><span class="sxs-lookup"><span data-stu-id="a78d3-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="a78d3-118">L'esempio di analisi delle vendite al dettaglio Mostra le vendite per tutti gli archivi di hello in una catena di distribuzione specifico.</span><span class="sxs-lookup"><span data-stu-id="a78d3-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="a78d3-119">Senza di riga, indipendentemente da quale district manager accede e visualizzazioni hello report, verranno visualizzate hello stessi dati.</span><span class="sxs-lookup"><span data-stu-id="a78d3-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="a78d3-120">I dirigenti ha determinato che ogni direttore dovrebbe visualizzare solo hello vendite per gli archivi di hello che gestiscono e toodo questa, sarà possibile utilizzare di riga.</span><span class="sxs-lookup"><span data-stu-id="a78d3-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="a78d3-121">La sicurezza a livello di riga viene creata in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="a78d3-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="a78d3-122">Quando vengono aperti hello set di dati e report, è possibile passare schema hello toosee della vista toodiagram:</span><span class="sxs-lookup"><span data-stu-id="a78d3-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="a78d3-123">Ecco alcuni aspetti toonotice con questo schema:</span><span class="sxs-lookup"><span data-stu-id="a78d3-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="a78d3-124">Tutte le misure, ad esempio **Total Sales**, vengono archiviati in hello **Sales** tabella dei fatti.</span><span class="sxs-lookup"><span data-stu-id="a78d3-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="a78d3-125">Sono presenti altre quattro tabelle relative alle dimensioni correlate, ovvero **Elemento**, **Tempo**, **Negozio** e **Distretto**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="a78d3-126">le frecce di Hello sulle linee di relazione hello indicano che modo i filtri possono avvenire da una tabella tooanother.</span><span class="sxs-lookup"><span data-stu-id="a78d3-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="a78d3-127">Ad esempio, se viene applicato un filtro a **ora [Date]**, nello schema corrente hello sarebbe filtrare solo verso il basso valori hello **Sales** tabella.</span><span class="sxs-lookup"><span data-stu-id="a78d3-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="a78d3-128">Altre tabelle non sarebbero interessate da questo filtro poiché tutti frecce hello hello relazione righe toohello punto vendita nella tabella e non da subito.</span><span class="sxs-lookup"><span data-stu-id="a78d3-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="a78d3-129">Hello **District** tabella indica che per ciascun gestore hello:</span><span class="sxs-lookup"><span data-stu-id="a78d3-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="a78d3-130">In base a questo schema, se si applica un filtro toohello **direttore** colonna nella tabella District hello e se tale filtro corrisponde a utente hello visualizzazione report hello, tale filtro filtrerà anche verso il basso hello **archivio**e **Sales** tabelle tooonly visualizzare i dati per quel particolare district manager.</span><span class="sxs-lookup"><span data-stu-id="a78d3-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="a78d3-131">Ecco come:</span><span class="sxs-lookup"><span data-stu-id="a78d3-131">Here’s how:</span></span>

1. <span data-ttu-id="a78d3-132">Nella scheda modellazione hello, fare clic su **gestione ruoli**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="a78d3-133">Creare un nuovo ruolo denominato **Manager**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="a78d3-134">In hello **District** tabella immettere l'espressione DAX seguente hello: **[direttore] = username)**</span><span class="sxs-lookup"><span data-stu-id="a78d3-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="a78d3-135">le regole hello toomake che siano lavorando, hello **modellazione** scheda, fare clic su **Visualizza come ruoli**e quindi immettere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a78d3-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="a78d3-136">Hello report verranno visualizzati dati come se hai eseguito l'accesso come **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="a78d3-137">L'applicazione hello filtro, il modo di hello abbiamo fatto in questo caso, verrà filtrano tutti i record di hello **District**, **archivio**, e **Sales** tabelle.</span><span class="sxs-lookup"><span data-stu-id="a78d3-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="a78d3-138">Tuttavia, a causa della direzione del filtro hello per le relazioni tra hello **Sales** e **ora**, **Sales** e **elemento**e **Elemento** e **ora** tabelle non verranno filtrate verso il basso.</span><span class="sxs-lookup"><span data-stu-id="a78d3-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="a78d3-139">Che può essere accettabile per questo requisito, tuttavia, se non si Gestioni toosee elementi per cui non dispongono di tutte le vendite, è stato possibile accendere bidirezionale filtro incrociato per hello relazioni e flusso hello filtro di sicurezza in entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="a78d3-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="a78d3-140">Questa operazione può essere eseguita mediante la modifica della relazione hello tra **Sales** e **elemento**, come segue:</span><span class="sxs-lookup"><span data-stu-id="a78d3-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="a78d3-141">A questo punto, i filtri possono inoltre passare da hello Sales tabella toohello **elemento** tabella:</span><span class="sxs-lookup"><span data-stu-id="a78d3-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="a78d3-142">Se si utilizza la modalità DirectQuery per i dati, è necessario tooenable bidirezionale-tra filtro selezionando queste due opzioni:</span><span class="sxs-lookup"><span data-stu-id="a78d3-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="a78d3-143">**File** -> **Opzioni e impostazioni** -> **Funzionalità di anteprima** -> **Abilita il filtro incrociato in entrambe le direzioni per DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="a78d3-144">**File** -> **Opzioni e impostazioni** -> **DirectQuery** -> **Consenti misure senza limitazioni in modalità DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="a78d3-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="a78d3-145">informazioni sul filtro incrociato bidirezionale, hello download toolearn [filtro incrociato bidirezionale in Power BI Desktop e di SQL Server Analysis Services 2016](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) white paper.</span><span class="sxs-lookup"><span data-stu-id="a78d3-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="a78d3-146">Questo conclude tutto il lavoro hello necessarie toobe eseguita in Power BI Desktop, ma non esiste uno più elemento di lavoro che deve toomake toobe eseguita hello e regole di lavoro è stato definito in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="a78d3-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="a78d3-147">Gli utenti vengono autenticati e autorizzati dall'applicazione e i token App sono utilizzati toogrant utente accesso tooa Power BI Embedded report specificato.</span><span class="sxs-lookup"><span data-stu-id="a78d3-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="a78d3-148">Power BI Embedded non ha informazioni specifiche sull'identità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a78d3-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="a78d3-149">Per toowork di riga, è necessario toopass un contesto aggiuntivo come parte del token di app:</span><span class="sxs-lookup"><span data-stu-id="a78d3-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="a78d3-150">**nome utente** (facoltativo): usato con una riga è una stringa che può essere usata toohelp identificare utente hello quando l'applicazione delle regole di riga.</span><span class="sxs-lookup"><span data-stu-id="a78d3-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="a78d3-151">Vedere l'articolo relativo all'uso della sicurezza a livello di riga con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="a78d3-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="a78d3-152">**ruoli** : una stringa contenente hello ruoli tooselect quando l'applicazione delle regole di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="a78d3-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="a78d3-153">Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="a78d3-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="a78d3-154">Per creare token hello, utilizzare hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) metodo.</span><span class="sxs-lookup"><span data-stu-id="a78d3-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="a78d3-155">Se proprietà username hello è presente, è inoltre necessario passare almeno un valore nei ruoli.</span><span class="sxs-lookup"><span data-stu-id="a78d3-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="a78d3-156">Ad esempio, è possibile modificare hello EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="a78d3-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="a78d3-157">La riga 55 di DashboardController può essere aggiornata da</span><span class="sxs-lookup"><span data-stu-id="a78d3-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="a78d3-158">to</span><span class="sxs-lookup"><span data-stu-id="a78d3-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="a78d3-159">token app completo Hello avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a78d3-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="a78d3-160">A questo punto, con tutte le parti di hello insieme, quando un utente accede a tooview l'applicazione di questo report, essi verrà solo essere toosee in grado di hello dati che sono consentiti toosee, come definito per i livelli di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="a78d3-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="a78d3-161">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a78d3-161">See also</span></span>

[<span data-ttu-id="a78d3-162">Sicurezza a livello di riga con Power BI</span><span class="sxs-lookup"><span data-stu-id="a78d3-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="a78d3-163">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a78d3-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a78d3-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a78d3-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a78d3-165">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="a78d3-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="a78d3-166">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="a78d3-166">More questions?</span></span> [<span data-ttu-id="a78d3-167">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="a78d3-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

