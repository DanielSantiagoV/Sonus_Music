# 📚 Documentación Detallada de Colecciones MongoDB - Sistema de Música

## 🎯 Propósito del Documento

Este archivo proporciona una documentación completa y detallada de todas las colecciones de MongoDB utilizadas en el sistema de música, incluyendo comentarios específicos sobre cada campo, su propósito, tipo de dato y ejemplos de uso práctico.

---

## 🎤 Colección: `artistas`

### 📋 Descripción General
La colección `artistas` almacena información completa sobre artistas musicales, incluyendo datos personales, profesionales y de redes sociales. Esta colección es fundamental para el sistema ya que establece la base para todas las relaciones musicales.

### 🏗️ Estructura de Campos

#### **Campo: `_id`**
- **Tipo**: String (ObjectId personalizado)
- **Formato**: `artista_XXX` (donde XXX es un número secuencial)
- **Ejemplo**: `"artista_001"`
- **Propósito**: Identificador único del artista en el sistema
- **Comentario**: Se utiliza un formato personalizado en lugar de ObjectId estándar para facilitar la legibilidad y debugging durante el desarrollo

#### **Campo: `nombre`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 1-50 caracteres)
- **Ejemplo**: `"The Beatles"`, `"Maroon 5"`, `"Ed Sheeran"`
- **Propósito**: Nombre artístico o real del artista
- **Comentario**: Puede incluir números, caracteres especiales y artículos como "The". Es el campo principal para búsquedas y filtros

#### **Campo: `pais`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 5-30 caracteres)
- **Ejemplo**: `"Reino Unido"`, `"Estados Unidos"`, `"Colombia"`
- **Propósito**: País de origen o residencia principal del artista
- **Comentario**: Permite segmentación geográfica para recomendaciones locales y análisis de mercado por región

#### **Campo: `genero`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 5-25 caracteres)
- **Ejemplo**: `"Rock"`, `"Pop Rock"`, `"Pop Latino"`
- **Propósito**: Género musical principal del artista
- **Comentario**: Aunque un artista puede interpretar múltiples géneros, se almacena el género más representativo para simplificar las consultas

#### **Campo: `redes_sociales`**
- **Tipo**: Object (subdocumento)
- **Estructura**: Contiene campos para diferentes plataformas sociales
- **Propósito**: Enlaces a perfiles oficiales del artista en redes sociales
- **Comentario**: Estructura anidada que permite agregar nuevas plataformas sin modificar el esquema principal

##### **Subcampo: `instagram`**
- **Tipo**: String
- **Formato**: `@username`
- **Ejemplo**: `"@thebeatles"`
- **Propósito**: Usuario de Instagram del artista
- **Comentario**: Se incluye el símbolo @ para facilitar la navegación directa

##### **Subcampo: `twitter`**
- **Tipo**: String
- **Formato**: `@username`
- **Ejemplo**: `"@thebeatles"`
- **Propósito**: Usuario de Twitter/X del artista
- **Comentario**: Permite integración con feeds de redes sociales para contenido dinámico

##### **Subcampo: `facebook`**
- **Tipo**: String
- **Formato**: `username` o `PageName`
- **Ejemplo**: `"TheBeatles"`
- **Propósito**: Página o perfil de Facebook del artista
- **Comentario**: No incluye @ ya que Facebook usa nombres de página

#### **Campo: `activo`**
- **Tipo**: Boolean
- **Valores**: `true` o `false`
- **Ejemplo**: `true`
- **Propósito**: Indica si el artista está activamente produciendo música
- **Comentario**: Útil para filtrar artistas activos vs. retirados en recomendaciones y búsquedas

#### **Campo: `fecha_debut`**
- **Tipo**: String (YYYY)
- **Formato**: Año de 4 dígitos
- **Ejemplo**: `"1960"`
- **Propósito**: Año en que el artista comenzó su carrera musical
- **Comentario**: Se almacena como string para mantener consistencia, aunque se podría convertir a Date para cálculos temporales

### 🔍 Casos de Uso Principales
- **Búsqueda por nombre**: Filtrado de artistas por patrones específicos
- **Segmentación geográfica**: Recomendaciones por región
- **Filtrado por género**: Categorización musical
- **Análisis de actividad**: Estadísticas de artistas activos vs. retirados
- **Integración social**: Enlaces directos a perfiles oficiales

