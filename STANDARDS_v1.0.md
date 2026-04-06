# 📋 DISATEQ STANDARDS v1.0

**Documento Fundacional Único de Estándares de Desarrollo**

- **Versión:** v1.0 (Marzo 2026)
- **Base:** 7 meses experiencia operativa en Piura
- **Clientes validados:** 35+ (Panel Remoto operativo)
- **Aplicación:** Todos los productos DISATEQ
- **Alcance:** Agnóstico en rubros (farmacia, restaurante, clínica, óptica, otros)
- **Estado:** Foundation operativamente validado
- **Vigencia:** Marzo 2026 - Marzo 2027 (review anual)

---

## 📑 TABLA DE CONTENIDOS

**PARTE 1: FUNDAMENTOS (Secciones 1-3)**
1. Introducción y Contexto
2. Principios Fundamentales
3. Herramientas Recomendadas

**PARTE 2: OPERATIVA PIURA (Secciones 4-5)**
4. Restricciones Operativas Piura
5. Seguridad Integral

**PARTE 3: ARQUITECTURA TÉCNICA (Secciones 6-12)**
6. Base de Datos
7. Arquitectura de Código
8. Transacciones e Idempotencia
9. Validación y Sanitización
10. Manejo de Errores
11. Testing

**PARTE 4: OPERACIÓN Y EVOLUCIÓN (Secciones 12-19)**
12. Control de Versiones y CI/CD
13. Diseño UI/UX y Herramientas
14. Fases de Desarrollo
15. Uso de IA en DISATEQ
16. Observabilidad y Monitoreo
17. Backup y Recuperación
18. Documentación
19. Evolución del Sistema

**PARTE 5: REFERENCIA Y AUDITORÍA (Secciones 20-26)**
20. Matriz de Decisiones
21. Anti-patrones a Evitar
22. Instrucción Paso-a-Paso para IA
23. Roadmap Futuro (2028+)
24. Glosario Operativo
25. Indicadores de Éxito por Etapa
26. Auditoría IA Operativa
27. Changelog

---

## 🎯 INTRODUCCIÓN Y CONTEXTO

### ¿Qué es este documento?

Este es el **estándar único de desarrollo DISATEQ v1.0**. Define cómo diseñamos, construimos, probamos y operamos software que funciona en la realidad peruana, comenzando en Piura, extensible a cualquier región/rubro.

No es académico. Es operativo: validado con 35+ clientes reales durante 7 meses.

### ¿Por qué existe?

DISATEQ compite por **confianza**, no features:
- Sistema que funciona sin internet (latencia variable Perú)
- Interfaz que entiende el cliente en 30 segundos (no confunde)
- Datos que nunca se pierden incluso si apagón (SUNAT obliga)
- Soporte que resuelve sin escalar siempre (escalable)

### ¿A quién va dirigido?

- **Developers:** Qué hacer para ser "DISATEQ-compliant"
- **DevOps:** Cómo configurar infraestructura robusta
- **Diseñadores:** Principios UI/UX DISATEQ
- **PMs:** Cómo guiar decisiones técnicas
- **IA/Claude Code:** Pasos explícitos para generar código válido

### Cómo leer este documento

Cada sección tiene:
- **Definición** (qué es)
- **Por qué importa** (impacto negocio)
- **Cómo implementar** (paso a paso)
- **Ejemplo práctico** (farmacia, restaurante, clínica, óptica)
- **Clasificación 🔴🟡🟢** (criticidad)

**🔴 CRÍTICO:** No negociable. Siempre. Sin excepción.
**🟡 REQUERIDO:** Por defecto. Si no aplica, documentar por qué.
**🟢 ADAPTABLE:** Si tiempo/valor permite. No bloqueante.

---

## 🧭 PRINCIPIOS FUNDAMENTALES

### Principio 1: Confianza sobre Complejidad

Cliente peruano no quiere tecnología sofisticada. Quiere **funcionar, no robar tiempo, no confundir**.

### Principio 2: Operativo antes que Perfecto

Código funcional hoy > arquitectura perfecta en 3 meses.

### Principio 3: Contextualizado a Perú

SUNAT, Multi-RUC, Informalidad desde día 1. No copiamos SaaS gringos.

### Principio 4: Agnóstico en Rubros

Mismo código base farmacia/restaurante/clínica/óptica. Diferencias en configuración, no código.

---

## 🛠️ HERRAMIENTAS RECOMENDADAS

