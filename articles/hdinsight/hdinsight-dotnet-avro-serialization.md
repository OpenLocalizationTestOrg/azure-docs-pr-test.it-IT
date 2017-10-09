---
title: aaaSerialize dati in Hadoop - Microsoft Avro Library - Azure | Documenti Microsoft
description: Informazioni su come tooserialize e deserializzare i dati in Hadoop in HDInsight hello Microsoft Avro Library toopersist toomemory, un database o file.
keywords: avro, avro hadoop
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Serializzare i dati in Hadoop con hello Microsoft Avro Library

>[!NOTE]
>Hello Avro SDK non è più supportata da Microsoft. libreria di Hello è community open source è supportato. le origini per la libreria hello Hello si trovano in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Questo argomento viene illustrato come hello toouse [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) oggetti tooserialize e altri dati strutture in flussi toopersist li toomemory, un database o un file. Viene inoltre illustrato come toodeserialize tali oggetti di toorecover hello originali.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa hello Apache Avro sistema di serializzazione dei dati per l'ambiente di Microsoft.NET hello. Apache Avro offre un formato compatto di interscambio dei dati binari per la serializzazione Usa <a href="http://www.json.org" target="_blank">JSON</a> toodefine uno schema indipendente dalla lingua che copra l'interoperabilità di linguaggio. I dati serializzati in un unico linguaggio possono essere letti in un altro linguaggio. I formati attualmente supportati sono C, C++, C#, Java, PHP, Python e Ruby. Informazioni dettagliate sul formato hello sono reperibile in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro specifica</a>. 

>[!NOTE]
>Hello Microsoft Avro Library non supporta hello procedura remota (RPC) le chiamate parte di questa specifica.
>

rappresentazione di Hello serializzato di un oggetto in hello sistema Avro è costituita da due parti: schema e il valore effettivo. schema Avro Hello descrive il modello di dati di indipendente dal linguaggio hello dei dati di hello serializzato con JSON. È presentato side-by-side con una rappresentazione binaria dei dati. Con schema hello separato dalla rappresentazione binaria di hello consente toobe ogni oggetto scritti con alcun sovraccarico per ogni valore, eseguire la serializzazione veloce e hello rappresentazione piccole.

## <a name="hello-hadoop-scenario"></a>scenario di Hadoop Hello
formato di serializzazione di Apache Avro Hello è ampiamente utilizzato in Azure HDInsight e altri ambienti di Apache Hadoop. Avro fornisce un modo pratico di toorepresent strutture di dati complessi all'interno di un processo Hadoop MapReduce. formato Hello di file Avro (file contenitore di oggetti Avro) è stato progettato toosupport hello distribuita MapReduce modello di programmazione. funzionalità chiave Hello che abilita la distribuzione di hello è che i file hello "divisibili" nel senso hello che uno può cercare qualsiasi punto in un file e avviare la lettura da un blocco specifico.

## <a name="serialization-in-avro-library"></a>Serializzazione nella libreria Avro
Hello libreria .NET per Avro supporta due tipi di serializzare oggetti in:

* **Reflection** -schema JSON hello per i tipi di hello viene automaticamente creato da dati di hello attributi del contratto di toobe di tipi .NET hello serializzato.
* **record generico** -schema A JSON è specificato in modo esplicito in un record rappresentato da hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe se nessun tipo .NET è presenti toodescribe hello lo schema per hello dati toobe serializzato.

Quando è noto schema dati hello tooboth hello scrittura e lettura del flusso di hello dati hello possono essere inviati senza schema. In casi quando viene utilizzato un file di contenitore di oggetti Avro, hello schema viene archiviato nel file hello. Altri parametri, ad esempio i codec hello usato per la compressione dei dati, possono essere specificati. Questi scenari sono descritte in dettaglio e illustrati nella hello esempi di codice seguente:

## <a name="install-avro-library"></a>Installare la libreria Avro
di seguito Hello sono necessari prima di installare la libreria hello:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (versione 6.0.4 o successive)

Si noti che la dipendenza Newtonsoft.Json.dll hello viene scaricata automaticamente con l'installazione di hello di hello Microsoft Avro Library. Hello procedura nella seguente sezione hello:

Hello Microsoft Avro Library viene distribuito come pacchetto NuGet che può essere installato da Visual Studio tramite hello seguente procedura:

1. Seleziona hello **progetto** -> scheda **Gestisci pacchetti NuGet...**
2. Ricerca di "Microsoft.Hadoop.Avro" in hello **ricerca Online** casella.
3. Fare clic su hello **installare** accanto troppo**libreria Avro di Microsoft Azure HDInsight**.

Si noti che hello Newtonsoft.Json.dll (> = 6.0.4) dipendenza viene anche scaricata automaticamente con Microsoft Avro Library hello.

