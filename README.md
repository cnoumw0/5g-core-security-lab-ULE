# 5g-core-security-lab-ULE
Laboratorio de seguridad para núcleos 5G containerizados

> Laboratorio reproducible para **evaluar la postura de seguridad de núcleos 5G**
> desplegados con Docker (**OAI**, **free5GC** y **Open5GS**), validando si los
> problemas detectados por las herramientas de auditoría se traducen en
> **riesgos reales** para funciones y servicios como **AMF**, **SMF**, **NRF** o
> **UPF**, usando **UERANSIM** para verificar el funcionamiento de la red.

---

##  Tabla de contenidos

1. [¿Qué es este proyecto?](#-qué-es-este-proye)
2. [Objetivos](#-objetivos)
3. [Estructura del repositorio](#-estructura-del-repositorio)
4. [Licencia](#-licencia)
5. [Autor](#-autor)

---

##  ¿Qué es este proyecto?

Este repositorio contiene el material completo de una **práctica de auditoría de
seguridad** sobre núcleos 5G containerizados. El trabajo se realiza en un
**entorno aislado y reproducible** y cubre tres familias de problemas:

| Tipo de problema | Descripción | Herramienta principal |
|---|---|---|
| **Vulnerabilidades del runtime** | Fallos en el daemon Docker, containerd o kernel que afectan al aislamiento. | Docker Bench + Falco |
| **Configuraciones inseguras** | Privilegios, capabilities, montajes, red, filesystem, etc. | Docker Bench for Security |
| **Incidencias en imágenes** | CVEs, secretos, Dockerfiles y Compose mal configurados. | Trivy (+ SBOM) |

El objetivo final no es solo **detectar** problemas, sino **comprobar si esos
problemas suponen un riesgo real** para las funciones del 5G Core
(AMF, SMF, NRF, UPF…) y **proponer mitigaciones** que reduzcan el riesgo sin
degradar el servicio legítimo.

---

## Objetivos

- **Evaluar** la postura de seguridad de los núcleos 5G desplegados con Docker
  (OAI, free5GC, Open5GS).
- **Detectar** vulnerabilidades del runtime, configuraciones inseguras e
  incidencias en las imágenes.
- **Validar** si los hallazgos se traducen en riesgos reales para AMF, SMF,
  NRF o UPF.
- **Verificar** el funcionamiento de la red con UERANSIM (registro de UEs,
  sesiones PDU y tráfico de usuario).
- **Aplicar** medidas de endurecimiento y comprobar la reducción del riesgo
  **sin degradar** el servicio legítimo.
- **Documentar** evidencias etiquetadas y una matriz
  **hallazgo → validación → impacto → mitigación**.

---

## Estructura del repositorio

5g-core-security-lab/
├── README.md               # Visión general, cómo levantar el entorno, resultados clave
├── SECURITY.md             # Política de reporte de vulnerabilidades (aunque sea un lab)
├── LICENSE                 # MIT o similar
├── .gitignore              # Ignorar .env, logs, resultados de escaneos pesados, etc.
├── docs/
├── app/
│   ├── core/               # Despliegues del 5G Core
│   │   ├── free5gc/
│   │   │   └── config/     # YAMLs de AMF, SMF, UPF, NRF...
│   │   ├── open5gs/
│   │   │   └── config/ 
│   │   └── oai/
│   │       └── config/ 
│   ├── ueransim/           # Configuración de gNB y UE
│   │   └── ...
│   └── scripts/            # Scripts de automatización (levantar, recolectar evidencias)
│       └── hardening/      # Dockerfiles y compose endurecidos
├── evidence/
│   ├── baseline/           # Salidas de Docker Bench, Trivy, logs de registro de UE
│   ├── scenarios/          # Resultados de cada escenario controlado
│   ├── hardening/          # Evidencias tras aplicar mitigaciones
│   └── sbom/               # SBOMs generados (CycloneDX/SPDX)
└── inventory/
    └── ...

---

## Licencia

MIT License

Copyright (c) 2026 Cephas Bryan Noumi Wakam

---

## Autor
Cephas Bryan Wakam Etokey

---
