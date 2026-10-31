# neryp_bot — Streamlit + Google Drive

Aplicación que transforma una URL pública en cinco imágenes editoriales para Instagram (1080 × 1350 px, 4:5). Cada lámina se sube a Google Drive inmediatamente después de generarse.

## Instalación local

```powershell
python -m venv .venv
.venv\\Scripts\\activate
pip install -r requirements.txt
```

## Configuración de Streamlit Secrets

En Streamlit Community Cloud: **App → Settings → Secrets**. Agrega:

```toml
OPENAI_API_KEY = "tu_api_key_de_openai"

[google_drive]
client_id = "CLIENT_ID_DE_GOOGLE"
client_secret = "CLIENT_SECRET_DE_GOOGLE"
refresh_token = "REFRESH_TOKEN_DE_GOOGLE"
folder_id = "1pCEHZRJ4104-EtpDAgWz4LpNpWfpkmPS"
```

No publiques estos valores en GitHub ni los compartas. El archivo `secrets.toml` real no debe subirse al repositorio.

## Preparar OAuth de Google Drive (una sola vez)

1. En Google Cloud Console crea o selecciona un proyecto.
2. Habilita **Google Drive API**.
3. Configura la pantalla de consentimiento OAuth y crea un cliente OAuth de tipo **Aplicación web** (o tipo apropiado para tu flujo de obtención del token).
4. Para obtener el refresh token, utiliza un flujo OAuth de usuario con acceso sin conexión (`access_type=offline`) y el alcance `https://www.googleapis.com/auth/drive`. Autoriza con la misma cuenta que tiene la carpeta compartida contigo.
5. Copia el Client ID, Client Secret y Refresh Token en Streamlit Secrets, dentro de `[google_drive]`.

Google puede revocar refresh tokens si se generan repetidamente, si el usuario revoca el acceso o por políticas de seguridad. Si la pantalla OAuth está en modo **Testing** y la app es externa, los refresh tokens normalmente caducan a los 7 días para scopes que no son básicos de identidad. Para uso continuo, configura el proyecto OAuth adecuadamente y completa la publicación/verificación que Google requiera.

La aplicación utiliza la carpeta indicada en `folder_id` como raíz. Crea una subcarpeta por carrusel, sube cada PNG en cuanto queda listo y al final agrega `copy_carrusel.txt` y `carrusel_completo.zip`. El historial lista las carpetas recientes.

## Modelos internos

- Texto: `gpt-4.1-mini`
- Imágenes: `gpt-image-2`

Los modelos no aparecen en la interfaz.

## Ejecutar

```powershell
streamlit run app.py
```

Los artículos deben ser públicos y accesibles. La generación requiere que la sesión siga activa; si se interrumpe, las imágenes que ya se hayan subido permanecen en Drive. Para que el trabajo continúe automáticamente tras un reinicio de Streamlit se necesitaría además un trabajador externo/cola de tareas.
