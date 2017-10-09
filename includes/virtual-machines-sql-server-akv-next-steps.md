## <a name="next-steps"></a>Passaggi successivi

Dopo aver attivato l'integrazione dell'insieme di credenziali delle chiavi di Azure, è possibile abilitare la crittografia di SQL Server nella macchina virtuale di SQL. In primo luogo, è necessario toocreate una chiave asimmetrica all'interno di credenziali delle chiavi e una chiave simmetrica in SQL Server nella VM. Quindi, sarà in grado di tooexecute T-SQL istruzioni tooenable della crittografia per il database e backup.

Esistono diversi tipi di crittografia di cui è possibile usufruire:

* [Transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Backup crittografati](https://msdn.microsoft.com/library/dn449489.aspx)
* [Crittografia a livello di colonna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Hello script Transact-SQL seguenti forniscono esempi per ognuna di queste aree.

### <a name="prerequisites-for-examples"></a>Prerequisiti per gli esempi

Ogni esempio è basato sui prerequisiti hello due: chiamata di una chiave asimmetrica dall'insieme di credenziali delle chiavi **CONTOSO_KEY** e le credenziali create dalla funzionalità di integrazione AKV hello chiamato **Azure_EKM_TDE_cred**. Hello comandi Transact-SQL seguenti questi prerequisiti per l'impostazione per l'esecuzione di esempi di hello.

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

### <a name="transparent-data-encryption-tde"></a>Transparent data encryption (TDE)

1. Creare un toobe di account di accesso di SQL Server utilizzata dal motore di Database hello per Transparent Data Encryption, quindi aggiungere tooit credenziali hello.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. Creare una chiave di crittografia database hello che verrà utilizzata per Transparent Data Encryption.

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a>Backup crittografati

1. Creare un toobe di account di accesso di SQL Server utilizzato dal motore di Database per la crittografia dei backup hello e aggiungere tooit credenziali hello.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. Database di backup hello specificando la crittografia con chiave asimmetrica di hello archiviata nell'insieme di credenziali chiave hello.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Crittografia a livello di colonna (CLE)

Questo script crea una chiave simmetrica protetta tramite la chiave asimmetrica nell'insieme di credenziali chiave hello hello e quindi utilizza i dati di hello tooencrypt chiave simmetrica nel database di hello.

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a>Risorse aggiuntive

Per ulteriori informazioni su come toouse queste funzionalità di crittografia, vedere [utilizzando EKM con le funzionalità di crittografia di SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Si noti che i passaggi di hello in questo articolo si presuppongono che si disponga già di SQL Server in esecuzione in una macchina virtuale di Azure. In caso contrario, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Per altre informazioni dettagliate sull'esecuzione di SQL Server nelle macchine virtuali di Azure, vedere [SQL Server nella panoramica delle macchine virtuali di Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
