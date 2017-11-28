---
title: aaaUse ScaleR e SparkR con Azure HDInsight | Documenti Microsoft
description: Usare ScaleR e SparkR con R Server e HDInsight
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="069fb-103">Uso combinato di ScaleR e SparkR in HDInsight</span><span class="sxs-lookup"><span data-stu-id="069fb-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="069fb-104">Questo articolo illustra come toopredict volo ritardi di arrivo utilizzando un **ScaleR** aggiunti a un modello di regressione logistica da dati sui ritardi dei voli e weather con **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="069fb-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="069fb-105">Questo scenario illustra le funzionalità di hello di ridimensionamento per la manipolazione dei dati in Spark utilizzato con Microsoft R Server per analitica.</span><span class="sxs-lookup"><span data-stu-id="069fb-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="069fb-106">combinazione di Hello di queste tecnologie consente tooapply funzionalità più recenti di hello in elaborazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="069fb-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="069fb-107">Sebbene vengano eseguiti nel motore di esecuzione di Hadoop Spark, entrambi i pacchetti sono bloccati da una condivisione dei dati in memoria in quanto ognuno di essi richiede le rispettive sessioni Spark.</span><span class="sxs-lookup"><span data-stu-id="069fb-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="069fb-108">Finché il problema viene risolto in una versione futura di R Server, la soluzione alternativa hello è toomaintain non sovrapposti Spark sessioni e dati tooexchange tramite i file intermedi.</span><span class="sxs-lookup"><span data-stu-id="069fb-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="069fb-109">Hello istruzioni di seguito viene illustrato che questi requisiti sono tooachieve semplice.</span><span class="sxs-lookup"><span data-stu-id="069fb-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="069fb-110">Utilizziamo un esempio di seguito inizialmente condiviso in una conversazione in strati 2016 Mario Inchiosa e Roni Burd che è anche disponibile tramite hello webinar [la creazione di una piattaforma di analisi scientifica dei dati scalabile con R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). esempio hello Usa SparkR toojoin hello compagnie aeree noto set ritardo di arrivo dati con dati meteorologici negli aeroporti di partenza e arrivo.</span><span class="sxs-lookup"><span data-stu-id="069fb-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="069fb-111">dati di Hello unita in join vengono quindi utilizzati come modello di regressione logistica ScaleR tooa input per stimare il ritardo di arrivo dell'utilità.</span><span class="sxs-lookup"><span data-stu-id="069fb-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="069fb-112">Hello simulazione di codice è stato inizialmente scritto per il Server di R in Spark in un cluster HDInsight in Azure.</span><span class="sxs-lookup"><span data-stu-id="069fb-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="069fb-113">Il concetto di hello di combinazione di utilizzo di hello di SparkR e ScaleR in uno script è valido nel contesto di hello degli ambienti locali.</span><span class="sxs-lookup"><span data-stu-id="069fb-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="069fb-114">In seguito hello, si presume un livello intermedio di conoscenza di R e R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) libreria di R Server.</span><span class="sxs-lookup"><span data-stu-id="069fb-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="069fb-115">Durante l'analisi di questo scenario si introdurrà anche l'uso di [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html).</span><span class="sxs-lookup"><span data-stu-id="069fb-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="069fb-116">set di dati Hello airline e previsioni del tempo</span><span class="sxs-lookup"><span data-stu-id="069fb-116">hello airline and weather datasets</span></span>

