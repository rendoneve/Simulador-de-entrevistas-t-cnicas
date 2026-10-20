# 🧑‍💻 Simulador de Entrevistas Técnicas con IA

Líder Técnico Virtual hecho con Streamlit y Gemini (`google-genai`). Hace una entrevista adaptativa de **3 preguntas** según la vacante y al final genera un reporte con calificación, fortalezas, áreas de mejora y dictamen (**APROBADO / NO APROBADO**).

UAdeO • Sistemas Inteligentes • Dra. Aiblis Susej Herrera Palafox

## Ejecución local

```bash
python -m pip install -r requirements.txt
```

Crea `.streamlit/secrets.toml` (no se sube a GitHub):

```toml
GEMINI_API_KEY = "TU_API_KEY"
```

```bash
python -m streamlit run app.py
```

## Despliegue

1. Sube `app.py`, `requirements.txt`, `.gitignore` y `README.md` a GitHub.
2. En [share.streamlit.io](https://share.streamlit.io) → **Create app** → repositorio, rama `main`, archivo `app.py`.
3. En **Advanced settings → Secrets** agrega `GEMINI_API_KEY = "..."` y pulsa **Deploy**.

## Cómo cumple los casos de prueba

| # | Caso | Implementación |
|---|------|----------------|
| 1 | Jailbreak / distracción | Gemini responde en JSON (`es_respuesta_tecnica`). Si es un desvío, declina, repite la pregunta y **no cuenta como turno**. |
| 2 | Límite de 3 turnos | El contador `respuestas` vive en `st.session_state`; tras la 3.ª respuesta el código muestra un cierre fijo, desactiva el chat y genera el reporte. Nunca hay 4.ª pregunta. |
| 3 | Reinicio limpio | El botón usa un *callback* que restablece todo el estado antes del siguiente rerun (contador 0, historial vacío, vacante desbloqueada). |
| 4 | Coherencia por vacante | Cada vacante tiene una lista de temas permitidos dentro de las *system instructions*. |
