---
title: La Importancia de Comprender el Código
date: 2023-10-20 08:00:00 +0200
categories: [Design]
tags: [code]
pin: true
---
Se sostiene a menudo que el libro más perjudicial no es aquel que no se lee, sino el que no se comprende. Dentro de la corriente del "Clean Code", hay un aspecto que, similarmente a la "S" de SOLID, no se aborda con la perspectiva adecuada.

## El código debe ser autodescriptivo

Esta es una premisa simple, pero para cualquiera que haya escrito o leído código ajeno, resulta ser un principio con el que es difícil no estar de acuerdo. Un código limpio, estructurado y correctamente denominado ofrece una visión clara del propósito, el flujo de datos y las llamadas, al igual que una novela bien estructurada y con ritmo adecuado facilita su lectura y comprensión.

## ¿Dónde radica el desafío?

Siguiendo el principio de "Divide y vencerás", un desarrollo suele segmentarse en partes más pequeñas para ser gestionadas por un ingeniero, y esta división se repite hasta granularizar el problema al máximo. No obstante, la cuestión se centra en entender: ¿hasta qué punto la solución compuesta por todas estas partes mantiene una coherencia que permita su lectura sin perder el contexto global?

## El Cómo y el Porqué

- **Cómo**: La tendencia a evitar comentarios se origina en el deseo de centrarse en cómo se realiza una tarea. Si el código necesita una explicación sobre lo que hace, claramente no está bien estructurado. Debe comunicar tanto a la máquina como al programador el propósito detrás de él.
  
- **Porqué**: Lo que el código no puede transmitir en su totalidad es la visión global. Así como un solo capítulo de un libro no ofrece una comprensión completa, los comentarios son necesarios para explicar el "porqué" detrás del código. Lo que puede ser evidente para un desarrollador puede no serlo para otro, especialmente en contextos con múltiples contribuidores.

## ¿Qué se debe comentar?

Es crucial comentar todo aquello que responda al "porqué" de la existencia del código. Se debe poder comprender una clase o función dentro del negocio o infraestructura sin tener que bucear en detalles superfluos. Por tanto, es esencial comentar:

1. **Clases completas**: Es improbable que un nombre por sí solo describa perfectamente una clase. Del mismo modo que los libros tienen resúmenes, las clases también requieren una breve descripción.
  
2. **Puntos de entrada**: Los métodos públicos deben aclarar sus expectativas y responsabilidades. Es esencial describir lo que se espera de un método público, lo que ofrece y las posibles contingencias.

## Conclusiones

Cuanto más amplio es el contexto, más se necesita concisión en los detalles para comprender el conjunto. Saber que un coche funciona es el resultado de todas sus piezas en conjunto, no de conocer en profundidad cada componente. En ambientes colaborativos, clarificar las interacciones es crucial para una efectiva cooperación entre equipos. Mientras que los cambios en requisitos empresariales suelen enfocarse en el "cómo", el "porqué" raramente cambia, y cuando lo hace, se discuten nuevos enfoques.
