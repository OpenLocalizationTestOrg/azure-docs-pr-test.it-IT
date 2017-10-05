---
title: Uso dei dati geospaziali in Azure Cosmos DB | Microsoft Docs
description: Informazioni su come creare, indicizzare ed eseguire query su oggetti spaziali con Azure Cosmos DB e l'API di DocumentDB.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="1ed53-103">Uso dei dati geospaziali e dei dati località GeoJSON in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1ed53-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="1ed53-104">Questo articolo offre un'introduzione alla funzionalità geospaziale in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1ed53-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="1ed53-105">Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ed53-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="1ed53-106">Come si archiviano i dati spaziali in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="1ed53-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="1ed53-107">Come si eseguono query su dati geospaziali in Azure Cosmos DB in SQL e LINQ?</span><span class="sxs-lookup"><span data-stu-id="1ed53-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="1ed53-108">Come si abilita o disabilita l'indicizzazione spaziale in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="1ed53-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="1ed53-109">Questo articolo illustra come usare i dati spaziali con l'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="1ed53-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="1ed53-110">Consultare il [progetto GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) per esempi di codice.</span><span class="sxs-lookup"><span data-stu-id="1ed53-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="1ed53-111">Introduzione ai dati spaziali</span><span class="sxs-lookup"><span data-stu-id="1ed53-111">Introduction to spatial data</span></span>
<span data-ttu-id="1ed53-112">I dati spaziali descrivono la posizione e la forma degli oggetti nello spazio.</span><span class="sxs-lookup"><span data-stu-id="1ed53-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="1ed53-113">Nella maggior parte delle applicazioni, questi corrispondono a oggetti sulla terra, vale a dire dati geospaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="1ed53-114">I dati spaziali possono essere utilizzati per rappresentare la posizione di una persona, un luogo di interesse o i confini di una città o di un lago.</span><span class="sxs-lookup"><span data-stu-id="1ed53-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="1ed53-115">Casi di utilizzo comuni includono spesso query di prossimità, ad esempio, "trova tutti i negozi vicino alla mia posizione attuale".</span><span class="sxs-lookup"><span data-stu-id="1ed53-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="1ed53-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="1ed53-116">GeoJSON</span></span>
<span data-ttu-id="1ed53-117">Azure Cosmos DB supporta l'indicizzazione e le query dei dati di punti geospaziali rappresentati tramite la [specifica GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="1ed53-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="1ed53-118">Le strutture di dati GeoJSON sono sempre oggetti JSON validi, quindi possono essere archiviate e sottoposte a query usando Azure Cosmos DB senza librerie o strumenti specializzati.</span><span class="sxs-lookup"><span data-stu-id="1ed53-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="1ed53-119">Gli SDK di Azure Cosmos DB forniscono classi helper e metodi che semplificano il lavoro con i dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="1ed53-120">Punti, oggetti linestring e poligoni</span><span class="sxs-lookup"><span data-stu-id="1ed53-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="1ed53-121">Un **punto** indica una posizione singola nello spazio.</span><span class="sxs-lookup"><span data-stu-id="1ed53-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="1ed53-122">Nei dati geospaziali, un punto rappresenta la posizione esatta, che può essere un indirizzo di un negozio, un chiosco, un'automobile o una città.</span><span class="sxs-lookup"><span data-stu-id="1ed53-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="1ed53-123">Un punto viene rappresentato in GeoJSON (e Azure Cosmos DB) tramite la sua coppia di coordinate o longitudine e latitudine.</span><span class="sxs-lookup"><span data-stu-id="1ed53-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="1ed53-124">Di seguito è riportato un esempio JSON per un punto.</span><span class="sxs-lookup"><span data-stu-id="1ed53-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="1ed53-125">**Punti in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="1ed53-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="1ed53-126">GeoJSON specifica la longitudine prima e la latitudine dopo.</span><span class="sxs-lookup"><span data-stu-id="1ed53-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="1ed53-127">Come in altre applicazioni di mapping, longitudine e latitudine sono angoli e sono espresse in gradi.</span><span class="sxs-lookup"><span data-stu-id="1ed53-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="1ed53-128">I valori della longitudine vengono misurati dal meridiano principale e sono compresi tra -180° e 180,0° gradi, mentre i valori della latitudine sono misurati dall'equatore e sono compresi tra -90,0° e 90,0°.</span><span class="sxs-lookup"><span data-stu-id="1ed53-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="1ed53-129">Azure Cosmos DB interpreta le coordinate come rappresentate secondo il sistema di riferimento WGS-84.</span><span class="sxs-lookup"><span data-stu-id="1ed53-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="1ed53-130">Per ulteriori informazioni sui sistemi di coordinate di riferimento, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="1ed53-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="1ed53-131">I punti possono essere incorporati in un documento di Azure Cosmos DB come illustrato in questo esempio di profilo utente contenente dati di località:</span><span class="sxs-lookup"><span data-stu-id="1ed53-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="1ed53-132">**Usare un profilo con località archiviata in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="1ed53-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="1ed53-133">Oltre ai punti, GeoJSON supporta oggetti linestring e poligoni.</span><span class="sxs-lookup"><span data-stu-id="1ed53-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="1ed53-134">**LineStrings** rappresentano una serie di due o più punti nello spazio e i segmenti lineari che li connettono.</span><span class="sxs-lookup"><span data-stu-id="1ed53-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="1ed53-135">Nei dati geospaziali, gli oggetti linestring di solito vengono usati per rappresentare autostrade o fiumi.</span><span class="sxs-lookup"><span data-stu-id="1ed53-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="1ed53-136">Un oggetto **poligono** è un perimetro costituito da punti connessi che forma un elemento LineString chiuso.</span><span class="sxs-lookup"><span data-stu-id="1ed53-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="1ed53-137">I poligoni vengono comunemente utilizzati per rappresentare formazioni naturali come laghi o giurisdizioni politiche come città e stati.</span><span class="sxs-lookup"><span data-stu-id="1ed53-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="1ed53-138">Di seguito è riportato un esempio di poligono in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1ed53-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="1ed53-139">**Poligoni in GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="1ed53-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> <span data-ttu-id="1ed53-140">La specifica GeoJSON richiede che per i poligoni validi l'ultima coppia di coordinate indicata corrisponda alla prima, in modo da creare una forma chiusa.</span><span class="sxs-lookup"><span data-stu-id="1ed53-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="1ed53-141">I punti all'interno di un poligono devono essere specificati in senso antiorario.</span><span class="sxs-lookup"><span data-stu-id="1ed53-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="1ed53-142">Un poligono specificato in senso orario rappresenta l'inverso dell'area al suo interno.</span><span class="sxs-lookup"><span data-stu-id="1ed53-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="1ed53-143">Oltre a punto, LineString e poligono, GeoJSON specifica inoltre la rappresentazione della modalità di raggruppamento di più posizioni geospaziali, nonché come associare proprietà arbitrarie alla georilevazione come **Caratteristica**.</span><span class="sxs-lookup"><span data-stu-id="1ed53-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="1ed53-144">Trattandosi di oggetti JSON validi, essi possono essere archiviati ed elaborati tutti in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1ed53-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="1ed53-145">Azure Cosmos DB supporta tuttavia solo l'indicizzazione automatica dei punti.</span><span class="sxs-lookup"><span data-stu-id="1ed53-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="1ed53-146">Sistemi di riferimento delle coordinate</span><span class="sxs-lookup"><span data-stu-id="1ed53-146">Coordinate reference systems</span></span>
<span data-ttu-id="1ed53-147">Poiché la forma della terra è irregolare, le coordinate dei dati geospaziali sono rappresentate in molti sistemi di coordinate di riferimento (CRS), ognuno con la propria struttura di riferimento e le proprie unità di misura.</span><span class="sxs-lookup"><span data-stu-id="1ed53-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="1ed53-148">Ad esempio, il "National Grid of Britain" è un sistema di riferimento molto accurato per il Regno Unito, ma non al suo esterno.</span><span class="sxs-lookup"><span data-stu-id="1ed53-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="1ed53-149">Il più diffuso CRS attualmente in uso è il World Geodetic System [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="1ed53-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="1ed53-150">Dispositivi GPS e molti servizi di mapping, tra cui Google Maps e le API di Bing Maps, utilizzano WGS-84.</span><span class="sxs-lookup"><span data-stu-id="1ed53-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="1ed53-151">Azure Cosmos DB supporta l'indicizzazione e l'esecuzione di query di dati geospaziali usando solo il CRS WGS-84.</span><span class="sxs-lookup"><span data-stu-id="1ed53-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="1ed53-152">Creazione di documenti con dati spaziali</span><span class="sxs-lookup"><span data-stu-id="1ed53-152">Creating documents with spatial data</span></span>
<span data-ttu-id="1ed53-153">Quando si creano documenti che contengono valori GeoJSON, essi vengono indicizzati automaticamente con un indice spaziale in base al criterio di indicizzazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="1ed53-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="1ed53-154">Se si usa un SDK di Azure Cosmos DB in un linguaggio tipizzato in modo dinamico come Python o Node.js, è necessario creare un GeoJSON valido.</span><span class="sxs-lookup"><span data-stu-id="1ed53-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="1ed53-155">**Creare documenti con i dati geospaziali in Node.js**</span><span class="sxs-lookup"><span data-stu-id="1ed53-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="1ed53-156">Se si lavora con le API di DocumentDB, è possibile usare le classi `Point` e `Polygon` all'interno dello spazio dei nomi `Microsoft.Azure.Documents.Spatial` per incorporare le informazioni sulla località all'interno di oggetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ed53-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="1ed53-157">Queste classi consentono di semplificare la serializzazione e la deserializzazione dei dati spaziali in GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="1ed53-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="1ed53-158">**Creare documenti con i dati geospaziali in .NET**</span><span class="sxs-lookup"><span data-stu-id="1ed53-158">**Create Document with Geospatial data in .NET**</span></span>

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="1ed53-159">Se non si dispone delle informazioni di latitudine e longitudine, ma si dispone di indirizzi fisici o del nome della posizione come la città o il paese, è possibile cercare le coordinate effettive tramite un servizio di geocodifica come i servizi REST di Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="1ed53-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="1ed53-160">Ulteriori informazioni sulla geocodifica di Bing Maps sono disponibili [qui](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed53-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="1ed53-161">Query sui tipi spaziali</span><span class="sxs-lookup"><span data-stu-id="1ed53-161">Querying spatial types</span></span>
<span data-ttu-id="1ed53-162">Dopo aver compreso come inserire i dati geospaziali, è ora possibile esaminare come eseguire query sui dati usando Azure Cosmos DB e LINQ.</span><span class="sxs-lookup"><span data-stu-id="1ed53-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="1ed53-163">Funzioni predefinite spaziali di SQL</span><span class="sxs-lookup"><span data-stu-id="1ed53-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="1ed53-164">Azure Cosmos DB supporta le seguenti funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="1ed53-165">Per altre informazioni sul set completo di funzioni predefinite del linguaggio SQL, vedere [Query di Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="1ed53-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="1ed53-166"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="1ed53-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="1ed53-167"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="1ed53-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1ed53-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1ed53-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1ed53-169">Restituisce la distanza tra le due espressioni GeoJSON punto, poligono o LineString.</span><span class="sxs-lookup"><span data-stu-id="1ed53-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1ed53-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1ed53-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1ed53-171">Restituisce un'espressione booleana che indica se il primo oggetto GeoJSON (punto, poligono o LineString) è all'interno del secondo oggetto GeoJSON (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="1ed53-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1ed53-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1ed53-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1ed53-173">Restituisce un'espressione booleana che indica se i due oggetti GeoJSON specificati (punto, poligono o LineString) si intersecano.</span><span class="sxs-lookup"><span data-stu-id="1ed53-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1ed53-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="1ed53-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="1ed53-175">Restituisce un valore booleano che indica se l'espressione GeoJSON punto, poligono o LineString specificata è valida.</span><span class="sxs-lookup"><span data-stu-id="1ed53-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1ed53-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="1ed53-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="1ed53-177">Restituisce un valore JSON che contiene un valore booleano valore se l'espressione GeoJSON punto, poligono o LineString specificata è valida e, se non valida, anche il motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="1ed53-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="1ed53-178">Le funzioni spaziali possono essere utilizzate per eseguire query di prossimità rispetto ai dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="1ed53-179">Ad esempio, di seguito è riportata una query che restituisce tutti i documenti della famiglia entro 30 km della posizione specificata utilizzando la funzione predefinita ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="1ed53-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="1ed53-180">**Query**</span><span class="sxs-lookup"><span data-stu-id="1ed53-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="1ed53-181">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="1ed53-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="1ed53-182">Se si include l'indicizzazione spaziale nel criterio di indicizzazione, le "query distance" verranno servite in modo efficiente tramite l'indice.</span><span class="sxs-lookup"><span data-stu-id="1ed53-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="1ed53-183">Per altre informazioni sull'indicizzazione spaziale, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="1ed53-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="1ed53-184">Se non si dispone di un indice spaziale per i percorsi specificati, è comunque possibile eseguire query spaziali specificando `x-ms-documentdb-query-enable-scan` intestazione della richiesta con il valore impostato su "true".</span><span class="sxs-lookup"><span data-stu-id="1ed53-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="1ed53-185">In .NET, questa operazione può essere eseguita passando l’argomento facoltativo **FeedOptions** alle query con [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) impostato su true.</span><span class="sxs-lookup"><span data-stu-id="1ed53-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="1ed53-186">Usare ST_WITHIN per verificare se un punto si trova all'interno di un poligono.</span><span class="sxs-lookup"><span data-stu-id="1ed53-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="1ed53-187">I poligoni vengono comunemente usati per rappresentare limiti come codici postali, confini di stato o formazioni naturali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="1ed53-188">Ancora una volta, se si include l'indicizzazione spaziale nel criterio di indicizzazione, le query "within" verranno servite in modo efficiente tramite l'indice.</span><span class="sxs-lookup"><span data-stu-id="1ed53-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="1ed53-189">Gli argomenti Polygon in ST_WITHIN possono contenere solo un anello singolo, ad esempio i poligoni non devono contenere aree vuote.</span><span class="sxs-lookup"><span data-stu-id="1ed53-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="1ed53-190">**Query**</span><span class="sxs-lookup"><span data-stu-id="1ed53-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="1ed53-191">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="1ed53-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="1ed53-192">Come per il funzionamento di tipi non corrispondenti nella query di Azure Cosmos DB, se il valore di località specificato in un argomento è non corretto o non è valido, verrà restituito **undefined** e il documento valutato verrà omesso nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="1ed53-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="1ed53-193">Se la query non restituisce alcun risultato, eseguire ST_ISVALIDDETAILED per eseguire il debug del tipo spatail non valido.</span><span class="sxs-lookup"><span data-stu-id="1ed53-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="1ed53-194">Azure Cosmos DB supporta anche l'esecuzione di query inverse, ovvero è possibile indicizzare poligoni o linee in Azure Cosmos DB, quindi eseguire una query per le aree che contengono un punto specificato.</span><span class="sxs-lookup"><span data-stu-id="1ed53-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="1ed53-195">Questo modello viene comunemente usato nella logistica per identificare, ad esempio, quando un furgone entra o esce da un'area designata.</span><span class="sxs-lookup"><span data-stu-id="1ed53-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="1ed53-196">**Query**</span><span class="sxs-lookup"><span data-stu-id="1ed53-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="1ed53-197">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="1ed53-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="1ed53-198">ST_ISVALID e ST_ISVALIDDETAILED possono essere utilizzati per verificare la validità di un oggetto spaziale.</span><span class="sxs-lookup"><span data-stu-id="1ed53-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="1ed53-199">Ad esempio, la seguente query controlla la validità di un punto con un valore di latitudine fuori scala (-132,8).</span><span class="sxs-lookup"><span data-stu-id="1ed53-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="1ed53-200">ST_ISVALID restituisce solo un valore booleano e ST_ISVALIDDETAILED restituisce il valore booleano e una stringa contenente il motivo per cui è considerato non valido.</span><span class="sxs-lookup"><span data-stu-id="1ed53-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="1ed53-201">** Query **</span><span class="sxs-lookup"><span data-stu-id="1ed53-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="1ed53-202">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="1ed53-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="1ed53-203">Queste funzioni possono essere usate anche per convalidare i poligoni.</span><span class="sxs-lookup"><span data-stu-id="1ed53-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="1ed53-204">Ad esempio, qui viene usata la funzione ST_ISVALIDDETAILED per convalidare un poligono che non è chiuso.</span><span class="sxs-lookup"><span data-stu-id="1ed53-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="1ed53-205">**Query**</span><span class="sxs-lookup"><span data-stu-id="1ed53-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="1ed53-206">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="1ed53-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="1ed53-207">Query di LINQ in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1ed53-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="1ed53-208">Il .NET SDK di DocumentDB fornisce inoltre metodi stub `Distance()` e `Within()` per l'utilizzo all'interno di espressioni LINQ.</span><span class="sxs-lookup"><span data-stu-id="1ed53-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="1ed53-209">Il provider LINQ di DocumentDB converte le chiamate di questi metodi nelle chiamate della funzione predefinita di SQL equivalente (ST_DISTANCE e ST_WITHIN rispettivamente).</span><span class="sxs-lookup"><span data-stu-id="1ed53-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="1ed53-210">Di seguito è riportato un esempio di query LINQ che consente di trovare tutti i documenti nella raccolta di Azure Cosmos DB il cui valore "location" è entro un raggio di 30 km dal punto specificato con LINQ.</span><span class="sxs-lookup"><span data-stu-id="1ed53-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="1ed53-211">**Query LINQ per Distance**</span><span class="sxs-lookup"><span data-stu-id="1ed53-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="1ed53-212">Analogamente, di seguito è riportata una query per trovare tutti i documenti il cui valore "location" è all'interno della casella o del poligono specificato.</span><span class="sxs-lookup"><span data-stu-id="1ed53-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="1ed53-213">**Query LINQ per Within**</span><span class="sxs-lookup"><span data-stu-id="1ed53-213">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="1ed53-214">Dopo aver compreso come eseguire query sui documenti con LINQ e SQL, è ora possibile esaminare come configurare Azure Cosmos DB per l'indicizzazione spaziale.</span><span class="sxs-lookup"><span data-stu-id="1ed53-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="1ed53-215">Indicizzazione</span><span class="sxs-lookup"><span data-stu-id="1ed53-215">Indexing</span></span>
<span data-ttu-id="1ed53-216">Come illustrato nel documento [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) (Indicizzazione indipendente dallo schema con Azure DocumentDB), il motore del database Azure Cosmos DB è stato progettato per essere realmente indipendente dallo schema e fornire supporto avanzato per JSON.</span><span class="sxs-lookup"><span data-stu-id="1ed53-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="1ed53-217">Il motore di database ottimizzato per la scrittura di Azure Cosmos DB riconosce a livello nativo i dati spaziali (punti, poligoni e linee) rappresentati nello standard GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="1ed53-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="1ed53-218">In breve, la geometria è proiettata dalle coordinate geodetiche su un piano 2D, quindi suddivisa progressivamente in celle utilizzando un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="1ed53-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="1ed53-219">Queste celle vengono mappate in 1D in base alla posizione della cella all'interno di una **curva di riempimento dello spazio di Hilbert**, che consente di mantenere la posizione dei punti.</span><span class="sxs-lookup"><span data-stu-id="1ed53-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="1ed53-220">Quando i dati località vengono indicizzati, passano attraverso un processo noto come **mosaico**, vale a dire tutte le celle che intersecano una posizione vengono identificate e archiviate come chiavi nell'indice di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1ed53-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="1ed53-221">In fase di query, anche argomenti come punti e poligoni sono tassellati per estrarre gli intervalli degli ID delle celle pertinenti e quindi usati per recuperare dati dall'indice.</span><span class="sxs-lookup"><span data-stu-id="1ed53-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="1ed53-222">Se si specifica un criterio di indicizzazione che include un indice spaziale per /* (tutti i percorsi), tutti i punti trovati all'interno dell'insieme vengono indicizzati per query spaziali efficienti (ST_WITHIN e ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="1ed53-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="1ed53-223">Gli indici spaziali non hanno un valore di precisione e utilizzano sempre un valore di precisione predefinito.</span><span class="sxs-lookup"><span data-stu-id="1ed53-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed53-224">Azure Cosmos DB supporta l'indicizzazione automatica dei tipi di dati Point, Polygon e LineString.</span><span class="sxs-lookup"><span data-stu-id="1ed53-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="1ed53-225">Il seguente frammento JSON mostra un criterio di indicizzazione con indicizzazione spaziale abilitata, ossia indicizza qualsiasi punto GeoJSON trovato all'interno di documenti per le query spaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="1ed53-226">Se si modifica il criterio di indicizzazione tramite il portale di Azure, è possibile specificare il seguente JSON come criterio di indicizzazione per abilitare l’indicizzazione spaziale nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="1ed53-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="1ed53-227">**JSON criterio di indicizzazione della raccolta con Spatial abilitato per punti e poligoni**</span><span class="sxs-lookup"><span data-stu-id="1ed53-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="1ed53-228">Ecco un frammento di codice in .NET che illustra come creare una raccolta con indicizzazione spaziale attivata per tutti i percorsi contenenti punti.</span><span class="sxs-lookup"><span data-stu-id="1ed53-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="1ed53-229">**Creare una raccolta con indicizzazione spaziale**</span><span class="sxs-lookup"><span data-stu-id="1ed53-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="1ed53-230">Di seguito viene descritto come modificare una raccolta esistente per sfruttare i vantaggi dell'indicizzazione spaziale su tutti i punti archiviati all'interno di documenti.</span><span class="sxs-lookup"><span data-stu-id="1ed53-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="1ed53-231">**Modificare una raccolta esistente con l'indicizzazione spaziale**</span><span class="sxs-lookup"><span data-stu-id="1ed53-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="1ed53-232">Se il valore GeoJSON della posizione all'interno del documento è non corretto o non valido, non verrà indicizzato per le query spaziali.</span><span class="sxs-lookup"><span data-stu-id="1ed53-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="1ed53-233">È possibile convalidare valori della posizione utilizzando ST_ISVALID e ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="1ed53-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="1ed53-234">Se la definizione della raccolta include una chiave di partizione, non viene segnalato lo stato di avanzamento della trasformazione dell'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="1ed53-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1ed53-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ed53-235">Next steps</span></span>
<span data-ttu-id="1ed53-236">Ora che si è appreso come iniziare a usare il supporto geospaziale in Azure Cosmos DB, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1ed53-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="1ed53-237">Iniziare a codificare con gli [esempi di codice .NET geospaziale in GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="1ed53-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="1ed53-238">Usare le query geospaziali in [Query Playground di Azure Cosmos DB](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="1ed53-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="1ed53-239">Altre informazioni sulle [query di Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="1ed53-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="1ed53-240">Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="1ed53-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

