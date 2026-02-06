# Suite de Casos de Prueba - SauceDemo

## Resumen de Cobertura

| Modulo  | Casos | ID Inicio | ID Fin |
|---------|-------|-----------|--------|
| Login   | 4     | TC-001    | TC-004 |
| Carrito | 3     | TC-005    | TC-007 |
| Checkout| 3     | TC-008    | TC-010 |

---

## Tabla de Casos de Prueba

| ID    | Modulo  | Titulo                                  | Pasos                                                | Resultado Esperado                         | Prioridad |
|-------|---------|-----------------------------------------|------------------------------------------------------|--------------------------------------------|-----------|
| TC-001| Login   | Login exitoso con usuario estandar      | 1. Ir a saucedemo.com<br>2. Ingresar standard_user / secret_sauce<br>3. Click Login | Redireccion a inventario con productos listados | Alta      |
| TC-002| Login   | Login fallido con credenciales invalidas| 1. Ir a saucedemo.com<br>2. Ingresar user / wrongpass<br>3. Click Login | Mensaje: "Username and password do not match" | Alta      |
| TC-003| Login   | Usuario bloqueado no accede             | 1. Ir a saucedemo.com<br>2. Ingresar locked_out_user / secret_sauce<br>3. Click Login | Mensaje: "Sorry, this user has been locked out" | Alta      |
| TC-004| Login   | Logout cierra sesion correctamente      | 1. Login con standard_user<br>2. Menu hamburguesa > Logout | Redireccion a pagina de login              | Media     |
| TC-005| Carrito | Agregar producto al carrito             | 1. Login con standard_user<br>2. Click "Add to cart" en primer producto<br>3. Verificar icono del carrito | Badge muestra "1", producto en carrito      | Alta      |
| TC-006| Carrito | Remover producto del carrito            | 1. Con al menos 1 producto en carrito<br>2. Ir a carrito<br>3. Click "Remove" en un item | Producto eliminado, contador actualizado    | Alta      |
| TC-007| Carrito | Verificar total del carrito             | 1. Agregar 2 productos al carrito<br>2. Ir a carrito<br>3. Revisar precios y subtotal | Suma de items = total mostrado (con impuesto si aplica) | Media     |
| TC-008| Checkout| Checkout completo exitoso               | 1. Con productos en carrito<br>2. Checkout<br>3. Completar: First Name, Last Name, Postal Code<br>4. Continuar > Finish | Mensaje "Thank you for your order"         | Alta      |
| TC-009| Checkout| Checkout falla con campos vacios        | 1. Con productos en carrito<br>2. Checkout<br>3. Dejar campos vacios<br>4. Click Continue | Mensaje de error solicitando completar datos | Alta      |
| TC-010| Checkout| Cancelar checkout vuelve al carrito     | 1. Con productos en carrito<br>2. Checkout<br>3. Click Cancel | Vuelta a pagina del carrito con items intactos | Media     |

---

## Detalle de Pasos (Expandido)

### TC-001: Login exitoso con usuario estandar

1. Abrir navegador y navegar a https://www.saucedemo.com/
2. En el campo Username ingresar: `standard_user`
3. En el campo Password ingresar: `secret_sauce`
4. Hacer clic en el boton "Login"
5. **Verificar:** La URL contiene "/inventory" y se muestran productos en la pagina

### TC-002: Login fallido con credenciales invalidas

1. Ir a https://www.saucedemo.com/
2. Ingresar Username: `user`, Password: `wrongpass`
3. Clic en "Login"
4. **Verificar:** Aparece mensaje de error rojo indicando que las credenciales no coinciden

### TC-003: Usuario bloqueado no accede

1. Ir a saucedemo.com
2. Ingresar Username: `locked_out_user`, Password: `secret_sauce`
3. Clic en "Login"
4. **Verificar:** Mensaje "Sorry, this user has been locked out" y permanencia en pagina de login

### TC-004: Logout cierra sesion correctamente

1. Realizar login con standard_user / secret_sauce
2. Clic en el menu hamburguesa (esquina superior izquierda)
3. Seleccionar "Logout"
4. **Verificar:** Redireccion a https://www.saucedemo.com/ con formulario de login visible

### TC-005: Agregar producto al carrito

1. Login con standard_user
2. En la pagina de inventario, clic en "Add to cart" del primer producto
3. Observar el icono del carrito en la barra superior
4. **Verificar:** Badge numerico muestra "1"
5. Clic en el icono del carrito
6. **Verificar:** El producto aparece en la lista del carrito

### TC-006: Remover producto del carrito

1. Tener al menos 1 producto en el carrito
2. Ir a la vista del carrito (clic en icono)
3. Localizar el boton "Remove" del producto
4. Clic en "Remove"
5. **Verificar:** El producto desaparece de la lista y el contador del carrito se actualiza o desaparece

### TC-007: Verificar total del carrito

1. Agregar 2 productos diferentes al carrito (anotar precios)
2. Ir al carrito
3. Sumar manualmente el precio de cada item
4. **Verificar:** El subtotal mostrado coincide con la suma manual

### TC-008: Checkout completo exitoso

1. Tener productos en el carrito
2. Clic en "Checkout"
3. Completar First Name: "Test", Last Name: "User", Postal Code: "12345"
4. Clic en "Continue"
5. Revisar resumen y clic en "Finish"
6. **Verificar:** Mensaje "Thank you for your order" y opcion de volver al inventario

### TC-009: Checkout falla con campos vacios

1. Con productos en carrito, clic en "Checkout"
2. No completar ningun campo del formulario
3. Clic en "Continue"
4. **Verificar:** Mensaje de error (ej. "First Name is required") y permanencia en formulario

### TC-010: Cancelar checkout vuelve al carrito

1. Con productos en carrito, ir a Checkout
2. Completar o no el formulario
3. Clic en "Cancel"
4. **Verificar:** Regreso a la pagina del carrito con los mismos productos

---

## Estados de Ejecucion

| Estado    | Descripcion                                      |
|-----------|--------------------------------------------------|
| No ejecutado | Caso aun no corrido                            |
| Pasado    | Resultado coincide con lo esperado               |
| Fallado   | Resultado no coincide; requiere reporte de bug   |
| Bloqueado | No se puede ejecutar por defecto o dependencia   |