### Prescrito (NO NEGOCIABLE):

```
BACKEND:
  ├─ PHP 8.2+
  ├─ PostgreSQL 15+
  ├─ Composer
  ├─ Docker
  └─ Git + GitHub Actions

INFRAESTRUCTURA:
  ├─ Versionado: Git
  ├─ Containerización: Docker
  ├─ CI/CD: GitHub Actions
  └─ WAF: Cloudflare free
```

### Recomendado (aplica por defecto):

```
FRONTEND:
  ├─ CSS: Tailwind o Bootstrap
  ├─ JS Framework: Vue 3, React, Svelte, Alpine.js
  ├─ Design: Figma (free)
  └─ Icons: Feather, Bootstrap Icons

CALIDAD:
  ├─ Linting: PHP-CS-Fixer
  ├─ Static analysis: PHPStan
  ├─ Security: composer audit
  └─ Monitoring: Sentry (free) o Datadog
```

### Agnóstico (elige uno):

```
ORM vs Raw SQL: Doctrine, Eloquent, Propel (elige)
Testing: PHPUnit, Pest, Codeception (elige)
Cache: Redis, Memcached, archivo (depende)
API: REST (estándar), GraphQL (si justificas)
```

---

## ⚡ RESTRICCIONES OPERATIVAS PIURA

### Realidad que determina la arquitectura:

Infraestructura internet y energía es **variable**. Sistema debe funcionar en eso, no en condiciones ideales.

### Latencia Internet

**Realidad:**
- Velocidad: 2-5 Mbps
- Latencia: 50-200ms
- Apagones: 0-2 veces/mes, 10min-2horas

**Implicación:** Offline-first es OBLIGATORIO

### Energía Inestable

**Realidad:**
- Apagones sin aviso
- Voltaje variable

**Implicación:** Transacciones ACID, UPS servidor

### Hardware Real (PC Escritorio)

```
CONFIGURACIÓN TÍPICA:
  ├─ CPU: Intel i5 / AMD Ryzen 5
  ├─ RAM: 8-16 GB
  ├─ SO: Windows 10/11
  └─ Costo: $400-800 usada, $1000-1500 nueva

PERIFÉRICOS:
  1. Impresora Tiquetera 58mm (Epson TM-T88, Star)
  2. Lector Códigos (handheld, USB/Bluetooth)
  3. Impresora A4 (HP, Canon, Brother)
  4. UPS (30-60 min batería)

TOTAL: ~$1,300-1,500 por punto venta
```

### Arquitectura Offline-First

```
CLIENTE FUNCIONA SIN INTERNET:
  ├─ Datos guardados localmente (SQLite/IndexedDB)
  ├─ Respuesta inmediata (< 200ms)
  ├─ Sincronización automática cuando conecta
  └─ Cero espera, cero frustración

SERVIDOR DISATEQ:
  ├─ API optimizada (compresión, cache)
  ├─ Idempotencia obligatoria
  ├─ Conflict resolution (servidor = fuente verdad)
  └─ Manejo apagones (transacciones ACID)

RESULTADO: Cliente nunca espera, nunca pierde dato
```

### Testing en Condiciones Reales

🔴 **CRÍTICO:** No testear en Lima o WiFi rápido

Validar siempre:
- Latencia 50-200ms (simulado)
- Ancho banda 2-5 Mbps
- Apagón a mitad operación
- Tablet sin batería

---

## 🔒 SEGURIDAD INTEGRAL

### 🔴 CRÍTICO:

**1. No credenciales hardcodeadas NUNCA**
- Todos secretos → variables de entorno (.env)
- .env NO va a Git

**2. Validación backend obligatoria**
- NUNCA confiar frontend
- Validar tipo, rango, formato

**3. SQL Injection prevention**
- SIEMPRE prepared statements
- Nunca concatenar strings

**4. XSS prevention**
- Escapar HTML output (htmlspecialchars)
- No confiar user input

**5. CSRF protection**
- Forms deben tener token CSRF
- Backend valida antes procesar

**6. Authentication + Authorization**
- Autenticación: ¿quién eres?
- Autorización: ¿qué puedes hacer?

**7. Password hashing**
- NUNCA guardar en plano
- SIEMPRE bcrypt o Argon2

**8. Dependency scanning**
- `composer audit` regularmente
- Librerías vulnerables = tu código tiene bug

### 🟡 REQUERIDO:

