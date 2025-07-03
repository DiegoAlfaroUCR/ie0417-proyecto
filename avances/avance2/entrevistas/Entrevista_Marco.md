# Transcripción de entrevista realizada a [Ing. Marco Villalta Fallas, MSc.](https://eie.ucr.ac.cr/profesores/m.villalta/)
## Entrevistador: Edgar Alvarado Taleno
## Fecha: 18/5/2025
## Se denota M para el entrevistado y el entrevistador como E.

---

**E:** Bueno, como les he dicho, era la entrevista para crear un proyecto de diseño de software donde estamos replanteando y replanteando algunas cosas que tal vez se pudieran mejorar, o, bueno, ver también como la estructura, digamos, como ver un proyecto más a fondo, no como los proyectillos que uno ve en algunas cosas.  
Entonces, comenzando, la entrevista se dividiría como en varias partes, una de estas es como experiencia general y posibilidad sobre lo que es el entorno, digamos.  
Voy a comenzar explicando el contexto así medio en disco.  
O sea, la forma en que nos pusieron a ver esto es como... ¿Está bien?  
Es como a partir de su opinión como usuario y también como su opinión como técnico, digamos, persona que se encarga de desarrollo y mantenimiento.  
Entonces, la primera es como experiencia general y posibilidad: ¿ha participado de alguna forma en el desarrollo?

**M:** Sí.

**E:** Pero… ¿Y cuál era su rol, digamos, en sí?

**M:** Yo ahorita estoy más que todo en testing y... de bombero.  
Sí, de bombero. Si hay un bug así que hay que arreglar, como que ya algo está reventando en la página de producción, yo me la entro.  
Entonces, más que todo en la parte de testing y de, no sé, bug tracker, algo así.

**E:** Cierto, creo que usted fue el que estaba arreglando las partes de…  
Bueno, usted fue el que implementó bien la parte de Docker, ¿no?

**M:** Sí, yo hice la parte de Docker, pero realmente la hice para la parte de integración y *deployment*.

**E:** Ah, cierto… por eso, es como, ¿qué ves? Para correr las pruebas unitarias por la parte de *testing*.  
Todo eso está encadenado, ¿no?  
Aquí tengo una pregunta sobre eso…  
Digamos, esto ya es como más de usuario.  
¿Desde cuándo utiliza la plataforma de EIEinfo?

**M:** Desde que se creó, más o menos.  
La administro como la parte de la información.  
O sea, como para subir noticias, para subir anuncios.  
Entonces, en ese sentido, como usuario.  
Y la he usado prácticamente desde que existió.

**E:** Ok, ok.  
Y… ya después, ¿como administrativo ahí? ¿Y como profe también?

**M:** Sí, también. Por ejemplo, como profe para solicitar asistencias.

**E:** Ok.  
Digamos, ahora otra…  
¿Qué funcionalidades cree que son las más útiles de la página?

**M:** Bueno, son varias cosas.  
Por ejemplo, la parte de hacer asignaciones de profesores, asignar los cursos.  
Los horarios.  
Poder subir archivos para los diferentes tipos de usuarios: profesores, administrativos, y usuarios.

**E:** Bueno, otra es… ¿Qué tan intuitiva y accesible le parece la plataforma?

**M:** ¿Desde la perspectiva de desarrollador o de usuario?

**E:** Usuario, usuario.

**M:** Ok, porque como desarrollador… no, es terrible.  
Pero bueno, como usuario…  
Sí, me parece que es...  
Por UX, si le pusiera una nota, le pondría un 8, tal vez.

**E:** ¿Por qué?

**M:** Porque no es claro que uno se tiene que loguear como usuario para tener acceso a cierta información.  
Entonces, en ese sentido, no es muy claro.

**E:** Ok, sí, sí. Eso todavía no lo he visto porque no he tenido acceso a eso, pero sí.  
Ahora esto es como *feedback* de usuario.  
¿Usted se encargaba como administrativo, como profesor?

**M:** Sí, como Soyla.

**E:** ¿Se considera que la plataforma cumple sus necesidades como profesor, administrativo y todo eso?

**M:** Como profesor y como administrativo, sí.  
Pero, vamos a ver, como administrativo para ver la información, sí.  
Para administrar la plataforma, no tanto.

**E:** Ok.  
Digamos, en cuanto a posibles mejoras o potencial crecimiento, ¿qué podría decir?

**M:** Hay cosas que no están muy maduras.  
Y a veces es un poco oscuro poder administrarla.  
Si uno quiere quitar algo o poner algo, no es muy claro.  
Me ha pasado que quiero quitar algo… y reviento.

