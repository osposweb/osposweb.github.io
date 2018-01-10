# Introducción

Esperamos que ya hayas leído el archivo README antes de venir aquí, que ya debería darte una buena pista de lo que trata este software. Una aplicación POS basada en web que utiliza MySQL como back-end y que solo requiere un navegador web en su punto de venta. Es una herramienta que le permite administrar sus existencias, ventas, emitir comprobantes o facturas y proporcionarle informes de ventas y existencias.

OSPOS es una aplicación web de código abierto escrita en PHP y es una evolución de una aplicación web llamada punto de venta PHP, cuando solía ser de código abierto antes de convertirse en una aplicación comercial. Desde ese momento, las dos aplicaciones divergieron y gracias a los diferentes colaboradores OSPOS evolucionó en una aplicación robusta que las tiendas pequeñas pueden usar.

# Características

-Gestión de stock (artículos y kits)
-Registro de venta con registro de transacciones
-Impresión de recibos y facturas y / o envío de correos electrónicos
-Generación e impresión de código de barras
-Base de datos de proveedores y clientes
-Usuario múltiple con control de permisos
-Recibos
-Informes sobre ventas, pedidos, estado de inventario
-Tarjeta de regalo
-Mensajería (SMS)
-Multi lenguaje
-Diferentes temas de UI
-Arquitectura


OSPOS es un código basado en CodeIgniter, por lo que un buen punto de partida para comprender la arquitectura del software es leer un tutorial (CodeIgniter) o una breve descripción en Wikipedia.

El código hace uso del patrón de arquitectura llamado Modelo-Vista-Controlador (MVC), arriba el enlace de Wikipedia contiene un enlace a la página MVC en caso de que quiera entender más. Por lo tanto, es importante que se acostumbre a los nombres de los directorios, como controladores, modelos, vistas y de qué se tratan.

Además del concepto de MVC, CodeIgniter usa la URL para apuntar a Clase / Funciones y utiliza una tabla de enrutamiento para facilitar la navegación a través de las vistas y de acuerdo con la ruta de la URL.
