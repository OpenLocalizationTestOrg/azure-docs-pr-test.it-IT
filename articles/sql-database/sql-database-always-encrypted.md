---
title: 'Always Encrypted: database SQL di Azure - Archivio certificati di Windows | Documentazione Microsoft'
description: Questo articolo illustra come i dati sensibili in un database SQL con la crittografia del database tramite toosecure hello guidata su Always Encrypted in SQL Server Management Studio (SSMS). Viene inoltre visualizzato come toostore le chiavi di crittografia nel certificato di Windows hello archiviano.
keywords: crittografia dati, crittografia sql, crittografia database, dati sensibili, crittografia sempre attiva
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Always Encrypted: Proteggere i dati sensibili nel Database SQL e archiviare le chiavi di crittografia nell'archivio certificati di Windows hello

Questo articolo illustra come toosecure dati sensibili in un database SQL del database con la crittografia del database tramite hello [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Viene inoltre visualizzato come toostore le chiavi di crittografia nel certificato di Windows hello archiviano.

Always Encrypted è una nuova tecnologia di crittografia di dati in Database SQL di Azure e SQL Server che consente di proteggere i dati sensibili archiviati nel server di hello, durante lo spostamento tra il client e server, mentre i dati di hello sono in uso, garanzia che i dati sensibili non viene visualizzato come testo non crittografato hello sistema di database Dopo che i dati crittografati, solo le applicazioni client o server applicazioni che dispongono di chiavi di accesso toohello possibile accedere a dati in testo normale. Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).

Dopo aver configurato hello database toouse Always Encrypted, si creerà un'applicazione client in c# con Visual Studio toowork con dati crittografato hello.

Seguire i passaggi hello toolearn questo articolo come tooset di crittografia sempre attiva per un database SQL di Azure. In questo articolo si apprenderà come hello tooperform seguenti attività:

* Utilizzare guidata sempre crittografato hello in SSMS toocreate [le chiavi Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).
* Creare una tabella di database e crittografare le colonne.
* Creare un'applicazione che inserisce, seleziona e visualizza i dati dalle colonne crittografato hello.

## <a name="prerequisites"></a>Prerequisiti
Per questa esercitazione occorrono:

* Un account e una sottoscrizione di Azure. Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versione successiva (computer hello client).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)

## <a name="create-a-blank-sql-database"></a>Creare un database SQL vuoto
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **Nuovo** > **Dati e archiviazione** > **Database SQL**.
3. Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente. Per istruzioni dettagliate sulla creazione di un database in hello portale di Azure, vedere [di un database SQL di Azure](sql-database-get-started-portal.md).
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted/create-database.png)

Stringa di connessione hello sarà necessario più avanti nell'esercitazione di hello. Dopo aver creato il database di hello, andare toohello nuova Clinic database e la copia hello stringa di connessione. È possibile ottenere la stringa di connessione hello in qualsiasi momento, ma è facile toocopy quando si utilizza hello portale di Azure.

1. Fare clic su **Database SQL** > **Clinic** > **Mostra stringhe di connessione del database**.
2. Copiare la stringa di connessione hello per **ADO.NET**.
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>La connessione a database toohello con SQL Server Management Studio
Aprire SQL Server Management Studio e connettersi toohello server con database Clinic hello.

1. Aprire SQL Server Management Studio. (Fare clic su **Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra se non è aperto).
2. Immettere il nome e le credenziali del server. nome del server Hello sono disponibili nel Pannello di database SQL di hello e nella stringa di connessione hello copiato in precedenza. Tra cui nome completo del server di tipo hello *database.windows.net*.
   
    ![Copiare la stringa di connessione hello](./media/sql-database-always-encrypted/ssms-connect.png)

Se hello **nuova regola Firewall** viene visualizzata la finestra Accedi tooAzure e consentono di SQL Server Management Studio creare una nuova regola firewall per l'utente.

## <a name="create-a-table"></a>Creare una tabella
In questa sezione si creerà un pazienti toohold di tabella. Questo sarà una normale tabella, inizialmente si configurerà la crittografia nella sezione successiva hello.

