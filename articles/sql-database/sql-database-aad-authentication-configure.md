---
title: l'autenticazione di Azure Active Directory aaaConfigure - SQL | Documenti Microsoft
description: Informazioni su come tooconnect tooSQL Database e SQL Data Warehouse mediante autenticazione di Azure Active Directory.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configurare e gestire l'autenticazione di Azure Active Directory con il database SQL oppure con SQL Data Warehouse

In questo articolo illustra come toocreate popolare Azure AD e quindi utilizzare Azure AD con Database SQL di Azure e SQL Data Warehouse. Per una panoramica vedere [Autenticazione di Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Connessione tooSQL Server in esecuzione in una macchina virtuale di Azure non è supportato con un account Azure Active Directory. Usare un account Active Directory di dominio.

## <a name="create-and-populate-an-azure-ad"></a>Creare e popolare un'istanza di Azure AD
Creare un'istanza di Azure AD e popolarla con utenti e gruppi. Azure AD può essere hello dominio gestito di Azure Active Directory del dominio iniziale. Azure AD può essere anche un locale Active Directory Domain Services che è federata con Azure AD hello.

Per ulteriori informazioni, vedere [integrazione delle identità locali con Azure Active Directory](../active-directory/active-directory-aadconnect.md), [aggiungere la propria tooAzure nome di dominio Active Directory](../active-directory/active-directory-add-domain.md), [Microsoft Azure supporta ora la federazione con Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [amministrazione della directory di Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [gestire Azure AD tramite Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), e [identità ibride Porte e protocolli obbligatori](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Facoltativo: Associare o modificare hello active directory a cui è attualmente associato alla sottoscrizione di Azure
tooassociate il database con la directory hello Azure AD per l'organizzazione, creare directory hello una directory attendibile per database di hosting hello di hello sottoscrizione di Azure. Per altre informazioni, vedere [Associazione delle sottoscrizioni di Azure ad Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Altre informazioni:** ogni sottoscrizione di Azure ha una relazione di trust con un'istanza di Azure AD. Ciò significa che tale tooauthenticate directory considera attendibili gli utenti, servizi e dispositivi. Più sottoscrizioni possono considerare attendibile hello stessa directory, ma una sottoscrizione considera attendibile solo una directory. È possibile visualizzare la directory considerata attendibile dalla sottoscrizione nella hello **impostazioni** scheda in [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Questa relazione di trust che dispone di una sottoscrizione con una directory è diversa dalla relazione hello che dispone di una sottoscrizione con tutte le altre risorse in Azure (siti Web, database e così via), che sono piuttosto risorse figlio di una sottoscrizione. Arresta anche se una sottoscrizione scade, accesso toothose ad altre risorse associate alla sottoscrizione hello. Directory hello rimane in Azure, ma è possibile associare un'altra sottoscrizione a tale directory e continuare utenti toomanage hello. Per altre informazioni sulle risorse, vedere [Informazioni sull'accesso alle risorse di Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Hello procedure seguenti viene descritto come hello toochange associata directory per una sottoscrizione specificata.
1. Connettersi tooyour [portale di Azure classico](https://manage.windowsazure.com/) utilizzando un amministratore della sottoscrizione di Azure.
2. Nel banner sinistro hello, selezionare **impostazioni**.
3. Le sottoscrizioni vengono visualizzate nella schermata Impostazioni hello. Se lo si desidera hello sottoscrizione non viene visualizzata, fare clic su **sottoscrizioni** nella parte superiore di hello, elenco a discesa hello **filtro dalla DIRECTORY** casella selezionare hello directory che contiene le sottoscrizioni e quindi fare clic su **Applica**.
   
    ![selezionare la sottoscrizione][4]
4. In hello **impostazioni** area, fare clic sulla sottoscrizione e quindi fare clic su **modifica DIRECTORY** nella parte inferiore di hello della pagina hello.
   
    ![ad-settings-portal][5]
5. In hello **modifica DIRECTORY** selezionare hello Azure Active Directory a cui è associata a SQL Server o SQL Data Warehouse e quindi fare clic sulla freccia di hello per successivo.
   
    ![edit-directory-select][6]
6. In hello **conferma** directory finestra di dialogo Mapping, verificare che "**verranno rimossi tutti i coamministratori.**"
   
    ![edit-directory-confirm][7]
7. Fare clic su hello controllo tooreload hello portale.

   > [!NOTE]
   > Quando si modifica directory hello, i coamministratori tooall accesso, utenti di Azure AD e gruppi e gli utenti delle risorse di directory di backup vengono rimosse e non è più necessario l'accesso toothis sottoscrizione e le relative risorse. Solo per, come un amministratore del servizio, configurare l'accesso per le entità in base a una nuova directory hello. Questa modifica potrebbe impiegare una notevole quantità di risorse tooall toopropagate di tempo. Modifica della directory di hello, anche le modifiche hello amministratore di Azure AD per Database SQL e SQL Data Warehouse e impedire l'accesso al database per eventuali utenti di Azure AD esistenti. salve Azure AD deve essere reimpostazione (come descritto di seguito) e Azure nuovi utenti di Active Directory devono essere creati.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Creare un amministratore di Azure Active Directory per il server SQL di Azure
Ogni server SQL Azure (che ospita un Database SQL o SQL Data Warehouse) inizia con un account di amministratore di server singolo di messaggio per l'amministratore del server SQL Azure intera hello. È necessario creare un secondo amministratore del server SQL, cioè un account Azure AD. Questa entità viene creata come un utente del database contenuti nel database master hello. Come amministratori, account di amministratore di hello server sono membri di hello **db_owner** ruolo in tutti gli utenti del database e immettere ogni database utente come hello **dbo** utente. Per ulteriori informazioni sugli account amministratore di server hello, vedere [gestione di database e account di accesso nel Database SQL di Azure](sql-database-manage-logins.md).

Quando si usa Azure Active Directory con la replica geografica, amministratore di hello Azure Active Directory deve essere configurato per hello primario sia i server secondari hello. Se un server non dispone di un amministratore di Azure Active Directory, quindi gli utenti e account di accesso di Azure Active Directory errore "Impossibile connettersi" tooserver.

> [!NOTE]
> Gli utenti che non sono basati su un account di Azure AD (incluso l'account amministratore del server SQL Azure hello), non è possibile creare gli utenti basati su Active Directory di Azure, perché non hanno toovalidate autorizzazioni proposte gli utenti del database con hello Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Eseguire il provisioning di un amministratore di Azure Active Directory per Azure SQL Server

Hello due procedure seguenti illustrano come tooprovision un amministratore di Azure Active Directory per il server SQL Azure nel portale di Azure hello e tramite PowerShell.

### <a name="azure-portal"></a>Portale di Azure
1. In hello [portale di Azure](https://portal.azure.com/)in hello angolo superiore destro, fare clic su toodrop la connessione di visualizzare un elenco di possibili Active Directory. Scegliere hello correggere Active Directory come valore predefinito di hello Azure AD. Questo passaggio collegamenti hello associazione sottoscrizione con Active Directory con il server SQL Azure assicurandosi che hello stessa sottoscrizione utilizzata sia per Azure AD e SQL Server. (hello Azure SQL server può essere che ospita il Database di SQL Azure o Azure SQL Data Warehouse.)   
    ![choose-ad][8]   
    
2. In hello a sinistra selezionare banner **istanze di SQL Server**, selezionare il **SQL server**e quindi in hello **SQL Server** pannello, fare clic su **amministratore di Active Directory**.   
3. In hello **amministratore di Active Directory** pannello, fare clic su **impostare l'amministratore di**.   
    ![Selezionare Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. In hello **aggiungere admin** pannello, cercare un utente, utente di selezionare hello o un gruppo toobe, un amministratore e quindi fare clic su **selezionare**. (il pannello di amministrazione di Active Directory hello Visualizza tutti i membri e i gruppi di Active Directory. Gli utenti e i gruppi non disponibili (in grigio) non possono essere selezionati, perché non sono supportati come amministratori di Azure AD. (Vedere hello elenco di amministratori supportati in hello **le funzionalità di Azure Active Directory e le limitazioni** sezione [utilizzare Azure Active Directory l'autenticazione per l'autenticazione con il Database SQL o SQL Data Warehouse](sql-database-aad-authentication.md).) Controllo di accesso basato sui ruoli (RBAC) si applica solo a toohello portal e non viene propagato tooSQL Server.   
    ![Selezionare l'amministratore](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Nella parte superiore di hello di hello **amministratore di Active Directory** pannello, fare clic su **salvare**.   
    ![Salvare l'impostazione dell'amministratore](./media/sql-database-aad-authentication/save-admin.png)   

il processo di Hello di modifica di messaggio per l'amministratore potrebbe richiedere alcuni minuti. Quindi viene visualizzato di nuovo amministratore hello in hello **amministratore di Active Directory** casella.

   > [!NOTE]
   > Quando si configura Azure AD salve, hello nuovo nome amministratore (utente o gruppo) non può essere già presente nel database master virtuale hello come un utente di autenticazione di SQL Server. Se presente, l'installazione di amministrazione di Azure AD hello avrà esito negativo; la creazione di rollback e che indica che tale amministratore (nome) già esiste. Poiché tali un utente di autenticazione di SQL Server non fa parte di hello Azure AD, impegno tooconnect toohello server utilizzando l'autenticazione di Azure AD ha esito negativo.
   > 


toolater rimuovere un amministratore, nella parte superiore di hello di hello **amministratore di Active Directory** pannello, fare clic su **rimuovere admin**, quindi fare clic su **salvare**.

### <a name="powershell"></a>PowerShell
toorun i cmdlet di PowerShell, è necessario toohave Azure PowerShell installato e in esecuzione. Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

un amministratore di Azure AD, tooprovision eseguire hello seguenti comandi PowerShell di Azure:

* Add-AzureRmAccount
* Select-AzureRmSubscription

I cmdlet utilizzati tooprovision e gestire l'amministrazione di Azure AD:

| Nome del cmdlet | Descrizione |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Esegue il provisioning di un amministratore di Azure Active Directory per il server di Azure SQL o per Azure SQL Data Warehouse. (Deve essere dalla sottoscrizione corrente hello). |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Rimuove un amministratore di Azure Active Directory per il server di Azure SQL o per Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Restituisce informazioni relative a un amministratore di Azure Active Directory attualmente configurata per il server di SQL Azure hello o Azure SQL Data Warehouse. |

Utilizzare PowerShell comando get-help toosee ulteriori informazioni, vedere per ognuno di questi comandi, ad esempio ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Hello dopo il provisioning di uno script denominato di un gruppo di amministratori di Azure AD **DBA_Group** (id di oggetto `40b79501-b343-44ed-9ce7-da4c8cc7353f`) per hello **demo_server** server in un gruppo di risorse denominato **gruppo 23** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Hello **DisplayName** parametro di input accetta nome visualizzato hello Azure AD o hello Nome entità utente. Ad esempio, ``DisplayName="John Smith"`` e ``DisplayName="johns@contoso.com"``. Per hello solo gruppi di Azure AD Azure AD nome visualizzato è supportato.

> [!NOTE]
> comando di Azure PowerShell Hello ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` impedirà di provisioning gli amministratori di Azure AD per gli utenti non supportati. Un utente non supportato può eseguire il provisioning, ma non è stato possibile connettersi tooa database. 
> 

esempio Hello utilizza hello facoltativo **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Hello Azure AD **ObjectID** è obbligatorio quando hello **DisplayName** non è univoco. hello tooretrieve **ObjectID** e **DisplayName** valori, utilizzare sezione Active Directory hello Classic del portale di Azure e visualizzare le proprietà di hello di un utente o gruppo.
> 

Hello di esempio seguente restituisce informazioni sui salve corrente AD Azure per server SQL di Azure:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Hello di esempio seguente rimuove un amministratore di Azure AD:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Tramite le API REST di hello, è possibile fornire anche un amministratore di Azure Active Directory. Per altre informazioni [informazioni di riferimento sull'API REST di gestione dei servizi e le operazioni per i database SQL di Azure](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
Si può anche effettuare il provisioning di un amministratore di Azure AD hello chiamante seguendo i comandi CLI:
| Comando | Descrizione |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Esegue il provisioning di un amministratore di Azure Active Directory per il server di Azure SQL o per Azure SQL Data Warehouse. (Deve essere dalla sottoscrizione corrente hello). |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Rimuove un amministratore di Azure Active Directory per il server di Azure SQL o per Azure SQL Data Warehouse. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Restituisce informazioni relative a un amministratore di Azure Active Directory attualmente configurata per il server di SQL Azure hello o Azure SQL Data Warehouse. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Aggiorna l'amministratore di Active Directory hello per un server SQL di Azure o Azure SQL Data Warehouse. |

Per altre informazioni sui comandi dell'interfaccia della riga di comando, vedere [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Configurare i computer client
In tutti i computer client, da cui le applicazioni o gli utenti connetteranno tooAzure Database SQL o utilizzando l'identità di Azure AD, Azure SQL Data Warehouse è necessario installare hello seguente software:

* .NET Framework 4.6 o versione successiva dalla pagina [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Azure Active Directory Authentication Library per SQL Server (**ADALSQL. DLL**) è disponibile in più lingue (x86 e amd64) dall'area download hello in [Microsoft Active Directory Authentication Library per Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

È possibile soddisfare questi requisiti tramite:

* L'installazione di uno [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) o [SQL Server Data Tools per Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) hello di soddisfa il requisito di .NET Framework 4.6.
* SQL Server Management Studio installa la versione di hello x86 di **ADALSQL. DLL**.
* SSDT installa la versione di hello amd64 di **ADALSQL. DLL**.
* Hello più recente di Visual Studio da [download di Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) soddisfa i requisiti di .NET Framework 4.6 hello, ma non installa versione amd64 obbligatorio hello di **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Creare utenti del database indipendente in tooAzure del database eseguito il mapping delle identità di Active Directory

L'autenticazione di Azure Active Directory richiede toobe agli utenti di database creato come utenti del database indipendente. Un utente del database indipendente in base a un'identità di Azure AD, è un utente del database che non dispone di un account di accesso nel database master hello e identità tooan mappe in hello directory di Azure AD associata al database hello. Hello Azure AD identity può essere un singolo account utente o un gruppo. Per altre informazioni sugli utenti di database indipendente, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Gli utenti del database (con eccezione hello degli amministratori) non possono essere creati usando portale. Ruoli RBAC non vengono propagati tooSQL Server, Database SQL o SQL Data Warehouse. I ruoli Azure RBAC vengono utilizzati per la gestione delle risorse di Azure e non si applicano autorizzazioni toodatabase. Ad esempio, hello **collaboratore di SQL Server** ruolo non consente l'accesso tooconnect toohello Database SQL o SQL Data Warehouse. deve disporre dell'autorizzazione di accesso Hello direttamente nel database di hello utilizzando istruzioni Transact-SQL.
>

un utente di Azure database contenuto basato su Active Directory (ad eccezione di hello amministratore del server cui appartiene il database di hello), la connessione database toohello con un'identità di Azure AD, come utente con toocreate almeno hello **ALTER ANY USER** autorizzazione. Utilizzare quindi hello sintassi Transact-SQL seguente:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* può essere hello nome principale di un nome di visualizzazione utente o hello Azure Active Directory per un gruppo di Azure AD.

**Esempi:** toocreate un utente del database indipendente che rappresenta un annuncio di Azure federati o gestiti utente di dominio:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate un utente del database indipendente che rappresenta un annuncio di Azure o federata gruppo di dominio, fornire il nome visualizzato hello di un gruppo di sicurezza:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate un utente del database indipendente che rappresenta un'applicazione che si connette utilizzando un token di Azure AD:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  È possibile creare un utente direttamente da Azure Active Directory diverso da hello Azure Active Directory associato alla sottoscrizione di Azure. Tuttavia, i membri di altre directory di Active Directory che sono gli utenti importati in hello associata Active Directory, denominata anche utenti esterni, è possibile aggiungere il gruppo di Active Directory tooan nel tenant di hello Active Directory. Tramite la creazione di un utente del database indipendente per tale gruppo di Active Directory, hello gli utenti da hello esterno di Active Directory possono ottenere accesso tooSQL Database.   

Per altre informazioni sulla creazione di utenti di database indipendente basati su identità di Azure Active Directory, vedere [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Amministratore di Azure Active Directory hello rimozione per il server SQL Azure impedisce la connessione server toohello qualsiasi utente di autenticazione di Azure AD. Se necessario, un amministratore del database SQL può eliminare manualmente gli utenti di Azure AD inutilizzabili.   

>  [!NOTE]
>  Se si riceve un **connessione Timeout scaduto**, potrebbe essere necessario hello tooset `TransparentNetworkIPResolution` parametro di toofalse di stringa di connessione hello. Per altre informazioni, vedere [Connection timeout issue with .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/) (Problema di timeout della connessione con .NET Framework 4.6.1 - TransparentNetworkIPResolution).   

   
Quando si crea un utente del database, che l'utente riceve hello **CONNETTI** autorizzazione e possono connettersi al database toothat come membro di hello **pubblica** ruolo. Inizialmente hello solo le autorizzazioni utente toohello disponibili sono le autorizzazioni concesse toohello **pubblica** ruolo o le autorizzazioni concesse tooany gruppi di Windows che sono membri di. Una volta si esegue il provisioning di un utente del database contenuti in base AD Azure, è possibile concedere autorizzazioni aggiuntive hello, hello stesso quando si concede l'autorizzazione tooany altro tipo di utente. In genere concedere le autorizzazioni dei ruoli toodatabase e aggiungere gli utenti tooroles. Per altre informazioni, vedere l'articolo relativo alle [nozioni di base delle autorizzazioni per il motore di database](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Per altre informazioni sui ruoli speciali del database SQL, vedere [Gestione di database e account di accesso nel database SQL di Azure](sql-database-manage-logins.md).
Un utente di dominio federato che verrà importato in un dominio di gestione, è necessario utilizzare l'identità del dominio hello gestito.

> [!NOTE]
> Agli utenti di Azure AD sono contrassegnati nei metadati di database hello al tipo E (EXTERNAL_USER) e per i gruppi con tipo X (EXTERNAL_GROUPS). Per altre informazioni, vedere [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Connettersi toohello utente database o data warehouse con SQL Server Management Studio o SSDT  
tooconfirm messaggio Azure AD per l'amministratore sia configurato correttamente, connettersi toohello **master** database utilizzando l'account amministratore hello Azure AD.
un utente di Azure database contenuto basato su Active Directory (ad eccezione di hello l'amministratore del server cui appartiene il database di hello) tooprovision connettersi toohello database con un'identità di Azure AD con database di access toohello.

> [!IMPORTANT]
> Il supporto per l'autenticazione di Azure Active Directory è disponibile con [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015. Hello versione di agosto 2016 di SQL Server Management Studio include anche il supporto per l'autenticazione universale di Active Directory, che consente agli amministratori toorequire multi-Factor Authentication con una chiamata telefonica, SMS, smart card, pin o la notifica dell'app mobile.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Utilizzando un tooconnect di identità di Azure AD utilizzando SQL Server Management Studio o SSDT  

Hello, seguire le procedure seguenti viene illustrato come tooconnect tooa SQL database con un'identità di Azure AD utilizzando SQL Server Management Studio o gli strumenti di Database di SQL Server.

### <a name="active-directory-integrated-authentication"></a>Autenticazione integrata di Active Directory

Utilizzare questo metodo se si è connessi in tooWindows utilizzando le credenziali di Azure Active Directory da un dominio federato.

1. Avviare Management Studio o gli strumenti di dati e in hello **connettersi tooServer** (o **connettersi tooDatabase motore**) della finestra di dialogo hello **autenticazione** selezionare **Integrata in active Directory -**. Password non è necessaria o può essere immesso perché le credenziali esistenti verranno presentate per la connessione hello.   

    ![Selezionare Autenticazione integrata di Active Directory][11]
2. Fare clic su hello **opzioni** pulsante e hello **le proprietà di connessione** hello della pagina **connettersi toodatabase** casella, il nome del tipo hello del database utente hello desiderato tooconnect A. (hello **ID tenant o nome di dominio Active Directory**"opzione è supportata solo per **Universal con connessione di autenticazione a più fattori** opzioni, in caso contrario è disponibile.)  

    ![Selezionare il nome di database hello][13]

## <a name="active-directory-password-authentication"></a>Autenticazione della password di Active Directory

Utilizzare questo metodo quando la connessione con un nome dell'entità di Azure AD mediante Azure AD hello gestito dominio. È possibile inoltre utilizzare per l'account federato senza dominio toohello di accesso, ad esempio quando si lavora in remoto.

Utilizzare questo metodo se si è connessi tooWindows utilizzando le credenziali da un dominio che non è federato con Azure o quando si utilizza l'autenticazione di Azure AD usando Azure Active Directory in base a hello iniziale o hello dominio client.

1. Avviare Management Studio o gli strumenti di dati e in hello **connettersi tooServer** (o **connettersi tooDatabase motore**) della finestra di dialogo hello **autenticazione** selezionare **Active Directory - Password**.
2. In hello **nome utente** , digitare il nome utente di Azure Active Directory in formato hello  **username@domain.com** . Deve trattarsi di un account da hello Azure Active Directory o un account da un dominio la federazione con hello Azure Active Directory.
3. In hello **Password** , digitare la password dell'utente per conto di hello Azure Active Directory o account di dominio federato.

    ![Selezionare Autenticazione della password di Active Directory][12]
4. Fare clic su hello **opzioni** pulsante e hello **le proprietà di connessione** hello della pagina **connettersi toodatabase** casella, il nome del tipo hello del database utente hello desiderato tooconnect A. (Vedere l'immagine di hello nell'opzione precedente hello).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Utilizzando un tooconnect di identità di Azure AD da un'applicazione client

Hello, seguire le procedure seguenti viene illustrato come tooconnect tooa SQL database con un'identità di Azure AD da un'applicazione client.

###  <a name="active-directory-integrated-authentication"></a>Autenticazione integrata di Active Directory

toouse autenticazione integrata di Windows, Active Directory del dominio deve essere federato con Azure Active Directory. L'applicazione client (o un servizio) connessione database toohello deve essere in esecuzione in un computer aggiunto al dominio con credenziali di dominio dell'utente.

tooconnect tooa database utilizzando integrato l'autenticazione e identità di Azure AD, è necessario impostare la parola chiave autenticazione hello nella stringa di connessione database hello tooActive Directory integrata. Hello seguente esempio di codice c# utilizza ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

parola chiave di stringa di connessione Hello ``Integrated Security=True`` non è supportato per la connessione tooAzure Database SQL. Quando si effettua una connessione ODBC, sarà anche necessario tooremove spazi e impostare l'autenticazione too'ActiveDirectoryIntegrated'.

### <a name="active-directory-password-authentication"></a>Autenticazione della password di Active Directory

tooconnect tooa database utilizzando integrato l'autenticazione e identità di Azure AD, è necessario impostare parola chiave di autenticazione hello tooActive la Password della Directory. stringa di connessione Hello deve contenere ID utente/UID e parole chiave Password o PWD e valori. Hello seguente esempio di codice c# utilizza ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Altre informazioni sui metodi di autenticazione di Azure AD usando hello demo codici di esempio disponibile all'indirizzo [Demo di Azure Active Directory l'autenticazione di GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Token Azure AD
Questo metodo di autenticazione consente a servizi di livello intermedio tooconnect tooAzure Database SQL o Azure SQL Data Warehouse ottenendo un token da Azure Active Directory (AAD). Consente scenari complessi, tra cui l'autenticazione basata su certificato. È necessario eseguire quattro passaggi di base toouse token autenticazione di Azure AD:

1. Registrare l'applicazione con Azure Active Directory e ottenere l'id client hello per il codice. 
2. Creare una database utente che rappresenta un'applicazione hello. (Completato in precedenza al passaggio 6).
3. Creare un certificato nel computer client di hello esegue un'applicazione hello.
4. Aggiungere il certificato di hello come chiave per l'applicazione.

Stringa di connessione di esempio:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Per altre informazioni, vedere [SQL Server Security Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)(Blog sulla sicurezza del server SQL).

### <a name="sqlcmd"></a>sqlcmd

Hello seguendo le istruzioni, connettersi utilizzando la versione 13.1 di sqlcmd, è disponibile da hello [area Download](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Passaggi successivi
- Per una panoramica dell'accesso e del controllo nel database SQL, vedere l'articolo relativo al [controllo dell'accesso al database SQL](sql-database-control-access.md).
- Per una panoramica degli account di accesso, degli utenti e dei ruoli del database nel database SQL, vedere l'articolo relativo ad [account di accesso, utenti e ruoli del database](sql-database-manage-logins.md).
- Per altre informazioni sulle entità di database, vedere [Entità](https://msdn.microsoft.com/library/ms181127.aspx).
- Per altre informazioni sui ruoli del database, vedere [Ruoli a livello di database](https://msdn.microsoft.com/library/ms189121.aspx).
- Per informazioni generali sulle regole del firewall, vedere l'articolo relativo alle [regole del firewall per il database SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

