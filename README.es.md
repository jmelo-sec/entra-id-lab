# Laboratorio de Microsoft Entra ID

[Read in English](README.md)

Laboratorio práctico de gestión de identidades y accesos en Microsoft Entra ID (las áreas de SC-300), documentado con capturas de pantalla.

## Sobre este laboratorio

Es un **laboratorio de formación** en un tenant personal. No es experiencia profesional en un entorno de producción. Lo hice para aprender y dejar constancia de lo que hice y los problemas que resolví.

Entorno: un tenant personal de Microsoft Entra ID con la prueba de P2 (30 días, sin coste) y una suscripción gratuita de Azure. Todos los nombres son ficticios. Las capturas están editadas: se ocultan correos, dominio del tenant, identificadores y direcciones IP.

## Áreas cubiertas

| Área | Temas |
| --- | --- |
| Gestión de identidades | Usuarios, grupos, licencias, colaboración externa, roles, unidades administrativas |
| Autenticación y acceso | SSPR, métodos de autenticación, Temporary Access Pass, acceso condicional, Identity Protection |
| Identidades de carga de trabajo | Registros de aplicaciones, consentimiento, identidades administradas, credenciales federadas |
| Gobierno de identidades | PIM, revisiones de acceso, gestión de derechos, términos de uso |
| Supervisión | Registros de inicio de sesión y auditoría, Log Analytics, KQL |

## Laboratorios

### 1. Tenant, usuarios y licencias

Preparé un tenant personal de Entra ID con un Administrador global solo en la nube, creé usuarios de prueba y activé la prueba de Entra ID P2 (30 días, sin renovación automática).

**Problema encontrado:** el botón de la prueba de licencia salía en gris al entrar con una cuenta Microsoft personal. Hizo falta una cuenta de administrador solo en la nube.

![usuarios](capturas/01-usuarios.png)

![licencias antes](capturas/02-licencias-antes.png)

![licencias p2](capturas/03-licencias-p2.png)

![facturacion](capturas/04-facturacion.png)

### 2. Licencias basadas en grupo

Asigné la licencia P2 a un grupo para que sus miembros la hereden automáticamente.

**Claves:** cada usuario necesita una ubicación de uso, el procesamiento es asíncrono y los grupos anidados no se admiten para licencias.

![licencia por grupo](capturas/05-licencia-por-grupo.png)

### 3. Colaboración externa (B2B)

Invité a un invitado externo con correo personal y revisé la configuración de colaboración externa: restricciones de invitación, nivel de acceso de invitados y listas de dominios permitidos o bloqueados.

![invitado](capturas/06-invitado.png)

![colaboracion externa](capturas/07-colaboracion-externa.png)

### 4. Roles y RBAC

Deleguié el rol de Administrador de usuarios y probé sus límites.

**Clave:** un Administrador de usuarios no puede restablecer la contraseña de un Administrador global ni asignar roles.

![rol admin usuarios](capturas/08-rol-admin-usuarios.png)

![limites rol](capturas/09-limites-rol.png)

### 5. Unidades administrativas

Limité un administrador a una unidad administrativa y comparé el acceso antes y después.

**Trampa:** los permisos se suman. Un rol asignado en todo el tenant anula el ámbito de la unidad administrativa.

![au antes](capturas/10-au-antes.png)

![au despues](capturas/11-au-despues.png)

### 6. Restablecimiento de contraseña de autoservicio (SSPR)

Habilité SSPR para un grupo seleccionado y revisé los métodos.

**Claves:** los administradores siempre necesitan dos métodos, y los métodos disponibles se gestionan en la directiva de métodos de autenticación, no en la página de SSPR.

![sspr](capturas/12-sspr.png)

![sspr metodos](capturas/13-sspr-metodos.png)

### 7. Cuenta de emergencia (break-glass)

Creé un Administrador global solo en la nube para emergencias, que se excluye de las directivas de acceso condicional.

![cuenta emergencia](capturas/14-cuenta-emergencia.png)

### 8. Acceso condicional

Creé una directiva que exige MFA a los usuarios del laboratorio. Empecé en modo solo informe, revisé los resultados y la herramienta What If, y después la activé.

**Clave:** el modo solo informe permite ver el impacto antes de aplicarla.

![ca solo informe](capturas/15-ca-solo-informe.png)

![ca informe ana](capturas/16-ca-informe-ana.png)

![ca que pasa si](capturas/17-ca-que-pasa-si.png)

![ca activada](capturas/18-ca-activada.png)

### 9. Privileged Identity Management (PIM)

Convertí a un usuario en elegible para un rol privilegiado en lugar de permanente, con ajustes de activación: duración, MFA y justificación. Activé el rol y comprobé que quedaba activo durante un tiempo limitado.

![pim configuracion](capturas/19-pim-configuracion.png)

![pim elegible](capturas/20-pim-elegible.png)

![pim activacion](capturas/21-pim-activacion.png)

![pim resultado](capturas/22-pim-resultado.png)

![pim rol activo](capturas/23-pim-rol-activo.png)

### 10. Identity Protection

