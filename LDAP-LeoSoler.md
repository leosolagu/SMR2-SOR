# OpenLDAP

## INSTALACIÓN LDAP (Ubuntu Server)
NOTA IMPORTANTE: debemos de haber configurado previamente nuestra configuracion IP tal como muestra en la captura.
<img width="961" height="179" alt="imagen" src="https://github.com/user-attachments/assets/d1e3bfe9-0cf2-403c-9ad0-3459e9e1ee19" />

Deberemos instalar el servicio con el siguiente comando: sudo apt install slapd ldap-utils
<img width="685" height="128" alt="imagen" src="https://github.com/user-attachments/assets/272644e0-d8e8-467c-ad26-ca045f0efee1" />

Acceremos al directorio /etc/hosts y configuraremos nuestro dominio, en mi caso será leo-dominio.cat.
NOTA: Durante la instalación deberemos ingresar la contraseña de administrador.
<img width="963" height="184" alt="imagen" src="https://github.com/user-attachments/assets/0d3233f8-2fe3-4ddb-8934-82675f6a42aa" />

## Configuración de LDAP (Ubuntu Server)

Para acceder a la configuración de LDAP deberemos poner el siguiente comando "Sudo dpkg-reconfigurar slapd"
<img width="763" height="172" alt="imagen" src="https://github.com/user-attachments/assets/ce3739ad-6ef2-4f03-865f-737a49084166" />

Nos aparecerá lo siguiente, que nos preguntará si queremos omitir la configuración le daremos que NO.

NOTA: le dí sin querer a siguiente y no pude hacerle captura
En el siguiente apartado deberemos poner el nombre del dominio que configuramos anteriormente.

Ahora deberemos darle nombre a nuestra organización, en mi caso lo llame "leo-dominio"
<img width="1173" height="693" alt="imagen" src="https://github.com/user-attachments/assets/320c04ea-4cff-468b-a551-6732912c2a25" />

Si le damos a continuar o OK, tendremos que ingresar la contraseña de administrador (La deberemos poner dos veces para confirmarla)
<img width="1169" height="487" alt="imagen" src="https://github.com/user-attachments/assets/5500db2f-7bc9-485b-8b65-e31708e78956" />

La siguiente pestaña nos dará la opción de eliminar la base de datos anterior, está bien si hubiesemos tenido una, pero como en mi caso no tengo ninguna, le daré a que no.
<img width="1166" height="345" alt="imagen" src="https://github.com/user-attachments/assets/c9e66b08-0dc8-4a25-911b-4f561a480af3" />

 En el caso de que le des a que no, te advertira de que tendrá que mover los datos de la antigua base de datos a la nueva. Le daremos SI
<img width="1160" height="248" alt="imagen" src="https://github.com/user-attachments/assets/255bcd14-6fa5-4b02-b1b8-67f828e7bbe0" />



NOTA: tuve un error y el dominio debería haberse llamado prova-ioc.cat. No me dí cuenta, pero el procedimiento es el mismo. Obviamente.




