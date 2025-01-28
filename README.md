# HadronterapyG4
Repositorio para recolectar el codigo de simulacion de hadronterapia 

## Clonar el repositorio en el servidor 
```
git clone https://github.com/castaned/HadronterapyG4
```
## Entrar a la carpeta HadronterapyG4 y crear una carpeta build para compilar el codigo 
```
mkdir build
cd build
```
Dentro del directorio build ejecurar el siguiente comando para compilar

```
cmake3 -DGeant4_DIR=/storage/apps/c6320/geant4/geant4-10.06.p03/lib64/Geant4-10.6.3/ ../hadrontherapy/
```

Una vez se compila, se crea el siguiente ejecutable con el comando make

```
make -j4
```
Antes de correr la simulación se debe ejecutar el script de configuración inicial y despues cargar los datos de liberias, este paso se debe realizar cada que quiera correr la simulación en una terminal nueva.

```
source ../configurar_geant4_v10.sh
. ../data.sh
```

Finalmente usar el ejecutable para correr simulación, en este caso tomará la configuración por default (no visualización) , solo checar que funciona y después salir con los siguientes comandos

Para correr la simulación:

```
./hadrontherapy
```

Para salir de la simulación:

```
exit
```

Para poder visualizar la simulación debemos hacer uso de los archivos de configuracion en este caso se encuentran en el directorio macro y hacemos uso del basico para poder visualizar.

```
./hadrontherapy  macro/defaultMacro_vis.mac
```




