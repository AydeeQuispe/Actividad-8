Modelos de memoria distribuida vs. memoria compartida

En la computación de alto rendimiento, los modelos de memoria desempeñan
un

papel crucial en la forma en que los sistemas gestionan y acceden a los
datos. Dos

modelos prominentes son la memoria compartida y la memoria distribuida.
Ambos

tienen sus ventajas y desafíos únicos y son adecuados para diferentes
tipos de

aplicaciones y arquitecturas de sistemas.

**Memoria** **compartida**

En el modelo de memoria compartida, múltiples procesadores tienen acceso
a una

región común de memoria. Este enfoque es característico de las
arquitecturas

multiprocesador simétrico (SMP), donde todos los procesadores comparten
la

misma memoria física y pueden leer y escribir en ella. Las principales
características

y desafíos del modelo de memoria compartida son:

> ● Acceso Uniforme: Los procesadores pueden acceder a cualquier
> ubicación de
>
> la memoria compartida con el mismo tiempo de acceso. Esto facilita la
>
> programación, ya que los desarrolladores pueden escribir programas sin
>
> preocuparse de la ubicación física de los datos.
>
> ● Coherencia de Caché: Uno de los mayores desafíos en los sistemas de
>
> memoria compartida es mantener la coherencia de caché. Dado que
>
> múltiples procesadores pueden almacenar en caché los mismos datos, es
>
> crucial asegurarse de que cualquier modiﬁcación se reﬂeje en todas las
>
> cachés. Protocolos como MESI (Modiﬁcado, Exclusivo, Compartido,
> Inválido)
>
> y MOESI (Modiﬁcado, Exclusivo, Compartido, Inválido, Propietario) se
> utilizan
>
> para gestionar esta coherencia.
>
> ● Sincronización: La sincronización es vital en los sistemas de
> memoria
>
> compartida para prevenir condiciones de carrera y garantizar la
> consistencia
>
> de los datos. Los mecanismos comunes de sincronización incluyen
>
> semáforos, mutexes y barreras. Aunque estos mecanismos son efectivos,
>
> pueden introducir sobrecarga y complicar la programación.
>
> ● Escalabilidad: La escalabilidad es un desafío signiﬁcativo en los
> sistemas de
>
> memoria compartida. A medida que se añaden más procesadores, el tráﬁco
>
> en el bus de memoria y la complejidad de mantener la coherencia de
> caché
>
> aumentan, lo que puede degradar el rendimiento.
>
> ● Programación: La programación en sistemas de memoria compartida es
>
> generalmente más sencilla debido a la uniformidad en el acceso a la
>
> memoria. Los desarrolladores pueden utilizar modelos de programación
>
> paralela como OpenMP, que simpliﬁcan la creación de aplicaciones
> paralelas.

**Estrategias** **de** **memoria** **compartida**

En sistemas multiprocesador donde múltiples procesadores acceden y
comparten la

misma memoria física, es crucial implementar estrategias efectivas para
garantizar

el rendimiento, la coherencia y la consistencia de los datos. A
continuación, se

explican las principales estrategias de memoria compartida, incluyendo
la

localización de datos, la reducción de contención, y la minimización de
la latencia de

caché.

1 . Localización de datos

La localización de datos en sistemas de memoria compartida implica
organizar y

almacenar los datos de manera que se optimice el acceso a la memoria por
parte de

los procesadores, minimizando la latencia de acceso y mejorando el
rendimiento

general del sistema.

Ejemplo: En una aplicación de procesamiento de imágenes, almacenar los
datos de

píxeles que se procesan juntos en ubicaciones contiguas de memoria puede
mejorar

signiﬁcativamente el rendimiento debido a un acceso más eﬁciente a la
caché.

Técnicas:

> ● Localidad espacial: Los datos que se utilizan juntos deben
> almacenarse cerca
>
> unos de otros en la memoria. Por ejemplo, las estructuras de datos
> contiguas
>
> en matrices.
>
> ● Localidad temporal: Los datos que se utilizan con frecuencia deben
>
> almacenarse en cachés para accesos rápidos. Por ejemplo, variables
> locales
>
> y datos frecuentemente accedidos en cachés L1 o L2.

Ventajas:

> ● Acceso rápido: Los procesadores pueden acceder rápidamente a los
> datos
>
> que necesitan, mejorando la eﬁciencia del sistema.
>
> ● Mejor utilización de la caché: Almacenar datos relacionados cerca
> unos de
>
> otros maximiza la eﬁciencia del uso de la caché.

Desafíos:

> ● Diseño complejo: Organizar los datos de manera eﬁciente puede ser
> complejo
>
> y requerir un diseño cuidadoso de la memoria.

2 . Reducción de contención

La contención ocurre cuando múltiples procesadores intentan acceder

simultáneamente a la misma ubicación de memoria, lo que puede causar
conﬂictos

y retrasos. Reducir la contención es crucial para mantener un
rendimiento óptimo en

sistemas de memoria compartida.

Ejemplo:

En una base de datos concurrente, múltiples transacciones pueden
intentar acceder

y modiﬁcar el mismo registro al mismo tiempo. La contención se puede
reducir

mediante el uso de particiones y técnicas de control de concurrencia.

Técnicas:

> ● Descomposición de tareas: Dividir las tareas en subtareas
> independientes que
>
> acceden a diferentes partes de la memoria, reduciendo la necesidad de
>
> acceso concurrente a las mismas ubicaciones.
>
> ● Bloqueo de granularidad ﬁna: Utilizar bloqueos más especíﬁcos (por
> ejemplo,
>
> a nivel de ﬁla en lugar de a nivel de tabla) para reducir la
> probabilidad de
>
> contención.
>
> ● Algoritmos concurrentes sin bloqueos: Implementar estructuras de
> datos y
>
> algoritmos que minimicen o eliminen el uso de bloqueos, como listas
>
> enlazadas sin bloqueo o pilas concurrentes.

Ventajas:

> ● Mejor concurrencia: Menos bloqueos y esperas entre procesadores,
>
> mejorando la eﬁciencia y el rendimiento.
>
> ● Mayor escalabilidad: Permite que el sistema escale mejor con el
> aumento del
>
> número de procesadores.

Desafíos:

> ● Complejidad de implementación: Implementar algoritmos concurrentes
> sin
>
> bloqueos puede ser técnicamente desaﬁante.

3 . Minimización de la latencia de caché

La latencia de caché se reﬁere al tiempo que tarda un procesador en
acceder a los

datos almacenados en caché. Minimizar esta latencia es esencial para
maximizar el

rendimiento en sistemas de memoria compartida.

Ejemplo:

En un sistema de procesamiento de transacciones ﬁnancieras, es crucial
acceder

rápidamente a los datos de las cuentas. Mantener estos datos en caché
reduce la

latencia y mejora el rendimiento del sistema.

Técnicas:

> ● Prefetching de datos: Anticipar qué datos serán necesarios
> próximamente y
>
> cargarlos en caché antes de que se soliciten.
>
> ● Políticas de reemplazo de caché: Utilizar políticas eﬁcientes de
> reemplazo de
>
> caché, como LRU (Least Recently Used) para mantener en caché los datos
>
> más relevantes.
>
> ● Agrupación de datos: Agrupar datos que se utilizan conjuntamente
> para que
>
> se almacenen juntos en caché y se accedan de manera más eﬁciente.
>
> ● Tamaño óptimo de caché: Determinar el tamaño óptimo de las cachés en
>
> diferentes niveles (L1, L2, L3) para equilibrar el espacio de
> almacenamiento y
>
> la latencia de acceso.

Ventajas:

> ● Mayor rendimiento: Acceso rápido a datos frecuentemente utilizados,
>
> mejorando la eﬁciencia del sistema.
>
> ● Reducción de latencia: Menos tiempo de espera para acceder a datos
>
> almacenados en caché.

Desafíos:

> ● Gestión de caché: Determinar qué datos almacenar y cuándo
> reemplazarlos
>
> puede ser complejo y requerir una gestión cuidadosa.
>
> ● Coherencia de caché: Mantener la coherencia de los datos en cachés
>
> múltiples es un desafío técnico signiﬁcativo.

4 . Coherencia y consistencia de caché

La coherencia de caché asegura que todas las copias de un dato en
diferentes

cachés sean iguales. La consistencia de caché garantiza el orden en que
las

operaciones de memoria son vistas por diferentes procesadores.

Ejemplo:

> En una aplicación de simulación cientíﬁca, varios procesadores pueden
> acceder y
>
> actualizar los mismos datos. Es crucial que todos los procesadores
> vean los
>
> mismos datos actualizados para evitar errores en los cálculos.
>
> Técnicas:
>
> ● Protocolos de coherencia (e.g., MESI): Utilizar protocolos de
> coherencia de
>
> caché como MESI (Modiﬁcado, Exclusivo, Compartido, Inválido) para
> asegurar
>
> que las actualizaciones de datos se propaguen correctamente a todas
> las
>
> cachés.
>
> ● Barreras de memoria: Implementar barreras de memoria para asegurar
> que
>
> todas las operaciones de lectura y escritura se completen antes de que
> se
>
> continúen otras operaciones.
>
> Ventajas:
>
> ● Datos consistentes: Asegura que todos los procesadores trabajen con
> los
>
> mismos datos, evitando errores.
>
> ● Sincronización eﬁciente: Permite la sincronización eﬁciente entre
> múltiples
>
> procesadores.
>
> Desafíos:
>
> ● Sobrecarga de comunicación: La propagación de actualizaciones entre
>
> cachés puede introducir sobrecarga de comunicación.
>
> ● Complejidad técnica: Implementar y gestionar protocolos de
> coherencia
>
> puede ser técnicamente desaﬁante.

keyboard_arrow_down

> Ejemplos
>
> ● Un sistema de memoria compartida típico podría ser un servidor de
> múltiples
>
> núcleos donde todos los núcleos pueden acceder a una base de datos en
>
> memoria. Si un núcleo actualiza un registro en la base de datos, todos
> los
>
> demás núcleos deben ver esta actualización inmediatamente, lo cual se
>
> gestiona a través de mecanismos de coherencia de caché.
>
> ● Consideremos una aplicación de simulación cientíﬁca que corre en un
>
> servidor SMP. Los diferentes núcleos del servidor pueden trabajar en
>
> diferentes partes de la simulación, pero necesitan acceder y
> actualizar una
>
> memoria compartida donde se almacenan las variables globales y los
>
> resultados parciales de la simulación. Utilizando OpenMP, los
> desarrolladores
>
> pueden paralelizar el bucle principal de la simulación para que cada
> núcleo
>
> trabaje en diferentes iteraciones

**Memoria** **distribuida**

En contraste, el modelo de memoria distribuida implica que cada
procesador tiene

su propia memoria local. Los procesadores se comunican entre sí mediante
un

mecanismo de paso de mensajes para compartir datos. Este modelo es

característico de los sistemas de procesamiento paralelo de memoria
distribuida

(DMPP) y las arquitecturas de clústeres.

> ● Autonomía de memoria: Cada procesador tiene acceso rápido a su
> propia
>
> memoria local, lo que reduce la latencia de acceso a los datos
> locales. Sin
>
> embargo, acceder a la memoria de otros procesadores requiere
>
> comunicación explícita, lo cual puede ser más lento.
>
> ● Paso de mensajes: La comunicación en sistemas de memoria distribuida
> se
>
> realiza mediante el paso de mensajes. Librerías como MPI (Message
> Passing
>
> Interface) son comunes y proporcionan las herramientas necesarias para
> la
>
> comunicación inter-procesador. Aunque el paso de mensajes introduce
>
> sobrecarga, es esencial para la coordinación y el intercambio de datos
> entre
>
> procesadores.
>
> ● Sincronización: La sincronización en sistemas de memoria distribuida
> es
>
> menos problemática en términos de coherencia de caché, pero sigue
> siendo
>
> crucial para coordinar la ejecución de tareas y el intercambio de
> datos. Los
>
> mensajes deben ser gestionados cuidadosamente para evitar bloqueos y
>
> garantizar la entrega correcta.
>
> ● Escalabilidad: Los sistemas de memoria distribuida generalmente
> escalan
>
> mejor que los de memoria compartida. A medida que se añaden más
>
> procesadores, cada uno con su propia memoria local, se reduce la
> contención
>
> por el acceso a la memoria, permitiendo que el sistema maneje un mayor
>
> número de procesadores de manera más eﬁciente.
>
> ● Programación: La programación en sistemas de memoria distribuida
> puede
>
> ser más compleja debido a la necesidad de gestionar explícitamente la
>
> comunicación y la sincronización. MPI es una herramienta comúnmente
>
> utilizada para este propósito, pero requiere una comprensión profunda
> de los
>
> patrones de comunicación y la estructura de datos distribuida.

**Estrategias** **de** **memoria** **distribuida**

En sistemas de memoria distribuida, donde cada procesador tiene su
propia

memoria local y los datos se reparten entre diferentes nodos, es crucial
implementar

estrategias eﬁcientes para manejar y acceder a los datos. Aquí se
explican tres

estrategias clave para mejorar el rendimiento en sistemas de memoria
distribuida:

localización de datos, reducción de contención y minimización de la
latencia de

caché.

> 1\. Localización de datos: La localización de datos se reﬁere a la
> estrategia de
>
> almacenar los datos lo más cerca posible de los procesadores que los
> utilizan
>
> con mayor frecuencia. Esto minimiza la necesidad de comunicación entre
>
> nodos y reduce la latencia de acceso a los datos.

Ejemplo: En un sistema de recomendación, los datos de un usuario pueden

almacenarse en el nodo donde se realizan los cálculos de recomendación
para ese

usuario. De esta forma, las consultas y actualizaciones de datos son
rápidas y

eﬁcientes.

Técnicas:

> ● Particionamiento de datos: Dividir los datos en particiones basadas
> en ciertos
>
> criterios (e.g., geográﬁcos, demográﬁcos) y asignar cada partición a
> un nodo
>
> especíﬁco.
>
> ● Replicación de datos: Mantener copias de los datos en múltiples
> nodos para
>
> asegurar que los datos estén disponibles localmente en varios nodos,
>
> reduciendo la latencia de acceso.
>
> ● Consistencia local: Asegurar que las operaciones de
> lectura/escritura en los
>
> datos locales se manejen de manera eﬁciente, y que las actualizaciones
> se
>
> propaguen a otros nodos según sea necesario.

Ventajas:

> ● Menor latencia: Acceso más rápido a los datos debido a su
> proximidad.
>
> ● Reducción de tráﬁco: Menos comunicación entre nodos, reduciendo el
> tráﬁco
>
> de red.

Desafíos:

> ● Equilibrio de carga: Asegurar que los datos y la carga de trabajo
> estén
>
> equilibrados entre los nodos.
>
> ● Consistencia de datos: Mantener la consistencia de los datos
> replicados entre
>
> diferentes nodos.
>
> 2\. Reducción de contención: La contención ocurre cuando múltiples
> nodos
>
> intentan acceder a los mismos recursos simultáneamente, lo que puede
>
> causar conﬂictos y retrasos. La reducción de contención se centra en
>
> minimizar estos conﬂictos para mejorar el rendimiento del sistema.

