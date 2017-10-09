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
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="31248-103">Connettere il server di Azure Analysis Services tooan</span><span class="sxs-lookup"><span data-stu-id="31248-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="31248-104">Questo articolo descrive la connessione server tooa tramite la modellazione dei dati e applicazioni di gestione come SQL Server Management Studio (SSMS) o SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="31248-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="31248-105">In alternativa, con applicazioni reporting client come Microsoft Excel, Power BI Desktop o applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="31248-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="31248-106">Connessioni tooAzure Analysis Services utilizzano HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31248-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="31248-107">Librerie client</span><span class="sxs-lookup"><span data-stu-id="31248-107">Client libraries</span></span>
[<span data-ttu-id="31248-108">Recuperare le librerie Client più recente di hello</span><span class="sxs-lookup"><span data-stu-id="31248-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="31248-109">Tutti i server tooa connessioni, indipendentemente dal tipo, richiedono aggiornato AMO, ADOMD.NET e OLEDB librerie tooconnect tooand interfaccia client con un server Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="31248-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="31248-110">Per SQL Server Management Studio, SSDT, Excel 2016 e Power BI, le librerie client più recente di hello installazione o l'aggiornamento con le versioni mensile.</span><span class="sxs-lookup"><span data-stu-id="31248-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="31248-111">Tuttavia, in alcuni casi, è possibile che un'applicazione potrebbe non essere hello più recente.</span><span class="sxs-lookup"><span data-stu-id="31248-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="31248-112">Ad esempio, quando viene aggiornato il ritardo di criteri o aggiornamenti di Office 365 sono su hello canale posticipata.</span><span class="sxs-lookup"><span data-stu-id="31248-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="31248-113">Nome server</span><span class="sxs-lookup"><span data-stu-id="31248-113">Server name</span></span>

<span data-ttu-id="31248-114">Quando si crea un server Analysis Services in Azure, specificare un univoco nome e hello regione in cui il server di hello toobe creato.</span><span class="sxs-lookup"><span data-stu-id="31248-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="31248-115">Quando si specifica il nome di server hello in una connessione, lo schema di denominazione di hello server è:</span><span class="sxs-lookup"><span data-stu-id="31248-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="31248-116">In protocollo è stringa **asazure**, area è hello Uri in cui è stato creato il server di hello (ad esempio, westus.asazure.windows.net) e nome hello del server univoco all'interno di area hello servername.</span><span class="sxs-lookup"><span data-stu-id="31248-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="31248-117">Ottenere il nome del server hello</span><span class="sxs-lookup"><span data-stu-id="31248-117">Get hello server name</span></span>
<span data-ttu-id="31248-118">In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server intera hello copia.</span><span class="sxs-lookup"><span data-stu-id="31248-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="31248-119">Se altri utenti nell'organizzazione si connette troppo toothis server, è possibile condividere il nome del server con essi.</span><span class="sxs-lookup"><span data-stu-id="31248-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="31248-120">Quando si specifica un nome di server, è necessario utilizzare intero percorso hello.</span><span class="sxs-lookup"><span data-stu-id="31248-120">When specifying a server name, hello entire path must be used.</span></span>

![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="31248-122">Stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="31248-122">Connection string</span></span>

<span data-ttu-id="31248-123">Quando ci si connette tooAzure Analysis Services utilizzando hello modello a oggetti tabulare hello utilizzare formati di stringa di connessione seguente:</span><span class="sxs-lookup"><span data-stu-id="31248-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="31248-124">Autenticazione integrata di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31248-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="31248-125">L'autenticazione integrata di preleva hello nella cache delle credenziali di Azure Active Directory, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="31248-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="31248-126">In caso contrario, finestra di accesso di Azure hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="31248-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="31248-127">Autenticazione di Azure Active Directory con nome utente e password</span><span class="sxs-lookup"><span data-stu-id="31248-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="31248-128">Autenticazione di Windows (sicurezza integrata)</span><span class="sxs-lookup"><span data-stu-id="31248-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="31248-129">Utilizzare account di Windows hello in esecuzione il processo corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="31248-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="31248-130">Connettersi usando un file con estensione odc</span><span class="sxs-lookup"><span data-stu-id="31248-130">Connect using an .odc file</span></span>
<span data-ttu-id="31248-131">Con le versioni precedenti di Excel, gli utenti possono connettersi ai server di Azure Analysis Services tooan utilizzando un file Office Data Connection (odc).</span><span class="sxs-lookup"><span data-stu-id="31248-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="31248-132">vedere, più toolearn [creare un file Office Data Connection (odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="31248-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="31248-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31248-133">Next steps</span></span>
<span data-ttu-id="31248-134">[Connettersi con Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="31248-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="31248-135">[Connettersi con Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="31248-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="31248-136">Gestire il server</span><span class="sxs-lookup"><span data-stu-id="31248-136">Manage your server</span></span>](analysis-services-manage.md)   

