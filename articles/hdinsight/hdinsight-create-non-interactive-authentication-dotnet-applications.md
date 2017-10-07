---
title: autenticazione non interattivo aaaCreate HDInsight .NET OLAF - Azure | Documenti Microsoft
description: Informazioni su come applicazioni di HDInsight .NET toocreate autenticazione non interattivo.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="d68ff-103">Creare applicazioni .NET HDInsight di autenticazione non interattive</span><span class="sxs-lookup"><span data-stu-id="d68ff-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="d68ff-104">È possibile eseguire l'applicazione .NET Azure HDInsight con identità dell'applicazione (non interattivo) o con identità hello di hello utente connesso di un'applicazione hello (interattiva).</span><span class="sxs-lookup"><span data-stu-id="d68ff-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="d68ff-105">Per un esempio di un'applicazione hello interattivo, vedere [connettersi tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="d68ff-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="d68ff-106">In questo articolo illustra come toocreate interattivo autenticazione .NET applicazione tooconnect tooAzure e gestire HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d68ff-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="d68ff-107">Dall'applicazione .NET non interattiva, è necessario disporre degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d68ff-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="d68ff-108">ID tenant della sottoscrizione di Azure, ovvero l'ID di directory.</span><span class="sxs-lookup"><span data-stu-id="d68ff-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="d68ff-109">Vedere [Ottenere l'ID tenant](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="d68ff-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="d68ff-110">ID client dell'applicazione di Hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d68ff-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="d68ff-111">Vedere [Creare un'applicazione Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Ottenere un ID applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="d68ff-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="d68ff-112">Hello Azure Active Directory dell'applicazione la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="d68ff-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="d68ff-113">Vedere [Ottenere la chiave di autenticazione dell'applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="d68ff-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d68ff-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d68ff-114">Prerequisites</span></span>
* <span data-ttu-id="d68ff-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d68ff-115">HDInsight cluster.</span></span> <span data-ttu-id="d68ff-116">Vedere [Esercitazione introduttiva](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="d68ff-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="d68ff-117">Assegnare toorole applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="d68ff-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="d68ff-118">È necessario assegnare tooa applicazione hello [ruolo](../active-directory/role-based-access-built-in-roles.md) toogrant le autorizzazioni per l'esecuzione di azioni.</span><span class="sxs-lookup"><span data-stu-id="d68ff-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="d68ff-119">È possibile impostare l'ambito hello a livello di hello di sottoscrizione hello, gruppo di risorse o la risorsa.</span><span class="sxs-lookup"><span data-stu-id="d68ff-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="d68ff-120">le autorizzazioni di Hello sono ereditati toolower livelli di ambito (ad esempio, l'aggiunta di un ruolo di lettore toohello applicazione per un gruppo di risorse significa che è possibile leggere il gruppo di risorse hello e le risorse contenute).</span><span class="sxs-lookup"><span data-stu-id="d68ff-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="d68ff-121">In questa esercitazione si imposteranno ambito hello a livello di gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d68ff-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="d68ff-122">Per ulteriori informazioni, vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="d68ff-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="d68ff-123">**hello tooadd applicazione Azure AD toohello del ruolo proprietario**</span><span class="sxs-lookup"><span data-stu-id="d68ff-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="d68ff-124">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d68ff-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d68ff-125">Fare clic su **gruppo di risorse** hello nel riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="d68ff-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="d68ff-126">Fare clic su gruppo di risorse hello che contiene il cluster di HDInsight hello in cui si eseguirà la query Hive più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d68ff-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="d68ff-127">Se sono presenti troppi gruppi di risorse, è possibile utilizzare il filtro di hello.</span><span class="sxs-lookup"><span data-stu-id="d68ff-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="d68ff-128">Fare clic su **Access control (IAM)** dal menu del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d68ff-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="d68ff-129">Fare clic su **Aggiungi** da hello **utenti** blade.</span><span class="sxs-lookup"><span data-stu-id="d68ff-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="d68ff-130">Seguire hello di hello istruzione tooadd **proprietario** toohello ruolo applicazione AD Azure creata nella procedura ultimo hello.</span><span class="sxs-lookup"><span data-stu-id="d68ff-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="d68ff-131">Quando viene completata correttamente, verrà visualizzata un'applicazione hello elencata nel Pannello di hello gli utenti con ruolo di proprietario hello.</span><span class="sxs-lookup"><span data-stu-id="d68ff-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="d68ff-132">Sviluppare l'applicazione client HDInsight</span><span class="sxs-lookup"><span data-stu-id="d68ff-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="d68ff-133">Creare un'applicazione console C#.</span><span class="sxs-lookup"><span data-stu-id="d68ff-133">Create a C# console application.</span></span>
2. <span data-ttu-id="d68ff-134">Aggiungere i seguenti pacchetti Nuget hello:</span><span class="sxs-lookup"><span data-stu-id="d68ff-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="d68ff-135">Utilizzare hello nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d68ff-135">Use hello following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="d68ff-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d68ff-136">Next steps</span></span>
* [<span data-ttu-id="d68ff-137">Creare un'applicazione e un'entità servizio di Azure Active Directory tramite il portale</span><span class="sxs-lookup"><span data-stu-id="d68ff-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="d68ff-138">Autenticazione di un'entità servizio con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d68ff-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="d68ff-139">Controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="d68ff-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
