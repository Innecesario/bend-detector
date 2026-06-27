# 🎸 Bend Detector

Un analizador de bends y control de afinación para guitarra, pensado para práctica con instrumento en mano.

**[▶ Probar ahora](https://innecesario.github.io/bend-detector/bend-detector.html)**

> El oído se acostumbra a escuchar nuestros propios bends calados y nos autoengañamos. Esta app actúa como un espejo implacable del control de tensión en los dedos.

---

## Qué hace

- **Detección de pitch en tiempo real** — algoritmo McLeod Pitch Method (MPM) sobre el micrófono del dispositivo, sin dependencias externas
- **Selección por cuerda y traste** — interfaz de guitarrista, no de músico de conservatorio: eliges la cuerda (E A D G B e) y el traste (0–24), y la app calcula la nota objetivo automáticamente
- **Tres intervalos de bend** — ½ tono (1 traste), 1 tono (2 trastes), 1½ tonos (3 trastes)
- **Barra de cents en tiempo real** — aguja que muestra la desviación respecto a la nota objetivo: verde (±15¢), amarillo (±35¢), rojo (más de 35¢)
- **Temporizador de mantenimiento** — barra de progreso que exige mantener el bend afinado durante 1 segundo continuo para contar como "conseguido"
- **Gráfica scrolling** — curva de pitch de los últimos 4 segundos para ver la forma del bend
- **Estadísticas de sesión** — intentos, bends conseguidos, porcentaje de éxito y desviación media en cents
- **Pantalla activa** — mantiene la pantalla encendida mientras el micrófono está activo (WakeLock API)
- **Sin dependencias** — un solo archivo HTML, abre y funciona

---

## Cómo usarlo

1. Abre la app en Chrome (móvil o escritorio)
2. Selecciona la **cuerda** y el **traste** de partida
3. Elige el **intervalo del bend** (½, 1 o 1½ tonos)
4. Pulsa **Iniciar micrófono** y acepta el permiso
5. Toca la nota y realiza el bend — la barra de cents y la gráfica responden en tiempo real
6. Mantén la nota afinada 1 segundo para que cuente como "conseguido"

> **Importante**: la app necesita HTTPS para acceder al micrófono. Funciona directamente desde GitHub Pages. Si la abres como archivo local (`file://`), el navegador denegará el permiso de micrófono.

---

## Cómo interpretar los resultados

| Color | Desviación | Significado |
|-------|-----------|-------------|
| 🟢 Verde | ±15 cents | Afinado — el bend está en el objetivo |
| 🟡 Amarillo | ±35 cents | Cerca — un poco corto o pasado |
| 🔴 Rojo | > 35 cents | Desafinado — el bend no llega o se pasa |

La **desviación media** al final de la sesión te dice si tiendes sistemáticamente a quedarte corto (negativo) o a pasarte (positivo).

---

## Configuración del micrófono

La app desactiva el procesado de audio del navegador (`echoCancellation`, `noiseSuppression`, `autoGainControl`) para no distorsionar la señal de la guitarra. Para mejores resultados:

- Usa una **interfaz de audio** o conecta la guitarra al móvil directamente
- Si usas el micrófono del dispositivo, acerca el móvil a la guitarra y toca en limpio (sin efectos de distorsión fuertes)
- La detección es más estable con guitarra eléctrica en limpio o acústica que con distorsión alta

---

## Tecnología

- **Web Audio API** — captura de micrófono con `getUserMedia` y análisis con `AnalyserNode`
- **McLeod Pitch Method (MPM)** — algoritmo de detección de pitch más robusto que YIN con armónicos de guitarra; implementado en JavaScript puro sin librerías externas
- **Clarity hold** — mantiene el último valor válido durante 120ms para evitar parpadeos en los transitorios de ataque del bend
- **WakeLock API** — mantiene la pantalla activa mientras el micrófono está encendido
- **Canvas 2D** — gráfica scrolling de pitch renderizada a 25fps
- **Vanilla JS** — sin frameworks ni dependencias externas

---

## Limitaciones conocidas (v1.0)

- La nota de partida se selecciona manualmente — no hay detección automática de cuándo empieza el bend
- Afinación estándar únicamente (E A D G B e) — no soporta Drop D, Open G ni otras afinaciones alternativas
- La detección puede ser inestable con distorsión alta o mucho ruido de fondo
- No disponible en Safari iOS (la WakeLock API no está soportada; el resto funciona)

---

## Mejoras futuras (v2.0)

- Módulo de vibrato: análisis de amplitud y frecuencia de la oscilación
- Detección automática de la nota de partida
- Afinaciones alternativas
- Exportar estadísticas de sesión

---

## Licencia

MIT — úsalo, modifícalo, compártelo libremente.
