---
title: aaaWorking con i dati geospaziali in Azure Cosmos DB | Documenti Microsoft
description: Comprendere come toocreate, indice e query oggetti spaziali con Azure Cosmos DB e hello API DocumentDB.
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
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="c8931-103">Uso dei dati geospaziali e dei dati località GeoJSON in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8931-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="c8931-104">Questo articolo è una funzionalità di geospatial introduzione toohello in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c8931-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="c8931-105">Dopo aver letto questo, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="c8931-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="c8931-106">Come si archiviano i dati spaziali in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c8931-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="c8931-107">Come si eseguono query su dati geospaziali in Azure Cosmos DB in SQL e LINQ?</span><span class="sxs-lookup"><span data-stu-id="c8931-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="c8931-108">Come si abilita o disabilita l'indicizzazione spaziale in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c8931-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="c8931-109">Questo articolo illustra come toowork con i dati spaziali con hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c8931-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="c8931-110">Consultare il [progetto GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) per esempi di codice.</span><span class="sxs-lookup"><span data-stu-id="c8931-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="c8931-111">Data di introduzione toospatial</span><span class="sxs-lookup"><span data-stu-id="c8931-111">Introduction toospatial data</span></span>
<span data-ttu-id="c8931-112">I dati spaziali descrivono hello posizione e la forma degli oggetti nello spazio.</span><span class="sxs-lookup"><span data-stu-id="c8931-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="c8931-113">Nella maggior parte delle applicazioni, che corrispondono tooobjects della terra hello, vale a dire i dati geospaziali.</span><span class="sxs-lookup"><span data-stu-id="c8931-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="c8931-114">Dati spaziali possono essere utilizzati toorepresent hello percorso di una persona, un punto di interesse o limite hello di una città o un lago.</span><span class="sxs-lookup"><span data-stu-id="c8931-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="c8931-115">Casi di utilizzo comuni includono spesso query di prossimità, ad esempio, "trova tutti i negozi vicino alla mia posizione attuale".</span><span class="sxs-lookup"><span data-stu-id="c8931-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="c8931-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="c8931-116">GeoJSON</span></span>
<span data-ttu-id="c8931-117">Azure Cosmos DB supporta l'indicizzazione e le query di dati geospaziali punto rappresentato utilizzando hello [GeoJSON specifica](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="c8931-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="c8931-118">Le strutture di dati GeoJSON sono sempre oggetti JSON validi, quindi possono essere archiviate e sottoposte a query usando Azure Cosmos DB senza librerie o strumenti specializzati.</span><span class="sxs-lookup"><span data-stu-id="c8931-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="c8931-119">Hello Azure Cosmos DB SDK forniscono classi di helper e metodi che rendono facilmente toowork con dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="c8931-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="c8931-120">Punti, oggetti linestring e poligoni</span><span class="sxs-lookup"><span data-stu-id="c8931-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="c8931-121">Un **punto** indica una posizione singola nello spazio.</span><span class="sxs-lookup"><span data-stu-id="c8931-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="c8931-122">Nei dati geospaziali, un punto rappresenta la posizione esatta di hello che può essere un indirizzo di un negozio di alimentari, continua, un'automobile o una città.</span><span class="sxs-lookup"><span data-stu-id="c8931-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="c8931-123">Un punto viene rappresentato in GeoJSON (e Azure Cosmos DB) tramite la sua coppia di coordinate o longitudine e latitudine.</span><span class="sxs-lookup"><span data-stu-id="c8931-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="c8931-124">Di seguito è riportato un esempio JSON per un punto.</span><span class="sxs-lookup"><span data-stu-id="c8931-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="c8931-125">**Punti in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c8931-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="c8931-126">Hello specifica GeoJSON specifica longitudine prima e la latitudine secondo.</span><span class="sxs-lookup"><span data-stu-id="c8931-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="c8931-127">Come in altre applicazioni di mapping, longitudine e latitudine sono angoli e sono espresse in gradi.</span><span class="sxs-lookup"><span data-stu-id="c8931-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="c8931-128">I valori di longitudine vengono misurati dal primo meridiano hello e sono compresi tra -180 e 180.0 gradi e latitudine vengono misurati dall'equatore hello di valori e sono compresi tra-90.0 e 90.0 gradi.</span><span class="sxs-lookup"><span data-stu-id="c8931-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="c8931-129">Azure DB Cosmos interpreta le coordinate come indicato al sistema di riferimento WGS 84 hello.</span><span class="sxs-lookup"><span data-stu-id="c8931-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="c8931-130">Per ulteriori informazioni sui sistemi di coordinate di riferimento, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="c8931-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="c8931-131">I punti possono essere incorporati in un documento di Azure Cosmos DB come illustrato in questo esempio di profilo utente contenente dati di località:</span><span class="sxs-lookup"><span data-stu-id="c8931-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="c8931-132">**Usare un profilo con località archiviata in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="c8931-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="c8931-133">Toopoints, GeoJSON inoltre supporta anche istanze linestring e poligoni.</span><span class="sxs-lookup"><span data-stu-id="c8931-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="c8931-134">**Oggetti linestring** rappresentano una serie di due o più punti nello spazio e hello segmenti lineari che li connettono.</span><span class="sxs-lookup"><span data-stu-id="c8931-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="c8931-135">In dati geospaziali, linestring sono comunemente usate toorepresent autostrade o fiumi.</span><span class="sxs-lookup"><span data-stu-id="c8931-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="c8931-136">Un oggetto **poligono** è un perimetro costituito da punti connessi che forma un elemento LineString chiuso.</span><span class="sxs-lookup"><span data-stu-id="c8931-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="c8931-137">Poligoni sono comunemente usate toorepresent formazioni naturali come laghi o politici giurisdizioni come città e province.</span><span class="sxs-lookup"><span data-stu-id="c8931-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="c8931-138">Di seguito è riportato un esempio di poligono in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8931-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="c8931-139">**Poligoni in GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="c8931-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="c8931-140">Hello GeoJSON specifica richiede che per i poligoni validi, hello ultima coppia di coordinate specificato deve essere uguale hello come hello innanzitutto toocreate una forma chiusa.</span><span class="sxs-lookup"><span data-stu-id="c8931-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="c8931-141">I punti all'interno di un poligono devono essere specificati in senso antiorario.</span><span class="sxs-lookup"><span data-stu-id="c8931-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="c8931-142">Un poligono specificato nell'ordine in senso orario rappresenta inverso hello dell'area di hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="c8931-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="c8931-143">In aggiunta tooPoint, LineString e poligono, GeoJSON specifica inoltre la rappresentazione di hello come toogroup più posizioni geospaziale, e come le proprietà arbitrarie tooassociate con geolocation come un **funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="c8931-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="c8931-144">Trattandosi di oggetti JSON validi, essi possono essere archiviati ed elaborati tutti in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8931-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="c8931-145">Azure Cosmos DB supporta tuttavia solo l'indicizzazione automatica dei punti.</span><span class="sxs-lookup"><span data-stu-id="c8931-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="c8931-146">Sistemi di riferimento delle coordinate</span><span class="sxs-lookup"><span data-stu-id="c8931-146">Coordinate reference systems</span></span>
<span data-ttu-id="c8931-147">Poiché la forma hello della terra hello è irregolare, le coordinate di dati geospaziali è rappresentato in molti sistemi di coordinate di riferimento (CR), ciascuno con i relativi frame di riferimento e le unità di misura.</span><span class="sxs-lookup"><span data-stu-id="c8931-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="c8931-148">Ad esempio, "National griglia di Gran Bretagna" hello è un sistema di riferimento è molto accurato per hello Regno Unito, ma non al suo esterno.</span><span class="sxs-lookup"><span data-stu-id="c8931-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="c8931-149">Hello CRS più diffusi in uso oggi è hello sistema World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="c8931-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="c8931-150">Dispositivi GPS e molti servizi di mapping, tra cui Google Maps e le API di Bing Maps, utilizzano WGS-84.</span><span class="sxs-lookup"><span data-stu-id="c8931-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="c8931-151">Azure Cosmos DB supporta l'indicizzazione e le query di dati geospaziali tramite hello CRS WGS 84.</span><span class="sxs-lookup"><span data-stu-id="c8931-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="c8931-152">Creazione di documenti con dati spaziali</span><span class="sxs-lookup"><span data-stu-id="c8931-152">Creating documents with spatial data</span></span>
<span data-ttu-id="c8931-153">Quando si creano i documenti che contengono valori GeoJSON, vengono indicizzati automaticamente con un indice spaziale in Criteri di indicizzazione toohello base della raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="c8931-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="c8931-154">Se si usa un SDK di Azure Cosmos DB in un linguaggio tipizzato in modo dinamico come Python o Node.js, è necessario creare un GeoJSON valido.</span><span class="sxs-lookup"><span data-stu-id="c8931-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="c8931-155">**Creare documenti con i dati geospaziali in Node.js**</span><span class="sxs-lookup"><span data-stu-id="c8931-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

