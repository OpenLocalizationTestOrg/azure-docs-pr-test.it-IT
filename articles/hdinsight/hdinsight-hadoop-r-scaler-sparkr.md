---
title: Usare ScaleR e SparkR con Azure HDInsight | Microsoft Docs
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
ms.openlocfilehash: 29733f6f6b725dd4735219ed221431805558a5e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="d1958-103">Uso combinato di ScaleR e SparkR in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1958-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="d1958-104">In questo articolo viene illustrato come stimare i ritardi dei voli di arrivo usando un modello di regressione logistica **ScaleR** sui ritardi dei voli e il meteo associato a **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="d1958-104">This article shows how to predict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="d1958-105">Questo scenario dimostra le capacità di ScaleR per la manipolazione dei dati in Spark con Microsoft R Server ai fini dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="d1958-105">This scenario demonstrates the capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="d1958-106">La combinazione di queste tecnologie consente di applicare le più recenti funzionalità di elaborazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="d1958-106">The combination of these technologies enables you to apply the latest capabilities in distributed processing.</span></span>

<span data-ttu-id="d1958-107">Sebbene vengano eseguiti nel motore di esecuzione di Hadoop Spark, entrambi i pacchetti sono bloccati da una condivisione dei dati in memoria in quanto ognuno di essi richiede le rispettive sessioni Spark.</span><span class="sxs-lookup"><span data-stu-id="d1958-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="d1958-108">Finché questo problema non verrà risolto in una versione futura di R Server, la soluzione alternativa consiste nel mantenere sessioni di Spark non sovrapposte e scambiare i dati tramite file intermedi.</span><span class="sxs-lookup"><span data-stu-id="d1958-108">Until this issue is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and to exchange data through intermediate files.</span></span> <span data-ttu-id="d1958-109">Le istruzioni riportate di seguito mostrano che questi requisiti sono semplici da rispettare.</span><span class="sxs-lookup"><span data-stu-id="d1958-109">The instructions here show that these requirements are straightforward to achieve.</span></span>

<span data-ttu-id="d1958-110">Verrà usato un esempio condiviso inizialmente in un discorso tenuto a Strata 2016 da Mario Inchiosa e Roni Burd, disponibile anche nel webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio) (Compilazione di una piattaforma Data Science scalabile con R). L'esempio usa SparkR per aggiungere il set di dati noti sui ritardi di arrivo delle compagnie aeree con i dati meteo degli aeroporti di partenza e di arrivo.</span><span class="sxs-lookup"><span data-stu-id="d1958-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="d1958-111">I dati aggiunti sono quindi usati come input per un modello di regressione logistica ScaleR per stimare il ritardo di arrivo dei voli.</span><span class="sxs-lookup"><span data-stu-id="d1958-111">The data joined is then used as input to a ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="d1958-112">Il codice dettagliato è stato scritto originariamente per R Server in esecuzione in Spark in un cluster HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1958-112">The code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="d1958-113">Tuttavia, il concetto di combinazione dell'uso di SparkR e ScaleR in un unico script è valido anche nel contesto di ambienti locali.</span><span class="sxs-lookup"><span data-stu-id="d1958-113">But the concept of mixing the use of SparkR and ScaleR in one script is also valid in the context of on-premises environments.</span></span> <span data-ttu-id="d1958-114">Nell'esempio seguente si suppone un livello intermedio di conoscenza di R e della libreria [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) di R Server.</span><span class="sxs-lookup"><span data-stu-id="d1958-114">In the following, we presume an intermediate level of knowledge of R and R the [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="d1958-115">Durante l'analisi di questo scenario si introdurrà anche l'uso di [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html).</span><span class="sxs-lookup"><span data-stu-id="d1958-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="the-airline-and-weather-datasets"></a><span data-ttu-id="d1958-116">Set di dati relativi alle compagnie aeree e alle previsioni meteo</span><span class="sxs-lookup"><span data-stu-id="d1958-116">The airline and weather datasets</span></span>

