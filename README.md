# Venta-de-Electrodom-sticos...2.0
- **Tablas principales (21 en total):**
  - Clientes, Productos, Categorías, Proveedores
  - Ventas, Detalle de ventas, Métodos de pago, Pagos
  - Compras, Detalle de compras, Inventario, Ubicaciones
  - Garantías, Devoluciones, Soporte técnico
  - Usuarios, Roles, Auditoría, Reportes
  - Configuraciones, Facturas

- **Relaciones clave:**
  - Una venta pertenece a un cliente y tiene múltiples productos.
  - Cada producto tiene categoría, proveedor y garantía.
  - El inventario se actualiza por entradas (compras) y salidas (ventas).

## 📋 TABLAS Y CAMPOS

### 1. `clientes`
| Campo        | Tipo           | Descripción                         |
|--------------|----------------|-------------------------------------|
| id_cliente   | SERIAL         | Clave primaria                      |
| nombre       | VARCHAR(100)   | Nombre del cliente                  |
| telefono     | VARCHAR(15)    | Teléfono de contacto                |
| direccion    | TEXT           | Dirección del cliente               |
| correo       | VARCHAR(100)   | Correo electrónico                  |

---

### 2. `productos`
| Campo        | Tipo            | Descripción                        |
|--------------|-----------------|------------------------------------|
| id_producto  | SERIAL          | Clave primaria                     |
| nombre       | VARCHAR(100)    | Nombre del producto                |
| descripcion  | TEXT            | Detalles adicionales               |
| categoria_id | INT             | Clave foránea a `categorias`       |
| precio       | NUMERIC(10,2)   | Precio de venta                    |
| stock        | INT             | Existencias actuales               |

---

### 3. `categorias`
| Campo        | Tipo           | Descripción                         |
|--------------|----------------|-------------------------------------|
| id_categoria | SERIAL         | Clave primaria                      |
| nombre       | VARCHAR(50)    | Nombre de la categoría              |

---

### 4. `proveedores`
| Campo        | Tipo           | Descripción                         |
|--------------|----------------|-------------------------------------|
| id_proveedor | SERIAL         | Clave primaria                      |
| nombre       | VARCHAR(100)   | Nombre del proveedor                |
| contacto     | VARCHAR(100)   | Persona de contacto                 |
| telefono     | VARCHAR(15)    | Teléfono                            |
| direccion    | TEXT           | Dirección                           |

---

### 5. `usuarios`
| Campo        | Tipo           | Descripción                         |
|--------------|----------------|-------------------------------------|
| id_usuario   | SERIAL         | Clave primaria                      |
| nombre       | VARCHAR(100)   | Nombre completo                     |
| correo       | VARCHAR(100)   | Correo electrónico                  |
| rol          | VARCHAR(50)    | Rol dentro del sistema              |
| contrasena   | TEXT           | Contraseña (idealmente cifrada)     |

---

### 6. `roles`
| Campo      | Tipo         | Descripción                  |
|------------|--------------|------------------------------|
| id_rol     | SERIAL       | Clave primaria               |
| nombre     | VARCHAR(50)  | Nombre del rol               |

---

### 7. `ventas`
| Campo      | Tipo           | Descripción                  |
|------------|----------------|------------------------------|
| id_venta   | SERIAL         | Clave primaria               |
| fecha      | TIMESTAMP      | Fecha y hora de la venta     |
| id_cliente | INT            | Clave foránea a `clientes`   |
| id_usuario | INT            | Clave foránea a `usuarios`   |
| total      | NUMERIC(10,2)  | Monto total de la venta      |

---

### 8. `detalle_venta`
| Campo        | Tipo           | Descripción                       |
|--------------|----------------|-----------------------------------|
| id_detalle   | SERIAL         | Clave primaria                    |
| id_venta     | INT            | Clave foránea a `ventas`         |
| id_producto  | INT            | Clave foránea a `productos`      |
| cantidad     | INT            | Cantidad vendida                 |
| subtotal     | NUMERIC(10,2)  | Precio total del producto        |

---

### 9. `metodos_pago`
| Campo        | Tipo           | Descripción                         |
|--------------|----------------|-------------------------------------|
| id_metodo    | SERIAL         | Clave primaria                      |
| nombre       | VARCHAR(50)    | Nombre del método (efectivo, etc.) |

---

### 10. `pagos`
| Campo      | Tipo           | Descripción                          |
|------------|----------------|--------------------------------------|
| id_pago    | SERIAL         | Clave primaria                       |
| id_venta   | INT            | Clave foránea a `ventas`             |
| id_metodo  | INT            | Clave foránea a `metodos_pago`       |
| monto      | NUMERIC(10,2)  | Monto pagado                         |

