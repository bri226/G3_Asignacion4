# <b>PROYECTO - GRUPO 3</b>
## Índice
- [Configuración de la herramienta Flutter](#configuración-de-la-herramienta-flutter)
    - [Para Windows](#para-windows)
    - [Para Mac](#para-mac)
- [Configuración de Ambiente de Desarrollo o IDE (Visual Studio Code)](#configurar-ambiente-de-desarrollo-o-ide-visual-studio-code)
    - [Añadir extensión](#añadir-extensión)
    - [Crear proyecto en VS Code](#crear-proyecto-en-vs-code)
        - [Para Windows](#para-windows-1)
        - [Para Mac](#para-mac-1)
- [Instalación de Dependencias y conexión al servidor](#instalación-de-dependencias-y-conexión-a-servidor)
- [Firebase](#firebase)
- [Diagrama de Despliegue](#diagrama-de-despliegue)
- [Requerimientos no funcionales](#requerimientos-no-funcionales)
- [Casos de uso](#casos-de-uso)
- [Ir a Fuentes](#fuentes)

---

## <b>Configuración de la herramienta Flutter</b>

### <b>Para Windows</b>

1. Requerimientos mínimos
    - Windows 10 o posterior (64 bits), basado en x86-64.
    - Espacio en disco: 1,64 GB
    - Windows PowerShell 5.0 (default)
    - Git para Windows 2.x 
2. Obtener el SDK de Flutter
    - Descargar haciendo clic [aquí](https://storage.googleapis.com/flutter_infra_release/releases/stable/windows/flutter_windows_3.10.5-stable.zip).

        <i>Nota</i>: Para versiones anteriores del SDK, clic [aquí](https://docs.flutter.dev/release/archive).
3. Extraer el zip en la ruta que se elija.

4. Actualizar el <b>path</b>
    - Ir a "Editar variables de entorno para su cuenta" en la barra de búsqueda de Inicio
    - En Variables de usuario, comprueba si hay una entrada llamada Path:
        - Si la entrada existe, añada la ruta completa a flutter\bin utilizando ; como separador de los valores existentes.
        - Si la entrada no existe, cree una nueva variable de usuario llamada Path con la ruta completa a flutter\bin como valor.
        - Cerrar y volver a abrir cualquier consola para que se guarden los cambios.

5. Ejecutar <i style="color:#2F98A4">flutter doctor</i>

        C:\src\flutter>flutter doctor

    - Instalar los software que falten u otras tareas que se indiquen en los resultados de la ejecución del comando.

### <b>Para Mac</b>
1. Requerimientos mínimos
    - Sistema Operativo macOS, versión 10.14 (Mojave) o posterior
    - Espacio en disco: 2,08 GB
    - Flutter utiliza git para la instalación y actualización.
2. Obtener el SDK de Flutter
    - Para procesadores Intel: clic [aquí](https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_3.10.5-stable.zip).
    - Para procesadores basados en la arquitectura ARM de Apple Silicon (nuestro caso, procesador M1): clic [aquí](https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_arm64_3.10.5-stable.zip).

3. Extraer el zip en la ruta que se elija.

        $ unzip ~/Downloads/flutter_macos_3.10.5-stable.zip


4. Añadir la herramienta Flutter al <b>path</b>

        $ export PATH="$PATH:`pwd`/flutter/bin"

5. Ejecutar <i style="color:#2F98A4">flutter doctor</i>

        flutter doctor 

    - Instalar los software que falten u otras tareas que se indiquen en los resultados de la ejecución del comando.

    ![img1](img/flutter-doctor.png)
 


## <b>Configuración Ambiente de Desarrollo o IDE (Visual Studio Code)</b>

### <b>Añadir extensión</b>
En la sección de <i>Extensions</i> (Ctrl + Shift + X), buscar e instalar:
- "Flutter" de [DartCode.org](https://dartcode.org/) 
- "Dart" de [DartCode.org](https://dartcode.org/) <i>(usualmente se instala junto con Flutter)</i>

<br>

### <b>Crear proyecto en VS Code</b>

#### <b>Para Windows</b>

1. Buscar archivo o Ctrl + P:

        > Flutter: New Project
    
    ![img2](img/create_project1.png)

2. Crear aplicación con Flutter:

    ![img3](img/create_project2.png)

3. Seleccionar la carpeta en la que se guardará el proyecto y crear nombre. El nombre del proyecto debe ir en minúsculas y separado por guiones bajos en caso fuera necesario.

    ![img4](img/create_project3.png)

#### <b>Para Mac</b>

1. En la consola de VS Code o en la terminal:

        > cd <ruta_donde_se_va_a_crear_el_proyecto> 
        > flutter create <nombre_de_app> 

## <b>Instalación de dependencias y conexión a servidor</b>

Para la conexión al servidor, se usará el mismo backend que se utilizó para la entrega anterior. Las dependencias se colocan en el archivo <b>pubspec.yaml</b>:
```yaml
 dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3
```

Luego de colocarlas, se instalan a través de la terminal con el comando:

        > flutter pub get

![img5](img/install_dependencies.png)


Para usarlas en un archivo dart, colocar esta línea:

```dart
    import 'package:http/http.dart' as http;
```

## <b>Firebase</b>

### Instalación de Firebase
<br>

- Con Node JS instalado, ejecutar (tanto para Windows como para Mac):

        > npm install -g firebase-tools


Seguir los siguientes pasos:
1. Iniciar sesión en Firebase con cuenta de Google ([link](https://console.firebase.google.com/)).
2. En la consola de Firebase, crear un proyecto.
3. Agregar app para Flutter

    ![img6](img/agregar_app_firebase.png)

4. En la nueva pantalla:
    - Preparar lugar de trabajo
        - Tener instalado el CLI de Firebase e iniciar sesión en la consola a través de:
            > firebase login
        - Tener instalado el SDK de Flutter
        - Tener un proyecto creado en Flutter
    - Instalar y ejecutar la CLI de FlutterFire
        - Ejecutar comando:
            > dart pub global activate flutterfire_cli
        - En la raíz del directorio del proyecto, ejecutar comando:
            > flutterfire configure --project=<nombre_proyecto>-debbe
        - Si no permite ejecutar ese último comando, ir a Inicio y buscar "Editar variables de entorno de esta cuenta" y agregar en PATH lo siguiente:
            > C:\Users\<usuario>\AppData\Local\Pub\Cache\bin
    - Inicializar Firebase:
        - En el archivo dart, importar:

        ```dart
        import 'package:firebase_core/firebase_core.dart';
        import 'firebase_options.dart';
        ```

        - Añadir el código:

        ```dart
        await Firebase.initializeApp(
            options: DefaultFirebaseOptions.currentPlatform,
        );
        ```
    
    - En caso salga error en la primera librería, ejecutar este comando en la raíz del directorio:

        > flutter pub add firebase_core

        <i>Eso debería resolver el problema</i>

## <b>Diagrama de Despliegue</b>
<br>

![img7](img/diagramadespliegue.png)

## <b>Requerimientos no funcionales</b>

 **1. Usabilidad:**
- La interfaz de usuario debe ser intuitiva y fácil de usar para usuarios no técnicos.
- Los tiempos de carga de la aplicación deben ser rápidos, para minimizar la espera del usuario.
- La aplicación debe ser compatible con una amplia gama de dispositivos móviles y tamaños de pantalla.

**2. Rendimiento:**
- Los tiempos de respuesta de la aplicación deben ser consistentes incluso bajo cargas de trabajo pesadas.
- La aplicación debe optimizarse para minimizar el consumo de recursos (CPU, memoria, batería) en el dispositivo móvil.
    
**3. Seguridad:**
- Los datos personales de los usuarios deben ser almacenados y transmitidos de manera segura, utilizando técnicas de encriptación adecuadas.
 - La aplicación debe implementar medidas de autenticación y autorización para garantizar el acceso seguro a las funciones y datos.
- Se debe realizar una validación adecuada de los datos de entrada para prevenir ataques como inyecciones de código o ataques de denegación de servicio.
  
**4. Escalabilidad:**
- La aplicación debe ser capaz de manejar un aumento en el número de usuarios y transacciones sin degradar su rendimiento.
- Debe ser posible agregar nuevos servicios o funcionalidades a la aplicación sin afectar negativamente su rendimiento o disponibilidad.
  
**5. Fiabilidad:**
- La aplicación debe ser estable y no debe bloquearse o cerrarse inesperadamente.
- La aplicación debe tener mecanismos de recuperación ante fallas, de modo que pueda continuar funcionando correctamente después de una interrupción.

<br>

## <b>Casos de Uso</b>
<br>

### <b>1. Crear cuenta</b>

Este proceso inicia cuando el usuario decide crear una cuenta en la aplicación. En caso no sea registrado con una cuenta no existente, el usuario deberá brindar su nombre, su nickname, un correo electrónico y una contraseña.

![img8](img/CrearCuenta.png)

Mockup relacionado: [clic aquí](#imagen-1)

### <b>2. Recuperar contraseña</b>

En caso el usuario olvide su contraseña, esta opción estará disponible en el view del Login. Al utilizar esta opción, el usuario deberá identificarse con su correo electrónico para verificar la existencia de la cuenta. Si la cuenta existe, se le enviará un mensaje al correo electrónico del usuario que contendrá un link para reestablecer la contraseña.

![img9](img/CambiarPass.png)

Mockup relacionado: [clic aquí](#imagen-2)

### <b>3. Iniciar sesión</b>

Este proceso inicia cuando el usuario quiere ingresar al contenido de la aplicación. El usuario deberá identificarse con su correo electrónico y contraseña, la cual será verificado si existe, para posteriormente ser autenticado para ingresar a sus datos en la aplicación.

![img10](img/Login.png)

Mockup relacionado: [clic aquí](#imagen-3)

### <b>4. Gestionar perfil</b>

En caso el usuario quiera modificar los datos dentro de su perfil, debe verificarse que el usuario que está realizando los cambios sea el mismo que ha iniciado sesión y no otro usuario. Si el usuario es verificado como propietario, será capaz de cambiar su foto de perfil, su apodo, su correo electrónico, su nombre y su contraseña.


![img11](img/GestionarPerfil.png)

Mockup relacionado: [clic aquí](#imagenes-4)

### <b>5. Visualizar otros usuarios</b>

El usuario podrá ser capaz de visualizar el contenido subido por los usuarios que él sigue o es seguido. Así también como el número de usuarios que lo siguen o que él sigue.

![img12](img/Visualizar.png)

Mockup relacionado: [clic aquí](#imagenes-5)

## <b>Mockups</b>

### Imagen 1
![img13](mockups/crear-cuenta.PNG)

### Imagen 2
![img14](mockups/restablecer-contraseña.PNG)

### Imagen 3
![img15](mockups/inicio-sesion.PNG)

### Imagenes 4
![img16](mockups/gestion-perfil.PNG)
![img17](mockups/gestion-perfil-2.PNG)

### Imagenes 5
![img18](mockups/perfil-principal.PNG)
![img19](mockups/seguidores.PNG)
![img20](mockups/seguidos.PNG)



---
### <b>Fuentes</b>:
+ SDK de Flutter: [link](https://docs.flutter.dev/get-started/install)
+ Referencia de Firebase CLI: [link](https://firebase.google.com/docs/cli?hl=es&authuser=0&_gl=1*1crcpgv*_ga*MTgyNDYwMjI3OC4xNjg2OTUzODQx*_ga_CW55HF8NVT*MTY4ODYxNDQ1OS40LjEuMTY4ODYxNTgxOC4wLjAuMA..#install_the_firebase_cli)

