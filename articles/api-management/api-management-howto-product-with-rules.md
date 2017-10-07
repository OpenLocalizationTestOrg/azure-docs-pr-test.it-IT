---
title: aaaProtect dell'API di gestione API di Azure | Documenti Microsoft
description: "Informazioni su come tooprotect dell'API di quote e limitazioni (limitazione di velocità) di criteri."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="39cfd-103">Proteggere le API con limiti di frequenza usando Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="39cfd-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="39cfd-104">Questa guida viene illustrato come è facile tooadd protezione per l'API di back-end mediante criteri di limite e quota velocità con gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="39cfd-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="39cfd-105">In questa esercitazione si creerà un prodotto di "Versione di valutazione gratuita" API che consente agli sviluppatori toomake backup too10 chiamate al minuto e backup tooa massimo di 200 chiamate alla settimana tooyour API utilizzando hello [frequenza delle chiamate limite per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [ Quota di utilizzo di set per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) criteri.</span><span class="sxs-lookup"><span data-stu-id="39cfd-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="39cfd-106">Verrà quindi pubblicare API hello e testare i criteri di limite di frequenza hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="39cfd-107">Più avanzati la limitazione delle richieste di scenari con hello [frequenza limite dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) criteri, vedere [richiesta avanzata di limitazione delle richieste a gestione API di Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="39cfd-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="39cfd-108"><a name="create-product"></a>toocreate un prodotto</span><span class="sxs-lookup"><span data-stu-id="39cfd-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="39cfd-109">In questo passaggio si creerà un prodotto con una versione di valutazione gratuita che non richiede l'approvazione della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="39cfd-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="39cfd-110">Se si già dispone di un prodotto configurato e si desidera toouse che per questa esercitazione, è possibile passare troppo[Configura frequenza delle chiamate per i criteri di limite e quota] [ Configure call rate limit and quota policies] e seguire l'esercitazione hello da lì, con il prodotto al posto del prodotto di valutazione gratuita di hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="39cfd-111">tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="39cfd-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="39cfd-113">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [gestione API in Gestione API di Azure prima] [ Manage your first API in Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="39cfd-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="39cfd-114">Fare clic su **prodotti** in hello **gestione API** menu hello toodisplay sinistro hello **prodotti** pagina.</span><span class="sxs-lookup"><span data-stu-id="39cfd-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="39cfd-116">Fare clic su **Aggiungi prodotto** toodisplay hello **Aggiungi nuovo prodotto** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Aggiungi nuovo prodotto][api-management-new-product-window]

<span data-ttu-id="39cfd-118">In hello **titolo** digitare **versione di valutazione gratuita**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="39cfd-119">In hello **descrizione** casella, hello di tipo testo seguente: **i sottoscrittori non saranno in grado di toorun 10 chiamate al minuto backup tooa massimo di 200 chiamate/settimana dopo il quale viene negato l'accesso.**</span><span class="sxs-lookup"><span data-stu-id="39cfd-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="39cfd-120">Lo stato dei prodotti in Gestione API può essere Aperto o Protetto.</span><span class="sxs-lookup"><span data-stu-id="39cfd-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="39cfd-121">Prodotti protetti devono essere toobefore sottoscritti possono essere utilizzati.</span><span class="sxs-lookup"><span data-stu-id="39cfd-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="39cfd-122">mentre i prodotti aperti possono essere usati senza sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="39cfd-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="39cfd-123">Verificare che **richiedono sottoscrizione** è toocreate selezionato un prodotto protetto che richiede una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="39cfd-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="39cfd-124">Questo è l'impostazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-124">This is hello default setting.</span></span>

<span data-ttu-id="39cfd-125">Se si desidera che un amministratore tooreview e accettare o rifiutare la sottoscrizione tenta toothis prodotto, selezionare **richiedono l'approvazione della sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="39cfd-126">Se la casella di controllo hello non è selezionata, i tentativi di sottoscrizione sarà approvata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="39cfd-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="39cfd-127">In questo esempio, le sottoscrizioni vengono approvate automaticamente, in modo non si seleziona la casella hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="39cfd-128">sviluppatore tooallow account toosubscribe nuovo prodotto toohello più volte, seleziona hello **può supportare più sottoscrizioni simultanee** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="39cfd-129">Questa esercitazione non prevede l'uso di più sottoscrizioni simultanee, quindi lasciare la casella deselezionata.</span><span class="sxs-lookup"><span data-stu-id="39cfd-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="39cfd-130">Dopo avere immesso tutti i valori, fare clic su **salvare** prodotto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="39cfd-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="39cfd-132">Per impostazione predefinita, i nuovi prodotti sono toousers visibile in hello **amministratori** gruppo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="39cfd-133">Verrà hello tooadd **sviluppatori** gruppo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="39cfd-134">Fare clic su **versione di valutazione gratuita**, quindi fare clic su hello **visibilità** scheda.</span><span class="sxs-lookup"><span data-stu-id="39cfd-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="39cfd-135">In Gestione API, i gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="39cfd-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="39cfd-136">Prodotti concedono toogroups visibilità e gli sviluppatori possono visualizzare e sottoscrivere i prodotti toohello toohello visibili i gruppi in cui appartengono.</span><span class="sxs-lookup"><span data-stu-id="39cfd-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="39cfd-137">Per ulteriori informazioni, vedere [come toocreate e utilizzare i gruppi in Gestione API di Azure][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="39cfd-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="39cfd-139">Seleziona hello **sviluppatori** casella di controllo e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="39cfd-140"><a name="add-api"></a>tooadd un'API toohello prodotto</span><span class="sxs-lookup"><span data-stu-id="39cfd-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="39cfd-141">In questo passaggio dell'esercitazione hello, si aggiungeranno hello API Echo toohello nuova versione di valutazione gratuita del prodotto.</span><span class="sxs-lookup"><span data-stu-id="39cfd-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="39cfd-142">Ogni istanza del servizio Gestione API preconfigurata con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API.</span><span class="sxs-lookup"><span data-stu-id="39cfd-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="39cfd-143">Per altre informazioni, vedere [Gestire la prima API in Gestione API di Azure][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="39cfd-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="39cfd-144">Fare clic su **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **versione di valutazione gratuita** prodotto hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="39cfd-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="39cfd-146">Fare clic su **tooproduct aggiungere API**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-146">Click **Add API tooproduct**.</span></span>

![Aggiungere tooproduct API][api-management-add-api]

<span data-ttu-id="39cfd-148">Selezionare **Echo API** (API Echo) e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="39cfd-150"><a name="policies"></a>tooconfigure criteri di limite e quota di frequenza delle chiamate</span><span class="sxs-lookup"><span data-stu-id="39cfd-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="39cfd-151">I limiti di velocità e le quote sono configurate nell'editor Criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="39cfd-152">i criteri di Hello due verrà aggiunta in questa esercitazione sono hello [frequenza delle chiamate limite per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [Set quota di utilizzo per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) criteri.</span><span class="sxs-lookup"><span data-stu-id="39cfd-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="39cfd-153">Nell'ambito del prodotto hello, è necessario applicare questi criteri.</span><span class="sxs-lookup"><span data-stu-id="39cfd-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="39cfd-154">Fare clic su **criteri** in hello **gestione API** menu di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="39cfd-155">In hello **prodotto** elenco, fare clic su **versione di valutazione gratuita**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-155">In hello **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="39cfd-157">Fare clic su **Aggiungi criterio** tooimport hello modello di criteri e avviare la creazione di criteri di limite e una quota di frequenza hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Aggiungi criteri][api-management-add-policy]

<span data-ttu-id="39cfd-159">Frequenza limite e quota criteri vengono in ingresso, in tal caso posizione hello cursore nell'elemento di hello in ingresso.</span><span class="sxs-lookup"><span data-stu-id="39cfd-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="39cfd-161">Scorrere l'elenco di hello dei criteri e individuare hello **frequenza delle chiamate limite per ogni sottoscrizione** voce di criterio.</span><span class="sxs-lookup"><span data-stu-id="39cfd-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="39cfd-163">Dopo aver hello cursore viene posizionato nel hello **in ingresso** elemento dei criteri, fare clic sulla freccia di hello accanto a **frequenza delle chiamate limite per ogni sottoscrizione** tooinsert il relativo modello di criteri.</span><span class="sxs-lookup"><span data-stu-id="39cfd-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="39cfd-164">Come si può vedere dal frammento di codice hello, criteri hello consentono l'impostazione dei limiti per le API del prodotto hello e le operazioni.</span><span class="sxs-lookup"><span data-stu-id="39cfd-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="39cfd-165">In questa esercitazione è non utilizzare tale funzionalità, quindi eliminare hello **api** e **operazione** gli elementi da hello **limite di velocità** elemento, tale che solo hello outer **limite di velocità** rimarrà elemento, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="39cfd-166">Nel prodotto di valutazione gratuita di hello, frequenza massima consentita di chiamata hello è 10 chiamate al minuto, quindi digitare **10** come valore hello hello **chiamate** attributo, e **60** per hello **periodo di rinnovo** attributo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="39cfd-167">hello tooconfigure **Set quota di utilizzo per ogni sottoscrizione** criteri, posizione del cursore immediatamente di sotto di hello appena aggiunti **limite di velocità** elemento all'interno di hello **in ingresso** elemento, quindi individuare e fare clic su hello freccia toohello sinistro **Set quota di utilizzo per ogni sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="39cfd-168">Allo stesso modo toohello **Set quota di utilizzo per ogni sottoscrizione** criteri, **Set quota di utilizzo per ogni sottoscrizione** criteri consentono l'impostazione di delimitatori per le API del prodotto hello e operazioni.</span><span class="sxs-lookup"><span data-stu-id="39cfd-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="39cfd-169">In questa esercitazione è non utilizzare tale funzionalità, quindi eliminare hello **api** e **operazione** gli elementi da hello **quota** elemento, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="39cfd-170">Le quote possono essere basate sul numero di hello chiamate per intervallo, la larghezza di banda o entrambi.</span><span class="sxs-lookup"><span data-stu-id="39cfd-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="39cfd-171">In questa esercitazione è non stiamo la limitazione della larghezza di banda in base, quindi eliminare hello **della larghezza di banda** attributo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="39cfd-172">Nel prodotto di valutazione gratuita di hello, quota hello è 200 chiamate alla settimana.</span><span class="sxs-lookup"><span data-stu-id="39cfd-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="39cfd-173">Specificare **200** come valore hello hello **chiamate** attributo e quindi specificare **604800** come valore hello hello **periodo di rinnovo** attributo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="39cfd-174">Gli intervalli dei criteri sono specificati in secondi.</span><span class="sxs-lookup"><span data-stu-id="39cfd-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="39cfd-175">intervallo di hello toocalculate per una settimana, è possibile moltiplicare hello numero di giorni (7 tramite un numero di ore del giorno (24) tramite un numero di minuti in un'ora (60) tramite un numero di secondi in un minuto (60) hello hello hello): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="39cfd-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="39cfd-176">Al termine della configurazione dei criteri di hello, deve corrispondere a hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="39cfd-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="39cfd-177">Dopo hello desiderato sono configurati i criteri, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-177">After hello desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="39cfd-179"><a name="publish-product"></a> prodotto hello toopublish</span><span class="sxs-lookup"><span data-stu-id="39cfd-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="39cfd-180">Ora che hello hello API vengono aggiunti e configurati i criteri di hello, prodotto hello deve essere pubblicata in modo che possono essere usata dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="39cfd-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="39cfd-181">Fare clic su **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **versione di valutazione gratuita** prodotto hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="39cfd-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="39cfd-183">Fare clic su **pubblica**, quindi fare clic su **Sì, pubblicarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="39cfd-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Pubblicazione prodotto][api-management-publish-product]

## <span data-ttu-id="39cfd-185"><a name="subscribe-account"></a>toosubscribe un prodotto di toohello account sviluppatore</span><span class="sxs-lookup"><span data-stu-id="39cfd-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="39cfd-186">Ora prodotto hello viene pubblicato, è disponibile toobe sottoscritto tooand utilizzato dagli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="39cfd-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="39cfd-187">Gli amministratori di un'istanza di gestione API sono prodotto tooevery automaticamente sottoscritto.</span><span class="sxs-lookup"><span data-stu-id="39cfd-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="39cfd-188">In questo passaggio dell'esercitazione, verrà sottoscrivere uno dei prodotti di hello developer non amministratore account toohello versione di valutazione gratuita.</span><span class="sxs-lookup"><span data-stu-id="39cfd-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="39cfd-189">Se l'account sviluppatore fa parte del ruolo amministratori di hello, è possibile proseguire con questo passaggio, anche se già iscritto.</span><span class="sxs-lookup"><span data-stu-id="39cfd-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="39cfd-190">Fare clic su **utenti** su hello **gestione API** menu hello a sinistra e quindi fare clic su nome hello del tuo account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="39cfd-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="39cfd-191">In questo esempio, utilizziamo hello **Clayton Gragg** account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="39cfd-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="39cfd-193">Fare clic su **Aggiungi sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-193">Click **Add Subscription**.</span></span>

![Aggiungi sottoscrizione][api-management-add-subscription-menu]

<span data-ttu-id="39cfd-195">Selezionare **Free Trial** e quindi fare clic su **Sottoscrivi**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Aggiungi sottoscrizione][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="39cfd-197">In questa esercitazione, più sottoscrizioni simultanee non sono abilitate per il prodotto di valutazione gratuita di hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="39cfd-198">In questo caso, sarebbe sottoscrizione hello tooname richiesta, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Aggiungi sottoscrizione][api-management-add-subscription-multiple]

