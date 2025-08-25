# VM-ubuntuserver-jammyjellyfish
**Buenos días**. Bienvenidos a mi repositorio sobre **Ubuntu Server** que he decidido crear en una VM y que estará basado en _Ubuntu Server 22.4.5 LTS (Jammy Jellyfish)_. Y que para ello usaremos **Oracle VirtualBox**.

## Creación de la máquina virtual

-Como no tenemos acceso a este software directamente en los repositorios de **Fedora 42 Workstation** encontré un blog donde explicaba paso a paso cómo instalarlo [Opçao Linux](https://www.blogopcaolinux.com.br/2016/03/instalando-oracle-virtualbox-no-fedora.html), añadiendo la clave pública de Oracle y las dependencias necesarias.
Fedora ya cuenta con un programa que nos permite hacer Máquinas Virtuales de una manera sencilla llamado _Boxes_, sin embargo prefiero usar Virtual Box que parece más profesional.
Ahora, nos bajamos la imagen .iso de [Ubuntu](https://ubuntu.com/download/alternative-downloads) <-Recordad que buscamos la versión 22.04.5 LTS. Seguidamente abrimos Oracle Virtual Machine.

-A nuestra VM [le vamos a poner el nombre de "MYLABS-UbuntuServer"](VMachine/instalacion/1.png). Seleccionamos la imagen que hemos almacenado e importante: Marcamos la casilla de "Skip unattended installation".Le ponemos de [base de memoria 2048 MB y 2 CPUs](VMachine/instalacion/2.png). No activamos EFI (en el caso de mi PC que funciona así).
[Le damos 25 GB .vdi](VMachine/instalacion/3.png), esto hace que el volumen se llame el nombre de nuestra máquina virtual+vdi. Una vez creada, hacemos clic en: Settings y en Network->Adapter 1 estará activado automáticamente Enable Network Adapter y [dejamos seleccionado NAT](VMachine/instalacion/7.png).

-Hacemos clic en _Port Forwarding_ y [creamos las reglas SSH, HTTP y HTTPS](VMachine/instalacion/4.png), creando así puertas desde nuestro host a la VM en modo NAT.

-A partir de aquí pongo una serie de pantallazos del proceso de instalación: [Paso 1](VMachine/instalacion/8.png), [Paso 2](VMachine/instalacion/9.png), [Paso 3](VMachine/instalacion/10.png),[Paso 4](VMachine/instalacion/11.png), [Paso 5](VMachine/instalacion/14.png), [Paso 6](VMachine/instalacion/13.png), [Paso 7](VMachine/instalacion/15.png).
Comento lo que hemos hecho: Una vez iniciada entrar en "Try or install Ubuntu Server"-> English (lo suelo poner en inglés porque a veces instalando otros idiomas se crean bugs)-> No, no queremos instalar la nueva versión de Ubuntu. Establecemos nuestro teclado español-> Ubuntu Server (minimized). Y luego tanto la configuración de red como el proxy los dejamos tal cual, presionamos en "done" y "done". Vemos que tenemos acceso a nuestra réplica y después de que se valide le damos a hecho.

-[Paso 8](VMachine/instalacion/16.png), [Paso 9](VMachine/instalacion/17.png), [Paso 10](VMachine/instalacion/18.png).
Seleccionamos "Use an entire disk y Set up this disk as an LVM Group" y hubiera dejado la configuración tal cual pero me dí cuenta de que si lo dejaba así si algún día necesito que el dispositivo ubuntu-lv, montado en /(la raíz) que sería donde guardaría el sistema base y algunos contenedores de Docker quizá no tendría suficiente espacio. Entonces pasamos de 10G a 20G. Le pongo de nombre a mi servidor *"mylabsubuntu"* y creo mi usuario.

-[Paso 11](VMachine/instalacion/20.png), [Paso 12](VMachine/instalacion/21.png), [Paso 13](VMachine/instalacion/22.png), [Paso 14](VMachine/instalacion/24.png). Luego en OracleVM, vamos a Settings-> Storage y donde dice Devices: Controller IDE, [borramos la imagen de Ubuntu](VMachine/instalacion/6.png) ya que si iniciásemos la VM otra vez nos saltaría el asistente para instalar Ubuntu Server.

-La iniciamos y por ahora parece que [se nos ejecuta automáticamente cloud-init](VMachine/instalacion/25.png), no le hacemos caso y le damos a enter, esto nos pedirá nuestro [usuario y nuestra contraseña](VMachine/instalacion/26.png).
-Para solucionar el tema de _cloud-init_, creamos un archivo en _/etc/cloud_ para desactivarlo llamado [cloud-init.disabled](VMachine/instalacion/28.png). Con el comando: sudo _touch /etc/cloud/cloud-init.disabled_. Así no lo borramos por si en alguna ocasión lo volvemos a necesitar reiniciamos y vemos que ya [inicia sin este proceso automático](VMachine/instalacion/29.png).

