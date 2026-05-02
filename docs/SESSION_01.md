# Session 01 — Setup técnico inicial

**Fecha:** 1 de mayo de 2026
**Duración aproximada:** 1 sesión larga (sin hijo presente)
**Estado del build:** primer build jugable funcional

---

## Logros

Se completó toda la infraestructura técnica del proyecto. Build mínima jugable corriendo en editor: cuadrado se mueve horizontalmente con teclado/gamepad y salta cuando toca suelo. Cámara Cinemachine sigue al jugador.

## Stack confirmado

- Unity 6 LTS (6000.4.5f1) con template Universal 2D (URP 2D)
- Visual Studio Code + C# Dev Kit + Unity extension de Microsoft
- Git + GitHub (repo privado) + Git LFS para binarios
- Input System nuevo (deprecando `Input.GetKey`)
- Cinemachine 3 con Position Composer (no Follow)
- ProBuilder, 2D Animation, PSD Importer instalados pero sin uso aún
- .NET SDK instalado, Xcode instalado pendiente de Apple Developer Program

## Estructura del proyecto

```
Assets/
├── _Project/
│   ├── Art/{Characters, Bosses, Environment, UI, KidDrawings}
│   ├── Audio/{Music, SFX}
│   ├── Prefabs/{Player, Bosses, Environment}
│   ├── Scenes/Level_01.unity
│   ├── Scripts/{Player, Bosses, Core, UI, Utils}
│   ├── Settings/PlayerInputActions.inputactions
│   └── ThirdParty/Kenney/
```

## Configuración crítica aplicada

- **Editor → Asset Serialization: Force Text** (clave para merges de Git)
- **Visible Meta Files**
- Bundle Identifier en Player Settings
- `.gitignore` oficial de Unity
- Git LFS configurado para `*.psd, *.png, *.jpg, *.wav, *.mp3, *.fbx`

## Input Actions (Player Action Map)

| Acción  | Tipo    | Bindings                                                |
|---------|---------|---------------------------------------------------------|
| Move    | Vector2 | WASD, flechas, gamepad leftStick                        |
| Jump    | Button  | Space, gamepad buttonSouth                              |
| Attack  | Button  | J, gamepad buttonWest                                   |
| Pause   | Button  | Escape, gamepad start                                   |

Touch para iOS pendiente — se agrega cuando haya nivel jugable y se conecte iPad.

## Escena Level_01

- Main Camera (Orthographic, Size 5)
- Global Light 2D
- CinemachineCamera (hermano de Player), Position Composer, Tracking Target = Player
- Ground: sprite cuadrado escalado a (20, 1, 1) en (0, -3, 0), Box Collider 2D, Layer = Ground
- Player: sprite cuadrado en (0, 0, 0), Rigidbody2D (Dynamic, Gravity 3, Freeze Rotation Z), Box Collider 2D, PlayerController script
- GroundCheck: hijo de Player en (0, -0.5, 0)

## PlayerController.cs

Script funcional con:
- Movimiento horizontal vía Input System (`linearVelocity`, no `velocity` deprecado)
- Salto con detección de suelo via `Physics2D.OverlapCircle`
- Gizmo verde para visualizar ground check radius
- Awake/OnEnable/OnDisable correctamente manejados para evitar memory leaks de Input System

## Cosas pendientes / decididas pero no implementadas

- **Apple Developer Program ($99/año):** suscribir solo cuando haya hito jugable real (mes 3-4)
- **Touch input para iOS:** agregar con On-Screen Stick/Button cuando haya nivel jugable
- **Switch Lite:** descartado (Nintendo Developer Program inviable para hobbyista)
- **Roblox:** descartado por preferencia explícita

## Próximos caminos posibles

1. **Sesión 1 con el hijo** (recomendado): mostrar build, dejarlo jugar, capturar reacciones e ideas en cuaderno físico
2. **Afinar feel del salto:** coyote time, jump buffering, variable jump height
3. **Diseño del primer jefe en papel:** mecánicas, fases, art assets a dibujar

Decisión sugerida: opción 1 antes que las otras. Sin reacción del hijo, las prioridades son ciegas.

## Lecciones operativas confirmadas

- La prep técnica nunca pasa frente al niño. Solo se le muestra lo jugable o creativo.
- El asterisco en el título de Unity (`Level_01*`) es señal de cambios sin guardar — no salir sin `Cmd+S`.
- Cada sesión termina con commit y push, sin excepción.
- Cinemachine 3 usa `CinemachineCamera` (no "Virtual Camera") y dropdown de Position Control en lugar de Add Component manual.
- En Unity 6, `Rigidbody2D.velocity` está deprecado: usar `linearVelocity`.

## Comando para retomar

Próximo chat se abre con algo como:

> "Seguimos con el platformer. Sesión 01 dejó el build con movimiento y salto. Vamos por [opción]."

---

*Documento generado al cierre de Session 01.*
