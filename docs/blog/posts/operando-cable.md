---
date: 2026-07-22
slug: donde-vive-el-operando
categories:
  - Investigación
---

# ¿Dónde vive el operando? El cable, no el tejido

El [post anterior](lesiones.md) terminó con una pregunta abierta. Lesionando
neuronas encontré que la *operación* ("capital-de") tiene un órgano removible — apagás las
neuronas correctas y el modelo pierde la operación — pero la *entidad* ("Italia") no: no había
tejido que sacar, en ninguna posición donde miré. Una factorización simétrica en el álgebra
(cosa + operación) resultó asimétrica en el tejido. No sabía por qué. Ahora sí, y la respuesta es
linda: **la entidad no es tejido almacenado, es un cable.**

<!-- more -->

## El error de buscar tejido

Una lesión saca cómputo que está *guardado* en algún lugar. Pero la entidad no se guarda en la
posición donde el modelo responde: se **mueve** hasta ahí, por atención, desde el token del país.
"La capital de **Italia** es…" — cuando el modelo llega a "es" y va a responder, tiene que *ir a
buscar* "Italia" unas posiciones atrás. Esa búsqueda es un cable de atención, no una neurona. Y a
un cable no lo lesionás apagando tejido: lo **cortás**.

La herramienta se llama *attention knockout* (Geva et al., [2304.14767](https://arxiv.org/abs/2304.14767),
que la usaron justo para rastrear el flujo de información factual): bloquear el edge de atención
consulta→entidad y ver qué se rompe.

## Cortando el cable

Corté la atención de la posición de respuesta hacia el token de la entidad, barriendo por qué
capas la corto (para encontrar *dónde* se mueve la entidad). Hay una banda clara — **~76% de
profundidad en el modelo chico, ~70% en el grande** — donde cortar ese cable destruye la
recuperación de la entidad. Y es dosis-dependiente: cuanto más ancha la ventana de capas que
corto, más severo. En Qwen3-1.7B la precisión cae de 63% a **36%** (ventana angosta) y a **15%**
(ventana ancha).

Lo lindo aparece leyendo las generaciones crudas. Sin el cable de la entidad, el modelo **mantiene
la operación y pierde la cosa**:

- Egypt / capital → *"the city of **Rome**"* — dice la capital de otro país. Sabe que va una
  ciudad; se equivoca de cuál.
- France / capital → *"a city that is known for its beautiful…"* — sabe que va una ciudad, no
  sabe cuál.
- Brazil / continent → *"located in the southern hemisphere"* — geografía preservada, entidad
  difusa.

Ese es el déficit de operando que las neuronas nunca habían dado, porque no estaba en las
neuronas.

## La disociación por sustrato

El control decisivo: cortar la atención hacia la **palabra-operador** ("capital", "currency") en
la misma banda. Y es **inerte** — la precisión casi no se mueve (61.7% / 63.3% / 80.0% en las tres
configuraciones que probé). El operador no se lee de su palabra por atención; se *construye*, tal
como afirma el paper. La diferencia entidad-vs-operador es contundente (Δ hasta −48 puntos,
McNemar p=1.3e-07) y **replica en el modelo de 8B**.

Entonces las dos mitades de la factorización tienen **dos sustratos distintos**:

- **La operación es tejido almacenado** — vive en neuronas MLP, la lesionás apagándolas.
- **La entidad es ruteo por atención** — vive en un cable, la lesionás cortándolo.

Por eso la lesión de neuronas nunca encontró el operando: no había *tejido de operando* que
encontrar, solo un cable — y una lesión no corta cables, un attention knockout sí.

## La letra chica

- Cortar un **filler funcional** ("the", "of") también degrada algo, así que "cortar atención a X"
  no es perfectamente específico. La disociación limpia y cargada de teoría es entidad-vs-palabra-
  operador (la palabra-operador es lo único genuinamente inerte).
- En el modelo de 8B el déficit de entidad es **degradación**, no sustitución limpia — el modelo
  pierde el hilo en vez de decir prolijamente la entidad equivocada. Misma textura que en el post
  anterior.
- Un modelo y medio, 12 países, 5 relaciones, en inglés. Cada número se recomputa desde artefactos
  ([`scripts/attn_knockout.py`](https://github.com/mpodeley/jspace-qwen) + `verify_numbers.py`).

Que la simetría del *álgebra* (cosa + operación) no implique simetría de la *implementación* —una
es un archivo, la otra es un cable— es, para mí, el tipo de cosa que hace que valga la pena abrir
la caja.

*El detalle técnico completo está en el [cuaderno de resultados](https://mpodeley.github.io/jspace-qwen/findings/)
(§3.9). El recorrido desde el principio: [el paper explicado fácil](https://mpodeley.github.io/assembled-thought/es/explained/).*