<span data-ttu-id="d1958-117">**AirOnTime08to12CSV**, il set di dati pubblico delle compagnie aree, contiene i dettagli sui voli in arrivo e in partenza per tutti i voli commerciali all'interno degli Stati Uniti da ottobre 1987 a dicembre 2012.</span><span class="sxs-lookup"><span data-stu-id="d1958-117">The **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span></span> <span data-ttu-id="d1958-118">Si tratta di un set di dati di grandi dimensioni con quasi 150 milioni di record totali,</span><span class="sxs-lookup"><span data-stu-id="d1958-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="d1958-119">che occupa poco meno di 4 GB dopo la decompressione.</span><span class="sxs-lookup"><span data-stu-id="d1958-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="d1958-120">Il set di dati è disponibile negli [archivi del governo statunitense](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)</span><span class="sxs-lookup"><span data-stu-id="d1958-120">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="d1958-121">e più comodamente come file zip (AirOnTimeCSV.zip) contenente un set di 303 file con estensione CSV mensili separati nel [repository di set di dati di Revolution Analytics](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="d1958-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="d1958-122">Per esaminare gli effetti delle condizioni meteorologiche sui ritardi di voli sono necessari anche i dati meteo di ogni aeroporto.</span><span class="sxs-lookup"><span data-stu-id="d1958-122">To see the effects of weather on flight delays, we also need the weather data at each of the airports.</span></span> <span data-ttu-id="d1958-123">Questi possono essere scaricati come file zip in formato non elaborato, suddivisi per mese dal [repository della National Oceanic and Atmospheric Administration](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="d1958-123">This data can be downloaded as zip files in raw form, by month, from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="d1958-124">Per questo esempio sono stati estratti i dati meteo da maggio 2007 a dicembre 2012 e sono stati usati i file dei dati orari in ognuno dei 68 zip mensili.</span><span class="sxs-lookup"><span data-stu-id="d1958-124">For the purposes of this example, we pull weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span></span> <span data-ttu-id="d1958-125">I file zip mensili contengono anche un mapping (YYYYMMstation.txt) tra l'ID della stazione meteo (WBAN), l'aeroporto di riferimento (CallSign) e l'offset di fuso orario dell'aeroporto rispetto all'ora UTC (TimeZone).</span><span class="sxs-lookup"><span data-stu-id="d1958-125">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport that it is associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="d1958-126">Tutti questi dati sono necessari per eseguire il join con i dati sui ritardi e il meteo registrati dalle compagnie aeree.</span><span class="sxs-lookup"><span data-stu-id="d1958-126">All of this information is needed when joining with the airline delay and weather data.</span></span>

## <a name="setting-up-the-spark-environment"></a><span data-ttu-id="d1958-127">Configurazione dell'ambiente Spark</span><span class="sxs-lookup"><span data-stu-id="d1958-127">Setting up the Spark environment</span></span>

<span data-ttu-id="d1958-128">Il primo passaggio consiste nel configurare l'ambiente Spark.</span><span class="sxs-lookup"><span data-stu-id="d1958-128">The first step is to set up the Spark environment.</span></span> <span data-ttu-id="d1958-129">Iniziare puntando alla directory contenente le directory dei dati di input, creando un contesto di calcolo Spark e quindi una funzione di registrazione per la registrazione delle informazioni alla console:</span><span class="sxs-lookup"><span data-stu-id="d1958-129">We begin by pointing to the directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session to reduce startup times 
#   (remember to stop it later!)
 
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

<span data-ttu-id="d1958-130">Aggiungere quindi "Spark_Home" al percorso di ricerca per i pacchetti R in modo che sia possibile usare SparkR e inizializzare una sessione SparkR:</span><span class="sxs-lookup"><span data-stu-id="d1958-130">Next we add “Spark_Home” to the search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

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

