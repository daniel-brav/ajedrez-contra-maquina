# PRD · Ajedrez Contra la Máquina

> Documento de requisitos del producto (Product Requirements Document).
> Complétalo en el Sprint 0 (historia H0.3) y pide la aprobación del profesor en un Issue.
> Cada requisito funcional (RF) se convierte en un Issue con la plantilla "Historia de usuario".

| Campo | Valor |
| --- | --- |
| Alumno | Daniel Bravo |
| Proyecto n.º | Ajedrez Contra la Máquina |
| Sitio de referencia | Chess.com / Lichess |
| Compañero revisor | Mariangel Cardona |
| URL desplegada | (se completa en el Sprint 5) |

## 1. Problema

Los aficionados y estudiantes de programación que desean practicar ajedrez de manera rápida y directa carecen de una plataforma web ligera, accesible y sin distracciones publicitarias que les permita jugar contra una inteligencia artificial o un motor local de forma fluida desde cualquier navegador web sin necesidad de instalaciones pesadas.

## 2. Usuarios

- **Usuario principal:** Estudiante o entusiasta del ajedrez que busca partidas rápidas contra la máquina, requiere una interfaz limpia e intuitiva y accede principalmente desde una laptop o PC de escritorio.
- **Usuario secundario:** Profesor o evaluador técnico que revisa el funcionamiento del motor de juego, la arquitectura del software y el cumplimiento de los estándares de desarrollo.

## 3. Objetivo y métrica de éxito

«Un usuario inicia una nueva partida de ajedrez contra la máquina y ejecuta su primer movimiento legal en menos de 5 segundos desde que carga la página».

## 4. Alcance del MVP

Entre 5 y 8 funcionalidades que SÍ entran este semestre.

1. Autenticación y gestión de perfiles de usuario locales o en sesión.
2. Tablero de ajedrez interactivo con validación de movimientos reglamentarios.
3. Motor de juego de inteligencia artificial (IA) para la respuesta automática de la máquina.
4. Historial y registro de movimientos de la partida actual.
5. Cronómetro y control de tiempo por jugador.
6. Sistema de notificaciones visuales para estados de jaque, jaque mate y tablas.

### Funcionalidades → carpetas de `src/` (screaming architecture)

Cada funcionalidad del alcance será una carpeta en `src/`. Nómbralas en inglés y en plural.

| Funcionalidad | Carpeta |
| --- | --- |
| Autenticación | `src/auth` |
| Partidas y Tablero | `src/games` |
| Motor de IA | `src/ai` |
| Historial de jugadas | `src/moves` |
| Perfiles de usuario | `src/users` |

## 5. Fuera de alcance

Lo que NO vas a construir.

- Torneos multijugador masivos en tiempo real con emparejamiento global en línea.
- Pasarelas de pago o tienda de aspectos (*skins*) de piezas de ajedrez.
- Aplicación nativa para dispositivos móviles (iOS / Android).

## 6. Requisitos funcionales

| ID | Requisito | Prioridad (alta, media, baja) |
| --- | --- | --- |
| RF-01 | El sistema debe permitir iniciar una nueva partida seleccionando el nivel de dificultad de la máquina. | Alta |
| RF-02 | El tablero debe validar que los movimientos de las piezas cumplan estrictamente con las reglas del ajedrez. | Alta |
| RF-03 | El motor de IA debe calcular y ejecutar su contra-jugada de forma automática tras el movimiento del usuario. | Alta |
| RF-04 | El sistema debe registrar y mostrar en pantalla el historial en notación algebraica de los movimientos realizados. | Media |
| RF-05 | El sistema debe detectar y notificar las condiciones de fin de partida (jaque mate, tablas o ahogado). | Alta |

## 7. Requisitos no funcionales

- Responsive, móvil primero (375 px y 1280 px).
- Lighthouse ≥ 90 en Accesibilidad y Buenas prácticas.
- 0 errores en la consola del navegador.
- Funciona con 10.000 registros sin congelarse.

## 8. Modelo de datos

Diagrama entidad-relación y tablas PostgreSQL con tipos, claves y restricciones.
GitHub dibuja diagramas Mermaid; edita este ejemplo:

```mermaid
erDiagram
  USUARIO ||--o{ PARTIDA : juega
  PARTIDA ||--|{ MOVIMIENTO : contiene
  
  USUARIO {
    int id PK
    text username
    text email
    timestamptz creado_en
  }
  PARTIDA {
    int id PK
    int usuario_id FK
    text estado
    text dificultad
    timestamptz fecha_inicio
  }
  MOVIMIENTO {
    int id PK
    int partida_id FK
    int numero_jugada
    text notacion_algebraica
    timestamptz realizado_en
  }
