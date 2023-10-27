---
title: Contaminacion de decode404 en Feign.Builder
date: 2023-10-27 08:00:00 +0200
categories: [Java]
tags: [code spring feign]
pin: true
image:
  path: /common/coments-image.jpeg
---

## Introducción

Spring Cloud OpenFeign ofrece una integración impecable para crear clientes HTTP. Sin embargo, cuando se trata de ciertas configuraciones como `decode404`, surge un error sutil pero crucial. Una vez que se instancia un cliente Feign con `decode404` configurado, esta configuración se propaga inesperadamente a otros clientes Feign debido a la naturaleza singleton del `Feign.Builder` dentro del contexto de Spring. Este artículo arroja luz sobre este comportamiento, sus implicaciones y una posible mitigación.

## Profundizando en `FeignClientFactoryBean`

### El Rol de `FeignClientFactoryBean`

`FeignClientFactoryBean` es esencial en Spring Cloud OpenFeign. Es responsable de construir el cliente Feign basado en las configuraciones dadas. Uno de los componentes que utiliza es el `Feign.Builder`, que, en algunas configuraciones, podría ser una instancia de `HystrixFeign.Builder`.

### La Naturaleza Singleton de `Feign.Builder`

El comportamiento predeterminado de Spring es crear beans como singletons, lo que significa que solo hay una instancia compartida de un bean en todo el contexto de Spring. Esto es eficiente en términos de memoria y coste de instanciación. Sin embargo, puede llevar a efectos secundarios no deseados si ese bean retiene un estado que afecta a otras partes del sistema, especialmente si el estado es mutable.

Cuando `FeignClientFactoryBean` configura el `Feign.Builder`, considera si la bandera `decode404` está activa. Si lo está, el constructor se modifica para manejar las respuestas 404 de una manera específica. Pero aquí está el descuido: `FeignClientFactoryBean` no tiene en cuenta la reconfiguración o el manejo del caso opuesto, es decir, cuando `decode404` está configurado como `false`.

Dado que `Feign.Builder` (ya sea uno predeterminado o `HystrixFeign.Builder`) se almacena como un bean singleton, cualquier modificación a su estado, como la activación de la bandera `decode404`, persiste en todo el contexto de la aplicación. Por lo tanto, todos los clientes Feign generados posteriormente heredarán esta configuración.

## Implicaciones

1. **Comportamiento Inesperado**: Los clientes Feign, que se esperaría que tratasen las respuestas 404 como errores, podrían manejarlas como respuestas válidas, lo que llevaría a flujos lógicos inesperados.
2. **Desafíos en Depuración**: Diagnosticar este comportamiento puede ser desafiante ya que los desarrolladores podrían no relacionar inmediatamente el comportamiento de un cliente Feign con la configuración de otro.
3. **Configuración Inconsistente**: Incluso si los desarrolladores intentan configurar explícitamente `decode404` como `false` para los clientes posteriores, el estado contaminado del constructor significa que no se aplica la configuración deseada.

## Mitigación

Una estrategia de mitigación potencial implica un poco de orquestación en el proceso de creación del cliente:

- **Configuración Ordenada**: Define una clase de configuración donde los clientes Feign se declaran en un orden específico. Asegúrate de que los clientes que no requieran la propiedad `decode404` se definan (y por lo tanto se instancien) antes que aquellos que sí lo hagan. Al hacer esto, los clientes que necesitan la propiedad `decode404` desactivada se configurarán antes de que ocurra cualquier modificación en el estado de `Feign.Builder`.

Este enfoque aprovecha la naturaleza secuencial de la instanciación y configuración de beans, garantizando que el `Feign.Builder` compartido esté en su estado predeterminado para los clientes iniciales y solo se modifique cuando sea necesario para los clientes posteriores.

## Conclusión

Aunque Spring Cloud OpenFeign ofrece una abstracción potente para crear clientes HTTP, es esencial estar al tanto de matices como la contaminación de `decode404` en `FeignClientFactoryBean`. Esto destaca la importancia de comprender las herramientas que usamos y su funcionamiento interno, especialmente al tratar con un estado compartido y mutable en un contexto singleton. Con decisiones informadas, los desarrolladores pueden aprovechar el poder de la herramienta mientras evitan posibles problemas, lo que lleva a arquitecturas de microservicios más robustas.
