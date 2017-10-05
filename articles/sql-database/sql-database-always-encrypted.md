---
title: 'Always Encrypted: database SQL di Azure - Archivio certificati di Windows | Documentazione Microsoft'
description: Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia del database usando la procedura guidata Always Encrypted di SQL Server Management Studio (SSMS). Descrive anche l'archiviazione delle chiavi di crittografia nell'archivio certificati di Windows.
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
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a>Crittografia sempre attiva: Proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia nell'archivio certificati di Windows

Questo articolo illustra come proteggere i dati sensibili in un database SQL con la crittografia del database tramite la [procedura guidata Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) di [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Descrive anche l'archiviazione delle chiavi di crittografia nell'archivio certificati di Windows.

La crittografia sempre attiva è una nuova tecnologia di crittografia dei dati del database SQL di Azure e di SQL Server, che protegge i dati sensibili inattivi sul server durante lo spostamento tra client e server e durante l'uso, assicurando che i dati sensibili non vengano mai visualizzati come testo non crittografato all'interno del sistema di database. Dopo avere crittografato i dati solo le applicazioni client o i server applicazioni, che hanno accesso alle chiavi, possono accedere ai dati di testo non crittografato. Per informazioni dettagliate, vedere l'articolo relativo alla [crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865.aspx).

Dopo avere configurato il database per usare la crittografia sempre attiva, viene creata un'applicazione client in C# con Visual Studio per lavorare con i dati crittografati.

Seguire i passaggi in questo articolo per imparare come configurare la crittografia sempre attiva per un database SQL di Azure. Questo articolo spiega come eseguire le attività seguenti:

* Usare la procedura guidata per la crittografia sempre attiva in SSMS per creare [chiavi con crittografia sempre attiva](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Creare una [chiave master di colonna (CMK, Column Master Key)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Creare una [chiave di crittografia di colonna (CEK, Column Encryption Key)](https://msdn.microsoft.com/library/mt146372.aspx).
* Creare una tabella di database e crittografare le colonne.
* Creare un'applicazione che inserisce, seleziona e visualizza i dati delle colonne crittografate.

## <a name="prerequisites"></a>Prerequisiti
Per questa esercitazione occorrono:

* Un account e una sottoscrizione di Azure. Nel caso in cui non siano disponibili, è possibile usare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versione 13.0.700.242 o successive.
* [.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o versioni successive (nel computer client).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)

## <a name="create-a-blank-sql-database"></a>Creare un database SQL vuoto
1. Accedere al [portale di Azure](https://portal.azure.com/).
2. Fare clic su **Nuovo** > **Dati e archiviazione** > **Database SQL**.
3. Creare un database **vuoto** denominato **Clinic** in un server nuovo o esistente. Per istruzioni dettagliate sulla creazione di un database nel portale di Azure, vedere [Primo database SQL di Azure](sql-database-get-started-portal.md).
   
    ![Creazione di un database vuoto](./media/sql-database-always-encrypted/create-database.png)

La stringa di connessione sarà necessaria più avanti nell'esercitazione. Dopo avere creato il database passare al nuovo database Clinic e copiare la stringa di connessione. È possibile ottenere la stringa di connessione in qualsiasi momento, ma è facile copiarla quando ci si trova nel portale di Azure.

1. Fare clic su **Database SQL** > **Clinic** > **Mostra stringhe di connessione del database**.
2. Copiare la stringa di connessione per **ADO.NET**.
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a>Connettersi al database con SSMS
Aprire SSMS e connettersi al server con il database Clinic.

1. Aprire SQL Server Management Studio. Fare clic su **Connetti** > **Motore di database** per aprire la finestra **Connetti al server**, se non è già aperta.
2. Immettere il nome e le credenziali del server. Il nome del server è disponibile nel pannello del database SQL e nella stringa di connessione copiata in precedenza. Digitare il nome completo del server, compreso *database.windows.net*.
   
    ![Copia della stringa di connessione](./media/sql-database-always-encrypted/ssms-connect.png)

Se viene visualizzata la finestra **Nuova regola firewall** , accedere ad Azure e lasciare che SSMS crei una nuova regola firewall per l'utente.

## <a name="create-a-table"></a>Creare una tabella
Questa sezione contiene istruzioni per creare una tabella con i dati dei pazienti. Sarà una normale tabella inizialmente; la crittografia verrà configurata nella sezione successiva.

1. Espandere **Database**.
2. Fare clic con il pulsante destro del mouse sul database **Clinic** e fare clic su **Nuova query**.
3. Incollare il comando Transact-SQL (T-SQL) seguente nella finestra della nuova query ed **eseguirlo** .

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
SSMS offre una procedura guidata per configurare facilmente la crittografia sempre attiva impostando la chiave master di colonna (CMK), la chiave di crittografia di colonna (CEK) e le colonne crittografate automaticamente.

1. Espandere **Database** > **Clinic** > **Tabelle**.
2. Fare clic con il pulsante destro del mouse sulla tabella **Patients** e selezionare **Crittografa colonne** per aprire la procedura guidata Always Encrypted:
   
    ![Crittografa colonne](./media/sql-database-always-encrypted/encrypt-columns.png)

La procedura guidata Always Encrypted include le sezioni seguenti: **Selezione colonne**, **Configurazione della chiave master** (CMK), **Convalida** e **Riepilogo**.

### <a name="column-selection"></a>Selezione colonne
Fare clic su **Avanti** nella pagina **Introduzione** per aprire la pagina **Selezione colonne**. In questa pagina verranno selezionate le colonne da crittografare, [il tipo di crittografia e la chiave di crittografia di colonna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) da usare.

Crittografare il **CF** e la **data di nascita** per ogni paziente. La colonna relativa al **CF** usa la crittografia deterministica, che supporta ricerche di uguaglianza, join e raggruppamenti. La colonna relativa alla **data di nascita** usa la crittografia casuale, che non supporta le operazioni.

Impostare il **Tipo di crittografia** per la colonna **CF** su **Deterministica** e la colonna **Data di nascita** su **Casuale**. Fare clic su **Avanti**.

![Crittografa colonne](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configurazione della chiave master
La pagina **Configurazione della chiave master** consente di impostare la CMK e selezionare il provider dell'archivio chiavi in cui verrà archiviata la CMK. Attualmente è possibile archiviare una chiave master di colonna nell'archivio certificati di Windows, nell'insieme di credenziali delle chiavi di Azure o in un modulo di protezione hardware. Questa esercitazione illustra come archiviare le chiavi nell'archivio certificati di Windows.

Verificare che l'**archivio certificati di Windows** sia selezionato e fare clic su **Avanti**.

![Configurazione della chiave master](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Convalida
È attualmente possibile crittografare le colonne o salvare uno script di PowerShell da eseguire in un secondo momento. Per questa esercitazione selezionare **Procedi per completare ora** e fare clic su **Avanti**.

### <a name="summary"></a>Riepilogo
Verificare che tutte le impostazioni siano corrette e fare clic su **Fine** per completare la configurazione della crittografia sempre attiva.

![Riepilogo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a>Confermare le azioni della procedura guidata
Al termine della procedura guidata, il database è configurato per la crittografia sempre attiva. La procedura guidata esegue le azioni seguenti:

* Creare una chiave CMK.
* Creare una chiave di crittografia di colonna (CEK).
* Configurazione delle colonne selezionate per la crittografia. La tabella **Patients** attualmente è vuota, ma eventuali dati esistenti nelle colonne selezionate sono ora crittografati.

È possibile verificare la creazione di chiavi in SSMS facendo clic su **Clinic** > **Sicurezza** > **Chiavi Always Encrypted**. Sono ora visibili le nuove chiavi generate dalla procedura guidata.

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a>Creare un'applicazione client che funziona con i dati crittografati
Ora che la crittografia Always Encrypted è configurata, è possibile creare un'applicazione che esegua alcuni *inserimenti* e *selezioni* nelle colonne crittografate. Per eseguire correttamente l'applicazione di esempio, è necessario avviarla nello stesso computer in cui è stata eseguita la procedura guidata per la crittografia sempre attiva. Per eseguire l'applicazione in un altro computer è necessario distribuire i certificati della crittografia sempre attiva nel computer che esegue l'applicazione client.  

> [!IMPORTANT]
> L'applicazione deve usare oggetti [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) per trasferire dati di testo non crittografato al server con colonne con la crittografia sempre attiva. Il trasferimento di valori letterali senza usare oggetti SqlParameter genererà un'eccezione.
> 
> 

1. Aprire Visual Studio e creare un'applicazione console C#. Verificare che il progetto sia impostato su **.NET Framework 4.6** o versione successiva.
2. Denominare il progetto **AlwaysEncryptedConsoleApp** e fare clic su **OK**.

![Nuova applicazione console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a>Modificare la stringa di connessione per abilitare la crittografia sempre attiva
Questa sezione descrive come abilitare la crittografia sempre attiva nella stringa di connessione del database. Si modificherà l'app console appena creata nella sezione successiva "Applicazione console di esempio della crittografia sempre attiva".

Per abilitare la crittografia Always Encrypted è necessario aggiungere la parola chiave **Column Encryption Setting** alla stringa di connessione e impostarla su **Enabled**.

È possibile impostarla direttamente nella stringa di connessione o tramite [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). L'applicazione di esempio nella sezione successiva mostra come usare **SqlConnectionStringBuilder**.

> [!NOTE]
> Questa è l'unica modifica specifica della crittografia sempre attiva da apportare a un'applicazione client. Se è presente un'applicazione esistente che archivia la stringa di connessione esternamente, ad esempio in un file di configurazione, è possibile abilitare la crittografia sempre attiva senza modificare il codice.
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a>Abilitare la crittografia sempre attiva nella stringa di connessione
Aggiungere la parola chiave seguente alla stringa di connessione:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Abilitare la crittografia sempre attiva con SqlConnectionStringBuilder
Il codice seguente mostra come abilitare la crittografia Always Encrypted tramite l'impostazione di [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) su [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Applicazione console di esempio della crittografia sempre attiva
Questo esempio dimostra come:

* Modificare la stringa di connessione per abilitare la crittografia sempre attiva.
* Inserire dati nelle colonne crittografate.
* Selezionare un record filtrando in base a un valore specifico in una colonna crittografata.

Sostituire il contenuto del file **Program.cs** con il codice seguente. Sostituire la stringa di connessione per la variabile globale connectionString nella riga immediatamente sopra il metodo Main con la stringa di connessione valida del portale di Azure. Questa è l'unica modifica che è necessario apportare al codice.

Eseguire l'app per vedere in azione la crittografia sempre attiva.

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
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

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
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
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

            Console.WriteLine("Press Enter to exit...");
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
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
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


        // This method simply deletes all records in the Patients table to reset our demo.
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


## <a name="verify-that-the-data-is-encrypted"></a>Verificare che i dati siano crittografati
È possibile verificare rapidamente che i dati effettivi nel server siano crittografati eseguendo una query dei dati della tabella **Patients** con SSMS. Usare la connessione corrente in cui l'impostazione di crittografia della colonna non è ancora abilitata.

Eseguire la query seguente nel database Clinic.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

È possibile osservare che le colonne crittografate non contengono dati di testo non crittografato.

   ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-encrypted.png)

Per usare SSMS per accedere ai dati di testo non crittografato, aggiungere il parametro **Column Encryption Setting=Enabled** alla connessione.

1. In SSMS fare clic con il pulsante destro del mouse sul server in **Esplora oggetti** e quindi fare clic su **Disconnetti**.
2. Fare clic su **Connetti** > **Motore di database** per aprire la finestra **Connetti al server** e quindi fare clic su **Opzioni**.
3. Fare clic su **Parametri aggiuntivi per la connessione** e digitare **Column Encryption Setting=Enabled**.
   
    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Eseguire la query seguente nel database **Clinic** .
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     È ora possibile visualizzare i dati non crittografati nelle colonne crittografate.

    ![Nuova applicazione console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Se ci si connette a SSMS (o a un client qualsiasi) da un altro computer, il computer non avrà accesso alle chiavi di crittografia e quindi non sarà in grado di decrittografare i dati.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Dopo avere creato un database che usa la crittografia sempre attiva, è possibile eseguire le operazioni seguenti:

* Eseguire questo esempio da un altro computer. Non avrà accesso alle chiavi di crittografia e quindi non avrà accesso ai dati non crittografati e non verrà eseguito correttamente.
* [Ruotare e pulire le chiavi](https://msdn.microsoft.com/library/mt607048.aspx).
* [Eseguire la migrazione dei dati già crittografati con la crittografia sempre attiva](https://msdn.microsoft.com/library/mt621539.aspx).
* [Distribuire certificati con crittografia Always Encrypted in altri computer client](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1). Vedere la sezione Rendere disponibili i certificati a utenti e applicazioni.

## <a name="related-information"></a>Informazioni correlate
* [Crittografia sempre attiva (sviluppo di client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx)
* [Crittografia di SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Procedura guidata della crittografia sempre attiva](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog della crittografia sempre attiva](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

