# Guía de configuración de Fedora 43

## 👋 Hola!
Si estás leyendo esta guía, probablemente tengas dudas acerca
del que hacer luego de haber instalado tu sistema, pero no te
preocupes, aquí te voy a mostrar de forma sencilla los pasos a
seguir para que tu sistema sea actualizado y funcional.

## 🔥 Primeros pasos - RPM Fusion
De las primeras cosas que debes hacer al instalar Fedora es
habilitar los repositorios RPM Fusion, que te permitiran
instalar software propietario (codecs, drivers, etc...)
Lo que resulta principalmente útil para las personas con
hardware Nvidia o AMD.
```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/
rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https:/
/mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-
release-$(rpm -E %fedora).noarch.rpm

sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
```

## ✅ Actualizaciones
Las actualizaciones son de las cosas más importantes a tener
en cuenta tu sistema, ya que permitiran mantener el software
actualizado.
```
sudo dnf update -y
```
> 💡 **Tip:** Considera el ejecutar `sudo dnf update` una vez
cada mes o semana :)

## 📦 Flathub
Fedora viene ya con un repositorio de Flatpak's preinstalado,
pero es algo límitado por lo que es recomendable habilitar
Flahub para sí tener mucha más disponibilidad de software.
```
flatpak remote-add --if-not-exists flathub https://dl.flathub
.org/repo/flathub.flatpakrepo
```

## 🎵 Multimedia y Codecs
Este es un paso importante porque te permitirá poder reproducir
la mayoría de audios y videos, así también como activar la
**Aceleración de Hardware**.

### Instalación de ffmpeg y gstreamer
```
sudo dnf swap ffmpeg-free ffmpeg --allowerasing

sudo dnf update @multimedia --setopt="install_weak_deps=False"
 --exclude=PackageKit-gstreamer-plugin
```

### Aceleración de Hardware Intel
```
sudo dnf install intel-media-driver libva-intel-driver
```

### Instalación de Mesa
```
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld
```

### Codecs de NVIDIA
```
sudo dnf install libva-nvidia-driver
```

## 🧹 Limpieza del Sistema
Luego de haber realizado todos estos pasos, solo queda limpiar
la caché que pudieran haber dejado algunas actualizaciones o
instalación de paquetes, con estos dos sencillo comandos podrás
hacer esto mismo de una forma rápida.
```
sudo dnf autoremove -y

sudo dnf clean all
```

## 👋 Gracias!
Esta guía fue hecha con ❤️ amor, con el propósito de facilitar
la tarea de configurar Fedora, eres libre de compartir y modificar
esta guía bajo la licencia **GNU General Public License v3.0**
