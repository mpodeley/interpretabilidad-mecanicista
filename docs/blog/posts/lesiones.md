---
date: 2026-07-17
slug: lesionar-un-modelo-de-lenguaje
categories:
  - Investigación
---

# Lesionar un modelo de lenguaje

Los neuropsicólogos entendieron el cerebro, en buena parte, rompiéndolo: un paciente pierde una
región por un ACV y de golpe no puede nombrar objetos aunque habla fluido, o habla en telegrama
aunque entiende todo. Cada déficit *selectivo* es un mapa de qué hace cada pieza. Un modelo de
lenguaje se deja lesionar con una precisión que ningún neurocirujano soñó — podés apagar una
neurona exacta, en todas las posiciones, y medir qué se rompe. Así que lo hice.

<!-- more -->

La pregunta venía de [mi paper](../../mi-investigacion.md): el pensamiento de un modelo sobre
"la capital de Italia" se separa en dos piezas — *la cosa* (Italia) y *la operación*
(capital-de). Si son piezas de verdad, deberían vivir en **tejido** distinto. ¿Hay un grupo de
neuronas que hace "capital-de", separable de las que manejan "Italia"? Y si lo lesionás, ¿el
modelo sufre una afasia específica?

Reglas del juego, prestadas de la neuropsicología y adaptadas con la disciplina de controles del
paper:

1. **Localizar con un contraste.** El diseño factorial del paper (12 países × 5 relaciones) *es*
   un localizador de fMRI: para cada neurona calculo cuánta de su actividad explica *la
   operación* versus *la entidad*. Eso rankea las neuronas por selectividad, exactamente como un
   vóxel se rankea por su respuesta a un contraste.
2. **Remover el tejido, no empujarlo.** Una lesión no es *steering*: la neurona se apaga en
   **todas** las posiciones, fijada a su valor medio, y el prompt hace la pregunta **verdadera**.
   No estamos inclinando al modelo hacia una respuesta; le sacamos una pieza y miramos qué se
   cae.
3. **El déficit tiene que ser selectivo.** Romper todo no enseña nada. La vara es: la lesión
   dirigida daña *su* función y deja intactas las demás — y controles del mismo tamaño, en las
   mismas capas, con la misma magnitud de activación, **no** reproducen el efecto.

## Primero, el mapa de lo que no se puede tocar

Antes de buscar funciones hay que saber dónde está la infraestructura. Ablé **cada una de las
448 cabezas de atención** de Qwen3-1.7B, una por vez. El resultado es un cerebro con una anatomía
sorprendentemente humana: **2 cabezas de 448 son intocables** — una sola, L1H5, multiplica la
perplejidad por **19.7** cuando la apagás; otra por 4.4 — y las **446 restantes** se pueden
quitar de a una con costo casi nulo (la mediana cuesta ×1.003). Un tronco encefálico diminuto y
una corteza enorme y redundante.

Ese detalle no es decorativo: es la razón por la que todos los controles tienen que estar
**pareados por profundidad**. Un control aleatorio global que por azar agarre L1H5 "le gana" a
cualquier lesión dirigida por motivos que no tienen nada que ver con la función. (Y de hecho
pasa: un control aleatorio de 48 cabezas que se traga a L1H5 dispara la perplejidad ×78.)

Y acá el primer hallazgo inesperado: **el tronco encefálico es un fenómeno de modelo chico.** El
mismo barrido en Qwen3-8B — las 1152 cabezas, una por vez — encuentra **cero** cabezas críticas.
Ni una sola supera ×2; la peor cuesta menos que eso. El modelo chico guarda una cabeza que no
puede perder; el grande, cuatro veces su tamaño, no guarda ninguna. *(Por qué — si la función se
distribuyó o simplemente sobra a escala — es una pregunta que este post abre y ataca al final.)*

## Validar el método con una función conocida

Antes de confiar en el bisturí sobre una función desconocida, lo pruebo en una que el campo ya
resolvió: las **induction heads**, el circuito que copia patrones del contexto (lo cuenta la
[página de circuitos del curso](../../curso/circuitos.md)). Localizarlas y lesionar las 48 más
selectivas: la capacidad de copiado colapsa **−79%**, mientras la perplejidad general
(×1.24), la aritmética (100%) y la recuperación de hechos quedan intactas. Los controles pareados
no la tocan. El método remueve una función conocida de forma selectiva. Luz verde.

## El resultado: la operación tiene órgano, la entidad no

Acá viene la asimetría, y es más interesante que la simetría que esperaba.

**La red-operador es tejido removible de verdad.** Lesionar las neuronas selectivas de operador
produce el síntoma exacto que había pre-registrado — el modelo responde *sobre el país correcto,
pero con la relación equivocada* — en **los cuatro tamaños de lesión**, ordenado por dosis, en
**los dos modelos**. Con 512 neuronas (de ~172 mil) la recuperación relacional cae de 61.7% a
**18.3%**, y el test estadístico honesto (Fisher exact contra el pool de todos los controles,
2160 celdas, corregido por Bonferroni) da p desde 8.9e-05 hasta **5.5e-09**. La perplejidad se
preserva en todo el rango. Es una afasia específica: el modelo "olvida qué le preguntaste" sin
perder el lenguaje.

