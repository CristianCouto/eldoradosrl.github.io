# Instalación del Sistema

El sistema funciona en una PC local con LM Studio + Backend Flask + Frontend React.

---

## Requisitos recomendados

| Componente | Especificación sugerida |
|---|---|
| RAM | 32 GB |
| CPU | Ryzen 7 5700G o similar |
| GPU | Placa Gráfica dedicada |
| OS | Windows 10 / 11 |

---

## Paso 1: Configuración Inicial (Servidor y Aplicación)
Antes de usar el chatbot, debes iniciar los servicios locales.

 1. Iniciar el Servidor de Modelos (LM Studio):
   * Abre LM Studio.
   * En la parte inferior derecha, haz clic en el modo Developer (Desarrollador).
   * Ve a la pestaña 🌐 LM Runtimes o a la pestaña del desarrollador (ícono de terminal).
   * Asegúrate de que el Status: Running esté encendido (botón verde). El script de Python usará esta instancia en localhost:1234 automáticamente.
    
2. Iniciar el Backend (Lógica del Chatbot):
   * Abre una terminal (Símbolo del sistema, PowerShell o Terminal).
   * Ejecuta el archivo principal del programa desde la raíz del proyecto:
         **python app.py**

3. Iniciar el Frontend (Interfaz Web):
   * Abre una nueva terminal y navega a la carpeta /frontend dentro de la raíz del proyecto:
         **cd frontend**
   * Ejecuta el comando para iniciar la interfaz web:
         **npm start**
   * Esto abrirá automáticamente la página web del chatbot en tu navegador.
     
---

## Paso 3: Interacción con el Chatbot
   💬 Realizar Consultas
   
1. En la parte derecha de la pantalla, verás el panel de chat.
   
2. Escribe tu consulta en la burbuja de texto de la parte inferior.
   * Nota: La primera consulta puede tardar significativamente más tiempo que las siguientes, ya que en este punto el modelo se estará inicializando.
     
3. Opción de Voz: Alternativamente, puedes usar el botón del micrófono 🎙️ a la derecha.
   * Al presionarlo por primera vez, se te pedirá permiso para usar el micrófono (selecciona Aceptar).
   * Habla tu consulta.
   * Vuelve a presionar el botón del micrófono para finalizar la grabación.
   * Tu voz se transcribirá en la burbuja de consulta. Puedes editar o añadir texto si es necesario.
     
4. Presiona el botón de Enviar (la flechita) ➡️ para que el modelo procese la consulta.
   
5. Escuchar Respuesta: Una vez que el modelo responda, verás un botón de altavoz 🔊 debajo de su respuesta. Púlsalo para escuchar la respuesta en voz humana
 
6. Fuentes: Más abajo, se listarán las fuentes utilizadas (tanto de los PDF como de la Wiki) para generar la respuesta.
 
7. El botón "Limpiar" 🗑️ elimina las consultas y respuestas hechas de la vista del usuario.

---

## Paso 3: Gestión de Archivos y Base de Conocimiento

El panel de la izquierda ("Gestión de Archivos") permite administrar la información a la que el chatbot tiene acceso. Pensada únicamente para que tengan acceso los admins. Usuarios comunes no tienen necesidad de entrar.

1. Acceso al Panel:
   * Al principio, el panel estará oculto, ingresa la clave técnica en el formulario (parte superior izquierda, bajo el logo) y haz clic en "Acceder" .
     
2. Administración del Conocimiento:

















