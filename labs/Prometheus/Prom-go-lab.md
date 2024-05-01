**INSTRUMENTING A GO APPLICATION FOR PROMETHEUS**

**Installation**

Install the required Prometheus libraries using `go get`:

```bash
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/promauto
go get github.com/prometheus/client_golang/prometheus/promhttp
```

**How Go Exposition Works**

*  Provide a `/metrics` HTTP endpoint.
*  Use the `prometheus/promhttp` library's HTTP handler.

**Example (Default Metrics):**

```go
package main

import (
        "net/http"

        "github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
        http.Handle("/metrics", promhttp.Handler())
        http.ListenAndServe(":2112", nil)
}
```

**Adding Your Own Metrics**

*  Create custom metrics (e.g., counters, gauges, histograms).
*  Use the `promauto` library for simplified registration.

**Example (Custom Counter):**

```go
package main

import (
        "net/http"
        "time"

        "github.com/prometheus/client_golang/prometheus"
        "github.com/prometheus/client_golang/prometheus/promauto"
        "github.com/prometheus/client_golang/prometheus/promhttp"
)

// ... (recordMetrics function)

var (
        opsProcessed = promauto.NewCounter(prometheus.CounterOpts{
                Name: "myapp_processed_ops_total",
                Help: "The total number of processed events",
        })
)

// ... (main function) 
```

**Summary**

This guide demonstrated how to create Go applications that expose Prometheus metrics and configure Prometheus to scrape those metrics.
