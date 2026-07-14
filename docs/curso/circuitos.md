# Circuitos

*Dentro del gigante hay algoritmos chiquitos y legibles, con piezas que cumplen roles. Ya
encontramos algunos.*

## De piezas sueltas a algoritmos

Hasta acá tenemos [features](features.md) (los conceptos-átomo) y
[herramientas causales](intervenciones.md) (para probar qué hace cada cosa). Un **circuito** es
el siguiente nivel: un **conjunto de componentes conectados** — cabezas de atención, MLPs,
features — que juntos implementan un algoritmo reconocible. No "el modelo suma", sino: *esta*
cabeza copia *esto* acá, *aquella* lee lo copiado y hace *aquello*, y la salida explica el
comportamiento.

La palabra viene del [ensayo fundacional de Distill](https://distill.pub/2020/circuits/zoom-in/)
(2020), que propuso el programa completo: las redes están llenas de sub-máquinas conectadas, y
se pueden mapear una por una, como hizo la biología con las rutas metabólicas.

## La estrella: induction heads

El circuito más famoso del campo resuelve un problema que parece trivial: **copiar patrones**.
Si el texto ya dijo "…Martín Fierro… " y más adelante aparece otra vez "Martín", ¿qué token
conviene predecir? "Fierro". Los transformers aprenden un mecanismo de dos piezas para esto:

1. Una cabeza de un piso temprano le anota a cada token información sobre **cuál fue el token
   anterior** (una cabeza "de token previo").
2. Una cabeza de un piso posterior — la **induction head** — usa esa anotación para buscar
   "¿dónde apareció antes el token actual?" y **copiar lo que vino después de esa aparición**.

Dos cabezas cooperando a través del [residual stream](transformer.md): un algoritmo de
búsqueda-y-copia, legible, verificado con las
[tres herramientas causales](intervenciones.md). Y el hallazgo más intrigante
([Anthropic, 2022](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html)):
durante el entrenamiento estas cabezas aparecen de golpe, en un "clic" — y ese momento coincide
con el salto en la capacidad del modelo de **aprender de los ejemplos que le das en el prompt**
(el famoso *in-context learning*). Un circuito concreto, ligado causalmente a una capacidad que
usás todos los días.

## El caso de estudio: IOI

El otro clásico:
[*Indirect Object Identification*](https://arxiv.org/abs/2211.00593) (Wang et al., 2022).
La tarea: *"Cuando Juan y María fueron al kiosco, Juan le dio una gaseosa a ___"* → "María".
Fácil para vos; ¿cómo lo hace GPT-2?

Usando activation patching de manera sistemática — la aplicación estrella de la
[página anterior](intervenciones.md) — los autores mapearon un circuito de **~26 cabezas de
atención organizadas en roles con nombre**: cabezas que detectan el nombre duplicado (Juan
aparece dos veces), cabezas que *inhiben* esa repetición, y "name movers" que copian el nombre
restante (María) a la posición de la respuesta. Cada rol verificado interviniéndolo; hasta
encontraron cabezas de respaldo que se despiertan cuando ablás las principales.

IOI importa menos por la tarea (es un juguete) que por la demostración: **un comportamiento
lingüístico completo, reducido a un diagrama de piezas con funciones** — y una advertencia:
tomó *meses* de trabajo experto para una tarea diminuta en un modelo chico.

## El problema del costo (y el puente a lo que sigue)

Esa advertencia es central al estado del campo hoy. Encontrar circuitos a mano no escala:
modelos mil veces más grandes, infinitas tareas, meses por circuito. Las dos respuestas
actuales:

- **Automatizar el descubrimiento** — que un algoritmo proponga el circuito y las intervenciones
  lo verifiquen. Los *attribution graphs* de la [página siguiente](sae.md) son el estado del
  arte de esta ruta.
- **Cambiar la unidad de análisis** — quizás las cabezas y neuronas no son las piezas correctas,
  y los circuitos se ven más limpios escritos en el lenguaje de [features](features.md)
  desenredados. También en la página siguiente.

!!! note "Honestidad técnica"
    Los circuitos encontrados hasta ahora explican *parcialmente* sus comportamientos (el de
    IOI reproduce la conducta en gran medida, no al 100%), en modelos chicos, en tareas
    elegidas por ser tratables. La apuesta del campo es que el método escala; el jurado sigue
    deliberando.

## Para profundizar

- [In-context Learning and Induction Heads](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html) —
  el paper de las induction heads.
- [Interpretability in the Wild (IOI)](https://arxiv.org/abs/2211.00593) — el paper del
  circuito de IOI.
- [Zoom In: An Introduction to Circuits](https://distill.pub/2020/circuits/zoom-in/) — el
  manifiesto original, todavía la mejor lectura conceptual.

**Siguiente y última parada:** desenredar los features automáticamente, y los mapas de
pensamiento más grandes dibujados hasta ahora. [SAEs y grafos de atribución →](sae.md)
