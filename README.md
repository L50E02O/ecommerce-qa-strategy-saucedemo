# ecommerce-qa-strategy-saucedemo

Proyecto de estrategia de QA Manual para la plataforma [SauceDemo](https://www.saucedemo.com/), un sitio de demostración e-commerce utilizado como entorno estándar para prácticas de pruebas de software.

## Objetivo del Proyecto

Este repositorio centraliza la documentación, casos de prueba y reportes de bugs derivados de las actividades de QA Manual sobre SauceDemo. El objetivo es establecer una estrategia de pruebas estructurada y reproducible que cubra los flujos críticos del e-commerce: autenticación, catálogo de productos, carrito de compras y proceso de checkout.

## Contenido del Repositorio

| Carpeta/Archivo      | Descripcion                                           |
|----------------------|-------------------------------------------------------|
| `documentation/`     | Documentos de estrategia y artefactos de QA Manual    |
| `documentation/TestPlan.md` | Plan de pruebas: alcance, riesgos y criterios de aceptacion |
| `documentation/TestCase_Suite.md` | Suite de casos de prueba ejecutables (Login, Carrito, Checkout) |
| `documentation/BugReport_Template.md` | Plantilla de reporte de bugs con ejemplos documentados |

## Enfoque de QA Manual

- **Metodo:** Pruebas manuales ejecutadas siguiendo casos de prueba documentados.
- **Cobertura:** Modulos Login, Carrito y Checkout como flujos de alto riesgo.
- **Trazabilidad:** Cada defecto reportado se vincula a un caso de prueba y criterio de aceptacion.

## Requisitos Previos

- Navegador web actualizado (Chrome, Firefox, Edge o Safari).
- Acceso a internet para conectarse a [SauceDemo](https://www.saucedemo.com/).
- Credenciales de prueba: `standard_user` / `secret_sauce` (documentadas en la aplicacion).

## Estructura Recomendada para Nuevos Documentos

```
ecommerce-qa-strategy-saucedemo/
├── README.md
├── documentation/
│   ├── TestPlan.md
│   ├── TestCase_Suite.md
│   └── BugReport_Template.md
└── .gitignore
```

## Como Contribuir

1. Revisa el `TestPlan.md` para entender el alcance y criterios de aceptacion.
2. Ejecuta los casos de `TestCase_Suite.md` siguiendo los pasos documentados.
3. Utiliza `BugReport_Template.md` para reportar cualquier defecto encontrado.
4. Mantén la nomenclatura y formato establecidos para facilitar la trazabilidad.

## Licencia

Este proyecto es de uso educativo y portfolio. SauceDemo es propiedad de Sauce Labs.
