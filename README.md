# Jardineria Queries
![img](jardin.png)

## Consultas multitabla (Composición interna)

   1. Obtén un listado con el nombre de cada cliente y el nombre y apellido de su representante de ventas.
   ```sql
   SELECT nombre_cliente, CONCAT(nombre, ' ', apellido1,  ' ',apellido2) AS nombre 
   FROM cliente 
   JOIN empleado ON cliente.codigo_empleado_rep_ventas = empleado.codigo_empleado;

   ```

   2. Muestra el nombre de los clientes que hayan realizado pagos junto con el nombre de sus representantes de ventas.
   ```sql
   SELECT nombre_cliente, CONCAT(empleado.nombre, ' ', empleado.apellido1, ' ', empleado.apellido2) AS nombre_representante_ventas
   FROM cliente
   JOIN pago ON cliente.codigo_cliente = pago.codigo_cliente
   JOIN empleado ON empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
   ORDER BY nombre_cliente ASC;
   ```

   3. Muestra el nombre de los clientes que no hayan realizado pagos junto con el nombre de sus representantes de ventas.
   ```sql
   SELECT nombre_cliente, CONCAT(empleado.nombre, ' ', empleado.apellido1, ' ', empleado.apellido2) AS nombre_representante_ventas
   FROM cliente
   LEFT JOIN pago ON cliente.codigo_cliente = pago.codigo_cliente
   JOIN empleado ON empleado.codigo_empleado = cliente.codigo_empleado_rep_ventas
   WHERE pago.codigo_cliente IS NULL
   ORDER BY nombre_cliente ASC;

   ```

   4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

   ```sql
   SELECT nombre_cliente, CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) AS nombre_representante_ventas, CONCAT(o.ciudad) AS ciudad_oficina
   FROM cliente c
   JOIN pago p ON c.codigo_cliente = p.codigo_cliente
   JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
   JOIN oficina o ON e.codigo_oficina = o.codigo_oficina
   ORDER BY nombre_cliente ASC;

   ```

   5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

   ```sql
   SELECT c.nombre_cliente AS cliente_sin_pago, CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) AS nombre_representante_de_ventas, o.ciudad AS ciudad_oficina
   FROM cliente c 
   LEFT JOIN pago p ON c.codigo_cliente = p.codigo_cliente 
   JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado 
   JOIN oficina o ON e.codigo_oficina = o.codigo_oficina 
   WHERE p.codigo_cliente IS NULL;

   ```

   6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada.

   ```sql
   SELECT CONCAT(o.linea_direccion1, ' ', o.linea_direccion2) AS ciudad_oficina 
   FROM oficina o 
   JOIN empleado e ON o.codigo_oficina = e.codigo_oficina 
   JOIN cliente c ON e.codigo_empleado = c.codigo_empleado_rep_ventas 
   WHERE c.ciudad = 'Fuenlabrada';

   ```

   7. Devuelve el nombre de los clientes y el nombre de sus representantes junto con la ciudad de la oficina a la que pertenece el representante.

   ```sql
   SELECT c.nombre_cliente, CONCAT(e.nombre, ' ', e.apellido1, ' ',e.apellido2) AS nombre_representante, o.ciudad AS ciudad_representante 
   FROM cliente c 
   JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado 
   JOIN oficina o ON e.codigo_oficina = o.codigo_oficina;
   ```

   8. Devuelve un listado con el nombre de los empleados junto con el nombre de sus jefes.

   ```sql
   SELECT e.nombre AS nombre_empleado, jefe.nombre AS nombre_jefe 
   FROM empleado e 
   LEFT JOIN empleado jefe ON jefe.codigo_jefe = e.codigo_empleado;
   ```

   9. Devuelve un listado que muestre el nombre de cada empleados, el nombre de su jefe y el nombre del jefe de sus jefe.
   ```sql
   SELECT CONCAT(e.nombre, ' ', e.apellido1, ' ', e.apellido2) AS nombre_empleado, CONCAT(jefe.nombre, ' ', jefe.apellido1, ' ', jefe.apellido2) AS nombre_jefe, CONCAT(jefe2.nombre, ' ', jefe2.apellido1, ' ', jefe2.apellido2) AS nombre_jefe_del_jefe
   FROM empleado e
   JOIN empleado jefe ON e.codigo_jefe = e2.codigo_empleado
   JOIN empleado jefe2 ON jefe.codigo_jefe = jefe2.codigo_empleado;
   ```

   10. Devuelve el nombre de los clientes a los que no se les ha entregado a tiempo un pedido.

   ```sql
   SELECT c.nombre_cliente AS nombre_cliente
   FROM cliente c
   JOIN pedido p ON c.codigo_cliente = p.codigo_cliente
   WHERE fecha_entrega > fecha_esperada OR fecha_entrega IS NULL;
   ```

   11. Devuelve un listado de las diferentes gamas de producto que ha comprado cada cliente.
   ```sql
   SELECT DISTINCT c.nombre_cliente, g.gama 
   FROM cliente c 
   JOIN pedido p ON c.codigo_cliente = p.codigo_cliente 
   JOIN detalle_pedido d ON p.codigo_pedido = d.codigo_pedido 
   JOIN producto pro ON d.codigo_producto = pro.codigo_producto 
   JOIN gama_producto g ON pro.gama = g.gama;
   ```

