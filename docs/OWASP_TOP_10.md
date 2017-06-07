# OWASP TOP 10

OWASP Top 10 es un documento de los diez riesgos de seguridad más importantes en aplicaciones web según la organización OWASP (en inglés Open Web Application Security Project, en español Proyecto Abierto de Seguridad de Aplicaciones Web). Esta lista se publica y actualiza cada tres años por dicha organización.
El objetivo de este proyecto según la OWASP top 10(2013), es crear conciencia acerca de la seguridad en aplicaciones mediante la identificación de algunos de los riesgos más críticos que enfrentan las organizaciones.1 Así mismo estos riesgos de seguridad son referenciados en artículos científicos, tesis de pregrado y postgrado, libros de seguridad y organizaciones como MITRE,2 SANS, PCI DSS, DISA, FCT.


OWASP Top 10 fue lanzado por primera vez en 2003, con actualizaciones en 2004 y 2007. La versión 2010 fue renovada para dar prioridad al riesgo, no sólo a la prevalencia. La edición 2013 sigue el mismo enfoque.
Los documentos del OWASP top 10 comenzaron a publicarse desde el 2004, haciendo un total de cuatro actualizaciones hasta la fecha, estos son además del Owasp top 10-2004 el Owasp top 10-2007, Owasp top 10-2010 y Owasp top 10-2013.3 Hay una versión inicial del 2003 pero no hay detalles en la página del proyecto más que la lista de los riesgos de seguridad de ese entonces.

<hr>

<table class="wikitable">
<tbody><tr>
<th>OWASP Top 10-2003</th>
<th>OWASP Top 10-2004</th>
<th>OWASP Top 10-2007</th>
<th>OWASP Top 10-2010</th>
<th>OWASP Top 10-2013</th>
<th>OWASP Top 10-2016</th>
</tr>
<tr>
<td>A1-Entrada no validada</td>
<td>A1-Entrada no validada</td>
<td>A1-Secuencia de comandos en sitios cruzados <a href="/wiki/XSS" class="mw-redirect" title="XSS">XSS</a></td>
<td>A1-<a href="/wiki/Inyecci%C3%B3n_SQL" title="Inyección SQL">Inyección</a></td>
<td>A1-<a href="/wiki/Inyecci%C3%B3n_SQL" title="Inyección SQL">Inyección</a></td>
<td>A1 - Verify for Security Early and Often</td>
</tr>
<tr>
<td>A2-Control de acceso interrumpido</td>
<td>A2-Control de acceso interrumpido</td>
<td>A2-Fallas de <a href="/wiki/Inyecci%C3%B3n_SQL" title="Inyección SQL">inyección</a></td>
<td>A2-Secuencia de comandos en sitios cruzados <a href="/wiki/XSS" class="mw-redirect" title="XSS">XSS</a></td>
<td>A2-Pérdida de autenticación y gestión de sesiones</td>
<td>A2 - Parameterize Queries</td>
</tr>
<tr>
<td>A3-Administración de cuentas y sesión interrumpida</td>
<td>A3-Administración de autenticación y sesión interrumpida</td>
<td>A3-Ejecución de ficheros malintencionados</td>
<td>A3-Pérdida de autenticación y gestión de sesiones</td>
<td>A3-Secuencia de comandos en sitios cruzados <a href="/wiki/XSS" class="mw-redirect" title="XSS">XSS</a></td>
<td>A3 - Encode Data</td>
</tr>
<tr>
<td>A4-Fallas de cross site scripting <a href="/wiki/XSS" class="mw-redirect" title="XSS">XSS</a></td>
<td>A4-Fallas de cross site scripting <a href="/wiki/XSS" class="mw-redirect" title="XSS">XSS</a></td>
<td>A4-Referencia insegura y directa a objetos</td>
<td>A4-Referencia directa insegura a objetos</td>
<td>A4-Referencia directa insegura a objetos</td>
<td>A4 - Validate All Inputs</td>
</tr>
<tr>
<td>A5-Desbordamiento de bufer</td>
<td>A5-Desbordamiento de bufer</td>
<td>A5-Falsificación de peticiones en sitios cruzados <a href="/wiki/CSRF" class="mw-redirect" title="CSRF">CSRF</a></td>
<td>A5-Falsificación de peticiones en sitios cruzados <a href="/wiki/CSRF" class="mw-redirect" title="CSRF">CSRF</a></td>
<td>A5-Configuración de seguridad incorrecta</td>
<td>A5 - Implement Identity and Authentication Controls</td>
</tr>
<tr>
<td>A6-Fallas de inyección de comandos</td>
<td>A6-Fallas de inyección</td>
<td>A6-Revelación de información y gestión incorrecta de errores</td>
<td>6-Defectuosa configuración de seguridad</td>
<td>A6-Exposición de datos sensibles</td>
<td>A6 - Implement Appropriate Access Controls</td>
</tr>
<tr>
<td>A7-Problemas de manejo de errores</td>
<td>A7-Manejo inadecuado de errores</td>
<td>A7-Pérdida de autenticación y gestión de sesiones</td>
<td>A7-Almacenamiento criptográfico inseguro</td>
<td>A7-Ausencia de control de acceso a las funciones</td>
<td>A7 - Protect Data</td>
</tr>
<tr>
<td>A8-Uso inseguro de criptografía</td>
<td>A8-Almacenamiento inseguro</td>
<td>A8-Almacenamiento criptográfico inseguro</td>
<td>A8-Falla de restricción de acceso a URL</td>
<td>A8-Falsificación de peticiones en sitios cruzados <a href="/wiki/CSRF" class="mw-redirect" title="CSRF">CSRF</a></td>
<td>A8 - Implement Logging and Intrusion Detection</td>
</tr>
<tr>
<td>A9-Fallas de administración remota(no aplicable)</td>
<td>A9-Negación de servicio</td>
<td>A9-Comunicaciones inseguras</td>
<td>A9-Protección insuficiente en la capa de transporte</td>
<td>A9-Uso de componentes con vulnerabilidades conocidas</td>
<td>A9 - Leverage Security Frameworks and Libraries</td>
</tr>
<tr>
<td>A10-Configuración indebida de servidor web y de aplicación</td>
<td>A10-Administración de configuración insegura</td>
<td>A10-Falla de restricción de acceso a URL</td>
<td>A10-Redirecciones y reenvíos no validados</td>
<td>A10-Redirecciones y reenvíos no validados</td>
<td>A10 - Error and Exception Handling</td>
</tr>
</tbody></table>