---

## 💿 Colección: `albumes`

### 📋 Descripción General
La colección `albumes` contiene información detallada sobre álbumes musicales, incluyendo metadatos como año de lanzamiento, sello discográfico y estadísticas de tracks. Esta colección actúa como intermediario entre artistas y canciones.

### 🏗️ Estructura de Campos

#### **Campo: `_id`**
- **Tipo**: String (ObjectId personalizado)
- **Formato**: `album_XXX` (donde XXX es un número secuencial)
- **Ejemplo**: `"album_001"`
- **Propósito**: Identificador único del álbum en el sistema
- **Comentario**: Formato consistente con otras colecciones para facilitar el mantenimiento

#### **Campo: `titulo`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 1-100 caracteres)
- **Ejemplo**: `"Abbey Road"`, `"÷ (Divide)"`, `"After Hours"`
- **Propósito**: Título oficial del álbum
- **Comentario**: Puede incluir caracteres especiales, símbolos y emojis. Es el campo principal para búsquedas

#### **Campo: `año`**
- **Tipo**: String (YYYY)
- **Formato**: Año de 4 dígitos
- **Ejemplo**: `"1969"`, `"2020"`
- **Propósito**: Año de lanzamiento del álbum
- **Comentario**: Permite filtrado temporal y análisis de tendencias por década

#### **Campo: `artista_id`**
- **Tipo**: String
- **Formato**: Referencia a `artistas._id`
- **Ejemplo**: `"artista_001"`
- **Propósito**: Referencia al artista que creó el álbum
- **Comentario**: Clave foránea que mantiene la integridad referencial con la colección artistas

#### **Campo: `artista`**
- **Tipo**: String
- **Ejemplo**: `"The Beatles"`
- **Propósito**: Nombre del artista (denormalizado)
- **Comentario**: Campo denormalizado para evitar joins en consultas frecuentes, mejora el rendimiento

#### **Campo: `genero`**
- **Tipo**: String
- **Ejemplo**: `"Rock"`, `"Pop Rock"`
- **Propósito**: Género musical del álbum
- **Comentario**: Puede diferir del género del artista si el álbum es experimental o crossover

#### **Campo: `sello`**
- **Tipo**: String
- **Ejemplo**: `"Apple Records"`, `"Octone Records"`
- **Propósito**: Compañía discográfica que publicó el álbum
- **Comentario**: Útil para análisis de mercado y derechos de autor

#### **Campo: `tracks`**
- **Tipo**: Number
- **Rango**: Típicamente 1-50
- **Ejemplo**: `17`, `12`
- **Propósito**: Número total de canciones en el álbum
- **Comentario**: Entero positivo que permite cálculos de duración promedio por track

#### **Campo: `duracion_total`**
- **Tipo**: String (MM:SS)
- **Formato**: Minutos:Segundos
- **Ejemplo**: `"47:23"`, `"52:50"`
- **Propósito**: Duración total del álbum
- **Comentario**: Formato legible que facilita la presentación al usuario

### 🔍 Casos de Uso Principales
- **Búsqueda por título**: Filtrado de álbumes por nombre
- **Filtrado temporal**: Álbumes por año o década
- **Análisis por sello**: Estadísticas de compañías discográficas
- **Cálculo de duración**: Promedios y totales de duración
- **Relación artista-álbum**: Navegación jerárquica

---

## 🎵 Colección: `canciones`

### 📋 Descripción General
La colección `canciones` es el núcleo del sistema, almacenando información detallada sobre cada canción individual, incluyendo letras, duración y metadatos de relación. Esta colección es la más consultada y requiere optimización de rendimiento.

### 🏗️ Estructura de Campos

#### **Campo: `_id`**
- **Tipo**: String (ObjectId personalizado)
- **Formato**: `cancion_XXX` (donde XXX es un número secuencial)
- **Ejemplo**: `"cancion_001"`
- **Propósito**: Identificador único de la canción en el sistema
- **Comentario**: Formato consistente para facilitar debugging y mantenimiento

#### **Campo: `titulo`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 1-100 caracteres)
- **Ejemplo**: `"Hey Jude"`, `"Shape of You"`, `"Blinding Lights"`
- **Propósito**: Título oficial de la canción
- **Comentario**: Campo principal para búsquedas de texto y filtros