<span data-ttu-id="39cfd-200">Dopo aver fatto clic **Sottoscrivi**, hello prodotto viene visualizzato in hello **sottoscrizione** elenco per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Sottoscrizione aggiunta][api-management-subscription-added]

## <span data-ttu-id="39cfd-202"><a name="test-rate-limit"></a>toocall un limite di frequenza hello operazione e di test</span><span class="sxs-lookup"><span data-stu-id="39cfd-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="39cfd-203">Ora che hello prodotto di valutazione gratuita è configurato e pubblicato, è possibile chiamare alcune operazioni e testare i criteri di limite di frequenza hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="39cfd-204">Portale per sviluppatori di toohello commutatore facendo **portale per sviluppatori** nel menu superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="39cfd-206">Fare clic su **API** in hello menu superiore e quindi fare clic su **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Portale per sviluppatori][api-management-developer-portal-api-menu]

<span data-ttu-id="39cfd-208">Fare clic su **GET Resource** (GET su risorsa) e quindi su **Prova**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="39cfd-210">Mantenere i valori dei parametri di valore predefinito di hello e quindi selezionare la chiave di sottoscrizione per il prodotto di valutazione gratuita di hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Chiave della sottoscrizione][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="39cfd-212">Se si dispone di più sottoscrizioni, essere certi tooselect hello chiave **versione di valutazione gratuita**, o altri criteri hello che sono stati configurati nei passaggi precedenti hello sarà attiva.</span><span class="sxs-lookup"><span data-stu-id="39cfd-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="39cfd-213">Fare clic su **inviare**e quindi visualizzare la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="39cfd-214">Hello nota **stato della risposta** di **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="39cfd-214">Note hello **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="39cfd-216">Fare clic su **inviare** con una frequenza maggiore di criteri di limite di frequenza hello di 10 chiamate al minuto.</span><span class="sxs-lookup"><span data-stu-id="39cfd-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="39cfd-217">Criteri di limite di frequenza hello vengano superato, lo stato della risposta **429 troppo numerose richieste** viene restituito.</span><span class="sxs-lookup"><span data-stu-id="39cfd-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="39cfd-219">Hello **contenuto della risposta** indica hello rimanenti intervallo prima di tentativi sarà ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="39cfd-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="39cfd-220">Quando il criterio di limite di velocità di hello di 10 chiamate al minuto è attivo, le chiamate successive avrà esito negativo fino a 60 secondi trascorsi da hello prima del prodotto prima è stato superato il limite di velocità hello di hello 10 chiamate con esito positivo toohello.</span><span class="sxs-lookup"><span data-stu-id="39cfd-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="39cfd-221">In questo esempio hello rimanenti intervallo è 54 secondi.</span><span class="sxs-lookup"><span data-stu-id="39cfd-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="39cfd-222"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39cfd-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="39cfd-223">Osservare una dimostrazione dell'impostazione di limiti di velocità e le quote in hello seguente video.</span><span class="sxs-lookup"><span data-stu-id="39cfd-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
