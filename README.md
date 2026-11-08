# Microsoft Entra ID lab

[Leer en español](README.es.md)

A hands-on lab covering identity and access management in Microsoft Entra ID (the SC-300 areas), documented with screenshots.

## About this lab

This is a **training lab** in a personal tenant. It is not professional experience in a production environment. I built it to learn and to leave evidence of what I did and the problems I solved.

Environment: a personal Microsoft Entra ID tenant with the P2 trial (30 days, no charge) and a free Azure subscription. All names are fictitious. Screenshots are redacted: emails, tenant domain, identifiers and IP addresses are hidden.

## Areas covered

| Area | Topics |
| --- | --- |
| Manage identities | Users, groups, licensing, external collaboration, roles, administrative units |
| Authentication and access | SSPR, authentication methods, Temporary Access Pass, Conditional Access, Identity Protection |
| Workload identities | App registrations, consent, managed identities, federated credentials |
| Identity governance | PIM, access reviews, entitlement management, terms of use |
| Monitoring | Sign-in and audit logs, Log Analytics, KQL |

## Labs

### 1. Tenant, users and licensing

Set up a personal Entra ID tenant with a cloud Global Admin, created test users and activated the Entra ID P2 trial (30 days, no auto-renewal).

**Problem found:** the licence trial button was greyed out when signed in with a personal Microsoft account. A cloud-only admin account was needed.

![usuarios](capturas/01-usuarios.png)

![licencias antes](capturas/02-licencias-antes.png)

![licencias p2](capturas/03-licencias-p2.png)

![facturacion](capturas/04-facturacion.png)

### 2. Group-based licensing

Assigned the P2 licence to a group so members inherit it automatically.

**Key points:** requires a usage location on each user, processing is asynchronous, and nested groups are not supported for licensing.

![licencia por grupo](capturas/05-licencia-por-grupo.png)

### 3. External collaboration (B2B)

Invited an external guest with a personal email and reviewed the external collaboration settings: invitation restrictions, guest access levels and domain allow/deny lists.

![invitado](capturas/06-invitado.png)

![colaboracion externa](capturas/07-colaboracion-externa.png)

### 4. Roles and RBAC

Delegated the User Administrator role and tested its limits.

**Key point:** a User Administrator cannot reset a Global Administrator's password nor assign roles.

![rol admin usuarios](capturas/08-rol-admin-usuarios.png)

![limites rol](capturas/09-limites-rol.png)

### 5. Administrative units

Scoped an administrator to an administrative unit and compared access before and after.

**Pitfall:** permissions are additive. A role assigned tenant-wide overrides the administrative unit scope.

![au antes](capturas/10-au-antes.png)

![au despues](capturas/11-au-despues.png)

### 6. Self-service password reset (SSPR)

Enabled SSPR for a selected group and reviewed the methods.

**Key points:** administrators always need two methods, and the available methods are managed in the Authentication methods policy, not on the SSPR page.

![sspr](capturas/12-sspr.png)

![sspr metodos](capturas/13-sspr-metodos.png)

### 7. Emergency (break-glass) account

Created a cloud-only Global Administrator for emergencies, to be excluded from Conditional Access policies.

![cuenta emergencia](capturas/14-cuenta-emergencia.png)

### 8. Conditional Access

Built a policy requiring MFA for lab users. Started in report-only mode, checked the results and the What If tool, then switched it on.

**Key point:** report-only lets you see the impact before enforcing.

![ca solo informe](capturas/15-ca-solo-informe.png)

![ca informe ana](capturas/16-ca-informe-ana.png)

![ca que pasa si](capturas/17-ca-que-pasa-si.png)

![ca activada](capturas/18-ca-activada.png)

### 9. Privileged Identity Management (PIM)

Made a user eligible for a privileged role instead of permanent, with activation settings: duration, MFA and justification. Activated the role and verified it became active for a limited time.

![pim configuracion](capturas/19-pim-configuracion.png)

![pim elegible](capturas/20-pim-elegible.png)

![pim activacion](capturas/21-pim-activacion.png)

![pim resultado](capturas/22-pim-resultado.png)

![pim rol activo](capturas/23-pim-rol-activo.png)

### 10. Identity Protection

Simulated a sign-in from an anonymous IP (Tor browser), observed the two real-time risk detections (anonymous IP and malicious IP), enforced a risk-based Conditional Access policy and remediated the risk.