**La red-operando no tiene órgano removible.** La predicción era que, lesionada, el modelo diría
*la capital de otro país* (relación intacta, entidad perdida). No pasa. En la posición de
consulta, la lesión no hace nada por encima de los controles. Y probé la hipótesis mecánica
obvia — que la entidad vive en el token del país, no en la consulta — lesionando **ahí**: falla
también. Lo que se rompe ahí es destrucción genérica (la perplejidad se dispara) o, en el modelo
grande, *la firma del operador otra vez*. Dos hipótesis muertas. La entidad no tiene, en ninguno
de los dos lugares donde la busqué, un tejido que puedas quitar para producir su déficit
específico.

Esa es la novedad, y es honesta: **una factorización simétrica en el álgebra no es simétrica en
el tejido.** El modelo *sí* separa la operación de la entidad —eso lo probó el paper por fuera—
pero la operación tiene una región lesionable y la entidad se comporta como algo más
distribuido, más redundante, sin un órgano que apagar. Es un paradigma de **operadores**.

Un detalle de disciplina que me gusta contar porque casi me como un espejismo: cuando leí las
generaciones crudas bajo la lesión de operando *creí* ver una anomia bellísima — *"es una
ciudad… no sé cuál"*. Pero el scoring riguroso mostró que "degradado" es el sumidero donde cae
**toda** falla (los controles ya están en ~37% de degradación), así que no puede contar como
firma de nada. Estaba leyendo señal en el pozo. El resultado sobrevive sin ese adorno; el adorno
no sobrevivía a su propio control.

## ¿Áreas o redes?

La última pregunta era geométrica: cuando una función *sí* tiene tejido, ¿está concentrada en un
lugar (un "área", como el área de Broca) o desparramada (una "red")? La respuesta —midiendo la
entropía de la distribución por capas contra un null de neuronas aleatorias— es que **depende de
la función**. Las redes de operador y operando están **concentradas**, apiladas al 84–93% de
profundidad (justo donde el paper había encontrado la palanca causal, hallada de nuevo por un
método que no sabe nada del paper). En cambio la distinción texto-vs-símbolo está **totalmente
distribuida** (indistinguible del azar). Un modelo con áreas localizadas y redes difusas
conviviendo — igual que un cerebro.

## Post-scriptum: ¿por qué el chico necesita una cabeza que el grande no?

Hay dos maneras en que el modelo grande podría "no necesitar" esa cabeza: la función se
distribuyó en un **conjunto** de cabezas (ninguna sola es crítica, pero un grupo sí), o
simplemente no la necesita. Una búsqueda greedy las distingue — quitar la cabeza cuya ablación
cuesta más, repetir.

En 1.7B el daño se **compone catastróficamente**: L1H5 sola ×19.7, y agregando de a una las
peores, la perplejidad trepa a ×270, ×23.000, hasta **×2.8 millones con 8 cabezas**. Un núcleo
crítico diminuto pero interdependiente. En 8B el mismo procedimiento con 12 cabezas llega a
**×4.3**. No hay núcleo catastrófico — ni una cabeza, ni un conjunto chico. Seis órdenes de
magnitud de diferencia. La respuesta es la segunda: **el modelo grande no concentra su cómputo
crítico en ningún puñado de cabezas.** El chico apila trabajo que no puede perder en unas pocas;
el grande lo desparrama tanto que ningún grupo chico importa.

¿Y qué *hace* L1H5? La hipótesis obvia —que sea un *attention sink*, una cabeza que vuelca casi
toda su atención al primer token (un patrón documentado como crítico)— **es falsa**. Sinks hay:
L19H4 manda el 97.4% de su atención al token 0. Pero las cabezas críticas no son sinks: L1H5
manda solo el **1.3%** (puesto 430 de 448). Es intocable por *otra* razón, todavía sin
identificar — un cabo suelto, honesto.

## La letra chica

- Todo esto es **un modelo y medio** (Qwen3-1.7B, con réplica en 8B) sobre 12 países y 5
  relaciones, en inglés. La red-operador replica en las dos escalas; la geometría también. El
  brazo de cabezas del modelo chico es ilegible por culpa del sink, y el del grande es legible
  pero no dice nada (la operación, a escala, no es un puñado de cabezas).
- Es **inspiración metodológica**, no una analogía literal con el cerebro. No comparé contra
  datos de fMRI ni afirmo que una capa del modelo "es" un área de Brodmann. Presté el método —
  localizar, lesionar, exigir selectividad — y todos los claims son sobre el modelo.
- Como siempre acá: cada número se recomputa desde artefactos persistidos
  ([`scripts/lesion_*.py`](https://github.com/mpodeley/jspace-qwen) + `verify_numbers.py`), y
  cada afirmación convive con el control que podría haberla matado. Un par de esos controles ya
  me pescaron dos sobre-afirmaciones en el camino; quedaron corregidas en el registro.

*Los detalles completos, con las tablas y los p-values, están en el
[cuaderno de resultados](https://mpodeley.github.io/jspace-qwen/findings/) (Parte 3). Si querés
el contexto del paper primero: [el paper explicado fácil](https://mpodeley.github.io/assembled-thought/es/explained/).*