Simulé un inicio de sesión desde una IP anónima (navegador Tor), observé las dos detecciones de riesgo en tiempo real (IP anónima e IP malintencionada), apliqué una directiva de acceso condicional basada en riesgo y corregí el riesgo.

![id protection](capturas/24-id-protection.png)

![ca riesgo inicio](capturas/25-ca-riesgo-inicio.png)

![riesgo lista](capturas/26-riesgo-lista.png)

![riesgo detalle](capturas/27-riesgo-detalle.png)

![ca02 resultado](capturas/28-ca02-resultado.png)

![riesgo corregido](capturas/29-riesgo-corregido.png)

### 11. Revisiones de acceso

Creé una revisión de la pertenencia a un grupo, la completé como revisor y comprobé los resultados y la auditoría.

**Problemas encontrados:** el ajuste *si los revisores no responden* quitó automáticamente a un usuario sin revisar, y la aplicación de los resultados se quedó atascada durante horas.

![revision acceso](capturas/30-revision-acceso.png)

![revision luis](capturas/31-revision-luis.png)

![revision resultados](capturas/32-revision-resultados.png)

![revision auditoria](capturas/33-revision-auditoria.png)

### 12. Gestión de derechos

Creé un paquete de acceso con aprobación. Un usuario solicitó acceso, otro lo aprobó y se concedió el acceso.

**Problema encontrado:** la solicitud fallaba hasta habilitar *Self* (cuenta propia) en *quién puede solicitar acceso*.

![paquete acceso](capturas/34-paquete-acceso.png)

![solicitud eva](capturas/35-solicitud-eva.png)

![aprobacion luis](capturas/36-aprobacion-luis.png)

![eva vuelve](capturas/37-eva-vuelve.png)

### 13. Términos de uso

Creé unos términos de uso a partir de un PDF y los exigí mediante acceso condicional.

**Problema encontrado:** los términos no aparecían hasta que la directiva usó *Requerir todos los controles seleccionados* en lugar de *Requerir uno de los controles seleccionados*.

![terminos de uso](capturas/38-terminos-de-uso.png)

![ca01 terminos](capturas/39-ca01-terminos.png)

![terminos aceptar](capturas/40-terminos-aceptar.png)

![ca01 controles](capturas/41-ca01-controles.png)

### 14. Registros de aplicaciones y consentimiento

Registré una aplicación, creé un secreto de cliente, añadí permisos delegados y de aplicación y concedí el consentimiento de administrador. Revisé la configuración de consentimiento de usuario y el flujo de consentimiento.

![registro app](capturas/42-registro-app.png)

![secreto](capturas/43-secreto.png)

![permisos antes](capturas/44-permisos-antes.png)

![permisos concedidos](capturas/45-permisos-concedidos.png)

![consentimiento usuario](capturas/46-consentimiento-usuario.png)

![flujo consentimiento](capturas/47-flujo-consentimiento.png)

### 15. Identidades de carga de trabajo

Creé una identidad administrada con un rol de Azure RBAC y una credencial federada para GitHub Actions (OIDC), de modo que no hace falta guardar secretos.

![identidad administrada](capturas/48-identidad-administrada.png)

![entidad servicio mi](capturas/49-entidad-servicio-mi.png)

![rbac identidad](capturas/50-rbac-identidad.png)

![credencial federada](capturas/51-credencial-federada.png)

### 16. Métodos de autenticación y Temporary Access Pass

Habilité el Temporary Access Pass en la directiva de métodos de autenticación, creé un código de un solo uso para un usuario e inicié sesión con él.

**Claves:** cuenta como autenticación fuerte, sirve una o varias veces según se cree y se escribe en el campo de contraseña.

![metodos autenticacion](capturas/52-metodos-autenticacion.png)

![tap creado](capturas/53-tap-creado.png)

![inicio con tap](capturas/54-inicio-con-tap.png)

### 17. Registros de inicio de sesión y auditoría

Revisé los registros de inicio de sesión (pestañas de detalles de autenticación y acceso condicional) y la entrada del registro de auditoría de la creación del Temporary Access Pass.

![registros inicio sesion](capturas/55-registros-inicio-sesion.png)

![detalle tap](capturas/56-detalle-tap.png)

![auditoria tap](capturas/57-auditoria-tap.png)

### 18. Log Analytics y KQL

Envié los registros de inicio de sesión y auditoría de Entra a un área de trabajo de Log Analytics y los consulté con KQL. Antes hubo que dar un rol en la suscripción al administrador del laboratorio.

**Notas:** solo se exportan los eventos nuevos, las horas están en UTC y el código de resultado `50074` indica que se exigió MFA, no que fallara la contraseña.

![asignacion rol azure](capturas/58a-asignacion-rol-azure.png)

![configuracion diagnostico](capturas/58-configuracion-diagnostico.png)

![kql inicios fallidos](capturas/59-kql-inicios-fallidos.png)

![kql auditoria](capturas/60-kql-auditoria.png)

## Autor

Juan Melo Torres · [GitHub](https://github.com/jmelo-sec) · [LinkedIn](https://www.linkedin.com/in/juan-melo-torres)

Estado: preparando el examen SC-300.
