---
title: passaggio aaaGeneric passo-passo connettore SQL | Documenti Microsoft
description: In questo articolo si verifica attraverso un semplice sistema HR utilizzando dettagliate hello connettore SQL generico.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Procedura dettagliata per la creazione del connettore Generic SQL
Questo argomento è una guida dettagliata. Verrà creato un semplice database delle risorse umane di esempio che sarà usato per importare alcuni utenti con la relativa appartenenza ai gruppi.

## <a name="prepare-hello-sample-database"></a>Preparare i database di esempio hello
In un server che esegue SQL Server, eseguire script SQL hello trovato nel [appendice](#appendix-a). Questo script crea un database di esempio con il nome di hello GSQLDEMO. modello a oggetti Hello per hello creati database simile a questa immagine:  
![Modello a oggetti](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Creare anche un utente a cui si desidera toouse tooconnect toohello database. In questa procedura dettagliata, utente hello viene chiamato FABRIKAM\SQLUser e si trova nel dominio hello.

## <a name="create-hello-odbc-connection-file"></a>Creare file di connessione ODBC hello
Hello connettore SQL generico utilizza ODBC tooconnect toohello remote server. È prima necessario toocreate un file con informazioni di connessione ODBC hello.

1. Avviare l'utilità di gestione di hello ODBC nel server:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Scheda selezionare hello **DSN su File**. Fare clic su **Aggiungi**.  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Hello out-of-box driver works costituisce, pertanto selezionarlo e fare clic su **successivo >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Assegnare, ad esempio, un nome file hello **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Fare clic su **Finish**(Fine).  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Connessione di hello tooconfigure Time. Origine dati hello viene fornita una descrizione valida e specificare il nome di hello del server di hello che esegue SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Selezionare come tooauthenticate con SQL. In questo caso si userà l'autenticazione di Windows.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Specificare il nome di hello hello del database di esempio, **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. In questa schermata mantenere tutte le selezioni predefinite. Fare clic su **Finish**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify funzionino come previsto, fare clic su **origine dati di Test**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Verificare che hello test ha esito positivo.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. file di configurazione ODBC Hello dovrebbe ora essere visibile nel DSN su File.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

È ora disponibile il file di hello è necessaria e iniziare a creare hello connettore.

## <a name="create-hello-generic-sql-connector"></a>Creare hello connettore SQL generico
1. In hello UI Synchronization Service Manager, selezionare **connettori** e **crea**. Selezionare **Generic SQL (Microsoft)** e assegnargli un nome descrittivo.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Trovare il file DSN hello creato nella sezione precedente hello e caricarlo toohello server. Fornire hello credenziali tooconnect toohello database.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. In questa procedura dettagliata si considera un caso semplificato in cui esistono due tipi di oggetti, **User** e **Group**.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. gli attributi di hello toofind, si vuole hello connettore toodetect tali attributi esaminando tabella hello stessa. Poiché **utenti** è una parola riservata in SQL, è necessario tooprovide in quadrato parentesi quadre [].  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Attributo di ancoraggio ora toodefine hello e attributo DN hello. Per **utenti**, utilizziamo combinazione hello di hello due attributi username ed EmployeeID. Per **Group**si usa GroupName, non molto plausibile in un caso reale, ma adeguato per questa procedura dettagliata.
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Non tutti i tipi di attributo possono essere rilevati in un database SQL. in particolare, non è tipo di attributo di riferimento Hello. Per il tipo di oggetto gruppo hello, dobbiamo toochange hello OwnerID e tooreference MemberID.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. gli attributi di Hello è selezionato come attributi di riferimento nel passaggio precedente hello richiedono questi valori sono un riferimento al tipo di oggetto di hello. In questo caso, hello il tipo di oggetto utente.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Nella pagina parametri globali hello selezionare **filigrana** come strategia di hello delta. Anche digitare nel formato di data/ora hello **AAAA-MM-gg hh: mm:**.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. In hello **Configura partizioni e gerarchie** pagina, selezionare entrambi i tipi di oggetto.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. In hello **Seleziona tipi di oggetti** e **selezione attributi**, selezionare i tipi di oggetto e tutti gli attributi. In hello **configurare Anchor** pagina, fare clic su **fine**.

## <a name="create-run-profiles"></a>Creare i profili di esecuzione
1. In hello UI Synchronization Service Manager, selezionare **connettori**, e **Configure Run Profiles**. Fare clic su **New Profile**(Nuovo profilo). Si inizierà con **Full Import**(Importazione completa).  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Selezionare il tipo di hello **importazione completa (solo fase)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Selezionare la partizione hello **oggetto = utente**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Selezionare **Table** (Tabella) e digitare **[USERS]**. Scorrere verso il basso sezione tipo di oggetto multivalore toohello e immettere dati hello come hello seguente immagine. Selezionare **fine** passaggio hello toosave.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Selezionare **New Step**(Nuovo passaggio). Questa volta selezionare **OBJECT=Group**. Hello ultima pagina, utilizzare configurazione hello come hello seguente immagine. Fare clic su **Finish**.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Facoltativo: se si vuole, è possibile configurare altri profili di esecuzione. Per questa procedura dettagliata viene utilizzato solo hello importazione completa.
7. Fare clic su **OK** toofinish la modifica di profili di esecuzione.

## <a name="add-some-test-data-and-test-hello-import"></a>Aggiungere alcuni importazione hello test e i dati di test
Immettere alcuni dati di prova nel database di esempio. Quando si è pronti, selezionare **Run** (Esegui) e **Full import** (Importazione completa).

In questo esempio si ottiene un utente con due numeri di telefono e un gruppo con alcuni membri.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Appendice A
**Database di esempio hello toocreate script SQL**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
