---
title: Samodzielnie śledzenia jednostek - EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: 5e60f5be-7bbb-4bf8-835e-0ac808d6c84a
caps.latest.revision: 3
ms.openlocfilehash: 2fb4e9f4d4008c57e90c49a011bebb320eb2bb58
ms.sourcegitcommit: 45494121254ad4fdcec613d1dd22d850068d6f39
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2018
ms.locfileid: "37913528"
---
# <a name="self-tracking-entities"></a><span data-ttu-id="e0a54-102">Samodzielnie śledzenia jednostek</span><span class="sxs-lookup"><span data-stu-id="e0a54-102">Self-tracking entities</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a54-103">Nie zaleca się przy użyciu szablonu samoobsługowego tracking jednostek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-103">We no longer recommend using the self-tracking-entities template.</span></span> <span data-ttu-id="e0a54-104">Tylko będą dostępne do obsługi istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0a54-104">It will only continue to be available to support existing applications.</span></span> <span data-ttu-id="e0a54-105">Jeśli aplikacja wymaga pracy z wykresami odłączonych jednostek, należy wziąć pod uwagę inne alternatywy dla takich jak [słupkowych jednostek](http://trackableentities.github.io/), która jest podobna do samoobsługowego-Tracking-jednostek, które jest bardziej aktywnie rozwijany przez technologię Społeczność lub pisanie kodu niestandardowego za pomocą śledzenia interfejsów API zmian niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="e0a54-105">If your application requires working with disconnected graphs of entities, consider other alternatives such as [Trackable Entities](http://trackableentities.github.io/), which is a technology similar to Self-Tracking-Entities that is more actively developed by the community, or writing custom code using the low-level change tracking APIs.</span></span>

<span data-ttu-id="e0a54-106">W aplikacji Entity Framework, na podstawie kontekstu jest odpowiedzialny za śledzenie zmian w obiekty.</span><span class="sxs-lookup"><span data-stu-id="e0a54-106">In an Entity Framework-based application, a context is responsible for tracking changes in your objects.</span></span> <span data-ttu-id="e0a54-107">Możesz następnie użyć metody SaveChanges aby utrwalić zmiany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e0a54-107">You then use the SaveChanges method to persist the changes to the database.</span></span> <span data-ttu-id="e0a54-108">Podczas pracy z aplikacjami N-warstwowej, obiekty jednostki zwykle jest odłączony od kontekstu i należy zdecydować, jak śledzić zmiany i raportu te zmiany do kontekstu.</span><span class="sxs-lookup"><span data-stu-id="e0a54-108">When working with N-Tier applications, the entity objects are usually disconnected from the context and you must decide how to track changes and report those changes back to the context.</span></span> <span data-ttu-id="e0a54-109">Samodzielnie śledzenia jednostek (ste) może pomóc śledzić zmiany w dowolnej warstwy, a następnie odtworzenia te zmiany do kontekstu do zapisania.</span><span class="sxs-lookup"><span data-stu-id="e0a54-109">Self-Tracking Entities (STEs) can help you track changes in any tier and then replay these changes into a context to be saved.</span></span>  

<span data-ttu-id="e0a54-110">Użyj ste tylko wtedy, gdy kontekst nie jest dostępna w ramach warstwy gdzie zostały wprowadzone zmiany do obiektu wykresu.</span><span class="sxs-lookup"><span data-stu-id="e0a54-110">Use STEs only if the context is not available on a tier where the changes to the object graph are made.</span></span> <span data-ttu-id="e0a54-111">Jeśli kontekst jest dostępny, nie ma potrzeby używania ste, ponieważ zajmie się kontekst śledzenia zmian.</span><span class="sxs-lookup"><span data-stu-id="e0a54-111">If the context is available, there is no need to use STEs because the context will take care of tracking changes.</span></span>  

<span data-ttu-id="e0a54-112">Ten element szablon generuje dwa .TT — pliki (szablon tekstowy):</span><span class="sxs-lookup"><span data-stu-id="e0a54-112">This template item generates two .tt (text template) files:</span></span>  