**1. Rate limiting** (anti-fuerza bruta)
**2. Logging sin sensibles**
**3. Content-Security-Policy headers**
**4. HTTPS obligatorio**

### 🟢 ADAPTABLE:

**1. Cifrado en reposo (AES-256)**
**2. 2FA para admin**
**3. VPN para acceso admin**

### Seguridad Infraestructura

🔴 **CRÍTICO:**
- Firewall (bloquea no autorizado)
- SSH hardening (sin passwords)
- DB access control (NO internet)
- SSL/TLS certificados (Let's Encrypt)
- Backup encryption (AES-256)
- WAF (Cloudflare)

🟡 **REQUERIDO:**
- Access logs + auditoría
- Secrets rotation
- Incident response plan
- Monitoring continuo

---

## 💾 BASE DE DATOS

### 🔴 CRÍTICO:

**1. PostgreSQL 15+ (único)**
- ACID, JSON, transacciones, UUID native
- No SQLite/MySQL en producción

**2. UUID como PRIMARY KEY**
- No INT auto-increment
- Distribuído, no predecible, offline-ok

**3. created_at, updated_at en TODAS tablas**
- Auditoría: cuándo creó, cuándo cambió
- Timezone: SIEMPRE UTC

**4. Índices en queries críticas**
- Query lenta = cliente enojado
- Índice en: ruc, empresa_id, comprobante_id

**5. No duplicidad datos**
- Una verdad, un lugar
- Si cambias, actualizar en un lugar

### 🟡 REQUERIDO:

**1. Migraciones versionadas**
- Flyway o Doctrine Migrations
- Cada cambio = nuevo archivo

**2. Normalización (3NF)**
**3. Foreign keys con restricciones**

### 🟢 ADAPTABLE:

**1. Soft delete**
**2. Versionado datos**
**3. Particionamiento (si tabla > 10M filas)**

---

## 🏗️ ARQUITECTURA DE CÓDIGO

### 🔴 CRÍTICO: Separación Mínima

```
3 capas obligatorias:

1. CONTROLLER (recibe HTTP)
   ├─ Parsea request
   ├─ Delega a Service
   ├─ Retorna response
   └─ NUNCA queries directo a BD

2. SERVICE (lógica negocio)
   ├─ Reglas de dominio
   ├─ Orquesta Repositories
   ├─ Manejo de errores
   └─ Transacciones aquí

3. REPOSITORY (acceso datos)
   ├─ Queries a BD
   ├─ Abstrae ORM o SQL raw
   ├─ NUNCA lógica negocio
   └─ Retorna entities puras
```

### 🟡 REQUERIDO: Clean Architecture

```
LAYERS:
1. Domain (lógica pura, sin dependencias)
2. Application (orquestación, DTOs)
3. Infrastructure (BD, APIs externas)
4. Presentation (HTTP, CLI)
```

### Type Hints Obligatorios (PHP 8.2)

```php
❌ function crearComprobante($datos) { ... }
✅ function crearComprobante(CrearComprobanteDTO $datos): Comprobante { ... }
```

---

## 🔄 TRANSACCIONES E IDEMPOTENCIA

### 🔴 CRÍTICO:

**1. Operaciones dinero SIEMPRE idempotentes**
- CPE creation (comprobante es dinero)
- Si cliente reintenta (falla red), no duplicar

**2. idempotency_key OBLIGATORIO**
```
1era: POST /cpe { idempotency_key: ABC, datos... } → crea CPE X
2da:  POST /cpe { idempotency_key: ABC, datos... } → retorna CPE X (sin crear)
```

**3. Transacciones ACID**
- Si falla a mitad: ROLLBACK automático
- Si apagón: PostgreSQL recupera

**4. Retry automático con backoff**
- 1er intento: inmediato
- 2do intento: esperar 1s
- 3er intento: esperar 5s

### 🟡 REQUERIDO:

**1. Detección operación duplicada**
**2. Logging de intentos**

---

## ✔️ VALIDACIÓN Y SANITIZACIÓN

### 🔴 CRÍTICO:

**1. Validación backend (NUNCA confiar frontend)**
**2. Prepared statements (SQL safe)**
**3. HTML escaping (XSS safe)**

### 🟡 REQUERIDO:

**1. Input type validation**
**2. Whitelist > Blacklist**
**3. Length limits**
**4. Rate limiting (anti-fuerza bruta)**

---

## 📢 MANEJO DE ERRORES

### 🔴 CRÍTICO:

**1. No silenciar errores NUNCA**
```php
❌ try { ... } catch() { }  (vacío)
✅ try { ... } catch(Exception $e) { 
    logger->error("msg: " . $e->getMessage()); 
    throw $e; 
  }
```

**2. Formato JSON estándar para errores**
```json
{
  "error": true,
  "message": "RUC inválido",
  "code": "INVALID_RUC",
  "trace_id": "abc123def456",
  "status": 400
}
```

**3. trace_id en TODO log**
- UUID único por request
- Seguir error de inicio a fin

### 🟡 REQUERIDO:

**1. Exception hierarchy** (Domain, Application, Infrastructure)
**2. Logs estructurados (JSON)**
**3. Niveles log** (DEBUG, INFO, WARNING, ERROR, CRITICAL)

---

## 🧪 TESTING

### 🟡 REQUERIDO:

**1. Unit tests en lógica crítica**
**2. Integration tests endpoints**
**3. Coverage mínimo 60%**

### 🟢 ADAPTABLE:

**1. E2E tests**
**2. Coverage 100% (aspiracional)**
**3. Performance tests**
**4. Load testing**

---

## 📌 CONTROL DE VERSIONES Y CI/CD

### 🟡 REQUERIDO:

**1. Git workflow (Gitflow)**
```
main: producción, tagged versiones
develop: staging, integración
feature/...: rama individual
bugfix/...: rama individual
hotfix/...: rama crítica
```

**2. Commits semánticos**
- [FEATURE], [FIX], [REFACTOR], [TEST], [DOCS], [SECURITY], [PERF]

**3. Pull Requests**
- Toda feature entra por PR (no push directo)
- 2+ code reviews
- Todos tests verdes

**4. Versionado semántico**
- v1.0.0 (mayor.menor.patch)
- v1.1.0: feature nueva
- v1.0.1: bug fix
- v2.0.0: breaking change

### 🟢 ADAPTABLE: CI/CD (GitHub Actions)

```
1. Tests corre
2. Linting chequea
3. Static analysis
4. Security scan
5. Si todo verde → build ok
```

---

## 🎨 DISEÑO UI/UX Y HERRAMIENTAS

### 🔴 CRÍTICO: Principios

**1. Simplicidad > Hermosura**
- 3 clics máximo para acción común
- Sin jargon técnico en interfaz

**2. Accesibilidad (WCAG 2.1 AA)**
- Contraste suficiente
- Alt text para imágenes
- Navegable con teclado

**3. Mobile-first (Piura usa celular/tablet)**
- Diseñar para 320px primero
- Responsive: 320, 768, 1024+
- Carga rápida (< 3s)

**4. Performance (crítico Piura)**
- Carga < 3 segundos
- Optimizar: minify, compress, lazy load

### 🟡 REQUERIDO:

**1. Design tokens** (colores, spacing centralizados)
**2. Component library**
**3. Responsive breakpoints**
**4. CSS framework** (Tailwind recomendado)

### Herramientas (sin pagar):

```
Design: Figma free, Penpot
Icons: Feather Icons, Bootstrap Icons
Colors: Coolors.co, Contrast Checker
Fonts: Google Fonts
Performance: Google PageSpeed, GTMetrix
Accessibility: WAVE, axe DevTools
```

---

## 📈 FASES DE DESARROLLO

No saltarse fases. No romper integridad datos.

```
1. ARQUITECTURA & DISEÑO (1-2 días)
2. SKELETON CODE (1 día)
3. DOMAIN LOGIC (2-3 días)
4. INFRASTRUCTURE (2-3 días)
5. HTTP LAYER (2 días)
6. TESTING (2 días)
7. SECURITY REVIEW (1 día)
8. DEPLOYMENT (1 día)
9. MONITOREO (continuo)

TOTAL: 14-17 días (2.5-4 semanas)
```

---

## 🤖 USO DE IA EN DISATEQ

### 🔴 CRÍTICO: Uso Seguro

**IA GENERA 80%, DEVELOPER VALIDA 20%**

**CUÁNDO USAR IA:**
✅ Boilerplate code
✅ Migration scripts
✅ Tests simples
✅ Documentación

**CUÁNDO NO USAR IA:**
❌ Lógica crítica
❌ Seguridad
❌ Auth/authz
❌ Encripción
❌ Cambios BD críticos

### Instrucciones IA (Prompt):

```
Eres developer DISATEQ. Generar código:

CONTEXTO:
- Proyecto: [nombre]
- Etapa: [qué etapa]
- Sección STANDARDS: [número]

REQUISITO:
[descripción qué hacer]

CHECKLIST DE VALIDACIÓN:

🔴 CRÍTICO (bloquea si falla):
  [ ] Type hints PHP 8.2: ¿presentes? SÍ/NO
  [ ] SQL Injection: ¿prepared statements? SÍ/NO
  [ ] XSS: ¿output escapado? SÍ/NO
  [ ] Credentials: ¿hardcodeadas? SÍ/NO

🟡 REQUERIDO:
  [ ] Arquitectura: ¿sigue 3 capas? SÍ/NO
  [ ] Nombres claros: ¿variable clara? SÍ/NO
  [ ] PHPDoc: ¿presente? SÍ/NO
  [ ] Tests: ¿agregó test? SÍ/NO
```

---

## 📊 OBSERVABILIDAD Y MONITOREO

### 🔴 CRÍTICO:

**1. Logs en operaciones críticas**
- CPE creado: log con id, empresa, usuario, hora
- Sincronización: log eventos y errores

**2. trace_id en TODOS logs**
- UUID único por request
- Sigue error de inicio a fin

### 🟡 REQUERIDO:

**1. Logs estructurados (JSON)**
**2. Niveles log** (DEBUG, INFO, WARNING, ERROR, CRITICAL)
**3. Alertas** (error rate, performance, BD down)

---

## 💾 BACKUP Y RECUPERACIÓN

### 🔴 CRÍTICO:

**1. Backup definido**
- BD completa: diario (mínimo cada 6h)
- Archivos: diario

**2. Recuperación PROBADA**
- Testear restauración semanal
- Validar data intacta
- Tiempo < 1 hora

### 🟡 REQUERIDO:

**1. Backup encryption** (AES-256)
**2. PITR** (Point-In-Time Recovery)
**3. Ubicaciones diversas** (local, NAS, cloud)

---

## 📚 DOCUMENTACIÓN

### 🟡 REQUERIDO:

**1. README.md**
- Qué es proyecto
- Setup local
- Tests, deploy

**2. API Specification**
- OpenAPI/Swagger
- Endpoints, parámetros, responses

**3. ARCHITECTURE.md**
- Diagrama alto nivel
- Flujos críticos
- Decisiones técnicas

---

## 🔄 EVOLUCIÓN DEL SISTEMA

### 🔴 CRÍTICO:

**No romper integridad datos**

Si necesitas cambiar schema:
1. Crear migración (no manual ALTER)
2. UP (cambio) + DOWN (revertir)
3. Test: UP/DOWN funcionan
4. Deploy staging primero
5. Validar queries no rompidas
6. Deploy producción

### 🟡 REQUERIDO:

**1. Migraciones versionadas**
**2. Versionado de API** (v1/, v2/)
**3. Deprecation warnings** (3 meses antes remover)

---

## 🎯 MATRIZ DE DECISIONES (QUICK REFERENCE)

| DECISIÓN | OPCIÓN A | OPCIÓN B | RECOMENDACIÓN |
|----------|----------|----------|----------------|
| ORM vs Raw SQL | Eloquent | Raw queries | ORM si simple, raw si específico |
| Caché | Redis | BD directo | Redis si > 1000 queries/min |
| Coverage | 100% | 60% | 60%+, 100% en crítico |
| Log storage | File | Cloud | File + alertas simples |
| API | REST | GraphQL | REST estándar, GraphQL si justificas |
| CSS | Tailwind | Bootstrap | Tailwind (más ligero) |
| Frontend | Vue 3 | React | Vue 3 estándar DISATEQ |
| DB encrypt | Sí | No | Sí para sensible |
| Soft delete | Sí | No | Sí si auditoría crítica |
| API version | v1, v2 | Único | Versionar si breaking |

---

## ⚠️ ANTI-PATRONES A EVITAR

❌ Queries en controller
❌ Lógica negocio en BD (stored procedures)
❌ God objects (1 clase 500 líneas)
❌ N+1 queries
❌ Silent errors (try/catch vacío)
❌ Credentials hardcodeadas
❌ No tests en crítico
❌ Comentarios engañosos
❌ Confiar frontend para seguridad

---

## 🤖 INSTRUCCIÓN PASO-A-PASO PARA IA

```
PASO 1: Identificar tipo sistema
PASO 2: Identificar fase actual
PASO 3: Aplicar 🔴 CRÍTICO (obligatorio)
PASO 4: Aplicar 🟡 REQUERIDO (by default)
PASO 5: Aplicar 🟢 ADAPTABLE (si time permite)
PASO 6: Validaciones post-IA

CHECKLIST ANTES USAR IA:
  [ ] Contexto claro (qué, por qué, cómo)
  [ ] Tipo código identificado (crítico? seguridad?)
  [ ] STANDARDS sección relevante señalada
  [ ] Salida esperada documentada

CHECKLIST DESPUÉS IA:
  [ ] ¿Tiene sentido lógica?
  [ ] Type hints correctos?
  [ ] SQL safe?
  [ ] No hardcoded secrets?
  [ ] Tests pasan?
  [ ] Linting ok?
  [ ] Static analysis ok?
  [ ] Code review aprobó?
```

---

## 🚀 ROADMAP FUTURO (2028+)

```
2026 (NOW):
  ├─ 1 servidor PostgreSQL
  ├─ Monolito limpio
  ├─ 20-30 clientes
  └─ Manual scaling

2027:
  ├─ 200+ clientes
  ├─ Múltiples servidores (2-3)
  ├─ Load balancer
  ├─ Redis caché
  └─ Kubernetes evaluación

2028+:
  ├─ 500+ clientes nacional
  ├─ Microservicios selectivos
  ├─ Multi-región
  └─ Advanced monitoring
```

**Nota:** No hagas hoy lo que harás en 2028. Agrega complejidad solo si existe.

---

## 📖 GLOSARIO OPERATIVO

### Arquitectura
Estructura componentes, capas, relaciones. En DISATEQ: 3 capas (Controller → Service → Repository).

### Diseño
Definición visual y funcional. Mobile-first, accesible WCAG 2.1 AA.

### Construcción
Implementación código siguiendo STANDARDS. PHP 8.2, PostgreSQL, Docker.

### Pruebas
Validación sistema funciona. Unit 60%+ coverage, Integration, Feature.

### Operación
Sistema funcionando producción, monitoreado, con soporte.

### Etapa / Fase
Sección ordenada desarrollo (9 fases). No saltarse, no mezclar.

### Indicador de Éxito
Métrica cuantificable validando completitud etapa.

### Requisito
Funcional: "Sistema crea CPE en < 2s"
No-Funcional: "Performance < 3s carga"

### Riesgo
Evento potencial impide cumplimiento.

### Deuda Técnica
Código funciona pero no sigue STANDARDS.

### Crítico (🔴)
No negociable. SIEMPRE.

### Requerido (🟡)
Por defecto. Si no aplica, documentar.

### Adaptable (🟢)
Si time/valor permite.

### Offline-First
Sistema funciona sin internet. Sincronización automática cuando conecta.

### Idempotencia
Operación dinero: si reintentas, no duplica.

### Trace ID
UUID único por request. Sigue error inicio-a-fin.

### Piura-Centric
Diseño para realidad Piura (latencia, energía, relaciones).

### Agnóstico
STANDARDS aplica igual farmacia/restaurante/clínica/óptica.

### Acompañamiento
Soporte continuo, no abandono post-venta.

---

## 📊 INDICADORES DE ÉXITO POR ETAPA

### Fase 1: ARQUITECTURA & DISEÑO

🔴 **CRÍTICO:**
- [ ] ARCHITECTURE.md completo
- [ ] ER diagram
- [ ] Flujo usuario documentado
- [ ] Decisiones técnicas justificadas
- [ ] Validación PM/CTO: SÍ

📊 **Indicadores:**
- Aprobación: SÍ/NO
- Riesgos identificados: ≥3
- Mitigaciones documentadas: 100%

✅ **Criterio aprobación:** PM y CTO firman ARCHITECTURE.md

### Fase 2: SKELETON CODE

🔴 **CRÍTICO:**
- [ ] Folder structure creada
- [ ] Interfaces definidas
- [ ] Build pasa (sin warnings)
- [ ] README.md con setup

📊 **Indicadores:**
- Compilación: ✅ limpia
- Warnings: 0
- Structure completitud: 100%

✅ **Criterio:** `composer install && vendor/bin/phpstan` retorna limpio

### Fase 3: DOMAIN LOGIC

🔴 **CRÍTICO:**
- [ ] Entities creadas
- [ ] Validaciones implementadas
- [ ] Excepciones Domain definidas
- [ ] Unit tests > 80% coverage

🟡 **REQUERIDO:**
- [ ] Documentación lógica
- [ ] ValueObjects si necesarios

📊 **Indicadores:**
- Coverage domain: ≥80%
- Tests pasan: 100%
- No dependencias externas: ✅

✅ **Criterio:** `phpunit --filter=Domain` retorna 100% verde

### Fase 4: INFRASTRUCTURE

🔴 **CRÍTICO:**
- [ ] Migraciones BD creadas
- [ ] Repositories implementados
- [ ] Conexiones externas (SUNAT, etc)
- [ ] Integration tests

📊 **Indicadores:**
- BD schema: validado
- Migraciones: UP/DOWN funcionan
- Coverage infra: ≥60%

✅ **Criterio:** `phpunit --filter=Integration` retorna 100% verde

### Fase 5: HTTP LAYER

🔴 **CRÍTICO:**
- [ ] Controllers implementados
- [ ] Routing configurado
- [ ] Error handling (400, 401, 403, 500)
- [ ] Feature tests

📊 **Indicadores:**
- POST /api/cpe + válido → 201 ✅
- POST /api/cpe + inválido → 400 ✅
- GET /api/cpe sin auth → 401 ✅
- Coverage HTTP: ≥60%

✅ **Criterio:** Postman tests pasan, cliente valida flujo

### Fase 6: TESTING

🔴 **CRÍTICO:**
- [ ] Unit tests: ≥80% critical
- [ ] Integration tests: endpoints
- [ ] Coverage total: ≥60%
- [ ] Linting: 0 errores
- [ ] PHPStan level 9

📊 **Indicadores:**
- Coverage: X%
- Test count: N
- Failures: 0
- Warnings: 0

✅ **Criterio:** `vendor/bin/phpunit --coverage-html` muestra ≥60%

### Fase 7: SECURITY REVIEW

🔴 **CRÍTICO:**
- [ ] SQL Injection: 0
- [ ] XSS: 0
- [ ] CSRF: tokens presentes
- [ ] Auth: correcto
- [ ] Secrets: NO hardcodeados
- [ ] composer audit: 0 vulnerables

🟡 **REQUERIDO:**
- [ ] Logs sin sensibles
- [ ] Rate limiting activo
- [ ] Headers security

📊 **Indicadores:**
- composer audit: 0 vulnerables
- Security check: PASA
- Code review: CTO firma

✅ **Criterio:** CTO firma security-checklist.md

### Fase 8: DEPLOYMENT

🔴 **CRÍTICO:**
- [ ] Docker image builds
- [ ] Migrations ready
- [ ] Env variables setted
- [ ] Health checks ok
- [ ] Smoke tests pasan

📊 **Indicadores:**
- Build time: < 5 min
- Health check: 200 OK
- DB connectivity: ✅
- Log output: limpio

✅ **Criterio:** Deploy staging + smoke tests pasan

### Fase 9: MONITOREO

🔴 **CRÍTICO:**
- [ ] Logs en operación
- [ ] Alertas configuradas
- [ ] Backup probado
- [ ] Runbook documentado

📊 **Indicadores:**
- Availability: ≥99%
- Error rate: <1%
- Response time P95: < 5s
- Backup last: < 24h

✅ **Criterio:** 7 días operativo sin incidentes críticos

---

## 🤖 AUDITORÍA IA OPERATIVA

### Framework Auditoría IA en DISATEQ

Auditoría IA (Claude, herramientas automáticas) asegura cumplimiento STANDARDS.

### 1. AUDITORÍA DE CÓDIGO (Semanal o por PR)

**Cuándo:** PR abierto contra main/develop
**Si:** Cambios > 50 líneas

**Proceso:**
```
1. GitHub Actions (automático)
   ├─ composer install
   ├─ vendor/bin/phpunit (tests)
   ├─ vendor/bin/php-cs-fixer check src/ (linting)
   ├─ vendor/bin/phpstan analyse src/ --level=9
   ├─ composer audit
   └─ Si FALLA: bloqueo automático

2. Si PASA: Claude Code Review (manual request)
   ├─ Análisis: patrones, vulnerabilidades, arquitectura
   ├─ Reporte: hallazgos + recomendaciones
   └─ Comentarios en PR

3. Revisión humana (CTO)
   ├─ Revisa comentarios Claude
   ├─ Revisa código 5-10 min
   ├─ Decide: aprueba o pide cambios
   └─ Comentario: "LGTM" + aprobación

4. MERGE (si aprobado)
   ├─ Dev no puede mergear sin aprobación
   └─ GitHub protection rule
```

**Métricas:**
- Coverage: ≥60%
- Linting errors: 0
- Security issues: 0
- Architecture violations: 0

### 2. CUMPLIMIENTO ESTÁNDARES (Quincenal)

**Cuándo:** Cada viernes 15:00

**Proceso:**
```
1. Recopilación datos (automático)
2. Análisis Claude (semiautomático)
   ├─ Compara vs STANDARDS_v1.0
   ├─ Verifica indicadores por etapa
   ├─ Detecta desviaciones
   └─ Calcula % adherence

3. Reporte (automático)
4. Reunión equipo (humano)
   ├─ 30-45 min
   ├─ Revisar hallazgos
   ├─ Discutir desviaciones
   ├─ Priorizar fixes
   └─ Asignar responsables
```

**Métricas:**
- STANDARDS adherence: ≥95%
- Coverage trend: 60%+
- Indicadores por etapa: OK
- Riesgos: Críticos = 0
- Deuda técnica: controlada

### 3. ANÁLISIS PERFORMANCE Y DATOS (Mensual)

**Cuándo:** Primer viernes

**Componentes:**
- Load test (100-500 usuarios)
- Data integrity audit
- Backup validation
- Plan optimización

**Métricas:**
- Response time P95: < 5s
- Error rate: <1%
- Data consistency: 100%

### 4. REPORTES PERIÓDICOS

**Semanal:** PRs merged, vulnerabilidades, coverage trend
**Quincenal:** Auditoría completa (ver sección anterior)
**Mensual:** Performance + Data + Backup

### 5. ROLES Y RESPONSABILIDADES

**Claude IA:**
- Análisis automático
- Detección patrones
- Generación reportes
- Sugerencias (NO decisiones)

**Developer:**
- Arregla hallazgos bloquantes
- Considera mejoras
- Responde comentarios
- Cierra issues

**CTO (Tech Lead):**
- Revisa reportes
- Valida hallazgos
- Aprueba fase
- Escala si crítico

**PM (Product Manager):**
- Integra hallazgos en roadmap
- Prioriza deuda técnica
- Comunica impacto
- Aprueba cambios

### 6. INTEGRACIÓN CICLO MEJORA

```
1. Code written
   ↓
2. Auditoría IA automática
   ↓
3. Dev arregla hallazgos
   ↓
4. CTO aprueba
   ↓
5. Merge + Deploy
   ↓
6. Monitoreo producción
   ↓
7. Auditoría periódica
   ↓
8. Hallazgos nuevos → roadmap
   ↓
[Iteración]
```

---

## 📋 CHANGELOG

### v1.0 (Marzo 2026)

**Foundation Standards**

- Base: 7 meses experiencia operativa Piura
- Validado: 35+ clientes Panel Remoto
- Agnóstico: farmacia, restaurante, clínica, óptica, otros
- Hardware real: PC escritorio + periféricos
- Offline-first obligatorio
- Seguridad integral (código + infra + operativa)
- Lenguaje técnico/sencillo + español peruano
- 🔴🟡🟢 clasificación en todo
- IA-ready (instrucciones paso-a-paso)
- Glosario operativo (20+ términos)
- Indicadores de éxito por etapa (9 fases)
- Auditoría IA operativa integrada
- Listo para GitHub + equipo

**Secciones:**
1. Introducción
2. Principios
3. Herramientas
4. Restricciones Piura
5. Seguridad
6. BD
7. Arquitectura
8. Transacciones
9. Validación
10. Errores
11. Testing
12. CI/CD
13. UI/UX
14. Fases
15. IA
16. Observabilidad
17. Backup
18. Documentación
19. Evolución
20. Matriz decisiones
21. Anti-patrones
22. Instrucción IA
23. Roadmap futuro
24. Glosario
25. Indicadores éxito
26. Auditoría IA
27. Changelog

---

**STANDARDS v1.0 — DOCUMENTO ÚNICO Y DEFINITIVO**

- **Base:** 7 meses Piura + 35+ clientes
- **Aplicación:** Todos productos DISATEQ
- **Estado:** Foundation operativamente validado
- **Vigencia:** Marzo 2026 - Marzo 2027 (review anual)
- **Próximo:** v1.1 con feedback real en Q3 2026

**Este es el estándar. Todo código DISATEQ se alinea a esto.**

Licencia: MIT