#### **Campo: `duracion`**
- **Tipo**: String (MM:SS)
- **Formato**: Minutos:Segundos
- **Ejemplo**: `"7:11"`, `"3:53"`, `"2:48"`
- **Propósito**: Duración exacta de la canción
- **Comentario**: Formato legible que permite cálculos de duración total y filtros por rango

#### **Campo: `artista_id`**
- **Tipo**: String
- **Formato**: Referencia a `artistas._id`
- **Ejemplo**: `"artista_001"`
- **Propósito**: Referencia al artista que interpreta la canción
- **Comentario**: Clave foránea para mantener integridad referencial

#### **Campo: `artista`**
- **Tipo**: String
- **Ejemplo**: `"The Beatles"`, `"Ed Sheeran"`
- **Propósito**: Nombre del artista (denormalizado)
- **Comentario**: Campo denormalizado para evitar joins en consultas frecuentes

#### **Campo: `album_id`**
- **Tipo**: String
- **Formato**: Referencia a `albumes._id`
- **Ejemplo**: `"album_001"`
- **Propósito**: Referencia al álbum que contiene la canción
- **Comentario**: Clave foránea para navegación jerárquica

#### **Campo: `album`**
- **Tipo**: String
- **Ejemplo**: `"Abbey Road"`, `"÷ (Divide)"`
- **Propósito**: Título del álbum (denormalizado)
- **Comentario**: Campo denormalizado para consultas eficientes

#### **Campo: `genero`**
- **Tipo**: String
- **Ejemplo**: `"Rock"`, `"Pop"`, `"R&B"`
- **Propósito**: Género musical de la canción
- **Comentario**: Puede diferir del género del álbum o artista para canciones específicas

#### **Campo: `letra`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 50-2000 caracteres)
- **Ejemplo**: `"Hey Jude, don't be afraid. Take a sad song and make it better..."`
- **Propósito**: Letra completa o fragmento representativo de la canción
- **Comentario**: Campo de texto largo que permite búsquedas semánticas y análisis de contenido

### 🔍 Casos de Uso Principales
- **Búsqueda por título**: Filtrado de canciones por nombre
- **Búsqueda en letras**: Contenido semántico y temático
- **Filtrado por duración**: Rangos de tiempo específicos
- **Navegación jerárquica**: Artista → Álbum → Canción
- **Análisis de contenido**: Patrones en letras y títulos

---

## 👤 Colección: `usuarios`

### 📋 Descripción General
La colección `usuarios` almacena información de los usuarios registrados en la plataforma, incluyendo preferencias musicales, datos de suscripción y ubicación geográfica. Esta colección es fundamental para personalización y análisis de comportamiento.

### 🏗️ Estructura de Campos

#### **Campo: `_id`**
- **Tipo**: String (ObjectId personalizado)
- **Formato**: `usuario_XXX` (donde XXX es un número secuencial)
- **Ejemplo**: `"usuario_001"`
- **Propósito**: Identificador único del usuario en el sistema
- **Comentario**: Formato consistente para facilitar el mantenimiento y debugging

#### **Campo: `nombre`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 2-50 caracteres)
- **Ejemplo**: `"Maria"`, `"John"`, `"Ana"`
- **Propósito**: Nombre real o de usuario del cliente
- **Comentario**: Campo principal para identificación personal y comunicación

#### **Campo: `correo`**
- **Tipo**: String
- **Formato**: Dirección de correo electrónico válida
- **Ejemplo**: `"maria@gmail.com"`, `"john123@hotmail.com"`
- **Propósito**: Dirección de correo para autenticación y comunicación
- **Comentario**: Debe ser único en el sistema y validado por formato

#### **Campo: `ciudad`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 2-50 caracteres)
- **Ejemplo**: `"Madrid"`, `"New York"`, `"Barcelona"`
- **Propósito**: Ciudad de residencia del usuario
- **Comentario**: Permite segmentación geográfica para eventos locales y recomendaciones

#### **Campo: `pais`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 5-30 caracteres)
- **Ejemplo**: `"España"`, `"Estados Unidos"`, `"México"`
- **Propósito**: País de residencia del usuario
- **Comentario**: Útil para análisis de mercado por región y cumplimiento legal

