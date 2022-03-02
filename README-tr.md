[![Docker Çekimleri](https://img.shields.io/docker/pulls/teamcyberless/cyberless3onlineserver.svg)](https://hub.docker.com/r/teamcyberless/cyberless3onlineserver)
[![Imaj Boyutu](https://img.shields.io/docker/image-size/teamcyberless/cyberless3onlineserver/latest.svg)](https://hub.docker.com/r/teamcyberless/cyberless3onlineserver)

| [English](https://github.com/TeamCyberless/CyberlessGameServer/blob/master/README.md) | [**Turkish**](https://github.com/TeamCyberless/CyberlessGameServer/blob/master/README-tr.md) |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |

# Cyberless III: Online Oyun Sunucusu

Cyberless III: Online, Çok oyunculu TPS nişancı karakter-bazlı oyundur. Bu depo şu anlık sadece Linux sunucusu barındırmaktadır.

Cyberless III: Online hakkında detaylı bilgi için [burayı](https://store.steampowered.com/app/1175540/Cyberless_III_Online/) ziyaret edebilir veya bize [e-posta](mailto:teamcyberless@gmail.com) gönderebilirsiniz.

## Etiketler

*   [`latest`](dockerfiles/latest/Dockerfile)

## Kullanım

### En son sürüm imajı çekmek için
```shell
docker pull teamcyberless/cyberless3onlineserver:latest
```

### Test etmek için
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it teamcyberless/cyberless3onlineserver:latest
```

### Bazı oyun sunucusu parametreleri ile test etmek için
```
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it teamcyberless/cyberless3onlineserver:latest \
  ./CyberlessIIIOnline/Binaries/Linux/CyberlessIIIOnlineServer-Linux-Shipping \
  /Game/Maps/Training?ServerPassword=passwd?TimeLimit=20?GoalScore=330 -server -log -Messaging
```

### Birim ile çalıştırma (İlk olarak birim oluşturmalısınız)
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it \
  --user cyberless \
  --mount source=<volume name>,target=/opt/CyberlessIIIOnlineServer \
  teamcyberless/cyberless3onlineserver:latest
```

### Hepsi bir arada
```shell
docker run \ 
  -p 7777:7777/udp \
  -p 7777:7777/tcp \
  -p 27015:27015/udp \
  -p 27015:27015/tcp \
  -it \
  --user cyberless \
  --mount source=<volume name>,target=/opt/CyberlessIIIOnlineServer \
  teamcyberless/cyberless3onlineserver:latest \
  ./CyberlessIIIOnline/Binaries/Linux/CyberlessIIIOnlineServer-Linux-Shipping \
  /Game/Maps/Training?ServerPassword=passwd?TimeLimit=20?GoalScore=330 -server -log -Messaging
```

## Kullanılan Portlar

* 7777 (TCP/UDP)
* 27015 (TCP/UDP)

## Sıklıkla kullanılan bazı parametreler

| **Parametre İsmi** | **Veri Tipi** | **Harita Parametresi** | **Açıklama**                                                                          | **Varsayılan Değer** |
| ------------------ | :-----------: | :--------------------: | ------------------------------------------------------------------------------------- | :------------------: |
| ServerPassword     |    string     |           ✔️            | Sunucuya giriş yapılırken sorulan şifre (boş değer şifre yok anlamına gelir).         |       *(boş)*        |
| TimeLimit          |    integer    |           ✔️            | Ekstra süre hariç toplam oyun süresi (0 sınırsız  oyun süresi demektir).              |    15 *(dakika)*     |
| GoalScore          |    integer    |           ✔️            | Takımların veya oyuncuların ulaşabileceği maksimum skor (0 değeri sınırsız demektir). |         300          |
| -LAN               |     bool      |           ❌            | Oyun sunucusunu lokalde başlatır                                                      | *(değer verilmemiş)* |