---
title: stringhe di filtro aaaConstructing per Progettazione tabelle hello | Documenti Microsoft
description: Creazione di stringhe di filtro per Progettazione tabelle hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="99f01-103">Creazione di stringhe di filtro per hello Progettazione tabelle</span><span class="sxs-lookup"><span data-stu-id="99f01-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="99f01-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="99f01-104">Overview</span></span>
<span data-ttu-id="99f01-105">toofilter dati in una tabella di Azure che viene visualizzato in Visual Studio di hello **Progettazione tabelle**, si costruisce una stringa di filtro e immetterla nel campo filtro hello.</span><span class="sxs-lookup"><span data-stu-id="99f01-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="99f01-106">sintassi della stringa di filtro Hello è definita da WCF Data Services hello ed è simile tooa clausola SQL WHERE, ma viene inviata toohello servizio tabella tramite una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="99f01-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="99f01-107">Hello **Progettazione tabelle** handle hello codifica appropriata, quindi toofilter su un valore di proprietà desiderato, è necessario immettere solo nome della proprietà hello, operatore di confronto, valore dei criteri, e, facoltativamente, il filtro operatore booleano hello campo.</span><span class="sxs-lookup"><span data-stu-id="99f01-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="99f01-108">Non è necessaria l'opzione query hello $filter tooinclude come se si costruisce una tabella di hello tooquery URL tramite hello [riferimento all'API REST di servizi di archiviazione](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="99f01-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="99f01-109">Hello WCF Data Services si basa su hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="99f01-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="99f01-110">Per informazioni dettagliate sull'opzione di query di sistema di filtro hello (**$filter**), vedere hello [specifica di convenzioni URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="99f01-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="99f01-111">Operatori di confronto</span><span class="sxs-lookup"><span data-stu-id="99f01-111">Comparison Operators</span></span>
<span data-ttu-id="99f01-112">Hello seguenti operatori logici sono supportati per tutti i tipi di proprietà:</span><span class="sxs-lookup"><span data-stu-id="99f01-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="99f01-113">Operatore logico</span><span class="sxs-lookup"><span data-stu-id="99f01-113">Logical operator</span></span> | <span data-ttu-id="99f01-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="99f01-114">Description</span></span> | <span data-ttu-id="99f01-115">Stringa di filtro di esempio</span><span class="sxs-lookup"><span data-stu-id="99f01-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99f01-116">eq</span><span class="sxs-lookup"><span data-stu-id="99f01-116">eq</span></span> |<span data-ttu-id="99f01-117">Uguale</span><span class="sxs-lookup"><span data-stu-id="99f01-117">Equal</span></span> |<span data-ttu-id="99f01-118">Città eq "Redmond"</span><span class="sxs-lookup"><span data-stu-id="99f01-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="99f01-119">gt</span><span class="sxs-lookup"><span data-stu-id="99f01-119">gt</span></span> |<span data-ttu-id="99f01-120">Maggiore di</span><span class="sxs-lookup"><span data-stu-id="99f01-120">Greater than</span></span> |<span data-ttu-id="99f01-121">Prezzo gt 20</span><span class="sxs-lookup"><span data-stu-id="99f01-121">Price gt 20</span></span> |
| <span data-ttu-id="99f01-122">ge</span><span class="sxs-lookup"><span data-stu-id="99f01-122">ge</span></span> |<span data-ttu-id="99f01-123">Maggiore o uguale troppo</span><span class="sxs-lookup"><span data-stu-id="99f01-123">Greater than or equal too</span></span>|<span data-ttu-id="99f01-124">Prezzo ge 10</span><span class="sxs-lookup"><span data-stu-id="99f01-124">Price ge 10</span></span> |
| <span data-ttu-id="99f01-125">lt</span><span class="sxs-lookup"><span data-stu-id="99f01-125">lt</span></span> |<span data-ttu-id="99f01-126">Minore di</span><span class="sxs-lookup"><span data-stu-id="99f01-126">Less than</span></span> |<span data-ttu-id="99f01-127">Prezzo lt 20</span><span class="sxs-lookup"><span data-stu-id="99f01-127">Price lt 20</span></span> |
| <span data-ttu-id="99f01-128">le</span><span class="sxs-lookup"><span data-stu-id="99f01-128">le</span></span> |<span data-ttu-id="99f01-129">Minore o uguale</span><span class="sxs-lookup"><span data-stu-id="99f01-129">Less than or equal</span></span> |<span data-ttu-id="99f01-130">Prezzo le 100</span><span class="sxs-lookup"><span data-stu-id="99f01-130">Price le 100</span></span> |
| <span data-ttu-id="99f01-131">ne</span><span class="sxs-lookup"><span data-stu-id="99f01-131">ne</span></span> |<span data-ttu-id="99f01-132">Diverso</span><span class="sxs-lookup"><span data-stu-id="99f01-132">Not equal</span></span> |<span data-ttu-id="99f01-133">Città ne "Londra"</span><span class="sxs-lookup"><span data-stu-id="99f01-133">City ne 'London'</span></span> |
| <span data-ttu-id="99f01-134">e</span><span class="sxs-lookup"><span data-stu-id="99f01-134">and</span></span> |<span data-ttu-id="99f01-135">e</span><span class="sxs-lookup"><span data-stu-id="99f01-135">And</span></span> |<span data-ttu-id="99f01-136">Prezzo le 200 and Prezzo gt 3,5</span><span class="sxs-lookup"><span data-stu-id="99f01-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="99f01-137">oppure</span><span class="sxs-lookup"><span data-stu-id="99f01-137">or</span></span> |<span data-ttu-id="99f01-138">oppure</span><span class="sxs-lookup"><span data-stu-id="99f01-138">Or</span></span> |<span data-ttu-id="99f01-139">Prezzo le 3,5 or Prezzo gt 200</span><span class="sxs-lookup"><span data-stu-id="99f01-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="99f01-140">not</span><span class="sxs-lookup"><span data-stu-id="99f01-140">not</span></span> |<span data-ttu-id="99f01-141">not</span><span class="sxs-lookup"><span data-stu-id="99f01-141">Not</span></span> |<span data-ttu-id="99f01-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="99f01-142">not isAvailable</span></span> |