#### **Campo: `suscripcion`**
- **Tipo**: String
- **Valores**: `"Free"`, `"Premium"`
- **Ejemplo**: `"Premium"`
- **Propósito**: Tipo de suscripción del usuario
- **Comentario**: Determina funcionalidades disponibles y nivel de servicio

#### **Campo: `fecha_registro`**
- **Tipo**: String (YYYY-MM-DD)
- **Formato**: Fecha ISO
- **Ejemplo**: `"2020-03-15"`
- **Propósito**: Fecha en que el usuario se registró en la plataforma
- **Comentario**: Permite análisis de retención y crecimiento de usuarios

#### **Campo: `generos_favoritos`**
- **Tipo**: Array de Strings
- **Ejemplo**: `["Pop", "Rock", "R&B"]`
- **Propósito**: Lista de géneros musicales preferidos del usuario
- **Comentario**: Array que permite múltiples preferencias para recomendaciones personalizadas

### 🔍 Casos de Uso Principales
- **Autenticación**: Validación de credenciales
- **Personalización**: Recomendaciones basadas en preferencias
- **Segmentación**: Análisis demográfico y geográfico
- **Análisis de suscripción**: Métricas de conversión y retención
- **Marketing**: Campañas dirigidas por ubicación y preferencias

---

## 📂 Colección: `playlists`

### 📋 Descripción General
La colección `playlists` almacena listas de reproducción creadas por usuarios, incluyendo metadatos como descripción, género principal y duración total. Esta colección es fundamental para la experiencia de usuario y el descubrimiento de música.

### 🏗️ Estructura de Campos

#### **Campo: `_id`**
- **Tipo**: String (ObjectId personalizado)
- **Formato**: `playlist_XXX` (donde XXX es un número secuencial)
- **Ejemplo**: `"playlist_001"`
- **Propósito**: Identificador único de la playlist en el sistema
- **Comentario**: Formato consistente para facilitar el mantenimiento

#### **Campo: `nombre`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 1-100 caracteres)
- **Ejemplo**: `"🎵 Party Vibes 🎉"`, `"Rock Classics"`, `"💕 Love Songs 💕"`
- **Propósito**: Nombre descriptivo de la playlist
- **Comentario**: Puede incluir emojis y caracteres especiales para personalización

#### **Campo: `descripcion`**
- **Tipo**: String
- **Longitud**: Variable (típicamente 10-200 caracteres)
- **Ejemplo**: `"Perfect for dancing and having fun with friends"`
- **Propósito**: Descripción detallada del propósito o contenido de la playlist
- **Comentario**: Permite búsquedas semánticas y comprensión del contexto

#### **Campo: `usuario_creador_id`**
- **Tipo**: String
- **Formato**: Referencia a `usuarios._id`
- **Ejemplo**: `"usuario_001"`
- **Propósito**: Referencia al usuario que creó la playlist
- **Comentario**: Clave foránea para mantener integridad referencial

#### **Campo: `usuario_creador`**
- **Tipo**: String
- **Ejemplo**: `"Maria"`, `"John"`
- **Propósito**: Nombre del usuario creador (denormalizado)
- **Comentario**: Campo denormalizado para evitar joins en consultas frecuentes

#### **Campo: `canciones_incluidas`**
- **Tipo**: Array de Strings
- **Formato**: Referencias a `canciones._id`
- **Ejemplo**: `["cancion_003", "cancion_004", "cancion_009"]`
- **Propósito**: Lista de IDs de canciones incluidas en la playlist
- **Comentario**: Array que permite orden personalizado y gestión de contenido

#### **Campo: `genero_principal`**
- **Tipo**: String
- **Ejemplo**: `"Pop"`, `"Rock"`, `"R&B"`
- **Propósito**: Género musical predominante en la playlist
- **Comentario**: Útil para categorización y recomendaciones automáticas

#### **Campo: `duracion_total`**
- **Tipo**: String (MM:SS)
- **Formato**: Minutos:Segundos
- **Ejemplo**: `"11:39"`, `"22:02"`
- **Propósito**: Duración total de la playlist
- **Comentario**: Calculado dinámicamente basado en las canciones incluidas

#### **Campo: `fecha_creacion`**
- **Tipo**: String (YYYY-MM-DD)
- **Formato**: Fecha ISO
- **Ejemplo**: `"2023-01-15"`
- **Propósito**: Fecha en que se creó la playlist
- **Comentario**: Permite análisis temporal y ordenamiento cronológico

