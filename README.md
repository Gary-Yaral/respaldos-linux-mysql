
# respaldos-linux-mysql 
Primero que nada necesitamos tener un editor de texto y para eso usaremos nano
## Instalación en CENTOS / RHEL
``` Console
  sudo yum install nano
```
o
``` Console
  sudo install nano
```

## IMPORTANTE!!
Deben tener instalado mysql o mariadb en su linux para poder ejecutar mysqldum

## Creación de un archivo .sh
``` Console
  sudo nano respaldo.sh
```
Al ejecutar el comando anterior se abrirá nano y podremos editar nuestro archivo de respaldo

## Contenido del archivo respaldo.sh
```
usuario=yaral
rutacarpeta=respaldos
ruta=/home/${usuario}/${rutacarpeta}
fecha=`date "+%d-%m-%y_%H-%M-%S"`
archivo=${ruta}/mirespaldo_${fecha}.sql
mipassword=""
echo $archivo
if [ -d $ruta ]; then
        echo "La carpeta existe"
        if [ -f /${archivo} ]; then
                rm -r $archivo
                mysqldump -u root --password=$mipassword $db > $archivo
        else
                mysqldump -u root --password=$mipassword $db > $archivo
        fi
else
        echo "La carpeta no existe"
        mkdir  $ruta
        mysqldump -u root --password=$mipassword $db > $archivo
fi


```

Luego, le tenemos que dar todos los permisos para que se pueda ejecutar

``` Console
  sudo chmod +x respaldo.sh
```
para ejecutarlo
```
  sudo ./respaldo.sh
```

## Crontab
```
    crontab -e
```

Una vez ejecutado ese comando podremos configurar cuando se ejecutará nuestro script