![id protection](capturas/24-id-protection.png)

![ca riesgo inicio](capturas/25-ca-riesgo-inicio.png)

![riesgo lista](capturas/26-riesgo-lista.png)

![riesgo detalle](capturas/27-riesgo-detalle.png)

![ca02 resultado](capturas/28-ca02-resultado.png)

![riesgo corregido](capturas/29-riesgo-corregido.png)

### 11. Access reviews

Created a review of a group's membership, completed it as a reviewer and checked the results and audit trail.

**Problems found:** the *if reviewers don't respond* setting automatically removed an unreviewed user, and applying the results stayed stuck for hours.

![revision acceso](capturas/30-revision-acceso.png)

![revision luis](capturas/31-revision-luis.png)

![revision resultados](capturas/32-revision-resultados.png)

![revision auditoria](capturas/33-revision-auditoria.png)

### 12. Entitlement management

Created an access package with approval. A user requested access, a second user approved it and access was granted.

**Problem found:** the request failed until *Self* (own account) was enabled in *who can request access*.

![paquete acceso](capturas/34-paquete-acceso.png)

![solicitud eva](capturas/35-solicitud-eva.png)

![aprobacion luis](capturas/36-aprobacion-luis.png)

![eva vuelve](capturas/37-eva-vuelve.png)

### 13. Terms of use

Created terms of use from a PDF and required them through Conditional Access.

**Problem found:** the terms did not appear until the policy used *Require all the selected controls* instead of *Require one of the selected controls*.

![terminos de uso](capturas/38-terminos-de-uso.png)

![ca01 terminos](capturas/39-ca01-terminos.png)

![terminos aceptar](capturas/40-terminos-aceptar.png)

![ca01 controles](capturas/41-ca01-controles.png)

### 14. App registrations and consent

Registered an application, created a client secret, added delegated and application permissions and granted admin consent. Reviewed the user consent settings and the consent flow.

![registro app](capturas/42-registro-app.png)

![secreto](capturas/43-secreto.png)

![permisos antes](capturas/44-permisos-antes.png)

![permisos concedidos](capturas/45-permisos-concedidos.png)

![consentimiento usuario](capturas/46-consentimiento-usuario.png)

![flujo consentimiento](capturas/47-flujo-consentimiento.png)

### 15. Workload identities

Created a managed identity with an Azure RBAC role and a federated credential for GitHub Actions (OIDC), so no secrets need to be stored.

![identidad administrada](capturas/48-identidad-administrada.png)

![entidad servicio mi](capturas/49-entidad-servicio-mi.png)

![rbac identidad](capturas/50-rbac-identidad.png)

![credencial federada](capturas/51-credencial-federada.png)

### 16. Authentication methods and Temporary Access Pass

Enabled the Temporary Access Pass in the authentication methods policy, created a one-time code for a user and signed in with it.

**Key points:** it counts as strong authentication, works once or several times depending on how it is created, and is typed in the password field.

![metodos autenticacion](capturas/52-metodos-autenticacion.png)

![tap creado](capturas/53-tap-creado.png)

![inicio con tap](capturas/54-inicio-con-tap.png)

### 17. Sign-in and audit logs

Reviewed the sign-in logs (authentication details and Conditional Access tabs) and the audit log entry for the creation of the Temporary Access Pass.

![registros inicio sesion](capturas/55-registros-inicio-sesion.png)

![detalle tap](capturas/56-detalle-tap.png)

![auditoria tap](capturas/57-auditoria-tap.png)

### 18. Log Analytics and KQL

Sent Entra sign-in and audit logs to a Log Analytics workspace and queried them with KQL. A role was granted at the subscription level to the lab administrator first.

**Notes:** only new events are exported, times are in UTC, and result code `50074` means MFA was required, not that the password failed.

![asignacion rol azure](capturas/58a-asignacion-rol-azure.png)

![configuracion diagnostico](capturas/58-configuracion-diagnostico.png)

![kql inicios fallidos](capturas/59-kql-inicios-fallidos.png)

![kql auditoria](capturas/60-kql-auditoria.png)

## Author

Juan Melo Torres · [GitHub](https://github.com/jmelo-sec) · [LinkedIn](https://www.linkedin.com/in/juan-melo-torres)

Status: studying for the SC-300 exam.
