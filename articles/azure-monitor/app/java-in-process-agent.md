---
title: Azure Monitor Application Insights Java
description: Monitorowanie wydajności aplikacji dla aplikacji Java działających w dowolnym środowisku bez konieczności modyfikacji kodu. Śledzenie rozproszone i mapa aplikacji.
ms.topic: conceptual
ms.date: 03/29/2020
ms.openlocfilehash: 36e2b419da2bccdf2f5f13227457172cf644994c
ms.sourcegitcommit: 9eda79ea41c60d58a4ceab63d424d6866b38b82d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2020
ms.locfileid: "96351541"
---
# <a name="java-codeless-application-monitoring-azure-monitor-application-insights"></a>Monitorowanie aplikacji bezkodu Java Azure Monitor Application Insights

Monitorowanie aplikacji bez kodu Java ma wszystkie informacje o prostotie — nie ma żadnych zmian w kodzie, a agent Java można włączyć za pomocą tylko kilku zmian konfiguracji.

 Agent Java działa w dowolnym środowisku i umożliwia monitorowanie wszystkich aplikacji Java. Innymi słowy, niezależnie od tego, czy aplikacje języka Java są uruchamiane na maszynach wirtualnych, lokalnie, w AKS, w systemie Windows, Linux — nazwa użytkownika, Agent Java 3,0 będzie monitorować aplikację.

Dodawanie Application Insights Java SDK do aplikacji nie jest już wymagane, ponieważ agent 3,0 automatycznie zbiera żądania, zależności i dzienniki.

Nadal możesz wysyłać niestandardowe dane telemetryczne z aplikacji. Agent 3,0 będzie śledził i skorelowany wraz ze wszystkimi danymi telemetrycznymi, które są zbierane.

Agent 3,0 obsługuje środowisko Java 8 i nowsze.

## <a name="quickstart"></a>Szybki start

**1. Pobierz agenta**

> [!WARNING]
> **W przypadku uaktualniania programu z wersji zapoznawczej 3,0**
>
> Uważnie Przejrzyj wszystkie [Opcje konfiguracji](./java-standalone-config.md) , ponieważ struktura JSON została całkowicie zmieniona, oprócz samej nazwy pliku, która wystąpiła tylko małymi literami.

