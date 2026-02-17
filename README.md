# Tron Encom 

### El concepto central es adaptar la famosa batalla de las Motos de Luz (Light Cycles) a una experiencia inmersiva.

**Perspectiva**: En lugar de la vista cenital (desde arriba) del arcade clásico, usarás una vista en primera persona (o tercera persona cercana). El jugador es la moto.

**Objetivo**: Derribar a tu oponente haciendolo chocar con tu estela de luz en un 1 vs 1.

**Estética**: Estilo "Synthwave/Cyberpunk". Fondo negro, líneas de neón brillantes (cian y naranja) y suelo de cuadrícula brillante.


**Estructura de Escenas (Flujo del Juego)**
    Para A-Frame, lo ideal no es recargar la página para cambiar de escena, sino usar estados dentro de una misma escena (Single Page Application logic). Sin embargo, conceptualmente tendrás 3 "pantallas":

1. Escena de Menú (UI Overlay):
        • Un panel flotante en 3D.
        • Título grande: "TRON VR".
        • Botón: "START" (Inicia el tick del juego).
        • Instrucciones visuales (ej. "Usa WASD para moverte con jugador 1  y las flechas para jugador 2").

2. Escena de Juego (Arena):
        • El entorno activo.
        • HUD (Heads-Up Display): Un texto flotante pegado a la  cámara que muestra el puntaje actual.

3. Escena de Game Over o Victoria:
        • Se activa al detectar colisión.
        • Muestra "Victory player 1 o 2".
        • Puntaje Final.
        • Botón "RETRY" (Reinicia posiciones y limpia las estelas).

**Funcionalidad y Lógica**
Aquí definimos cómo programar las reglas básicas:
1. **Movimiento y Control:**
    El sistema de navegación se basa en un desplazamiento continuo para simular la inercia de las motocicletas de luz.
    - **Movimiento Automático:** El avance es constante. El usuario no controla la aceleración, solo la dirección.
    - **Mecánica de Rotación:**       Los giros están limitados estrictamente a ángulos de **90 grados**.
    - **Desktop:** Entrada mediante WASD para jugador 1 y flechas para jugador 2.
    - **VR:** Implementación mediante la detección de rotación del visor o uso de los *thumbsticks* del controlador. 
2. **Sistema de Estela (Light Wall):**
        La estela es el elemento arquitectónico generado por el movimiento del jugador que actúa como obstáculo físico.
        * **Generación de Geometría:** Instanciación de entidades `<a-box>` de forma dinámica.
         * **Estrategia de Optimización:**
        * Para evitar la degradación del rendimiento por exceso de nodos en el DOM, se debe escalar un único segmento de pared mientras la trayectoria sea rectilínea.
        * Se crea una nueva entidad de muro únicamente cuando se registra un evento de giro.

3. **Detección de Colisiones (Raycasting)**
        Para una detección precisa en un entorno 3D, se utilizará el método de proyección de rayos.
        * **Implementación:** Se proyecta un componente `raycaster` desde el frente del vehículo.
        * **Lógica de Intersección:** * Los objetos colisionables van a estar filtrados bajo la clase `.wall`.
        * Al detectar una intersección positiva, el sistema disparará la rutina de *Victoria*.

---


### Boceto 

![boceto](/img/tronboceto.jpeg)