Ejemplo: En una base de datos distribuida, múltiples nodos pueden
intentar acceder

y actualizar el mismo registro simultáneamente. La contención se puede
reducir

mediante técnicas de particionamiento y replicación.

Técnicas:

> ● Particionamiento horizontal: Dividir una base de datos en tablas más
>
> pequeñas (shards) y asignar cada shard a un nodo diferente, reduciendo
> la
>
> contención en tablas grandes.
>
> ● Bloqueo de granularidad ﬁna: Utilizar bloqueos más especíﬁcos en
> lugar de
>
> bloquear grandes regiones de datos. Por ejemplo, en lugar de bloquear
> toda
>
> una tabla, bloquear solo las ﬁlas o columnas especíﬁcas que están
> siendo
>
> accedidas.
>
> ● Control optimista de concurrencia: Permitir que múltiples
> transacciones se
>
> procesen simultáneamente sin bloquearse entre sí y resolver los
> conﬂictos
>
> solo si ocurren (e.g., utilizando técnicas de versionado).

Ventajas:

> ● Mejor utilización del sistema: Menos tiempo de espera para los
> nodos,
>
> aumentando la eﬁciencia del sistema.
>
> ● Mayor concurrencia: Permite que más transacciones se procesen
>
> simultáneamente.

Desafíos:

> ● Complejidad de implementación: Estrategias como el control optimista
> de
>
> concurrencia pueden ser complejas de implementar y gestionar.
>
> ● Conﬂictos de datos: Aumenta la posibilidad de conﬂictos que deben
>
> resolverse eﬁcientemente.
>
> 3\. Minimización de la latencia de caché La latencia de caché se
> reﬁere al tiempo
>
> que tarda un procesador en acceder a los datos almacenados en caché.
>
> Minimizar esta latencia es crucial para mejorar el rendimiento del
> sistema.

Ejemplo:

En un sistema de procesamiento de datos en tiempo real, como una
plataforma de

análisis de eventos, es fundamental acceder rápidamente a los datos más
recientes.

Minimizar la latencia de caché asegura que los análisis se realicen lo
más rápido

posible.

Técnicas:

> ● Prefetching de datos: Anticipar qué datos serán necesarios
> próximamente y
>
> cargarlos en caché antes de que se soliciten, reduciendo el tiempo de
> espera.
>
> ● Cache Locality: Organizar los datos en memoria de manera que las
>
> operaciones accedan secuencialmente a áreas contiguas de memoria,
>
> aprovechando mejor la jerarquía de la memoria caché.
>
> ● Políticas de reemplazo de caché: Implementar políticas de reemplazo
>
> eﬁcientes (e.g., LRU - Least Recently Used) para mantener en caché los
> datos
>
> que se acceden con mayor frecuencia.
>
> ● Caché distribuida: Implementar una caché distribuida que se extiende
> a través
>
> de múltiples nodos, permitiendo que los datos caché se almacenen en
> varios
>
> lugares para un acceso rápido desde cualquier nodo.

Ventajas:

> ● Mayor velocidad de acceso: Reducción del tiempo necesario para
> acceder a
>
> datos frecuentemente utilizados.
>
> ● Mejor rendimiento global: Optimización del uso de la memoria caché y
>
> reducción de la latencia.

Desafíos:

> ● Administración de caché: Determinar qué datos almacenar y cuándo
>
> reemplazar datos en la caché puede ser complicado.
>
> ● Consistencia de caché: Mantener la coherencia de los datos
> almacenados en
>
> caché en un entorno distribuido puede ser difícil y costoso en
> términos de
>
> recursos.

Ejemplos

> ● En un sistema de memoria distribuida, podríamos tener un clúster de
>
> computadoras donde cada nodo del clúster tiene su propia memoria
> local.
>
> Para resolver un problema conjunto, como un análisis de grandes datos,
> los
>
> nodos deben intercambiar información mediante mensajes. Si un nodo
> realiza
>
> un cálculo que otros nodos necesitan, debe enviar los resultados a los
> nodos
>
> pertinentes.
>
> ● Un ejemplo práctico de memoria distribuida es un sistema de
> recomendación
>
> en un clúster de Hadoop. Cada nodo del clúster procesa una parte de
> los
>
> datos de usuario y elementos para generar recomendaciones. Los nodos
>
> deben intercambiar datos sobre usuarios y elementos similares para
> mejorar
>
> la precisión de las recomendaciones. Utilizando MPI, los
> desarrolladores
>
> pueden implementar un algoritmo que coordina la comunicación entre
> nodos
>
> para compartir información relevante.

Comparación de modelos

Latencia y rendimiento:

> ● Memoria compartida: Baja latencia de acceso a memoria compartida,
> pero
>
> alta latencia y complejidad en la coherencia de caché.
>
> ● Memoria distribuida: Baja latencia en acceso a memoria local, pero
> alta
>
> latencia en comunicación inter-procesador.
>
> Escalabilidad:
>
> ● Memoria compartida: Escalabilidad limitada debido a la contención de
>
> memoria y la complejidad de mantener la coherencia.
>
> ● Memoria distribuida: Mejor escalabilidad, adecuada para grandes
> clústeres,
>
> pero requiere manejo explícito de comunicación y sincronización.
>
> Complejidad de programación:
>
> ● Memoria compartida: Más sencilla debido a la uniformidad de acceso a
>
> memoria, pero requiere mecanismos de sincronización.
>
> ● Memoria distribuida: Más compleja debido a la necesidad de gestionar
> el
>
> paso de mensajes y la sincronización.
>
> **Aplicaciones** **adecuadas**:
>
> ● Memoria compartida: Aplicaciones que requieren acceso rápido a datos
>
> compartidos y donde la coherencia puede ser gestionada eﬁcientemente.
>
> ● Memoria distribuida: Aplicaciones que pueden ser descompuestas en
> tareas
>
> independientes que requieren poca comunicación, o donde la
> comunicación
>
> puede ser optimizada mediante el paso de mensajes.

keyboard_arrow_down

> Ejercicios
>
> 1 . Coherencia de caché: Explica cómo se mantiene la coherencia de
> caché en un
>
> sistema de memoria compartida utilizando el protocolo MESI. Incluya
> ejemplos de
>
> transiciones de estados de caché cuando dos procesadores acceden y
> modiﬁcan la
>
> misma línea de caché.
>
> Respuesta Esperada:
>
> ● Debea describir los cuatro estados del protocolo MESI (Modiﬁcado,
> Exclusivo,
>
> Compartido, Inválido) y explicar las transiciones de estados cuando:
>
> ○ Un procesador lee una línea de caché por primera vez.
>
> ○ Un segundo procesador lee la misma línea de caché.
>
> ○ El primer procesador modiﬁca la línea de caché.
>
> ○ El segundo procesador intenta leer la línea de caché modiﬁcada.

El protocolo MESI (Modiﬁcado, Exclusivo, Compartido, Inválido) es un
protocolo de

coherencia de caché que se utiliza para mantener la coherencia en
sistemas de

memoria compartida. Los cuatro estados de una línea de caché en este
protocolo

son:

Modiﬁcado (M): La línea de caché ha sido modiﬁcada y es la única copia
válida. Está

sucia (diferente de la memoria principal). Exclusivo (E): La línea de
caché es la única

copia válida y coincide con la memoria principal (está limpia).
Compartido (S): La

línea de caché puede estar en múltiples cachés y coincide con la memoria
principal

(está limpia). Inválido (I): La línea de caché no es válida.