Pobierz plik [ApplicationInsights-Agent-3.0.0. jar](https://github.com/microsoft/ApplicationInsights-Java/releases/download/3.0.0/applicationinsights-agent-3.0.0.jar)

**2. wskaż JVM do agenta**

Dodaj `-javaagent:path/to/applicationinsights-agent-3.0.0.jar` do ARGUMENTÓW JVM aplikacji

Typowe argumenty JVM obejmują `-Xmx512m` i `-XX:+UseG1GC` . Jeśli wiesz, gdzie je dodać, już wiesz, gdzie je dodać.

Aby uzyskać dodatkową pomoc dotyczącą konfigurowania argumentów JVM aplikacji, zobacz [porady dotyczące aktualizowania ARGUMENTÓW JVM](./java-standalone-arguments.md).

**3. wskaż agenta Application Insights zasobem**

Jeśli nie masz jeszcze zasobu Application Insights, możesz utworzyć nowy, wykonując czynności opisane w [przewodniku tworzenia zasobów](./create-new-resource.md).

Wskaż agenta Application Insights zasobem, ustawiając zmienną środowiskową:

```
APPLICATIONINSIGHTS_CONNECTION_STRING=InstrumentationKey=...
```

Lub tworząc plik konfiguracji o nazwie `applicationinsights.json` i umieszczając go w tym samym katalogu, co `applicationinsights-agent-3.0.0.jar` , z następującą zawartością:

```json
{
  "connectionString": "InstrumentationKey=..."
}
```

Parametry połączenia można znaleźć w zasobie Application Insights:

:::image type="content" source="media/java-ipa/connection-string.png" alt-text="Application Insights parametry połączenia":::

**4. to wszystko!**

Teraz uruchom aplikację i przejdź do zasobu Application Insights w Azure Portal, aby wyświetlić dane monitorowania.

> [!NOTE]
> Wyświetlenie danych monitorowania w portalu może potrwać kilka minut.


## <a name="configuration-options"></a>Opcje konfiguracji

W `applicationinsights.json` pliku można dodatkowo skonfigurować:

* Nazwa roli w chmurze
* Wystąpienie roli w chmurze
* Próbkowanie
* Metryki JMX
* Wymiary niestandardowe
* Procesory telemetrii (wersja zapoznawcza)
* Rejestrowanie z autozbieraniem
* Zbierane metryki Micrometer (w tym metryki uruchamiającego rozruch z sprężyną)
* Puls
* Serwer proxy HTTP
* Samodiagnostyka

Aby uzyskać szczegółowe informacje, zobacz [Opcje konfiguracji](./java-standalone-config.md) .

## <a name="auto-collected-requests-dependencies-logs-and-metrics"></a>Aplikacje zbierane z autogromadzeniem, zależności, dzienniki i metryki

### <a name="requests"></a>Żądania

* JMS konsumenci
* Kafka konsumenci
* Sieci i strumień sieci
* Serwletów
* Planowanie wiosny

### <a name="dependencies-with-distributed-trace-propagation"></a>Zależności z propagacją rozproszonego śledzenia

* Apache HttpClient i HttpAsyncClient
* gRPC
* Java. NET. HttpURLConnection
* JMS
* Kafka
* Klient z sieciami
* OkHttp

### <a name="other-dependencies"></a>Inne zależności

* Cassandra
* JDBC
* MongoDB (asynchroniczne i synchroniczne)
* Redis (sałaty i Jedis)

### <a name="logs"></a>Dzienniki

* Java. util. Logging
* Log4J (łącznie z właściwościami MDC)
* SLF4J/Logback (łącznie z właściwościami MDC)

### <a name="metrics"></a>Metryki

* Micrometer (w tym metryki uruchamiającego uruchamianie sprężynowe)
* Metryki JMX

## <a name="sending-custom-telemetry-from-your-application"></a>Wysyłanie niestandardowych danych telemetrycznych z aplikacji

Naszym celem w programie 3.0 + jest umożliwienie wysyłania niestandardowych danych telemetrycznych przy użyciu standardowych interfejsów API.

Obsługujemy interfejs API Micrometer, OpenTelemetry i popularne struktury rejestrowania. Application Insights Java 3,0 automatycznie przechwytuje dane telemetryczne i skorelowanie ich wraz ze wszystkimi automatycznie zebranymi danymi telemetrycznymi.

### <a name="supported-custom-telemetry"></a>Obsługiwana niestandardowa Telemetria

Poniższa tabela przedstawia obecnie obsługiwane typy niestandardowych danych telemetrycznych, które można włączyć, aby uzupełnić agenta Java 3,0. Podsumowując, metryki niestandardowe są obsługiwane za pomocą micrometer, niestandardowe wyjątki i ślady mogą być włączane za pomocą platform rejestrowania, a dowolny typ telemetrii niestandardowej jest obsługiwany za pomocą [Application Insights Java 2. x SDK](#sending-custom-telemetry-using-application-insights-java-sdk-2x). 

|                     | Mikrometr | Log4J, logback, lip | zestaw SDK 2. x |
|---------------------|------------|---------------------|---------|
| **Zdarzenia niestandardowe**   |            |                     |  Tak    |
| **Metryki niestandardowe**  |  Tak       |                     |  Tak    |
| **Zależności**    |            |                     |  Tak    |
| **Wyjątki**      |            |  Tak                |  Tak    |
| **Wyświetlenia stron**      |            |                     |  Tak    |
| **Żądania**        |            |                     |  Tak    |
| **Ślady**          |            |  Tak                |  Tak    |

W tej chwili nie planujemy zwolnić zestawu SDK z Application Insights 3,0.

Application Insights Java 3,0 już nasłuchuje na danych telemetrycznych wysyłanych do Application Insights Java SDK 2. x. Ta funkcja jest ważną częścią wątku uaktualnienia dla istniejących użytkowników w wersji 2. x i pełni ważną lukę w naszej niestandardowej pomocy technicznej telemetrii do momentu, w którym interfejs API OpenTelemetry jest w całości.

## <a name="sending-custom-telemetry-using-application-insights-java-sdk-2x"></a>Wysyłanie niestandardowej telemetrii przy użyciu Application Insights Java SDK 2. x

Dodaj `applicationinsights-core-2.6.0.jar` do swojej aplikacji (wszystkie wersje 2. x są obsługiwane przez Application Insights Java 3,0, ale warto użyć najnowszej wersji, jeśli masz wybór):

```xml
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-core</artifactId>
    <version>2.6.0</version>
  </dependency>
```

Utwórz TelemetryClient:

  ```java
private static final TelemetryClient telemetryClient = new TelemetryClient();
```

i służy do wysyłania niestandardowych danych telemetrycznych.

### <a name="events"></a>Zdarzenia

  ```java
telemetryClient.trackEvent("WinGame");
```
### <a name="metrics"></a>Metryki

Można wysłać dane telemetryczne metryk za pośrednictwem [Micrometer](https://micrometer.io):

```java
  Counter counter = Metrics.counter("test_counter");
  counter.increment();
```

Można również użyć Application Insights Java SDK 2. x:

```java
  telemetryClient.trackMetric("queueLength", 42.0);
```

### <a name="dependencies"></a>Zależności

```java
  boolean success = false;
  long startTime = System.currentTimeMillis();
  try {
      success = dependency.call();
  } finally {
      long endTime = System.currentTimeMillis();
      RemoteDependencyTelemetry telemetry = new RemoteDependencyTelemetry();
      telemetry.setTimestamp(new Date(startTime));
      telemetry.setDuration(new Duration(endTime - startTime));
      telemetryClient.trackDependency(telemetry);
  }
```

### <a name="logs"></a>Dzienniki
Możesz wysyłać niestandardowe dane telemetryczne dziennika za pośrednictwem ulubionej struktury rejestrowania.

Można również użyć Application Insights Java SDK 2. x:

```java
  telemetryClient.trackTrace(message, SeverityLevel.Warning, properties);
```

### <a name="exceptions"></a>Wyjątki
Możesz wysłać niestandardową telemetrię wyjątku za pośrednictwem ulubionej struktury rejestrowania.

Można również użyć Application Insights Java SDK 2. x:

```java
  try {
      ...
  } catch (Exception e) {
      telemetryClient.trackException(e);
  }
```
