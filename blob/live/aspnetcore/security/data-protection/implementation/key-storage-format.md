---
title: "In Softwareschlüsselspeicher-Format"
author: tdykstra
description: "Dieses Dokument erläutert die Implementierungsdetails für das ASP.NET Core-Schutz-Schlüsselspeicher-Datenformat."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-storage-format
ms.openlocfilehash: 4b796df19349227ceabad185c539720cee7e7c83
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="key-storage-format"></a><span data-ttu-id="6874b-103">In Softwareschlüsselspeicher-Format</span><span class="sxs-lookup"><span data-stu-id="6874b-103">Key Storage Format</span></span>

<a name="data-protection-implementation-key-storage-format"></a>

<span data-ttu-id="6874b-104">Objekte werden im XML-Darstellung im Ruhezustand gespeichert.</span><span class="sxs-lookup"><span data-stu-id="6874b-104">Objects are stored at rest in XML representation.</span></span> <span data-ttu-id="6874b-105">Der Standardname für das Verzeichnis zum Speichern von Schlüsseln ist % LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span><span class="sxs-lookup"><span data-stu-id="6874b-105">The default directory for key storage is %LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span></span>

## <a name="the-key-element"></a><span data-ttu-id="6874b-106">Die \<Schlüssel >-Element</span><span class="sxs-lookup"><span data-stu-id="6874b-106">The \<key> element</span></span>

<span data-ttu-id="6874b-107">Schlüssel, die als Objekte der obersten Ebene im Repository Schlüssel vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6874b-107">Keys exist as top-level objects in the key repository.</span></span> <span data-ttu-id="6874b-108">Gemäß der Konvention Schlüssel verfügen über eine der Dateiname **Schlüssel-{Guid} .xml**, wobei {Guid} die Id des Schlüssels ist.</span><span class="sxs-lookup"><span data-stu-id="6874b-108">By convention keys have the filename **key-{guid}.xml**, where {guid} is the id of the key.</span></span> <span data-ttu-id="6874b-109">Jede dieser Dateien enthält einen einzelnen Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="6874b-109">Each such file contains a single key.</span></span> <span data-ttu-id="6874b-110">Das Format der Datei lautet wie folgt.</span><span class="sxs-lookup"><span data-stu-id="6874b-110">The format of the file is as follows.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<key id="80732141-ec8f-4b80-af9c-c4d2d1ff8901" version="1">
  <creationDate>2015-03-19T23:32:02.3949887Z</creationDate>
  <activationDate>2015-03-19T23:32:02.3839429Z</activationDate>
  <expirationDate>2015-06-17T23:32:02.3839429Z</expirationDate>
  <descriptor deserializerType="{deserializerType}">
    <descriptor>
      <encryption algorithm="AES_256_CBC" />
      <validation algorithm="HMACSHA256" />
      <enc:encryptedSecret decryptorType="{decryptorType}" xmlns:enc="...">
        <encryptedKey>
          <!-- This key is encrypted with Windows DPAPI. -->
          <value>AQAAANCM...8/zeP8lcwAg==</value>
        </encryptedKey>
      </enc:encryptedSecret>
    </descriptor>
  </descriptor>
