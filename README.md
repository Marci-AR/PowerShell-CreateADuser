# PowerShell-Create AD User
Cómo crear usuarios en Directorio Activo con PowerShell desde un archivo<br>
How to create AD users by powershell from file

Este es un script básico para crear masivamente usuarios en AD desde un archivo .csv con los datos necesarios para darlos de alta..

# Lista de propiedades

A continuación listo las propiedades que podemos incluir en nuestro script (puedes consultarlo poniendo help New-ADUser en PS). En la lista podemos ver el nombre de la propiedad seguido del tipo de dato que acepta la propiedad: <br>

<pre><code>[-Name] &lt;String&gt;
[-AccountExpirationDate &lt;DateTime&gt;]
[-AccountNotDelegated &lt;Boolean&gt;]
[-AccountPassword &lt;SecureString&gt;]
[-AllowReversiblePasswordEncryption &lt;Boolean&gt;]
[-AuthenticationPolicy &lt;ADAuthenticationPolicy&gt;]
[-AuthenticationPolicySilo &lt;ADAuthenticationPolicySilo&gt;]
[-AuthType {Negotiate | Basic}]
[-CannotChangePassword &lt;Boolean&gt;]
[-Certificates &lt;X509Certificate[]&gt;]
[-ChangePasswordAtLogon &lt;Boolean&gt;]
[-City &lt;String&gt;]
[-Company &lt;String&gt;]
[-CompoundIdentitySupported &lt;Boolean&gt;]
[-Country &lt;String&gt;]
[-Credential &lt;PSCredential&gt;]
[-Department &lt;String&gt;]
[-Description &lt;String&gt;]
[-DisplayName &lt;String&gt;]
[-Division &lt;String&gt;]
[-EmailAddress &lt;String&gt;]
[-EmployeeID &lt;String&gt;]
[-EmployeeNumber &lt;String&gt;]
[-Enabled &lt;Boolean&gt;]
[-Fax &lt;String&gt;]
[-GivenName &lt;String&gt;]
[-HomeDirectory &lt;String&gt;]
[-HomeDrive &lt;String&gt;]
[-HomePage &lt;String&gt;]
[-HomePhone &lt;String&gt;]
[-Initials &lt;String&gt;]
[-Instance &lt;ADUser&gt;]
[-KerberosEncryptionType {None | DES | RC4 | AES128 | AES256}]
[-LogonWorkstations &lt;String&gt;]
[-Manager &lt;ADUser&gt;]
[-MobilePhone &lt;String&gt;]
[-Office &lt;String&gt;]
[-OfficePhone &lt;String&gt;]
[-Organization &lt;String&gt;]
[-OtherAttributes &lt;Hashtable&gt;]
[-OtherName &lt;String&gt;]
[-PassThru]
[-PasswordNeverExpires &lt;Boolean&gt;]
[-PasswordNotRequired &lt;Boolean&gt;]
[-Path &lt;String&gt;]
[-POBox &lt;String&gt;]
[-PostalCode &lt;String&gt;]
[-PrincipalsAllowedToDelegateToAccount &lt;ADPrincipal[]&gt;]
[-ProfilePath &lt;String&gt;]
[-SamAccountName &lt;String&gt;]
[-ScriptPath &lt;String&gt;]
[-Server &lt;String&gt;]
[-ServicePrincipalNames &lt;String[]&gt;]
[-SmartcardLogonRequired &lt;Boolean&gt;]
[-State &lt;String&gt;]
[-StreetAddress &lt;String&gt;]
[-Surname &lt;String&gt;]
[-Title &lt;String&gt;]
[-TrustedForDelegation &lt;Boolean&gt;]
[-Type &lt;String&gt;]
[-UserPrincipalName &lt;String&gt;]
[-Confirm]
[-WhatIf]
[&lt;CommonParameters&gt;]</code></pre>

Tomamos como ejemplo la primera propiedad y vemos:<br>
<pre><code>[-Name](propiedad) &lt;String&gt;(tipo de dato, en este caso String)</code></pre>

# Creando el script
Lo primero que tenemos que hacer es importar el modulo de Directorio Activo
<pre><code>Import-Module ActiveDirectory</code></pre>

Aunque sea un script básico, a mi me gusta definir la ruta y el archivo de origen en una variable. En este caso vamos a usar un archivo .csv como origen de los datos que necesitaremos para crear los usuarios. <br>
Empezamos indicando cual será el directorio de origen y para este script elegiremos que el directorio sea el mismo donde se encuentra nuestro archivo .ps1. Para ello usaremos la variable automática de powershell $PSScriptRoot y lo meteremos en la variable $directorio_origen:
<pre><code>$directorio_origen = $PSScriptRoot</code></pre>
Y ahora le decimos cómo se llamará el archivo de donde cargaremos los datos y lo meteremos en la variable $archivo_origen concatenado con un "+" el valor de la variable $directorio_origen con un string con el nombre que queramos ponerle al archivo precedido de "\\" para que complete la dirección del archivo:
<pre><code>$archivo_origen = $directorio_origen+"\users.csv"</code></pre>
