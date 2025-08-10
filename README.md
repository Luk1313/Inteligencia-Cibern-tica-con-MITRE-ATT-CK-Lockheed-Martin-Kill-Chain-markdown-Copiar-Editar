# 🛡️ Guía Operativa — MITRE ATT&CK y Lockheed Martin Kill Chain

Este repositorio contiene fundamentos, metodología y ejemplos prácticos para aplicar **MITRE ATT&CK** y **Lockheed Martin Cyber Kill Chain** en investigaciones y operaciones de inteligencia cibernética.

---

## 📌 Objetivo
Proporcionar a analistas y equipos de seguridad un manual para:
- **Identificar**, **clasificar** y **seguir** el ciclo de un ataque.
- Usar marcos reconocidos internacionalmente para estructurar inteligencia.
- Integrar estos modelos en informes, dashboards y procesos SOC/CTI.

---

## 📖 Fundamentos

### 🔹 1. MITRE ATT&CK
- **Definición:** Base de conocimiento global que documenta **tácticas, técnicas y procedimientos (TTPs)** usados por actores de amenazas.
- **Estructura:**
  - **Tácticas:** Objetivo general del atacante (ej. “Persistence”).
  - **Técnicas:** Cómo logra ese objetivo (ej. “Create Account”).
  - **Subtécnicas:** Variante específica (ej. “Local Account”).
- **Usos en inteligencia:**
  - Mapear evidencias forenses contra técnicas conocidas.
  - Correlacionar IoCs con TTPs para atribución.
  - Priorizar defensas en función de TTPs más usados en la región o sector.
- **Recursos:**
  - [MITRE ATT&CK Web](https://attack.mitre.org/)
  - [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

---

### 🔹 2. Lockheed Martin Cyber Kill Chain
- **Definición:** Modelo que describe las **7 fases** de un ciberataque desde el reconocimiento hasta la acción final.
- **Fases:**
  1. **Reconnaissance** – Recopilación de información.
  2. **Weaponization** – Creación del artefacto malicioso.
  3. **Delivery** – Envío del artefacto.
  4. **Exploitation** – Ejecución del exploit.
  5. **Installation** – Instalación de malware o puertas traseras.
  6. **Command & Control (C2)** – Comunicación con servidor atacante.
  7. **Actions on Objectives** – Robo, sabotaje o destrucción.
- **Usos en inteligencia:**
  - Determinar en qué fase fue detectado un ataque.
  - Establecer medidas para interrumpir el ciclo antes de que cumpla su objetivo.
- **Recursos:**
  - [Kill Chain Oficial](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)

---

## ⚖️ Comparativa Rápida

| Característica | MITRE ATT&CK | Kill Chain |
|----------------|--------------|-----------|
| **Enfoque** | Técnicas y tácticas específicas | Fases generales del ataque |
| **Detalle** | Alto, con subcategorías y mapeo a IoCs/TTPs | Más conceptual y lineal |
| **Uso ideal** | Análisis forense y atribución | Estrategia de defensa y prevención |
| **Base** | Inteligencia de amenazas global | Ciclo de ataque militar adaptado a ciberseguridad |

---

## 🛠️ Cómo usar ambos modelos juntos

1. **Fase de detección:**
   - Detectar IoCs (IP, hash, dominio) y evidencias.
   - Clasificarlos según la táctica y técnica de MITRE.
2. **Mapeo en Kill Chain:**
   - Ubicar el incidente en la fase correspondiente del ciclo.
3. **Análisis cruzado:**
   - Determinar técnicas de MITRE usadas en cada fase de Kill Chain.
4. **Defensa proactiva:**
   - Implementar controles que interrumpan el ciclo en fases tempranas.
5. **Reporte de inteligencia:**
   - Documentar hallazgos en formato estándar para CTI/SOC.

---

## 📌 Ejemplo Práctico

**Caso:** Campaña de phishing con malware bancario.
1. **Kill Chain:**  
   - Reconnaissance → Obtención de correos corporativos.  
   - Weaponization → Creación de documento malicioso con macro.  
   - Delivery → Envío por correo.  
   - Exploitation → Usuario abre documento y habilita macros.  
   - Installation → Instalación de troyano bancario.  
   - C2 → Comunicación con servidor en IP maliciosa.  
   - Actions → Robo de credenciales y datos financieros.  

2. **MITRE ATT&CK:**  
   - T1566.001 (Phishing vía email)  
   - T1204.002 (Ejecución de macros)  
   - T1055 (Inyección de proceso)  
   - T1071.001 (C2 por HTTP/S)  

---

## 📎 Recursos adicionales
- [MITRE ATT&CK API](https://attack.mitre.org/resources/)
- [ATT&CK Navigator GitHub](https://github.com/mitre-attack/attack-navigator)
- [Lockheed Martin Kill Chain PDF](https://www.lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/Kill%20Chain.pdf)

---

## 📂 Estructura del repositorio
