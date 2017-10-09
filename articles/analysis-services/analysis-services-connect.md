---
title: aaaConnect tooAzure Analysis Services | Documenti Microsoft
description: Informazioni su come tooconnect tooand ottenere dati da un server Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Connettere il server di Azure Analysis Services tooan

Questo articolo descrive la connessione server tooa tramite la modellazione dei dati e applicazioni di gestione come SQL Server Management Studio (SSMS) o SQL Server Data Tools (SSDT). In alternativa, con applicazioni reporting client come Microsoft Excel, Power BI Desktop o applicazioni personalizzate. Connessioni tooAzure Analysis Services utilizzano HTTPS.

## <a name="client-libraries"></a>Librerie client
[Recuperare le librerie Client più recente di hello](analysis-services-data-providers.md)

Tutti i server tooa connessioni, indipendentemente dal tipo, richiedono aggiornato AMO, ADOMD.NET e OLEDB librerie tooconnect tooand interfaccia client con un server Analysis Services. Per SQL Server Management Studio, SSDT, Excel 2016 e Power BI, le librerie client più recente di hello installazione o l'aggiornamento con le versioni mensile. Tuttavia, in alcuni casi, è possibile che un'applicazione potrebbe non essere hello più recente. Ad esempio, quando viene aggiornato il ritardo di criteri o aggiornamenti di Office 365 sono su hello canale posticipata.

## <a name="server-name"></a>Nome server

Quando si crea un server Analysis Services in Azure, specificare un univoco nome e hello regione in cui il server di hello toobe creato. Quando si specifica il nome di server hello in una connessione, lo schema di denominazione di hello server è:

```
<protocol>://<region>/<servername>
```
 In protocollo è stringa **asazure**, area è hello Uri in cui è stato creato il server di hello (ad esempio, westus.asazure.windows.net) e nome hello del server univoco all'interno di area hello servername.

### <a name="get-hello-server-name"></a>Ottenere il nome del server hello
In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server intera hello copia. Se altri utenti nell'organizzazione si connette troppo toothis server, è possibile condividere il nome del server con essi. Quando si specifica un nome di server, è necessario utilizzare intero percorso hello.

![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Stringa di connessione

Quando ci si connette tooAzure Analysis Services utilizzando hello modello a oggetti tabulare hello utilizzare formati di stringa di connessione seguente:

###### <a name="integrated-azure-active-directory-authentication"></a>Autenticazione integrata di Azure Active Directory
L'autenticazione integrata di preleva hello nella cache delle credenziali di Azure Active Directory, se disponibile. In caso contrario, finestra di accesso di Azure hello viene visualizzato.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Autenticazione di Azure Active Directory con nome utente e password

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Autenticazione di Windows (sicurezza integrata)
Utilizzare account di Windows hello in esecuzione il processo corrente di hello.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Connettersi usando un file con estensione odc
Con le versioni precedenti di Excel, gli utenti possono connettersi ai server di Azure Analysis Services tooan utilizzando un file Office Data Connection (odc). vedere, più toolearn [creare un file Office Data Connection (odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Passaggi successivi
[Connettersi con Excel](analysis-services-connect-excel.md)    
[Connettersi con Power BI](analysis-services-connect-pbi.md)   
[Gestire il server](analysis-services-manage.md)   

