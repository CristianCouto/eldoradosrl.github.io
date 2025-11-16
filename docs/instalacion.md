# Instalación del Sistema 🤖 Chatbot RAG para El Dorado SRL

Este instructivo te guiará en la instalación y ejecución del chatbot RAG (Generación Aumentada por Recuperación) desarrollado para El Dorado S.R.L.
El chatbot te permitirá consultar información de la Wiki interna y de documentos PDF, utilizando un modelo de lenguaje grande (LLM) que se ejecuta localmente.

El sistema funciona en una PC local con LM Studio + Backend Flask + Frontend React.

---

## Requisitos del Sistema

### Hardware (Recomendado)

| Componente | Especificación sugerida |
|---|---|
| RAM | 16 GB |
| CPU | Ryzen 7 5000 series, Intel i5 o similar |
| GPU | Placa Gráfica dedicada |
| OS | Windows 10 / 11 |

### Software (Obligatorio)

* **[Python 3.10+](https://www.python.org/downloads/)**
* **[Node.js 18+](https://nodejs.org/en)** (incluyendo npm)
* **[LM Studio](https://lmstudio.ai/)**

#### Configuración del Modelo en LM Studio

1.  **Descargar el Modelo:**
    * Abre LM Studio y usa el buscador (pestaña 🏠) para encontrar y descargar el modelo recomendado: **`Meta-Llama-3-8B-Instruct-GGUF`**.
    * (Puedes ver detalles de este modelo [aquí](https://huggingface.co/lmstudio-community/Meta-Llama-3-8B-Instruct-GGUF)).

2.  **Configurar el archivo `.env`:**
    * En la raíz del proyecto, encontrarás un archivo `.env` que le indica al backend (Python) qué modelo debe usar.
    * Las líneas relevantes son:
        ```env
        # Modelo a usar en LM Studio (asegúrate que coincida)
        LLM_MODEL_NAME="Meta-Llama-3-8B-Instruct"
        ```
    * **¡Importante!** Nota que el nombre en el `.env` (línea 22) **no** incluye el sufijo `-GGUF`. El script está configurado para usar el string `Meta-Llama-3-8B-Instruct`.

#### Opcional: Cambiar de Modelo

Puedes optar por usar un modelo diferente al recomendado.

* **Modelos más potentes (ej. 70B):** Darán respuestas más precisas y coherentes, pero requerirán una GPU muy potente y mucha RAM, y serán más lentos.
* **Modelos más pequeños (ej. 3B):** Serán mucho más rápidos y consumirán menos recursos, pero la calidad de la respuesta puede ser inferior.

Si descargas un modelo diferente, **debes actualizar la línea 22** del archivo `.env` para que el valor `LLM_MODEL_NAME` coincida **exactamente** con el "Model Name" que LM Studio espera.

---

## 1. Primera Instalación (Configuración Única)

Sigue estos pasos **solo la primera vez** que configures el sistema en una nueva computadora.

### Paso 1.1: Clonar el Repositorio

Abre una terminal (Git Bash, Símbolo del sistema, etc.) y clona el proyecto:

```bash
git clone [https://github.com/santiagooroz-equipo1-pp2-eldorado-2c-2025.git](https://github.com/santiagooroz-equipo1-pp2-eldorado-2c-2025.git)
cd santiagooroz-equipo1-pp2-eldorado-2c-2025
````

### Paso 1.2: Configuración del Backend (Raíz)

En la raíz del proyecto, crea un entorno virtual e instala las dependencias de Python.

1.  Crear entorno virtual:

    ```bash
    python -m venv venv
    ```

2.  Activar entorno virtual:

      * En Windows: `venv\Scripts\activate`
      * En macOS/Linux: `source venv/bin/activate`

3.  Instalar dependencias:

    ```bash
    pip install -r requirements.txt
    ```

### Paso 1.3: Configuración del Frontend

1.  Navega a la carpeta del frontend:
    ```bash
    cd frontend
    ```
2.  Instala las dependencias de Node.js:
    ```bash
    npm install
    ```
3.  Regresa a la carpeta raíz:
    ```bash
    cd ..
    ```

### Paso 1.4: Indexación Inicial (¡Importante\!)

Antes de iniciar la aplicación por primera vez, debes generar la base de datos vectorial (ChromaDB).

  * Asegúrate de estar en la **raíz del proyecto** (`santiagooroz-equipo1-pp2-eldorado-2c-2025`).

  * Asegúrate de que tu **entorno virtual** (`venv`) esté activado.

  * Ejecuta el script de indexación:

    ```bash
    python indexing.py
    ```

Esto leerá los archivos de `data/pdfs` y la Wiki, generará los *embeddings* y los guardará en la base de datos vectorial (`data/chroma_db_v...`).

-----

## 2\. Ejecución Normal (Uso Diario)

Una vez completada la instalación, sigue estos pasos para usar el chatbot.

### Paso 2.1: Iniciar el Servidor de Modelos (LM Studio)

1.  Abre LM Studio.
2.  Ve a la pestaña del servidor local (ícono `<>`).
3.  Selecciona el modelo que descargaste (ej. `Meta-Llama-3-8B-Instruct-GGUF`).
4.  Haz clic en **Start Server** (Iniciar Servidor).
5.  Asegúrate de que el servidor esté activo en `http://localhost:1234`.

### Paso 2.2: Iniciar el Backend y Frontend

Hemos incluido scripts para facilitar el inicio simultáneo del backend (Flask) y el frontend (React).

  * **En Windows:**
    Haz doble clic en el archivo:
    `iniciar_chatbot.bat`

  * **En macOS/Linux:**
    Ejecuta en la terminal:

    ```bash
    chmod +x mac-linux-iniciar.command
    ./mac-linux-iniciar.command
    ```

Esto iniciará ambos servicios y abrirá automáticamente la página web del chatbot (`http://localhost:3000`) en tu navegador.

 **Método Alternativo (Manual):**
 Si los scripts fallan, puedes iniciar los servicios manualmente en dos terminales separadas (ambas en la raíz del proyecto y con `venv` activado):

 1.  **Terminal 1 (Backend):**
      ```bash
      python app.py
      ```
 

 2.  **Terminal 2 (Frontend):**
     ```bash
     cd frontend
     npm start
     ```

-----

## 3\. Interacción con el Chatbot

Una vez que la aplicación esté abierta en tu navegador:

### 3.1. Realizar Consultas 💬

1.  En la parte derecha de la pantalla, verás el panel de chat.
2.  Escribe tu consulta en la burbuja de texto de la parte inferior.
      * **Nota:** La primera consulta puede tardar significativamente más tiempo que las siguientes, ya que el modelo se está inicializando.
3.  Presiona el botón de **Enviar** (la flechita) ➡️.

### 3.2. Opción de Voz 🎙️

1.  Puedes usar el botón del micrófono 🎙️ a la derecha.
2.  Al presionarlo por primera vez, se te pedirá permiso para usar el micrófono (selecciona **Aceptar**).
3.  Habla tu consulta.
4.  Vuelve a presionar el botón del micrófono para finalizar la grabación.
5.  Tu voz se transcribirá en la burbuja de consulta. Puedes editar o añadir texto si es necesario.
6.  Presiona **Enviar** ➡️.

### 3.3. Escuchar Respuesta y Ver Fuentes

1.  **Escuchar Respuesta:** Una vez que el modelo responda, verás un botón de altavoz 🔊 debajo de su respuesta. Púlsalo para escuchar la respuesta.
2.  **Fuentes:** Más abajo, se listarán las fuentes utilizadas (PDFs o Wiki) para generar la respuesta.
3.  **Limpiar:** El botón "Limpiar" 🗑️ elimina el historial de chat de la vista del usuario.

-----

## 4\. Gestión de Archivos (Administradores)

El panel de la izquierda ("Gestión de Archivos") permite administrar la información a la que el chatbot tiene acceso. Esta sección es solo para administradores.

1.  **Acceso al Panel:**

      * Ingresa la clave técnica en el formulario (parte superior izquierda, bajo el logo) y haz clic en "Acceder".

2.  **Administración del Conocimiento:**

      * Desde aquí podrás ver los archivos PDF cargados y forzar una re-indexación de la base de conocimiento si se realizan cambios.
        
        <img width="549" height="723" alt="Panel de administración del chatbot" src="https://github.com/user-attachments/assets/76d72499-26cc-494b-b06c-cb020317ddd7" />
