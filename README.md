# Taller: anima los tokens con HyperFrames

Sesión del 4 de noviembre de 2026 · [juandavid.xyz](https://juandavid.xyz)

En este taller vas a hacer un video de 10 segundos con [HyperFrames](https://github.com/heygen-com/hyperframes). El video cuenta un dato real: cuántos tokens de Claude se gastaron editando los videos del Nivelatorio de Vibecoding. El reto tiene dos partes:

1. Que el video cuente un hallazgo, no que solo muestre barras.
2. Que lo logres en el menor número de turnos posible. Anota cuántos usaste.

## Requisitos

- Node.js 22 o superior (`node -v`)
- FFmpeg (`ffmpeg -version`; en Mac: `brew install ffmpeg`)
- Claude Code o cualquier agente que acepte skills

## Pasos

```bash
# 1. Clona el repo y entra a la carpeta
git clone https://github.com/juandaveth/taller-hyperframes-tokens
cd taller-hyperframes-tokens

# 2. Instala el skill de HyperFrames para tu agente
npx skills add heygen-com/hyperframes

# 3. Crea el proyecto y copia los datos
npx hyperframes init tokens-video --example blank
cp datos/tokens-por-video.csv tokens-video/
cd tokens-video

# 4. Abre Claude Code aquí y pega el prompt de prompt.md

# 5. Mira el resultado en el navegador
npx hyperframes preview

# 6. Valida y exporta
npx hyperframes check
npx hyperframes render --output tokens.mp4
```

El prompt base está en [prompt.md](prompt.md). Cámbialo a tu gusto: otro hallazgo, otros colores u otra duración. Lo que no cambia es decidir todo antes de enviarlo.

## Los datos

`datos/tokens-por-video.csv` tiene una fila por video del Nivelatorio:

| Columna | Qué es |
| --- | --- |
| `video` | Nombre de la carpeta del video |
| `formato` | `youtube` (clase) o `reel` (invitación en Instagram) |
| `turnos` | Respuestas de Claude asignadas a ese video |
| `salida` | Tokens que Claude escribió |
| `cache_escrita` | Tokens guardados en caché |
| `cache_leida` | Tokens releídos de la caché |
| `total` | Suma de entrada, salida y caché |
| `duracion_s` | Duración del video final, en segundos |
| `millones_por_min` | Millones de tokens por minuto de video final |
| `pct_cache_leida` | Porcentaje del total que fue relectura de caché |

Algunos hallazgos para animar:

- **Reels contra clases.** Los reels de las sesiones 2 y 3 costaron unas 10 veces más tokens por minuto que las clases (promedio de las clases: 3,0 M/min).
- **Caché.** Entre el 97 % y el 99 % de los tokens fue Claude releyendo la conversación.
- **Duración.** La sesión 1 dura 26 minutos y fue la más barata por minuto.

Son cifras aproximadas. Salen de los registros de Claude Code, y cada turno se asignó al video según la carpeta en la que trabajaba Claude.

## Si terminas rápido

Cambia una sola cosa (un color, el orden de las barras) directamente en el HTML y vuelve a renderizar sin pedírselo a Claude. Vas a ver que un video hecho con código se edita como cualquier página web.