### 🔍 Casos de Uso Principales
- **Descubrimiento**: Playlists recomendadas por género o tema
- **Personalización**: Creación y gestión de listas personales
- **Compartir**: Socialización de gustos musicales
- **Análisis**: Estadísticas de uso y popularidad
- **Recomendaciones**: Sugerencias basadas en contenido similar

---

## 🔗 Relaciones entre Colecciones

### 📊 Diagrama de Relaciones
```
usuarios (1) ←→ (N) playlists
  ↓
artistas (1) ←→ (N) albumes
  ↓
albumes (1) ←→ (N) canciones
  ↓
playlists (N) ←→ (N) canciones
```

### 🔍 Tipos de Relaciones

#### **Relación 1:N (Uno a Muchos)**
- **Usuario → Playlists**: Un usuario puede crear múltiples playlists
- **Artista → Álbumes**: Un artista puede tener múltiples álbumes
- **Álbum → Canciones**: Un álbum puede contener múltiples canciones

#### **Relación N:N (Muchos a Muchos)**
- **Playlists ↔ Canciones**: Una playlist puede contener múltiples canciones, y una canción puede estar en múltiples playlists

#### **Relación 1:1 (Uno a Uno)**
- **Artista ↔ Perfil**: Cada artista tiene un perfil único
- **Usuario ↔ Cuenta**: Cada usuario tiene una cuenta única

### 💡 Estrategias de Denormalización

#### **Campos Denormalizados**
- `artista` en `albumes` y `canciones`
- `album` en `canciones`
- `usuario_creador` en `playlists`

#### **Propósito de Denormalización**
- **Rendimiento**: Evita joins en consultas frecuentes
- **Legibilidad**: Facilita la comprensión de los datos
- **Mantenimiento**: Simplifica las consultas de lectura

#### **Consideraciones**
- **Consistencia**: Los campos denormalizados deben mantenerse sincronizados
- **Espacio**: Aumenta ligeramente el uso de almacenamiento
- **Actualización**: Requiere lógica para mantener consistencia

---

## 🎯 Casos de Uso Avanzados

### 🔍 Búsquedas Complejas

#### **Búsqueda Multi-Colección**
```javascript
// Encontrar todas las canciones de artistas activos en playlists de usuarios premium
db.canciones.aggregate([
  {
    $lookup: {
      from: "artistas",
      localField: "artista_id",
      foreignField: "_id",
      as: "artista_info"
    }
  },
  {
    $lookup: {
      from: "playlists",
      localField: "_id",
      foreignField: "canciones_incluidas",
      as: "playlist_info"
    }
  },
  {
    $match: {
      "artista_info.activo": true,
      "playlist_info.usuario_creador_id": {
        $in: db.usuarios.find({ "suscripcion": "Premium" }).map(u => u._id)
      }
    }
  }
])
```

#### **Análisis de Tendencias**
```javascript
// Analizar géneros más populares por década
db.albumes.aggregate([
  {
    $group: {
      _id: {
        decada: { $substr: ["$año", 0, 3] + "0" },
        genero: "$genero"
      },
      count: { $sum: 1 }
    }
  },
  {
    $sort: { "_id.decada": 1, "count": -1 }
  }
])
```

### 📊 Agregaciones Complejas

#### **Estadísticas de Usuario**
```javascript
// Calcular estadísticas completas de un usuario
db.usuarios.aggregate([
  {
    $match: { "_id": "usuario_001" }
  },
  {
    $lookup: {
      from: "playlists",
      localField: "_id",
      foreignField: "usuario_creador_id",
      as: "playlists_creadas"
    }
  },
  {
    $lookup: {
      from: "canciones",
      localField: "generos_favoritos",
      foreignField: "genero",
      as: "canciones_recomendadas"
    }
  },
  {
    $project: {
      nombre: 1,
      total_playlists: { $size: "$playlists_creadas" },
      total_canciones_recomendadas: { $size: "$canciones_recomendadas" },
      generos_favoritos: 1
    }
  }
])
```

---

## 🚀 Optimizaciones Recomendadas

### 📈 Índices Sugeridos