## <a name="preparing-the-weather-data"></a><span data-ttu-id="d1958-131">Preparazione dei dati meteo</span><span class="sxs-lookup"><span data-stu-id="d1958-131">Preparing the weather data</span></span>

<span data-ttu-id="d1958-132">Per preparare i dati meteo, creare un subset per le colonne necessarie per la modellazione:</span><span class="sxs-lookup"><span data-stu-id="d1958-132">To prepare the weather data, we subset it to the columns needed for modeling:</span></span> 

- <span data-ttu-id="d1958-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="d1958-133">"Visibility"</span></span>
- <span data-ttu-id="d1958-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="d1958-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="d1958-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="d1958-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="d1958-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="d1958-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="d1958-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="d1958-137">"WindSpeed"</span></span>
- <span data-ttu-id="d1958-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="d1958-138">"Altimeter"</span></span>

<span data-ttu-id="d1958-139">Aggiungere quindi un codice aeroporto associato a una stazione meteo e convertire le misurazioni dall'ora locale in ora UTC.</span><span class="sxs-lookup"><span data-stu-id="d1958-139">Then we add an airport code associated with the weather station and convert the measurements from local time to UTC.</span></span>

<span data-ttu-id="d1958-140">Iniziare creando un file per eseguire il mapping delle informazioni sulla stazione meteo (WBAN) al codice dell'aeroporto.</span><span class="sxs-lookup"><span data-stu-id="d1958-140">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span></span> <span data-ttu-id="d1958-141">È stato possibile ottenere questa correlazione dal file di mapping incluso con i dati meteo,</span><span class="sxs-lookup"><span data-stu-id="d1958-141">We could get this correlation from the mapping file included with the weather data.</span></span> <span data-ttu-id="d1958-142">eseguendo il mapping del campo *CallSign* (ad esempio, LAX) nel file di dati meteo con *Origin* nei dati relativi alle compagnie aeree.</span><span class="sxs-lookup"><span data-stu-id="d1958-142">By mapping the *CallSign* (for example, LAX) field in the weather data file to *Origin* in the airline data.</span></span> <span data-ttu-id="d1958-143">Tuttavia, si dispone di un altro mapping per il campo *WBAN* in *AirportID* (ad esempio, 12892 per LAX) che include il *fuso orario*, salvato in un file CSV denominato "wban-to-airport-id-tz.CSV", che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="d1958-143">However, we just happened to have another mapping on hand that maps *WBAN* to *AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="d1958-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d1958-144">For example:</span></span>

| <span data-ttu-id="d1958-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="d1958-145">AirportID</span></span> | <span data-ttu-id="d1958-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="d1958-146">WBAN</span></span> | <span data-ttu-id="d1958-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="d1958-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="d1958-148">10685</span><span class="sxs-lookup"><span data-stu-id="d1958-148">10685</span></span> | <span data-ttu-id="d1958-149">54831</span><span class="sxs-lookup"><span data-stu-id="d1958-149">54831</span></span> | <span data-ttu-id="d1958-150">-6</span><span class="sxs-lookup"><span data-stu-id="d1958-150">-6</span></span>
| <span data-ttu-id="d1958-151">14871</span><span class="sxs-lookup"><span data-stu-id="d1958-151">14871</span></span> | <span data-ttu-id="d1958-152">24232</span><span class="sxs-lookup"><span data-stu-id="d1958-152">24232</span></span> | <span data-ttu-id="d1958-153">-8</span><span class="sxs-lookup"><span data-stu-id="d1958-153">-8</span></span>
| <span data-ttu-id="d1958-154">..</span><span class="sxs-lookup"><span data-stu-id="d1958-154">..</span></span> | <span data-ttu-id="d1958-155">..</span><span class="sxs-lookup"><span data-stu-id="d1958-155">..</span></span> | <span data-ttu-id="d1958-156">..</span><span class="sxs-lookup"><span data-stu-id="d1958-156">..</span></span>

