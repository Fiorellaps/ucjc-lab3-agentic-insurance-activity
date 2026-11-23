<img src="https://iddigitalschool.com/wp-content/uploads/2024/03/UCJC-Horizontal_Granate.png" alt="Universidad Camilo José Cela" width="300">

# Laboratorio 3 · Gestión de reclamaciones con agentes de IA

Programación Avanzada y Entornos de Desarrollo para la IA · Tema 3

Desarrollo de un sistema multiagente que analiza partes de siniestro de una aseguradora ficticia (Aseguradora Norte): expondrás los datos con un servidor MCP, consultarás las condiciones de las pólizas con RAG sobre Chroma y orquestarás agentes con CrewAI que clasifiquen cada parte, verifiquen la cobertura y propongan una resolución. Pondrás en práctica lo visto en el Tema 3: modelos fundacionales, RAG, agentes, MCP y seguridad (guardrails, policies y aprobación humana).

Todos los datos son inventados y han sido generados para la actividad.

## Qué vas a practicar

| Paso | Contenido |
|---|---|
| Clasificación del parte | tipo de siniestro, gravedad y datos que faltan |
| RAG con Chroma | consulta de las condiciones de las pólizas (`docs/`) y cita de la cláusula |
| Servidor MCP con FastMCP | al menos 3 tools sobre los CSV: póliza, histórico y validación de importes con el tarifario |
| Orquestación con CrewAI | al menos 3 agentes con roles distintos y un patrón justificado (secuencial, supervisor o jerárquico) |
| Salida estructurada | informe en JSON validado con Pydantic |
| Seguridad | guardrail de salida, policy fuera del prompt, aprobación humana y prueba con partes maliciosos |

## Archivos

| Archivo | Contenido |
|---|---|
| `docs/` | 5 PDF con las condiciones generales, las de auto, hogar y responsabilidad civil, y el procedimiento de tramitación (para el RAG) |
| `partes/txt/` | 81 partes de siniestro en texto |
| `partes/pdf/` | 8 partes de siniestro en PDF |
| `data/asegurados.csv` | 300 asegurados con póliza, producto y estado (activa, impagada o anulada) |
| `data/siniestros_historicos.csv` | Histórico de siniestros por asegurado |
| `data/tarifario.csv` | Importes orientativos mínimos y máximos por concepto |

Los partes son de calidad variable: algunos están completos, otros incompletos o ambiguos, y alguno contiene indicios de fraude o instrucciones sospechosas. Forma parte del reto detectarlo.

## Requisitos

- Al menos 3 agentes con roles distintos y un patrón de orquestación justificado.
- RAG con Chroma sobre los PDF de `docs/`. Las resoluciones deben citar la cláusula consultada.
- Servidor MCP propio con FastMCP y al menos 3 tools sobre los CSV.
- Salida estructurada con Pydantic y al menos un guardrail de salida.
- Al menos una policy aplicada fuera del prompt (por ejemplo, niveles de aprobación por importe o restricción de las tools de cada agente).
- Aprobación humana (human-in-the-loop) cuando el procedimiento lo exija.
- Prueba de seguridad con los partes que contienen instrucciones maliciosas, explicando cómo se comporta tu sistema.

El modelo, los campos que extraes, las tools adicionales (por ejemplo, detección de duplicados), la presentación del resultado (notebook, Chainlit o Streamlit) y la forma de medir la calidad son libres. La publicación es opcional.

## Cómo empezar

```bash
python -m venv .venv
source .venv/bin/activate        # en Windows: .venv\Scripts\activate
pip install crewai fastmcp chromadb pypdf pydantic
```

Puedes usar un modelo local con Ollama (por ejemplo, `ollama pull llama3.1:8b`) o un modelo por API. El modelo de embeddings por defecto de Chroma funciona en inglés; prueba uno multilingüe si trabajas en español.

## Entrega

- Código del proyecto listo para ejecutar.
- (Opcional) Memoria breve (1-2 páginas): agentes y patrón elegido, tools del MCP, diseño del RAG (tamaño de fragmento y modelo de embeddings), guardrail y policy aplicados, y resultado de la prueba de seguridad.