<span data-ttu-id="069fb-117">Hello **AirOnTime08to12CSV** set di dati pubblico di compagnie aeree contiene informazioni su volo in arrivo e i dettagli di partenza per tutti i voli commerciali all'interno di hello negli Stati Uniti, da tooDecember 1987 ottobre 2012.</span><span class="sxs-lookup"><span data-stu-id="069fb-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="069fb-118">Si tratta di un set di dati di grandi dimensioni con quasi 150 milioni di record totali,</span><span class="sxs-lookup"><span data-stu-id="069fb-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="069fb-119">che occupa poco meno di 4 GB dopo la decompressione.</span><span class="sxs-lookup"><span data-stu-id="069fb-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="069fb-120">È disponibile da hello [US government archivi](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span><span class="sxs-lookup"><span data-stu-id="069fb-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="069fb-121">In modo più semplice, è disponibile come file zip (AirOnTimeCSV.zip) contenente un set di 303 file CSV mensili separati da hello [repository dataset Revolution Analitica](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="069fb-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="069fb-122">effetti hello toosee di meteo sui ritardi dei voli, è necessario anche dati meteorologici hello in ognuno degli aeroporti hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="069fb-123">Questi dati possono essere scaricati come file zip in formato non elaborato, in base al mese, da hello [repository National pesce e amministrazione senso](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="069fb-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="069fb-124">Ai fini di hello di questo esempio, si estraggono i dati meteo da maggio 2007 – dicembre 2012 e utilizzati file di dati all'interno di ogni zips mensile 68 hello oraria hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="069fb-125">file zip mensile Hello anche contengono il mapping (YYYYMMstation.txt) tra hello weather stazione ID (WBAN), che è associata a (indicativo di chiamata), in aeroporto hello e hello fuso dell'aeroporto orario dall'ora UTC (fuso orario).</span><span class="sxs-lookup"><span data-stu-id="069fb-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="069fb-126">Tutte queste informazioni è necessario quando si uniscono dati hello airline ritardo e previsioni del tempo.</span><span class="sxs-lookup"><span data-stu-id="069fb-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="069fb-127">Impostazione di ambiente Spark hello</span><span class="sxs-lookup"><span data-stu-id="069fb-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="069fb-128">primo passaggio Hello è tooset ambiente Spark hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="069fb-129">Iniziamo toohello directory che contiene la directory di dati di input, la creazione di un contesto di calcolo Spark e creazione di una funzione di registrazione per la registrazione informativo toohello console:</span><span class="sxs-lookup"><span data-stu-id="069fb-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="069fb-130">Successivamente è aggiungere "Spark_Home" toohello di percorso di ricerca per i pacchetti R in modo che è possibile utilizzare SparkR e inizializzare una sessione SparkR:</span><span class="sxs-lookup"><span data-stu-id="069fb-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="069fb-131">Preparazione dei dati meteo hello</span><span class="sxs-lookup"><span data-stu-id="069fb-131">Preparing hello weather data</span></span>

<span data-ttu-id="069fb-132">dati meteo tooprepare hello è subset è colonne toohello necessarie per la modellazione:</span><span class="sxs-lookup"><span data-stu-id="069fb-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="069fb-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="069fb-133">"Visibility"</span></span>
- <span data-ttu-id="069fb-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="069fb-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="069fb-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="069fb-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="069fb-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="069fb-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="069fb-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="069fb-137">"WindSpeed"</span></span>
- <span data-ttu-id="069fb-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="069fb-138">"Altimeter"</span></span>

<span data-ttu-id="069fb-139">È quindi aggiungere un codice di aeroporto associato alla stazione meteo hello e convertire le misure di hello da tooUTC ora locale.</span><span class="sxs-lookup"><span data-stu-id="069fb-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="069fb-140">Iniziamo con la creazione di un codice del file di toomap hello stazione meteo (WBAN) info tooan aeroporto.</span><span class="sxs-lookup"><span data-stu-id="069fb-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="069fb-141">È stato possibile ottenere questa correlazione dal file di mapping hello incluso con i dati meteorologici hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="069fb-142">Da hello mapping *indicativo di chiamata* (ad esempio, LAX) campo nel file di dati meteo hello troppo*origine* nei dati airline hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="069fb-143">Tuttavia, ecco toohave un altro mapping d' parte che esegue il mapping *WBAN* troppo*AirportID* (ad esempio, 12892 per LAX) e include *fuso orario* che è stato salvato tooa File CSV denominato "wban-a-aeroporto-id-fuso orario. CSV"che è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="069fb-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="069fb-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="069fb-144">For example:</span></span>

| <span data-ttu-id="069fb-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="069fb-145">AirportID</span></span> | <span data-ttu-id="069fb-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="069fb-146">WBAN</span></span> | <span data-ttu-id="069fb-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="069fb-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="069fb-148">10685</span><span class="sxs-lookup"><span data-stu-id="069fb-148">10685</span></span> | <span data-ttu-id="069fb-149">54831</span><span class="sxs-lookup"><span data-stu-id="069fb-149">54831</span></span> | <span data-ttu-id="069fb-150">-6</span><span class="sxs-lookup"><span data-stu-id="069fb-150">-6</span></span>
| <span data-ttu-id="069fb-151">14871</span><span class="sxs-lookup"><span data-stu-id="069fb-151">14871</span></span> | <span data-ttu-id="069fb-152">24232</span><span class="sxs-lookup"><span data-stu-id="069fb-152">24232</span></span> | <span data-ttu-id="069fb-153">-8</span><span class="sxs-lookup"><span data-stu-id="069fb-153">-8</span></span>
| <span data-ttu-id="069fb-154">..</span><span class="sxs-lookup"><span data-stu-id="069fb-154">..</span></span> | <span data-ttu-id="069fb-155">..</span><span class="sxs-lookup"><span data-stu-id="069fb-155">..</span></span> | <span data-ttu-id="069fb-156">..</span><span class="sxs-lookup"><span data-stu-id="069fb-156">..</span></span>

