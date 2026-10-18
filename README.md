# Rincón Provincia Ubatense: Entre Montañas y Leyendas

**Plataforma web de promoción turística con asistente conversacional bilingüe basado en inteligencia artificial.**

[![Laravel](https://img.shields.io/badge/Laravel-Backend-red)](https://laravel.com/)
[![PHP](https://img.shields.io/badge/PHP-8.2-blue)](https://www.php.net/)
[![MySQL](https://img.shields.io/badge/MySQL-Database-orange)](https://www.mysql.com/)
[![Gemini](https://img.shields.io/badge/AI-Gemini-blueviolet)](https://ai.google.dev/)

## 1. Descripción del proyecto

Rincón Provincia Ubatense: Entre Montañas y Leyendas es una plataforma web desarrollada para promover el turismo de la provincia de Ubaté, Cundinamarca, Colombia. Su propósito es facilitar el acceso a información sobre destinos turísticos, gastronomía, hospedajes, glamping y lugares de interés religioso y cultural de los municipios de la región.

El proyecto integra un asistente conversacional inteligente que utiliza la API de Gemini para interpretar preguntas en lenguaje natural y generar respuestas basadas en la información turística registrada en la base de datos de la aplicación.

El chatbot permite realizar consultas en español e inglés, de acuerdo con el idioma utilizado por el usuario. De esta manera, la plataforma busca mejorar el acceso a la información turística y facilitar el descubrimiento de lugares de interés.

## 2. Objetivos

### Objetivo general

Desarrollar un aplicativo web que permita la gestión y visualización de información sobre lugares turísticos, hospedajes y gastronomía acerca de los 10 municipios que conforman la provincia de Ubaté. 
### Objetivos específicos

- Analizar la información turística, geográfica y comercial de los diez municipios de 
la provincia de Ubaté mediante el levantamiento de datos estructurados, garantizando su 
compatibilidad con el esquema de almacenamiento del sistema. 
- Diseñar la arquitectura del software, la interfaz de usuario y el modelo relacional de 
la base de datos con módulos de RA, geolocalización e itinerarios, asegurando la 
escalabilidad y la correcta navegación dentro del aplicativo web. 
- Implementar los módulos funcionales del aplicativo web (y validar su desempeño 
mediante pruebas de usabilidad y rendimiento, logrando un porcentaje de efectividad 
superior al 90% en la consulta de información turística.

## 3. Alcance del proyecto

La plataforma está orientada a turistas nacionales y a emprendedores del sector turístico interesados en la promoción de destinos y servicios de la provincia de Ubaté.

Los municipios contemplados en el proyecto son:

- Carmen de Carupa
- Cucunubá
- Fúquene
- Guachetá
- Lenguazaque
- Simijaca
- Susa
- Sutatausa
- Tausa
- Ubaté

Las categorías turísticas incluyen:

- Lugares turísticos y naturaleza.
- Restaurantes y gastronomía.
- Turismo religioso.
- Hospedajes.
- Glamping.

El asistente conversacional complementa la plataforma al permitir que los usuarios consulten la información disponible mediante preguntas escritas.

## 4. Tecnologías utilizadas

| Tecnología | Función |
|---|---|
| Laravel | Framework para la lógica del servidor y la organización de la aplicación. |
| PHP | Lenguaje de programación del backend. |
| MySQL | Almacenamiento de usuarios y registros turísticos. |
| Blade | Motor de plantillas utilizado por Laravel. |
| HTML, CSS y JavaScript | Estructura, estilos e interactividad de la interfaz. |
| Bootstrap | Apoyo al diseño adaptable de la interfaz, donde está integrado. |
| Gemini API | Generación de respuestas conversacionales contextualizadas. |
| Git y GitHub | Control de versiones y alojamiento del código fuente. |
| XAMPP | Entorno utilizado para el desarrollo local. |

## 5. Arquitectura del sistema

El sistema sigue una arquitectura web en la que Laravel gestiona las solicitudes, accede a los datos y se comunica con el proveedor de inteligencia artificial.

### Componentes principales

**Interfaz del chatbot:** permite al usuario escribir preguntas y visualizar las respuestas generadas.

**ChatbotController:** recibe las solicitudes del usuario, valida la pregunta y obtiene los registros turísticos que se utilizarán como contexto.

**Modelo Place:** representa los lugares turísticos almacenados en la base de datos.

**Base de datos MySQL:** almacena la información estructurada que utiliza la aplicación.

**GeminiService:** prepara las instrucciones, construye la solicitud a la API de Gemini y procesa la respuesta.

**Gemini API:** interpreta la pregunta junto con el contexto proporcionado y genera una respuesta en lenguaje natural.

### Flujo de funcionamiento

1. El usuario escribe una pregunta en el chatbot.
2. La interfaz envía la pregunta al backend de Laravel.
3. `ChatbotController` valida la solicitud.
4. El controlador consulta los registros turísticos mediante el modelo `Place`.
5. `GeminiService` construye el prompt con la pregunta y el contexto recuperado.
6. La solicitud se envía a Gemini mediante la API.
7. La respuesta se devuelve a la interfaz para que el usuario pueda leerla.

**Representación de la arquitectura:**

Usuario → Interfaz web → ChatbotController → Modelo Place y MySQL → GeminiService → Gemini API → Respuesta al usuario.

## 6. Base de conocimiento

La base de conocimiento inicial está constituida por la información turística estructurada y almacenada en MySQL.

Entre los campos utilizados para describir los lugares se encuentran:

- Nombre.
- Descripción.
- Municipio.
- Categoría o tipo de lugar.

El controlador obtiene los registros turísticos y los transforma en un contexto textual que se incorpora a la solicitud enviada a Gemini.

Este enfoque permite que el asistente utilice información específica del proyecto en lugar de depender exclusivamente del conocimiento general del modelo de lenguaje.

### Limitaciones de la base de conocimiento

La precisión de las respuestas depende de la calidad, actualidad y disponibilidad de los registros almacenados.

Si un precio, horario, contacto o característica no está registrado en el contexto suministrado, el chatbot debe indicar que no dispone de esa información, en lugar de inventarla.

La implementación descrita utiliza una base de datos relacional como fuente de conocimiento y contexto incorporado al prompt. No se afirma que utilice embeddings, una base de datos vectorial o un sistema RAG avanzado, puesto que estos componentes no forman parte de la implementación actual documentada.

## 7. Integración con Gemini API

La integración se realiza desde el servicio `App\Services\GeminiService`, responsable de comunicarse con Gemini.

El servicio utiliza la clave API y el modelo configurados mediante variables de entorno y el archivo `config/services.php`.

La solicitud contiene las instrucciones del chatbot, la información turística recuperada y la pregunta del usuario. Gemini procesa estos elementos y devuelve una respuesta que Laravel entrega al frontend.

### Manejo de errores

La integración contempla el manejo de respuestas fallidas y errores de comunicación. También incluye reintentos para ciertos errores temporales, como los relacionados con indisponibilidad del servicio o límites de solicitudes.

Si la API no puede proporcionar una respuesta, la aplicación debe comunicar el problema de forma controlada, sin mostrar claves secretas ni información sensible.

La disponibilidad del chatbot depende de la conectividad, la configuración de la API, las condiciones de uso del proveedor y los límites de la cuenta.

## 8. Prompt Engineering

El chatbot utiliza instrucciones explícitas para definir su propósito y restringir el tipo de respuestas que puede generar.

### Propósito del System Prompt

El asistente se presenta como un orientador turístico virtual de Rincón Provincia Ubatense: Entre Montañas y Leyendas.

Sus instrucciones principales son:

- Detectar el idioma de la pregunta y responder en el mismo idioma.
- Responder en español cuando la consulta esté en español.
- Respond in English when the user asks in English.
- Utilizar la información turística suministrada en el contexto.
- No inventar destinos, restaurantes, hoteles, precios, horarios ni datos.
- Indicar claramente cuando la información solicitada no está disponible.
- Mantener respuestas claras, breves y relacionadas con el turismo.
- Utilizar los datos correspondientes al municipio o categoría consultados.
- Recomendar únicamente lugares presentes en la información proporcionada.

### Prevención de respuestas no fundamentadas

Las instrucciones del prompt buscan reducir las respuestas inventadas mediante la delimitación del dominio y el uso de información contextual.

Sin embargo, las instrucciones por sí solas no garantizan la eliminación absoluta de errores. Por ello, es importante realizar pruebas con preguntas sin respuesta, solicitudes ambiguas y consultas que incluyan datos no registrados.

## 9. Funcionalidades del proyecto

- Consulta de información turística.
- Organización de destinos por municipio y categoría.
- Interacción con un asistente conversacional integrado en la interfaz.
- Consultas mediante lenguaje natural.
- Respuestas en español e inglés.
- Uso de registros turísticos como contexto para la generación de respuestas.
- Validación de las preguntas recibidas por el backend.
- Manejo de errores de comunicación con el servicio de inteligencia artificial.

Las funcionalidades descritas corresponden al alcance implementado y deben ampliarse únicamente cuando las nuevas características se desarrollen y prueben.

## 10. Instalación y ejecución local

### Requisitos previos

- PHP compatible con la versión de Laravel del proyecto.
- Composer.
- MySQL.
- XAMPP u otro entorno compatible.
- Una clave API válida de Gemini.
- Node.js y npm, si el proyecto requiere instalar o compilar recursos frontend.

### Paso 1. Clonar el repositorio

```bash
https://github.com/sutajazmar-hub/RINCON-PROVINCIA-UBATENSE-MACHINE-LEARNING.git
```

Ingresar a la carpeta del proyecto:

```bash
cd PGC
```


### Paso 2. Instalar dependencias

```bash
composer install
```

### Paso 3. Configurar el archivo de entorno

Copiar `.env.example` y crear el archivo `.env`.

En Windows puede hacerse manualmente desde el explorador de archivos o mediante la terminal.

### Paso 4. Generar la clave de Laravel

```bash
php artisan key:generate
```

### Paso 5. Configurar la base de datos

Crear una base de datos MySQL y configurar las variables correspondientes en `.env`.

Ejemplo:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=pageweb
DB_USERNAME=root
DB_PASSWORD=
```

### Paso 6. Configurar Gemini

Agregar las variables de entorno:

```env
GEMINI_API_KEY=tu_clave_api
GEMINI_MODEL=gemini-3.6-flash
```

El nombre del modelo debe coincidir con el que esté configurado y disponible para la cuenta utilizada.

**Seguridad:** no publicar la API Key, el archivo `.env` ni las credenciales de la base de datos.

### Paso 7. Preparar la base de datos

Ejecutar las migraciones: 

```bash
php artisan migrate
```

Los registros turísticos existentes deben cargarse mediante los seeders, archivos de importación o procedimientos de respaldo correspondientes. Ejecutar las migraciones no garantiza que los lugares ya registrados se creen automáticamente.

### Paso 8. Instalar recursos frontend si es necesario

Si el proyecto utiliza un proceso de compilación con npm:

```bash
npm install
npm run build
```

### Paso 9. Iniciar Laravel

```bash
php artisan serve
```

Abrir en el navegador la dirección local indicada por Laravel, normalmente:

`http://127.0.0.1:8000`

## 11. Seguridad y buenas prácticas

El proyecto debe mantener las credenciales fuera del repositorio y utilizar variables de entorno para los datos sensibles.

Se recomienda:

- Mantener `.env` excluido mediante `.gitignore`.
- No incorporar claves API directamente en el código.
- Validar las entradas recibidas por el backend.
- Gestionar de manera controlada los errores de la API.
- Evitar que los mensajes de error revelen credenciales o detalles sensibles.
- Configurar credenciales independientes para producción.
- Revisar los permisos de acceso a las funciones de la aplicación.
- Verificar que las dependencias se encuentren instaladas y actualizadas.

## 12. Pruebas del chatbot

Las pruebas permiten verificar el funcionamiento de la integración y la calidad de las respuestas.

| Prueba | Resultado esperado |
|---|---|
| Pregunta turística en español | Respuesta en español basada en el contexto. |
| Pregunta turística en inglés | Respuesta en inglés basada en el contexto. |
| Consulta sobre un municipio | Información correspondiente a los registros disponibles de ese municipio. |
| Solicitud de recomendación | Recomendaciones limitadas a los lugares suministrados. |
| Pregunta sobre un dato inexistente | Indicación de que la información no está disponible. |
| Pregunta vacía | Rechazo mediante la validación del backend. |
| Error temporal de Gemini | Mensaje controlado sin exponer información sensible. |
| Pregunta fuera del ámbito turístico | Respuesta que mantiene el propósito y las restricciones del asistente. |


## 13. Declaración de la Persona Transhumana de la Universidad de Cundinamarca

### 13.1. Relación con el proyecto

La Declaración de la Persona Transhumana de la Universidad de Cundinamarca plantea compromisos relacionados con la autonomía, la responsabilidad, el desarrollo personal, el cuidado de la vida, la transformación positiva y la convivencia armónica.

En Rincón Provincia Ubatense, estos compromisos se relacionan con el desarrollo de tecnología orientada al servicio de las personas y al acceso al conocimiento de la región.

El chatbot se plantea como una herramienta de apoyo que facilita la consulta de información turística, pero no reemplaza la autonomía ni el criterio de los usuarios. La persona conserva la responsabilidad de evaluar la información y tomar sus propias decisiones.

Asimismo, la plataforma puede contribuir a la difusión del patrimonio natural, cultural y gastronómico de los municipios, siempre que la información sea presentada de manera responsable y se mantenga actualizada.

### 13.2. Reflexión en español

**¿De qué manera el agente/chatbot respeta y fomenta los principios de la Declaración de la Persona Transhumana de la Universidad de Cundinamarca en el contexto del aprendizaje y la interacción tecnológica?**

El chatbot de Rincón Provincia Ubatense se relaciona con la Declaración de la Persona Transhumana porque busca utilizar la tecnología como una herramienta para el aprendizaje, el desarrollo personal y el servicio a la comunidad. Su propósito no consiste únicamente en generar respuestas mediante inteligencia artificial, sino en facilitar el acceso a información turística de la provincia de Ubaté y contribuir al reconocimiento de sus municipios, sus lugares de interés y sus actividades económicas y culturales.

Uno de los principios que se relaciona con el proyecto es la autonomía. El asistente permite que cada usuario formule sus propias preguntas, explore diferentes destinos y utilice la información disponible para tomar decisiones de acuerdo con sus intereses. La herramienta orienta al usuario, pero no pretende decidir por él ni reemplazar su capacidad de análisis.

También se relaciona con la responsabilidad y la ética en el uso de la tecnología. El prompt del chatbot establece que las respuestas deben basarse en la información turística suministrada y que no se deben inventar lugares, precios, horarios ni otros datos. Cuando la información no está disponible, el asistente debe reconocer esa limitación. Esta decisión busca promover una interacción más transparente y recordar que las respuestas generadas por inteligencia artificial deben evaluarse de manera crítica.

Otro aspecto importante es la transformación positiva del entorno. Al centralizar información sobre los destinos turísticos, la plataforma puede ayudar a los visitantes a descubrir lugares de la región y favorecer la visibilidad de las iniciativas turísticas locales. Su valor social depende de que la información se mantenga actualizada, se presente con respeto y contribuya a una relación responsable con las comunidades y el entorno natural.

Finalmente, la posibilidad de realizar consultas en español e inglés busca facilitar el acceso a la información a personas con diferentes necesidades lingüísticas. Desde esta perspectiva, la inteligencia artificial funciona como un recurso de apoyo al conocimiento y a la comunicación. Sin embargo, su uso debe estar acompañado de supervisión humana, revisión de los datos y reconocimiento de sus limitaciones. De esta manera, el proyecto se aproxima a los principios de autonomía, responsabilidad, aprendizaje y transformación positiva promovidos por la Declaración de la Persona Transhumana.

### 13.3. Reflection in English

**How does the implemented AI agent/chatbot align with and support the Transhuman Person Declaration of Universidad de Cundinamarca regarding ethical AI integration, human augmentation, and educational transformation?**

The Rincón Provincia Ubatense chatbot relates to the Transhuman Person Declaration of Universidad de Cundinamarca because it uses technology as a tool for learning, personal development, and service to the community. Its purpose is not simply to generate answers through artificial intelligence, but to make tourism information about the Ubaté Province more accessible and help users discover the region's municipalities, attractions, cultural activities, and local services.

One important principle connected to this project is autonomy. The chatbot allows users to ask their own questions, explore different destinations, and use the available information to make decisions according to their interests. The assistant provides guidance, but it does not make decisions on behalf of users or replace their ability to think critically.

The project also relates to responsibility and ethical technology use. The chatbot's prompt instructs the model to rely on the tourism information provided and not to invent places, prices, schedules, or other facts. When information is unavailable, the assistant should acknowledge this limitation. This approach aims to encourage transparency and remind users that AI-generated responses should be evaluated critically.

Another relevant principle is positive transformation of the surrounding community. By organizing tourism information in one platform, the project may help visitors discover destinations across the region and increase the visibility of local tourism initiatives. Its social value depends on maintaining accurate information, presenting it respectfully, and encouraging responsible relationships with local communities and the natural environment.

Finally, allowing users to ask questions in Spanish and English can improve access to information for people with different language needs. From this perspective, artificial intelligence becomes a resource that supports knowledge and communication. However, its use should remain accompanied by human oversight, data verification, and awareness of its limitations. In this way, the project supports the principles of autonomy, responsibility, learning, and positive transformation promoted by the Transhuman Person Declaration.

## 14. Despliegue de la aplicación

**Estado actual:** desarrollo y pruebas locales mediante XAMPP.

- **Repositorio GitHub:** https://github.com/sutajazmar-hub/RINCON-PROVINCIA-UBATENSE-MACHINE-LEARNING.git
- **Aplicación en producción:** pendiente de despliegue.
- **URL pública:** agregar cuando el despliegue se encuentre disponible y haya sido probado.

Para realizar el despliegue es necesario configurar un entorno compatible con Laravel, variables de entorno seguras, una base de datos accesible, los registros turísticos necesarios y el acceso a Gemini API.


## 15. Trabajo futuro

Entre las posibles mejoras del proyecto se encuentran:

- Optimizar la recuperación de registros para enviar a Gemini únicamente la información relevante para cada consulta.
- Incorporar mecanismos adicionales de evaluación de las respuestas.
- Mejorar la actualización y administración de la información turística.
- Ampliar las pruebas de seguridad, rendimiento y accesibilidad.
- Evaluar técnicas de recuperación aumentada por generación (RAG) si el crecimiento de la base de conocimiento lo requiere.
- Desplegar la aplicación en un servicio en la nube.
- Incorporar mejoras de experiencia de usuario para visitantes y emprendedores.

Estas mejoras se consideran posibilidades futuras y no funcionalidades implementadas hasta que se desarrollen y verifiquen.

## 16. Referencias

Google. (s. f.). *Gemini API documentation*. https://ai.google.dev/gemini-api/docs

Laravel. (s. f.). *Laravel documentation*. https://laravel.com/docs

Universidad de Cundinamarca. (2022, 24 de agosto). *Declaración persona transhumana*. https://www.ucundinamarca.edu.co/index.php/noticias-ucundinamarca/120-rectoria/3816-declaracionpersonatranshumana

## 17. Autores

Proyecto académico desarrollado en el contexto del programa de Ingeniería de Sistemas y Computación de la Universidad de Cundinamarca.

**Proyecto:** Rincón Provincia Ubatense: Entre Montañas y Leyendas.

**Creadoras de oportunidades:** Eiddy Estefanía Paez Rincón y Lizeth Jazbleidy Suta Martinez

**Repositorio:** https://github.com/sutajazmar-hub/RINCON-PROVINCIA-UBATENSE-MACHINE-LEARNING.git 

**Aplicación publicada:** [Agregar enlace cuando esté desplegada].

