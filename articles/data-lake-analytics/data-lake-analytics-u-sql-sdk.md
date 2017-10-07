---
title: locale aaaScale U-SQL eseguire e testare con Azure Data Lake U-SQL SDK | Documenti Microsoft
description: Informazioni su come eseguire e i test con riga di comando e le interfacce di programmazione nella workstation locale toouse processi tooscale U-SQL di Azure Data Lake U-SQL SDK locali.
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Ridimensionare esecuzione e test locali di U-SQL con l'SDK U-SQL di Azure Data Lake

Quando si sviluppano script U-SQL, è toorun comuni e script di test U-SQL localmente inviare prima toocloud. Per questo scenario, Azure Data Lake offre un pacchetto NuGet, denominato SDK U-SQL di Azure Data Lake, tramite cui è possibile ridimensionare facilmente l'esecuzione e il test locali di U-SQL. È inoltre possibile toointegrate questo U-SQL di test con l'elemento di configurazione (integrazione continua) sistema tooautomate hello compilazione e test.

Se si è interessati come toomanually locale esecuzione e il debug di script U-SQL con strumenti di grafica, è possibile utilizzare Azure Data Lake Tools per Visual Studio per tale. Altre informazioni sono disponibili [qui](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Installare l'SDK U-SQL di Azure Data Lake

È possibile ottenere hello Azure Data Lake U-SQL SDK [qui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) in Nuget.org. E prima di utilizzarlo, è necessario toomake che si dispone di dipendenze, come indicato di seguito.

### <a name="dependencies"></a>Dipendenze

Hello SDK Data Lake U-SQL, è necessario hello seguenti dipendenze:

- [Microsoft .NET Framework 4.6 o versione successiva](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 e Windows SDK 10.0.10240.0 o versione successiva (CppSDK in questo articolo). Esistono due modi tooget CppSDK:

    - Installare [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). È una cartella \Windows Kits\10 nella cartella programmi hello - ad esempio C:\Program Files (x86) \Windows Kits\10\. Versione di Windows 10 SDK hello in \Windows Kits\10\Lib sono anche disponibili. Se non viene visualizzato, le cartelle, reinstallare Visual Studio e che tooselect hello Windows 10 SDK durante l'installazione di hello. Se si dispone di questo installato con Visual Studio, del compilatore locale di hello U-SQL troverà automaticamente.

    ![Windows 10 SDK ad esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Installare [Strumenti Data Lake per Visual Studio](http://aka.ms/adltoolsvs). È possibile trovare hello commercializzato solo se preconfezionato C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK file Visual C++ e Windows SDK. In questo caso, compilatore locale di hello U-SQL non è possibile trovare dipendenze hello automaticamente. Percorso di CppSDK toospecify hello è necessario per tale. È possibile copiare tooanother percorso dei file di hello o utilizzarla lasciandola invariata.

## <a name="understand-basic-concepts"></a>Comprendere i concetti di base

### <a name="data-root"></a>Radice dei dati

cartella dati radice Hello è "archivio locale" per l'account di calcolo locale hello. Account archivio Azure Data Lake toohello equivalente di un account Data Lake Analitica è. Cartella radice di dati diverso cambio tooa è analoga a commutazione tooa archivio diverso account. Se si desidera tooaccess comunemente condiviso dati con le cartelle radice di dati diverso, è necessario utilizzare i percorsi assoluti negli script. In alternativa, creare collegamenti simbolici di file system (ad esempio, **mklink** in NTFS) in hello dati radice cartella toopoint toohello di dati condivisi.

cartella dati radice Hello viene utilizzato per:

- Archiviare i metadati locali, inclusi database, tabelle, funzioni con valori di tabella e assembly.
- Cercare hello di input e i percorsi di output che sono definiti come percorsi relativi nel U-SQL. Utilizzando i percorsi relativi rende più semplice toodeploy il tooAzure progetti U-SQL.

### <a name="file-path-in-u-sql"></a>Percorso dei file in U-SQL

Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale. percorso relativo di Hello è toohello relativo percorso della cartella radice di dati specificato. È consigliabile che si utilizza "/" come script compatibili con lato server hello hello toomake separatore di percorso. Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti. In questi esempi, C:\LocalRunDataRoot è cartella dati radice hello.

|Percorso relativo|Percorso assoluto|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Directory di lavoro

Quando si esegue uno script U-SQL hello in locale, una directory di lavoro viene creata durante la compilazione in directory di esecuzione corrente. Inoltre toohello compilazione restituisce, hello necessari file di runtime per l'esecuzione locale sarà directory di lavoro toothis copia shadow. Hello cartella radice di directory di lavoro viene chiamato "ScopeWorkDir" e il file hello in hello directory di lavoro sono i seguenti:

|Directory/File|Directory/File|Directory/File|Definizione|Descrizione|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Stringa di hash della versione di runtime|Copia shadow dei file di runtime necessari per l'esecuzione locale|
| |Script_66AE4909AA0ED06C| |Nome di script + stringa hash del percorso dello script|Output di compilazione e registrazione del passaggio di esecuzione|
| | |\_script\_.abr|Output del compilatore|File algebra|
| | |\_ScopeCodeGen\_.*|Output del compilatore|Codice gestito generato|
| | |\_ScopeCodeGenEngine\_.*|Output del compilatore|Codice nativo generato|
| | |referenced assemblies|Riferimento assembly|File assembly di riferimento|
| | |deployed_resources|Distribuzione risorse|File di distribuzione risorse|
| | |xxxxxxxx.xxx[1..n]\_\*.*|Log di esecuzione|Log dei passaggi di esecuzione|


## <a name="use-hello-sdk-from-hello-command-line"></a>Utilizzare hello SDK dalla riga di comando hello

### <a name="command-line-interface-of-hello-helper-application"></a>Interfaccia della riga di comando di un'applicazione hello helper

In SDK directory\build\runtime, LocalRunHelper.exe è un'applicazione hello helper della riga di comando che fornisce interfacce funzioni toomost di hello usata esecuzione locale. Si noti che entrambi hello comandi e opzioni dell'argomento hello tra maiuscole e minuscole. tooinvoke è:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Eseguire LocalRunHelper.exe senza argomenti oppure con hello **Guida** passare le informazioni della Guida di hello tooshow:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Informazioni sul supporto in hello:

-  **Comando** offre hello il nome del comando.  
-  **Argomento richiesto** elenca gli argomenti che devono essere forniti.  
-  **Argomento facoltativo** elenca gli argomenti facoltativi con i valori predefiniti.  Gli argomenti booleani facoltativi non dispongono di parametri e i relativi aspetti significa valore predefinito di tootheir negativo.

### <a name="return-value-and-logging"></a>Valore restituito e registrazione

Restituisce un'applicazione Hello helper **0** per l'esito positivo e **-1** per errore. Per impostazione predefinita, il supporto di hello invia la console corrente tutti i messaggi toohello. Tuttavia, la maggior parte dei comandi di hello supportano hello **- MessageOut percorso_file_registro** argomento facoltativo che reindirizza hello genera file di log tooa.

### <a name="environment-variable-configuring"></a>Configurazione della variabile di ambiente

Per l'esecuzione locale di U-SQL è necessaria una radice di dati specificata come account di archiviazione locale, oltre a un percorso CppSDK specificato per le dipendenze. È possibile sia argomento hello impostato nella variabile di ambiente della riga di comando o è impostata per loro.

- Set hello **SCOPE_CPP_SDK** variabile di ambiente.

    Se si ottengono con Microsoft Visual C++ e SDK di Windows hello installando Data Lake Tools per Visual Studio, verificare di aver hello seguente cartella:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Definire una nuova variabile di ambiente denominata **SCOPE_CPP_SDK** toopoint toothis directory. O copiare hello cartella toohello altro percorso e specificare **SCOPE_CPP_SDK** come che.

    Nella variabile di ambiente hello toosetting aggiunta, è possibile specificare hello **- CppSDK** argomento quando si utilizza la riga di comando hello. Questo argomento sovrascrive la variabile di ambiente CppSDK predefinita.

- Set hello **LOCALRUN_DATAROOT** variabile di ambiente.

    Definire una nuova variabile di ambiente denominata **LOCALRUN_DATAROOT** che punta toohello radice dei dati.

    Nella variabile di ambiente hello toosetting aggiunta, è possibile specificare hello **- DataRoot** argomento con il percorso dati radice hello quando si utilizza una riga di comando. Questo argomento sovrascrive la variabile di ambiente data-root predefinita. È necessario tooadd questa riga di comando tooevery argomento, che si esegue in modo che è possibile sovrascrivere una variabile di ambiente hello predefinita dati radice per tutte le operazioni.

### <a name="sdk-command-line-usage-samples"></a>Esempi di uso della riga di comando SDK

#### <a name="compile-and-run"></a>Compila ed esegui

Hello **eseguire** comando viene utilizzato toocompile hello script ed eseguire quindi i risultati compilati. Gli argomenti della riga di comando sono una combinazione degli argomenti di **compile** ed **execute**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

di seguito Hello sono argomenti facoltativi per **eseguire**:


|Argomento|Valore predefinito|Descrizione|
|--------|-------------|-----------|
|-CodeBehind|False|script Hello è CS code-behind|
|-CppSDK| |Directory CppSDK|
|-DataRoot| Variabile di ambiente DataRoot|DataRoot per l'esecuzione locale, predefinito troppo variabile di ambiente 'LOCALRUN_DATAROOT'|
|-MessageOut| |Messaggi di dump nel file di console tooa|
|-Parallel|1|Eseguire hello piano con hello specificato parallelism|
|-References| |Elenco di assembly di riferimento per i percorsi tooextra o file di dati di code-behind, separato da ';'|
|-UdoRedirect|False|Genera la configurazione di reindirizzamento di assembly Udo|
|-UseDatabase|master|Database toouse per code-behind di registrazione assembly temporaneo|
|-Verbose|False|Mostrare gli output dettagliati dal runtime|
|-WorkDir|Directory corrente|Directory per l'uso del compilatore e gli output|
|-RunScopeCEP|0|ScopeCEP modalità toouse|
|-ScopeCEPTempPath|temp|Toouse percorso temporaneo per il flusso di dati|
|-OptFlags| |Elenco delimitato da virgole con i flag di ottimizzazione|


Ad esempio:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Oltre a combinazione **compilare** e **eseguire**, è possibile compilare ed eseguire file eseguibili compilato hello separatamente.

#### <a name="compile-a-u-sql-script"></a>Compilare uno script U-SQL

Hello **compilare** comando è tooexecutables script utilizzati toocompile U-SQL.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

di seguito Hello sono argomenti facoltativi per **compilare**:


|Argomento|Descrizione|
|--------|-----------|
| -CodeBehind [valore predefinito 'False']|script Hello è CS code-behind|
| -CppSDK [valore predefinito '']|Directory CppSDK|
| -DataRoot [valore predefinito 'DataRoot environment variable']|DataRoot per l'esecuzione locale, predefinito troppo variabile di ambiente 'LOCALRUN_DATAROOT'|
| -MessageOut [valore predefinito '']|Messaggi di dump nel file di console tooa|
| -References [valore predefinito '']|Elenco di assembly di riferimento per i percorsi tooextra o file di dati di code-behind, separato da ';'|
| -Shallow [valore predefinito 'False']|Compilazione superficiale|
| -UdoRedirect [valore predefinito 'False']|Genera la configurazione di reindirizzamento di assembly Udo|
| -UseDatabase [valore predefinito 'master']|Database toouse per code-behind di registrazione assembly temporaneo|
| -WorkDir [valore predefinito 'Current Directory']|Directory per l'uso del compilatore e gli output|
| -RunScopeCEP [valore predefinito '0']|ScopeCEP modalità toouse|
| -ScopeCEPTempPath [valore predefinito 'temp']|Toouse percorso temporaneo per il flusso di dati|
| -OptFlags [valore predefinito '']|Elenco delimitato da virgole con i flag di ottimizzazione|


Di seguito sono riportati alcuni esempi d'uso.

Compilare uno script U-SQL:

    LocalRunHelper compile -Script d:\test\test1.usql

Compilare uno script U-SQL e impostare come cartella di dati radice hello. Si noti che ciò comporterà la sovrascrittura hello set variabile di ambiente.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Compilare uno script U-SQL e impostare la directory di lavoro, un assembly di riferimento e un database:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Eseguire i risultati compilati

Hello **eseguire** comando viene utilizzato tooexecute compilati risultati.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

di seguito Hello sono argomenti facoltativi per **eseguire**:

|Argomento|Descrizione|
|--------|-----------|
|-DataRoot [valore predefinito '']|Radice dei dati per l'esecuzione dei metadati. Il valore predefinito è toohello **LOCALRUN_DATAROOT** variabile di ambiente.|
|-MessageOut [valore predefinito '']|I messaggi nel file di tooa console hello di dump.|
|-Parallel [valore predefinito '1']|Indicatore toorun hello generato esecuzione locale con hello specificato il livello di parallelismo.|
|-Verbose [valore predefinito 'False']|Indicatore tooshow dettagliato restituisce dal runtime.|

Ecco un esempio d'uso:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Utilizzare hello SDK con interfacce di programmazione

interfacce di programmazione Hello si trovano in hello LocalRunHelper.exe. È possibile utilizzare le funzionalità di hello toointegrate di hello SDK U-SQL e hello tooscale framework di test c# test locale script U-SQL. In questo articolo, si utilizzerà hello standard c# unit test progetto tooshow come toouse queste interfacce tootest script U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Passaggio 1: Creare configurazione e progetto per unit test C#

- Creare un progetto per unit test C# tramite File > Nuovo > Progetto > Visual C# > Test > Progetto unit test.
- Aggiungere LocalRunHelper.exe come riferimento per il progetto hello. Hello LocalRunHelper.exe si trova in \build\runtime\LocalRunHelper.exe nel pacchetto Nuget.

    ![Riferimento aggiunta dell'SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- U-SQL SDK **solo** ambiente supporto x64, assicurarsi che tooset compilazione destinazione della piattaforma come x64. È possibile farlo da Proprietà progetto > Build > Piattaforma di destinazione.

    ![Progetto configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Verificare che tooset l'ambiente di test come x64. In Visual Studio è possibile impostarlo tramite Test > Impostazioni test > Architettura processore predefinita > x64.

    ![Ambiente di testing configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Verificare che toocopy tutti i file nella directory di lavoro tooproject NugetPackage\build\runtime\ che è in genere in ProjectFolder\bin\x64\Debug dipendenza.

### <a name="step-2-create-u-sql-script-test-case"></a>Passaggio 2: Creare test case per lo script U-SQL

Di seguito è riportato il codice di esempio hello per test di script U-SQL. Per i test, è necessario tooprepare script, file di input e output previsto.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Interfacce di programmazione in LocalRunHelper.exe

LocalRunHelper.exe fornisce interfacce di programmazione per compilazione locale U-SQL, eseguire hello, interfacce hello e così via sono elencate di seguito.

**Costruttore**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|.|Tipo|Descrizione|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|per i messaggi di output, impostare toonull toouse Console|

**Proprietà**

|Proprietà|Tipo|Descrizione|
|--------|----|-----------|
|AlgebraPath|string|file di Hello percorso tooalgebra (file algebra è uno dei risultati della compilazione hello)|
|CodeBehindReferences|string|Se script hello dispone di ulteriori code-behind riferimenti, specificare i percorsi di hello separati da ';'|
|CppSdkDir|string|Directory CppSDK|
|CurrentDir|string|La directory corrente|
|DataRoot|string|Il percorso della radice dei dati|
|DebuggerMailPath|string|Hello percorso toodebugger mailslot|
|GenerateUdoRedirect|bool|Se lo si desidera il caricamento degli assembly toogenerate reindirizzamento esegue l'override di configurazione|
|HasCodeBehind|bool|Se lo script hello è code-behind|
|InputDir|string|La directory per i dati di input|
|MessagePath|string|Il percorso del file dump del messaggio|
|OutputDir|string|La directory per i dati di output|
|Parallelismo|int|Algebra hello toorun di parallelismo|
|ParentPid|int|PID del padre hello in cui hello servizio controlla tooexit, set too0 o tooignore negativo|
|ResultPath|string|Il percorso del file dump del risultato|
|RuntimeDir|string|La directory di runtime|
|ScriptPath|string|Dove toofind hello script|
|Shallow|bool|Indica se la compilazione è superficiale o no|
|TempDir|string|Directory Temp|
|UseDataBase|string|Specificare hello database toouse per code-behind di registrazione di assembly temporaneo, master per impostazione predefinita|
|WorkDir|string|La directory di lavoro preferita|


**Metodo**

|Metodo|Descrizione|Return|.|
|------|-----------|------|---------|
|public bool DoCompile()|Compilare script di hello U-SQL|Se l'esito è positivo, restituisce il valore true| |
|public bool DoExec()|Esecuzione del risultato hello compilato|Se l'esito è positivo, restituisce il valore true| |
|public bool DoRun()|Eseguire script hello U-SQL (compilazione + Execute)|Se l'esito è positivo, restituisce il valore true| |
|public bool IsValidRuntimeDir(string path)|Verificare se un determinato percorso hello è il percorso di runtime valido|Se è valido, restituisce il valore true|percorso di Hello della directory di runtime|


## <a name="faq-about-common-issue"></a>Domande frequenti sui problemi comuni

### <a name="error-1"></a>Errore 1:
E_CSC_SYSTEM_INTERNAL: Internal error! Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies. modulo specificato Hello non trovato.

Verificare i seguenti hello:

- Assicurarsi di avere un ambiente x64. piattaforma di destinazione di compilazione Hello e ambiente di test hello deve essere x64, fare riferimento troppo**passaggio 1: c# creare unit test del progetto e la configurazione** sopra.
- Assicurarsi di che aver copiato tutti i file nella directory di lavoro tooproject NugetPackage\build\runtime\ dipendenza.


## <a name="next-steps"></a>Passaggi successivi

* toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).
* informazioni di diagnostica toolog, vedere [accesso ai log di diagnostica per Azure Data Lake Analitica](data-lake-analytics-diagnostic-logs.md).
* toosee una query più complessa, vedere [analizzare i log di sito Web usando Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).
* vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data Lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md).
* visualizzazione di esecuzione vertice hello toouse, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