<span data-ttu-id="069fb-157">file Hello seguente codice legge ogni dei dati non elaborati weather oraria hello, le colonne di toohello subset è necessaria, unisce i file di mapping stazione meteo hello, regola hello orari data tooUTC misurazioni e quindi scrive una nuova versione del file hello:</span><span class="sxs-lookup"><span data-stu-id="069fb-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="069fb-158">L'importazione di hello airline e previsioni del tempo dati tooSpark frame di dati</span><span class="sxs-lookup"><span data-stu-id="069fb-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="069fb-159">Ora è usare hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) funzione hello tooimport meteo e airline tooSpark dati frame di dati.</span><span class="sxs-lookup"><span data-stu-id="069fb-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="069fb-160">Questa funzione, come molti altri metodi Spark, viene eseguita in modo differito, vale a dire che viene accodata per l'esecuzione, ma eseguita solo quando è necessario.</span><span class="sxs-lookup"><span data-stu-id="069fb-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="069fb-161">Pulizia e trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="069fb-161">Data cleansing and transformation</span></span>

<span data-ttu-id="069fb-162">Successivamente, viene eseguito una certa pulitura dati airline hello è stato importato toorename colonne.</span><span class="sxs-lookup"><span data-stu-id="069fb-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="069fb-163">È solo variabili hello necessite e arrotondare volte partenza pianificato verso il basso toohello più vicino tooenable ora l'unione di dati più recenti weather hello in partenza:</span><span class="sxs-lookup"><span data-stu-id="069fb-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="069fb-164">È ora possibile eseguire operazioni simili su dati meteorologici hello:</span><span class="sxs-lookup"><span data-stu-id="069fb-164">Now we perform similar operations on hello weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="069fb-165">Unione di dati meteo e airline hello</span><span class="sxs-lookup"><span data-stu-id="069fb-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="069fb-166">È possibile utilizzare hello SparkR [join](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) funzione toodo un left outer join di dati airline e previsioni del tempo di hello da partenza AirportID e datetime.</span><span class="sxs-lookup"><span data-stu-id="069fb-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="069fb-167">outer join di Hello consente tooretain tutti i dati di airline hello registra anche se non sono presenti dati meteo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="069fb-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="069fb-168">Join hello, è rimuovere alcune colonne ridondanti e la ridenominazione hello mantenuto tooremove hello in arrivo frame di dati prefisso introdotto da join hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="069fb-169">In questo modo, si aggiungere dati meteo e airline hello in arrivo AirportID e datetime basati:</span><span class="sxs-lookup"><span data-stu-id="069fb-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="069fb-170">Salvare i risultati tooCSV per lo scambio con ScaleR</span><span class="sxs-lookup"><span data-stu-id="069fb-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="069fb-171">È stata completata join hello dobbiamo toodo con SparkR.</span><span class="sxs-lookup"><span data-stu-id="069fb-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="069fb-172">Si salvare i dati di hello di hello finale frame di dati di Spark "joinedDF5" tooa CSV per tooScaleR input e quindi chiudere timeout sessione SparkR hello.</span><span class="sxs-lookup"><span data-stu-id="069fb-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="069fb-173">È possibile indicare in modo esplicito SparkR toosave hello CSV risultante nel parallelismo di sufficienti tooenable 80 partizioni distinte nell'elaborazione ScaleR:</span><span class="sxs-lookup"><span data-stu-id="069fb-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="069fb-174">Importare tooXDF per l'utilizzo da ScaleR</span><span class="sxs-lookup"><span data-stu-id="069fb-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="069fb-175">È possibile usare file CSV hello di airline unita in join e di dati meteo-è per la modellazione tramite un'origine dati di testo ScaleR.</span><span class="sxs-lookup"><span data-stu-id="069fb-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="069fb-176">Ma è importarlo tooXDF in primo luogo, in quanto è più efficiente quando si esegue più operazioni sui set di dati hello:</span><span class="sxs-lookup"><span data-stu-id="069fb-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="069fb-177">Suddivisione dei dati per il training e il test</span><span class="sxs-lookup"><span data-stu-id="069fb-177">Splitting data for training and test</span></span>

