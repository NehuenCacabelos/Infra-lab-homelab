# Laboratorio de Infraestructura: Proxy Inverso y Balanceo de Carga con Docker

Este proyecto demuestra la implementación de una arquitectura de microservicios utilizando **Docker** y **Nginx** como Proxy Inverso de Capa 7. El objetivo principal es simular un entorno de producción con alta disponibilidad y resolución de nombres mediante Virtual Hosting.

## 🚀 Arquitectura del Proyecto

La infraestructura se divide en dos capas principales conectadas por una red virtual aislada:

1.  **Capa de Entrada (Edge):** Un contenedor Nginx que actúa como Proxy Inverso, gestionando certificados (simulados) y ruteo por nombre de dominio.
2.  **Capa de Aplicación (Backend):** Un clúster de contenedores Nginx Alpine escalados dinámicamente para demostrar balanceo de carga.



## 🛠️ Tecnologías Utilizadas

* **Docker & Docker Compose:** Orquestación de contenedores.
* **Nginx:** Proxy inverso y balanceador de carga (Round Robin).
* **Linux (Ubuntu Server):** Host de infraestructura.

## 📋 Características Implementadas

* **Virtual Hosting:** Gestión de múltiples dominios (`app1.test`, `app2.test`) bajo una sola dirección IP.
* **Networking Aislado:** Uso de una red bridge externa (`web_network`) para comunicación inter-container segura sin exponer puertos de backend al host.
* **Escalabilidad Horizontal:** Despliegue de réplicas dinámicas mediante la directiva `--scale` de Docker Compose.
* **Alta Disponibilidad (HA):** Configuración de `upstream` para failover automático en caso de caída de nodos.

## 🔧 Configuración del Entorno

### 1. Preparación de la Red
```bash
docker network create web_network
