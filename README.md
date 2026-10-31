# neryp_bot — Streamlit

Aplicación web que convierte una URL de artículo en cinco imágenes editoriales
para Instagram, 1080 × 1350 px (4:5), más un ZIP y copy sugerido.

## Instalar en Windows

```powershell
cd ruta\a\neryp_bot
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

## Configurar API

Copia `.env.example` a `.env` y agrega tu clave:

```env
OPENAI_API_KEY=tu_api_key
OPENAI_TEXT_MODEL=gpt-4.1-mini
OPENAI_IMAGE_MODEL=gpt-image-1
```

También puedes pegar la API Key en la barra lateral de la aplicación.
Nunca subas `.env` a GitHub.

## Ejecutar

```powershell
streamlit run app.py
```

Abre normalmente http://localhost:8501. La computadora debe permanecer encendida
y la aplicación activa para usarla localmente.

## Publicar

Puedes desplegarla en Streamlit Community Cloud conectando el repositorio privado
si tu plan/flujo de despliegue lo permite, o en otro servidor compatible.
En la nube guarda `OPENAI_API_KEY` como secreto, no en el repositorio.

## Limitaciones

Algunos sitios bloquean la extracción, requieren login o cargan texto con JavaScript.
Cada carrusel genera cinco imágenes y consume créditos de API. Antes de hacer pública
la app conviene añadir autenticación, cuotas por usuario, límites de gasto y controles
adicionales de seguridad para las URLs.
