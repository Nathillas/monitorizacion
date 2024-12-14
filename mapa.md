
# Mapa Conceptual

Este mapa conceptual describe un sistema de monitorización basado en **Prometheus** y **Grafana**, mostrando cómo interactúan los componentes principales.
![](/img/mapa.png)

## Componentes Principales

### 1. **Prometheus**
- Actúa como el servidor principal de monitorización.
- Recopila métricas a través de peticiones HTTP desde diferentes fuentes o exportadores.
- Centraliza los datos para su análisis y procesamiento.

### 2. **Grafana**
- Es el visualizador de los datos recopilados por Prometheus.
- Proporciona una interfaz gráfica para interpretar y analizar las métricas.
- Se conecta a Prometheus para generar dashboards visuales en tiempo real.

## Exportadores y Fuentes de Datos
Prometheus obtiene datos de varias fuentes mediante peticiones HTTP. Los componentes de los que extrae métricas incluyen:

- **Application Server**: Monitoriza las métricas específicas de la aplicación en ejecución.
- **API Server**: Proporciona datos sobre el rendimiento y uso de las APIs.
- **Consul Exporter**: Extrae métricas relacionadas con el servicio de registro y descubrimiento de Consul.
- **Node Exporter**: Recopila información del sistema operativo, como uso de CPU, memoria y disco.

## Flujo de Datos
1. Los exportadores y servidores proporcionan datos a Prometheus a través de HTTP.
2. Prometheus almacena y organiza las métricas.
3. Grafana consulta los datos almacenados en Prometheus para generar visualizaciones comprensibles.

Este flujo permite a los administradores de sistemas supervisar y optimizar aplicaciones y recursos en tiempo real de forma eficiente.
