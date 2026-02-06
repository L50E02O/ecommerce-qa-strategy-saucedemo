# Plan de Pruebas - SauceDemo E-commerce

## 1. Informacion General

| Campo          | Valor                                           |
|----------------|--------------------------------------------------|
| Proyecto       | SauceDemo E-commerce QA Strategy                 |
| Tipo de pruebas| Manual, funcionales                              |
| SUT            | https://www.saucedemo.com/                       |
| Version SUT    | Demo estandar (sin version especifica)           |
| Ultima actualizacion | 2025-02-05                             |

## 2. Alcance

### 2.1 Modulos Incluidos

| Modulo     | Descripcion                                   | Prioridad |
|------------|-----------------------------------------------|-----------|
| Login      | Autenticacion de usuarios (estandar, bloqueado, problem) | Alta      |
| Carrito    | Agregar, quitar y modificar cantidades en el carrito     | Alta      |
| Checkout   | Informacion del comprador, resumen y finalizacion        | Alta      |

### 2.2 Modulos Excluidos

- Integraciones con pasarelas de pago reales.
- Pruebas de carga o rendimiento.
- Pruebas de accesibilidad (a11y).
- Pruebas de compatibilidad multiplataforma/movil.

### 2.3 Criterios de Entrada

- El sitio https://www.saucedemo.com/ esta accesible.
- Las credenciales de prueba estan disponibles.
- Navegador web actualizado y funcionando correctamente.

## 3. Riesgos

| ID  | Riesgo                                  | Impacto | Probabilidad | Mitigacion                              |
|-----|-----------------------------------------|---------|--------------|-----------------------------------------|
| R01 | Cambios no documentados en la aplicacion| Alto    | Media        | Revisar la aplicacion antes de cada ciclo |
| R02 | Credenciales de prueba alteradas        | Alto    | Baja         | Verificar credenciales al inicio de sesion |
| R03 | Inestabilidad de red o disponibilidad   | Medio   | Media        | Documentar fallos y reintentar en horario distinto |
| R04 | Diferentes comportamientos por navegador| Medio   | Baja         | Ejecutar casos criticos en 2+ navegadores |
| R05 | Datos residuales afectan el resultado   | Bajo    | Media        | Cerrar sesion y limpiar carrito entre pruebas |

## 4. Criterios de Aceptacion

### 4.1 Login

| ID   | Criterio                                                | Resultado Esperado                          |
|------|---------------------------------------------------------|---------------------------------------------|
| AC-L1| Usuario estandar puede autenticarse correctamente        | Redireccion al inventario sin errores       |
| AC-L2| Credenciales invalidas muestran mensaje de error         | Mensaje claro, sin revelar datos sensibles  |
| AC-L3| Usuario bloqueado no accede al inventario                | Mensaje indicando que el usuario esta bloqueado |
| AC-L4| Usuario problem presenta delays pero funciona            | La aplicacion responde eventualmente        |
| AC-L5| Logout cierra sesion correctamente                       | Redireccion a pagina de login               |

### 4.2 Carrito

| ID   | Criterio                                                | Resultado Esperado                          |
|------|---------------------------------------------------------|---------------------------------------------|
| AC-C1| Agregar producto actualiza contador del carrito          | Badge del carrito refleja la cantidad       |
| AC-C2| Quitar producto desde la pagina del carrito              | Producto desaparece y total se recalcula    |
| AC-C3| Cantidad y precios se muestran correctamente             | Suma de items coincide con total mostrado   |
| AC-C4| Carrito vacio permite continuar comprando                | Usuario puede volver al inventario          |
| AC-C5| Carrito persiste al navegar entre paginas                | Items no se pierden al ir y volver          |

### 4.3 Checkout

| ID   | Criterio                                                | Resultado Esperado                          |
|------|---------------------------------------------------------|---------------------------------------------|
| AC-CH1| Formulario de checkout valida campos obligatorios        | Mensaje de error si falta nombre/apellido/codigo |
| AC-CH2| Resumen muestra items y total correctos                  | Coincide con carrito previo al checkout     |
| AC-CH3| Compra completada muestra mensaje de confirmacion        | "Thank you for your order" visible          |
| AC-CH4| Boton Cancel devuelve al carrito                         | Usuario puede modificar el pedido           |
| AC-CH5| Compra finalizada resetea el carrito                     | Nuevo carrito vacio para siguiente sesion   |

## 5. Entregables

- Casos de prueba documentados en `TestCase_Suite.md`.
- Reportes de bugs en formato `BugReport_Template.md`.
- Evidencias (capturas, pasos reproducibles) asociadas a cada defecto.

## 6. Criterios de Salida

- Todos los casos de prueba planificados han sido ejecutados.
- Defectos criticos y altos han sido reportados y priorizados.
- La documentacion esta actualizada y consistente con los hallazgos.