## Consultas multitabla (Composición externa)

   1. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago.
   
   ```sql
   
   ```

   2. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pedido.
   
   ```sql
   
   ```

   3. Devuelve un listado que muestre los clientes que no han realizado ningún pago y los que no han realizado ningún pedido.
   
   ```sql
   
   ```

   4. Devuelve un listado que muestre solamente los empleados que no tienen una oficina asociada.
   
   ```sql
   
   ```

   5. Devuelve un listado que muestre solamente los empleados que no tienen un cliente asociado.
   
   ```sql
   
   ```

   6. Devuelve un listado que muestre solamente los empleados que no tienen un cliente asociado junto con los datos de la oficina donde trabajan.
   
   ```sql
   
   ```

   7. Devuelve un listado que muestre los empleados que no tienen una oficina asociada y los que no tienen un cliente asociado.
   
   ```sql
   
   ```

   8. Devuelve un listado de los productos que nunca han aparecido en un pedido.
   
   ```sql
   
   ```

   9. Devuelve un listado de los productos que nunca han aparecido en un pedido. El resultado debe mostrar el nombre, la descripción y la imagen del producto.
   
   ```sql
   
   ```

   10. Devuelve las oficinas donde no trabajan ninguno de los empleados que hayan sido los representantes de ventas de algún cliente que haya realizado la compra de algún producto de la gama Frutales.
   
   ```sql
   
   ```

   11. Devuelve un listado con los clientes que han realizado algún pedido pero no han realizado ningún pago.
   
   ```sql
   
   ```

   12. Devuelve un listado con los datos de los empleados que no tienen clientes asociados y el nombre de su jefe asociado.
   
   ```sql
   
   ```


## Consultas sobre una tabla

   1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.

   ```sql
   SELECT codigo_oficina, ciudad 
   FROM oficina;
   ```

   2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.
   
   ```sql
   SELECT telefono , ciudad 
   FROM oficina
   WHERE pais='España';
   
   ```

   3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo jefe tiene un código de jefe igual a 7.
   
   ```sql
   SELECT nombre, apellido1, apellido2, email
   FROM empleado
   WHERE empleado.codigo_jefe = 7;
   ```

   4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la empresa.
   
   ```sql
   SELECT puesto, CONCAT(nombre,' ',apellido1,' ',apellido2) AS nombre_jefe, email 
   FROM empleado 
   WHERE codigo_jefe IS NULL;
   ```

   5. Devuelve un listado con el nombre, apellidos y puesto de aquellos empleados que no sean representantes de ventas.
   
   ```sql
   SELECT CONCAT(nombre, ' ', apellido1, ' ', apellido2) AS nombre_empleado, puesto 
   FROM empleado 
   WHERE puesto <> 'Representante Ventas';
   ```

   6. Devuelve un listado con el nombre de los todos los clientes españoles.
   
   ```sql
   SELECT nombre_cliente
   FROM cliente c
   WHERE c.pais = 'Spain';
   ```

   7. Devuelve un listado con los distintos estados por los que puede pasar un pedido.
   
   ```sql
   SELECT DISTINCT estado 
   FROM pedido;
   ```

   8. Devuelve un listado con el código de cliente de aquellos clientes que realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:

    Utilizando la función YEAR de MySQL.
    Utilizando la función DATE_FORMAT de MySQL.
    Sin utilizar ninguna de las funciones anteriores.

    
   ```sql
   SELECT codigo_cliente 
   FROM pago 
   WHERE YEAR(fecha_pago) = 2008;

   SELECT DISTINCT codigo_cliente
   FROM cliente c
   JOIN pago p ON c.codigo_cliente = p.codigo_cliente
   WHERE DATE_FORMAT(p.fecha_pago, "%Y") = 2008;
   ```

   9. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos que no han sido entregados a tiempo.
   
   ```sql
   SELECT codigo_pedido, codigo_cliente, fecha_esperada, fecha_entrega
   FROM pedido 
   WHERE fecha_entrega > fecha_esperada;
   ```

   10. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al menos dos días antes de la fecha esperada.

   
   ```sql
   
   ```

    Utilizando la función ADDDATE de MySQL.
    Utilizando la función DATEDIFF de MySQL.
    ¿Sería posible resolver esta consulta utilizando el operador de suma + o resta -?

   11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.
   
   ```sql
   SELECT * 
   FROM pedido 
   WHERE estado='rechazado' AND YEAR(fecha_pedido)=2009;
   ```

   12. Devuelve un listado de todos los pedidos que han sido entregados en el mes de enero de cualquier año.
   
   ```sql
   SELECT *
   FROM pedido
   WHERE estado = 'Entregado' AND DATE_FORMAT(fecha_pedido, "%c") = 01;
   ```

   13. Devuelve un listado con todos los pagos que se realizaron en el año 2008 mediante Paypal. Ordene el resultado de mayor a menor.
   
   ```sql
   SELECT * 
   FROM pago  
   WHERE YEAR(fecha_pago) = 2008 AND forma_pago = 'Paypal' 
   ORDER BY fecha_pago DESC;
   ```

   14. Devuelve un listado con todas las formas de pago que aparecen en la tabla pago. Tenga en cuenta que no deben aparecer formas de pago repetidas.
   
   ```sql
   
   ```

   15. Devuelve un listado con todos los productos que pertenecen a la gama Ornamentales y que tienen más de 100 unidades en stock. El listado deberá estar ordenado por su precio de venta, mostrando en primer lugar los de mayor precio.
   
   ```sql
   
   ```

   16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y cuyo representante de ventas tenga el código de empleado 11 o 30.
   
   ```sql
   
   ```