<span data-ttu-id="069fb-178">È utilizzare toosplit rxDataStep dati 2012 hello per il test e mantenere rest hello per il training:</span><span class="sxs-lookup"><span data-stu-id="069fb-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="069fb-179">Eseguire il training e il test di un modello di regressione logistica</span><span class="sxs-lookup"><span data-stu-id="069fb-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="069fb-180">Ora siamo toobuild pronto un modello.</span><span class="sxs-lookup"><span data-stu-id="069fb-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="069fb-181">influenza hello toosee di dati meteo sulla ritardo nell'ora di arrivo hello, utilizziamo routine di regressione logistica del ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="069fb-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="069fb-182">Usato da toomodel se un ritardo di arrivo di maggiore di 15 minuti è influenzato dalle weather hello negli aeroporti di partenza e arrivo hello:</span><span class="sxs-lookup"><span data-stu-id="069fb-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="069fb-183">Ora vediamo come su hello dati di test da eseguire alcune stime e analisi ROC e AUC.</span><span class="sxs-lookup"><span data-stu-id="069fb-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="069fb-184">Assegnazione di punteggi in un'altra posizione</span><span class="sxs-lookup"><span data-stu-id="069fb-184">Scoring elsewhere</span></span>

<span data-ttu-id="069fb-185">È anche possibile usare modello hello per i dati di punteggio in un'altra piattaforma.</span><span class="sxs-lookup"><span data-stu-id="069fb-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="069fb-186">Salvataggio di file RDS tooan e il trasferimento e l'importazione di servizi desktop remoto in una destinazione di assegnazione dei punteggi di ambiente, ad esempio SQL Server R Services.</span><span class="sxs-lookup"><span data-stu-id="069fb-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="069fb-187">È importante tooensure che livelli di fattore hello di hello toobe di dati con punteggio corrispondono a quelle in cui hello modello è stato compilato.</span><span class="sxs-lookup"><span data-stu-id="069fb-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="069fb-188">Che corrispondenza può essere ottenuta tramite l'estrazione e il salvataggio delle informazioni di colonna hello associato hello modellazione dei dati tramite del ScaleR `rxCreateColInfo()` funzione e quindi l'applicazione di origine di dati di input toohello informazioni tale colonna per la stima.</span><span class="sxs-lookup"><span data-stu-id="069fb-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="069fb-189">Nell'esempio hello è salvare alcune righe del set di dati test hello ed estrarre e utilizzare le informazioni sulla colonna hello da questo esempio nello script di stima hello:</span><span class="sxs-lookup"><span data-stu-id="069fb-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="069fb-190">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="069fb-190">Summary</span></span>

<span data-ttu-id="069fb-191">In questo articolo è stato illustrato come sia possibile toocombine ricorso SparkR per manipolare i dati con ScaleR per lo sviluppo di modelli di Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="069fb-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="069fb-192">In questo scenario è necessario gestire sessioni di Spark separate eseguendo una sola sessione alla volta e scambiando i dati tramite file CSV.</span><span class="sxs-lookup"><span data-stu-id="069fb-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="069fb-193">Anche se semplice, questo processo sarà ancora più semplice nella prossima versione di R Server in cui SparkR e ScaleR potranno condividere una sessione di Spark e pertanto i relativi DataFrame.</span><span class="sxs-lookup"><span data-stu-id="069fb-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="069fb-194">Passaggi successivi e altre informazioni</span><span class="sxs-lookup"><span data-stu-id="069fb-194">Next steps and more information</span></span>

- <span data-ttu-id="069fb-195">Per ulteriori informazioni sull'utilizzo del Server di R in Spark, vedere hello [Introduzione alla Guida in MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="069fb-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="069fb-196">Per informazioni generali su R Server, vedere hello [Guida introduttiva di R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) articolo.</span><span class="sxs-lookup"><span data-stu-id="069fb-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="069fb-197">Per informazioni su R Server in HDInsight, vedere [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) (Panoramica di R Server in Azure HDInsight) e [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md) (R Server in Azure HDInsight).</span><span class="sxs-lookup"><span data-stu-id="069fb-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="069fb-198">Per altre informazioni sull'uso di SparkR, vedere:</span><span class="sxs-lookup"><span data-stu-id="069fb-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="069fb-199">Documento Apache SparkR</span><span class="sxs-lookup"><span data-stu-id="069fb-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="069fb-200">[Panoramica di SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) di Databricks</span><span class="sxs-lookup"><span data-stu-id="069fb-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