- <span data-ttu-id="e0a54-113">** \<Nazwę modelu\>.tt** generuje plik typów jednostek i klasa pomocnika, która zawiera logikę śledzenia zmian, która jest używana przez własny śledzenia jednostek i metody rozszerzenia, które umożliwiają ustawianie stanu na własnym śledzenie jednostki.</span><span class="sxs-lookup"><span data-stu-id="e0a54-113">The **\<model name\>.tt** file generates the entity types and a helper class that contains the change-tracking logic that is used by self-tracking entities and the extension methods that allow setting state on self-tracking entities.</span></span>  
- <span data-ttu-id="e0a54-114">** \<Nazwę modelu\>. Context.TT** generuje plik pochodnej kontekstu i klasa rozszerzenia, która zawiera **applychanges —** metody **ObjectContext** i **obiektu ObjectSet** klasy.</span><span class="sxs-lookup"><span data-stu-id="e0a54-114">The **\<model name\>.Context.tt** file generates a derived context and an extension class that contains **ApplyChanges** methods for the **ObjectContext** and **ObjectSet** classes.</span></span> <span data-ttu-id="e0a54-115">Te metody zbadania informacji śledzenia zmian, które znajduje się na wykresie własnym śledzenia jednostek wywnioskowania zestaw operacji, które należy wykonać, aby zapisać zmiany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e0a54-115">These methods examine the change-tracking information that is contained in the graph of self-tracking entities to infer the set of operations that must be performed to save the changes in the database.</span></span>  

## <a name="get-started"></a><span data-ttu-id="e0a54-116">Rozpocznij</span><span class="sxs-lookup"><span data-stu-id="e0a54-116">Get Started</span></span>  

<span data-ttu-id="e0a54-117">Aby rozpocząć pracę, odwiedź stronę [Self-Tracking jednostek wskazówki](walkthrough.md) strony.</span><span class="sxs-lookup"><span data-stu-id="e0a54-117">To get started, visit the [Self-Tracking Entities Walkthrough](walkthrough.md) page.</span></span>  

