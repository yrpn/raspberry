# Alapok

## Telepítendő csomagok
`ntfs-3g`, `ufw`

## Ntfs külső HDD csatlakoztatása
Létrehozunk egy mappát, ahova a felcsatolás történik majd
```bash
sudo mkdir /mnt/hdd
```

Megkeressük a felcsatolandó meghajtót
```bash
sudo fdisk -l
```
A lehetséges nevek pl `/dev/sda1`, `/dev/sda2`, …,vagy `/dev/sdb1`, `/dev/sdb2`, …

Ezek után meg kell keresni a meghajtóhoz tartozó egyedi azonosítót **UUID**-t
```bash
sudo blkid
```

Az automatikus csatoláshoz szerkesztenünk kell egy fájlt a rendszerben
```bash
sudo nano /etc/fstab
```

A fájl legvégére beírjuk a következő sort azzal a **UUID** értékkel amit az előző parancsban megkaptunk
```
UUID=10BE83A5BE8381C8 /mnt/hdd ntfs-3g defaults,async,noatime,big_writes,nofail 0 0
```

Szerkesztést követően a <kbd>CTRL</kbd>+<kbd>X</kbd> parancs kiadását követően a felülírást választva elmentjük a fájlt

Ellenőrzésképpen futtassuk az alábbi parancsot, hogy a felcsatolás megtörténik-e
```bash
sudo mount -a
```

Hiba nélküli lefutás után ellenőrizhetjük, hogy a meghajtónk ténylegesen csatolva lett-e
(ez a parancs minden meghajtó információit tartalmazza)
```bash
sudo df -h
```

## Docker
### Docker telepítés
```bash
curl -sSL https://get.docker.com | sh

sudo usermod -aG docker $USER
```
### Portainer install
```bash
docker pull portainer/portainer-ce:latest

docker volume create portainer_data

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
