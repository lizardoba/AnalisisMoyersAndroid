# Análisis de Moyers y Tanaka - App Android

Aplicación Android nativa para análisis de predicción de espacio en dentición mixta utilizando los métodos de Moyers y Tanaka & Johnston. Desarrollada con Firebase para gestión de datos de pacientes.

## Características

✅ Cálculo de análisis Moyers con interpolación automática
✅ Cálculo de Tanaka & Johnston
✅ Gestión de datos de pacientes con Firebase
✅ Autenticación segura
✅ Almacenamiento en la nube
✅ Interfaz intuitiva y responsiva
✅ Exportación de reportes

## Estructura del Proyecto

```
AnalisisMoyersAndroid/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/orthodontics/analisis/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── AnalysisActivity.kt
│   │   │   │   ├── PatientsActivity.kt
│   │   │   │   ├── ReportsActivity.kt
│   │   │   │   ├── models/
│   │   │   │   │   ├── Patient.kt
│   │   │   │   │   ├── AnalysisResult.kt
│   │   │   │   │   └── MoyersData.kt
│   │   │   │   ├── repositories/
│   │   │   │   │   ├── PatientRepository.kt
│   │   │   │   │   └── FirebaseRepository.kt
│   │   │   │   ├── viewmodels/
│   │   │   │   │   ├── AnalysisViewModel.kt
│   │   │   │   │   └── PatientViewModel.kt
│   │   │   │   └── utils/
│   │   │   │       ├── MoyersCalculator.kt
│   │   │   │       ├── TanakaCalculator.kt
│   │   │   │       └── Constants.kt
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml
│   │   │   │   │   ├── activity_analysis.xml
│   │   │   │   │   ├── activity_patients.xml
│   │   │   │   │   └── fragment_results.xml
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   └── dimens.xml
│   │   │   │   └── drawable/
│   │   │   │       └── (iconos y drawables)
│   │   │   └── AndroidManifest.xml
│   │   └── test/ (pruebas unitarias)
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── gradle/
│   └── wrapper/
├── build.gradle.kts (raíz)
├── settings.gradle.kts
├── firebase-config/
│   ├── google-services.json (IMPORTANTE: añadir tu archivo)
│   └── firebase-setup.md
└── README.md
```

## Requisitos Previos

- Android Studio Jellyfish (2023.3.1) o superior
- JDK 11 o superior
- Android SDK 24+ (API level 24)
- Proyecto Firebase creado
- Cuenta de Google

## Instalación y Configuración

### 1. Descargar Android Studio

```bash
# Desde: https://developer.android.com/studio
```

### 2. Clonar el Repositorio

```bash
git clone https://github.com/lizardoba/AnalisisMoyersAndroid.git
cd AnalisisMoyersAndroid
```

### 3. Configurar Firebase

#### Paso 3.1: Crear Proyecto en Firebase
- Ve a [Firebase Console](https://console.firebase.google.com/)
- Crea un nuevo proyecto llamado "Análisis Moyers"
- Selecciona "Agregar app Android"
- Introduce el nombre del paquete: `com.orthodontics.analisis`
- Descarga el archivo `google-services.json`

#### Paso 3.2: Agregar google-services.json

```
AnalisisMoyersAndroid/app/google-services.json
```

Copia el archivo descargado de Firebase a la carpeta `app/`

### 4. Abrir en Android Studio

```bash
# Abre Android Studio
# File > Open > Selecciona la carpeta del proyecto
```

Android Studio descargará automáticamente las dependencias necesarias.

### 5. Ejecutar la App

```
Run > Run 'app' (Shift + F10)
```

OAltarnativamente, conecta un dispositivo Android y ejecuta desde el botón "Run".

## Dependencias

```gradle
dependencies {
    // Firebase
    implementation(platform("com.google.firebase:firebase-bom:32.7.1"))
    implementation("com.google.firebase:firebase-auth-ktx")
    implementation("com.google.firebase:firebase-firestore-ktx")
    implementation("com.google.firebase:firebase-analytics-ktx")
    
    // AndroidX
    implementation("androidx.appcompat:appcompat:1.6.1")
    implementation("androidx.constraintlayout:constraintlayout:2.1.4")
    implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.6.2")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.6.2")
    
    // Material Design
    implementation("com.google.android.material:material:1.10.0")
    
    // Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-play-services:1.7.3")
}
```

## Estructura de Base de Datos Firestore

```
users/
├── {userId}/
│   ├── email: string
│   ├── name: string
│   ├── createdAt: timestamp
│   └── clinic: string

patients/
├── {patientId}/
│   ├── userId: string
│   ├── name: string
│   ├── birthDate: date
│   ├── gender: string ("M"/"F")
│   ├── createdAt: timestamp
│   └── analyses: array

analyses/
├── {analysisId}/
│   ├── patientId: string
│   ├── userId: string
│   ├── date: timestamp
│   ├── incisivosMM: number
│   ├── gender: string
│   ├── arcada: string ("Superior"/"Inferior")
│   ├── espacioModelo: number
│   ├── moyersResult: number
│   ├── moyersDiscrepancy: number
│   ├── tanakaResult: number
│   ├── tanakaDiscrepancy: number
│   └── notes: string
```

## Guía de Desarrollo

### Agregar Nueva Funcionalidad

1. **Crear el Modelo:**
   ```kotlin
   data class NewFeature(
       val id: String,
       val name: String,
       val data: Any
   )
   ```

2. **Crear el Repository:**
   ```kotlin
   class NewFeatureRepository {
       suspend fun fetchData() = withContext(Dispatchers.IO) {
           // Lógica de Firebase
       }
   }
   ```

3. **Crear el ViewModel:**
   ```kotlin
   class NewFeatureViewModel : ViewModel() {
       // Lógica del estado
   }
   ```

4. **Crear la UI (Activity/Fragment)**

### Pruebas

```bash
# Ejecutar pruebas unitarias
./gradlew test

# Ejecutar pruebas de instrumentación
./gradlew connectedAndroidTest
```

## Compilar Apk para Distribución

```bash
# Debug
./gradlew assembleDebug

# Release
./gradlew assembleRelease
```

El APK se encontrará en: `app/build/outputs/apk/`

## Publicar en Google Play Store

1. Crear un account de desarrollador: $25 USD
2. Generar keystore:
   ```bash
   keytool -genkey -v -keystore release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
   ```
3. Firmar el release APK en Android Studio
4. Subir a Play Store Console

## Características Planeadas

- [ ] Captura de fotos de pacientes integrada
- [ ] Análisis Bolton
- [ ] Reportes en PDF
- [ ] Sincronización offline
- [ ] App para iOS con React Native
- [ ] Dashboard web para clínicas

## Contribuciones

Las contribuciones son bienvenidas. Por favor:
1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## Licencia

Este proyecto está bajo la licencia MIT. Ver `LICENSE` para más detalles.

## Autor

**Dr. Lizardo Barba Ortiz**
- Ortodoncista - Centro Integral Infantil y Familiar (Gniius)
- GitHub: [@lizardoba](https://github.com/lizardoba)
- Email: contacto@ortoapp.com

## Soporte

Para reportar bugs o sugerencias:
- Issues: [GitHub Issues](https://github.com/lizardoba/AnalisisMoyersAndroid/issues)
- Email: support@ortoapp.com

---

**Última actualización:** Noviembre 2025
**Versión:** 1.0.0-beta