codice sorgente Microsoft Avro Library Hello è disponibile all'indirizzo [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Compilare schemi tramite la libreria Avro
Hello Microsoft Avro Library contiene una generazione di codice utilità che consente di creare i tipi c# automaticamente in base alle hello è definito in precedenza lo schema JSON. utilità per la generazione di codice Hello non viene distribuita come un eseguibile binario, ma è possibile compilare facilmente tramite hello seguente procedura:

1. Scaricare il file con estensione zip hello con la versione più recente di hello del codice sorgente di HDInsight SDK da <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK per Hadoop</a>. (Fare clic su hello **scaricare** icona, non hello **Scarica** scheda.)
2. Estrarre hello directory tooa HDInsight SDK nel computer di hello con .NET Framework 4 è installato e connesso toohello Internet per scaricare i pacchetti NuGet dipendenze necessarie. Di seguito, si presuppone che il codice sorgente hello è tooC:\SDK estratti.
3. Passare la cartella toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools ed eseguire build.bat. (hello chiamate file MSBuild dalla distribuzione di hello 32 bit di .NET Framework hello. Se si desidera una versione a 64 bit hello toouse, modifica Build. bat seguente hello commenti nel file hello.) Verificare che la compilazione hello ha esito positivo. In alcuni sistemi MSBuild può generare avvisi, Questi avvisi non influiscono utilità hello, purché non siano presenti errori di compilazione.)
4. utilità Hello compilato si trova in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget familiarità con la sintassi della riga di comando hello, eseguire comando seguente dalla cartella hello in cui si trova utilità per la generazione di codice hello hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

utilità di hello tootest, è possibile generare classi c# dal file dello schema JSON esempio hello fornito con il codice sorgente hello. Eseguire hello comando seguente:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Questo dovrebbe tooproduce due file c# nella directory corrente hello: SensorData.cs e Location.cs.

la logica di hello toounderstand utilità per la generazione di codice hello è in uso durante la conversione di tipi tooC # hello JSON schema, vedere hello file GenerationVerification.feature nella C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Spazi dei nomi vengono estratti dallo schema JSON hello, utilizzando la logica di hello descritta nel file hello menzionato nel paragrafo precedente hello. Spazi dei nomi estratti dallo schema hello hanno la precedenza su qualsiasi viene fornito con il parametro /n hello hello utilità riga di comando. Se si desidera spazi dei nomi hello toooverride contenuti all'interno dello schema di hello, utilizzare il parametro /nf hello. Ad esempio, di eseguire tutti gli spazi dei nomi hello SampleJSONSchema.avsc toomy.own.nspace, di toochange hello il seguente comando:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Sugli esempi di hello
Sei esempi forniti in questo argomento vengono illustrati i diversi scenari supportati da Microsoft Avro Library hello. Hello Microsoft Avro Library è progettato toowork con qualsiasi flusso. Per semplicità e coerenza, in questi esempi i dati vengono modificati usando flussi di memoria anziché flussi di file o database. approccio Hello eseguita in un ambiente di produzione dipende dall'origine dati, i requisiti di scenario esatti hello e volume, vincoli relativi alle prestazioni e altri fattori.

Hello come primo mostra due esempi tooserialize e deserializzare i dati nei buffer di flusso di memoria tramite la reflection e record di tipo generico. Hello dello schema in questi due casi presuppone toobe condivisi tra hello lettori e writer fuori banda.

Hello terza e quarta esempi viene illustrato come tooserialize e deserializzare i dati utilizzando i file hello Avro oggetto contenitore. Quando i dati vengono archiviati in un file contenitore Avro, lo schema viene sempre archiviato con quanto hello schema deve essere condiviso per la deserializzazione.

Hello che contiene l'esempio hello primi quattro esempi possono essere scaricati dal hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure esempi di codice</a> sito.

Hello quinto esempio viene illustrato come file contenitore dell'oggetto toouse un codec di compressione personalizzata per Avro. Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure esempi di codice</a> sito.

esempio di sesto Hello viene illustrato come toouse Avro serializzazione tooupload dati tooAzure nell'archiviazione Blob e analizzarli tramite Hive con un cluster HDInsight (Hadoop). Può essere scaricato da hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure esempi di codice</a> sito.

Di seguito sono collegamenti descritti nell'argomento hello toohello sei campioni:

* <a href="#Scenario1">**Serializzazione con reflection** </a> -schema JSON hello per toobe tipi serializzati viene automaticamente creato da dati di hello attributi del contratto.
* <a href="#Scenario2">**Serializzazione con record generico** </a> -schema JSON hello è specificato in modo esplicito in un record di alcun tipo .NET non è disponibile per la reflection.
* <a href="#Scenario3">**Serializzazione utilizzando i file oggetto contenitore con reflection** </a> -schema JSON hello viene compilato automaticamente ed è condiviso con dati serializzato hello tramite un file di contenitore di oggetti Avro.
* <a href="#Scenario4">**Serializzazione utilizzando i file oggetto contenitore con record generico** </a> -schema JSON hello in modo esplicito specificato prima della serializzazione hello e condivisi con i dati di hello tramite un file di contenitore di oggetti Avro.
* <a href="#Scenario5">**Serializzazione utilizzando i file oggetto contenitore con un codec di compressione personalizzata** </a> -hello nell'esempio viene illustrato come un Avro toocreate oggetto file contenitore con un'implementazione personalizzata di .NET del codec di compressione dati hello Deflate.
* <a href="#Scenario6">**Utilizzando i dati di tooupload Avro per il servizio Microsoft Azure HDInsight hello** </a> -esempio hello viene illustrata l'interazione di serializzazione Avro con hello servizio HDInsight. Un attiva Azure sottoscrizione e accesso tooan Azure HDInsight cluster sono necessari toorun in questo esempio.

## <a name="Scenario1"></a>Esempio 1: Serializzazione con reflection
schema JSON Hello per i tipi di hello può essere automaticamente generato da hello Microsoft Avro Library tramite reflection da dati hello attributi del contratto di hello c# oggetti toobe serializzato. Hello Microsoft Avro Library consente di creare un [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello campi toobe serializzato.

In questo esempio, gli oggetti (un **SensorData** classe con un membro **percorso** struct) vengono serializzati tooa flusso di memoria e il flusso viene a sua volta deserializzato. Hello risultato viene quindi confrontato toohello iniziale dell'istanza tooconfirm tale hello **SensorData** oggetto recuperato è identica toohello originale.

schema di Hello in questo esempio si presuppone che toobe condivisi tra hello lettori e writer, quindi formato contenitore di oggetti Avro hello non è necessario. Per un esempio di come tooserialize e deserializzare i dati nei buffer di memoria tramite reflection con formato di contenitore oggetto hello quando schema hello deve essere condivisi con i dati di hello, vedere <a href="#Scenario3">serializzazione utilizzando i file oggetto contenitore con reflection</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Esempio 2: Serializzazione con un record generico
Uno schema JSON può essere specificato in modo esplicito in un record generico quando la reflection non può essere utilizzata perché non è possibile rappresentare dati hello tramite le classi .NET con un contratto dati. Questo metodo risulta più lento rispetto all'uso della reflection. In tali casi, lo schema di hello per hello dati può essere dinamico, vale a dire, non è noto in fase di compilazione. Dati rappresentati come valori delimitati da virgole per i file (CSV) il cui schema è sconosciuto fino a quando non viene trasformato il formato Avro toohello in fase di esecuzione è riportato un esempio di questo tipo di scenario dinamico.