<span data-ttu-id="d1958-157">Il codice seguente legge ognuno dei file di dati relativi al meteo non elaborati per ora, crea i subset per le colonne necessari, unisce il file di mapping della stazione meteo, modifica orari e date dei valori in UTC e quindi scrive una nuova versione del file:</span><span class="sxs-lookup"><span data-stu-id="d1958-157">The following code reads each of the hourly raw weather data files, subsets to the columns we need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file:</span></span>

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

## <a name="importing-the-airline-and-weather-data-to-spark-dataframes"></a><span data-ttu-id="d1958-158">Importazione dei dati relativi al meteo e alle compagnie aeree per i DataFrame di Spark</span><span class="sxs-lookup"><span data-stu-id="d1958-158">Importing the airline and weather data to Spark DataFrames</span></span>

<span data-ttu-id="d1958-159">A questo punto verrà usata la funzione SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) per importare i dati relativi al meteo e alle compagnie aeree nei DataFrame di Spark.</span><span class="sxs-lookup"><span data-stu-id="d1958-159">Now we use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span></span> <span data-ttu-id="d1958-160">Questa funzione, come molti altri metodi Spark, viene eseguita in modo differito, vale a dire che viene accodata per l'esecuzione, ma eseguita solo quando è necessario.</span><span class="sxs-lookup"><span data-stu-id="d1958-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for the airline data

