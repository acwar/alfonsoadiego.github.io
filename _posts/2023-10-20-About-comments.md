---
title: Comentarios en comentarios
date: 2023-10-20 08:00:00 +0200
categories: [Design]
tags: [code]
pin: true
---
Se dice que el libro que mas daño hace no es el que no se lee, sino el que no se entiende. De toda la corriente _Clean Code_ hay un
punto que, al igual que pasa con la S de SOLID, no se toma con la perspectiva debida.

> El código debe explicarse solo

Es una afirmación sencilla y si has escrito suficiente y sobre todo, si has leido suficiente codigo de un tercero, es una máxima de la que 
nadie podria estar en contra. Un código limpio, estructurado y bien nominado ayuda mucho a tener un contexto claro de que se está haciendo,
del flujo de datos y llamadas; de la misma manera que una novela bien estrcuturada y con el ritmo correcto ayuda a completarla y disfrutar
de toda la historia que nos presenta el escritor.

## ¿Donde está el problema?

Como norma general, siguiendo el conocido _Divide and Conquer_, un desarrollo se divide en piezas mas pequeñas que
pueden ser acometidas por un ingeniero, iterando tantas veces sean necesarias hasta que puedes tener el problema
suficientemente granulado.

La solución final es por tanto la suma de todos esos problemas pequeños, ¿a partir de que punto todos esos problemas
no tienen la linealidad suficente para ser leidos sin perder el contexto? ¿Cuanto detalle de un libro puedes retener
en antes de tener que volver a consultarlo? 

## El Como y el Porqué

### Cómo
El ánimo detras de no escribir comentarios viene de plantear únicamente el _como_ se hace un trabajo, es de ahi
que se considera que un comentario es un gasto en mantenimiento que *no* se puede trazar y estamos de acuerdo. Si
tu código necesita explicación de que está haciendo, es claro que no lo hace bien.

> El código debe comunicar tanto a la maquina como al humano que se pretende que se haga.

### Porque 
Lo que el código como líneas únicas no es capaz de transmitir es el **conjunto**, de la misma manera que un solo
párrafo o capitulo de un libro no da la idea de todo el volumen. Por eso los comentarios deben existir para explicar
el **Porqué** del mismo. Lo que para desarrollador puede parecer tremendamente obvio, puede ser un misterio insondable
para otro (y este efecto se acentua en contextos con ownership compartido).

## ¿Que comentar?
Todo aquello que ayude a responde el _porque_ un código existe. Una linea o una función existe porque es parte de un
servicio y/o clase que acomete una porcion del negocio (o eventualmente de la infraestructura), ¿se puede entender esa
clase, entender el negocio que la llevo a existir, leyendo solo el codigo que la implementa?, y si esta clase es 
una dependencia de otra, ¿debemos leerla tambien cuando tratemos de leer alguna de las clases de las que es dependencia?;
"Cuando la leas tendras una idea de que hace y sabras leerla en el contexto de la otra" ¿y no es eso precisamente tener
un comentario en la cabeza que resume esa clase?

Ayuda a poder seguir el hilo lógico de una solucion poder contar con una explicación de sus partes, por ello entiendo
es en el mejor de los intereses comentar:
1. Clases completas: Nunca vamos a elegir un nombre perfecto para una clase ni va a estar en el paquete que nos haga
comprender todo su contexto de un chasquido. Los libros tienen resumenes y prefacios para entender que contienen o que 
vamos a encontrar, las clases tambien los necesitan.
2. Puntos de entrada: Los métodos públicos deben indicar que se espera de ellos. Con el mismo ánimo que existe toda 
una metodologia para definir API publicas, conviene contar con la descripcion de que espera un método publico para 
funcionar, que se supone que te brinda y que puede ocurrir.

## Conclusiones
A mayor es el contexto, mayor es la necesidad de brevedad en las partes para poder comprender el todo. Sabes que tu
coche se mueve por la suma de todas las piezas funcionando, no sabiendo el detalle exacto de como funciona cada pieza.

En entornos con contextos compartidos, tener interacciones claras beneficia mucho la interaccion entre equipos. 
Los cambios frecuentes de los requisitos de negocio en general se centran en como se hacen las cosas pero rara vez
en el _porque_ (en esos raros casos, se discuten implementaciones nuevas).
