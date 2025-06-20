	```sql
	
	-- create la base de datos Stage_Northwind
	create database Stage_Northwind

	-- create la base de datos datamart_Northwind
	create database datamart_Northwind

	-- imoplementar la base de datos de Stage_Northwind  , 
	use Stage_Northwind


	create table categorias(
	categoriasid int not null,
	nombrecategoria varchar (15));

	create table clientes (
	clienteid char (5) not null,
	compania varchar (40) not null,
	ciudad varchar (15) ,
	region varchar (15),
	codigopostal char (10),
	pais nvarchar (15)
	);

	create table empleado(
	empleadoid int not null,
	nombre varchar (10)not null,
	apellido varchar (20)not null,
	fecha_contratacion date,
	);

	create table producto (
	productoid int not null,
	nombre_producto varchar (50)not null,
	presio_unitario decimal (15,2) not null, 
	);

	create table provedor(
	provedorid int not null,
	provedor_nombre varchar (40)not null,
	ciudad varchar (15), 
	region varchar (15),
	pais varchar (15)
	);

	create table ventas (
	clienteid char (5) not null,
	empleado_codigo int not null,
	producto_codigo int not null,
	ventas_order datetime not null,
	ventas_monto decimal (15,2)not null,
	ventas_unidades int not null,
	ventas_precio_unitario decimal (15,2)not null,
	ventas_descuento decimal (15,2)not null,
	);

-- Create el datamart_Northwind
use datamart_Northwind

create table dim_cliente (
cliente_Skey int not null identity (1,1),
cliente_codigoBkey char (5)not null ,
cliente_compania varchar (40) not null ,
cliente_ciudad varchar (15)not null ,
cliente_region varchar (25)not null ,
clinete_pais varchar (15) not null ,
constraint pk_dimcliente
primary key (cliente_Skey)

);

create table dim_empleado(
empleado_Skey int not null identity (1,1),
emplado_codigoBkey int not null,

empleado_nombre_ompleto varchar (100) not null,
constraint pk_dimepleado
primary key (empleado_Skey)
);

create table dim_producto (
producto_Skey  int not null identity (1,1),
producto_codigoBkey int not null,
producto_nombre varchar (80) not null,
producto_categoria_nombre varchar (15) not null,
constraint pk_dimproducto
primary key (producto_Skey)
);

create table dim_tiempo(
tiempo_Skey int not null identity (1,1),
tiempo_FechaActual datetime not null,
tiempo_anio int not null,
tiempo_trimestre int not null,
tiempo_mes int not null,
tiempo_semana int not null,
tiempo_dia_de_anio int not null,
tiempo_deia_de_mes int not null,
tiempo_dia__semana int not null

constraint pk_dimtimpo
primary key (tiempo_Skey)

);


create table fact_ventas(
cliente_Skey int not null,
empleados_Skey int not null,
producto_Skey int not null,
timpo_Skey int not null,
ventas_Norden int not null,
ventas_monto  decimal(15,2) not null,
ventas_unidades int not null,
ventas_punitario decimal (15,2) not null
ventas_descuento decimal (15,2) not null

constraint pk_factVentas
primary key (cliente_Skey, empleados_Skey,producto_Skey,timpo_Skey  ),
constraint pk_factVentas_dimcliente 
foreign key (cliente_Skey)
references dim_cliente(cliente_Skey),
constraint pk_factVentas_dimempleado
foreign key (empleados_Skey)
references dim_empleado(empleados_Skey),
constraint pk_factVentas_dimproducto
foreign key (producto_Skey)
references dim_producto(producto_Skey),
constraint pk_factVentas_dimtimpo
foreign key (timpo_Skey)
references dim_tiempo(timpo_Skey)
);

```