**E:** Pero desde el usuario, ¿verdad?

**M:** Sí, como usuario administrador.

**E:** Ah ok.

**M:** Es que está el perfil de administrativo, el de docente y el de administrador.

**E:** Ah, cierto.

**M:** Como perfil de docente, que es un usuario silvestre, está bien.  
Pero como administrativo, ahí se hace cada vez más complicado.  
Veo los logs y cada rato hay cosas reventando.  
Por todos lados.

**E:** ¿En qué partes están reventando?

**M:** Ah, es interesante. Son muchas.  
Tengo que ir poco a poco viendo dónde.  
Porque en los logs aparece que algo falló, pero la página no se cae.  
Entonces, son cosas que tengo que ir rastreando.
Entonces, son cosas que tengo que ir rastreando.

**E:** Ok, ok.  
Dice, sí, es que las instancias, información del curso…  
Digamos, como profesor, tipo las instancias creo que están bien hechas, entonces como para las instancias, declarar instancias.

**M:** Ok, información de los cursos, me imagino que sí.

**E:** Bueno, encargado de laboratorio, creo que es, director de departamento, tampoco, creo que no.  
Ahora, con mantenimiento y confianza, con confiabilidad…  
¿Ha experimentado fallas, errores, limitaciones del uso de la plataforma? ¿Con qué frecuencia?

**M:** A ver… si tuviera que poner una frecuencia de 0 a 5, le pondría que topo con errores con una frecuencia de 1 o 2.  
En una escala de 5.

**E:** ¿Y eso está relacionado con qué?

**M:** Cuando quiero quitar o agregar información.  
Sí, es que, dependiendo de lo que quieras hacer.  
Por ejemplo, si quiero borrar un administrativo que ya no está acá, como fue creado a puro principio, a veces pasa que no lo puedo borrar en la plataforma.

**E:** Ok.

**M:** Y eso es porque fue creado al principio y hubo dependencias nuevas que no se actualizaron.  
Algo pasó ahí, entonces tengo que meterme en la base de datos y hacerlo oscuramente desde la base de datos.

**E:** Ok.

**M:** Eso no me gusta…

**E:** Entonces eso ya es como el código que está ahí vivo y lento.

**M:** Exactamente.  
Y es que el diseño de la base de datos está un poco extraño.  
Se fue construyendo poco a poco, entonces no hubo un diseño desde el inicio.  
No fue escalable.

**E:** Ok, es como que no se diseñó escalablemente.

**M:** No tuvo lo mejor.  
No fue como que alguien se sentara a decir: la base de datos va a ser así, con estas tablas, estas llaves, estas relaciones…  
Fue como: “hagamos esta tabla, ocupamos esto, pégamelo aquí”, y después relacionar otra cosa, y así.  
Entonces no necesariamente está lo mejor posible diseñada.  
Pero eso ya es algo que difícilmente se vaya a arreglar.

**E:** En sí fue como que se diseñó pero no escalable, digamos.

**M:** Es que aquí nosotros no vemos bases de datos.  
Lo lógico es que uno se siente, piense en necesidades actuales, futuras, cómo conectar bien las tablas… pero eso no pasó.

**E:** Ok, sí.  
¿Alguna otra cosa?

**M:** Bueno, por ahí hacen falta pruebas unitarias.

**E:** Sí.

**M:** Hay muy pocas.  
De hecho, se hicieron en el 2023.  
Las únicas que hay están en el 2023 y hasta hace poco las estoy integrando a la parte de CI/CD.  
Y faltan muchas.  
A mí me dice Teo: “Marco, yo sé que usted siempre me pide pruebas unitarias, pero necesitamos esto ya funcionando”.  
Y yo pues bueno… entonces tengo que hacer una prueba muy funcional, por encima, y mandarlo a producción así.  
Hacen falta muchas pruebas unitarias.

**E:** Sí, es que yo cuando estuve revisando el código, creo que las únicas que vi fueron las de Docker, que había varias.

**M:** Ah sí, esas son funcionales, muy por encima.

**E:** Cierto, aquí me genera una duda…  
Ustedes utilizan integración continua, ¿verdad?  
Pero, ¿cómo la utilizan? ¿Con qué?

**M:** Yo tengo acá instalado en uno de los servidores un servicio de *Drone*.  
No utilizo el de GitLab directamente, porque el del centro de informática tiene muy pocos recursos asignados.  
Entonces, duraría demasiado cada vez que quiero hacer un *deployment* o una integración.  
Lo tengo acá, entonces hay una conexión entre el repositorio y este servicio que tengo acá de CI/CD.  
Y eso a mí me da más control de todo el proceso, porque puedo ver qué está pasando bien por debajo.

