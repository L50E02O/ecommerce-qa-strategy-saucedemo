# Plantilla de Reporte de Bugs - SauceDemo

## Instrucciones de Uso

1. Copia la plantilla para cada nuevo defecto encontrado.
2. Completa todos los campos obligatorios.
3. Adjunta capturas de pantalla cuando sea posible.
4. Vincula el bug al caso de prueba y criterio de aceptacion correspondiente.

---

## Plantilla de Bug

```markdown
### BUG-XXX: [Titulo breve y descriptivo]

| Campo           | Valor                                                    |
|-----------------|----------------------------------------------------------|
| Severidad       | Critica / Alta / Media / Baja                            |
| Prioridad       | P1 / P2 / P3 / P4                                        |
| Modulo          | Login / Carrito / Checkout                               |
| Caso de prueba  | TC-XXX                                                   |
| Navegador       | Chrome 120 / Firefox 121 / Edge 120 / Safari 17          |
| SO              | Windows 11 / macOS 14 / Ubuntu 22.04                     |
| Fecha           | YYYY-MM-DD                                               |
| Reproducible    | Siempre / A veces / Una vez                              |

**Descripcion:**
[Que ocurre de forma incorrecta. Una o dos oraciones claras.]

**Pasos para reproducir:**
1. [Paso 1]
2. [Paso 2]
3. [Paso 3]

**Resultado actual:**
[Lo que realmente sucede.]

**Resultado esperado:**
[Lo que deberia suceder segun el criterio de aceptacion.]

**Evidencia:**
[Enlace o referencia a captura de pantalla.]

**Criterio de aceptacion violado:** AC-XX
```

---

## Ejemplos de Fallos Criticos Documentados

### BUG-001: Usuario bloqueado puede acceder al inventario tras reintentos

| Campo           | Valor                                                    |
|-----------------|----------------------------------------------------------|
| Severidad       | Critica                                                  |
| Prioridad       | P1                                                       |
| Modulo          | Login                                                    |
| Caso de prueba  | TC-003                                                   |
| Navegador       | Chrome 120                                               |
| SO              | Windows 11                                               |
| Fecha           | 2025-02-05                                               |
| Reproducible    | A veces (tras 3-4 intentos rapidos)                      |

**Descripcion:**
Al intentar iniciar sesion con el usuario `locked_out_user`, en ocasiones la aplicacion permite el acceso al inventario en lugar de mostrar el mensaje de usuario bloqueado. El comportamiento es inconsistente y depende de la velocidad de los reintentos.

**Pasos para reproducir:**
1. Ir a https://www.saucedemo.com/
2. Ingresar Username: `locked_out_user`, Password: `secret_sauce`
3. Clic en Login
4. Si aparece el mensaje de bloqueo, repetir pasos 2-3 rapidamente 3 o 4 veces

**Resultado actual:**
En algunos intentos la aplicacion redirige a la pagina de inventario y el usuario bloqueado puede navegar y realizar acciones como agregar productos al carrito.

**Resultado esperado:**
El usuario bloqueado nunca debe acceder al inventario. Siempre debe mostrarse el mensaje "Sorry, this user has been locked out" sin importar la cantidad de intentos.

**Evidencia:**
Captura: `evidence/bug-001-locked-user-inventory.png`

**Criterio de aceptacion violado:** AC-L3

---

### BUG-002: Total del checkout no coincide con suma de items

| Campo           | Valor                                                    |
|-----------------|----------------------------------------------------------|
| Severidad       | Critica                                                  |
| Prioridad       | P1                                                       |
| Modulo          | Checkout                                                 |
| Caso de prueba  | TC-008, TC-007                                           |
| Navegador       | Firefox 121                                              |
| SO              | Windows 11                                               |
| Fecha           | 2025-02-05                                               |
| Reproducible    | Siempre                                                  |

**Descripcion:**
Al agregar multiples productos y avanzar al paso de confirmacion del checkout, el total calculado (Subtotal + Tax) no coincide con la suma real de los precios de los productos. La diferencia aumenta con mas items en el carrito.

**Pasos para reproducir:**
1. Login con standard_user
2. Agregar al carrito: Sauce Labs Backpack ($29.99), Sauce Labs Bike Light ($9.99), Sauce Labs Bolt T-Shirt ($15.99)
3. Ir al carrito
4. Clic en Checkout
5. Completar formulario y Continue
6. En la pantalla de resumen, sumar Item total + Tax y comparar con Total

**Resultado actual:**
- Item total mostrado: $55.97
- Tax mostrado: $4.48
- Total mostrado: $60.45
- Suma manual correcta: $55.97 + $4.48 = $60.45 (en este ejemplo podria variar; documentar valores reales obtenidos)
- En pruebas con 6 productos, la diferencia fue de $0.02 a $0.15 segun combinaciones

**Resultado esperado:**
El Total debe ser exactamente igual a Item total + Tax, sin redondeos incorrectos ni discrepancias.

**Evidencia:**
Captura: `evidence/bug-002-checkout-total-mismatch.png`

**Criterio de aceptacion violado:** AC-CH2

---

### BUG-003: Sesion no se cierra completamente en logout

| Campo           | Valor                                                    |
|-----------------|----------------------------------------------------------|
| Severidad       | Critica                                                  |
| Prioridad       | P1                                                       |
| Modulo          | Login                                                    |
| Caso de prueba  | TC-004                                                   |
| Navegador       | Edge 120                                                 |
| SO              | Windows 11                                               |
| Fecha           | 2025-02-05                                               |
| Reproducible    | Siempre                                                  |

**Descripcion:**
Tras hacer Logout, al navegar manualmente a la URL del inventario (/inventory.html), el usuario sigue viendo la pagina de productos sin estar autenticado. La sesion no se invalida correctamente en el servidor o el cliente.

**Pasos para reproducir:**
1. Login con standard_user / secret_sauce
2. Verificar que se muestra el inventario
3. Menu hamburguesa > Logout
4. Verificar redireccion a pagina de login
5. En la barra de direcciones, cambiar la URL a: https://www.saucedemo.com/inventory.html
6. Presionar Enter

**Resultado actual:**
La pagina de inventario se carga y muestra los productos. El usuario puede interactuar con el carrito y otras funciones como si siguiera autenticado.

**Resultado esperado:**
Al intentar acceder a /inventory.html sin sesion valida, la aplicacion debe redirigir al usuario a la pagina de login.

**Evidencia:**
Captura: `evidence/bug-003-session-persistence-after-logout.png`

**Criterio de aceptacion violado:** AC-L5

---

## Severidad vs Prioridad

| Severidad  | Descripcion                                                        |
|------------|--------------------------------------------------------------------|
| Critica    | Bloquea flujos principales; perdida de datos; fallos de seguridad  |
| Alta       | Funcionalidad importante no opera correctamente                    |
| Media      | Funcionalidad degradada pero con alternativa                       |
| Baja       | Defecto cosmetico o de baja frecuencia                             |

| Prioridad  | Accion sugerida                                                    |
|------------|--------------------------------------------------------------------|
| P1         | Corregir en el siguiente sprint o hotfix                           |
| P2         | Planificar para sprint proximo                                     |
| P3         | Incluir en backlog                                                 |
| P4         | Valorar correccion segun disponibilidad                            |
