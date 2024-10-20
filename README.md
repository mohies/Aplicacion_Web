# Proyecto de Aplicación Web de Torneos de Videojuegos

## Descripción
Este proyecto es una aplicación web diseñada para gestionar torneos de videojuegos, donde los usuarios pueden registrarse, participar en torneos y seguir su progreso a través de clasificaciones y perfiles de jugador.
La aplicación será una plataforma donde los usuarios pueden organizar y participar en torneos de videojuegos. En este espacio, los jugadores tendrán la oportunidad de crear sus propios torneos en distintas categorías, como deportes, estrategia o acción, y así invitar a otros a unirse. Cada usuario tendrá su perfil personal, donde podrán ver sus estadísticas, historial de participación y logros obtenidos en los torneos. Además, se incluirá una tabla de clasificación que mostrará a los mejores jugadores de cada torneo, fomentando un ambiente competitivo y colaborativo. Todo esto busca ofrecer una experiencia completa y divertida para los amantes de los videojuegos, permitiendo que se conecten y compitan entre sí de manera fácil y accesible.


## Modelos

### 1. Usuario
- **nombre**: `CharField` (max_length=200) - Nombre del usuario.
- **correo**: `EmailField` (max_length=200) - Correo electrónico del usuario.
- **clave_de_acceso**: `CharField` (max_length=200) - Clave de acceso del usuario.
- **fecha_registro**: `DateTimeField` - Fecha y hora de registro del usuario.

### 2. PerfilDeJugador
- **usuario**: `OneToOneField` (Usuario) - Relación uno a uno con el modelo Usuario.
- **puntos**: `IntegerField` - Puntos acumulados por el jugador.
- **nivel**: `IntegerField` - Nivel del jugador.
- **ranking**: `IntegerField` - Ranking del jugador en la clasificación.

### 3. Equipo
- **nombre**: `CharField` (max_length=200) - Nombre del equipo.
- **logotipo**: `URLField` (max_length=200) - URL del logotipo del equipo.
- **fecha_ingreso**: `DateField` - Fecha de ingreso del equipo.
- **puntos_contribuidos**: `IntegerField` - Puntos que el equipo ha contribuido.

### 4. Participante
- **usuario**: `OneToOneField` (Usuario) - Relación uno a uno con el modelo Usuario.
- **puntos_obtenidos**: `IntegerField` - Puntos obtenidos por el participante.
- **posicion_final**: `IntegerField` - Posición final en el torneo.
- **fecha_inscripcion**: `DateField` - Fecha de inscripción al torneo.

### 5. Torneo
- **nombre**: `CharField` (max_length=200) - Nombre del torneo.
- **descripcion**: `TextField` - Descripción del torneo.
- **categoria**: `CharField` (max_length=100) - Categoría del torneo.
- **duracion**: `DurationField` - Duración del torneo.

### 6. Consola
- **nombre**: `CharField` (max_length=200) - Nombre de la consola.
- **marca**: `CharField` (max_length=100) - Marca de la consola.
- **tipo**: `CharField` (max_length=100) - Tipo de consola.
- **precio**: `DecimalField` (max_digits=10, decimal_places=2) - Precio de la consola.

### 7. Juego
- **torneo**: `ForeignKey` (Torneo) - Relación muchos a uno con el modelo Torneo.
- **nombre**: `CharField` (max_length=200) - Nombre del juego.
- **genero**: `CharField` (max_length=50) - Género del juego.
- **id_consola**: `ForeignKey` (Consola) - Relación muchos a uno con el modelo Consola.

### 8. Espectador
- **usuario**: `OneToOneField` (Usuario) - Relación uno a uno con el modelo Usuario.
- **nivel_interes**: `IntegerField` - Nivel de interés del espectador.
- **comentarios**: `TextField` - Comentarios del espectador.
- **frecuencia_visitas**: `IntegerField` - Frecuencia de visitas al sitio.

### 9. Clasificacion
- **usuario**: `OneToOneField` (Usuario) - Relación uno a uno con el modelo Usuario.
- **ranking**: `IntegerField` - Ranking del usuario.
- **puntos**: `IntegerField` - Puntos acumulados por el usuario.
- **torneos_ganados**: `IntegerField` - Cantidad de torneos ganados.

### 10. ParticipanteEquipo
- **participante**: `ForeignKey` (Participante) - Relación muchos a uno con el modelo Participante.
- **equipo**: `ForeignKey` (Equipo) - Relación muchos a uno con el modelo Equipo.
- **rol**: `CharField` (max_length=100) - Rol del participante en el equipo.
- **fecha_ingreso**: `DateField` - Fecha de ingreso al equipo.

## Modelo Entidad-Relación
[Modelo Entidad-Relación](img/Modelo_Entidad_Relacion.drawio.png)