**E:** ¿Corren las pruebas funcionales?

**M:** Sí, hay que correr las pruebas funcionales.  
La parte de CI/CD no está como integrada con el GitLab de la UCR, sino con Drone.

**E:** Sí, sí, sí.  
Es que cuando estuve revisando, estoy más acostumbrado a GitHub Actions.  
Entonces fue como… ¿de aquí qué? ¿Dónde están?

**M:** Y eso que no estoy usando Jenkins, que es el estándar en la industria.  
No me gusta mucho Jenkins, ya me parece que es un monstruo, un pulpo que no me gusta.

**E:** Bueno, ¿ha encontrado problemas con el rendimiento de la página?

**M:** Qué pregunta más interesante.  
Realmente no he medido muy bien el *performance*.  
Le he asignado recursos para que funcione bien, pero no tengo métricas de desempeño.

**E:** O sea, pero por lo menos, viendo las cifras por encima…

**M:** Bien, sí.



**E:** Ok.  
¿Problemas de seguridad?

**M:** ¿Problemas de seguridad?  
Vieras que Django es bastante, bastante bueno como para cachar esos detalles.  
No he tenido tiempo como para hacerle un… para atacarla.  
Me encantaría, pero apenas puedo, la reviso.

**E:** Ok.

**M:** No he tenido chance, no he encontrado problemas serios de seguridad, para serte sincero.

**E:** Ok, ok.  
Entonces, ¿algunas áreas de crecimiento?  
¿Qué funcionalidades le gustaría ver implementadas en la plataforma?

**M:** Es como más general, creo…  
Veamos, a ver…  
Bueno, de hecho, ahorita yo tengo un estudiante que está desarrollando una página para bodega.  
Hay un módulo de inventario, pero está más orientado al inventario de los bienes, ¿no?  
No tanto al proceso metodológico de la bodega.  
Entonces, está terminando un estudiante mío eso.  
Es una página aparte en Django, pero eventualmente lo mejor sería integrarlo.  
Entonces, eso es algo que hace falta.

**M:** Cosas que hacen falta más:  
Habilitar bien el módulo de reservas que nos dan.  
Hay una parte que no está en la página, ni siquiera le aparece a nadie, pero sí está programada.  
Es para poder reservar espacios.  
Aulas.

**E:** Ah, ok, cierto, eso sería…

**M:** Sería bueno echarle el ojo, revisarlo bien, integrarlo.

**E:** Digamos, como profesor, ¿hay algo que crea que le podría facilitar?

**M:** Como profe… o administrativo… no, realmente.

**E:** ¿Ve oportunidades para integrar otras herramientas o sistemas institucionales?

Por ejemplo, Teo… ¿cuál fue el que dijo?  
Arreglar la conexión entre las pantallas.  
**M:** Sí, cierto, las pantallas.  
Eso sería bueno.  
No sé en qué quedó. A mí me lo preguntaron hace como dos meses.  
Y yo, híjole… no sé dónde está.

**E:** Ok.  
O sea, ¿hay algo por ahí, pero no se acuerda cómo funcionaba?

**M:** De hecho, no lo logré volver a poner a funcionar.

**E:** ¿O alguna otra herramienta?

**M:** ¿Alguna otra herramienta?  
Veamos a ver…  
Ya sea tipo de mantenimiento o algo más aparte.  
Se podría, por ejemplo, hacer algo interesante, tal vez conectar un bot de anuncios y de eventos o servicios al canal de la escuela.  
Cuando se crea algo, que mande ahí.  
Sería místico.

**E:** Bueno, aquí están otros aspectos muy místicos.  
Ya me pasé un toquecillo de tiempo, sorry.  
Digamos, ¿desafíos técnicos que encuentra en la implementación?  
O sea, como desarrollador que está presente, ¿qué desafíos está encontrando ahorita?

**M:** ¿Como desarrollador?  
No está bien documentado.  
No hay documentación.  
Eso es...  
O sea, está el código ahí, pero no está comentado.  
No está documentado.  
Yo no puedo correrlo con Sphinx, no puedo con Doxygen generar algo como para… eso.  
Entonces, ¿dónde puedo ver esta cosa que me está fallando?  
Falta documentación como desarrollador.  
Eso es fundamental.  
No hay documentación.  
Al principio el esfuerzo fue noble, pero ya después se perdió.  
Se perdió completamente.  
Y de hecho, cuando lo vi, no tenía un estilo fijo.  
Como que en alguno hacía como un tipo y en el otro…

**E:** Bueno, yo creo que sería solo eso.  
Muchas gracias.

**M:** Con gusto.
