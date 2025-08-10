# 📚 Fundamentos de MITRE ATT&CK

## 1. Introducción
MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) es una **base de conocimiento global** que documenta **tácticas, técnicas y procedimientos (TTPs)** utilizados por actores de amenazas reales.

Se utiliza para **detectar, analizar y responder** a incidentes de ciberseguridad.

---

## 2. Estructura
- **Tácticas:** El objetivo general del atacante (ej. “Persistence”, “Privilege Escalation”).
- **Técnicas:** Cómo se ejecuta ese objetivo (ej. “Create Account”).
- **Subtécnicas:** Variante específica de la técnica (ej. “Local Account”).
- **Procedimientos:** Implementaciones reales usadas por amenazas conocidas.

---

## 3. Usos principales
1. **Mapeo forense:** Asociar hallazgos de incidentes con TTPs.
2. **Atribución:** Relacionar patrones con grupos APT conocidos.
3. **Priorizar defensa:** Proteger contra técnicas más usadas en el sector.
4. **Evaluación de madurez:** Comparar capacidades defensivas contra la matriz ATT&CK.

---

## 4. Ejemplo práctico
**Caso:** Detección de PowerShell sospechoso en un endpoint.
- **Táctica:** Execution
- **Técnica:** T1059.001 — PowerShell
- **Subtécnica:** Uso de comandos remotos para descargar payload.
- **Acción:** Bloquear ejecución y aislar host.

---



## 6. Ejemplos prácticos y clasificación personalizada

A continuación, se muestra una simulación de cómo registrar y clasificar hallazgos usando MITRE ATT&CK, integrando datos de nuestra investigación interna.

| Nº | Evidencia detectada                          | Táctica (MITRE)       | Técnica / ID            | Subtécnica           | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|----------------------------------------------|-----------------------|-------------------------|----------------------|---------------------|-------------------|--------------|
| 1  | Script PowerShell con descarga remota        | Execution             | T1059.001 - PowerShell  | Download & Execute   | APT28               | **Alta**          | Intento de conexión a IP maliciosa en RU |
| 2  | Uso de credenciales comprometidas            | Credential Access     | T1078 - Valid Accounts  | Local Account        | Desconocido         | Media             | Contraseña obtenida vía phishing |
| 3  | Conexión C2 a servidor en Tor                 | Command & Control     | T1090.003 - Proxy       | Tor                   | Lazarus Group       | **Alta**          | Persistencia confirmada vía tráfico cifrado |
| 4  | Movimiento lateral con PsExec                | Lateral Movement      | T1570 - Lateral Tool Transfer | N/A           | FIN7                | Alta              | Expansión a servidores internos |
| 5  | Escaneo masivo de puertos TCP                 | Reconnaissance        | T1046 - Network Service Scanning | N/A        | Script kiddies      | Baja              | Actividad previa a intrusión |

---

## 7. Clasificación según nuestra investigación

En nuestro marco interno, la priorización se define así:

- **Alta:** Actividad confirmada que compromete sistemas críticos o involucra actores APT conocidos.
- **Media:** Actividad sospechosa sin evidencia de explotación, pero con TTPs conocidos.
- **Baja:** Actividad común o automatizada sin impacto inmediato.

---

## 8. Flujo de uso en investigación

1. **Identificar** el evento sospechoso (logs, EDR, SIEM).
2. **Mapear** contra MITRE ATT&CK (táctica, técnica, subtécnica).
3. **Asignar prioridad** según:
   - Criticidad del sistema afectado.
   - Historial de explotación de esa técnica.
   - Actores relacionados.
4. **Documentar** en la bitácora de inteligencia.
5. **Difundir** el hallazgo al equipo de respuesta.

---

## 9. Herramientas útiles para clasificación

- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/) → Para mapear visualmente hallazgos.
- [ATT&CK Workbench](https://attack.mitre.org/resources/attack-workbench/) → Para crear taxonomías personalizadas.
- [MISP](https://www.misp-project.org/) → Para gestionar y correlacionar IoCs.

---



## Ejemplo 2 – Incidentes en Infraestructura Cloud

| Nº | Evidencia detectada                           | Táctica (MITRE)           | Técnica / ID                | Subtécnica             | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|-----------------------------------------------|---------------------------|-----------------------------|------------------------|---------------------|-------------------|--------------|
| 1  | Acceso no autorizado a consola AWS            | Initial Access            | T1078 - Valid Accounts      | Cloud Accounts         | APT29               | **Alta**          | Compromiso de credenciales IAM |
| 2  | Creación de nuevas llaves API sin autorización| Persistence               | T1098 - Account Manipulation| API Keys               | Desconocido         | Alta              | Persistencia en entorno productivo |
| 3  | Bucket S3 con permisos públicos               | Exfiltration              | T1537 - Transfer Data to Cloud Account | N/A         | N/A                 | Media             | Riesgo de fuga de datos sensibles |
| 4  | Escaneo de puertos a instancias EC2           | Reconnaissance            | T1046 - Network Service Scanning | N/A              | Script kiddies      | Baja              | Actividad previa a explotación |
| 5  | Uso de Lambda para ejecutar código malicioso  | Execution                 | T1059 - Command and Scripting Interpreter | N/A    | N/A                 | Alta              | Uso de servicio legítimo como vector de ataque |

---

## Ejemplo 3 – Incidentes en Red Corporativa

| Nº | Evidencia detectada                           | Táctica (MITRE)           | Técnica / ID                | Subtécnica             | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|-----------------------------------------------|---------------------------|-----------------------------|------------------------|---------------------|-------------------|--------------|
| 1  | Envío masivo de phishing con adjuntos maliciosos | Initial Access          | T1566.001 - Spearphishing Attachment | N/A   | APT32               | **Alta**          | Documento PDF con macro maliciosa |
| 2  | Uso de SMB para moverse entre servidores      | Lateral Movement          | T1021.002 - SMB/Windows Admin Shares | N/A  | Desconocido         | Alta              | Transferencia de payload entre hosts |
| 3  | Creación de túnel SSH hacia servidor externo  | Command & Control         | T1572 - Protocol Tunneling  | SSH                    | FIN8                | Alta              | C2 persistente no autorizado |
| 4  | Modificación de reglas de firewall            | Defense Evasion           | T1562.004 - Disable or Modify Firewall | N/A   | N/A                 | Alta              | Intento de abrir puertos para acceso remoto |
| 5  | Escaneo de vulnerabilidades internas          | Discovery                 | T1046 - Network Service Scanning | N/A              | Script kiddies      | Media             | Herramienta Nmap detectada en activo interno |

## Ejemplo 4 – Incidentes en IoT / OT Industrial

| Nº | Evidencia detectada                              | Táctica (MITRE)         | Técnica / ID                        | Subtécnica               | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|--------------------------------------------------|-------------------------|--------------------------------------|--------------------------|---------------------|-------------------|--------------|
| 1  | Acceso remoto no autorizado a PLC                | Initial Access          | T0866 - Remote Services              | N/A                      | Xenotime            | **Alta**          | Riesgo de alteración de procesos críticos |
| 2  | Cambio no programado en lógica de control        | Impact                  | T0831 - Modify Control Logic         | N/A                      | Desconocido         | Alta              | Modificación directa en línea de producción |
| 3  | Escaneo de red Modbus/TCP                        | Reconnaissance          | T0842 - Network Sniffing             | N/A                      | Desconocido         | Media             | Indicios de reconocimiento interno |
| 4  | Desactivación de alarmas de seguridad            | Defense Evasion         | T0853 - Service Stop                  | N/A                      | APT33               | Alta              | Posible preparación para sabotaje |
| 5  | Uso de credenciales por defecto en dispositivos  | Initial Access          | T0812 - Valid Accounts               | Default Accounts         | Script kiddies      | Alta              | Configuración insegura detectada |

---

## Ejemplo 5 – Incidentes en Correo Corporativo (BEC / Phishing)

| Nº | Evidencia detectada                              | Táctica (MITRE)         | Técnica / ID                        | Subtécnica               | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|--------------------------------------------------|-------------------------|--------------------------------------|--------------------------|---------------------|-------------------|--------------|
| 1  | Suplantación de dominio en correos recibidos     | Initial Access          | T1586.002 - Domain Spoofing          | N/A                      | Silent Starling     | **Alta**          | Ataque de Business Email Compromise |
| 2  | Uso de enlaces acortados hacia sitios maliciosos | Initial Access          | T1204.001 - User Execution           | Malicious Link           | Desconocido         | Alta              | Redirección a portal de phishing |
| 3  | Creación de reglas automáticas para ocultar correos | Persistence           | T1114.003 - Email Forwarding Rule    | N/A                      | FIN4                | Alta              | Oculta comunicaciones legítimas |
| 4  | Adjuntos con macros maliciosas                   | Execution               | T1566.001 - Spearphishing Attachment | N/A                      | APT28               | Alta              | Documento Word con VBA para descargar malware |
| 5  | Acceso desde direcciones IP inusuales            | Initial Access          | T1078 - Valid Accounts               | N/A                      | Desconocido         | Media             | Posible compromiso de cuenta |

---

## Ejemplo 6 – Incidentes en Aplicaciones Web

| Nº | Evidencia detectada                              | Táctica (MITRE)         | Técnica / ID                        | Subtécnica               | Actor/Grupo posible | Prioridad interna | Observaciones |
|----|--------------------------------------------------|-------------------------|--------------------------------------|--------------------------|---------------------|-------------------|--------------|
| 1  | Inyección SQL detectada en formulario de login   | Initial Access          | T1190 - Exploit Public-Facing Application | SQL Injection      | Script kiddies      | **Alta**          | Intento de extraer credenciales |
| 2  | Explotación de vulnerabilidad XSS                | Execution               | T1059.007 - Cross Site Scripting     | N/A                      | Desconocido         | Media             | Robo de cookies de sesión |
| 3  | Fuerza bruta contra panel de administración     | Credential Access       | T1110.001 - Password Guessing        | N/A                      | Desconocido         | Alta              | Intento reiterado de acceso no autorizado |
| 4  | Escaneo de endpoints ocultos                     | Reconnaissance          | T1595 - Active Scanning              | N/A                      | Desconocido         | Baja              | Mapear superficie de ataque web |
| 5  | Carga de archivo malicioso                        | Initial Access          | T1105 - Ingress Tool Transfer        | Webshell                 | APT41               | Alta              | Posible ejecución remota en servidor |
