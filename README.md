# HadronterapyG4
Repositorio para recolectar el codigo de simulacion de hadronterapia 

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
Antes de correr la simulación se debe ejecutar el script de configuración inicial y despues cargar los datos de liberias, este paso se debe realizar cada que quiera correr la simulación en una terminal nueva.

```
source ../../../configurar_geant4_v10.sh
. ../../../data.sh 
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

Después se modifica únicamente la siguiente línea y se guarda el archivo

```
/gps/ene/mono 60.0 MeV
```

Para posteriormente correr la simulación, al terminar de correr este generará varios archivos, nos concentraremos en el llamado Dose.out.
Renombrar el archivo con el siguiente nombre Dose_"Valor de enegía inicial".out, es decir, para este primer ejemplo será Dose_60.out.
El código para renombrar el archivo es el siguiente:

```
mv Dose.out Dose_60.out
```

Repetir estos últimos 2 pasos para enegías iniciales de 50, 70 y 90.

## Análisis en Python

Estos 4 archivos de salida son archivos csv y los graficaremos para ver su comportamiento, par esto primero copiamos la carpeta en donde ya está el código realizado.

```
cp /LUSTRE/home/ccd/HadronterapyG4/Codigos/Analisis-A .
```

Ahora corremos el código para poder visualizar la gráfica.



