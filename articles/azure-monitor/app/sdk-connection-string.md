---
title: Parametry połączenia na platformie Azure Application Insights | Microsoft Docs
description: Jak używać parametrów połączenia.
ms.topic: conceptual
author: timothymothra
ms.author: tilee
ms.date: 01/17/2020
ms.custom: devx-track-js, devx-track-csharp
ms.reviewer: mbullwin
ms.openlocfilehash: df87b060423aeff9fa5f83f21634395fe30e0bbb
ms.sourcegitcommit: 8d1b97c3777684bd98f2cfbc9d440b1299a02e8f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/09/2021
ms.locfileid: "102486288"
---
# <a name="connection-strings"></a>Parametry połączeń

## <a name="overview"></a>Omówienie

Parametry połączenia zapewniają użytkownikom usługi Application Insights jedno ustawienie konfiguracji, eliminując konieczność stosowania wielu ustawień serwera proxy. Wysoce przydatne w przypadku intranetowych serwerów sieci Web, suwerennych lub hybrydowych środowisk w chmurze, które chcą wysyłać dane do usługi monitorowania.

Pary klucz wartość umożliwiają użytkownikom łatwe definiowanie kombinacji sufiksu prefiksu dla każdej usługi Application Insights (AI)/produktu.

> [!IMPORTANT]
> Nie zalecamy ustawiania parametrów połączenia i klucza Instrumentacji. W przypadku, gdy użytkownik ustawił oba elementy, w zależności od ustawienia ustawiono pierwszeństwo. 


## <a name="scenario-overview"></a>Omówienie scenariusza 

Scenariusze klientów, które są wizualizowane z największym wpływem:

- Wyjątki zapory lub przekierowania serwera proxy 

    W przypadkach, gdy wymagane jest monitorowanie intranetowego serwera sieci Web, nasze wcześniejsze rozwiązanie poprosiło klientów o dodanie poszczególnych punktów końcowych usługi do konfiguracji. Aby uzyskać więcej informacji, zobacz [tutaj](../faq.md#can-i-monitor-an-intranet-web-server). 
    Parametry połączenia oferują lepszą alternatywę, skracając ten nakład pracy do jednego ustawienia. Prosty prefiks, zmiana sufiksu, umożliwia automatyczne zapełnianie i przekierowywanie wszystkich punktów końcowych do odpowiednich usług. 

- Suwerenne lub hybrydowe środowiska chmury

    Użytkownicy mogą wysyłać dane do zdefiniowanego [regionu Azure Government](../../azure-government/compare-azure-government-global-azure.md#application-insights).
    Parametry połączeń umożliwiają definiowanie ustawień punktu końcowego dla serwerów intranetowych lub ustawień chmury hybrydowej. 

## <a name="getting-started"></a>Wprowadzenie

### <a name="finding-my-connection-string"></a>Szukasz moich parametrów połączenia?

Parametry połączenia są wyświetlane w bloku przegląd zasobu Application Insights.

![parametry połączenia w bloku przeglądu](media/overview-dashboard/overview-connection-string.png)

### <a name="schema"></a>Schemat

#### <a name="max-length"></a>Długość maksymalna

Połączenie ma maksymalną obsługiwaną długość wynoszącą 4096 znaków.

#### <a name="key-value-pairs"></a>Pary klucz-wartość

Parametry połączenia składają się z listy ustawień reprezentowanych jako pary klucz-wartość oddzielone średnikami: `key1=value1;key2=value2;key3=value3`

#### <a name="syntax"></a>Składnia

- `InstrumentationKey` (np.: 00000000-0000-0000-0000-000000000000)  Ciąg połączenia jest polem **wymaganym** .
- `Authorization` (np.: iKey) (To ustawienie jest opcjonalne, ponieważ dzisiaj obsługujemy tylko autoryzację iKey).
- `EndpointSuffix` (np.: applicationinsights.azure.cn) Ustawienie sufiksu punktu końcowego spowoduje nawiązanie połączenia z zestawem SDK z chmurą platformy Azure. Zestaw SDK będzie gromadzić pozostałe punkty końcowe dla poszczególnych usług.
- Jawne punkty końcowe.
  Każdą usługę można jawnie przesłaniać w parametrach połączenia.
   - `IngestionEndpoint` (np.: `https://dc.applicationinsights.azure.com` )
   - `LiveEndpoint` (np.: `https://live.applicationinsights.azure.com` )
   - `ProfilerEndpoint` (np.: `https://profiler.monitor.azure.com` )
   - `SnapshotEndpoint` (np.: `https://snapshot.monitor.azure.com` )

#### <a name="endpoint-schema"></a>Schemat punktu końcowego

`<prefix>.<suffix>`
- Prefiks: Określa usługę. 
- Sufiks: definiuje wspólną nazwę domeny.

##### <a name="valid-suffixes"></a>Prawidłowe sufiksy

Oto lista prawidłowych sufiksów 
- applicationinsights.azure.cn
- applicationinsights.us


Zobacz również: https://docs.microsoft.com/azure/azure-monitor/app/custom-endpoints#regions-that-require-endpoint-modification


##### <a name="valid-prefixes"></a>Prawidłowe prefiksy

- Pozyskiwanie danych [telemetrycznych](./app-insights-overview.md):`dc`
- [Metryki na żywo](./live-stream.md): `live`
- [Profiler](./profiler-overview.md): `profiler`
- [Migawka](./snapshot-debugger.md): `snapshot`



## <a name="connection-string-examples"></a>Przykłady parametrów połączenia


### <a name="minimal-valid-connection-string"></a>Minimalne prawidłowe parametry połączenia

`InstrumentationKey=00000000-0000-0000-0000-000000000000;`

W tym przykładzie ustawiono tylko klucz Instrumentacji.

- Domyślna wartość schematu autoryzacji to "iKey" 
- Klucz Instrumentacji: 00000000-0000-0000-0000-000000000000
- Identyfikatory URI usługi regionalnej są oparte na [ustawieniach domyślnych zestawu SDK](https://github.com/microsoft/ApplicationInsights-dotnet/blob/develop/BASE/src/Microsoft.ApplicationInsights/Extensibility/Implementation/Endpoints/Constants.cs) i łączą się z publiczną globalną platformą Azure:
   - Pozyskiwania `https://dc.services.visualstudio.com/`
   - Metryki na żywo: `https://rt.services.visualstudio.com/`
   - Profilera `https://profiler.monitor.azure.com/`
   - Oknie `https://snapshot.monitor.azure.com/`



### <a name="connection-string-with-endpoint-suffix"></a>Parametry połączenia z sufiksem punktu końcowego

`InstrumentationKey=00000000-0000-0000-0000-000000000000;EndpointSuffix=ai.contoso.com;`

W tym przykładzie parametry połączenia określają sufiks punktu końcowego, a zestaw SDK będzie konstruować punkty końcowe usługi.

- Domyślna wartość schematu autoryzacji to "iKey" 
- Klucz Instrumentacji: 00000000-0000-0000-0000-000000000000
- Identyfikatory URI usługi regionalnej są oparte na podanym sufiksie punktu końcowego: 
   - Pozyskiwania `https://dc.ai.contoso.com`
   - Metryki na żywo: `https://live.ai.contoso.com`
   - Profilera `https://profiler.ai.contoso.com`
   - Oknie `https://snapshot.ai.contoso.com`  



### <a name="connection-string-with-explicit-endpoint-overrides"></a>Parametry połączenia z jawnym zastąpień punktu końcowego 

`InstrumentationKey=00000000-0000-0000-0000-000000000000;IngestionEndpoint=https://custom.com:111/;LiveEndpoint=https://custom.com:222/;ProfilerEndpoint=https://custom.com:333/;SnapshotEndpoint=https://custom.com:444/;`

W tym przykładzie parametry połączenia określają jawne zastąpienia dla każdej usługi. Zestaw SDK będzie używać dokładnych punktów końcowych, które nie są modyfikowane.

- Domyślna wartość schematu autoryzacji to "iKey" 
- Klucz Instrumentacji: 00000000-0000-0000-0000-000000000000
- Identyfikatory URI usługi regionalnej są oparte na wartościach jawnego zastąpienia: 
   - Pozyskiwania `https://custom.com:111/`
   - Metryki na żywo: `https://custom.com:222/`
   - Profilera `https://custom.com:333/`
   - Oknie `https://custom.com:444/`  


## <a name="how-to-set-a-connection-string"></a>Jak ustawić parametry połączenia

Parametry połączenia są obsługiwane w następujących wersjach zestawu SDK:
- .NET i .NET Core v 2.12.0
- Java v, 2.5.1 i Java 3,0
- 2.3.0 JavaScript v
- NodeJS v 1.5.0
- 1.0.0 Python v

Parametry połączenia można ustawić za pomocą kodu, zmiennej środowiskowej lub pliku konfiguracji.



### <a name="environment-variable"></a>Zmienna środowiskowa

- Parametry połączenia: `APPLICATIONINSIGHTS_CONNECTION_STRING`

### <a name="code-samples"></a>Przykłady kodu

# <a name="netnetcore"></a>[.NET/. Core](#tab/net)

Ustaw właściwość [TelemetryConfiguration. ConnectionString](https://github.com/microsoft/ApplicationInsights-dotnet/blob/add45ceed35a817dc7202ec07d3df1672d1f610d/BASE/src/Microsoft.ApplicationInsights/Extensibility/TelemetryConfiguration.cs#L271-L274) lub [ApplicationInsightsServiceOptions. ConnectionString](https://github.com/microsoft/ApplicationInsights-dotnet/blob/81288f26921df1e8e713d31e7e9c2187ac9e6590/NETCORE/src/Shared/Extensions/ApplicationInsightsServiceOptions.cs#L66-L69)

Zestaw .NET jawnie ustawiony:
```csharp
var configuration = new TelemetryConfiguration
{
    ConnectionString = "InstrumentationKey=00000000-0000-0000-0000-000000000000;"
};
```

Plik konfiguracji .NET:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings">
    <ConnectionString>InstrumentationKey=00000000-0000-0000-0000-000000000000</ConnectionString>
</ApplicationInsights>
```

Zestaw w sposób jawny:
```csharp
public void ConfigureServices(IServiceCollection services)
{
    var options = new ApplicationInsightsServiceOptions { ConnectionString = "InstrumentationKey=00000000-0000-0000-0000-000000000000;" };
    services.AddApplicationInsightsTelemetry(options: options);
}
```

Podstawowe config.jsw: 

```json
{
  "ApplicationInsights": {
    "ConnectionString" : "InstrumentationKey=00000000-0000-0000-0000-000000000000;"
    }
  }
```


# <a name="java"></a>[Java](#tab/java)


Język Java (v 2.5. x) jawnie ustawiony:
```java
TelemetryConfiguration.getActive().setConnectionString("InstrumentationKey=00000000-0000-0000-0000-000000000000");
```

ApplicationInsights.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings">
    <ConnectionString>InstrumentationKey=00000000-0000-0000-0000-000000000000;</ConnectionString>
</ApplicationInsights>
```

# <a name="javascript"></a>[JavaScript](#tab/js)

Ważne: język JavaScript nie obsługuje użycia zmiennych środowiskowych.

Za pomocą fragmentu kodu:

Bieżący fragment kodu (wymieniony poniżej) jest w wersji "5". wersja jest zaszyfrowana w fragmencie kodu jako OHR: "#", a [Bieżąca wersja jest również dostępna w witrynie GitHub](https://go.microsoft.com/fwlink/?linkid=2156318).

```html
<script type="text/javascript">
!function(T,l,y){var S=T.location,k="script",D="instrumentationKey",C="ingestionendpoint",I="disableExceptionTracking",E="ai.device.",b="toLowerCase",w="crossOrigin",N="POST",e="appInsightsSDK",t=y.name||"appInsights";(y.name||T[e])&&(T[e]=t);var n=T[t]||function(d){var g=!1,f=!1,m={initialize:!0,queue:[],sv:"5",version:2,config:d};function v(e,t){var n={},a="Browser";return n[E+"id"]=a[b](),n[E+"type"]=a,n["ai.operation.name"]=S&&S.pathname||"_unknown_",n["ai.internal.sdkVersion"]="javascript:snippet_"+(m.sv||m.version),{time:function(){var e=new Date;function t(e){var t=""+e;return 1===t.length&&(t="0"+t),t}return e.getUTCFullYear()+"-"+t(1+e.getUTCMonth())+"-"+t(e.getUTCDate())+"T"+t(e.getUTCHours())+":"+t(e.getUTCMinutes())+":"+t(e.getUTCSeconds())+"."+((e.getUTCMilliseconds()/1e3).toFixed(3)+"").slice(2,5)+"Z"}(),iKey:e,name:"Microsoft.ApplicationInsights."+e.replace(/-/g,"")+"."+t,sampleRate:100,tags:n,data:{baseData:{ver:2}}}}var h=d.url||y.src;if(h){function a(e){var t,n,a,i,r,o,s,c,u,p,l;g=!0,m.queue=[],f||(f=!0,t=h,s=function(){var e={},t=d.connectionString;if(t)for(var n=t.split(";"),a=0;a<n.length;a++){var i=n[a].split("=");2===i.length&&(e[i[0][b]()]=i[1])}if(!e[C]){var r=e.endpointsuffix,o=r?e.location:null;e[C]="https://"+(o?o+".":"")+"dc."+(r||"services.visualstudio.com")}return e}(),c=s[D]||d[D]||"",u=s[C],p=u?u+"/v2/track":d.endpointUrl,(l=[]).push((n="SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details)",a=t,i=p,(o=(r=v(c,"Exception")).data).baseType="ExceptionData",o.baseData.exceptions=[{typeName:"SDKLoadFailed",message:n.replace(/\./g,"-"),hasFullStack:!1,stack:n+"\nSnippet failed to load ["+a+"] -- Telemetry is disabled\nHelp Link: https://go.microsoft.com/fwlink/?linkid=2128109\nHost: "+(S&&S.pathname||"_unknown_")+"\nEndpoint: "+i,parsedStack:[]}],r)),l.push(function(e,t,n,a){var i=v(c,"Message"),r=i.data;r.baseType="MessageData";var o=r.baseData;return o.message='AI (Internal): 99 message:"'+("SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details) ("+n+")").replace(/\"/g,"")+'"',o.properties={endpoint:a},i}(0,0,t,p)),function(e,t){if(JSON){var n=T.fetch;if(n&&!y.useXhr)n(t,{method:N,body:JSON.stringify(e),mode:"cors"});else if(XMLHttpRequest){var a=new XMLHttpRequest;a.open(N,t),a.setRequestHeader("Content-type","application/json"),a.send(JSON.stringify(e))}}}(l,p))}function i(e,t){f||setTimeout(function(){!t&&m.core||a()},500)}var e=function(){var n=l.createElement(k);n.src=h;var e=y[w];return!e&&""!==e||"undefined"==n[w]||(n[w]=e),n.onload=i,n.onerror=a,n.onreadystatechange=function(e,t){"loaded"!==n.readyState&&"complete"!==n.readyState||i(0,t)},n}();y.ld<0?l.getElementsByTagName("head")[0].appendChild(e):setTimeout(function(){l.getElementsByTagName(k)[0].parentNode.appendChild(e)},y.ld||0)}try{m.cookie=l.cookie}catch(p){}function t(e){for(;e.length;)!function(t){m[t]=function(){var e=arguments;g||m.queue.push(function(){m[t].apply(m,e)})}}(e.pop())}var n="track",r="TrackPage",o="TrackEvent";t([n+"Event",n+"PageView",n+"Exception",n+"Trace",n+"DependencyData",n+"Metric",n+"PageViewPerformance","start"+r,"stop"+r,"start"+o,"stop"+o,"addTelemetryInitializer","setAuthenticatedUserContext","clearAuthenticatedUserContext","flush"]),m.SeverityLevel={Verbose:0,Information:1,Warning:2,Error:3,Critical:4};var s=(d.extensionConfig||{}).ApplicationInsightsAnalytics||{};if(!0!==d[I]&&!0!==s[I]){var c="onerror";t(["_"+c]);var u=T[c];T[c]=function(e,t,n,a,i){var r=u&&u(e,t,n,a,i);return!0!==r&&m["_"+c]({message:e,url:t,lineNumber:n,columnNumber:a,error:i}),r},d.autoExceptionInstrumented=!0}return m}(y.cfg);function a(){y.onInit&&y.onInit(n)}(T[t]=n).queue&&0===n.queue.length?(n.queue.push(a),n.trackPageView({})):a()}(window,document,{
src: "https://js.monitor.azure.com/scripts/b/ai.2.min.js", // The SDK URL Source
// name: "appInsights", // Global SDK Instance name defaults to "appInsights" when not supplied
// ld: 0, // Defines the load delay (in ms) before attempting to load the sdk. -1 = block page load and add to head. (default) = 0ms load after timeout,
// useXhr: 1, // Use XHR instead of fetch to report failures (if available),
crossOrigin: "anonymous", // When supplied this will add the provided value as the cross origin attribute on the script tag
// onInit: null, // Once the application insights instance has loaded and initialized this callback function will be called with 1 argument -- the sdk instance (DO NOT ADD anything to the sdk.queue -- As they won't get called)
cfg: { // Application Insights Configuration
  connectionString:"InstrumentationKey=00000000-0000-0000-0000-000000000000;"
}});
</script>
```

> [!NOTE]
> Aby można było uzyskać czytelność i zmniejszyć liczbę błędów języka JavaScript, wszystkie możliwe opcje konfiguracji są wyświetlane w nowym wierszu kodu wstawki powyżej, jeśli nie chcesz zmieniać wartości w wierszu z komentarzem, możesz go usunąć.

Konfiguracja ręczna:
```javascript
import { ApplicationInsights } from '@microsoft/applicationinsights-web'

const appInsights = new ApplicationInsights({ config: {
  connectionString: 'InstrumentationKey=00000000-0000-0000-0000-000000000000;'
  /* ...Other Configuration Options... */
} });
appInsights.loadAppInsights();
appInsights.trackPageView();
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("InstrumentationKey=00000000-0000-0000-0000-000000000000;");
appInsights.start();
```

# <a name="python"></a>[Python](#tab/python)

Zalecamy, aby użytkownicy ustawili zmienną środowiskową.

Aby jawnie ustawić parametry połączenia:

```python
from opencensus.ext.azure.trace_exporter import AzureExporter
from opencensus.trace.samplers import ProbabilitySampler
from opencensus.trace.tracer import Tracer

tracer = Tracer(exporter=AzureExporter(connection_string='InstrumentationKey=00000000-0000-0000-0000-000000000000'), sampler=ProbabilitySampler(1.0))
```

---

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę w czasie wykonywania za pomocą rozwiązań:

* [Maszyna wirtualna platformy Azure i zestaw skalowania maszyn wirtualnych platformy Azure — aplikacje hostowane](./azure-vm-vmss-apps.md)
* [Serwer usług IIS](./monitor-performance-live-website-now.md)
* [Aplikacje internetowe platformy Azure](./azure-web-apps.md)

Rozpocznij pracę w czasie programowania za pomocą rozwiązań:

* [ASP.NET](./asp-net.md)
* [ASP.NET Core](./asp-net-core.md)
* [Java](./java-get-started.md)
* [Node.js](./nodejs.md)
* [Python](./opencensus-python.md)