## <a name="considerations-when-working-with-self-tracking-entities"></a><span data-ttu-id="e0a54-118">Zagadnienia dotyczące pracy z własnym śledzenia jednostek</span><span class="sxs-lookup"><span data-stu-id="e0a54-118">Considerations When Working with Self-Tracking Entities</span></span>  
> [!IMPORTANT]
> <span data-ttu-id="e0a54-119">Nie zaleca się przy użyciu szablonu samoobsługowego tracking jednostek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-119">We no longer recommend using the self-tracking-entities template.</span></span> <span data-ttu-id="e0a54-120">Tylko będą dostępne do obsługi istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0a54-120">It will only continue to be available to support existing applications.</span></span> <span data-ttu-id="e0a54-121">Jeśli aplikacja wymaga pracy z wykresami odłączonych jednostek, należy wziąć pod uwagę inne alternatywy dla takich jak [słupkowych jednostek](http://trackableentities.github.io/), która jest podobna do samoobsługowego-Tracking-jednostek, które jest bardziej aktywnie rozwijany przez technologię Społeczność lub pisanie kodu niestandardowego za pomocą śledzenia interfejsów API zmian niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="e0a54-121">If your application requires working with disconnected graphs of entities, consider other alternatives such as [Trackable Entities](http://trackableentities.github.io/), which is a technology similar to Self-Tracking-Entities that is more actively developed by the community, or writing custom code using the low-level change tracking APIs.</span></span>

<span data-ttu-id="e0a54-122">Podczas pracy z własnym śledzenie jednostek, należy wziąć pod uwagę następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e0a54-122">Consider the following when working with self-tracking entities:</span></span>  

- <span data-ttu-id="e0a54-123">Upewnij się, że projekt klienta ma odwołanie do zestawu zawierającego typów jednostek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-123">Make sure that your client project has a reference to the assembly containing the entity types.</span></span> <span data-ttu-id="e0a54-124">Jeśli dodasz tylko odwołanie do usługi do projektu klienta, projekt klienta użyje typy serwerów proxy usługi WCF i nie rzeczywiste własnym śledzenie typów jednostek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-124">If you add only the service reference to the client project, the client project will use the WCF proxy types and not the actual self-tracking entity types.</span></span> <span data-ttu-id="e0a54-125">Oznacza to, że nie będzie można uzyskać funkcji automatyczne powiadomienie o zarządzających śledzenia jednostki na kliencie.</span><span class="sxs-lookup"><span data-stu-id="e0a54-125">This means that you will not get the automated notification features that manage the tracking of the entities on the client.</span></span> <span data-ttu-id="e0a54-126">Jeśli nie chcesz jej celowo i obejmuje dodatkowe typy jednostek, należy ręcznie ustawić informacji śledzenia zmian na klienta, aby zmiany wysyłane z powrotem do usługi.</span><span class="sxs-lookup"><span data-stu-id="e0a54-126">If you intentionally do not want to include the entity types, you will have to manually set change-tracking information on the client for the changes to be sent back to the service.</span></span>  
- <span data-ttu-id="e0a54-127">Wywołania operacji usługi powinny być bezstanowe i Utwórz nowe wystąpienie obiektu kontekstu.</span><span class="sxs-lookup"><span data-stu-id="e0a54-127">Calls to the service operation should be stateless and create a new instance of object context.</span></span> <span data-ttu-id="e0a54-128">Zalecamy również utworzenie obiektu kontekstu w **przy użyciu** bloku.</span><span class="sxs-lookup"><span data-stu-id="e0a54-128">We also recommend that you create object context in a **using** block.</span></span>  
- <span data-ttu-id="e0a54-129">Kiedy wykres, który został zmodyfikowany na kliencie z usługą i wysyła następnie zamierzasz kontynuować pracę z tym samym wykresie na komputerze klienckim, należy ręcznie wykonać iterację wykresu i wywołania **AcceptChanges** metody dla każdego obiektu do Zresetuj śledzenie zmian.</span><span class="sxs-lookup"><span data-stu-id="e0a54-129">When you send the graph that was modified on the client to the service and then intend to continue working with the same graph on the client, you have to manually iterate through the graph and call the **AcceptChanges** method on each object to reset the change tracker.</span></span>  

    > <span data-ttu-id="e0a54-130">Jeśli obiekty w grafie zawierają właściwości wartościami wygenerowanych w bazie danych (na przykład wartości tożsamości lub współbieżności), platformy Entity Framework spowoduje zastąpienie wartości tych właściwości z wartościami bazy danych, wygenerowane po **SaveChanges** metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="e0a54-130">If objects in your graph contain properties with database-generated values (for example, identity or concurrency values), Entity Framework will replace values of these properties with the database-generated values after the **SaveChanges** method is called.</span></span> <span data-ttu-id="e0a54-131">Możesz zaimplementować operację usługi do zwrócenia zapisanych obiektów lub Podaj listę wartości wygenerowanej właściwości dla obiektów do klienta.</span><span class="sxs-lookup"><span data-stu-id="e0a54-131">You can implement your service operation to return saved objects or a list of generated property values for the objects back to the client.</span></span> <span data-ttu-id="e0a54-132">Klient musiałby Zamień wystąpień obiektów lub wartości właściwości obiektu do obiektów lub wartości właściwości zwrócony przez operację usługi.</span><span class="sxs-lookup"><span data-stu-id="e0a54-132">The client would then need to replace the object instances or object property values with the objects or property values returned from the service operation.</span></span>  
- <span data-ttu-id="e0a54-133">Scalanie wykresów z wielu żądań usługi może stanowić obiekty ze zduplikowanymi wartościami klucza w wynikowym wykresie.</span><span class="sxs-lookup"><span data-stu-id="e0a54-133">Merging graphs from multiple service requests may introduce objects with duplicate key values in the resulting graph.</span></span> <span data-ttu-id="e0a54-134">Entity Framework nie powoduje usunięcia obiektów z zduplikowane klucze po wywołaniu **applychanges —** metody, ale zamiast tego zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-134">Entity Framework does not remove the objects with duplicate keys when you call the **ApplyChanges** method but instead throws an exception.</span></span> <span data-ttu-id="e0a54-135">Aby uniknąć wykresy ze zduplikowanymi wartościami klucza, postępuj zgodnie z jednym z wzorców opisanego w następujący wpis w blogu: [jednostek Self-Tracking: applychanges — i zduplikowanych podmiotów](http://go.microsoft.com/fwlink/?LinkID=205119&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e0a54-135">To avoid having graphs with duplicate key values follow one of the patterns described in the following blog: [Self-Tracking Entities: ApplyChanges and duplicate entities](http://go.microsoft.com/fwlink/?LinkID=205119&clcid=0x409).</span></span>  
- <span data-ttu-id="e0a54-136">Po zmianie relacji między obiektami, ustawiając właściwość klucza obcego referencyjna właściwość nawigacji jest ustawiona na wartość null i nie są zsynchronizowane do odpowiedniej jednostki podmiotu zabezpieczeń na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="e0a54-136">When you change the relationship between objects by setting the foreign key property, the reference navigation property is set to null and not synchronized to the appropriate principal entity on the client.</span></span> <span data-ttu-id="e0a54-137">Po dołączeniu do kontekstu obiektów programu graph (na przykład, po wywołaniu metody **applychanges —** metoda), właściwości klucza obcego i właściwości nawigacji są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="e0a54-137">After the graph is attached to the object context (for example, after you call the **ApplyChanges** method), the foreign key properties and navigation properties are synchronized.</span></span>  

    > <span data-ttu-id="e0a54-138">Nie ma właściwości nawigacji odwołania synchronizowane z odpowiedniego obiektu podmiotu zabezpieczeń może być problem, jeśli określono usuwanie kaskadowe w relacji klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="e0a54-138">Not having a reference navigation property synchronized with the appropriate principal object could be an issue if you have specified cascade delete on the foreign key relationship.</span></span> <span data-ttu-id="e0a54-139">Jeśli usuniesz główny, Usuń nie będą przekazywane do obiektów zależnych.</span><span class="sxs-lookup"><span data-stu-id="e0a54-139">If you delete the principal, the delete will not be propagated to the dependent objects.</span></span> <span data-ttu-id="e0a54-140">Jeśli masz kaskadowo określony, należy użyć właściwości nawigacji, aby zmienić relacji zamiast ustawiać właściwości klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="e0a54-140">If you have cascade deletes specified, use navigation properties to change relationships instead of setting the foreign key property.</span></span>  
- <span data-ttu-id="e0a54-141">Samodzielnie śledzenie jednostek nie są włączone do wykonywania ładowania z opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="e0a54-141">Self-tracking entities are not enabled to perform lazy loading.</span></span>  
- <span data-ttu-id="e0a54-142">Serializacja binarna i serializacji obiektów zarządzania stan programu ASP.NET nie jest obsługiwane przez własny śledzenie jednostek.</span><span class="sxs-lookup"><span data-stu-id="e0a54-142">Binary serialization and serialization to ASP.NET state management objects is not supported by self-tracking entities.</span></span> <span data-ttu-id="e0a54-143">Można jednak dostosować szablon, aby dodać obsługę serializacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="e0a54-143">However, you can customize the template to add the binary serialization support.</span></span> <span data-ttu-id="e0a54-144">Aby uzyskać więcej informacji, zobacz [za pomocą serializacji binarnej i ViewState z jednostkami Self-Tracking](http://go.microsoft.com/fwlink/?LinkId=199208).</span><span class="sxs-lookup"><span data-stu-id="e0a54-144">For more information, see [Using Binary Serialization and ViewState with Self-Tracking Entities](http://go.microsoft.com/fwlink/?LinkId=199208).</span></span>  

### <a name="security-considerations"></a><span data-ttu-id="e0a54-145">Zagadnienia dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e0a54-145">Security Considerations</span></span>  

<span data-ttu-id="e0a54-146">Następujące zagadnienia dotyczące zabezpieczeń powinny brane pod uwagę podczas pracy z własnym śledzenie jednostki:</span><span class="sxs-lookup"><span data-stu-id="e0a54-146">The following security considerations should be taken into account when working with self-tracking entities:</span></span>  

- <span data-ttu-id="e0a54-147">Usługa nie należy ufać żądań kierowanych do pobrania lub aktualizowanie danych w kliencie niezaufanej lub za pośrednictwem niezaufanej kanału.</span><span class="sxs-lookup"><span data-stu-id="e0a54-147">A service should not trust requests to retrieve or update data from a non-trusted client or through a non-trusted channel.</span></span> <span data-ttu-id="e0a54-148">Klient musi zostać uwierzytelniony: bezpieczne koperty kanału lub komunikat powinien być używany.</span><span class="sxs-lookup"><span data-stu-id="e0a54-148">A client must be authenticated: a secure channel or message envelope should be used.</span></span> <span data-ttu-id="e0a54-149">Aby upewnić się, że są one zgodne z oczekiwaniami i jest uzasadnione zmiany dla danego scenariusza, można sprawdzić poprawności żądania klientów do aktualizacji lub odbierać dane.</span><span class="sxs-lookup"><span data-stu-id="e0a54-149">Clients' requests to update or retrieve data must be validated to ensure they conform to expected and legitimate changes for the given scenario.</span></span>  
- <span data-ttu-id="e0a54-150">Należy unikać poufnych informacji jako klucze jednostek (na przykład numery ubezpieczenia społecznego).</span><span class="sxs-lookup"><span data-stu-id="e0a54-150">Avoid using sensitive information as entity keys (for example, social security numbers).</span></span> <span data-ttu-id="e0a54-151">Zmniejsza to możliwość przypadkowo szeregowania informacje poufne na własnym śledzenie wykresy jednostki do klienta, który nie jest w pełni zaufany.</span><span class="sxs-lookup"><span data-stu-id="e0a54-151">This mitigates the possibility of inadvertently serializing sensitive information in the self-tracking entity graphs to a client that is not fully trusted.</span></span> <span data-ttu-id="e0a54-152">Za pomocą skojarzeń niezależnie od oryginalnego klucza podmiotu, który jest powiązany z tą, która jest deserializowana mogą zostać wysłane do klienta, jak również.</span><span class="sxs-lookup"><span data-stu-id="e0a54-152">With independent associations, the original key of an entity that is related to the one that is being serialized might be sent to the client as well.</span></span>  
- <span data-ttu-id="e0a54-153">Aby uniknąć propagowanie komunikaty o wyjątkach, zawierających poufne dane w warstwie klienta wywołania **applychanges —** i **SaveChanges** na serwerze warstwy musi być ujęte w kodzie obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="e0a54-153">To avoid propagating exception messages that contain sensitive data to the client tier, calls to **ApplyChanges** and **SaveChanges** on the server tier should be wrapped in exception-handling code.</span></span>  