1. Espandere **Database**.
2. Pulsante destro del mouse hello **Clinic** database e fare clic su **nuova Query**.
3. Hello Incolla seguente Transact-SQL (T-SQL) in nuova finestra query di hello e **Execute** è.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>Crittografare le colonne configurando la crittografia sempre attiva
SQL Server Management Studio include una procedura guidata tooeasily configurare Always Encrypted tramite la configurazione di hello CMK, CEK e le colonne crittografate automaticamente.

1. Espandere **Database** > **Clinic** > **Tabelle**.
2. Pulsante destro del mouse hello **pazienti** tabella e selezionare **crittografa colonne** guidata sempre crittografato hello di tooopen:
   
    ![Crittografa colonne](./media/sql-database-always-encrypted/encrypt-columns.png)

Creazione guidata sempre crittografato Hello include hello le sezioni seguenti: **selezione colonna**, **configurazione chiave Master** (CMK), **convalida**, e ** Riepilogo**.

### <a name="column-selection"></a>Selezione colonne
Fare clic su **Avanti** su hello **Introduzione** hello tooopen pagina **selezione colonna** pagina. In questa pagina, verranno selezionate le colonne desiderate tooencrypt, [hello tipo di crittografia e specificare la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Crittografare il **CF** e la **data di nascita** per ogni paziente. Hello **SSN** colonna verrà usata la crittografia deterministica, che supporta le ricerche di uguaglianza, join e group by. Hello **data di nascita** colonna utilizzerà la crittografia casuale, che non supporta le operazioni.

Set hello **tipo di crittografia** per hello **SSN** colonna troppo**deterministica** hello e **data di nascita** colonna troppo** Casuale**. Fare clic su **Avanti**.

![Crittografa colonne](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configurazione della chiave master
Hello **configurazione chiave Master** pagina è in cui impostare la CMK e provider dell'archivio chiavi hello selezionare dove hello CMK verranno archiviati. Attualmente, è possibile archiviare una chiave CMK nell'archivio certificati di Windows hello, insieme di credenziali chiave di Azure o un modulo di protezione hardware (HSM). Questa esercitazione illustra in che modo toostore le chiavi nel certificato di Windows hello archiviano.

Verificare che l'**archivio certificati di Windows** sia selezionato e fare clic su **Avanti**.

![Configurazione della chiave master](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Convalida
È possibile crittografare colonne hello ora o salvare un toorun di script di PowerShell in un secondo momento. Per questa esercitazione, selezionare **procedere ora toofinish** e fare clic su **Avanti**.

### <a name="summary"></a>Riepilogo
Verificare che le impostazioni di hello siano tutti corrette e fare clic su **fine** installazione hello toocomplete per Always Encrypted.

![Riepilogo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Verificare le azioni della procedura guidata di hello
Al termine procedura hello, il database è configurato per Always Encrypted. Hello hello di guidata eseguito le azioni seguenti:

* Creare una chiave CMK.
* Creare una chiave di crittografia di colonna (CEK).
* Hello configurato selezionate colonne per la crittografia. Il **pazienti** tabella non è attualmente disponibili dati, ma i dati esistenti nelle colonne selezionata hello ora sono crittografati.

È possibile verificare la creazione di hello delle chiavi di hello in SSMS passando troppo**Clinic** > **sicurezza** > **le chiavi Always Encrypted**. È ora possibile visualizzare hello le nuove chiavi hello generato automaticamente dalla procedura guidata.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Creare un'applicazione client che interagisce con i dati crittografato hello
Ora che Always Encrypted è configurato, è possibile compilare un'applicazione che esegue *inserisce* e *seleziona* su hello colonne crittografate. toosuccessfully eseguire hello applicazione di esempio, è necessario eseguirlo su hello stesso computer in cui è stato eseguito guidata sempre crittografato hello. un'applicazione hello toorun in un altro computer, è necessario distribuire Always Encrypted certificati toohello computer che esegue hello client app.  

> [!IMPORTANT]
> L'applicazione deve usare [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) oggetti quando si passa server toohello dati di testo normale con colonne con crittografia sempre attiva. Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.
> 
> 

1. Aprire Visual Studio e creare un'applicazione console C#. Verificare che il progetto è stato impostato troppo**.NET Framework 4.6** o versione successiva.
2. Progetto hello nome **AlwaysEncryptedConsoleApp** e fare clic su **OK**.

![Nuova applicazione console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modificare il tooenable di stringa di connessione Always Encrypted
Questa sezione viene illustrato come tooenable sempre crittografato nella stringa di connessione di database. Si modificherà l'applicazione console hello che appena creata nella sezione successiva di hello, "Always Encrypted applicazione console di esempio".

tooenable Always Encrypted, è necessario hello tooadd **Column Encryption Setting** connessione tooyour parola chiave di stringa e impostarlo troppo**abilitato**.

È possibile impostare questo valore direttamente nella stringa di connessione hello oppure è possibile impostarlo utilizzando un [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). applicazione di esempio Hello hello sezione successiva viene illustrato come toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Questo è unica modifica hello necessaria in un client applicazione specifico tooAlways crittografato. Se si dispone di un'applicazione esistente che archivia la stringa di connessione esternamente (ovvero, in un file di configurazione), potrebbe essere in grado di tooenable Always Encrypted senza modificare il codice.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Abilita sempre crittografato nella stringa di connessione hello
Aggiungere hello seguente stringa di connessione tooyour (parola chiave):

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder
Hello codice seguente viene illustrato come impostando tooenable sempre crittografato hello [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) troppo[abilitato](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Applicazione console di esempio della crittografia sempre attiva
Questo esempio dimostra come:

* Modificare il tooenable di stringa di connessione Always Encrypted.
* Inserire i dati in colonne crittografato hello.
* Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.

Sostituire il contenuto di hello di **Program.cs** con hello seguente codice. Sostituire la stringa di connessione hello per la variabile globale connectionString hello nella riga hello direttamente sopra hello metodo Main con la stringa di connessione valida da hello portale di Azure. Si tratta di modifica di hello solo se è necessario codice toothis toomake.

Eseguire hello app toosee Always Encrypted in azione.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a>Verificare che siano crittografati dati hello
È possibile controllare rapidamente che i dati effettivi di hello nel server di hello sono crittografati eseguendo una query hello **pazienti** dati con SQL Server Management Studio. (Utilizzare la connessione corrente in cui impostazione di crittografia di colonna hello non è ancora abilitato).

Eseguire hello seguente query sul database Clinic hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

È possibile vedere che le colonne crittografato hello non contengano i dati di testo normale.

   ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess hello dati in testo normale, è possibile aggiungere hello **Column Encryption Setting = abilitata** connessione toohello di parametro.

1. In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e quindi fare clic su **Disconnetti**.
2. Fare clic su **Connetti** > **motore di Database** tooopen hello **connettersi tooServer** finestra e quindi fare clic su **opzioni**.
3. Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Esecuzione hello query su hello riportata di seguito **Clinic** database.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     È ora possibile visualizzare dati in formato testo hello nelle colonne crittografato hello.

    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Se ci si connette a SQL Server Management Studio (o qualsiasi client) da un computer diverso, non avrà accesso toohello chiavi di crittografia e non sarà in grado di toodecrypt dati di hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un database che Usa crittografia sempre attiva, è necessario seguente hello toodo:

* Eseguire questo esempio da un altro computer. Non sarà possibile chiavi di crittografia toohello di accesso, in modo che non avrà accesso ai dati di testo normale toohello e non funzionerà correttamente.
* [Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).
* [Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).
* [Distribuire macchine di Always Encrypted certificati tooother client](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (vedere la sezione "Rendendo tooApplications disponibili i certificati e gli utenti" hello).

## <a name="related-information"></a>Informazioni correlate
* [Crittografia sempre attiva (sviluppo di client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx)
* [Crittografia di SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Procedura guidata della crittografia sempre attiva](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog della crittografia sempre attiva](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