Questo esempio viene illustrato come toocreate e utilizzare un [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specificare uno schema JSON, come toopopulate con dati hello e come quindi tooserialize e deserializzarlo. Hello risultato viene confrontato toohello tooconfirm di istanze iniziale che hello record recuperato è identica toohello originale.

schema di Hello in questo esempio si presuppone che toobe condivisi tra hello lettori e writer, quindi formato contenitore di oggetti Avro hello non è necessario. Per un esempio di come tooserialize e deserializzare i dati nei buffer di memoria usando un record generico con il formato di contenitore oggetto hello quando schema hello deve essere incluso con i dati serializzato hello, vedere hello <a href="#Scenario4">serializzazione utilizzando contenitore di oggetti i file con record generico</a> esempio.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Esempio 3: serializzazione mediante file contenitore di oggetti e serializzazione con reflection
Questo esempio è simile scenario toohello in hello <a href="#Scenario1"> primo esempio</a>, in cui schema hello è specificato in modo implicito tramite la reflection. Hello differenza è che in questo caso, schema hello non viene considerato come toobe lettore toohello che deserializza noto. Hello **SensorData** toobe oggetti serializzati e lo schema specificato in modo implicito vengono archiviati in un file di contenitore di oggetti Avro rappresentato da hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.

in questo esempio con i dati di Hello vengono serializzati [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) e deserializzato con [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). Hello risulta quindi confrontati toohello istanze iniziale tooensure identità.

Hello in hello oggetto dati file contenitore è compresso tramite predefinito hello [ **Deflate** ] [ deflate-100] codec di compressione da .NET Framework 4. Vedere hello <a href="#Scenario5"> quinto esempio</a> in toolearn in questo argomento come una versione più recente e superiore di hello toouse [ **Deflate** ] [ deflate-110] compressione codec disponibili in .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Esempio 4: serializzazione mediante file contenitore di oggetti e serializzazione con un record generico
Questo esempio è simile scenario toohello in hello <a href="#Scenario2"> secondo esempio</a>, in schema di hello è specificato in modo esplicito con JSON. Hello differenza è che in questo caso, schema hello non viene considerato come toobe lettore toohello che deserializza noto.

Hello set di dati di test vengono raccolti in un elenco di [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) oggetti tramite uno schema definito in modo esplicito di JSON e quindi archiviati in un file contenitore oggetto rappresentato da hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe. Questo file contenitore crea un writer che sono utilizzati tooserialize hello dati, non compressi, flusso di memoria tooa che viene quindi salvato tooa file. Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parametro utilizzato per creare il lettore di hello specifica che i dati non sono compressi.

dati Hello viene quindi in grado di leggere dal file hello e deserializzati in una raccolta di oggetti. Questa raccolta è toohello confrontati elenco iniziale di tooconfirm record Avro che siano identici.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Esempio 5: serializzazione mediante file contenitore di oggetti con un codec di compressione personalizzato
Hello quinto esempio viene illustrato come file contenitore dell'oggetto toouse un codec di compressione personalizzata per Avro. Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello [Azure esempi di codice](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) sito.

Hello [Avro specifica](http://avro.apache.org/docs/current/spec.html#Required+Codecs) consente l'utilizzo di un codec di compressione facoltativo (inoltre troppo**Null** e **Deflate** impostazioni predefinite). In questo esempio non implementa un nuovo codec, ad esempio Snappy (indicato come un codec supportato facoltativo in hello [Avro specifica](http://avro.apache.org/docs/current/spec.html#snappy)). Viene illustrato come toouse hello implementazione di .NET Framework 4.5 di hello [ **Deflate** ] [ deflate-110] codec, che fornisce un algoritmo di compressione migliore in base a hello [zlib](http://zlib.net/) libreria di compressione di una versione di .NET Framework 4 hello predefinita.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Esempio 6: Utilizzo di dati di tooupload Avro per hello servizio Microsoft Azure HDInsight
esempio di sesto Hello illustra alcuni toointeracting correlati tecniche programmazione con il servizio di Azure HDInsight hello. Un esempio che contiene il codice hello per questo esempio può essere scaricato da hello [Azure esempi di codice](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) sito.

esempio Hello hello quanto segue:

* Si connette tooan cluster del servizio HDInsight esistente.
* Serializza i diversi file CSV e il caricamento di archiviazione Blob di hello risultato tooAzure. (file CSV hello distribuiti insieme: esempio hello e rappresentano un estratto i dati cronologici AMEX Stock distribuiti da [Infochimps](http://www.infochimps.com/) per il periodo di hello 1970-2010. esempio Hello legge i dati di file CSV, converte hello tooinstances record di hello **Stock** classe e quindi li serializza tramite reflection. Definizione di tipo azionario viene creato da uno schema JSON tramite hello utilità per la generazione di codice Microsoft Avro Library.
* Crea una nuova tabella esterna denominata **scorte** nell'Hive e lo collega toohello dati caricati nel passaggio precedente hello.
* Esegue una query Hive tramite hello **scorte** tabella.

Esempio hello, inoltre, esegue una procedura di pulizia prima e dopo le operazioni principali. Durante hello pulizia tutti hello relative cartelle e i dati Blob di Azure vengono rimossi tabella Hive hello viene eliminata. È inoltre possibile richiamare una stored procedure di pulizia hello dalla riga di comando di esempio hello.

esempio Hello è hello seguenti prerequisiti:

* Una sottoscrizione di Microsoft Azure attiva con il relativo ID sottoscrizione.
* Un certificato di gestione per la sottoscrizione di hello con chiave privata corrispondente hello. Hello certificato deve essere installato in hello corrente utente privato archiviazione nel computer utilizzato hello toorun: esempio hello.
* Un cluster HDInsight attivo.
* Un account di archiviazione di Azure collegati cluster HDInsight toohello da prerequisito precedente hello, con chiave di accesso primaria o secondaria corrispondente hello.

Le informazioni di hello dai prerequisiti hello deve essere immesso toohello file di configurazione di esempio prima di eseguita l'esempio hello. Esistono due modi possibili toodo è:

* Modificare il file app. config hello nella directory radice di esempio hello e quindi compilare l'esempio hello
* Innanzitutto compilare l'esempio hello e quindi modificare AvroHDISample.exe.config nella directory di compilazione hello

In entrambi i casi, è necessario eseguire tutte le modifiche in hello  **<appSettings>**  sezione Impostazioni. Seguire i commenti di hello nel file hello.
Hello esempio viene eseguito dalla riga di comando hello eseguendo hello comando seguente (dove hello file ZIP con l'esempio hello presupposto tooC:\AvroHDISample toobe estratti; se in caso contrario, utilizzare hello rilevanti percorso file):

    AvroHDISample run C:\AvroHDISample\Data

tooclean di cluster hello, eseguire hello comando seguente:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