Ejemplo de transiciones de estados:

Un procesador (P1) lee una línea de caché por primera vez:

> ● Estado inicial: Inválido (I)
>
> ● Estado ﬁnal: Exclusivo (E) si es la única copia, o Compartido (S) si
> otros
>
> cachés ya tienen la línea.

Un segundo procesador (P2) lee la misma línea de caché:

> ● Estado inicial en P1: Exclusivo (E) o Compartido (S)
>
> ● Estado ﬁnal en P1 y P2: Compartido (S) en ambos, ya que ambos tienen
> una
>
> copia limpia de la línea.

El primer procesador (P1) modiﬁca la línea de caché:

> ● Estado inicial en P1: Compartido (S)
>
> ● Transición: P1 envía un mensaje de invalidación a otros cachés.
>
> ● Estado ﬁnal en P1: Modiﬁcado (M)
>
> ● Estado ﬁnal en P2: Inválido (I)

El segundo procesador (P2) intenta leer la línea de caché modiﬁcada:

> ● Estado inicial en P2: Inválido (I)
>
> ● Transición: P2 solicita la línea de caché.
>
> ● P1 debe escribir la línea modiﬁcada en la memoria principal
> (write-back).
>
> ● Estado ﬁnal en P1: Compartido (S) después de la actualización.
>
> ● Estado ﬁnal en P2: Compartido (S) después de recibir la línea
> actualizada.
>
> Estos pasos ilustran cómo el protocolo MESI maneja la coherencia de
> caché
>
> en un sistema de memoria compartida, asegurando que todos los
>
> procesadores tengan una vista consistente de los datos en caché.

2 . Implementa un programa en C utilizando POSIX threads (pthread) que
demuestre

el uso de mutexes para proteger una variable compartida. El programa
debe crear

varios hilos que incrementen una variable global compartida de manera
segura.

\[2\]

> error
>
> 0 s
>
> \#include \<stdio.h\>
>
> \#include \<stdlib.h\>
>
> \#include \<pthread.h\>
>
> \#deﬁne NUM_THREADS 5
>
> \#deﬁne NUM_INCREMENTS 1000000

pthread_mutex_t mutex;

int shared_variable = 0;

void\* increment(void\* arg) {

> for (int i = 0; i \< NUM_INCREMENTS; i++) {
>
> pthread_mutex_lock(&mutex);
>
> shared_variable++;
>
> pthread_mutex_unlock(&mutex);
>
> }
>
> pthread_exit(NULL);

}

int main() {

> pthread_t threads\[NUM_THREADS\];
>
> pthread_mutex_init(&mutex, NULL);
>
> for (int i = 0; i \< NUM_THREADS; i++) {
>
> pthread_create(&threads\[i\], NULL, increment, NULL);
>
> }
>
> for (int i = 0; i \< NUM_THREADS; i++) {
>
> pthread_join(threads\[i\], NULL);
>
> }
>
> pthread_mutex_destroy(&mutex);
>
> printf("Final value of shared_variable: %d\n", shared_variable);
>
> return 0;

}

\[ \]

> \## Tu respuesta

3 . Describe los diferentes modelos de consistencia de memoria
(consistencia

estricta, consistencia secuencial, consistencia causal) y cómo afectan
el

comportamiento observable de los programas en un sistema de memoria

compartida.

Respuesta Esperada:

Debes explicar:

> ● Consistencia estricta: Todas las operaciones de memoria son vistas
> por
>
> todos los procesadores en el orden exacto en que ocurren.
>
> ● Consistencia secuencial: Las operaciones de memoria de todos los
>
> procesadores se intercalan en un orden secuencial que es consistente
> con el
>
> orden de programa de cada procesador.
>
> ● Consistencia causal: Solo las operaciones de memoria que son
> causalmente
>
> relacionadas deben ser vistas en el mismo orden por todos los
> procesadores.

Modelos de Consistencia de Memoria en Sistemas de Memoria Compartida

Los modelos de consistencia de memoria determinan cómo las operaciones
de

memoria (lecturas y escrituras) realizadas por diferentes procesadores
son vistas

por todos los procesadores en un sistema de memoria compartida. A
continuación,

se describen tres modelos importantes de consistencia de memoria:
consistencia

estricta, consistencia secuencial y consistencia causal. Consistencia
Estricta

Deﬁnición: Todas las operaciones de memoria son vistas por todos los

procesadores en el orden exacto en que ocurren.

Impacto:

> ● Cada lectura ve la última escritura.
>
> ● Ejemplo: Si P1 escribe un valor y luego P2 lee, P2 ve inmediatamente
> el valor
>
> de P1.
>
> ● Desventaja: Difícil de implementar en sistemas distribuidos por la
> necesidad
>
> de sincronización instantánea.

Consistencia Secuencial Deﬁnición: Las operaciones de memoria de todos
los

procesadores se intercalan en un orden global que respeta el orden del
programa de

cada procesador.

Impacto:

> ● Todos los procesadores acuerdan un único orden de las operaciones.
>
> ● Ejemplo: P1 escribe dos valores y P2 los lee en el mismo orden.
>
> ● Desventaja: Más relajado que la consistencia estricta, permite
> optimizaciones
>
> pero sigue siendo complejo en sistemas distribuidos.

Consistencia Causal Deﬁnición: Solo las operaciones de memoria
causalmente

relacionadas deben ser vistas en el mismo orden por todos los
procesadores.

Operaciones independientes pueden ser vistas en diferentes órdenes.

Impacto:

> ● Preserva las relaciones causales.
>
> ● Ejemplo: Si P1 escribe un valor que P2 usa para otra escritura,
> todos deben
>
> ver ambas en el mismo orden.
>
> ● Desventaja: Más ﬂexible y eﬁciente, pero más complejo para razonar
> sobre el
>
> comportamiento del programa.

Resumen

> ● Consistencia Estricta: Lecturas siempre ven la última escritura, muy
> intuitivo
>
> pero difícil de implementar.
>
> ● Consistencia Secuencial: Operaciones se intercalan en un orden
> global
>
> respetando el orden del programa, permite optimizaciones.
>
> ● Consistencia Causal: Solo las operaciones relacionadas causalmente
> deben
>
> ser vistas en el mismo orden, mejora rendimiento y ﬂexibilidad.

4 . Explica cómo el paso de mensajes en un sistema de memoria
distribuida permite

la comunicación entre nodos. Describa las ventajas y desventajas del
paso de

mensajes comparado con la memoria compartida.

Respuesta Esperada:

Debes explicar:

> ● Cómo los nodos envían y reciben mensajes para compartir datos.
>
> ● Ventajas: No requiere coherencia de caché, escalabilidad mejorada,
> adecuado
>
> para sistemas distribuidos.
>
> ● Desventajas: Latencia en la comunicación, mayor complejidad en la
>
> programación, sobrecarga de comunicación.

Comunicación mediante Paso de Mensajes en un Sistema de Memoria
Distribuida

Cómo funciona el Paso de Mensajes

En un sistema de memoria distribuida, los nodos (computadoras
individuales) se

comunican entre sí enviando y recibiendo mensajes. Cada nodo tiene su
propia

memoria local y no comparte memoria directamente con otros nodos. Para

compartir datos, un nodo debe empaquetar la información en un mensaje y
enviarlo

a otro nodo, que lo recibe, desempaqueta y procesa.

Envío de Mensajes:

> ● Un nodo empaqueta datos en un formato de mensaje.
>
> ● Utiliza una red de comunicación (como Ethernet o Inﬁniband) para
> enviar el
>
> mensaje a otro nodo.

Recepción de Mensajes:

> ● El nodo destinatario recibe el mensaje a través de la red.
>
> ● Desempaqueta el mensaje para extraer los datos y luego los procesa.

Ventajas del Paso de Mensajes

No requiere coherencia de caché:

> ● En sistemas de memoria compartida, mantener la coherencia de la
> caché es
>
> complejo y costoso.
>
> ● En el paso de mensajes, cada nodo maneja su propia memoria local,
>
> eliminando la necesidad de coherencia de caché.

Escalabilidad mejorada:

> ● Los sistemas de paso de mensajes escalan mejor que los de memoria
>
> compartida porque la comunicación se maneja de manera explícita.
>
> ● Es posible agregar más nodos sin enfrentar los mismos problemas de
>
> coherencia y latencia que en la memoria compartida.

Adecuado para sistemas distribuidos:

> ● Ideal para entornos donde los nodos están geográﬁcamente dispersos o
>
> cuando se utiliza una infraestructura de red como Internet.
>
> ● Permite la creación de aplicaciones distribuidas que pueden
> ejecutarse en
>
> diferentes ubicaciones físicas.

Desventajas del Paso de Mensajes

Latencia en la comunicación:

> ● El envío y recepción de mensajes a través de una red introduce
> latencia.
>
> ● La velocidad de acceso a datos remotos es más lenta comparada con el
>
> acceso a memoria compartida local.

Mayor complejidad en la programación:

> ● Los desarrolladores deben gestionar explícitamente el envío y la
> recepción de
>
> mensajes. La- programación y depuración de aplicaciones distribuidas
> puede
>
> ser más compleja debido a la necesidad de sincronización y manejo de
>
> errores en la comunicación.

Sobrecarga de comunicación:

> ● El protocolo de comunicación y el empaquetamiento/desempaquetamiento
>
> de mensajes introducen sobrecarga.
>
> ● tráﬁco de red puede convertirse en un cuello de botella si no se
> gestiona
>
> adecuadamente.

Por tanto, el paso de mensajes permite la comunicación efectiva en
sistemas

distribuidos, mejorando la escalabilidad y eliminando la necesidad de
coherencia de

caché, pero a costa de mayor latencia, complejidad y sobrecarga en la

comunicación.

5 . Compare los modelos de consistencia eventual y consistencia fuerte
en sistemas

de memoria distribuida. Proporcione ejemplos de aplicaciones donde cada
modelo

sería más adecuado.

Respuesta Esperada:

Debes describir:

> ● Consistencia fuerte: Las actualizaciones son visibles
> instantáneamente a
>
> todos los nodos, proporcionando una vista consistente de los datos en
> todo
>
> momento.
>
> ● Consistencia eventual: Las actualizaciones se propagan gradualmente
> y
>
> todos los nodos eventualmente alcanzan una consistencia, pero puede
> haber
>
> inconsistencias temporales.
>
> ● Ejemplos: Consistencia fuerte es crucial para aplicaciones
> ﬁnancieras,
>
> mientras que la consistencia eventual es adecuada para redes sociales
> y
>
> sistemas de caching distribuido.

Consistencia Fuerte vs. Consistencia Eventual en Sistemas de Memoria
Distribuida

Consistencia Fuerte

Descripción:

> ● Las actualizaciones son visibles instantáneamente a todos los nodos.
>
> ● Proporciona una vista consistente de los datos en todo momento.
> Ejemplo de
>
> Aplicaciones:
>
> ● Aplicaciones Financieras: Transacciones bancarias y sistemas de pago
>
> requieren consistencia inmediata para evitar discrepancias y asegurar
> la
>
> integridad de los datos.

Consistencia Eventual Descripción:

> ● Las actualizaciones se propagan gradualmente.
>
> ● Todos los nodos eventualmente alcanzan una consistencia, pero puede
> haber
>
> inconsistencias temporales.

Ejemplo de Aplicaciones:

> ● Redes Sociales: Los posts y los likes pueden tardar en propagarse a
> todos los
>
> usuarios, y pequeñas inconsistencias temporales son aceptables.
>
> ● Sistemas de Caching Distribuido: Los datos almacenados en cachés
> pueden
>
> ser leídos rápidamente, aunque puedan estar ligeramente
> desactualizados
>
> por un corto periodo de tiempo. Resumen Consistencia Fuerte: Crucial
> para
>
> aplicaciones donde la precisión y la sincronización inmediata son
> esenciales,
>
> como en el sector ﬁnanciero. Consistencia Eventual: Adecuada para
>
> aplicaciones donde pequeñas inconsistencias temporales son tolerables,
>
> como en redes sociales y sistemas de caching distribuido.

6 . Implementa un programa en Python que utilice el módulo
multiprocessing para

demostrar la memoria compartida. Crea varios procesos que incrementen
una

variable compartida de manera segura utilizando un Value y un Lock.

\[12\]

> 0 s
>
> import multiprocessing
>
> def increment(shared_value, lock):
>
> for \_ in range(10000):
>
> with lock:
>
> shared_value.value += 1
>
> def main():
>
> \# Crear una variable compartida
>
> shared_value = multiprocessing.Value('i', 0)
>
> \# Crear un lock para la sincronización
>
> lock = multiprocessing.Lock()
>
> processes = \[\]
>
> \# Crear y arrancar 4 procesos
>
> for \_ in range(4):
>
> p = multiprocessing.Process(target=increment, args=(shared_value,
> lock))
>
> processes.append(p)
>
> p.start()
>
> \# Esperar a que todos los procesos terminen
>
> for p in processes:
>
> p.join()
>
> \# Imprimir el valor ﬁnal de la variable compartida
>
> print(f"Final value: {shared_value.value}")
>
> if \_\_name\_\_ == "\_\_main\_\_":
>
> main()

Final value: 40000

7 . Explica la diferencia entre coherencia de caché y consistencia de
caché.

Proporciona ejemplos de cómo estos conceptos afectan el rendimiento de
un

sistema multiprocesador.

Respuesta esperada:

Debes explicar:

> ● Coherencia de Caché: Garantiza que todas las copias de un dato en
> diferentes
>
> cachés sean iguales.
>
> ● Consistencia de Caché: Garantiza el orden en que las operaciones de
>
> memoria son vistas por diferentes procesadores.
>
> ● Ejemplos: Condiciones de carrera debido a la falta de coherencia,
> problemas
>
> de sincronización debido a la falta de consistencia.

Diferencia entre Coherencia de Caché y Consistencia de Caché

Coherencia de Caché:

> ● Garantiza que todas las copias de un dato en diferentes cachés sean
> iguales.
>
> ● Se asegura de que cualquier cambio realizado en un dato en una caché
> se
>
> reﬂeje en todas las otras copias del mismo dato en otras cachés.
>
> ● Ejemplo: Si un procesador modiﬁca un valor en su caché, la copia en
> la caché
>
> de otro procesador se invalida o se actualiza para reﬂejar el cambio.

Consistencia de Caché:

> ● Garantiza el orden en que las operaciones de memoria son vistas por
>
> diferentes procesadores.
>
> ● Se asegura de que las operaciones de lectura y escritura realizadas
> por
>
> diferentes procesadores se vean en el mismo orden en todas las cachés.
>
> ● Ejemplo: Si el procesador A escribe en la memoria y luego realiza
> una
>
> operación de lectura, la operación de lectura no debe devolver un
> valor
>
> anterior al valor escrito por el procesador A.

Ejemplos de Impacto en el Rendimiento

Falta de Coherencia de Caché:

> ● Si dos cachés contienen copias diferentes de un mismo dato y ninguno
> de los
>
> procesadores invalida o actualiza las copias en las otras cachés,
> puede
>
> producirse una condición de carrera.
>
> ● Ejemplo: Dos procesadores leen una misma variable en caché, la
> modiﬁcan y
>
> luego la escriben de vuelta en la memoria principal sin
> sincronización, lo que
>
> resulta en una incoherencia de los datos.

Falta de Consistencia de Caché:

> ● Si los procesadores ven operaciones de memoria en un orden
> diferente,
>
> pueden surgir problemas de sincronización y lógica.
>
> ● Ejemplo: Si un procesador A escribe en la memoria y luego realiza
> una
>
> operación de lectura, pero otro procesador B ve la operación de
> lectura antes
>
> de la escritura, B podría obtener un valor incorrecto o
> desactualizado.

En resumen, la coherencia de caché se centra en la consistencia de los
datos entre

cachés, mientras que la consistencia de caché se reﬁere al orden en que
se ven las

operaciones de memoria. Ambos conceptos son fundamentales para el
rendimiento

y la integridad de los sistemas multiprocesador.

8 . Implementa un programa en Python que simule la coherencia de caché
utilizando

threading. Crea un sistema donde múltiples hilos modiﬁquen una variable

compartida y utilice bloqueos para garantizar la coherencia.

\[13\]

> 0 s
>
> import threading
>
> \# Variable compartida entre los threads.
>
> shared_value = 0
>
> \# Candado (lock) para asegurar la exclusión mutua.
>
> lock = threading.Lock()
>
> \# Función que modiﬁca la variable compartida.
>
> def modify_shared_value():
>
> global shared_value \# Indica que se está utilizando la variable
> global shared_value
>
> for \_ in range(10000): \# Repite 10000 veces
>
> with lock: \# Asegura la exclusión mutua al adquirir el lock
>
> temp = shared_value \# Copia el valor actual de shared_value en una
> variable temporal
>
> temp += 1 \# Incrementa la variable temporal
>
> shared_value = temp \# Actualiza shared_value con el valor
> incrementado
>
> \# Función principal que conﬁgura e inicia los threads.
>
> def main():
>
> threads = \[\] \# Lista para almacenar los objetos thread
>
> for \_ in range(4): \# Crea 4 threads
>
> t = threading.Thread(target=modify_shared_value) \# Inicializa el
> thread con la función modify_shared_value
>
> threads.append(t) \# Añade el thread a la lista de threads
>
> t.start() \# Inicia la ejecución del thread
>
> for t in threads: \# Espera a que todos los threads terminen
>
> t.join() \# Espera a que el thread t termine
>
> \# Imprime el valor ﬁnal de la variable compartida
>
> print(f"Final value: {shared_value}")
>
> \# Punto de entrada del programa.
>
> if \_\_name\_\_ == "\_\_main\_\_":
>
> main() \# Llama a la función principal para iniciar el programa

Final value: 40000

\[ \]

> \## Tu respuesta

9 .Describe cómo funciona un sistema de snoop bus para mantener la
coherencia de

caché en un sistema multiprocesador. ¿Cuáles son los desafíos asociados
con el

snoop bus?

Respuesta Esperada:

Debes explicar:

> ● Funcionamiento del snoop bus: Todas las cachés observan (snooping)
> el bus
>
> de datos para detectar operaciones relevantes y mantener la
> coherencia.
>
> ● Desafíos: Escalabilidad limitada debido al tráﬁco en el bus,
> latencia,
>
> complejidad de implementación.

Funcionamiento del Snoop Bus en un Sistema Multiprocesador Un sistema de
snoop

bus mantiene la coherencia de caché en un sistema multiprocesador
mediante un

mecanismo donde todas las cachés observan (o snoopean) el bus de datos
para

detectar operaciones relevantes y actualizar sus estados en
consecuencia. Aquí está

cómo funciona:

Observación del Bus:

> ● Cada caché monitorea todas las transacciones en el bus.
>
> ● Cuando una caché realiza una operación de lectura o escritura, emite
> una
>
> señal en el bus.

Detectar y Responder:

> ● Las demás cachés observan esta señal y veriﬁcan si tienen una copia
> de la
>
> línea de caché afectada.
>
> ● Si tienen una copia y es necesario, invalidan o actualizan su copia
> para
>
> mantener la coherencia.

Coherencia de Datos:

> ● Si una caché modiﬁca una línea de datos, otras cachés invalidan sus
> copias
>
> de esa línea.
>
> ● Esto asegura que siempre haya una única versión válida de los datos
> en todo
>
> el sistema.

Desafíos del Snoop Bus

Escalabilidad Limitada:

> ● El tráﬁco en el bus aumenta con el número de procesadores, lo que
> limita la
>
> escalabilidad del sistema.
>
> ● Con muchos procesadores, el bus puede saturarse, impidiendo que el
> sistema
>
> escale eﬁcientemente.

Latencia:

> ● El tiempo necesario para que todas las cachés observen y respondan a
> las
>
> operaciones en el bus introduce latencia.
>
> ● Esto puede afectar el rendimiento del sistema, especialmente en
> operaciones
>
> intensivas en memoria.

Complejidad de Implementación:

> ● Implementar un sistema de snoop bus es complejo debido a la
> necesidad de
>
> sincronizar todas las cachés.
>
> ● Asegurar que todas las cachés tengan una vista coherente de los
> datos
>
> requiere mecanismos soﬁsticados. En resumen, un snoop bus mantiene la
>
> coherencia de caché al permitir que todas las cachés monitoreen el bus
> de
>
> datos y respondan a las operaciones de memoria relevantes. Sin
> embargo,
>
> enfrenta desafíos signiﬁcativos en términos de escalabilidad, latencia
> y
>
> complejidad de implementación.

10 . Implementa un programa en Python que simule un sistema de snoop bus

utilizando hilos. Cada hilo representa un núcleo con su propia caché y
observa una

lista compartida de operaciones de memoria.

\[10\]

> 1 s
>
> import threading
>
> import time
>
> \# Se inicializa una memoria compartida simulada con 10 enteros todos
> inicializados a 0.
>
> shared_memory = \[0\] \* 10
>
> \# Lista para registrar las operaciones en el bus.
>
> bus_operations = \[\]
>
> \# Se crea un candado (lock) para asegurar la exclusión mutua en el
> bus.
>
> bus_lock = threading.Lock()
>
> \# Clase que representa la caché de un procesador.
>
> class Cache:
>
> def \_\_init\_\_(self, id):
>
> \# Identiﬁcador único para cada caché.
>
> self.id = id
>
> \# Se inicializa la caché local con 10 enteros todos inicializados a
> 0.
>
> self.cache = \[0\] \* 10
>
> def read(self, index):
>
> \# Asegura la exclusión mutua al registrar una operación de lectura en
> el bus.
>
> with bus_lock:
>
> bus_operations.append((self.id, 'read', index))
>
> \# Retorna el valor de la caché en el índice especiﬁcado.
>
> return self.cache\[index\]
>
> def write(self, index, value):
>
> \# Asegura la exclusión mutua al registrar una operación de escritura
> en el bus.
>
> with bus_lock:
>
> bus_operations.append((self.id, 'write', index, value))
>
> \# Escribe el valor en la caché en el índice especiﬁcado.
>
> self.cache\[index\] = value
>
> def snoop(self):
>
> while True:
>
> \# Asegura la exclusión mutua para acceder a las operaciones del bus.
>
> with bus_lock:
>
> if bus_operations:
>
> \# Extrae la primera operación de la lista.
>
> op = bus_operations.pop(0)
>
> if op\[1\] == 'write':
>
> \# Si es una operación de escritura, actualiza la caché con el nuevo
> valor.
>
> self.cache\[op\[2\]\] = op\[3\]
>
> \# Pausa breve para simular el tiempo de procesamiento.
>
> time.sleep(0.01)

