# neryp_bot — Streamlit

Aplicación que transforma una URL pública en cinco imágenes editoriales para
Instagram (1080 × 1350 px, 4:5), además de un ZIP y copy sugerido.

## Instalar en Windows

```powershell
python -m venv .venv
.venv\\Scripts\\activate
pip install -r requirements.txt
```

## API Key en Secrets (no en la interfaz)

**Local:** crea `.streamlit/secrets.toml`:

```toml
OPENAI_API_KEY = "tu_api_key"
```

**Streamlit Community Cloud:** App settings → Secrets y pega el mismo bloque TOML.

No subas el archivo real `secrets.toml` a GitHub; `.gitignore` ya lo excluye.
La aplicación no muestra ni solicita la clave en pantalla.

## Ejecutar

```powershell
streamlit run app.py
```

Abre normalmente http://localhost:8501. La computadora debe permanecer encendida
mientras la aplicación se use localmente.

Algunos sitios bloquean la extracción o requieren JavaScript, login o suscripción.
Cada carrusel genera cinco imágenes y consume créditos de OpenAI API. Antes de
hacer pública la app, agrega autenticación y límites de uso.
