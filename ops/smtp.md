# Aw ye aw yɛrɛ ka SMTP bataki ciyɔrɔ jɔ

## dakun fɔlɔ

SMTP bɛ se ka baarakɛminɛnw san k’a ɲɛsin sankaba feerelaw ma, i n’a fɔ:

* [Amazɔni SES SMTP ye](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali sankaba email push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Aw bɛ se fana k’aw yɛrɛ ka batakiw dilan - cikan dan tɛ, musaka bɛɛ lajɛlen ka dɔgɔ.

Jɛ la, an bɛ an yɛrɛ ka lɛtɛrɛw dilancogo jira senfɛ-senfɛ.

## Server sugandili

SMTP baarakɛminɛn min bɛ a yɛrɛ ladon, o bɛ foroba IP de wajibiya ni port 25, 456 ani 587 da wulilen ye.

Foroba sankaba minnu bɛ baara kɛ tuma caman na, olu ye o kurunbonkarilaw bali ka da a kan, wa a bɛ se ka kɛ k’u da wuli ni baara yamaruya dilen ye, nka a bɛ gɛlɛyaba lase o bɛɛ kɔfɛ.

N b’a ɲini i fɛ i ka sanni kɛ jatigila dɔ fɛ min kɔnɔ nin portw dabɔlen don ani min bɛ dɛmɛ don ka reverse domain names sigi sen kan.

Yan, n bɛ [Contabo](https://contabo.com) laadi .

Contabo ye jatigila dilanbaga ye min sigilen bɛ Munich, Alimanjamana na, a sigira senkan san 2003 ni sɔngɔw ye minnu bɛ ɲɔgɔn sɔsɔ kosɛbɛ.

N’i ​​ye Euro sugandi k’a kɛ sanni wari ye, a sɔngɔ bɛna dɔgɔya (sɛrɛkili min hakilijagabɔlan ye 8GB ye ani CPU 4, o musaka bɛ se yuan 529 ɲɔgɔn ma san kɔnɔ, wa a sigili fɔlɔ sara ye fu ye san kelen kɔnɔ).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Ni i bɛ komandi kɛ, remark `prefer AMD` , ani server min bɛ ni AMD CPU ye, o bɛna baara kɛcogo ɲuman sɔrɔ.

Ninnu na, n bɛna Contabo ka VPS ta ka kɛ misali ye walasa k’a jira i yɛrɛ ka mail server jɔcogo.

## Ubuntu sitɛmu labɛncogo

Baarakɛminɛn min bɛ yen o ye Ubuntu 22.04 ye

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Ni server min bɛ ssh kan, o bɛ `Welcome to TinyCore 13!` (i n’a fɔ a jiralen bɛ cogo min na ja in na), o kɔrɔ ye ko sistɛmu ma sigi sen kan fɔlɔ. Aw ye ssh tigɛ ka miniti damadɔ makɔnɔ walasa ka don kokura.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ni `Welcome to Ubuntu 22.04.1 LTS` bɔra, a daminɛ bɛ dafa, wa i bɛ se ka taa ɲɛ ni nin wale ninnu ye.

### [A bɛ se ka kɛ] Yiriwali sigida daminɛ

Nin wale in ye ŋaniyataama ye.

Walasa ka nɔgɔya sɔrɔ, n ye ubuntu porogaramuw sigili n’u sitɛmu labɛncogo bila [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) kɔnɔ.

Aw bɛ nin cikan in kɛ walasa ka a sigi ni digi kelen ye.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Sinuwa baarakɛlaw, aw ka baara kɛ ni nin cikan in ye o nɔ na, ​​wa kan, waatibolodacogo, a ɲɔgɔnnaw bɛna sigi u yɛrɛma.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo bɛ IPV6 baara kɛ

IPV6 daminɛ walasa SMTP fana ka se ka batakiw ci ni IPV6 ladɛrɛsiw ye.

`/etc/sysctl.conf` ladilan

Aw bɛ nin zana ninnu sɛmɛntiya walima ka fara u kan

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Aw bɛ tugu [contabo kalan kɔ: IPv6 ɲɔgɔndan farali aw ka baarakɛminɛn kan](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

`/etc/netplan/01-netcfg.yaml` ladilan, ka zana damadɔ fara a kan i n’a fɔ a jiralen bɛ cogo min na ja in na (Contabo VPS default configuration file bɛ ni nin zana ninnu ye kaban, uncomment u dɔrɔn).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

O kɔfɛ, `netplan apply` walasa ka labɛncogo sɛmɛntiyalen kɛ ka baara kɛ.

Labɛnni kɛlen kɔ, i bɛ se ka baara kɛ ni `curl 6.ipw.cn` walasa ka i ka kɛnɛma réseau ipv6 ladɛrɛsi lajɛ.

## Clone ka configuration marayɔrɔ ops

```
git clone https://github.com/wactax/ops.soft.git
```

## SSL seere fu dɔ labɛn i ka domani tɔgɔ kama

Sɛbɛn cili bɛ SSL seere de wajibiya walasa ka kodɔn ani ka bolonɔ bila.

An bɛ baara kɛ ni [acme.sh](https://github.com/acmesh-official/acme.sh) ye walasa ka seereyaw dilan.

acme.sh ye da wulilen ye seereyaw bolonɔbila baarakɛminɛn ye min bɛ kɛ ni otomatiki ye ,

Aw bɛ don configuration warehouse ops.soft kɔnɔ, ka `./ssl.sh` boli, ani `conf` foli bɛna dabɔ **sanfɛla ɲɛbilasɛbɛn** kɔnɔ .

Aw ye aw ka DNS dilanbaga ɲini ka bɔ [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) la , ka `conf/conf.sh` ladilan .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

O kɔfɛ, aw bɛ `./ssl.sh 123.com` boli walasa ka `123.com` ni `*.123.com` seereyaw dilan aw ka domani tɔgɔ kama.

Boli fɔlɔ bɛna [acme.sh](https://github.com/acmesh-official/acme.sh) sigi a yɛrɛma ani ka baara bolodalen dɔ fara a kan walasa ka otomatiki kuraya. Aw bɛ se ka `crontab -l` ye, o ɲɔgɔnna zana bɛ yen i n’a fɔ nin.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Sɛbɛn min bɛ sɔrɔ o sira ye fɛn ye i n'a fɔ `/mnt/www/.acme.sh/123.com_ecc。`

Seere kurayali bɛna `conf/reload/123.com.sh` script wele, ka nin script in ladilan, i bɛ se ka cikanw fara a kan i n’a fɔ `nginx -s reload` walasa ka seereyaw cache kura ye baarakɛminɛnw na minnu bɛ tali kɛ ɲɔgɔn na.

## SMTP sèrvèr jɔ ni chasquid ye

[chasquid](https://github.com/albertito/chasquid) ye SMTP baarakɛminɛn dafalen ye min sɛbɛnnen bɛ Go kan na.

I n’a fɔ mail server porogaramu kɔrɔw nɔnabila i n’a fɔ Postfix ani Sendmail, chasquid ka nɔgɔn ani a baara ka nɔgɔn, wa a ka nɔgɔn fana yiriwali filanan na.

Run `./chasquid/init.sh 123.com` bɛna sigi sen kan a yɛrɛma ni digi kelen ye (123.com bila i ka cikan tɔgɔ bila a nɔ na).

## Email Signature DKIM labɛn

DKIM bɛ kɛ ka imɛri bolonɔbila ci walasa ka batakiw bali ka jate i n’a fɔ fɛn tiɲɛnenw.

Cikan in kɛlen kɔ ka ɲɛ, a bɛna ɲini i fɛ i ka DKIM sɛbɛn sigi sen kan (i n’a fɔ a jiralen bɛ cogo min na jukɔrɔ).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

TXT sɛbɛn dɔ fara i ka DNS kan dɔrɔn (i n’a fɔ a jiralen bɛ cogo min na jukɔrɔ).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Baarakɛcogo cogoya & sɛbɛnw lajɛ

 `systemctl status chasquid` Baara cogoya lajɛ.

Baarakɛcogo nɔgɔman cogoya bɛ i n’a fɔ a jiralen bɛ cogo min na ja in na

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` walima `journalctl -xeu chasquid` bɛ se ka filiw sɛbɛn lajɛ.

## Domani tɔgɔ labɛncogo kɔsegin

Domani tɔgɔ min bɛ kɔsegin, o ye ka sira Di IP ladɛrɛsi ma ka ɲɛnabɔ ka kɛɲɛ ni domani tɔgɔ ye min bɛ bɛn o ma.

Ni i ye domani tɔgɔ kɔsegin, o bɛ se ka batakiw bali ka dɔn iko spam.

Ni bataki sɔrɔla, baarakɛla min bɛ bataki sɔrɔ, o bɛna domani tɔgɔ kɔsegin sɛgɛsɛgɛli kɛ cibaga ka IP ladɛrɛsi kan walasa k’a dɔn ni cibaga ka baarakɛyɔrɔ tɔgɔ kɔseginlen bɛ.

Ni ciden-sɛrɛkili tɛ ni kɔsegin-yɔrɔ tɔgɔ ye walima ni kɔsegin-domɛni tɔgɔ ma bɛn ciden cibaga ka IP ladɛrɛsi ma, cikan sɔrɔbaga bɛ se k’a dɔn ko o e-mail ye spam ye walima ka ban a la.

Aw ye taa [https://my.contabo.com/rdns](https://my.contabo.com/rdns) la ani ka a labɛn i n’a fɔ a jiralen bɛ cogo min na jukɔrɔ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Domɛni tɔgɔ kɔkanna sigili kɔfɛ, aw hakili to a la ka domani tɔgɔ ipv4 ni ipv6 ɲɛfɛla ɲɛnabɔli labɛn ka taa sèrwɛri la.

## Chasquid.conf ka jatigila tɔgɔ sɛgɛsɛgɛ

`conf/chasquid/chasquid.conf` bεε bε bεn ka kɛɲɛ ni kɔsegin domain tɔgɔ nafa ye.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

O kɔfɛ, `systemctl restart chasquid` boli walasa ka baara daminɛ kokura.

## Backup conf ka git marayɔrɔ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Misali la, n bɛ conf foli back up kɛ n yɛrɛ ka github processus kɔnɔ i n’a fɔ nin cogo in na

Aw ye fɛnmarayɔrɔ dɔ dabɔ fɔlɔ

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Aw bɛ don conf directory kɔnɔ ka bila depo kɔnɔ

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## A’ ye ciden fara a kan

ka boli

```
chasquid-util user-add i@wac.tax
```

Ka se ka ciden fara a kan

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Aw ye a lajɛ ni tɔgɔlasɛbɛn bilalen don ka ɲɛ

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Baarakɛla faralen kɔfɛ, `chasquid/domains/wac.tax/users` bɛna ladamu, aw hakili to a la k’a bila fɛnmarayɔrɔ la.

## DNS bɛ SPF sɛbɛnni fara a kan

SPF ( Sender Policy Framework ) ye imɛri sɛgɛsɛgɛli fɛɛrɛ ye min bɛ kɛ ka imɛri nanbara bali.

A bɛ bataki cibaga dɔ ka danyɔrɔ sɛgɛsɛgɛ n’a y’a lajɛ ni ciden ka IP ladɛrɛsi bɛ bɛn a ka domani tɔgɔ DNS sɛbɛnw ma, a b’a fɔ ko a ye min ye, o bɛ nanbarakɛlaw bali ka bataki nkalonmaw ci.

SPF sɛbɛnw farali bɛ se ka kɛ sababu ye ka batakiw bali ka dɔn ko u ye fɛn tiɲɛnenw ye ni a bɛ se ka kɛ.

Ni i ka domain name server tɛ SPF suguya dɛmɛ, i ka TXT suguya sɛbɛn fara a kan dɔrɔn.

Misali la, `wac.tax` ka SPF ye nin ye

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ka ɲɛsin `_spf.wac.tax` ma

`v=spf1 a:smtp.wac.tax ~all`

A kɔlɔsi ko n ye `include:_spf.google.com` don yan, o bɛ kɛ bawo n bɛna `i@wac.tax` labɛn i n’a fɔ cikan ladɛrɛsi Google mailbox kɔnɔ kɔfɛ.

## DNS labɛncogo DMARC

DMARC ye (Domain-based Message Authentication, Reporting & Conformance) daɲɛ surun ye.

A bɛ Kɛ ka SPF bounces (SPF bounces) Minɛ (n’a sɔrɔla o sababu Bɔra configuration filiw la, walima mɔgɔ wɛrɛ b’a Kɛ i n’a fɔ i ye spam ci).

TXT sɛbɛn `_dmarc` fara a kan , .

A kɔnɔkow bɛ nin cogo in na

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Paramɛtɛrɛ kelen-kelen bɛɛ kɔrɔ ye nin ye

### p (Politiki) .

A bɛ imɛriw ɲɛnabɔcogo jira minnu tɛ SPF (Sender Policy Framework) walima DKIM (DomainKeys Identified Mail) sɛgɛsɛgɛli kɛ. p paramɛtiri bɛ se ka sigi nafa saba dɔ la kelen na:

* si tɛ: Fɛɛrɛ si tɛ kɛ, sɛgɛsɛgɛli jaabi dɔrɔn de bɛ segin ka di cibaga ma imɛri laseli fɛɛrɛ fɛ.
* Kɛrɛnkɛrɛnnenya la: Bataki minnu ma tɛmɛ sɛgɛsɛgɛli la, i k’olu bila spam folder kɔnɔ, nka u tɛna ban o bataki la k’a ɲɛsin u yɛrɛ ma.
* ban: Ka ban k’a ɲɛsin imɛri ma minnu tɛ se ka sɛgɛsɛgɛli kɛ.

### fo (Dɛsɛ sugandiliw) .

Kunnafoni hakɛ min bɛ segin kunnafoni dicogo fɛɛrɛ fɛ, o bɛ o jira. A bɛ se ka sigi nin nafa ninnu dɔ la kelen na:

* 0: Laseli kɛ dantigɛli jaabiw kan cikanw bɛɛ la
* 1: Cikan minnu ma se ka sɛgɛsɛgɛli kɛ, olu dɔrɔn de fɔ
* d: Domɛni tɔgɔ sɛgɛsɛgɛli dɛsɛw dɔrɔn de fɔ
* s: SPF sɛgɛsɛgɛli dɛsɛw dɔrɔn de fɔ
* l: DKIM sɛgɛsɛgɛli dɛsɛw dɔrɔn de fɔ

### rua & ruf ye baara kɛ

* rua (URI laseli ka ɲɛsin rapɔɔriw lajɛlen ma): Imɛri ladɛrɛsi min bɛ kɛ ka kunnafoniw sɔrɔ minnu lajɛlen don
* ruf (Reporting URI for Forensic reports): imɛri ladɛrɛsi walasa ka kunnafoni caman sɔrɔ

## MX sɛbɛnw fara a kan walasa ka batakiw ci Google Mail ma

Komin n ma se ka tɔn ka batakibɔlan fu sɔrɔ min bɛ diɲɛ bɛɛ ka ladɛrɛsiw dɛmɛ (Catch-All, a bɛ se ka bataki cilenw sɔrɔ nin domani tɔgɔ in na, k’a sɔrɔ dan ma kɛ a daminɛcogo la), n ye chasquid kɛ ka batakiw bɛɛ ci n ka Gmail batakibɔlan kɔnɔ.

**Ni i yɛrɛ ka jagokɛyɔrɔ saralen bɛ i bolo, i kana MX sɛmɛntiya ani ka nin fɛɛrɛ in tɛmɛ.**

`conf/chasquid/domains/wac.tax/aliases` , ka bataki cicogo sigi

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` bɛ imɛli bɛɛ jira, `i` ye cibaga ka imɛri ladɛrɛsi daminɛ ye min dabɔra sanfɛ. Walasa ka bataki ci, baarakɛla kelen-kelen bɛɛ ka kan ka layini dɔ fara a kan.

O kɔ fɛ, MX sɛbɛn Fàra o kan (n b’a Jira k’a ɲɛsin kɔsegin-yɔrɔ tɔgɔ ladɛrɛsi ma yan, i n’a fɔ a jiralen bɛ cogo min na zana fɔlɔ la ja in na).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Labɛnni bannen kɔfɛ, i bɛ se ka baara kɛ ni imayili ladɛrɛsi wɛrɛw ye walasa ka bataki ci `i@wac.tax` ani `any123@wac.tax` walasa k’a lajɛ n’i bɛ se ka batakiw sɔrɔ Gmail kɔnɔ.

Ni o tɛ, aw bɛ chasquid log ( `grep chasquid /var/log/syslog` ) lajɛ.

## Aw ye bataki ci i@wac.tax ni Google Mail ye

Google Mail ye bataki sɔrɔlen kɔfɛ, n jigi tun b’a la cogo min na ko n bɛna jaabi di ni `i@wac.tax` ye sanni ka jaabi di ni i.wac.tax@gmail.com ye.

Aw ye taa [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) la ka "Add another email address" digi.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

O kɔfɛ, i ka sɛgɛsɛgɛli kode sɛbɛn min sɔrɔla imɛri la min cilen don.

A laban na, a bɛ se ka sigi i n’a fɔ ciden ka ladɛrɛsi dafalen (ka fara sugandili kan ka jaabi di ni ladɛrɛsi kelen ye).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

O cogo la, an ye SMTP bataki ciyɔrɔ sigili dafa ani o waati kelen na, an bɛ baara kɛ ni Google Mail ye walasa ka batakiw ci ani k’u sɔrɔ.

## I ka kɔrɔbɔli bataki ci walasa k’a lajɛ ni labɛn in ɲɛnabɔra

Aw bɛ don `ops/chasquid` kɔnɔ

Run `direnv allow` to install dependencies (direnv sigilen don kilisi kelen daminɛcogo tɛmɛnen na ani hook dɔ farala shell kan)

o kɔ, boli

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Paramɛtɛrɛw kɔrɔ ye nin ye

* baarakɛla: SMTP baarakɛla tɔgɔ
* tɛmɛsira: SMTP tɔgɔlasɛbɛn
* ka: sɔrɔbaga

Aw bɛ se ka kɔrɔbɔli imɛri ci.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

A ka ɲi ka baara kɛ ni Gmail ye walasa ka kɔrɔbɔli batakiw sɔrɔ walasa k’a lajɛ ni labɛnw ɲɛnabɔra.

### TLS sariya sirili

I n’a fɔ a jiralen bɛ cogo min na ja in na, nin dakun fitinin in bɛ yen, o kɔrɔ ye ko SSL seere in daminɛna ka ɲɛ.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

O kɔ, i ka "Show Original Email" digi.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM (DKIM) ye

I n’a fɔ a jiralen bɛ cogo min na ja in na, Gmail ka bataki fɔlɔ ɲɛ bɛ DKIM jira, o kɔrɔ ye ko DKIM labɛncogo ɲɛnabɔra.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Aw ye Received lajɛ imɛri fɔlɔ kuncɛyɔrɔ la, aw bɛ se k’a ye ko ciden ka ladɛrɛsi ye IPV6 ye, o kɔrɔ ye ko IPV6 fana labɛnna ka ɲɛ.