#### **Colección: `artistas`**
```javascript
// Índice en nombre para búsquedas de texto
db.artistas.createIndex({ "nombre": 1 })

// Índice compuesto en país y género
db.artistas.createIndex({ "pais": 1, "genero": 1 })

// Índice en fecha_debut para análisis temporal
db.artistas.createIndex({ "fecha_debut": 1 })
```

#### **Colección: `canciones`**
```javascript
// Índice de texto en título y letra
db.canciones.createIndex({ "titulo": "text", "letra": "text" })

// Índice en artista_id para joins eficientes
db.canciones.createIndex({ "artista_id": 1 })

// Índice en género para filtros rápidos
db.canciones.createIndex({ "genero": 1 })
```

#### **Colección: `usuarios`**
```javascript
// Índice único en correo
db.usuarios.createIndex({ "correo": 1 }, { unique: true })

// Índice en suscripción para segmentación
db.usuarios.createIndex({ "suscripcion": 1 })

// Índice compuesto en ciudad y país
db.usuarios.createIndex({ "ciudad": 1, "pais": 1 })
```

### 🔧 Configuraciones de Rendimiento

#### **Configuración de WiredTiger**
```javascript
// Configuración recomendada para colecciones grandes
db.adminCommand({
  setParameter: 1,
  wiredTigerConcurrentReadTransactions: 128,
  wiredTigerConcurrentWriteTransactions: 128
})
```

#### **Configuración de Memoria**
```javascript
// Asignar memoria específica para índices
db.adminCommand({
  setParameter: 1,
  maxIndexBuildMemoryUsageMegabytes: 1024
})
```

---

## 📝 Notas de Mantenimiento

### 🔄 Sincronización de Datos Denormalizados

#### **Trigger de Actualización**
```javascript
// Función para mantener sincronizados los campos denormalizados
function actualizarCamposDenormalizados(coleccion, campo, valor, id) {
  if (coleccion === "artistas") {
    // Actualizar nombre en albumes y canciones
    db.albumes.updateMany(
      { "artista_id": id },
      { $set: { "artista": valor } }
    )
    db.canciones.updateMany(
      { "artista_id": id },
      { $set: { "artista": valor } }
    )
  }
}
```

#### **Validación de Integridad**
```javascript
// Función para validar integridad referencial
function validarIntegridadReferencial() {
  // Verificar que todas las referencias existen
  const referenciasInvalidas = db.canciones.find({
    "artista_id": { $nin: db.artistas.distinct("_id") }
  })
  
  if (referenciasInvalidas.count() > 0) {
    print("⚠️  Referencias inválidas encontradas en canciones")
    return false
  }
  return true
}
```

### 📊 Monitoreo y Métricas

#### **Estadísticas de Colección**
```javascript
// Obtener estadísticas detalladas de cada colección
db.runCommand({
  collStats: "artistas",
  scale: 1024 * 1024 // Resultado en MB
})

db.runCommand({
  collStats: "canciones",
  scale: 1024 * 1024
})
```

#### **Análisis de Consultas**
```javascript
// Habilitar profiling para análisis de rendimiento
db.setProfilingLevel(2, { slowms: 100 })

// Ver consultas lentas
db.system.profile.find({ millis: { $gt: 100 } }).sort({ millis: -1 })
```

---

## 🎯 Conclusión

Este documento proporciona una guía completa para entender y trabajar con las colecciones de MongoDB en el sistema de música. Cada campo ha sido diseñado con un propósito específico, considerando tanto la funcionalidad como el rendimiento.

### 🔑 Puntos Clave
- **Estructura Relacional**: Las colecciones mantienen relaciones lógicas bien definidas
- **Denormalización Estratégica**: Campos duplicados para optimizar consultas frecuentes
- **Flexibilidad**: Esquema que permite crecimiento y evolución del sistema
- **Rendimiento**: Índices y configuraciones optimizadas para consultas rápidas
- **Mantenibilidad**: Código y documentación que facilitan el desarrollo futuro

### 🚀 Próximos Pasos
1. **Implementar índices** sugeridos para optimizar consultas
2. **Configurar monitoreo** para detectar problemas de rendimiento
3. **Desarrollar funciones** de mantenimiento para datos denormalizados
4. **Crear tests** para validar integridad referencial
5. **Documentar APIs** que utilicen estas colecciones

---

*Documento generado para el Taller de Expresiones Regulares con MongoDB - Sistema de Música* 