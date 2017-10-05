---
title: Creare applicazioni .NET HDInsight di autenticazione non interattive - Azure | Microsoft Docs
description: Informazioni su come creare applicazioni .NET HDInsight di autenticazione non interattive.
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="5802b-103">Creare applicazioni .NET HDInsight di autenticazione non interattive</span><span class="sxs-lookup"><span data-stu-id="5802b-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="5802b-104">È possibile eseguire l'applicazione .NET Azure HDInsight con l'identità specifica dell'applicazione (non interattiva) o con l'identità dell'utente che ha eseguito l'accesso all'applicazione (interattiva).</span><span class="sxs-lookup"><span data-stu-id="5802b-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="5802b-105">Per un esempio dell'applicazione interattiva, vedere [Connettersi ad Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="5802b-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="5802b-106">Questo articolo descrive come creare un'applicazione .NET di autenticazione non interattiva per connettersi ad Azure e gestire HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5802b-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="5802b-107">Dall'applicazione .NET non interattiva, è necessario disporre degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5802b-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="5802b-108">ID tenant della sottoscrizione di Azure, ovvero l'ID di directory.</span><span class="sxs-lookup"><span data-stu-id="5802b-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="5802b-109">Vedere [Ottenere l'ID tenant](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="5802b-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="5802b-110">ID client dell'applicazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5802b-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="5802b-111">Vedere [Creare un'applicazione Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Ottenere un ID applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="5802b-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="5802b-112">Chiave privata dell'applicazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5802b-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="5802b-113">Vedere [Ottenere la chiave di autenticazione dell'applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="5802b-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5802b-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5802b-114">Prerequisites</span></span>
* <span data-ttu-id="5802b-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5802b-115">HDInsight cluster.</span></span> <span data-ttu-id="5802b-116">Vedere [Esercitazione introduttiva](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="5802b-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="5802b-117">Assegnare l'applicazione Azure AD a un ruolo</span><span class="sxs-lookup"><span data-stu-id="5802b-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="5802b-118">È necessario assegnare l'applicazione a un [ruolo](../active-directory/role-based-access-built-in-roles.md) per concederle autorizzazioni per l'esecuzione di azioni.</span><span class="sxs-lookup"><span data-stu-id="5802b-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="5802b-119">È possibile impostare l'ambito al livello della sottoscrizione, del gruppo di risorse o della risorsa.</span><span class="sxs-lookup"><span data-stu-id="5802b-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="5802b-120">Le autorizzazioni vengono ereditate a livelli inferiori dell'ambito. Se ad esempio si aggiunge un'applicazione al ruolo Lettore per un gruppo di risorse, l'applicazione è in grado di leggere il gruppo di risorse e le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="5802b-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="5802b-121">In questa esercitazione verrà impostato l'ambito a livello di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5802b-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="5802b-122">Per altre informazioni, vedere [Usare le assegnazioni di ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5802b-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="5802b-123">**Per aggiungere il ruolo Proprietario all'applicazione Azure AD**</span><span class="sxs-lookup"><span data-stu-id="5802b-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="5802b-124">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5802b-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5802b-125">Fare clic su **Gruppo di risorse** nel pannello di sinistra.</span><span class="sxs-lookup"><span data-stu-id="5802b-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="5802b-126">Fare clic sul gruppo di risorse contenente il cluster HDInsight in cui verrà eseguita la query Hive più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5802b-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="5802b-127">Se è presente un numero eccessivo di gruppi di risorse, è possibile usare il filtro.</span><span class="sxs-lookup"><span data-stu-id="5802b-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="5802b-128">Scegliere **Controllo di accesso (IAM)** dal menu del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5802b-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="5802b-129">Fare clic su **Aggiungi** nel pannello **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="5802b-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="5802b-130">Seguire le istruzioni per aggiungere il ruolo **Proprietario** all'applicazione Azure AD creata nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="5802b-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="5802b-131">Al termine, l'applicazione verrà visualizzata nel pannello Utenti con il ruolo Proprietario.</span><span class="sxs-lookup"><span data-stu-id="5802b-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="5802b-132">Sviluppare l'applicazione client HDInsight</span><span class="sxs-lookup"><span data-stu-id="5802b-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="5802b-133">Creare un'applicazione console C#.</span><span class="sxs-lookup"><span data-stu-id="5802b-133">Create a C# console application.</span></span>
2. <span data-ttu-id="5802b-134">Aggiungere i pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="5802b-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="5802b-135">Usare il codice di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="5802b-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="5802b-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5802b-136">Next steps</span></span>
* [<span data-ttu-id="5802b-137">Creare un'applicazione e un'entità servizio di Azure Active Directory tramite il portale</span><span class="sxs-lookup"><span data-stu-id="5802b-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="5802b-138">Autenticazione di un'entità servizio con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5802b-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="5802b-139">Controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="5802b-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