<span data-ttu-id="c8931-156">Se si lavora con hello APIs DocumentDB, è possibile utilizzare hello `Point` e `Polygon` classi all'interno di hello `Microsoft.Azure.Documents.Spatial` informazioni sul percorso di spazio dei nomi tooembed all'interno di oggetti di applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8931-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="c8931-157">Queste classi consentono di semplificare hello serializzazione e deserializzazione dei dati spaziali in GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="c8931-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="c8931-158">**Creare documenti con i dati geospaziali in .NET**</span><span class="sxs-lookup"><span data-stu-id="c8931-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="c8931-159">Se si dispongano di informazioni di latitudine e longitudine hello, ma dispone di indirizzi fisici hello o nome di percorso, ad esempio città o paese, è possibile cercare le coordinate effettivo hello tramite un servizio di geocodifica come servizi REST di Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="c8931-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="c8931-160">Ulteriori informazioni sulla geocodifica di Bing Maps sono disponibili [qui](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8931-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="c8931-161">Query sui tipi spaziali</span><span class="sxs-lookup"><span data-stu-id="c8931-161">Querying spatial types</span></span>
<span data-ttu-id="c8931-162">Ora che sono state utilizzate come esaminare i dati geospaziali tooinsert, esaminiamo come tooquery tali dati con database di Cosmos Azure usando SQL e LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8931-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="c8931-163">Funzioni predefinite spaziali di SQL</span><span class="sxs-lookup"><span data-stu-id="c8931-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="c8931-164">DB Cosmos Azure supporta hello seguendo le funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziale.</span><span class="sxs-lookup"><span data-stu-id="c8931-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="c8931-165">Per ulteriori informazioni sul set completo di hello delle funzioni predefinite in hello linguaggio SQL, consultare troppo[Query Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="c8931-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="c8931-166"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="c8931-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="c8931-167"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="c8931-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8931-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8931-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8931-169">Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="c8931-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8931-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8931-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8931-171">Restituisce un'espressione booleana che indica se hello prima GeoJSON oggetto (punto, poligono o LineString) all'interno di hello secondo GeoJSON oggetto (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="c8931-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8931-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c8931-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c8931-173">Restituisce un'espressione booleana che indica se si intersecano hello due GeoJSON oggetti specificati (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="c8931-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8931-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="c8931-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="c8931-175">Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.</span><span class="sxs-lookup"><span data-stu-id="c8931-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c8931-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="c8931-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="c8931-177">Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="c8931-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="c8931-178">Le funzioni spaziali possono essere utilizzati tooperform prossimità query sui dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="c8931-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="c8931-179">Ad esempio, ecco una query che restituisce che tutti i prodotti della famiglia di documenti che è all'interno di 30 km di hello posizione specificata usando hello ST_DISTANCE funzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c8931-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="c8931-180">**Query**</span><span class="sxs-lookup"><span data-stu-id="c8931-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="c8931-181">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="c8931-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="c8931-182">Se si include l'indicizzazione spaziale nei criteri di indicizzazione, quindi "query di distanza" verrà utilizzata in modo efficiente tramite indice hello.</span><span class="sxs-lookup"><span data-stu-id="c8931-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="c8931-183">Per ulteriori informazioni sugli indici spaziali, vedere sezione hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="c8931-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="c8931-184">Se non è un indice per hello percorsi specificati, è comunque possibile eseguire le query spaziali specificando `x-ms-documentdb-query-enable-scan` impostare l'intestazione di richiesta con valore hello troppo "true".</span><span class="sxs-lookup"><span data-stu-id="c8931-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="c8931-185">In .NET, questo scopo è possibile passare hello facoltativo **FeedOptions** tooqueries argomento con [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) impostare tootrue.</span><span class="sxs-lookup"><span data-stu-id="c8931-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="c8931-186">ST_WITHIN può essere utilizzato toocheck se si trova un punto all'interno di un poligono.</span><span class="sxs-lookup"><span data-stu-id="c8931-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="c8931-187">Poligoni sono, in genere limiti toorepresent usato come formazioni naturale, i limiti di stato o i codici postali zip.</span><span class="sxs-lookup"><span data-stu-id="c8931-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="c8931-188">Nuovo se si include l'indicizzazione spaziale nei criteri di indicizzazione, quindi "all'interno di" query verrà utilizzata in modo efficiente tramite indice hello.</span><span class="sxs-lookup"><span data-stu-id="c8931-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="c8931-189">Argomenti poligono ST_WITHIN possono contenere solo un anello singolo, ad esempio hello poligoni non deve contenere fori in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="c8931-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="c8931-190">**Query**</span><span class="sxs-lookup"><span data-stu-id="c8931-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="c8931-191">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="c8931-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="c8931-192">Tipi simili di mancata corrispondenza toohow funziona in Azure Cosmos DB query, se hello percorso specificato l'argomento non è corretto o non valido, quindi viene valutata troppo**definito** e toobe documento hello valutata ignorati da hello risultati della query.</span><span class="sxs-lookup"><span data-stu-id="c8931-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="c8931-193">Se la query non restituisce alcun risultato, eseguire toodebug ST_ISVALIDDETAILED perché hello spatail tipo non è valido.</span><span class="sxs-lookup"><span data-stu-id="c8931-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="c8931-194">DB Cosmos Azure supporta inoltre l'esecuzione di query inversa, ad esempio, è possibile indicizzare poligoni o righe nel database di Azure Cosmos, quindi eseguire una query per le aree di hello che contengono un punto specificato.</span><span class="sxs-lookup"><span data-stu-id="c8931-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="c8931-195">Questo modello viene comunemente usato in logistica tooidentify ad esempio, quando un autocarro entra o esce da un'area designata.</span><span class="sxs-lookup"><span data-stu-id="c8931-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="c8931-196">**Query**</span><span class="sxs-lookup"><span data-stu-id="c8931-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="c8931-197">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="c8931-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="c8931-198">ST_ISVALID e ST_ISVALIDDETAILED possono essere utilizzati toocheck se un oggetto spaziale è valido.</span><span class="sxs-lookup"><span data-stu-id="c8931-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="c8931-199">Ad esempio, hello seguente query controlla la validità di hello di un punto con un timeout del valore di latitudine intervallo (-132.8).</span><span class="sxs-lookup"><span data-stu-id="c8931-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="c8931-200">ST_ISVALID restituisce solo un valore booleano, e restituisce ST_ISVALIDDETAILED hello booleani e una stringa che contiene il motivo di hello perché è considerato non valido.</span><span class="sxs-lookup"><span data-stu-id="c8931-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="c8931-201">** Query **</span><span class="sxs-lookup"><span data-stu-id="c8931-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="c8931-202">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="c8931-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="c8931-203">Queste funzioni possono essere utilizzati toovalidate poligoni.</span><span class="sxs-lookup"><span data-stu-id="c8931-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="c8931-204">Ad esempio, qui utilizziamo ST_ISVALIDDETAILED toovalidate un poligono che non è stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="c8931-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="c8931-205">**Query**</span><span class="sxs-lookup"><span data-stu-id="c8931-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="c8931-206">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="c8931-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="c8931-207">Esecuzione di query LINQ in hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c8931-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="c8931-208">Hello, DocumentDB .NET SDK anche provider stub metodi `Distance()` e `Within()` per l'utilizzo all'interno di espressioni LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8931-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="c8931-209">provider LINQ DocumentDB Hello converte queste metodo chiama toohello equivalente SQL chiamate alle funzioni predefinite (ST_DISTANCE e ST_WITHIN rispettivamente).</span><span class="sxs-lookup"><span data-stu-id="c8931-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="c8931-210">Ecco un esempio di una query LINQ che consente di trovare tutti i documenti nella raccolta di Azure Cosmos DB hello è il cui valore di "location" entro un raggio di 30km di hello specificato punto utilizzando LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8931-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="c8931-211">**Query LINQ per Distance**</span><span class="sxs-lookup"><span data-stu-id="c8931-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="c8931-212">Analogamente, ecco una query per trovare tutti i documenti hello cui "location" è all'interno di hello specificato casella/poligono.</span><span class="sxs-lookup"><span data-stu-id="c8931-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="c8931-213">**Query LINQ per Within**</span><span class="sxs-lookup"><span data-stu-id="c8931-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="c8931-214">Ora che sono state utilizzate descritto tooquery documenti utilizzando LINQ e SQL, esaminiamo come tooconfigure DB Cosmos Azure per l'indicizzazione spaziale.</span><span class="sxs-lookup"><span data-stu-id="c8931-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="c8931-215">Indicizzazione</span><span class="sxs-lookup"><span data-stu-id="c8931-215">Indexing</span></span>
<span data-ttu-id="c8931-216">Come descritto in hello [Schema indipendente dall'indicizzazione con Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) carta, sono state progettate toobe motore di database del database di Azure Cosmos realmente indipendente di schema e forniscono un supporto eccellente per JSON.</span><span class="sxs-lookup"><span data-stu-id="c8931-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="c8931-217">motore di database con ottimizzazione per la scrittura di Hello di Azure Cosmos DB a livello nativo riconosce i dati spaziali (punta, poligoni e linee) rappresentati nello standard GeoJSON hello.</span><span class="sxs-lookup"><span data-stu-id="c8931-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="c8931-218">In breve, geometry hello viene proiettato da coordinate geodetico su un piano 2D quindi suddiviso progressivamente in celle utilizzando un **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="c8931-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="c8931-219">Queste celle vengono mappate too1D in base alla posizione di hello della cella hello all'interno di un **curva di riempimento dello spazio di Hilbert**, che consente di mantenere la località di punti.</span><span class="sxs-lookup"><span data-stu-id="c8931-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="c8931-220">Inoltre quando i dati sulla località sono indicizzati, passano attraverso un processo noto come **a mosaico**, vale a dire tutte hello le celle che intersecano una posizione vengono identificate e archiviate come chiavi di indice di hello Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8931-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="c8931-221">In fase di query argomenti quali punti e poligoni sono anche tooextract mosaico hello degli intervalli di ID cella appropriata, quindi tooretrieve dati dall'indice hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="c8931-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="c8931-222">Se si specifica un criterio di indicizzazione che include un indice spaziale per / * (tutti i percorsi), quindi vengono indicizzati tutti i punti di presente all'interno di raccolta hello per le query spaziali efficiente (ST_WITHIN e ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="c8931-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="c8931-223">Gli indici spaziali non hanno un valore di precisione e utilizzano sempre un valore di precisione predefinito.</span><span class="sxs-lookup"><span data-stu-id="c8931-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="c8931-224">Azure Cosmos DB supporta l'indicizzazione automatica dei tipi di dati Point, Polygon e LineString.</span><span class="sxs-lookup"><span data-stu-id="c8931-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="c8931-225">Hello frammento di codice JSON seguente mostra un criterio di indicizzazione con abilitata l'indicizzazione spaziale, vale a dire qualsiasi punto GeoJSON trovato all'interno dei documenti per le query spaziali di indice.</span><span class="sxs-lookup"><span data-stu-id="c8931-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="c8931-226">Se si modifica hello hello portale di Azure tramite criteri di indicizzazione, è possibile specificare hello seguente JSON per l'indicizzazione tooenable criteri spaziali l'indicizzazione nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="c8931-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="c8931-227">**JSON criterio di indicizzazione della raccolta con Spatial abilitato per punti e poligoni**</span><span class="sxs-lookup"><span data-stu-id="c8931-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="c8931-228">Di seguito è un frammento di codice in .NET che illustra come una raccolta con l'indicizzazione spaziale toocreate attivata per tutti i percorsi contenenti punti.</span><span class="sxs-lookup"><span data-stu-id="c8931-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="c8931-229">**Creare una raccolta con indicizzazione spaziale**</span><span class="sxs-lookup"><span data-stu-id="c8931-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="c8931-230">Di seguito è illustrato come modificare un vantaggio di tootake raccolta esistente di indicizzazione spaziale su tutti i punti che vengono archiviati all'interno dei documenti.</span><span class="sxs-lookup"><span data-stu-id="c8931-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="c8931-231">**Modificare una raccolta esistente con l'indicizzazione spaziale**</span><span class="sxs-lookup"><span data-stu-id="c8931-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="c8931-232">Se il percorso di hello GeoJSON valore all'interno di documento hello è in formato non valido o non valido, quindi non ottenere indicizzata per le query spaziali.</span><span class="sxs-lookup"><span data-stu-id="c8931-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="c8931-233">È possibile convalidare valori della posizione utilizzando ST_ISVALID e ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="c8931-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="c8931-234">Se la definizione della raccolta include una chiave di partizione, non viene segnalato lo stato di avanzamento della trasformazione dell'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="c8931-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c8931-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8931-235">Next steps</span></span>
<span data-ttu-id="c8931-236">Ora che è stata apprese sull'avvio tooget con supporto geospaziali in Azure Cosmos DB, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c8931-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="c8931-237">Avviare la codifica con hello [esempi di codice Geospatial .NET su GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="c8931-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="c8931-238">Ottenere mani nei con geospatial query in hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="c8931-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="c8931-239">Altre informazioni sulle [query di Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="c8931-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="c8931-240">Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="c8931-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

