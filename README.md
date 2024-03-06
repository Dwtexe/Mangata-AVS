<h1 align="center"> Mangata AVS

# 01.03.2024 tarihinden Daha önceden kurulum yapanlar için güncelleme yöntemi . [Tıkla](#güncelleme)
# Güncellemeyi yaptıktan sonra karşınıza çıkan hatalar anlamları/çözümleri için [TIKLA](#Hatalar)


# Güncelleme 

> Güncelleme adımlarına başlayalım. 

> Unutmadan Stake yaptığınız rETH ve sETH miktarlarının toplamının 1ETH yi geçmesi veya eşit olması şart.

> [TIKLA](https://goerli.eigenlayer.xyz/) Aşağıdaki gibi 1ETH yi geçmiş veya eşit olmalı
![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/62f8e068-a665-489c-9c4f-22ed776604c7)

```
cd avs-operator-setup
```

```
docker compose down
```

> .env dosyanızı yedeklemeniz gerekmekte. isterseniz nano .env yapıp direkt kopyalayın ekrandaki her şeyi

```
git reset --hard
```
```
git pull
```

```
docker compose pull
```
```
docker compose down
```

> Az önce yazdığımız kodlar ile node dosyalarımızı güncelledik. 
> bu nedenle güncellenmiş env dosyasını düzenlememiz gerekmektedir.

```
nano .env
```

![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/aba7ddda-1bc1-40d1-9414-85f22e82e80d)

>resmideki çift süslü parantezli yerleri yedeklediğimiz dosyadan kopyalayın başka hiçbir şeye **dokunmayın**. 

>***SÜSÜLÜ PARANTEZLERİ DE SİLİN!!!***

>Eğer sizin env dosyanız resimdeki gibi değil ise aşağıdaki kodları yazın.

```
rm -rf .env
```

```
nano .env
```

> Aşağıdaki kısmı kopyalayıp bir not defterinde açın **süslü parantezleri silip** gerekli değerleri yazın. 

> Sonra da az önce boş bir sayfa olarak açtığımız .env dosyasına yapıştırın sağ tık ile yapıştırın.

```
MAIN_SERVICE_IMAGE=mangatasolutions/avs-finalizer:80ac399c2c2f103dd8de1be62c114d5090cd11cd
MAIN_SERVICE_NAME=avs-finalizer-node

#COLORBT_SHOW_HIDDEN=1
#RUST_BACKTRACE=full

# Goerli contracts deployment
AVS_REGISTRY_COORDINATOR_ADDR=0x5620cDb94BaAaD10c20483bd8705DA711b2Bc0a3

# Finalizer Service Manager RPC
AVS_RPC_URL=https://avs-aggregator-testnet.mangata.online/
# register with AVS when the node starts
OPT_IN_AT_STARTUP=true

RUST_LOG=avs=info

###############################################################################
####### TODO: Operators please update below values for your node ##############
###############################################################################

# TODO: Operators need to update this to provide connection to ETH & network nodes
CHAIN_ID=5
ETH_RPC_URL={{RPC url https://goerli.infura.io/v3/ şeklinde olacak}}
ETH_WS_URL= {{Websocket url wss://goerli.infura.io/ws/v3/ şeklinde olacak}}
SUBSTRATE_RPC_URL=wss://collator-01-ws-rollup-testnet.mangata.online:443

# TODO: Operators need to update this to their own keys, either use files or encoded JSON
# this is where your keys are stored on local storage
ECDSA_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/{{eigenlayer_cüzdan_adınız}}.ecdsa.key.json
BLS_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/{{eigenlayer_cüzdan_adınız}}.bls.key.json

# this is where the node binary finds the keys in the docker container
ECDSA_KEY_FILE=/app/operator_keys/ecdsa_key.json
BLS_KEY_FILE=/app/operator_keys/bls_key.json

# it is possible to pass the encoded json key directly with these env flags
# comment above both ECDSA_KEY_FILE & BLS_KEY_FILE if used
#ECDSA_KEY_JSON=
#BLS_KEY_JSON=

# TODO: Operators need to add password to decrypt the above keys
ECDSA_KEY_PASSWORD={{Şifrenizi buraya yazın}}
BLS_KEY_PASSWORD={{Şifrenizi buraya yazın}}
```


> İşiniz bittiği zaman bu resimdeki gibi gözükmesi lazım dosyanızın.

![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/918c7b2b-033c-4a5a-9620-6af2ebf03a68)

> env ile işiniz bitince

```
docker compose up -d
```

```
docker logs -f avs-finalizer-node
```
## Duyuru
## Şuanda Node unuz düzgün çalışmayacaktır. Mangatanın RPC sunucusu (https://avs-aggregator-testnet.mangata.online/) düzgün çalışmamaktadır. 
## Bu nedenle aşağıdaki [TIKLA](#Hatalar) kısmındaki RPC Hatalarını görmeniz doğaldır.
## Yapabileceğiniz hiçbir şey yok ekipten haber bekliyoruz.
## ![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/0342eaa6-1f64-475e-9a68-94620c3d8078)
## Node unuz yukarıdaki resimdeki gibi ise sorun yok demektir birazdan rpc hataları ekranda gözükür dert etmeyin sorunsuz kurulumu tamamlamışsınız.
## Duyuru bitti.

>Loglara girelim ve ardından resimdeki gibi gözükmesi lazım. 

![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/b2ace762-4a95-4cef-a95d-795ed015c5db)

> Ama biraz sürebilir bu logların akmaya başlması şuan ağ çok yavaş.
> Resimdeki gibi Sucesfully registered yazdıysa bırakın kendi haline çok da kafaya takmayın. 
> 30dk sonra ✅ görmez iseniz logda bi sorun olmuş olabilir. 
> Telegram grubuna gelin çözelim sorunu hem rehbere de ekleriz başka karşılaşanlar için iyi olur.

> Güncelleme Rehberini Yazan : @dwtexe 
> Esenlikler Dilerim.

## Duyuru
## Şuanda Node unuz düzgün çalışmayacaktır. Mangatanın RPC sunucusu (https://avs-aggregator-testnet.mangata.online/) düzgün çalışmamaktadır. 
## Bu nedenle aşağıdaki [TIKLA](#Hatalar) kısmındaki RPC Hatalarını görmeniz doğaldır.
## Yapabileceğiniz hiçbir şey yok ekipten haber bekliyoruz.
## ![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/0342eaa6-1f64-475e-9a68-94620c3d8078)
## Node unuz yukarıdaki resimdeki gibi ise sorun yok demektir birazdan rpc hataları ekranda gözükür dert etmeyin sorunsuz kurulumu tamamlamışsınız.
## Duyuru bitti.

# Hatalar

> 24 saat sonra tekrardan buradayım.

> Evet şimdi çok fazla karşımıza çıkan herkesin sorduğu ve sormaktan sıkılmadığı hataları açıklayalım ve çözümleri varsa çözüme kavuşturalım.


### 1 - RPC Hataları

> Aşağıdaki hatalara RPC errors denir. Sizle alakalı değiller biryerlerinizi yırtmak pahasına çözüm arasanız da bulamayacaksınız bu yüzden sormayı bırakın.

> Mangata'nın çözmesi gereken bir sorun bu onlardan haber bekleyeceğiz başka yapılabilecek **hiçbir şey yok**

![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/8fdbac8d-4b6c-43a6-aceb-07e47b30e23f)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/6da44650-3590-49ec-8d02-fa64c8c67b6f)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/d81e1339-9f99-4356-a9c3-5bd53c46ae58)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/c45ee3e7-1c75-4338-9418-a40614685526)