\# Función que simula las tareas del CPU, escribiendo y leyendo de la
caché.

def cpu_task(cache, index, value):

> \# Escribe un valor en la caché.
>
> cache.write(index, value)
>
> print(f"CPU {cache.id} wrote {value} at index {index}")
>
> \# Pausa para simular el tiempo de procesamiento.
>
> time.sleep(1)
>
> \# Lee el valor de la caché.
>
> read_value = cache.read(index)
>
> print(f"CPU {cache.id} read {read_value} from index {index}")

def main():

> \# Crea cuatro instancias de caché, una para cada CPU.
>
> caches = \[Cache(i) for i in range(4)\]
>
> threads = \[\]
>
> \# Inicia un thread para cada caché que ejecuta la función snoop en
> segundo plano.
>
> for cache in caches:
>
> t = threading.Thread(target=cache.snoop)
>
> t.daemon = True
>
> t.start()
>
> \# Inicia threads para cada CPU que ejecuta la función cpu_task.
>
> for i, cache in enumerate(caches):
>
> t = threading.Thread(target=cpu_task, args=(cache, i % 10, i))
>
> threads.append(t)
>
> t.start()
>
> \# Espera a que todos los threads de CPU terminen.
>
> for t in threads:
>
> t.join()
>
> \# Punto de entrada del programa.
>
> if \_\_name\_\_ == "\_\_main\_\_":
>
> main()

CPU 0 wrote 0 at index 0CPU 1 wrote 1 at index 1

CPU 2 wrote 2 at index 2

CPU 3 wrote 3 at index 3

CPU 0 read 0 from index 0

CPU 1 read 1 from index 1

CPU 2 read 2 from index 2

CPU 3 read 3 from index 3

\[ \]

> \## Tu respuesta

11 . Describe el protocolo MESI para la coherencia de caché. Explica los
cuatro

estados posibles y cómo las transiciones de estado aseguran la
coherencia de los

datos.

Respuesta Esperada:

Debes explicar:

> ● Estados del Protocolo MESI: Modiﬁcado (M), Exclusivo (E), Compartido
> (S),
>
> Inválido (I).
>
> ● Transiciones: Cómo y cuándo ocurren las transiciones entre estos
> estados
>
> basadas en las operaciones de lectura y escritura de los procesadores.

\[ \]

> \## Tu respuesta

Protocolo MESI para la Coherencia de Caché El protocolo MESI es un
protocolo de

coherencia de caché utilizado en sistemas multiprocesador para asegurar
que las

copias de datos en las cachés de los diferentes procesadores se
mantengan

coherentes. El nombre "MESI" proviene de los cuatro estados posibles que
una línea

de caché puede tener:

Modiﬁcado (M):

> ● La línea de caché ha sido modiﬁcada y es diferente de la memoria
> principal.
>
> ● Solo esta caché tiene una copia válida.
>
> ● Si otro procesador necesita esta línea, se debe escribir de vuelta a
> la memoria
>
> principal (write-back).

Exclusivo (E):

> ● La línea de caché es la única copia válida y es igual a la memoria
> principal.
>
> ● No ha sido modiﬁcada por la caché actual.
>
> ● Si se modiﬁca, se transiciona a Modiﬁcado (M).

Compartido (S):

> ● La línea de caché es igual a la memoria principal y puede estar
> presente en
>
> múltiples cachés.
>
> ● No ha sido modiﬁcada y es coherente en todas las cachés que la
> contienen.

Inválido (I):

> ● La línea de caché no contiene datos válidos.
>
> ● Cualquier acceso a esta línea resultará en una lectura desde la
> memoria
>
> principal o una actualización desde otra caché.

Transiciones de Estado Las transiciones entre estos estados ocurren en
función de

las operaciones de lectura y escritura de los procesadores y la
interacción entre

ellos. Aquí se describen algunas transiciones clave:

Inválido (I) a Compartido (S):

> ● Ocurre cuando un procesador lee una línea que no tiene en su caché
> (miss de
>
> lectura) y otros procesadores tienen la línea en estado Compartido (S)
> o
>
> Exclusivo (E).

Inválido (I) a Exclusivo (E):

> ● Ocurre cuando un procesador lee una línea que no tiene en su caché y
> ningún
>
> otro procesador tiene la línea en su caché.

Compartido (S) a Modiﬁcado (M):

> ● Ocurre cuando un procesador escribe en una línea que está en estado
>
> Compartido (S).
>
> ● Se invalida la línea en las otras cachés.

Exclusivo (E) a Modiﬁcado (M):

> ● Ocurre cuando un procesador escribe en una línea que está en estado
>
> Exclusivo (E).

Modiﬁcado (M) a Inválido (I):

> ● Ocurre cuando otro procesador intenta leer o escribir en una línea
> que está en
>
> estado Modiﬁcado (M).
>
> ● La línea se escribe de vuelta a la memoria principal y luego se
> invalida.

Compartido (S) a Inválido (I):

> ● Ocurre cuando un procesador escribe en una línea que está en estado
>
> Compartido (S) en otras cachés.
>
> ● La línea se invalida en esas cachés.

Resumen El protocolo MESI asegura la coherencia de los datos a través de
estos

estados y transiciones, permitiendo que los datos sean compartidos de
manera

eﬁciente entre los procesadores mientras se mantiene la integridad y
coherencia de

la información en la memoria caché y principal.

12 . Implementa un programa en Python que simule el protocolo MESI. Crea
una

clase CacheLine con los cuatro estados y simule operaciones de lectura y
escritura

que provoquen transiciones de estado.

\[8\]

> 0 s
>
> class CacheLine:
>
> def \_\_init\_\_(self):
>
> self.state = 'I' \# Initial state is Invalid
>
> self.value = None
>
> def read(self):
>
> if self.state == 'I':
>
> self.state = 'S'
>
> print("Transition to Shared")
>
> return self.value
>
> def write(self, value):
>
> if self.state in ('I', 'S'):
>
> self.state = 'M'
>
> print("Transition to Modiﬁed")
>
> self.value = value
>
> def get_state(self):
>
> return self.state

def main():

> cache_line = CacheLine()
>
> \# Simulate write operation
>
> print("Writing value 42")
>
> cache_line.write(42)
>
> print(f"State after write: {cache_line.get_state()}")
>
> \# Simulate read operation
>
> print("Reading value")
>
> value = cache_line.read()
>
> print(f"State after read: {cache_line.get_state()}")
>
> if \_\_name\_\_ == "\_\_main\_\_":
>
> main()

Writing value 42

Transition to Modiﬁed

State after write: M

Reading value

State after read: M

13 . Implementa un programa en C usando OpenMP que utilice una barrera
para

sincronizar los hilos en diferentes fases de un cálculo. El programa
debe dividir un

cálculo en dos fases y asegurarse de que todos los hilos completen la
primera fase

antes de pasar a la segunda.

\[ \]