logmsg('create a SparkR DataFrame for the airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for the weather data

logmsg('create a SparkR DataFrame for the weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="d1958-161">Pulizia e trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="d1958-161">Data cleansing and transformation</span></span>

<span data-ttu-id="d1958-162">Successivamente viene eseguita una pulizia dei dati relativi alle compagnie aeree importati per rinominare le colonne.</span><span class="sxs-lookup"><span data-stu-id="d1958-162">Next we do some cleanup on the airline data we’ve imported to rename columns.</span></span> <span data-ttu-id="d1958-163">Verranno tenute le sole variabili necessarie e gli orari di partenza pianificati saranno arrotondati all'ora più vicina per consentire l'unione con i dati meteo più recenti alla partenza:</span><span class="sxs-lookup"><span data-stu-id="d1958-163">We only keep the variables needed, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data at departure:</span></span>

```
logmsg('clean the airline data') 
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

# Select desired columns from the flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time to full hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="d1958-164">A questo punto si eseguiranno operazioni simili sui dati meteo:</span><span class="sxs-lookup"><span data-stu-id="d1958-164">Now we perform similar operations on the weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean the weather data') 
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

## <a name="joining-the-weather-and-airline-data"></a><span data-ttu-id="d1958-165">Unione in join dei dati meteo e delle compagnie aeree</span><span class="sxs-lookup"><span data-stu-id="d1958-165">Joining the weather and airline data</span></span>

<span data-ttu-id="d1958-166">La funzione [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) di SparkR verrà ora usata per eseguire un left outer join dei dati sulle compagnie aeree e dei dati meteo in base ai valori di datetime e AirportID di partenza.</span><span class="sxs-lookup"><span data-stu-id="d1958-166">We now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="d1958-167">L'outer join consente di conservare tutti i record dei dati relativi alle compagnie aeree, anche in assenza di dati meteo corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d1958-167">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="d1958-168">Dopo il join verranno rimosse alcune colonne ridondanti e verranno rinominate le colonne conservate per rimuovere il prefisso DataFrame introdotto dal join.</span><span class="sxs-lookup"><span data-stu-id="d1958-168">Following the join, we remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span></span>

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

<span data-ttu-id="d1958-169">In modo analogo verrà eseguito il join dei dati meteo e dei dati delle compagnie aeree in base ai valori datetime e AirportID di arrivo:</span><span class="sxs-lookup"><span data-stu-id="d1958-169">In a similar fashion, we join the weather and airline data based on arrival AirportID and datetime:</span></span>

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

## <a name="save-results-to-csv-for-exchange-with-scaler"></a><span data-ttu-id="d1958-170">Salvare i risultati in un file con formato CSV per lo scambio con ScaleR</span><span class="sxs-lookup"><span data-stu-id="d1958-170">Save results to CSV for exchange with ScaleR</span></span>

<span data-ttu-id="d1958-171">Questa azione completa i join che è necessario eseguire con SparkR.</span><span class="sxs-lookup"><span data-stu-id="d1958-171">That completes the joins we need to do with SparkR.</span></span> <span data-ttu-id="d1958-172">I dati verranno salvati da "joinedDF5" del DataFrame di Spark finale in un file CSV per ScaleR e quindi verrà chiusa la sessione di SparkR.</span><span class="sxs-lookup"><span data-stu-id="d1958-172">We save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span></span> <span data-ttu-id="d1958-173">È possibile indicare in modo esplicito a SparkR di salvare il file CSV risultante in 80 partizioni separate per abilitare un parallelismo sufficiente durante l'elaborazione in ScaleR:</span><span class="sxs-lookup"><span data-stu-id="d1958-173">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output the joined data from Spark to CSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result to directory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down the SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-to-xdf-for-use-by-scaler"></a><span data-ttu-id="d1958-174">Importare in XDF per l'uso da parte di ScaleR</span><span class="sxs-lookup"><span data-stu-id="d1958-174">Import to XDF for use by ScaleR</span></span>

<span data-ttu-id="d1958-175">È possibile usare direttamente il file CSV dei dati relativi al meteo e alle compagnie aeree aggiunti per la modellazione tramite un'origine dati di testo ScaleR.</span><span class="sxs-lookup"><span data-stu-id="d1958-175">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="d1958-176">Tuttavia, il file CSV dovrà prima essere importato con estensione XDF, in quanto è più efficiente quando si eseguono più operazioni sul set di dati:</span><span class="sxs-lookup"><span data-stu-id="d1958-176">But we import it to XDF first, since it is more efficient when running multiple operations on the dataset:</span></span>

```
logmsg('Import the CSV to compressed, binary XDF format') 

# set the Spark compute context for R Server 
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

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="d1958-177">Suddivisione dei dati per il training e il test</span><span class="sxs-lookup"><span data-stu-id="d1958-177">Splitting data for training and test</span></span>

<span data-ttu-id="d1958-178">rxDataStep viene usato per suddividere i dati del 2012 per il test e mantenere il resto per il training:</span><span class="sxs-lookup"><span data-stu-id="d1958-178">We use rxDataStep to split out the 2012 data for testing and keep the rest for training:</span></span>

```
# split out the training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out the testing data

logmsg('split out the test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="d1958-179">Eseguire il training e il test di un modello di regressione logistica</span><span class="sxs-lookup"><span data-stu-id="d1958-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="d1958-180">A questo punto è possibile compilare un modello.</span><span class="sxs-lookup"><span data-stu-id="d1958-180">Now we are ready to build a model.</span></span> <span data-ttu-id="d1958-181">Per visualizzare l'influenza dei dati meteo sui ritardi dell'ora di arrivo verrà usata la routine di regressione logistica di ScaleR.</span><span class="sxs-lookup"><span data-stu-id="d1958-181">To see the influence of weather data on delay in the arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="d1958-182">Questa viene usata per la modellazione se un ritardo di arrivo maggiore di 15 minuti è influenzato dal meteo negli aeroporti di partenza e arrivo:</span><span class="sxs-lookup"><span data-stu-id="d1958-182">We use it to model whether an arrival delay of greater than 15 minutes is influenced by the weather at the departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use the scalable rxLogit() function but set max iterations to 3 for the purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="d1958-183">Esaminare come procede sui dati di test eseguendo alcune previsioni e analizzando le curve ROC e AUC.</span><span class="sxs-lookup"><span data-stu-id="d1958-183">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over the test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use the scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under the Curve (AUC).

logmsg('calculate the roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="d1958-184">Assegnazione di punteggi in un'altra posizione</span><span class="sxs-lookup"><span data-stu-id="d1958-184">Scoring elsewhere</span></span>

<span data-ttu-id="d1958-185">È possibile anche usare il modello per l'assegnazione di punteggi ai dati in un'altra piattaforma</span><span class="sxs-lookup"><span data-stu-id="d1958-185">We can also use the model for scoring data on another platform.</span></span> <span data-ttu-id="d1958-186">salvandolo come file di Servizi desktop remoto e trasferendo e importando questo file di Servizi desktop remoto nell'ambiente per l'assegnazione di punteggi di destinazione, ad esempio Servizi R per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1958-186">By saving it to an RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="d1958-187">È importante assicurarsi che i factor level dei dati a cui assegnare un punteggio corrispondano a quelli in cui è stato creato il modello.</span><span class="sxs-lookup"><span data-stu-id="d1958-187">It is important to ensure that the factor levels of the data to be scored match those on which the model was built.</span></span> <span data-ttu-id="d1958-188">Questa corrispondenza può essere ottenuta tramite l'estrazione e il salvataggio delle informazioni sulla colonna associate ai dati di modellazione tramite la funzione `rxCreateColInfo()` di ScaleR, quindi applicando queste informazioni sulla colonna all'origine dati di input per la previsione.</span><span class="sxs-lookup"><span data-stu-id="d1958-188">That match can be achieved by extracting and saving the column infomation associated with the modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information to the input data source for prediction.</span></span> <span data-ttu-id="d1958-189">Di seguito sono state salvate alcune righe del set di dati di test e le informazioni sulla colonna verranno estratte e usate da questo esempio nello script di previsione:</span><span class="sxs-lookup"><span data-stu-id="d1958-189">In the following we save a few rows of the test dataset and extract and use the column information from this sample in the prediction script:</span></span>

```
# save the model and a sample of the test dataset 

logmsg('save serialized version of the model and a sample of the test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop the spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="d1958-190">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d1958-190">Summary</span></span>

<span data-ttu-id="d1958-191">In questo articolo è stato illustrato come è possibile combinare l'uso di SparkR per manipolare i dati con ScaleR per lo sviluppo di modelli di Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="d1958-191">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="d1958-192">In questo scenario è necessario gestire sessioni di Spark separate eseguendo una sola sessione alla volta e scambiando i dati tramite file CSV.</span><span class="sxs-lookup"><span data-stu-id="d1958-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="d1958-193">Anche se semplice, questo processo sarà ancora più semplice nella prossima versione di R Server in cui SparkR e ScaleR potranno condividere una sessione di Spark e pertanto i relativi DataFrame.</span><span class="sxs-lookup"><span data-stu-id="d1958-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="d1958-194">Passaggi successivi e altre informazioni</span><span class="sxs-lookup"><span data-stu-id="d1958-194">Next steps and more information</span></span>

- <span data-ttu-id="d1958-195">Per altre informazioni sull'uso di R Server in Spark, vedere la [Guida introduttiva su MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="d1958-195">For more information on use of R Server on Spark, see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="d1958-196">Per informazioni generali su R Server, vedere l'articolo [Introduzione a Microsoft R Server](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node).</span><span class="sxs-lookup"><span data-stu-id="d1958-196">For general information on R Server, see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="d1958-197">Per informazioni su R Server in HDInsight, vedere [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) (Panoramica di R Server in Azure HDInsight) e [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md) (R Server in Azure HDInsight).</span><span class="sxs-lookup"><span data-stu-id="d1958-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="d1958-198">Per altre informazioni sull'uso di SparkR, vedere:</span><span class="sxs-lookup"><span data-stu-id="d1958-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="d1958-199">Documento Apache SparkR</span><span class="sxs-lookup"><span data-stu-id="d1958-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="d1958-200">[Panoramica di SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) di Databricks</span><span class="sxs-lookup"><span data-stu-id="d1958-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
