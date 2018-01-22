---
title: Migrieren der Konfiguration
author: ardalis
description: 
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: migration/configuration
ms.openlocfilehash: 90d9f730d31c2c70aec3d47610b9031a7d8e621b
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="migrating-configuration"></a><span data-ttu-id="6ef0b-102">Migrieren der Konfiguration</span><span class="sxs-lookup"><span data-stu-id="6ef0b-102">Migrating Configuration</span></span>

<span data-ttu-id="6ef0b-103">Durch [Steve Smith](https://ardalis.com/) und [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="6ef0b-103">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="6ef0b-104">In der vorherigen Artikel wir begann [Migrieren eines ASP.NET MVC-Projekts zu ASP.NET Core MVC](mvc.md).</span><span class="sxs-lookup"><span data-stu-id="6ef0b-104">In the previous article, we began [migrating an ASP.NET MVC project to ASP.NET Core MVC](mvc.md).</span></span> <span data-ttu-id="6ef0b-105">In diesem Artikel wir die Konfiguration migrieren.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-105">In this article, we migrate configuration.</span></span>

<span data-ttu-id="6ef0b-106">[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples) ([Vorgehensweise zum Herunterladen](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6ef0b-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="setup-configuration"></a><span data-ttu-id="6ef0b-107">Setup-Konfiguration</span><span class="sxs-lookup"><span data-stu-id="6ef0b-107">Setup Configuration</span></span>

<span data-ttu-id="6ef0b-108">ASP.NET Core wird nicht mehr verwendet, die *"Global.asax"* und *"Web.config"* Dateien, die frühere Versionen von ASP.NET verwendet.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-108">ASP.NET Core no longer uses the *Global.asax* and *web.config* files that previous versions of ASP.NET utilized.</span></span> <span data-ttu-id="6ef0b-109">In früheren Versionen von ASP.NET Startlogik für die Anwendung im positioniert wurde ein `Application_StartUp` Methode innerhalb *"Global.asax"*.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-109">In earlier versions of ASP.NET, application startup logic was placed in an `Application_StartUp` method within *Global.asax*.</span></span> <span data-ttu-id="6ef0b-110">Später werden Sie in ASP.NET MVC eine *Startup.cs* Datei im Stammverzeichnis des Projekts; enthalten war, und es wurde aufgerufen, wenn die Anwendung gestartet.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-110">Later, in ASP.NET MVC, a *Startup.cs* file was included in the root of the project; and, it was called when the application started.</span></span> <span data-ttu-id="6ef0b-111">ASP.NET Core hat dieser Ansatz vollständig von übernommen platzieren Startlogik für alle in der *Startup.cs* Datei.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-111">ASP.NET Core has adopted this approach completely by placing all startup logic in the *Startup.cs* file.</span></span>

<span data-ttu-id="6ef0b-112">Die *"Web.config"* Datei auch in ASP.NET Core ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-112">The *web.config* file has also been replaced in ASP.NET Core.</span></span> <span data-ttu-id="6ef0b-113">Konfiguration selbst kann nun konfiguriert werden, und als Teil der Schritte beim Starten einer Anwendung in beschriebenen *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-113">Configuration itself can now be configured, as part of the application startup procedure described in *Startup.cs*.</span></span> <span data-ttu-id="6ef0b-114">Konfiguration kann XML-Dateien weiterhin nutzen, sondern in der Regel ASP.NET Core Projekte werden platzieren Konfigurationswerte in einer JSON-formatierten Datei wie z. B. *appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-114">Configuration can still utilize XML files, but typically ASP.NET Core projects will place configuration values in a JSON-formatted file, such as *appsettings.json*.</span></span> <span data-ttu-id="6ef0b-115">ASP.NET-Core-Konfigurationssystem kann leicht Umgebungsvariablen, zugreifen, die einen Speicherort im sicheren und stabilen für umgebungsspezifische Werte angeben können.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-115">ASP.NET Core's configuration system can also easily access environment variables, which can provide a more secure and robust location for environment-specific values.</span></span> <span data-ttu-id="6ef0b-116">Dies gilt insbesondere für geheime Schlüssel, wie z. B. Verbindungszeichenfolgen und API-Schlüssel, die nicht in die quellcodeverwaltung überprüft werden sollen.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-116">This is especially true for secrets like connection strings and API keys that should not be checked into source control.</span></span> <span data-ttu-id="6ef0b-117">Finden Sie unter [Konfiguration](xref:fundamentals/configuration/index) Weitere Informationen zur Konfiguration in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-117">See [Configuration](xref:fundamentals/configuration/index) to learn more about configuration in ASP.NET Core.</span></span>

<span data-ttu-id="6ef0b-118">Für diesen Artikel beginnen wir mit dem teilweise migriert ASP.NET Core-Projekt aus [vorherigen Artikel](mvc.md).</span><span class="sxs-lookup"><span data-stu-id="6ef0b-118">For this article, we are starting with the partially-migrated ASP.NET Core project from [the previous article](mvc.md).</span></span> <span data-ttu-id="6ef0b-119">Zum Einrichten des Konfiguration fügen die folgenden Konstruktor und die Eigenschaft, um die *Startup.cs* Datei befindet sich im Stammverzeichnis des Projekts:</span><span class="sxs-lookup"><span data-stu-id="6ef0b-119">To setup configuration, add the following constructor and property to the *Startup.cs* file located in the root of the project:</span></span>

[!code-csharp[Main](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]

<span data-ttu-id="6ef0b-120">Beachten Sie, dass an diesem Punkt der *Startup.cs* Datei wird nicht kompiliert werden, da wir benötigen Sie Folgendes hinzufügen `using` Anweisung:</span><span class="sxs-lookup"><span data-stu-id="6ef0b-120">Note that at this point, the *Startup.cs* file will not compile, as we still need to add the following `using` statement:</span></span>

```csharp
using Microsoft.Extensions.Configuration;
```

<span data-ttu-id="6ef0b-121">Hinzufügen einer *appsettings.json* Datei im Stammverzeichnis des Projekts mit der entsprechenden Elementvorlage:</span><span class="sxs-lookup"><span data-stu-id="6ef0b-121">Add an *appsettings.json* file to the root of the project using the appropriate item template:</span></span>

![Hinzufügen von "appSettings" JSON](configuration/_static/add-appsettings-json.png)

## <a name="migrate-configuration-settings-from-webconfig"></a><span data-ttu-id="6ef0b-123">Migrieren von Konfigurationseinstellungen aus der Datei "Web.config"</span><span class="sxs-lookup"><span data-stu-id="6ef0b-123">Migrate Configuration Settings from web.config</span></span>

<span data-ttu-id="6ef0b-124">Unsere ASP.NET MVC-Projekt enthielt, die erforderliche Datenbank-Verbindungszeichenfolge in *"Web.config"*in die `<connectionStrings>` Element.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-124">Our ASP.NET MVC project included the required database connection string in *web.config*, in the `<connectionStrings>` element.</span></span> <span data-ttu-id="6ef0b-125">In unserem Projekt ASP.NET Core Kegel zum Speichern dieser Informationen in den *appsettings.json* Datei.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-125">In our ASP.NET Core project, we are going to store this information in the *appsettings.json* file.</span></span> <span data-ttu-id="6ef0b-126">Open *appsettings.json*, und beachten Sie, dass sie bereits die Folgendes umfasst:</span><span class="sxs-lookup"><span data-stu-id="6ef0b-126">Open *appsettings.json*, and note that it already includes the following:</span></span>

[!code-json[Main](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]


<span data-ttu-id="6ef0b-127">In der markierten Zeile in der oben dargestellten, ändern Sie den Namen der Datenbank von **_CHANGE_ME** auf den Namen der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-127">In the highlighted line depicted above, change the name of the database from **_CHANGE_ME** to the name of your database.</span></span>

## <a name="summary"></a><span data-ttu-id="6ef0b-128">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="6ef0b-128">Summary</span></span>

<span data-ttu-id="6ef0b-129">ASP.NET Core setzt alle Startlogik für die Anwendung in eine einzelne Datei, in der die erforderlichen Dienste und Abhängigkeiten definiert und konfiguriert werden können.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-129">ASP.NET Core places all startup logic for the application in a single file, in which the necessary services and dependencies can be defined and configured.</span></span> <span data-ttu-id="6ef0b-130">Er ersetzt die *"Web.config"* Datei in eine flexible Konfiguration-Funktion, die eine Vielzahl von Dateiformaten wie JSON sowie Umgebungsvariablen nutzen können.</span><span class="sxs-lookup"><span data-stu-id="6ef0b-130">It replaces the *web.config* file with a flexible configuration feature that can leverage a variety of file formats, such as JSON, as well as environment variables.</span></span>