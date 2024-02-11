
# Docker ve İlgili Araçların Kurulum Rehberi

Bu rehber, Ubuntu üzerinde Docker ve gerekli araçların nasıl kurulacağını adım adım anlatmaktadır.

## Sistem Güncellemesi

Öncelikle, mevcut paketlerinizi güncelleyerek başlayın:

```bash
sudo apt update -y && sudo apt upgrade -y
```

## Önceden Kurulu Paketlerin Kaldırılması

Docker ve bağlı paketler zaten kuruluysa, çakışmayı önlemek için bunları kaldırın:

```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## Gerekli Paketlerin Kurulumu

Docker'ın sorunsuz çalışması için bazı önkoşulların kurulması gerekmektedir:

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
```

## Docker'ın Resmi GPG Anahtarının Eklenmesi

Docker paketlerinin güvenliği için, Docker'ın GPG anahtarını sisteminize ekleyin:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

## Docker'ın APT Kaynağının Eklenmesi

Docker'ın resmi APT deposunu sisteminize ekleyin:

```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Sistemin Güncellenmesi ve Docker'ın Kurulumu

Son olarak, paket listelerini güncelleyin ve Docker ile ilgili paketleri kurun:

```bash
sudo apt update -y && sudo apt upgrade -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Elbette, verdiğiniz talimatları Türkçeye çevirerek bir Markdown dosyası formatında düzenleyeceğim:

# Snapshotter Lite Düğüm Kurulum Rehberi

Bu rehber, PowerLoom deposundan Snapshotter Lite düğümünü klonlama, kurma ve çalıştırma adımlarını adım adım anlatmaktadır.

## Deposunun Klonlanması

Başlamak için, aşağıdaki komutu kullanarak `powerloom` adında bir dizine repositoriyi klonlayın:

```bash
git clone -b simulation_mode https://github.com/PowerLoom/snapshotter-lite powerloom
```

## Çalışma Dizinini Değiştirme

Depo klonlandıktan sonra, çalışma dizininizi `powerloom` dizinine değiştirin:

```bash
cd powerloom
```

## Yapı Betiğini Çalıştırma

Snapshotter Lite düğümünü başlatmak için terminalde `build.sh` betiğini çalıştırın:

```bash
./build.sh
```

## Kurulum Sırasında Girilmesi Gereken Değerler

Kurulum sırasında, aşağıdaki değerleri girmeniz istenecektir:

- `$SOURCE_RPC_URL`: Ethereum Ana Ağı için herhangi bir RPC kullanın, örneğin Ankr, Infura veya Alchemy.
- `SIGNER_ACCOUNT_ADDRESS`: İmzalayan hesap adresi için bir yan cüzdan kullanın. Lütfen ana/birincil cüzdanınızı kullanmayın.
- `SIGNER_ACCOUNT_PRIVATE_KEY`: Yan cüzdanınızdan özel anahtarı kullanın.

### İpucu

Yan cüzdan oluşturmak için, Metamask üzerinde yeni bir cüzdan oluşturarak basitçe yapabilirsiniz.

Bu, projenin kök dizininde bir `.env` dosyası oluşturan tek seferlik bir yapılandırma sürecidir.
```
