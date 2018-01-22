---
title: "Konfigurieren Sie die Primärschlüsseldaten Identitätstyp"
author: AdrienTorris
description: "In diesem Artikel werden die Schritte zum Konfigurieren des gewünschten Datentyps für den Primärschlüssel ASP.NET Core Identity verwendet."
ms.author: scaddie
manager: wpickett
ms.date: 09/28/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-primary-key-configuration
ms.openlocfilehash: da46aa90a434a978a55467da982d746eb2d959ee
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="configure-the-aspnet-core-identity-primary-key-data-type"></a><span data-ttu-id="8f40c-103">Konfigurieren der ASP.NET Core Primärschlüsseldaten Identitätstyp</span><span class="sxs-lookup"><span data-stu-id="8f40c-103">Configure the ASP.NET Core Identity primary key data type</span></span>

<span data-ttu-id="8f40c-104">ASP.NET Core Identität können Sie so konfigurieren Sie den Datentyp verwendet, um einen Primärschlüssel darstellen.</span><span class="sxs-lookup"><span data-stu-id="8f40c-104">ASP.NET Core Identity allows you to configure the data type used to represent a primary key.</span></span> <span data-ttu-id="8f40c-105">Identität verwendet die `string` -Datentyp in der Standardeinstellung.</span><span class="sxs-lookup"><span data-stu-id="8f40c-105">Identity uses the `string` data type by default.</span></span> <span data-ttu-id="8f40c-106">Sie können dieses Verhalten überschreiben.</span><span class="sxs-lookup"><span data-stu-id="8f40c-106">You can override this behavior.</span></span>

## <a name="customize-the-primary-key-data-type"></a><span data-ttu-id="8f40c-107">Anpassen des Primärschlüsseldaten-Typs</span><span class="sxs-lookup"><span data-stu-id="8f40c-107">Customize the primary key data type</span></span>

1. <span data-ttu-id="8f40c-108">Erstellen Sie eine benutzerdefinierte Implementierung von der [IdentityUser](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser-1) Klasse.</span><span class="sxs-lookup"><span data-stu-id="8f40c-108">Create a custom implementation of the [IdentityUser](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser-1) class.</span></span> <span data-ttu-id="8f40c-109">Es stellt den Typ zum Erstellen von Benutzerobjekten verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="8f40c-109">It represents the type to be used for creating user objects.</span></span> <span data-ttu-id="8f40c-110">Im folgenden Beispiel, das standardmäßige `string` Typ wird mit ersetzt `Guid`.</span><span class="sxs-lookup"><span data-stu-id="8f40c-110">In the following example, the default `string` type is replaced with `Guid`.</span></span>

    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationUser.cs?highlight=4&range=7-13)]

1. <span data-ttu-id="8f40c-111">Erstellen Sie eine benutzerdefinierte Implementierung von der [IdentityRole](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityrole-1) Klasse.</span><span class="sxs-lookup"><span data-stu-id="8f40c-111">Create a custom implementation of the [IdentityRole](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.identity.entityframeworkcore.identityrole-1) class.</span></span> <span data-ttu-id="8f40c-112">Er den Typ darstellt, für das Role-Objekte erstellen.</span><span class="sxs-lookup"><span data-stu-id="8f40c-112">It represents the type to be used for creating role objects.</span></span> <span data-ttu-id="8f40c-113">Im folgenden Beispiel, das standardmäßige `string` Typ wird mit ersetzt `Guid`.</span><span class="sxs-lookup"><span data-stu-id="8f40c-113">In the following example, the default `string` type is replaced with `Guid`.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationRole.cs?highlight=3&range=7-12)]
    
1. <span data-ttu-id="8f40c-114">Erstellen Sie eine benutzerdefinierte Datenbank Context-Klasse.</span><span class="sxs-lookup"><span data-stu-id="8f40c-114">Create a custom database context class.</span></span> <span data-ttu-id="8f40c-115">Es erbt von der Entity Framework Database Context-Klasse für die Identität verwendet.</span><span class="sxs-lookup"><span data-stu-id="8f40c-115">It inherits from the Entity Framework database context class used for Identity.</span></span> <span data-ttu-id="8f40c-116">Die `TUser` und `TRole` Argumente verweisen, die benutzerdefinierte Benutzer und die Rolle Klassen, die jeweils im vorherigen Schritt erstellt.</span><span class="sxs-lookup"><span data-stu-id="8f40c-116">The `TUser` and `TRole` arguments reference the custom user and role classes created in the previous step, respectively.</span></span> <span data-ttu-id="8f40c-117">Die `Guid` -Datentyp für den Primärschlüssel definiert ist.</span><span class="sxs-lookup"><span data-stu-id="8f40c-117">The `Guid` data type is defined for the primary key.</span></span>

    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Data/ApplicationDbContext.cs?highlight=3&range=9-26)]
    
1. <span data-ttu-id="8f40c-118">Registrieren Sie benutzerdefinierte Datenbank Context-Klasse, wenn die Identity-Dienst in der app-Start-Klasse hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8f40c-118">Register the custom database context class when adding the Identity service in the app's startup class.</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8f40c-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8f40c-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    <span data-ttu-id="8f40c-120">Die `AddEntityFrameworkStores` Methode nicht akzeptieren ein `TKey` Argument als es wurde in ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="8f40c-120">The `AddEntityFrameworkStores` method doesn't accept a `TKey` argument as it did in ASP.NET Core 1.x.</span></span> <span data-ttu-id="8f40c-121">Der Primärschlüssel-Datentyp wird abgeleitet, durch die Analyse der `DbContext` Objekt.</span><span class="sxs-lookup"><span data-stu-id="8f40c-121">The primary key's data type is inferred by analyzing the `DbContext` object.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=6-8&range=25-37)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8f40c-122">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8f40c-122">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    <span data-ttu-id="8f40c-123">Die `AddEntityFrameworkStores` Methode akzeptiert eine `TKey` Arguments, den primären Schlüssel den Datentyp angibt.</span><span class="sxs-lookup"><span data-stu-id="8f40c-123">The `AddEntityFrameworkStores` method accepts a `TKey` argument indicating the primary key's data type.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=9-11&range=39-55)]
    
    ---

## <a name="test-the-changes"></a><span data-ttu-id="8f40c-124">Testen Sie die Änderungen</span><span class="sxs-lookup"><span data-stu-id="8f40c-124">Test the changes</span></span>

<span data-ttu-id="8f40c-125">Nach Abschluss der konfigurationsänderungen gibt die Eigenschaft, die den Primärschlüssel darstellt. der neue Datentyp wieder.</span><span class="sxs-lookup"><span data-stu-id="8f40c-125">Upon completion of the configuration changes, the property representing the primary key reflects the new data type.</span></span> <span data-ttu-id="8f40c-126">Das folgende Beispiel veranschaulicht den Zugriff auf die Eigenschaft in einer MVC-Controller.</span><span class="sxs-lookup"><span data-stu-id="8f40c-126">The following example demonstrates accessing the property in an MVC controller.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Controllers/AccountController.cs?name=snippet_GetCurrentUserId&highlight=6)]