> \#include \<stdio.h\>
>
> \#include \<omp.h\>
>
> \#deﬁne NUM_THREADS 4
>
> \#deﬁne ARRAY_SIZE 16
>
> int main() {
>
> int array\[ARRAY_SIZE\];
>
> for (int i = 0; i \< ARRAY_SIZE; i++) {
>
> array\[i\] = i;
>
> }
>
> omp_set_num_threads(NUM_THREADS);
>
> \#pragma omp parallel
>
> {
>
> int id = omp_get_thread_num();
>
> int nthreads = omp_get_num_threads();
>
> // Fase 1: Sumar 10 a cada elemento del array
>
> for (int i = id; i \< ARRAY_SIZE; i += nthreads) {
>
> array\[i\] += 10;
>
> }
>
> // Sincronización de barrera
>
> \#pragma omp barrier
>
> // Fase 2: Multiplicar cada elemento por 2
>
> for (int i = id; i \< ARRAY_SIZE; i += nthreads) {
>
> array\[i\] \*= 2;
>
> }
>
> }
>
> printf("Array ﬁnal:\n");
>
> for (int i = 0; i \< ARRAY_SIZE; i++) {
>
> printf("%d ", array\[i\]);
>
> }
>
> printf("\n");
>
> return 0;
>
> }

\[ \]

> \## Tu respuesta

14 . Implementa un programa en C utilizando MPI (Message Passing
Interface) para

sumar los elementos de un array distribuido entre varios procesos. Cada
proceso

calcula la suma parcial de su porción y luego los resultados parciales
se combinan

en el proceso raíz.

\[7\]

> error
>
> 0 s
>
> \#include \<mpi.h\>
>
> \#include \<stdio.h\>
>
> \#include \<stdlib.h\>
>
> \#deﬁne ARRAY_SIZE 100
>
> \#deﬁne ROOT 0
>
> int main(int argc, char\*\* argv) {
>
> MPI_Init(&argc, &argv);
>
> int rank, size;
>
> MPI_Comm_rank(MPI_COMM_WORLD, &rank);
>
> MPI_Comm_size(MPI_COMM_WORLD, &size);
>
> int local_size = ARRAY_SIZE / size;
>
> int\* array = NULL;
>
> int\* local_array = (int\*)malloc(local_size \* sizeof(int));
>
> if (rank == ROOT) {
>
> array = (int\*)malloc(ARRAY_SIZE \* sizeof(int));
>
> for (int i = 0; i \< ARRAY_SIZE; i++) {
>
> array\[i\] = i + 1;
>
> }
>
> }

MPI_Scatter(array, local_size, MPI_INT, local_array, local_size,
MPI_INT, ROOT, MPI_COMM_WORLD);

> int local_sum = 0;
>
> for (int i = 0; i \< local_size; i++) {
>
> local_sum += local_array\[i\];
>
> }
>
> int global_sum;
>
> MPI_Reduce(&local_sum, &global_sum, 1, MPI_INT, MPI_SUM, ROOT,
> MPI_COMM_WORLD);
>
> if (rank == ROOT) {
>
> printf("Total sum: %d\n", global_sum);
>
> free(array);
>
> }
>
> free(local_array);
>
> MPI_Finalize();
>
> return 0;
>
> }

\[ \]

> \# Tu respuesta

15 . Implementa un programa en C utilizando POSIX threads (pthread) que

implemente el algoritmo de productor-consumidor con un búfer compartido.
Usa

mutexes y condiciones para sincronizar los accesos al búfer.

\[6\]

> error
>
> 0 s
>
> \#include \<stdio.h\>
>
> \#include \<stdlib.h\>
>
> \#include \<pthread.h\>
>
> \#include \<unistd.h\>
>
> \#deﬁne BUFFER_SIZE 10
>
> int buffer\[BUFFER_SIZE\];

int count = 0;

pthread_mutex_t mutex;

pthread_cond_t cond_producer, cond_consumer;

void\* producer(void\* arg) {

> for (int i = 0; i \< 20; i++) {
>
> pthread_mutex_lock(&mutex);
>
> while (count == BUFFER_SIZE) {
>
> pthread_cond_wait(&cond_producer, &mutex);
>
> }
>
> buffer\[count++\] = i;
>
> printf("Produced: %d\n", i);
>
> pthread_cond_signal(&cond_consumer);
>
> pthread_mutex_unlock(&mutex);
>
> sleep(rand() % 2);
>
> }
>
> pthread_exit(NULL);

}

void\* consumer(void\* arg) {

> for (int i = 0; i \< 20; i++) {
>
> pthread_mutex_lock(&mutex);
>
> while (count == 0) {
>
> pthread_cond_wait(&cond_consumer, &mutex);
>
> }
>
> int item = buffer\[--count\];
>
> printf("Consumed: %d\n", item);
>
> pthread_cond_signal(&cond_producer);
>
> pthread_mutex_unlock(&mutex);
>
> sleep(rand() % 3);
>
> }
>
> pthread_exit(NULL);

}

int main() {

> pthread_t prod_thread, cons_thread;
>
> pthread_mutex_init(&mutex, NULL);
>
> pthread_cond_init(&cond_producer, NULL);
>
> pthread_cond_init(&cond_consumer, NULL);
>
> pthread_create(&prod_thread, NULL, producer, NULL);
>
> pthread_create(&cons_thread, NULL, consumer, NULL);
>
> pthread_join(prod_thread, NULL);
>
> pthread_join(cons_thread, NULL);
>
> pthread_mutex_destroy(&mutex);
>
> pthread_cond_destroy(&cond_producer);
>
> pthread_cond_destroy(&cond_consumer);
>
> return 0;
>
> }

\[ \]

> \## Tu respuesta
>
> 16.Discute cómo los algoritmos pueden ser optimizados para sistemas de
>
> memoria compartida. Incluye estrategias como la localización de datos,
> la
>
> reducción de contención y la minimización de la latencia de caché.

Respuesta Esperada:

Debea explicar:

> ● Localización de datos: Mantener los datos que son accedidos
>
> frecuentemente juntos en memoria para aprovechar la caché.
>
> ● Reducción de contención: Usar estructuras de datos concurrentes
>
> optimizadas y particionar tareas para minimizar el acceso simultáneo a
> la
>
> misma memoria.
>
> ● Minimización de la latencia de caché: Acceder a los datos en
> patrones que
>
> maximicen la eﬁciencia de la caché, evitando el "cache thrashing".

Optimización de Algoritmos para Sistemas de Memoria Compartida
Localización de

Datos

Descripción:

> ● Mantener juntos en memoria los datos que se acceden frecuentemente.
>
> ● Aprovecha la jerarquía de caché para mejorar el rendimiento.

Estrategia:

> ● Organizar estructuras de datos para que elementos relacionados estén
>
> contiguos en memoria. Ejemplo: Almacenar elementos de una matriz o
> lista
>
> uno al lado del otro.

Reducción de Contención Descripción:

> ● Minimizar el acceso simultáneo a la misma memoria por múltiples
> threads o
>
> procesos.
>
> ● Mejora la eﬁciencia y reduce los cuellos de botella.

Estrategia:

> ● Usar estructuras de datos concurrentes optimizadas, como
>
> ConcurrentHashMap.
>
> ● Particionar tareas para que diferentes threads trabajen en
> diferentes
>
> segmentos de datos.

Minimización de la Latencia de Caché Descripción:

> ● Acceder a los datos en patrones que maximicen la eﬁciencia de la
> caché.
>
> ● Evita el "cache thrashing" (cuando la caché se llena y vacía
> rápidamente).
>
> Estrategia:
>
> ● Acceder a los datos de manera secuencial en lugar de aleatoria.
>
> ● Reutilizar datos que ya están en la caché antes de traer nuevos
> datos.
>
> Resumen
>
> ● Localización de Datos: Mantener juntos los datos frecuentemente
> accedidos
>
> para mejorar el uso de la caché.
>
> ● Reducción de Contención: Utilizar estructuras de datos concurrentes
> y
>
> particionar tareas para reducir el acceso simultáneo.
>
> ● Minimización de la Latencia de Caché: Acceder a datos en patrones
> eﬁcientes
>
> para evitar el "cache thrashing" y maximizar el rendimiento.
