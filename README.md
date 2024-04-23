# API-RESERVAS

1- Laravel Sanctum -> Tokens

	composer require laravel/sanctum


2- Publicar las Migraciones

	php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"


3- Configurar .env

Crear BD

4- EJECUTAR LAS MIGRACIONES

	php artisan migrate


5- CREAR LAS RUTAS

6- CREAR LOS MODELOS + MIGRACION + CONTROLADOR (RESOURCE)

	php artisan make:model Reserva -mcr


7- Crear un Controlador (este se encargara de el login y el register)

	php artisan make:controller AuthController


8- AÑADIR LOS CAMPOS A LA MIGRACION (TABLA) DE reserva


	$table->string('modelo')
	$table->string('año')
	$table->enum('status', ['activo', 'cancelado', 	'completado'])->default('activo');

	ó
	$table->integer('status') 
	
	etc
	

2. Utilizando Boolean:
Si solo necesitas dos estados (por ejemplo, "activo" y "cancelado"), podrías usar un campo boolean.

php
Copy code
Schema::create('reservas', function (Blueprint $table) {
    $table->id();
    // ... otros campos ...
    $table->boolean('status')->default(true); // true: Activo, false: Cancelado
    $table->timestamps();
});




9- DEVOLVER TODAS LAS RESERVAS EN INDEX

	$reservas = Reserva::all()
	return $reservas;

10- Ruta

Route::get('products', [ReservaController::class, 'index']);

LEVANTAR SERVIDOR Y PROBAR EN POSTMAN Y PROBAR CON LA PRIMERA REQUEST DE TIPO GET (ENDPOINT).

https:127.0.1:8000/api/reservas


11- AUTHCONTROLLER -> login y register
	


Integración 4D-CarTrawler

Mes 1: Desarrollo de las API's
Semana 1-2: Investigación y diseño de las API's REST/HTTP utilizando Laravel.
Semana 3-4: Implementación de los endpoints GET y POST.
Mes 2: Integración y pruebas
Semana 1-2: Integración de las API's con el sistema 4D.
Semana 3-4: Pruebas de integración y corrección de errores.

Se deben desarrollar las API que deben ser consumidas por CarTrawler para agregar, actualizar o anular reservas.
El objetivo es que estas APIs pueden ser utilizadas por otras OTAs, Aseguradoras y Mayoristas de Turismo.
Descripción técnica:
•	Las API’s deben ser de tipo REST o HTTP, estas deben ser desarrolladas con el framework Laravel.
•	Para aceptar las peticiones de un tercero (en este caso CarTrawler) de realizarse por tokens. Es importante llevar un registro o log de conexión y el tipo de acción que se ha realizado
•	Las acciones a ejecutar son: GET y POST.
•	Se deben crear los métodos en el 4D para procesar cada acción.




Desarrollar APIs de integración con CarTrawler para facilitar la gestión de reservas de vehículos:
Este objetivo implica la creación de interfaces de programación de aplicaciones (APIs) que permitan la comunicación entre el sistema de gestión de Car Rental y la plataforma de CarTrawler. Estas APIs deben ser diseñadas para ser eficientes, seguras y fáciles de usar.
Se requerirá un análisis exhaustivo de los requisitos de integración proporcionados por CarTrawler para asegurar que las API cumplan con sus estándares y permitan una comunicación fluida entre los sistemas.
El desarrollo de estas APIs debe incluir la implementación de funciones para agregar, actualizar y cancelar reservas de vehículos, así como para gestionar cualquier información adicional necesaria para el proceso de reserva.
Además del desarrollo de las APIs en sí, se deben establecer mecanismos para autenticar y autorizar las solicitudes de CarTrawler, lo que puede implicar el uso de tokens de seguridad u otros métodos de autenticación.	





