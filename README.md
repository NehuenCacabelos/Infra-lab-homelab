# Cluster de Microservicios con Balanceo de Carga (Nginx + Docker)

Este proyecto documenta la migración de servicios nativos en Ubuntu a una arquitectura de contenedores de alta disponibilidad, implementando un Proxy Inverso con capacidad de **Virtual Hosting** y **Escalabilidad Horizontal**.

## 🏗️ Arquitectura de Red

Se implementó una red virtual externa de tipo **bridge** denominada `web_network`. 

* **Aislamiento:** Los contenedores backend no exponen puertos al host.
* **Resolución DNS:** El proxy se comunica con los backends mediante sus nombres de servicio internos de Docker.



## 🛠️ Componentes Técnicos

### 1. Proxy Inverso y Balanceo (Capa 7)
Ubicado en `/proxy`, utiliza Nginx para distribuir el tráfico.
* **Algoritmo:** Round Robin (por defecto).
* **Failover:** Implementación de `proxy_next_upstream` para asegurar que el tráfico se redirija a instancias sanas en caso de fallo de un contenedor.

### 2. Cluster de Aplicaciones (Backend)
Ubicado en `/cluster-apps`, utiliza imágenes ligeras `nginx:alpine`.
* **Escalabilidad:** Diseñado para escalar horizontalmente de forma dinámica.

## 🚀 Guía de Despliegue

### Paso 1: Preparar la Red
```bash
docker network create web_network