</key>
```

<span data-ttu-id="6874b-111">Die \<Schlüssel >-Element enthält die folgenden Attribute und untergeordneten Elemente:</span><span class="sxs-lookup"><span data-stu-id="6874b-111">The \<key> element contains the following attributes and child elements:</span></span>

* <span data-ttu-id="6874b-112">Die Schlüssel-ID. Dieser Wert wird als autorisierend behandelt; der Dateiname ist einfach eine äußerst für Menschen lesbar.</span><span class="sxs-lookup"><span data-stu-id="6874b-112">The key id. This value is treated as authoritative; the filename is simply a nicety for human readability.</span></span>

* <span data-ttu-id="6874b-113">Die Version der \<Schlüssel > Element, das zurzeit auf 1 fest.</span><span class="sxs-lookup"><span data-stu-id="6874b-113">The version of the \<key> element, currently fixed at 1.</span></span>

* <span data-ttu-id="6874b-114">Der Schlüssel erstellen, aktivieren und Ablauf von Datumsangaben.</span><span class="sxs-lookup"><span data-stu-id="6874b-114">The key's creation, activation, and expiration dates.</span></span>

* <span data-ttu-id="6874b-115">Ein \<Deskriptor >-Element, das Objektberechtigungsinformationen für die authentifizierten Verschlüsselung-Implementierung, die als Bestandteil dieser Schlüssel enthält.</span><span class="sxs-lookup"><span data-stu-id="6874b-115">A \<descriptor> element, which contains information on the authenticated encryption implementation contained within this key.</span></span>

<span data-ttu-id="6874b-116">Im obigen Beispiel ist der Schlüssel-Id ist {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, erstellt und auf dem 19. März 2015 aktiviert wurde und er verfügt über eine Lebensdauer von 90 Tagen.</span><span class="sxs-lookup"><span data-stu-id="6874b-116">In the above example, the key's id is {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, it was created and activated on March 19, 2015, and it has a lifetime of 90 days.</span></span> <span data-ttu-id="6874b-117">(Gelegentlich möglicherweise das Datum der Aktivierung etwas vor dem Erstellungsdatum erreicht wie in diesem Beispiel liegen.</span><span class="sxs-lookup"><span data-stu-id="6874b-117">(Occasionally the activation date might be slightly before the creation date as in this example.</span></span> <span data-ttu-id="6874b-118">Dies ist aufgrund einer Nit wie die APIs arbeiten, und ist in der Praxis harmlos.)</span><span class="sxs-lookup"><span data-stu-id="6874b-118">This is due to a nit in how the APIs work and is harmless in practice.)</span></span>

## <a name="the-descriptor-element"></a><span data-ttu-id="6874b-119">Die \<Deskriptor >-Element</span><span class="sxs-lookup"><span data-stu-id="6874b-119">The \<descriptor> element</span></span>

<span data-ttu-id="6874b-120">Die äußere \<Deskriptor >-Element enthält ein Attribut-DeserializerType, also der Assembly qualifizierte Name eines Typs der IAuthenticatedEncryptorDescriptorDeserializer implementiert.</span><span class="sxs-lookup"><span data-stu-id="6874b-120">The outer \<descriptor> element contains an attribute deserializerType, which is the assembly-qualified name of a type which implements IAuthenticatedEncryptorDescriptorDeserializer.</span></span> <span data-ttu-id="6874b-121">Dieser Typ ist verantwortlich für das Lesen des inneren \<Deskriptor >-Element und für die Analyse der enthaltenen Informationen.</span><span class="sxs-lookup"><span data-stu-id="6874b-121">This type is responsible for reading the inner \<descriptor> element and for parsing the information contained within.</span></span>

<span data-ttu-id="6874b-122">Bestimmte Format der \<Deskriptor >-Elements hängt von der authentifizierten Encryptor Implementierung gekapselt durch den Schlüssel, und jedes Typs Deserialisierungsprogramm erwartet ein etwas anderes Format für diese.</span><span class="sxs-lookup"><span data-stu-id="6874b-122">The particular format of the \<descriptor> element depends on the authenticated encryptor implementation encapsulated by the key, and each deserializer type expects a slightly different format for this.</span></span> <span data-ttu-id="6874b-123">Im Allgemeinen jedoch dieses Element enthält algorithmische Informationen (Namen, Typen, OIDs oder ähnlich) und Materialien, die für den geheimen Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="6874b-123">In general, though, this element will contain algorithmic information (names, types, OIDs, or similar) and secret key material.</span></span> <span data-ttu-id="6874b-124">Im obigen Beispiel gibt der Deskriptor an, dass dieses Schlüssels dient als Wrapper für Verschlüsselung mit AES-256-CBC + HMACSHA256-Validierung.</span><span class="sxs-lookup"><span data-stu-id="6874b-124">In the above example, the descriptor specifies that this key wraps AES-256-CBC encryption + HMACSHA256 validation.</span></span>

## <a name="the-encryptedsecret-element"></a><span data-ttu-id="6874b-125">Die \<EncryptedSecret >-Element</span><span class="sxs-lookup"><span data-stu-id="6874b-125">The \<encryptedSecret> element</span></span>

<span data-ttu-id="6874b-126">Ein <encryptedSecret> Element enthält die verschlüsselte Form des Schlüsselmaterials geheimen kann vorhanden sein, wenn [ist die Verschlüsselung von geheimen Schlüsseln im Ruhezustand aktiviert](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest).</span><span class="sxs-lookup"><span data-stu-id="6874b-126">An <encryptedSecret> element which contains the encrypted form of the secret key material may be present if [encryption of secrets at rest is enabled](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest).</span></span> <span data-ttu-id="6874b-127">Das Attribut DecryptorType werden die Assembly qualifizierte Name eines Typs der IXmlDecryptor implementiert.</span><span class="sxs-lookup"><span data-stu-id="6874b-127">The attribute decryptorType will be the assembly-qualified name of a type which implements IXmlDecryptor.</span></span> <span data-ttu-id="6874b-128">Dieser Typ ist verantwortlich für das Lesen des inneren <encryptedKey> Element- und entschlüsseln, um den ursprünglichen Klartext zu gewinnen.</span><span class="sxs-lookup"><span data-stu-id="6874b-128">This type is responsible for reading the inner <encryptedKey> element and decrypting it to recover the original plaintext.</span></span>

<span data-ttu-id="6874b-129">Wie bei \<Deskriptor >, die bestimmten Format der <encryptedSecret> -Elements hängt von der-ruhender Verschlüsselungsmechanismus verwendet.</span><span class="sxs-lookup"><span data-stu-id="6874b-129">As with \<descriptor>, the particular format of the <encryptedSecret> element depends on the at-rest encryption mechanism in use.</span></span> <span data-ttu-id="6874b-130">Im obigen Beispiel wird der Hauptschlüssel verschlüsselt unter Verwendung von Windows DPAPI pro des Kommentars.</span><span class="sxs-lookup"><span data-stu-id="6874b-130">In the above example, the master key is encrypted using Windows DPAPI per the comment.</span></span>

## <a name="the-revocation-element"></a><span data-ttu-id="6874b-131">Die \<Revocation >-Element</span><span class="sxs-lookup"><span data-stu-id="6874b-131">The \<revocation> element</span></span>

<span data-ttu-id="6874b-132">Revocations, die als Objekte der obersten Ebene im Repository Schlüssel vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6874b-132">Revocations exist as top-level objects in the key repository.</span></span> <span data-ttu-id="6874b-133">Gemäß der Konvention verfügen Revocations den Dateinamen **Revocation-{Zeitstempel} .xml** (für aufheben aller Schlüssel vor einem bestimmten Datum) oder **Revocation-{Guid} .xml** (für das Sperren eines bestimmten Schlüssels).</span><span class="sxs-lookup"><span data-stu-id="6874b-133">By convention revocations have the filename **revocation-{timestamp}.xml** (for revoking all keys before a specific date) or **revocation-{guid}.xml** (for revoking a specific key).</span></span> <span data-ttu-id="6874b-134">Jede Datei enthält ein einziges \<Revocation > Element.</span><span class="sxs-lookup"><span data-stu-id="6874b-134">Each file contains a single \<revocation> element.</span></span>

<span data-ttu-id="6874b-135">Für Revocations der einzelnen Schlüssel, den Inhalt der Datei werden folgendermaßen aus.</span><span class="sxs-lookup"><span data-stu-id="6874b-135">For revocations of individual keys, the file contents will be as below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T22:45:30.2616742Z</revocationDate>
  <key id="eb4fc299-8808-409d-8a34-23fc83d026c9" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="6874b-136">In diesem Fall wird nur der angegebene Schlüssel gesperrt.</span><span class="sxs-lookup"><span data-stu-id="6874b-136">In this case, only the specified key is revoked.</span></span> <span data-ttu-id="6874b-137">Wenn die Schlüssel-Id ist "\*", jedoch wie in der folgenden Beispiel werden alle Schlüssel, deren Datum vor dem angegebenen Sperrdatum ist, gesperrt.</span><span class="sxs-lookup"><span data-stu-id="6874b-137">If the key id is "\*", however, as in the below example, all keys whose creation date is prior to the specified revocation date are revoked.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T15:45:45.7366491-07:00</revocationDate>
  <!-- All keys created before the revocation date are revoked. -->
  <key id="*" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="6874b-138">Die \<Grund > Element wird vom System nie gelesen.</span><span class="sxs-lookup"><span data-stu-id="6874b-138">The \<reason> element is never read by the system.</span></span> <span data-ttu-id="6874b-139">Es ist einfach eine bequeme Möglichkeit, eine lesbare Ursache für die Sperrung zu speichern.</span><span class="sxs-lookup"><span data-stu-id="6874b-139">It is simply a convenient place to store a human-readable reason for revocation.</span></span>