# Plano 3D · backend

API de [Plano 3D](https://github.com/St-Alejo/plano3d-frontend): de la foto de un plano arquitectónico a un
modelo 3D. FastAPI con arquitectura hexagonal, visión por computadora (OpenCV + red de muros ONNX + OCR),
estructura de obra, cantidades y fotos realistas con IA (OpenAI `gpt-image-2`).

## Correr en local

```bash
python -m venv .venv && .venv/Scripts/activate      # Windows (en Linux/Mac: source .venv/bin/activate)
pip install -e ".[dev,ocr]" && pip install --no-deps "rapidocr-onnxruntime>=1.4"
PLANO3D_MODE=memory uvicorn plano3d.main:app --reload --port 8000   # → http://localhost:8000/docs
```

Claves opcionales en `.env` (nunca se suben): `OPENAI_API_KEY` (fotos con IA), `ANTHROPIC_API_KEY` o
`GROQ_API_KEY` (lector y chat con IA). Sin ellas la app funciona con lo local.

## Pruebas

```bash
ruff check src tests && mypy && pytest
```

## Despliegue

Cada push a `main` construye la imagen `ghcr.io/st-alejo/plano3d-backend` (GitHub Actions). La demo corre en
**Azure Container Apps** (consumo, escala a cero) en modo `memory`: sin base de datos, los proyectos viven
mientras el contenedor está encendido.

El frontend está en [plano3d-frontend](https://github.com/St-Alejo/plano3d-frontend). El historial completo
del proyecto (antes de separarlo) está en [plano3d](https://github.com/St-Alejo/plano3d).
