---
title: "Abhängigkeitsinjektion in Controllern"
author: ardalis
description: 
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/controllers/dependency-injection
ms.openlocfilehash: 21cffcd285879fdca81cb7d92d0f079d4bf7756c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="dependency-injection-into-controllers"></a><span data-ttu-id="591ff-102">Abhängigkeitsinjektion in Controllern</span><span class="sxs-lookup"><span data-stu-id="591ff-102">Dependency injection into controllers</span></span>

<a name="dependency-injection-controllers"></a>

<span data-ttu-id="591ff-103">Durch [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="591ff-103">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="591ff-104">ASP.NET Core MVC-Controller, sollte ihre Abhängigkeiten explizit über ihre Konstruktoren anfordern.</span><span class="sxs-lookup"><span data-stu-id="591ff-104">ASP.NET Core MVC controllers should request their dependencies explicitly via their constructors.</span></span> <span data-ttu-id="591ff-105">In einigen Fällen einzelne Controlleraktionen erfordern möglicherweise einen Dienst und es möglicherweise nicht sinnvoll, um auf Controllerebene anzufordern.</span><span class="sxs-lookup"><span data-stu-id="591ff-105">In some instances, individual controller actions may require a service, and it may not make sense to request at the controller level.</span></span> <span data-ttu-id="591ff-106">In diesem Fall können Sie auch auswählen, einen Dienst als Parameter auf die Aktionsmethode einzufügen.</span><span class="sxs-lookup"><span data-stu-id="591ff-106">In this case, you can also choose to inject a service as a parameter on the action method.</span></span>

<span data-ttu-id="591ff-107">[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample) ([Vorgehensweise zum Herunterladen](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="591ff-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="591ff-108">Abhängigkeitsinjektion</span><span class="sxs-lookup"><span data-stu-id="591ff-108">Dependency Injection</span></span>

<span data-ttu-id="591ff-109">Abhängigkeitsinjektion ist eine Technik, die folgt die [Abhängigkeit Umkehrung Prinzip](http://deviq.com/dependency-inversion-principle/), sodass bei Anwendungen, die von lose verbundenen Modulen gebildet werden.</span><span class="sxs-lookup"><span data-stu-id="591ff-109">Dependency injection is a technique that follows the [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/), allowing for applications to be composed of loosely coupled modules.</span></span> <span data-ttu-id="591ff-110">ASP.NET Core verfügt über integrierte Unterstützung für [Abhängigkeitsinjektion](../../fundamentals/dependency-injection.md), wodurch Anwendungen einfacher zu testen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="591ff-110">ASP.NET Core has built-in support for [dependency injection](../../fundamentals/dependency-injection.md), which makes applications easier to test and maintain.</span></span>

## <a name="constructor-injection"></a><span data-ttu-id="591ff-111">Konstruktoreinfügung</span><span class="sxs-lookup"><span data-stu-id="591ff-111">Constructor Injection</span></span>

<span data-ttu-id="591ff-112">ASP.NET Core der integrierte Unterstützung für Konstruktor basierende Abhängigkeitsinjektion erstreckt sich bis MVC-Controller.</span><span class="sxs-lookup"><span data-stu-id="591ff-112">ASP.NET Core's built-in support for constructor-based dependency injection extends to MVC controllers.</span></span> <span data-ttu-id="591ff-113">Durch einen Diensttyp einfach Ihre Domänencontroller als Konstruktorparameter hinzufügen, versucht ASP.NET Core, dieses Typs mit der integrierten Dienstcontainer aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="591ff-113">By simply adding a service type to your controller as a constructor parameter, ASP.NET Core will attempt to resolve that type using its built in service container.</span></span> <span data-ttu-id="591ff-114">Dienste werden in der Regel, jedoch nicht immer mit Schnittstellen definiert.</span><span class="sxs-lookup"><span data-stu-id="591ff-114">Services are typically, but not always, defined using interfaces.</span></span> <span data-ttu-id="591ff-115">Wenn Ihre Anwendung von Geschäftslogik, die von der aktuellen Zeit abhängig ist, können Sie z. B. einen Dienst, der die Zeit (statt eine feste Programmierung ihn), ruft einfügen die ermöglichen würden die Tests Implementierungen zu übergeben, die einem bestimmten Zeitpunkt zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="591ff-115">For example, if your application has business logic that depends on the current time, you can inject a service that retrieves the time (rather than hard-coding it), which would allow your tests to pass in implementations that use a set time.</span></span>

[!code-csharp[Main](dependency-injection/sample/src/ControllerDI/Interfaces/IDateTime.cs)]


<span data-ttu-id="591ff-116">Implementieren einer Schnittstelle wie dieses, sodass die Systemuhr zur Laufzeit verwendet, ist trivial:</span><span class="sxs-lookup"><span data-stu-id="591ff-116">Implementing an interface like this one so that it uses the system clock at runtime is trivial:</span></span>

[!code-csharp[Main](dependency-injection/sample/src/ControllerDI/Services/SystemDateTime.cs)]


<span data-ttu-id="591ff-117">Mit diesem erfüllt können wir den Dienst in unser Controller verwenden.</span><span class="sxs-lookup"><span data-stu-id="591ff-117">With this in place, we can use the service in our controller.</span></span> <span data-ttu-id="591ff-118">In diesem Fall haben wir die Programmlogik zum hinzugefügt der `HomeController` `Index` Methode, um dem Benutzer einen Gruß anzeigen auf Grundlage der Tageszeit.</span><span class="sxs-lookup"><span data-stu-id="591ff-118">In this case, we have added some logic to the `HomeController` `Index` method to display a greeting to the user based on the time of day.</span></span>

[!code-csharp[Main](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=8,10,12,17,18,19,20,21,22,23,24,25,26,27,28,29,30&range=1-31,51-52)]

<span data-ttu-id="591ff-119">Wenn wir die Anwendung jetzt ausführen, wird es sehr wahrscheinlich einen Fehler auftreten:</span><span class="sxs-lookup"><span data-stu-id="591ff-119">If we run the application now, we will most likely encounter an error:</span></span>

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Unable to resolve service for type 'ControllerDI.Interfaces.IDateTime' while attempting to activate 'ControllerDI.Controllers.HomeController'.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.GetService(IServiceProvider sp, Type type, Type requiredBy, Boolean isDefaultParameterRequired)
```

<span data-ttu-id="591ff-120">Dieser Fehler tritt auf, wenn es einen Dienst in nicht konfiguriert haben die `ConfigureServices` -Methode in unserer `Startup` Klasse.</span><span class="sxs-lookup"><span data-stu-id="591ff-120">This error occurs when we have not configured a service in the `ConfigureServices` method in our `Startup` class.</span></span> <span data-ttu-id="591ff-121">Um anzugeben, die Anforderungen für `IDateTime` sollten korrigiert werden, mithilfe einer Instanz von `SystemDateTime`, fügen Sie die hervorgehobene Zeile in der Liste unten, um Ihre `ConfigureServices` Methode:</span><span class="sxs-lookup"><span data-stu-id="591ff-121">To specify that requests for `IDateTime` should be resolved using an instance of `SystemDateTime`, add the highlighted line in the listing below to your `ConfigureServices` method:</span></span>

[!code-csharp[Main](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=4&range=26-27,42-44)]

> [!NOTE]
> <span data-ttu-id="591ff-122">Diese bestimmten Dienst mit einer von mehreren verschiedenen Lebensdauer Optionen implementiert werden kann (`Transient`, `Scoped`, oder `Singleton`).</span><span class="sxs-lookup"><span data-stu-id="591ff-122">This particular service could be implemented using any of several different lifetime options (`Transient`, `Scoped`, or `Singleton`).</span></span> <span data-ttu-id="591ff-123">Finden Sie unter [Abhängigkeitsinjektion](../../fundamentals/dependency-injection.md) zu verstehen, wie jede dieser Bereichsoptionen das Verhalten des Diensts auswirken.</span><span class="sxs-lookup"><span data-stu-id="591ff-123">See [Dependency Injection](../../fundamentals/dependency-injection.md) to understand how each of these scope options will affect the behavior of your service.</span></span>

<span data-ttu-id="591ff-124">Sobald der Dienst konfiguriert wurde, sollte Ausführen der Anwendung, und navigieren zur Startseite die Nachricht einen zeitbasierten anzeigen, wie erwartet:</span><span class="sxs-lookup"><span data-stu-id="591ff-124">Once the service has been configured, running the application and navigating to the home page should display the time-based message as expected:</span></span>

![Grußformel bei der Server](dependency-injection/_static/server-greeting.png)

>[!TIP]
> <span data-ttu-id="591ff-126">Finden Sie unter [Controllerlogik testen](testing.md) zu erfahren, wie Sie Abhängigkeiten explizit anfordern [http://deviq.com/explicit-dependencies-principle/](http://deviq.com/explicit-dependencies-principle/) im Controller wird der Code einfacher zu testen.</span><span class="sxs-lookup"><span data-stu-id="591ff-126">See [Testing Controller Logic](testing.md) to learn how to explicitly request dependencies [http://deviq.com/explicit-dependencies-principle/](http://deviq.com/explicit-dependencies-principle/) in controllers makes code easier to test.</span></span>

<span data-ttu-id="591ff-127">ASP.NET Core des integrierten Abhängigkeitsinjektion unterstützt das Vorhandensein nur eines einzelnen Konstruktors für Klassen, die Dienste anfordern.</span><span class="sxs-lookup"><span data-stu-id="591ff-127">ASP.NET Core's built-in dependency injection supports having only a single constructor for classes requesting services.</span></span> <span data-ttu-id="591ff-128">Wenn Sie mehr als einen Konstruktor verfügen, erhalten Sie möglicherweise eine Ausnahme, die besagt:</span><span class="sxs-lookup"><span data-stu-id="591ff-128">If you have more than one constructor, you may get an exception stating:</span></span>

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Multiple constructors accepting all given argument types have been found in type 'ControllerDI.Controllers.HomeController'. There should only be one applicable constructor.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.FindApplicableConstructor(Type instanceType, Type[] argumentTypes, ConstructorInfo& matchingConstructor, Nullable`1[]& parameterMap)
```

<span data-ttu-id="591ff-129">Wie in die Fehlermeldung angegeben, können Sie dieses Problem, dass nur einen einzelnen Konstruktor beheben.</span><span class="sxs-lookup"><span data-stu-id="591ff-129">As the error message states, you can correct this problem having just a single constructor.</span></span> <span data-ttu-id="591ff-130">Sie können auch [ersetzen standardmäßig Dependency Injection-Unterstützung mit einer Implementierung von Drittanbietern](../../fundamentals/dependency-injection.md#replacing-the-default-services-container)viele mehrere Konstruktoren werden, unterstützen.</span><span class="sxs-lookup"><span data-stu-id="591ff-130">You can also [replace the default dependency injection support with a third party implementation](../../fundamentals/dependency-injection.md#replacing-the-default-services-container), many of which support multiple constructors.</span></span>

## <a name="action-injection-with-fromservices"></a><span data-ttu-id="591ff-131">Aktion-Injection mit FromServices</span><span class="sxs-lookup"><span data-stu-id="591ff-131">Action Injection with FromServices</span></span>

<span data-ttu-id="591ff-132">In einigen Fällen benötigen Sie keinen Dienst für mehr als eine Aktion innerhalb Ihres Controllers.</span><span class="sxs-lookup"><span data-stu-id="591ff-132">Sometimes you don't need a service for more than one action within your controller.</span></span> <span data-ttu-id="591ff-133">In diesem Fall kann es sinnvoll, den Dienst als Parameter an die Aktionsmethode einzufügen.</span><span class="sxs-lookup"><span data-stu-id="591ff-133">In this case, it may make sense to inject the service as a parameter to the action method.</span></span> <span data-ttu-id="591ff-134">Dies erfolgt durch den Parameter mit dem Attribut kennzeichnen `[FromServices]` wie hier gezeigt:</span><span class="sxs-lookup"><span data-stu-id="591ff-134">This is done by marking the parameter with the attribute `[FromServices]` as shown here:</span></span>

[!code-csharp[Main](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=1&range=33-38)]

## <a name="accessing-settings-from-a-controller"></a><span data-ttu-id="591ff-135">Zugreifen auf Einstellungen von einem Controller</span><span class="sxs-lookup"><span data-stu-id="591ff-135">Accessing Settings from a Controller</span></span>

<span data-ttu-id="591ff-136">Zugriff auf Anwendungs- oder Einstellungen innerhalb eines Controllers ist ein allgemeines Muster.</span><span class="sxs-lookup"><span data-stu-id="591ff-136">Accessing application or configuration settings from within a controller is a common pattern.</span></span> <span data-ttu-id="591ff-137">Dieser Zugriff sollte die in beschriebenen Optionen-Muster verwenden [Konfiguration](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="591ff-137">This access should use the Options pattern described in [configuration](xref:fundamentals/configuration/index).</span></span> <span data-ttu-id="591ff-138">Sie sollten im Allgemeinen Einstellungen nicht direkt aus Ihrem Controller mithilfe der Abhängigkeitsinjektion anfordern.</span><span class="sxs-lookup"><span data-stu-id="591ff-138">You generally should not request settings directly from your controller using dependency injection.</span></span> <span data-ttu-id="591ff-139">Ein besserer Ansatz besteht darin Anforderung eine `IOptions<T>` Instanz, in denen `T` ist die Konfigurationsklasse, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="591ff-139">A better approach is to request an `IOptions<T>` instance, where `T` is the configuration class you need.</span></span>

<span data-ttu-id="591ff-140">Um mit dem Muster Optionen zu arbeiten, müssen Sie eine Klasse erstellen, die Optionen, wie diese darstellt:</span><span class="sxs-lookup"><span data-stu-id="591ff-140">To work with the options pattern, you need to create a class that represents the options, such as this one:</span></span>

[!code-csharp[Main](dependency-injection/sample/src/ControllerDI/Model/SampleWebSettings.cs)]

<span data-ttu-id="591ff-141">Dann müssen Sie so konfigurieren Sie die Anwendung verwenden Sie das Modell für die Optionen, und fügen Sie Ihrer Konfigurationsklasse auf die Auflistung der Dienste in `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="591ff-141">Then you need to configure the application to use the options model and add your configuration class to the services collection in `ConfigureServices`:</span></span>

[!code-csharp[Main](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=3,4,5,6,9,16,19&range=14-44)]

> [!NOTE]
> <span data-ttu-id="591ff-142">In der obigen Liste konfigurieren wir die Anwendung, die Einstellungen aus einer JSON-formatierten Datei zu lesen.</span><span class="sxs-lookup"><span data-stu-id="591ff-142">In the above listing, we are configuring the application to read the settings from a JSON-formatted file.</span></span> <span data-ttu-id="591ff-143">Sie können auch die Einstellungen vollständig im Code konfigurieren, wie im obigen kommentierten Code gezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="591ff-143">You can also configure the settings entirely in code, as is shown in the commented code above.</span></span> <span data-ttu-id="591ff-144">Finden Sie unter [Konfiguration](xref:fundamentals/configuration/index) für weitere Konfigurationsoptionen.</span><span class="sxs-lookup"><span data-stu-id="591ff-144">See [Configuration](xref:fundamentals/configuration/index) for further configuration options.</span></span>

<span data-ttu-id="591ff-145">Nachdem Sie eine stark typisierte Konfigurationsobjekt angegeben haben (in diesem Fall `SampleWebSettings`) und wurde jedoch hinzugefügt, auf die Auflistung Dienste können fordern sie eine beliebige andere Methode Controller bzw. die Aktionsmethode Anfordern einer Instanz von `IOptions<T>` (in diesem Fall `IOptions<SampleWebSettings>`) .</span><span class="sxs-lookup"><span data-stu-id="591ff-145">Once you've specified a strongly-typed configuration object (in this case, `SampleWebSettings`) and added it to the services collection, you can request it from any Controller or Action method by requesting an instance of `IOptions<T>` (in this case, `IOptions<SampleWebSettings>`).</span></span> <span data-ttu-id="591ff-146">Der folgende Code zeigt, wie eine die Einstellungen von einem Controller anfordern möchten:</span><span class="sxs-lookup"><span data-stu-id="591ff-146">The following code shows how one would request the settings from a controller:</span></span>

[!code-csharp[Main](./dependency-injection/sample/src/ControllerDI/Controllers/SettingsController.cs?highlight=3,5,7&range=7-22)]

<span data-ttu-id="591ff-147">Nach dem Muster Optionen können Sie Einstellungen und Konfigurationen, um Sie voneinander entkoppelt werden, und stellt sicher, liegt im Anschluss an des Controllers [Trennung von Anliegen](http://deviq.com/separation-of-concerns/), da sie nicht wissen, wo oder wie benötigt auf Einstellungen für die gefunden Informationen.</span><span class="sxs-lookup"><span data-stu-id="591ff-147">Following the Options pattern allows settings and configuration to be decoupled from one another, and ensures the controller is following [separation of concerns](http://deviq.com/separation-of-concerns/), since it doesn't need to know how or where to find the settings information.</span></span> <span data-ttu-id="591ff-148">Es auch erleichtert den Controller Komponententest [Controllerlogik testen](testing.md), da es ist keine [Fensterdekorationen](http://deviq.com/static-cling/) oder direkte Instanziierung von für Einstellungenklassen innerhalb der Controllerklasse.</span><span class="sxs-lookup"><span data-stu-id="591ff-148">It also makes the controller easier to unit test [Testing Controller Logic](testing.md), since there is no [static cling](http://deviq.com/static-cling/) or direct instantiation of settings classes within the controller class.</span></span>