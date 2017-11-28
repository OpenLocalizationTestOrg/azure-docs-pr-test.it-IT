---
title: Connettersi ad Azure Analysis Services | Microsoft Docs
description: Informazioni su come connettersi e ottenere dati da un server di Analysis Services in Azure.
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
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="63fe7-103">Connettersi a un server di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="63fe7-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="63fe7-104">In questo articolo viene descritta la connessione a un server tramite modellazione di dati e applicazioni di gestione come SQL Server Management Studio (SSMS) o SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="63fe7-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="63fe7-105">In alternativa, con applicazioni reporting client come Microsoft Excel, Power BI Desktop o applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="63fe7-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="63fe7-106">Le connessioni ad Azure Analysis Services usano HTTPS.</span><span class="sxs-lookup"><span data-stu-id="63fe7-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="63fe7-107">Librerie client</span><span class="sxs-lookup"><span data-stu-id="63fe7-107">Client libraries</span></span>
[<span data-ttu-id="63fe7-108">Ottenere le librerie client più recenti</span><span class="sxs-lookup"><span data-stu-id="63fe7-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="63fe7-109">Tutte le connessioni a qualunque tipo di server richiedono le librerie client AMO, ADOMD.NET e OLEDB aggiornate per connettersi e interagire con un server di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="63fe7-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="63fe7-110">Per SSMS, SSDT, Excel 2016 e Power BI, le librerie client più recenti vengono installate o aggiornate con le versioni mensili.</span><span class="sxs-lookup"><span data-stu-id="63fe7-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="63fe7-111">In alcuni casi, tuttavia, è possibile che un'applicazione non abbia la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="63fe7-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="63fe7-112">Ad esempio, quando alcuni criteri ritardano gli aggiornamenti o quando gli aggiornamenti di Office 365 sono su Deferred Channel.</span><span class="sxs-lookup"><span data-stu-id="63fe7-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="63fe7-113">Nome server</span><span class="sxs-lookup"><span data-stu-id="63fe7-113">Server name</span></span>

<span data-ttu-id="63fe7-114">Quando si crea un server di Analysis Services in Azure, si specifica un nome univoco e l'area in cui il server deve essere creato.</span><span class="sxs-lookup"><span data-stu-id="63fe7-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="63fe7-115">Quando si specifica il nome del server in una connessione, lo schema di denominazione del server è il seguente:</span><span class="sxs-lookup"><span data-stu-id="63fe7-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="63fe7-116">Dove protocol è la stringa **asazure**, region è l'Uri in cui è stato creato il server, ad esempio westus.asazure.windows.net, e servername è il nome del server univoco all'interno dell'area.</span><span class="sxs-lookup"><span data-stu-id="63fe7-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="63fe7-117">Ottenere il nome del server</span><span class="sxs-lookup"><span data-stu-id="63fe7-117">Get the server name</span></span>
<span data-ttu-id="63fe7-118">Nel **portale di Azure** > server > **Panoramica** > **Nome server** copiare l'intero nome del server.</span><span class="sxs-lookup"><span data-stu-id="63fe7-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="63fe7-119">Se anche altri utenti nell'organizzazione si connettono a questo server, è opportuno condividere il nome del server.</span><span class="sxs-lookup"><span data-stu-id="63fe7-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="63fe7-120">Quando si specifica un nome di server, è necessario usare l'intero percorso.</span><span class="sxs-lookup"><span data-stu-id="63fe7-120">When specifying a server name, the entire path must be used.</span></span>

![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="63fe7-122">Stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="63fe7-122">Connection string</span></span>

<span data-ttu-id="63fe7-123">Quando ci si connette a Azure Analysis Services usando il modello a oggetti tabulare, usare i formati seguenti per la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="63fe7-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="63fe7-124">Autenticazione integrata di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63fe7-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="63fe7-125">L'autenticazione integrata seleziona la cache delle credenziali di Azure Active Directory, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="63fe7-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="63fe7-126">In caso contrario, viene visualizzata la finestra di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="63fe7-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="63fe7-127">Autenticazione di Azure Active Directory con nome utente e password</span><span class="sxs-lookup"><span data-stu-id="63fe7-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="63fe7-128">Autenticazione di Windows (sicurezza integrata)</span><span class="sxs-lookup"><span data-stu-id="63fe7-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="63fe7-129">Usare l'account di Windows su cui è in esecuzione il processo corrente.</span><span class="sxs-lookup"><span data-stu-id="63fe7-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="63fe7-130">Connettersi usando un file con estensione odc</span><span class="sxs-lookup"><span data-stu-id="63fe7-130">Connect using an .odc file</span></span>
<span data-ttu-id="63fe7-131">Con le versioni precedenti di Excel, gli utenti possono connettersi a un server di Azure Analysis Services usando un file Office Data Connection, con estensione odc.</span><span class="sxs-lookup"><span data-stu-id="63fe7-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="63fe7-132">Per altre informazioni, vedere [Creare un file Office Data Connection (con estensione odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="63fe7-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="63fe7-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63fe7-133">Next steps</span></span>
<span data-ttu-id="63fe7-134">[Connettersi con Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="63fe7-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="63fe7-135">[Connettersi con Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="63fe7-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="63fe7-136">Gestire il server</span><span class="sxs-lookup"><span data-stu-id="63fe7-136">Manage your server</span></span>](analysis-services-manage.md)   

