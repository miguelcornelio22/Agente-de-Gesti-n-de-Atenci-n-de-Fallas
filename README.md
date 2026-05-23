# 🛠️ Agente de Gestión de Fallas – Industria de Hidrocarburos

Este proyecto implementa un **agente inteligente de gestión de fallas** para la industria de hidrocarburos, diseñado con **LangChain**, **Python** y **PostgreSQL**.  
Su objetivo es mejorar la **eficiencia y rapidez en la atención de incidentes críticos**, garantizando continuidad operativa y seguridad.

---

## 🌍 Contexto e importancia
La industria de hidrocarburos es un pilar del desarrollo económico del Perú:  
- Provee energía para transporte, industria y generación eléctrica.  
- Genera empleo y recursos fiscales.  
- Conecta regiones mediante infraestructura crítica (ductos, plantas, estaciones).  

⚠️ **Impacto de fallas:**  
Una falla en equipos críticos puede detener la producción, afectar el suministro energético y generar pérdidas millonarias.  
Por ello, contar con un **sistema de gestión de fallas eficiente y rápido** es vital para la seguridad y sostenibilidad.

---

## ⚙️ Arquitectura del sistema
![Arquitectura del sistema](docs/arquitectura_agente.png)

**Componentes principales:**
1. **Input:** Texto libre del reporte de falla.  
2. **Orquestador (`create_agent`):** Coordina herramientas y middlewares.  
3. **Middlewares:**  
   - Validación de ID y ubicación.  
   - Verificación de criticidad baja/media sin stock (nota preventiva).  
4. **Herramientas (Tools):**  
   - Procesar reporte.  
   - Integrar datos desde CSV.  
   - Evaluar criticidad.  
   - Generar informe PDF.  
5. **Memoria:** Registro persistente en PostgreSQL.  
6. **Output:** Informe PDF y orden de trabajo.

---

## 🚀 Funcionalidades
- Validación automática de reportes.  
- Evaluación de criticidad y generación de alertas preventivas.  
- Creación de informes PDF estructurados.  
- Registro persistente en base de datos Postgres.  
- Monitoreo del flujo con **LangSmith Tracing**.

---

## 📊 Ejemplo de uso
```python
reporte = "El compresor CMP-2002 en Planta-Lima presenta criticidad baja y no tiene stock disponible."
config = {"configurable": {"thread_id": "demo_flujo"}}

resultado = agente_fallas.invoke({"messages": [HumanMessage(content=reporte)]}, config=config)

for msg in resultado["messages"]:
    print(msg.content)
