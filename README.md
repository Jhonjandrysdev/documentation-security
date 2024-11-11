# PRACTICAS DE SEGURIDAD PARA SITIO WEB EN WORDPRESS E IMPLEMENTACIÓN EN PRODUCCIÓN

1 - Mantener WordPress, temas y plugins actualizados: Las actualizaciones corrigen vulnerabilidades o inconsistencias de seguridad, por lo que es vital mantener instaladas siempre las versiones más recientes de WordPress, sus temas y plugins.

1.1 Para su uso en producción se puede configurar las actualizaciones automaticas en nuestro sitio web de la siguiente manera:

```php
Se añade esta función en nuestro acrhivo wp-config.php
define('WP_AUTO_UPDATE_CORE', true);
```


2 - Usar autenticación en dos pasos: Añadir un segundo factor de autenticación nos ayuda a proteger las cuentas de nuestros ususarios, ya que, incluso si las credenciales son robadas, un atacante o la persona que robo la cuenta necesitaría acceso adicional para ingresar al sitio.

2.1 Para el uso de esta buena practica en producción se puede instalar diferentes plugins como son:
```python
Estos plugins permiten generar la autenticación en dos pasos a las cuentas de usuario en WordPress.

- Two Factor Authentication
-  WP 2FA
```

3 - Limitar intentos de inicio de sesión: Restringir la cantidad de intentos fallidos de inicio de sesión para conocer y prevenir un ataque de seguridad.

3.1 Para uso en producción se puede instalar los siguientes plugins para realizar bloqueos en IP
```python
Este plugin permiten el bloqueo de la dirección IP de quien intente acceder y falle repetidamente.

- Limit Login Attempts Reloaded 
```

4 - Configurar certificados SSL/TLS: Con el fin de asegurar que la información entre el navegador del usuario y el servidor esté encriptada.

```
Para asegurar la información con este metodo en apache, que se agrega en el archivo .htacess se forza el HTTPS de la dirección web.

RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

5 -  Restringir el acceso a la API REST: Limitar el uso de la API REST para usuarios autenticados y deshabilita el acceso a usuarios no registrados, para evitar vulnerabilidades o ataques a los endpoints de los usuarios que no esten autenticados.

```php
    Mediantes este codigo que se agrega en el archivo functions.php limitamos el acceso a la API de solo los usuarios autenticados

    add_filter('rest_authentication_errors', function($result) {
    if (!is_user_logged_in()) {
        return new WP_Error('rest_cannot_access', __('No tienes permisos para acceder a la API REST'), array('status' => rest_authorization_required_code()));
    }
    return $result;
});
```