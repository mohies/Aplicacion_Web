# Aplicacion_Web

from django.db import models
from django.utils import timezone

class Usuario(models.Model):
    nombre = models.CharField(max_length=200)
    correo = models.EmailField(max_length=200)
    clave_de_acceso = models.CharField(max_length=200)
    fecha_registro = models.DateTimeField(blank=True, null=True)
    
    def __str__(self):
        return self.nombre

class PerfilDeJugador(models.Model):
    usuario = models.OneToOneField(Usuario, on_delete=models.CASCADE)
    puntos = models.IntegerField(default=0, blank=False)
    nivel = models.IntegerField(default=0, blank=False)
    ranking = models.IntegerField(default=0, blank=False)
    avatar = models.URLField(max_length=200)

class Torneo(models.Model):
    nombre = models.CharField(max_length=200)
    descripcion = models.TextField()
    categoria = models.CharField(max_length=100)
    duracion = models.DurationField()
    fecha_inicio = models.DateField(default=timezone.now)
    
    def __str__(self):
        return self.nombre

class Consola(models.Model):
    nombre = models.CharField(max_length=200)
    marca = models.CharField(max_length=100)
    tipo = models.CharField(max_length=100)
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    
    def __str__(self):
        return self.nombre

class Juego(models.Model):
    torneo = models.ForeignKey(Torneo, on_delete=models.CASCADE)
    nombre = models.CharField(max_length=200)
    genero = models.CharField(max_length=50)
    consola = models.ForeignKey(Consola, on_delete=models.CASCADE)
    descripcion = models.TextField()
    
    def __str__(self):
        return self.nombre

class Participante(models.Model):
    puntos_obtenidos = models.IntegerField(default=0, blank=False)
    posicion_final = models.IntegerField(default=0, blank=False)
    fecha_inscripcion = models.DateField(default=timezone.now)
    tiempo_jugado = models.FloatField()

class Espectador(models.Model):
    usuario = models.OneToOneField(Usuario, on_delete=models.CASCADE)  # Cambiado a OneToOneField
    nivel_interes = models.IntegerField(default=0, blank=False)
    comentarios = models.TextField()
    frecuencia_visitas = models.IntegerField()
    suscripcion = models.BooleanField(default=False)
    
    def __str__(self):
        return self.usuario.nombre

class Equipo(models.Model):
    nombre = models.CharField(max_length=200)
    logotipo = models.URLField(max_length=200, blank=True, null=True)
    fecha_ingreso = models.DateField(default=timezone.now)
    puntos_contribuidos = models.IntegerField(default=0, blank=False)
    
    def __str__(self):
        return self.nombre

class Clasificacion(models.Model):
    usuario = models.ForeignKey(Usuario, on_delete=models.CASCADE)
    ranking = models.IntegerField(default=0, blank=False)
    puntos = models.IntegerField(default=0, blank=False)
    torneos_ganados = models.IntegerField(default=0, blank=False)

class ParticipanteEquipo(models.Model):
    participante = models.ForeignKey(Participante, on_delete=models.CASCADE)
    equipo = models.ForeignKey(Equipo, on_delete=models.CASCADE)
    rol = models.CharField(max_length=100)
    fecha_ingreso = models.DateField(default=timezone.now)
    puntos_contribuidos = models.IntegerField(default=0, blank=False)
    tiempo_jugado = models.FloatField(default=0.0)

class TorneoJuego(models.Model):
    torneo = models.ForeignKey(Torneo, on_delete=models.CASCADE)
    juego = models.ForeignKey(Juego, on_delete=models.CASCADE)
    puntos = models.IntegerField(default=0, blank=False)
    fecha_participacion = models.DateField(default=timezone.now)
    estado = models.CharField(max_length=50, choices=[
        ('activo', 'Activo'),
        ('completado', 'Completado'),
        ('pendiente', 'Pendiente'),
    ], default='activo')

    # Atributos adicionales para la relación intermedia
    comentarios = models.TextField(blank=True, null=True)
    tiempo_jugado = models.FloatField(default=0.0)

class TorneoParticipante(models.Model):
    torneo = models.ForeignKey(Torneo, on_delete=models.CASCADE)
    participante = models.ForeignKey(Participante, on_delete=models.CASCADE)
    fecha_inscripcion = models.DateField(default=timezone.now)
    puntos_obtenidos = models.IntegerField(default=0, blank=False)
    posicion_final = models.IntegerField(default=0, blank=False)
