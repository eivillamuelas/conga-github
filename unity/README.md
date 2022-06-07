# MlAgents - Unity

[Instrucciones originales](https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Installation.md)

## Instalar **Unity 2018.4** o posterior

[Descargar](https://unity3d.com/get-unity/download) e instalar Unity.

## Instalar **Python 3.6.1** o superior

Se recomienda [instalar](https://www.python.org/downloads/) Python 3.6 o 3.7.
Si usas Windows, instala la version x86-64 y no x86.
si tu ambiente Python no incluye `pip3`, mira estas [instrucciones](https://packaging.python.org/guides/installing-using-linux-tools/#installing-pip-setuptools-wheel-with-linux-package-managers) para instalarlo.

## Instalar **Anaconda**

### 1. crear un ambiente en Anaconda (enviroments o env)

```sh
conda create -n <venv name> python=3.8
conda activate <venv name>
```

### 2. instalar pytorch
  
```sh
pip3 install torch~=1.7.1 -f https://download.pytorch.org/whl/torch_stable.html
```
  
### 3. instalar mlagents
  
```sh
python -m pip install mlagents==0.28.0
```

Si da el siguiente error:

```sh
TypeError: Descriptors cannot not be created directly.
If this call came from a _pb2.py file, your generated code is out of date and must be regenerated with protoc >= 3.19.0.
If you cannot immediately regenerate your protos, some other possible workarounds are:
 1. Downgrade the protobuf package to 3.20.x or lower.
 2. Set PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python (but this will use pure-Python parsing and will be much slower).

More information: https://developers.google.com/protocol-buffers/docs/news/2022-05-06#python-updates
```

será necesario instalar la version 3.20.0 del protobuf

```sh
pip install protobuf==3.20.0
```

### 4. comprobar que la instalación es correcta con el comando `mlagents-learn --help`

## Abrir Unity

### 1. Instalar `com.unity.ml-agents` Unity package

Instalar el programa directamente en Unity.
[Intrucciones de instalación](https://docs.unity3d.com/Manual/upm-ui-install.html)

### 2. Crear escena

### 3. Entrenamiento

A. abrir ambiente de Anaconda donde hemos instalado pytorch y mlagents

B. crear o descargar archivo de configuración .yaml [config](https://github.com/Unity-Technologies/ml-agents/tree/main/config). No es necesario que esté en la misma carpeta del proyecto de unity

C. redirigir anaconda a la carpeta donde se encuantra la configuración 

```sh
cd [PATH]
```

D. iniciar el aprendizaje

```sh
mlagents-learn ./trainer_config.yaml --run-id 24_agents_gpuOn_5M
```

si usamos `--run-id` indicaremos el id del entrenamiento. Si no se ha hecho un entrenamiento anterior con ese id el proceso se iniciará. Si ya existiese uno previo no empezaráy tendremos dos opciones, o sobreescribirlo con el comando `--force` o continuar el entrenamiento con `--resume`.

C. observar el entrenamiento en Tensorboard

abrir otro terminal en el directorio de la configuración (donde se encuentra el archivo .yaml) y acceder al localhost.

```sh
cd [PATH]
conda activate [ENV_NAME]
tensorboard --logdir results
```