Análisis de Requisitos: Revisaría detalladamente la documentación proporcionada por CarTrawler para comprender las necesidades de integración. Esto incluiría entender los tipos de paquetes de arriendo de vehículos, las acciones que se deben realizar (agregar, actualizar o anular reservas), y los datos que se intercambiarán entre los sistemas.
Diseño de las API's: Basado en los requisitos, diseñaría las API's que se utilizarán para la integración. Las API's deben seguir los estándares RESTful o HTTP y se desarrollarán utilizando el framework Laravel. Esto incluiría definir los endpoints, los métodos HTTP (GET, POST, PUT, DELETE), y la estructura de los datos que se enviarán y recibirán.
Implementación de la Seguridad: Dado que las peticiones vendrán de un tercero (CarTrawler), implementaría un sistema de autenticación basado en tokens para asegurar que solo las solicitudes válidas sean procesadas. Esto implica la generación y verificación de tokens en cada solicitud.
Desarrollo de los Métodos en 4D: Paralelamente al desarrollo de las API's en Laravel, implementaría los métodos necesarios en el sistema 4D para procesar cada acción requerida por CarTrawler. Esto podría implicar la creación de nuevos objetos o métodos para manejar las operaciones de reserva.
Registro de Actividades: Implementaría un sistema de registro o log para almacenar un historial de todas las peticiones realizadas a las API's. Esto proporcionará un seguimiento de las actividades realizadas y será útil para fines de auditoría y solución de problemas.
Pruebas y Depuración: Antes de pasar a la fase de integración completa, realizaría pruebas exhaustivas de las API's y los métodos en 4D para asegurar su funcionalidad y fiabilidad. Esto incluiría pruebas unitarias, pruebas de integración y pruebas de aceptación.
Una vez completados estos pasos iniciales, procedería con la integración completa entre 4D y CarTrawler, realizando pruebas adicionales y ajustes según sea necesario para garantizar una integración exitosa y sin problemas.




Objetivos Específicos:
1. Desarrollar APIs de integración con CarTrawler para facilitar la gestión de reservas de vehículos:
Este objetivo implica la creación de interfaces de programación de aplicaciones (APIs) que permitan la comunicación entre el sistema de gestión de Car Rental y la plataforma de CarTrawler. Estas APIs deben ser diseñadas para ser eficientes, seguras y fáciles de usar.
   - Se requerirá un análisis exhaustivo de los requisitos de integración proporcionados por CarTrawler para asegurar que las API cumplan con sus estándares y permitan una comunicación fluida entre los sistemas.
   - El desarrollo de estas APIs debe incluir la implementación de funciones para agregar, actualizar y cancelar reservas de vehículos, así como para gestionar cualquier información adicional necesaria para el proceso de reserva.
   - Además del desarrollo de las APIs en sí, se deben establecer mecanismos para autenticar y autorizar las solicitudes de CarTrawler, lo que puede implicar el uso de tokens de seguridad u otros métodos de autenticación.



Integración 4D-CarTrawler:
Desarrollo de APIs utilizando Laravel para integrar Car Rental con CarTrawler.
Automatización de la gestión de reservas y comunicación bidireccional entre sistemas.
Uso de tokens para la autenticación y registro de peticiones.







******************************************************************************


Para implementar las APIs en Laravel y resolver el problema de integración entre 4D y CarTrawler, aquí te detallo cómo podrías hacerlo paso a paso:

### Paso 1: Análisis de Requisitos
- Revisa detalladamente la documentación proporcionada por CarTrawler para entender los requisitos de integración.
- Identifica los tipos de paquetes de arriendo de vehículos y las acciones a realizar: agregar, actualizar o anular reservas.
  
### Paso 2: Diseño de las API's
- Define los endpoints de la API que representarán las acciones a realizar (agregar, actualizar, anular reservas).
- Diseña la estructura de los datos que se enviarán y recibirán en cada endpoint.
  
### Paso 3: Implementación de la Seguridad
- Implementa un sistema de autenticación basado en tokens para validar las solicitudes de CarTrawler.
- Genera tokens para las solicitudes válidas y verifica estos tokens en cada petición recibida.

### Paso 4: Desarrollo de los Métodos en 4D
- Desarrolla los métodos en 4D que procesarán las acciones solicitadas a través de las API.
- Asegúrate de que estos métodos puedan manejar las operaciones de reserva (agregar, actualizar, anular).

### Paso 5: Registro de Actividades
- Implementa un sistema de registro o log para almacenar todas las actividades realizadas a través de las API.
  
### Paso 6: Pruebas y Depuración
- Realiza pruebas unitarias para cada endpoint de la API.
- Realiza pruebas de integración entre la API y el sistema 4D.
- Depura cualquier error o problema encontrado durante las pruebas.

### Ejemplo de Endpoint en Laravel para agregar una reserva:

```php
// routes/api.php
Route::post('/reservas', 'ReservaController@agregar');

// ReservaController.php
public function agregar(Request $request)
{
    // Validar la solicitud
    $request->validate([
        'id_vehiculo' => 'required|integer',
        'fecha_inicio' => 'required|date',
        'fecha_fin' => 'required|date',
        // Otros campos necesarios
    ]);

    // Crear la reserva en 4D
    $reserva = new Reserva();
    $reserva->id_vehiculo = $request->id_vehiculo;
    $reserva->fecha_inicio = $request->fecha_inicio;
    $reserva->fecha_fin = $request->fecha_fin;
    // Guardar la reserva
    $reserva->save();

    // Registrar la actividad
    Log::info('Reserva agregada', ['reserva' => $reserva]);

    // Retornar respuesta
    return response()->json(['message' => 'Reserva agregada con éxito', 'reserva' => $reserva], 201);
}
```

### Recursos recomendados para aprender Laravel y APIs:

1. **Cursos Online:**
   - [Laravel from Scratch](https://laracasts.com/series/laravel-6-from-scratch) en Laracasts.
   - [API Development with Laravel](https://www.udemy.com/course/laravel-api-development/) en Udemy.

2. **Documentación:**
   - [Laravel Documentation](https://laravel.com/docs).

3. **Videos en YouTube:**
   - "Laravel API Tutorial" o "Laravel API Development Tutorial".

4. **Búsqueda de Palabras Clave:**
   - "Laravel API development tutorial", "Laravel REST API tutorial", "Laravel authentication with tokens".

Espero que esta guía te sea útil para comenzar con el desarrollo de las APIs en Laravel para la integración con CarTrawler. ¡Buena suerte en tu proyecto!





Para la integración entre el sistema de gestión de Car Rental y CarTrawler, es probable que necesites implementar varios endpoints que permitan realizar diferentes acciones sobre las reservas de vehículos. Aquí te detallo algunos ejemplos de endpoints que podrías necesitar:

1. **Agregar Reserva**
   - `POST /reservas`: Agrega una nueva reserva de vehículo.

2. **Actualizar Reserva**
   - `PUT /reservas/{id}`: Actualiza una reserva existente identificada por su ID.

3. **Anular Reserva**
   - `DELETE /reservas/{id}`: Anula una reserva existente identificada por su ID.

4. **Obtener Detalles de Reserva**
   - `GET /reservas/{id}`: Obtiene los detalles de una reserva específica.

5. **Listar Reservas**
   - `GET /reservas`: Obtiene una lista de todas las reservas.

6. **Buscar Reservas por Fecha**
   - `GET /reservas?fecha_inicio={fecha}`: Filtra las reservas por fecha de inicio.

7. **Buscar Reservas por Vehículo**
   - `GET /reservas?vehiculo_id={id}`: Filtra las reservas por ID de vehículo.

8. **Confirmar Reserva**
   - `POST /reservas/{id}/confirmar`: Confirma una reserva pendiente.

9. **Cancelar Reserva**
   - `POST /reservas/{id}/cancelar`: Cancela una reserva confirmada.

10. **Verificar Disponibilidad de Vehículo**
    - `GET /vehiculos/disponibles`: Obtiene una lista de vehículos disponibles para reserva.

Estos son solo ejemplos generales y podrías necesitar ajustarlos según los requisitos específicos de tu proyecto y las necesidades de CarTrawler. Recuerda que cada endpoint debe ser seguro, eficiente y cumplir con los estándares RESTful para una integración exitosa.

Espero que esta lista te ayude a tener una idea clara de los endpoints que podrías necesitar implementar para tu proyecto de integración con CarTrawler.






Para desarrollar las APIs de integración con CarTrawler utilizando Laravel, necesitarás varios elementos clave que te ayudarán a estructurar y organizar tu código de manera efectiva. Aquí te detallo los principales elementos que necesitarás:

### Elementos Principales:

1. **Modelos**
   - **Reserva**: Representa la entidad de reserva de vehículos, con atributos como ID, fecha de inicio, fecha de fin, vehículo asignado, estado de la reserva, entre otros.
   - **Vehículo**: Representa la entidad de vehículo disponible para alquiler, con atributos como ID, marca, modelo, tipo, disponibilidad, etc.

2. **Controladores**
   - **ReservaController**: Maneja las acciones relacionadas con la gestión de reservas, como agregar, actualizar, anular, confirmar y cancelar reservas.
   - **VehiculoController**: Maneja las acciones relacionadas con la gestión de vehículos, como obtener la disponibilidad y detalles de los vehículos.

3. **Rutas**
   - Define las rutas para cada endpoint en el archivo `routes/api.php`. Por ejemplo:
     ```php
     Route::post('/reservas', 'ReservaController@store');
     Route::put('/reservas/{id}', 'ReservaController@update');
     Route::delete('/reservas/{id}', 'ReservaController@destroy');
     // ... otras rutas
     ```

4. **Migraciones**
   - Crea migraciones para definir la estructura de las tablas en la base de datos para Reservas y Vehículos. Las migraciones te permitirán mantener un registro de los cambios en tu esquema de base de datos.
   
5. **Peticiones (Requests)**
   - Utiliza peticiones para validar y sanitizar los datos de entrada antes de procesar las solicitudes en los controladores. Por ejemplo, una petición `StoreReservaRequest` para validar los datos al crear una nueva reserva.

6. **Servicios**
   - **CarTrawlerService**: Un servicio para manejar la comunicación con la API de CarTrawler, que incluye métodos para autenticarse, enviar solicitudes HTTP y procesar respuestas.

7. **Autenticación y Autorización**
   - Implementa un sistema de autenticación basado en tokens para validar las solicitudes entrantes de CarTrawler. Puedes utilizar paquetes como Laravel Passport para facilitar este proceso.

8. **Logs**
   - Configura un sistema de registro para registrar todas las actividades y errores relacionados con las solicitudes a las APIs. Laravel proporciona un potente sistema de registro integrado que puedes utilizar.

9. **Pruebas**
   - Desarrolla pruebas unitarias y de características para asegurar que tus endpoints funcionen como se espera y para identificar y corregir posibles problemas antes de la implementación en producción.

10. **Documentación**
    - Documenta tus APIs para proporcionar información detallada sobre cómo consumirlas, qué endpoints están disponibles, qué datos se esperan, etc. Puedes usar herramientas como Swagger o Postman para generar documentación interactiva de tus APIs.

Estos son los elementos principales que necesitarás para desarrollar las APIs de integración con CarTrawler en Laravel. A medida que avances en el desarrollo, es posible que necesites agregar o modificar algunos elementos según los requisitos específicos de tu proyecto y las necesidades de CarTrawler.



















Para implementar la autenticación basada en tokens en Laravel, puedes utilizar Laravel Passport, que es una biblioteca oficial que proporciona una implementación completa de OAuth2 para Laravel. A continuación, te muestro cómo puedes implementar tokens de acceso utilizando Laravel Passport en tu proyecto:

### Instalación de Laravel Passport

Primero, instala Laravel Passport a través de Composer:

```bash
composer require laravel/passport
```

### Configuración

Después de instalar el paquete, publica los archivos de configuración y migraciones con el siguiente comando:

```bash
php artisan passport:install
```

Este comando generará las claves de encriptación necesarias y creará las migraciones necesarias para Passport.

### Implementación

#### 1. Configuración de Passport

Una vez instalado, deberás agregar el `HasApiTokens` trait a tu modelo `User`. Si aún no tienes un modelo `User`, puedes crear uno utilizando el comando `php artisan make:model User`.

```php
use Laravel\Passport\HasApiTokens;

class User extends Authenticatable
{
    use HasApiTokens, Notifiable;
    // ...
}
```

#### 2. Definición de las rutas de autenticación

En tu archivo `routes/api.php`, define las rutas necesarias para la autenticación:

```php
Route::post('login', 'AuthController@login');
Route::post('register', 'AuthController@register');
```

#### 3. Controlador de Autenticación

Crea un controlador `AuthController` para manejar las solicitudes de inicio de sesión y registro:

```php
php artisan make:controller AuthController
```

En el controlador `AuthController`, implementa los métodos `login` y `register`:

```php
use App\User;
use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\Validator;

class AuthController extends Controller
{
    public function register(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:6|confirmed',
        ]);

        if ($validator->fails()) {
            return response(['errors' => $validator->errors()->all()], 422);
        }

        $data = $request->all();
        $data['password'] = bcrypt($data['password']);

        $user = User::create($data);
        $token = $user->createToken('MyApp')->accessToken;

        return response(['user' => $user, 'access_token' => $token]);
    }

    public function login(Request $request)
    {
        $data = $request->validate([
            'email' => 'required|string|email',
            'password' => 'required|string',
        ]);

        if (!Auth::attempt($data)) {
            return response(['message' => 'Invalid credentials']);
        }

        $token = Auth::user()->createToken('MyApp')->accessToken;

        return response(['user' => Auth::user(), 'access_token' => $token]);
    }
}
```

#### 4. Proteger rutas

Para proteger tus rutas y requerir autenticación, utiliza el middleware `auth:api`:

```php
Route::middleware('auth:api')->group(function () {
    Route::get('user', 'UserController@details');
    // otras rutas protegidas
});
```

Esto requerirá que el usuario envíe un token de acceso válido en la cabecera de la solicitud para acceder a las rutas protegidas.

### Ejemplo de uso del token

Una vez que un usuario se registra o inicia sesión con éxito, recibirás un token de acceso que deberás incluir en las cabeceras de tus solicitudes para acceder a las rutas protegidas:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Con esto, habrás implementado la autenticación basada en tokens en tu aplicación Laravel utilizando Laravel Passport.























Claro, aquí te proporciono un ejemplo más enfocado en tu caso de uso específico para la gestión de reservas de vehículos con CarTrawler.

### Endpoints de Reserva

1. **Crear una nueva reserva**

   ```
   POST /api/reservas
   ```
   
   Body de la solicitud:
   ```json
   {
       "vehiculo_id": 1,
       "fecha_inicio": "2024-05-01",
       "fecha_fin": "2024-05-10",
       "cliente_id": 1,
       "paquete": "Inclusive",
       "kilometros": 1000,
       "coberturas": "Básicas"
   }
   ```

2. **Actualizar una reserva existente**

   ```
   PUT /api/reservas/{id}
   ```
   
   Body de la solicitud:
   ```json
   {
       "fecha_inicio": "2024-05-02",
       "fecha_fin": "2024-05-12",
       "paquete": "Exclusive"
   }
   ```

3. **Obtener detalles de una reserva**

   ```
   GET /api/reservas/{id}
   ```

4. **Cancelar una reserva**

   ```
   DELETE /api/reservas/{id}
   ```

### Implementación de la Autenticación con Tokens

#### Modelo `User`

En tu modelo `User`, asegúrate de usar el trait `HasApiTokens` de Passport:

```php
use Laravel\Passport\HasApiTokens;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable
{
    use HasApiTokens, Notifiable;

    // ...
}
```

#### Controlador de Reservas (`ReservaController`)

Crea un controlador `ReservaController` para manejar las operaciones CRUD de las reservas:

```bash
php artisan make:controller ReservaController --api
```

```php
namespace App\Http\Controllers;

use App\Models\Reserva;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class ReservaController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth:api');
    }

    public function store(Request $request)
    {
        $data = $request->validate([
            'vehiculo_id' => 'required|integer|exists:vehiculos,id',
            'fecha_inicio' => 'required|date',
            'fecha_fin' => 'required|date',
            'cliente_id' => 'required|integer|exists:clientes,id',
            'paquete' => 'required|string|in:Inclusive,Exclusive',
            'kilometros' => 'required|integer',
            'coberturas' => 'required|string',
        ]);

        $reserva = Reserva::create($data);

        return response()->json($reserva, 201);
    }

    public function update(Request $request, $id)
    {
        $reserva = Reserva::findOrFail($id);

        $data = $request->validate([
            'fecha_inicio' => 'nullable|date',
            'fecha_fin' => 'nullable|date',
            'paquete' => 'nullable|string|in:Inclusive,Exclusive',
        ]);

        $reserva->update($data);

        return response()->json($reserva, 200);
    }

    public function show($id)
    {
        $reserva = Reserva::findOrFail($id);

        return response()->json($reserva);
    }

    public function destroy($id)
    {
        $reserva = Reserva::findOrFail($id);
        $reserva->delete();

        return response()->json(null, 204);
    }
}
```

Con esto, tendrás un conjunto básico de endpoints para la gestión de reservas de vehículos. Los usuarios deberán autenticarse con un token válido para acceder a estos endpoints protegidos.

Recuerda ajustar los modelos y las validaciones según las necesidades específicas de tu aplicación y realizar pruebas exhaustivas para asegurar su correcto funcionamiento.
![Captura de pantalla 2024-04-22 223645](https://github.com/josecanahuate/API-RESERVAS/assets/58529823/401ead3d-e24c-4644-be45-f1e682f70b5e)

