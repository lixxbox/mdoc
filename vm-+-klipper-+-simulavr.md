# VM + Klipper + simulavr

## VM aufsetzen

Virtualbox, Netzwerk -&gt; Bridgemode  
Frisches debian, kein root-pw.

**Denk an Snapshots, du Depp!**

## Klipper und Moonraker mit Kiauh installieren

```text
cd ~
git clone https://github.com/th33xitus/kiauh.git
cd kiauh/
git checkout kiauh-rework
./kiauh.sh
```

Mehrere Klipper und Moonraker Instanzen anlegen.

## Simulavr

```text
sudo apt-get install cmake swig
```

```text
cd ~
git clone git://git.savannah.nongnu.org/simulavr.git
cd simulavr/
make python
make build

cd ~/klipper
make menuconfig
```

* Enable extra low-level configuration options \[✔\]
* Micro-controller Architecture \[Atmega AVR\]
* Processor model \[atmega644p\]
* Processor speed \[20Mhz\]
* Compile for simulavr software emulation \[✔\]

\[Q\]uit  
Save \[Y\]es

```text
make
```

Der Befehl wird im Klipper Verzeichnis ausgeführt muss laufen. -&gt;&gt; Service ??

```text
PYTHONPATH=~/simulavr/build/pysimulavr/ ./scripts/avrsim.py -m atmega644 -s 20000000 -b 250000 out/klipper.elf
```

## moonraker.conf anpassen

cors\_domain anpassen. `http://<ip>` hinzufügen, wo die mainsail Dateien liegen \(z.B. vom pi im LAN\).

## printer.cfg anpassen

### Klipper Beispielkonfig "simulavr":

{% embed url="https://github.com/KevinOConnor/klipper/blob/master/config/generic-simulavr.cfg" %}

### Mainsail

{% embed url="https://docs.mainsail.app/necessary-configuration" %}



```text
sudo /bin/sh -c "cat > /etc/systemd/system/simulavr.service" << EOF
#Systemd service file for simulavr
[Unit]
Description=Starts simulavr on startup
After=network.target
[Install]
WantedBy=multi-user.target
[Service]
Type=simple
RemainAfterExit=yes
ExecStart=PYTHONPATH=~/simulavr/build/pysimulavr/ ./scripts/avrsim.py -m atmega644 -s 20000000 -b 250000 out/klipper.elf
Restart=always
RestartSec=10
EOF
}
```

