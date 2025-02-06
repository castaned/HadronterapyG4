# HadronterapyG4
Repositorio para recolectar el codigo de simulacion de hadronterapia 

## Entrar al servidor ACARUS 

Antes de correr la simulación se debe ejecutar el script de configuración inicial y despues cargar los datos de liberias, este paso se debe realizar cada que quiera correr la simulación en una terminal nueva.

```
source configurar_geant4_v10.sh
. data.sh 
```

## Clonar el repositorio en el servidor 
```
git clone https://github.com/castaned/HadronterapyG4
```
Entrar a la carpeta HadronterapyG4 para crear la siguiente carpeta

```
cd HadronterapyG4
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
si arroja error tratar de volver a hacer el setup de Geant4 de nueva cuenta 

```
source /storage/apps/c6320/geant4/geant4-10.06.p03/bin/geant4.sh
```

Una vez se compila, se crea el siguiente ejecutable con el comando make

```
make -j4
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

# Primer análisis

## Para empezar se abre el archivo de visuacilación (desde la carpeta build) con el siguiente código para poder modificar el archivo sin necesidad de cerrarlo

```
emacs macro/defaultMacro_vis.mac &
```

## A partir de aquí se va modicar el ese mismo macro 3 veces variando la energía inicial.

Primero se corre el macro sin modificaciones(el cual tendrá una energía inicial de 60 MeV) con el siguiente código

```
./hadrontherapy  macro/defaultMacro_vis.mac
```
Nos enfocaremos solamente en un archivo de salida llamado "Dose.out", para esto cambiaremos el nombre para identificar cada archivo de salida.
Renombraremos el archivo con el siguiente orden Dose_"Valor de enegía inicial".out, es decir, para este primer ejemplo será Dose_60.out.
El código para renombrar el archivo es el siguiente:

```
mv Dose.out Dose_60.out
```

Ahora modificaremos la siguiente línea del archivo macro(que debería seguir abierto) para cambiar a una energía inicial de 50 MeV:

```
/gps/ene/mono 50.0 MeV
```
Esto volverá a generar un archivo de salida "Dose.out" por lo que se tendrá que renombrar(siguiendo la secuencia) para un posterior análisis con el siguiente código:

```
mv Dose.out Dose_50.out
```

Repetir estos últimos 2 pasos para enegías iniciales de 70 y 90, para finalmente tener 4 archivos de salida "Dose_50.out", "Dose_60.out", "Dose_70.out" y "Dose_90.out" 

## Análisis en Python

Estos 4 archivos de salida son archivos csv y los graficaremos para ver su comportamiento, para poder acceder al código primero cambiaremos de directorio a la carpeta llamada "Codigos" 

```
cd ../../Codigos/
```

Después ejecutaremos lo siguiente

```
jupyter notebook Analisis-A.ipynb
```

Ahora corremos el código para poder visualizar la gráfica.

![Analisis_A](https://github.com/user-attachments/assets/08cf64b5-2fec-4488-ac24-cd4c63fb0d83)

## Segundo Análisis 

Para este segundo análisis se van a variar los niveles de energía de la misma forma que en primer análisis, solo que este caso las dimensiones del detector y del voxel van a ser 
incrementadas.
Primero se regresa a la carpeta build, si está en la carpeta codigos utilizar el siguiente comando

```
cd ../Hadrontherapy/build
```

Posteriormente se tiene que modificar el macro "defaultMacro_vis.mac", ejecute el siguiente comando para abrir modificar dicho archivo sin tener que cerrarlo:

```
emacs /macro/defaultMacro_vis.mac &
```

Una vez abierto el macro modificar la siguiente línea:

```
/changeDetector/size 8 8 8 cm
/changeDetector/voxelSize .2 80 80 mm
```

Realizado este cambio se procederá a cambiar de nuevo la energía inicial de la misma manera que la primera parte, variandolo así de 50 MeV, 60 MeV, 70MeV y 90 MeV.