### 2 - .env Hataları

> Gelelim ikinci en çok karşılaşılan hatalar kısmına.

> Bu hatalar sizden kaynaklı aması maması yok! .env dosyanızda hata var.

>Yok olmaz öyle şey benim .env dosyasını benden iyi mi tanıyacaksınız diyebilirsiniz. Ama sizi üzecek bir haberim var... Maalesef sizden iyi tanıyorum.

>Üst taraflarda attığım .env dosyasının boş hali ile karşılaştırın ve sadece değiştirin dediğim kısımları düzgün şekilde yaptığınızdan emin olana kadar tekrar tekrar kontrol edin.

>Bazı arkadaşlar şifrelerini unuttuğu için her kısım doğru olsa da hata alıp kendilerini parçalıyorlar. Şifrenizden emin olun lütfen.


![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/fc7d7b20-4894-4208-a403-d0673a7063a7)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/984c1f42-1cc8-41dd-b018-383d11d22922)

### 3 - Log düşmemesi

> Az bekleyin düşer ama düşmeyedebilir şu sıra malum mangata ekibinin düzeltmesi gereken bir rpc sıkıntısı var.

> Node u düzenli olarak sorunsuz çalışan birinin olduğunu sanmıyorum.

> Ara ara log düşüyor sonra hata alıyoruz sonra tekrar canlanır gibi oluyor vs yani çok kafaya takmayın ve Mangata ekibinden haber bekleyin.

![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/0342eaa6-1f64-475e-9a68-94620c3d8078)

> Son olarak da lütfen çözümünü bulduğunuz ya da çözemeseniz bile neden kaynaklandığını anladığınız hatalar var ise bana ulaşın.
> Telegram/Discord : @dwtexe