---

### 11. `facturas`
| Campo           | Tipo           | Descripción                       |
|------------------|----------------|-----------------------------------|
| id_factura       | SERIAL         | Clave primaria                    |
| id_venta         | INT            | Clave foránea a `ventas`         |
| numero_factura   | VARCHAR(20)    | Código o folio de la factura     |
| fecha_emision    | DATE           | Fecha de emisión                 |

---

### 12. `compras`
| Campo        | Tipo           | Descripción                        |
|--------------|----------------|------------------------------------|
| id_compra    | SERIAL         | Clave primaria                     |
| fecha        | TIMESTAMP      | Fecha y hora de compra             |
| id_proveedor | INT            | Clave foránea a `proveedores`     |
| total        | NUMERIC(10,2)  | Monto total de la compra           |

---

### 13. `detalle_compra`
| Campo         | Tipo           | Descripción                         |
|---------------|----------------|-------------------------------------|
| id_detalle    | SERIAL         | Clave primaria                      |
| id_compra     | INT            | Clave foránea a `compras`           |
| id_producto   | INT            | Clave foránea a `productos`         |
| cantidad      | INT            | Cantidad adquirida                  |
| costo_unitario| NUMERIC(10,2)  | Costo por unidad                    |

---

### 14. `inventario_movimientos`
| Campo          | Tipo         | Descripción                            |
|----------------|--------------|----------------------------------------|
| id_movimiento  | SERIAL       | Clave primaria                         |
| id_producto    | INT          | Clave foránea a `productos`            |
| tipo_movimiento| VARCHAR(20)  | 'entrada' o 'salida'                   |
| cantidad       | INT          | Cantidad afectada                      |
| fecha          | TIMESTAMP    | Fecha del movimiento                   |
| descripcion    | TEXT         | Detalles del motivo                    |

---

### 15. `ubicaciones`
| Campo         | Tipo           | Descripción                          |
|---------------|----------------|--------------------------------------|
| id_ubicacion  | SERIAL         | Clave primaria                       |
| nombre        | VARCHAR(100)   | Nombre del lugar (almacén, etc.)     |
| descripcion   | TEXT           | Descripción opcional                 |

---

### 16. `garantias`
| Campo         | Tipo         | Descripción                          |
|---------------|--------------|--------------------------------------|
| id_garantia   | SERIAL       | Clave primaria                       |
| id_producto   | INT          | Clave foránea a `productos`          |
| duracion_meses| INT          | Duración de la garantía              |
| condiciones   | TEXT         | Texto con condiciones aplicables     |

---

### 17. `devoluciones`
| Campo          | Tipo         | Descripción                           |
|----------------|--------------|---------------------------------------|
| id_devolucion  | SERIAL       | Clave primaria                        |
| id_venta       | INT          | Clave foránea a `ventas`              |
| id_producto    | INT          | Producto devuelto                     |
| motivo         | TEXT         | Motivo de la devolución               |
| fecha          | DATE         | Fecha de la devolución                |

---

### 18. `soporte_tecnico`
| Campo           | Tipo         | Descripción                            |
|-----------------|--------------|----------------------------------------|
| id_ticket       | SERIAL       | Clave primaria                         |
| id_cliente      | INT          | Cliente que reporta el problema        |
| descripcion     | TEXT         | Descripción del problema               |
| fecha_apertura  | DATE         | Fecha de registro del ticket           |
| estado          | VARCHAR(20)  | Estado: abierto, cerrado, etc.         |

---

### 19. `reportes`
| Campo           | Tipo         | Descripción                          |
|-----------------|--------------|--------------------------------------|
| id_reporte      | SERIAL       | Clave primaria                       |
| titulo          | VARCHAR(100) | Título del reporte                   |
| fecha_creacion  | DATE         | Fecha en que se generó               |
| contenido       | TEXT         | Resumen del reporte                  |

---

### 20. `auditoria`
| Campo         | Tipo         | Descripción                           |
|---------------|--------------|---------------------------------------|
| id_evento     | SERIAL       | Clave primaria                        |
| id_usuario    | INT          | Clave foránea a `usuarios`            |
| accion        | TEXT         | Descripción de la acción realizada    |
| fecha         | TIMESTAMP    | Fecha y hora del evento               |

---

### 21. `configuraciones`
| Campo       | Tipo          | Descripción                          |
|-------------|---------------|--------------------------------------|
| id_config   | SERIAL        | Clave primaria                       |
| clave       | VARCHAR(50)   | Nombre de la configuración           |
| valor       | TEXT          | Valor asignado                       |

---