## Subconsultas

#### Con operadores básicos de comparación

1. Devuelve el nombre del cliente con mayor límite de crédito.
 ```sql
   
   ```

2. Devuelve el nombre del producto que tenga el precio de venta más caro.
 ```sql
   
   ```
3. Devuelve el nombre del producto del que se han vendido más unidades. (Tenga en cuenta que tendrá que calcular cuál es el número total de unidades que se han vendido de cada producto a partir de los datos de la tabla `detalle_pedido`)
 ```sql
   
   ```
4. Los clientes cuyo límite de crédito sea mayor que los pagos que haya realizado. (Sin utilizar `INNER JOIN`).
 ```sql
   
   ```
5. Devuelve el producto que más unidades tiene en stock.
 ```sql
   
   ```
6. Devuelve el producto que menos unidades tiene en stock.
 ```sql
   
   ```
7. Devuelve el nombre, los apellidos y el email de los empleados que están a cargo de **Alberto Soria**.
 ```sql
   
   ```
#### Subconsultas con ALL y ANY

1. Devuelve el nombre del cliente con mayor límite de crédito.
 ```sql
   
   ```
2. Devuelve el nombre del producto que tenga el precio de venta más caro.
 ```sql
   
   ```
3. Devuelve el producto que menos unidades tiene en stock.
 ```sql
   
   ```

#### Subconsultas con IN y NOT IN

1. Devuelve el nombre, apellido1 y cargo de los empleados que no representen a ningún cliente.
2. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago.
3. Devuelve un listado que muestre solamente los clientes que sí han realizado algún pago.
4. Devuelve un listado de los productos que nunca han aparecido en un pedido.
5. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos empleados que no sean representante de ventas de ningún cliente.
6. Devuelve las oficinas donde **no trabajan** ninguno de los empleados que hayan sido los representantes de ventas de algún cliente que haya realizado la compra de algún producto de la gama `Frutales`.
7. Devuelve un listado con los clientes que han realizado algún pedido pero no han realizado ningún pago.

#### Subconsultas con EXISTS y NOT EXISTS

1. Devuelve un listado que muestre solamente los clientes que no han realizado ningún pago.
2. Devuelve un listado que muestre solamente los clientes que sí han realizado algún pago.
3. Devuelve un listado de los productos que nunca han aparecido en un pedido.
4. Devuelve un listado de los productos que han aparecido en un pedido alguna vez.


# Tips for Querys
## Tips con GROUP BY

1. Agrupar por más de una columna


```sql

```

2. Having para aggregate functions


```sql
SELECT e.nombre AS nombre_empleado_rep_ventas, COUNT(c.nombre_cliente)
FROM cliente c JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
GROUP BY e.nombre
HAVING COUNT(c.nombre_cliente) > 4;
```

3. GROUP BY con funcion escalar

```sql

```

4. GROUP BY de dos consultas con UNION ALL
- las dos consultas deben tener el mismo alias de columna
- union all
- alias para la union()
- la consulta exterior tiene el group by

```sql

```

5. Concatenar valores del resultado

```sql
SELECT e.nombre AS nombre_empleado_rep_ventas, GROUP_CONCAT(c.nombre_cliente SEPARATOR ', ') AS clientes
FROM cliente c
JOIN empleado e ON c.codigo_empleado_rep_ventas = e.codigo_empleado
GROUP BY e.nombre;
```


## Tips con WHERE

1. IN para comparar con colecciones ()

```sql
SELECT * FROM producto
WHERE gama IN (1,2)
```

2. Subconsulta con WHERE

```sql

```

3. LIKE

```sql

```

4. Subconsulta dentro de IN

```sql
SELECT * FROM producto
WHERE gama IN(
   SELECT gama FROM gama_producto
   WHERE gama like 'alta'
)
```

5.

```sql

```
## Tips con SELECT