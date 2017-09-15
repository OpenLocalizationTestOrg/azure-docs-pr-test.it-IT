## <a name="next-steps"></a><span data-ttu-id="a9e9f-101">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9e9f-101">Next steps</span></span>

<span data-ttu-id="a9e9f-102">Dopo aver attivato l'integrazione dell'insieme di credenziali delle chiavi di Azure, è possibile abilitare la crittografia di SQL Server nella macchina virtuale di SQL.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="a9e9f-103">Innanzitutto, è necessario creare una chiave asimmetrica nell'insieme di credenziali delle chiavi e una chiave simmetrica in SQL Server nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="a9e9f-104">A questo punto, sarà possibile eseguire istruzioni T-SQL per abilitare la crittografia per i database e i backup.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="a9e9f-105">Esistono diversi tipi di crittografia di cui è possibile usufruire:</span><span class="sxs-lookup"><span data-stu-id="a9e9f-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="a9e9f-106">Transparent data encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="a9e9f-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="a9e9f-107">Backup crittografati</span><span class="sxs-lookup"><span data-stu-id="a9e9f-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="a9e9f-108">Crittografia a livello di colonna (CLE)</span><span class="sxs-lookup"><span data-stu-id="a9e9f-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="a9e9f-109">Gli script Transact-SQL seguenti forniscono esempi per ognuna di queste aree.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="a9e9f-110">Prerequisiti per gli esempi</span><span class="sxs-lookup"><span data-stu-id="a9e9f-110">Prerequisites for examples</span></span>

<span data-ttu-id="a9e9f-111">Ogni esempio è basato su due prerequisiti: una chiave asimmetrica dall'insieme di credenziali delle chiavi denominata **CONTOSO_KEY** e una credenziale creata dalla funzionalità di integrazione di AKV denominata **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="a9e9f-112">I comandi Transact-SQL seguenti consentono di configurare questi prerequisiti per l'esecuzione degli esempi.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="a9e9f-113">Transparent data encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="a9e9f-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="a9e9f-114">Creare un account di accesso di SQL Server che può essere usato dal motore di database per la TDE, quindi aggiungere la credenziale.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="a9e9f-115">Creare la chiave di crittografia del database che verrà usata per la TDE.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="a9e9f-116">Backup crittografati</span><span class="sxs-lookup"><span data-stu-id="a9e9f-116">Encrypted backups</span></span>

1. <span data-ttu-id="a9e9f-117">Creare un account di accesso di SQL Server che può essere usato dal motore di database per la crittografia dei backup, quindi aggiungere la credenziale.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="a9e9f-118">Eseguire il backup del database specificando la crittografia con la chiave asimmetrica archiviata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="a9e9f-119">Crittografia a livello di colonna (CLE)</span><span class="sxs-lookup"><span data-stu-id="a9e9f-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="a9e9f-120">Questo script crea una chiave simmetrica protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi e quindi usa la chiave simmetrica per crittografare i dati nel database.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="a9e9f-121">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a9e9f-121">Additional resources</span></span>

<span data-ttu-id="a9e9f-122">Per altre informazioni su come usare queste funzionalità di crittografia, vedere l'argomento relativo all' [uso di EKM con le funzionalità di crittografia di SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="a9e9f-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="a9e9f-123">Si noti che i passaggi in questo articolo presuppongono che si disponga già di SQL Server in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e9f-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="a9e9f-124">In caso contrario, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a9e9f-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="a9e9f-125">Per altre informazioni dettagliate sull'esecuzione di SQL Server nelle macchine virtuali di Azure, vedere [SQL Server nella panoramica delle macchine virtuali di Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9e9f-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>