<span data-ttu-id="99f01-143">Quando si crea una stringa di filtro, hello regole seguenti sono importanti:</span><span class="sxs-lookup"><span data-stu-id="99f01-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="99f01-144">Utilizzare gli operatori logici di hello toocompare tooa valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="99f01-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="99f01-145">Si noti che non è possibile toocompare tooa dinamica valore della proprietà; un lato dell'espressione hello deve essere una costante.</span><span class="sxs-lookup"><span data-stu-id="99f01-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="99f01-146">Tutte le parti della stringa di filtro hello maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="99f01-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="99f01-147">valore costante Hello deve essere di hello del tipo di dati stesso come proprietà hello affinché hello filtro tooreturn valido risultati.</span><span class="sxs-lookup"><span data-stu-id="99f01-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="99f01-148">Per ulteriori informazioni sui tipi di proprietà supportati, vedere [hello comprensione modello di dati del servizio tabelle](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="99f01-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="99f01-149">Applicazione di filtri alle proprietà della stringa</span><span class="sxs-lookup"><span data-stu-id="99f01-149">Filtering on String Properties</span></span>
<span data-ttu-id="99f01-150">Quando si filtra le proprietà della stringa, racchiudere la costante di stringa hello tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="99f01-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="99f01-151">Hello seguendo i filtri di esempio hello **PartitionKey** e **RowKey** proprietà; chiave ulteriore proprietà anche possibile aggiungere la stringa di filtro toohello:</span><span class="sxs-lookup"><span data-stu-id="99f01-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="99f01-152">Anche se non è necessario, è possibile racchiudere ogni espressione di filtro tra parentesi:</span><span class="sxs-lookup"><span data-stu-id="99f01-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="99f01-153">Si noti che hello del servizio tabelle non supporta query con caratteri jolly non sono supportate sia in Progettazione tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="99f01-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="99f01-154">Tuttavia, è possibile eseguire utilizzando gli operatori di confronto sul prefisso desiderato hello di corrispondenza dei prefissi.</span><span class="sxs-lookup"><span data-stu-id="99f01-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="99f01-155">Hello esempio seguente vengono restituite le entità con una proprietà LastName che inizia con la lettera hello 'A':</span><span class="sxs-lookup"><span data-stu-id="99f01-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="99f01-156">Applicazione di filtri alle proprietà numeriche</span><span class="sxs-lookup"><span data-stu-id="99f01-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="99f01-157">toofilter su un numero intero o un numero a virgola mobile, specificare il numero di hello senza virgolette.</span><span class="sxs-lookup"><span data-stu-id="99f01-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="99f01-158">Questo esempio restituisce tutte le entità con una proprietà Age il cui valore è maggiore di 30:</span><span class="sxs-lookup"><span data-stu-id="99f01-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="99f01-159">Questo esempio vengono restituite tutte le entità con una proprietà AmountDue il cui valore è minore o uguale a too100.25:</span><span class="sxs-lookup"><span data-stu-id="99f01-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="99f01-160">Applicazione di filtri alle proprietà booleane</span><span class="sxs-lookup"><span data-stu-id="99f01-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="99f01-161">toofilter su un valore booleano, specificare **true** o **false** senza virgolette.</span><span class="sxs-lookup"><span data-stu-id="99f01-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="99f01-162">Hello esempio seguente restituisce tutte le entità in cui hello proprietà IsActive è impostata troppo**true**:</span><span class="sxs-lookup"><span data-stu-id="99f01-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="99f01-163">È anche possibile scrivere questa espressione di filtro senza operatore logico hello.</span><span class="sxs-lookup"><span data-stu-id="99f01-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="99f01-164">Nell'esempio seguente di hello, hello servizio tabella restituirà anche tutte le entità in cui IsActive è **true**:</span><span class="sxs-lookup"><span data-stu-id="99f01-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="99f01-165">tutte le entità in cui IsActive è false, è possibile utilizzare hello non tooreturn operatore:</span><span class="sxs-lookup"><span data-stu-id="99f01-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="99f01-166">Applicazione di filtri alle proprietà DateTime</span><span class="sxs-lookup"><span data-stu-id="99f01-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="99f01-167">toofilter su un valore DateTime, specificare hello **datetime** (parola chiave), seguita dalla costante data/ora hello tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="99f01-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="99f01-168">costante di data/ora Hello deve essere in formato UTC combinato, come descritto [la formattazione dei valori di proprietà DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="99f01-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="99f01-169">Hello di esempio seguente restituisce le entità in proprietà CustomerSince hello è uguale tooJuly 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="99f01-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
