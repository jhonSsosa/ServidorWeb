# Servidor Web con Java

## 1. Instalación

### Prerrequisitos

Para ejecutar este proyecto, necesitas tener instalado lo siguiente:

- **Java JDK 11** o superior
- **Apache Maven** (opcional, si deseas manejar dependencias)
- **Un IDE de Java** (IntelliJ IDEA, Eclipse o VS Code con soporte para Java)

### Clonar el repositorio

```sh
git clone https://github.com/jhonSsosa/ServidorWeb.git
cd WebProyect
```

### Compilación y ejecución manual

Si deseas compilar y ejecutar manualmente sin Maven:

```sh
javac -d out -sourcepath src src/com/mycompany/webproyect/*.java
java -cp out com.mycompany.webproyect.HTTPServer
```

Si deseas compilar con Maven:

```sh
mvn clean compile exec:java
```

---

## 2. Ejecución

### Iniciar el servidor

```sh
java -cp out com.mycompany.webproyect.HTTPServer
```

El servidor se iniciará en el puerto **35000**.

### Acceder al servidor

Una vez iniciado, puedes acceder desde tu navegador en:

```
http://localhost:35000
```

Para probar la obtención de archivos, introduce el nombre de un archivo en el formulario y presiona **Submit**.

---

## 3. Arquitectura del Prototipo

### Descripción General

Este servidor web simple implementa un mecanismo para recibir solicitudes HTTP y servir archivos estáticos desde la carpeta **resources**. Se implementa sin frameworks web como Spring o Spark, utilizando únicamente Java y las clases de red de `java.net`.

### Componentes

#### 1. `HTTPServer.java`
- Inicia el servidor en el puerto 35000.
- Acepta solicitudes **GET** y las redirige a `FileController`.
- Construye la respuesta HTTP y la envía al cliente.

#### 2. `FileController.java`
- Maneja la lectura de archivos desde `resources`.
- Determina el tipo MIME adecuado (HTML, CSS, imágenes, etc.).
- Devuelve el contenido del archivo solicitado o un **error 404** si no existe.

#### 3. Recursos estáticos (`resources/`)
- Contiene archivos HTML, CSS e imágenes que el servidor entrega al cliente.
- **Ejemplo:** `index.html`, `style.css`, `image.jpg`.

### Esquema de comunicación

1. El cliente envía una solicitud **GET** a `/getfile?file=nombre.html`.
2. El servidor busca el archivo en **resources**.
3. Si el archivo existe, se envía con el tipo MIME correspondiente.
4. Si no existe, devuelve un **error 404**.

---

## 4. Evaluación y Pruebas

### Pruebas realizadas

#### 1. Prueba de acceso a archivos estáticos
- **Caso esperado:** Al solicitar `index.html`, el servidor responde con su contenido.
- **Resultado obtenido:** Se visualiza correctamente en el navegador.

#### 2. Prueba de solicitudes con diferentes archivos
- Se probaron archivos como `style.css`, `image.jpg` y `script.js`.
- **Resultado:** Se enviaron correctamente con sus respectivos tipos MIME.

#### 3. Prueba de error 404
- Se probó solicitando un archivo inexistente.
- **Resultado esperado:** `Error 404 - Archivo no encontrado`.
- **Resultado obtenido:** Mensaje de error correcto devuelto por el servidor.

### Prueba con cliente Java (invocación REST)

Se utilizó una prueba en Java para invocar el servidor:

```java
URL url = new URL("http://localhost:35000/index.html");
HttpURLConnection con = (HttpURLConnection) url.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
System.out.println("Código de respuesta: " + responseCode);
```

**Resultados:** Se obtuvo el código **200** y la respuesta con el contenido HTML esperado.

---

## 5. Conclusión

El servidor web cumple con la funcionalidad básica de servir archivos estáticos y responder a solicitudes **GET**. Se ha probado su funcionalidad con archivos **HTML, CSS e imágenes**, asegurando su correcto funcionamiento.
