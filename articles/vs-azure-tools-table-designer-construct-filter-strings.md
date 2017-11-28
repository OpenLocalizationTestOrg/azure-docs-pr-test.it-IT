---
title: Creazione di stringhe di filtro per Progettazione tabelle | Documentazione Microsoft
description: Creazione di stringhe di filtro per Progettazione tabelle
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
ms.openlocfilehash: 069224d84462b4955912ce1462a65298a5acc04a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="constructing-filter-strings-for-the-table-designer"></a><span data-ttu-id="062ce-103">Creazione di stringhe di filtro per Progettazione tabelle</span><span class="sxs-lookup"><span data-stu-id="062ce-103">Constructing Filter Strings for the Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="062ce-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="062ce-104">Overview</span></span>
<span data-ttu-id="062ce-105">Per filtrare i dati in una tabella di Azure visualizzata in **Progettazione tabelle**di Visual Studio, creare una stringa di filtro e immetterla nel campo del filtro.</span><span class="sxs-lookup"><span data-stu-id="062ce-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span></span> <span data-ttu-id="062ce-106">La sintassi della stringa di filtro è definita da WCF Data Services ed è simile a una clausola WHERE SQL, ma viene inviata al servizio tabelle con una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="062ce-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span></span> <span data-ttu-id="062ce-107">**Progettazione tabelle** gestisce automaticamente la codifica appropriata, quindi per filtrare in base a un valore di proprietà desiderato, è necessario immettere solo il nome della proprietà, l'operatore di confronto, il valore dei criteri e, facoltativamente, l'operatore booleano nel campo del filtro.</span><span class="sxs-lookup"><span data-stu-id="062ce-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span></span> <span data-ttu-id="062ce-108">Non è necessario includere l'opzione di query $filter come quando si crea un URL per eseguire la query della tabella in base alle [Informazioni di riferimento sulle API REST dei servizi di archiviazione](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="062ce-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="062ce-109">WCF Data Services si basa su [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="062ce-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="062ce-110">Per i dettagli sull'opzione di query del sistema di filtro (**$filter**), vedere la [specifica sulle convenzioni URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="062ce-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="062ce-111">Operatori di confronto</span><span class="sxs-lookup"><span data-stu-id="062ce-111">Comparison Operators</span></span>
<span data-ttu-id="062ce-112">Gli operatori logici seguenti sono supportati per tutti i tipi di proprietà:</span><span class="sxs-lookup"><span data-stu-id="062ce-112">The following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="062ce-113">Operatore logico</span><span class="sxs-lookup"><span data-stu-id="062ce-113">Logical operator</span></span> | <span data-ttu-id="062ce-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="062ce-114">Description</span></span> | <span data-ttu-id="062ce-115">Stringa di filtro di esempio</span><span class="sxs-lookup"><span data-stu-id="062ce-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="062ce-116">eq</span><span class="sxs-lookup"><span data-stu-id="062ce-116">eq</span></span> |<span data-ttu-id="062ce-117">Uguale</span><span class="sxs-lookup"><span data-stu-id="062ce-117">Equal</span></span> |<span data-ttu-id="062ce-118">Città eq "Redmond"</span><span class="sxs-lookup"><span data-stu-id="062ce-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="062ce-119">gt</span><span class="sxs-lookup"><span data-stu-id="062ce-119">gt</span></span> |<span data-ttu-id="062ce-120">Maggiore di</span><span class="sxs-lookup"><span data-stu-id="062ce-120">Greater than</span></span> |<span data-ttu-id="062ce-121">Prezzo gt 20</span><span class="sxs-lookup"><span data-stu-id="062ce-121">Price gt 20</span></span> |
| <span data-ttu-id="062ce-122">ge</span><span class="sxs-lookup"><span data-stu-id="062ce-122">ge</span></span> |<span data-ttu-id="062ce-123">Maggiore o uguale a</span><span class="sxs-lookup"><span data-stu-id="062ce-123">Greater than or equal to</span></span> |<span data-ttu-id="062ce-124">Prezzo ge 10</span><span class="sxs-lookup"><span data-stu-id="062ce-124">Price ge 10</span></span> |
| <span data-ttu-id="062ce-125">lt</span><span class="sxs-lookup"><span data-stu-id="062ce-125">lt</span></span> |<span data-ttu-id="062ce-126">Minore di</span><span class="sxs-lookup"><span data-stu-id="062ce-126">Less than</span></span> |<span data-ttu-id="062ce-127">Prezzo lt 20</span><span class="sxs-lookup"><span data-stu-id="062ce-127">Price lt 20</span></span> |
| <span data-ttu-id="062ce-128">le</span><span class="sxs-lookup"><span data-stu-id="062ce-128">le</span></span> |<span data-ttu-id="062ce-129">Minore o uguale</span><span class="sxs-lookup"><span data-stu-id="062ce-129">Less than or equal</span></span> |<span data-ttu-id="062ce-130">Prezzo le 100</span><span class="sxs-lookup"><span data-stu-id="062ce-130">Price le 100</span></span> |
| <span data-ttu-id="062ce-131">ne</span><span class="sxs-lookup"><span data-stu-id="062ce-131">ne</span></span> |<span data-ttu-id="062ce-132">Diverso</span><span class="sxs-lookup"><span data-stu-id="062ce-132">Not equal</span></span> |<span data-ttu-id="062ce-133">Città ne "Londra"</span><span class="sxs-lookup"><span data-stu-id="062ce-133">City ne 'London'</span></span> |
| <span data-ttu-id="062ce-134">e</span><span class="sxs-lookup"><span data-stu-id="062ce-134">and</span></span> |<span data-ttu-id="062ce-135">e</span><span class="sxs-lookup"><span data-stu-id="062ce-135">And</span></span> |<span data-ttu-id="062ce-136">Prezzo le 200 and Prezzo gt 3,5</span><span class="sxs-lookup"><span data-stu-id="062ce-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="062ce-137">oppure</span><span class="sxs-lookup"><span data-stu-id="062ce-137">or</span></span> |<span data-ttu-id="062ce-138">oppure</span><span class="sxs-lookup"><span data-stu-id="062ce-138">Or</span></span> |<span data-ttu-id="062ce-139">Prezzo le 3,5 or Prezzo gt 200</span><span class="sxs-lookup"><span data-stu-id="062ce-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="062ce-140">not</span><span class="sxs-lookup"><span data-stu-id="062ce-140">not</span></span> |<span data-ttu-id="062ce-141">not</span><span class="sxs-lookup"><span data-stu-id="062ce-141">Not</span></span> |<span data-ttu-id="062ce-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="062ce-142">not isAvailable</span></span> |

<span data-ttu-id="062ce-143">Quando si crea una stringa di filtro, tenere presente le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="062ce-143">When constructing a filter string, the following rules are important:</span></span>

* <span data-ttu-id="062ce-144">Usare gli operatori logici per confrontare una proprietà con un valore.</span><span class="sxs-lookup"><span data-stu-id="062ce-144">Use the logical operators to compare a property to a value.</span></span> <span data-ttu-id="062ce-145">Si noti che non è possibile confrontare una proprietà con un valore dinamico. Un elemento dell'espressione deve essere una costante.</span><span class="sxs-lookup"><span data-stu-id="062ce-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span></span>
* <span data-ttu-id="062ce-146">Viene effettuata la distinzione tra maiuscole e minuscole per tutte le parti della stringa di filtro.</span><span class="sxs-lookup"><span data-stu-id="062ce-146">All parts of the filter string are case-sensitive.</span></span>
* <span data-ttu-id="062ce-147">Il valore costante deve essere dello stesso tipo di dati della proprietà affinché il filtro restituisca risultati validi.</span><span class="sxs-lookup"><span data-stu-id="062ce-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="062ce-148">Per altre informazioni sui tipi di proprietà supportati, vedere [Informazioni sul modello di dati del servizio tabelle](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="062ce-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="062ce-149">Applicazione di filtri alle proprietà della stringa</span><span class="sxs-lookup"><span data-stu-id="062ce-149">Filtering on String Properties</span></span>
<span data-ttu-id="062ce-150">Quando si applicano filtri alle proprietà della stringa, includere la costante di stringa tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="062ce-150">When you filter on string properties, enclose the string constant in single quotation marks.</span></span>

<span data-ttu-id="062ce-151">L'esempio seguente applica filtri alle proprietà **PartitionKey** e **RowKey**. Alla stringa di filtro possono essere aggiunte anche altre proprietà non chiave:</span><span class="sxs-lookup"><span data-stu-id="062ce-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="062ce-152">Anche se non è necessario, è possibile racchiudere ogni espressione di filtro tra parentesi:</span><span class="sxs-lookup"><span data-stu-id="062ce-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="062ce-153">Si noti che le query con caratteri jolly non sono supportate né nel servizio tabelle né in Progettazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="062ce-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span></span> <span data-ttu-id="062ce-154">Tuttavia, è possibile eseguire la corrispondenza di prefissi usando gli operatori di confronto sul prefisso desiderato.</span><span class="sxs-lookup"><span data-stu-id="062ce-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span></span> <span data-ttu-id="062ce-155">L'esempio seguente restituisce le entità con una proprietà LastName che inizia con la lettera "A":</span><span class="sxs-lookup"><span data-stu-id="062ce-155">The following example returns entities with a LastName property beginning with the letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="062ce-156">Applicazione di filtri alle proprietà numeriche</span><span class="sxs-lookup"><span data-stu-id="062ce-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="062ce-157">Per applicare filtri a un numero intero o a virgola mobile, specificare il numero senza virgolette.</span><span class="sxs-lookup"><span data-stu-id="062ce-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span></span>

<span data-ttu-id="062ce-158">Questo esempio restituisce tutte le entità con una proprietà Age il cui valore è maggiore di 30:</span><span class="sxs-lookup"><span data-stu-id="062ce-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="062ce-159">Questo esempio restituisce tutte le entità con una proprietà AmountDue il cui valore è minore o uguale a 100,25:</span><span class="sxs-lookup"><span data-stu-id="062ce-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="062ce-160">Applicazione di filtri alle proprietà booleane</span><span class="sxs-lookup"><span data-stu-id="062ce-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="062ce-161">Per applicare filtri a un valoppuree booleano, specificare **true** oppure **false** senza virgolette.</span><span class="sxs-lookup"><span data-stu-id="062ce-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="062ce-162">L'esempio seguente restituisce tutte le entità in cui la proprietà IsActive è impostata su **true**:</span><span class="sxs-lookup"><span data-stu-id="062ce-162">The following example returns all entities where the IsActive property is set to **true**:</span></span>

    IsActive eq true

<span data-ttu-id="062ce-163">Questa espressione di filtro può essere scritta anche senza operatore logico.</span><span class="sxs-lookup"><span data-stu-id="062ce-163">You can also write this filter expression without the logical operator.</span></span> <span data-ttu-id="062ce-164">Nell'esempio seguente il servizio tabelle restituirà anche tutte le entità in cui IsActive è **true**:</span><span class="sxs-lookup"><span data-stu-id="062ce-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="062ce-165">Per restituire tutte le entità in cui IsActive è false, è possibile usare l'operatore not:</span><span class="sxs-lookup"><span data-stu-id="062ce-165">To return all entities where IsActive is false, you can use the not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="062ce-166">Applicazione di filtri alle proprietà DateTime</span><span class="sxs-lookup"><span data-stu-id="062ce-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="062ce-167">Per applicare filtri a un valore DateTime, specificare la parola chiave **datetime** , seguita dalla costante data/ora tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="062ce-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span></span> <span data-ttu-id="062ce-168">La costante data/ora tra virgolette singole deve essere nel formato UTC combinato, come descritto in [Formattazione di valori della proprietà DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="062ce-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="062ce-169">L'esempio seguente restituisce le entità in cui la proprietà CustomerSince è uguale a 10 luglio 2008:</span><span class="sxs-lookup"><span data-stu-id="062ce-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
