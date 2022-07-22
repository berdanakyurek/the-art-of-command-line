🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [polski](README-pl.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# Komut Satırı Sanatı

- [Açıklama](#açıklama)
- [Temeller](#temeller)
- [Günlük kullanım](#günlük-kullanım)
- [Dosya ve veri işleme](#dosya-ve-veri-işleme)
- [Sistem hata ayıklama](#sistem-hata-ayıklama)
- [Tek satırlık komutlar](#tek-satırlık-komutlar)
- [Karmaşık ama kullanışlı](#karmaşık-ama-kullanışlı)
- [Sadece macOS](#sadece-macos)
- [Sadece Windows](#sadece-windows)
- [Daha fazla kaynak](#daha-fazla-kaynak)
- [Sorumluluk reddi](#sorumluluk-reddi)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Komut satırını akıcı kullanmak genellikle göz ardı edilse de bir mühendis olarak esnekliğinizi ve veriminizi hem doğrudan, hem de dolaylı olarak artırır. Bu metin, Linux ile çalışırken faydalı bulduğumuz notların ve tavsiyelerin bir derlemesidir. Kimi tavsiyeler basit iken kimileri oldukça spesifik, karmaşık veya anlaşılması zordur. Bu sayfa uzun olmasa da doğru kullanabilirseniz ve buradaki tüm bilgileri öğrenebilirseniz, çok şey biliyor olacaksınız.


Bu çalışma [bir çok yazar ve çevirmenin](AUTHORS.md) eseridir.
Bunların bazıları
[ilk olarak](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)'da,
[ortaya çıktı](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
ancak sonradan GitHub'a taşındı ve orjinal yazardan daha yetenekli insanlar sayısız iyileştirmeler yaptı.

Eğer komut satırı ile ilgili bir sorunuz varsa [**bir soru gönderin**](https://airtable.com/shrzMhx00YiIVAWJg). Eğer bir hata veya daha iyi olabilecek bir şey tespit ederseniz lütfen [**katkıda bulunun**](/CONTRIBUTING.md)!

## Açıklama

Kapsam:

- Bu rehber hem yeni başlayanlar, hem de tecrübeli kullanıcılar için uygundur. Amaçlar *genişlik* (önemli olan her şey), *spesifiklik* (en yaygın vakaların somut örneklerini vermek) ve *özlülük* (gerekli olmayan veya konudan sapan ve dış kaynaklardan kolaylıkla bulunabilecek şeylerden kaçınmak)'tür. Her tavsiye bazı durumlarda önemlidir veya alternatiflerine göre önemli ölçüde zaman kazandırır.
- Bu rehber, "[Sadece macOS](#sadece-macos)" ve "[Sadece Windows](#sadece-windows)" bölümleri hariç Linux içindir. Diğer öğelerin çoğu diğer unicelar'a veya macOS'a (ve hatta Cygwin'e) yüklenebilir.
- Çoğu ipucu diğer shell'lere ve genel olarak Bash scriptlere uyumlu olsa da, odak interaktif Bash üzerinedir.
- Bu rehber hem "standart" Unix komutlarını, hem de paket yükleme gerektiren komutları (dahil edilmeyi hak edecek kadar önemli oldukları sürece) içerir.

Notlar:

- Bu rehberi tek sayfaya sığdırmak için içerik referanslar ile dahil edilmiştir. Fikri ve Google'da nasıl aratacağınızı anladıktan sonra daha fazla detay araştırabilirsiniz. Yeni programlar indirmek için `apt`, `yum`, `dnf`, `pacman`, `pip` veya `brew` (uygun görüleni) kullanın.
- Komutların, seçeneklerin, pipe'ların ne yaptığının faydalı bir dökümünü almak için [Explainshell](http://explainshell.com/) kullanın.


## Temeller

- Temel Bash öğrenin. `man bash` yazın ve dökümanın tamanına en azından bir göz atın. Takip etmesi oldukça kolay ve o kadar da uzun değil. Alternatif shell'ler de iyi olabilir, ancak Bash güçlüdür ve her zaman kullanılabilir(Kendi bilgisayarınızda *yalnızca* zsh, fish, etc. öğrenmek sizi mevcut sunucuları kullanmak gibi çok sayıda durumda sınırlayacaktır).

- En azından bir metin-tabanlı editör kullanmayı iyi öğrenin. `nano` basit düzeyde editleme (açma, düzenleme, kaydetme, arama) için en basit seçeneklerden biridir. Ancak, usta bir terminal kullanıcısı için  öğrenmesi zor ama değerli, hızlı ve tüm özelliklere sahip Vim (`vi`) editörü yeri doldurulamazdır. Çok sayıda insan özellikle daha büyük düzenleme için Emacs de kullanmaktadır. (Tabi ki , kapsamlı bir projede çalışan modern bir yazılım geliştiricinin saf metin tabanlı bir editör kullanması pek mümkün değildir ve modern IDE'lere ve araçlara da aşina olunmalıdır.)

- Döküman bulma:
  - `man` komutu kullanarak resmi dökümantasyon okumayı öğrenin (Meraklısına, `man man` komutu bölüm numaralarını listeler, örneğin 1, "normal" komutlar; 5, dosyalar/gelenekler ve 8, yönetim için kullanılır). Man sayfalarını `apropos` ile bulabilirsiniz.
  - Bazı komutlar çalıştırılabilir dosyalar değildir, Bash içerisinde tanımlıdır. Bu komutlar ile ilgili `help` ve `help -d` komutları kullanılarak yardım alınabilir. `type command` komutu kullanılarak bir komutun çalıştırılabilir mi, shell içerisinde tanımlı mı yoksa bir alias mı olduğu öğrenilebilir.
    - `curl cheat.sh/command` komutu bir komutun nasıl kullanılacağını yaygın örneklerle gösteren kısa bir döküman verir.

-  `>` ve `<` kullanarak input ve output yönlendirmeyi ve `|` ile pipe kullanmayı öğrenin. `>` output dosyasının üzerine yazar ve `>>` sonuna ekler. stdout ve stderr'i öğrenin.

-  `*` (ve  bekli de  `?` ve `[`...`]`) ve tırmak ile glob kullanmayı ve çift `"` ve tek `'` tırnak arasındaki farkı öğrenin.

- Bash iş yönetimine aşina olun: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, vb.

- `ssh` ve  `ssh-agent`, `ssh-add`, vb. aracılığıyla basit şifresiz kimlik doğrulama işlemlerini öğrenin.

- Temel dosya yönetimi: `ls` ve `ls -l` (özelikle `ls -l`'deki her bir sütunun ne anlama geldiğini öğrenin), `less`, `head`, `tail` ve `tail -f` (vaya daha iyisi, `less +F`), `ln` ve `ln -s` (hard ve soft linkler arasındaki farkları ve avantajları öğrenin), `chown`, `chmod`, `du` (disk kullanımının hızlı bir özeti için: `du -hs *`). Dosya sistemi yönetimi için, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. inode'un ne demek olduğu öğrenin (`ls -i` veya `df -i`).

- Temel ağ yönetimi: `ip` veya `ifconfig`, `dig`, `traceroute`, `route`.

- Bir versiyon kontrol sistemi kullanmayı öğrenin (örneğin `git`).

- Regular expression'ları ve `grep`/`egrep`'in çeşitli flag'larını iyice öğrenin. `-i`, `-o`, `-v`, `-A`, `-B` ve `-C` seçenekleri bilmeye değer.

- Paketleri bulmak ve yüklemek için `apt-get`, `yum`, `dnf` veya `pacman` (dağıtıma bağlı olarak) kullanmayı öğrenin. Python tabanlı komut satırı araçlarını yüklemek için `pip` kullanın (aşağıdakilerden bazıları en hızlı `pip` ile yüklenir).


## Günlük kullanım

- Bash içerisinde, bir komutu tamamlamak veya olası komutları listelemek için **Tab** butonunu kullanın ve komut geçmişi içerisinde arama yapmak için **ctrl-r** kısayolunu kullanın (bastıktan sonra aramak istediğiniz ifadeyi yazın. **ctrl-r**'ye tekrar tekrar basarak sonuçlar arasında gezin, bulduğunuz komutu çalıştırmak için **Enter** tuşuna basın, veya sağ ok tuşuna basarak bulduğunuz komutu mevcut satıra koyup düzenleme yapın).

- Bash içerisinde, son kelimeyi silmek için **ctrl-w**, imlecin bulunduğu konumdan satırın başına kadar olan metni silmek için **ctrl-u** kısayolunu kullanın. Bir önceki ve bir sonraki kelimeye gitmek için **alt-b** ve **alt-f**, imleci satırın başına getirmek için **ctrl-a**, imleci satırın sonuna getirmek için **ctrl-e**, imlecin bulunduğu konumdan satırın sonuna kadar olan metni silmek için **ctrl-k**, ekranı temizlemek için **ctrl-l** kısayolunu kullanın. Bash'teki tüm varsayılan kısayolları görmek için `man readline` komutunu kullanın. Bash içerisinde çok sayıda kısayol vardır. Örneğin, **alt-.** önceki komutlar arasında gezer ve **alt-*** bir globu genişletir.


- Alternatif olarak, eğer vi tarzı kısayolları seviyorsanız `set -o vi` kullanın (ve tersine çevirmek için `set -o emacs` kullanın).

- Uzun komutları düzenlemek için, editörünüzü ayarladıktan sonra (örneğin `export EDITOR=vim`), **ctrl-x** **ctrl-e** kısayolu, mevcut komutu çok satırda düzenleme için bir editör içinde açar. Veya  vi tarzında, **escape-v**.

- Son komutları görmek için `history` komutunu kullanın. Bulduğunuz bir komutu tekrar çalıştırmak için `!n` ( `n` komut numarası olmak üzere) komutunu kullanın. Başta, `!$` (son argüman) ve `!!` (son komut) olmak üzere çok sayıda kısaltma bulunur. (man sayfasındaki "HISTORY EXPANSION" kısmına bakın). Ancak bunlar genellikle **ctrl-r** ve **alt-.** ile kolaylıkla değiştirilebilir.

- `cd` ile home dizinine gidebilirsiniz. Dosyalara home dizinine göre erişebilmek için `~` ön ekini kullanabilirsiniz (örneğin `~/.bashrc`). `sh` scriptlerinde home dizini olarak `$HOME` kullanın.

- Bir önceki çalışma dizinine dönmek için: `cd -`.

- Eğer bir komut yazarken yarı yolda vazgeçerseniz **alt-#** kısayolu ile satırın başına bir `#` sembolü ekleyin ve bir yorum satırı olarak çalıştırın (veya **ctrl-a**, **#**, **enter** kullanın). Böylelikle bu komuta daha sonra komut geçmişini kullanarak ulaşabilirsiniz.

- `xargs` (veya `parallel`) kullanın. Çok güçlüdür. Ayrıca satır başına kaç öğe çalıştırılacağını (`-L`) ve paralel çalışmayı (`-P`) da kontrol edebilirsiniz. Eğer doğru şeyi yapacağından emin değilseniz önce `xargs echo` kullanın. Ayrıca `-I{}` de kullanışlıdır. Örnekler:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` kullanışlı bir process ağacı çıkarır.

- Processleri bulmak veya sinyal göndermek için `pgrep` ve `pkill` kullanın (`-f` de kullanışlıdır).

- Processlere gönderebileceğiniz çeşitli sinyalleri bilin. Örneğin, bir processi askıya almak için `kill -STOP [pid]` kullanın. Tüm liste için `man 7 signal` komutunu kullanın.

- Eğer bir arka plan processinin sonsuza kadar çalışmaya devam etmesini istiyorsanız `nohup` veya `disown` kullanın.

- Process'lerin ne dinlediğini `netstat -lntp` veya `ss -plat` (TCP için; UDP için `-u` ekleyin) veya `lsof -iTCP -sTCP:LISTEN -P -n` (macOS'ta da çalışır) kullanın.

- Ayrıca açık soket ve dosyalar için `lsof` ve `fuser` kullanın.

- Sistemin ne kadar süredir çalıştığını öğrenmek için `uptime` veya `w` kullanın.

- Sıklıkla kullanılan komutlara kısayol eklemek için `alias` kullanın. Örneğin, `alias ll='ls -latr'` `ll` aliasını yaratır.

- Aliasları, shell ayarlarını ve sıklıkla kullandığınız komutları `~/.bashrc` içerisine koyun ve [login shell'lerin de bunu kullanması için gerekli ayarlamaları yapın](http://superuser.com/a/183980/7106). Bu, ayarlarınızı her shellde kullanılabilir yapacaktır.

- Çevre değişkeni ayarlarını ve giriş yapıldığında çalışması gereken komutları `~/.bash_profile` içerisine koyun. Grafik arayüz içerisinden çalıştırılan shell'lerde ve `cron` işlerinde farklı ayarlamalar gereklidir.

- Konfigürasyon dosyalarınızı (`.bashrc` ve `.bash_profile`) farklı bilgisayarlar arasında senkronize etmek için Git kullanın.

- Boşluk içeren değişken ve dosya adları dikkat gerektirir. Bash değişkenlerini tırnak ile çevreleyin, örneğin `"$FOO"`. Dosya adlarını null karakteri ile bitirmek için `-0` veya `-print0` seçeneklerini kullanın, örneğin `locate -0 pattern | xargs -0 ls -al` veya `find / -print0 -type d | xargs -0 ls -al`. Boşluk içeren dosya adları üzerinde for döngüsü ile yineleme yapmak için `IFS=$'\n'` kullanarak IFS'inizi bir yeni satır karakteri olarak belirleyin.

- Bash scriptlerinde, çıktıyı debug etmek için `set -x` (veya genişletilmemiş değişkenler ve yorumlar dahil saf girdiyi kaydeden `set -v`) komutunu kullanın. Kullanmamak için iyi bir sebebiniz olmadığı sürece katı modlar kullanın: Hata (sıfır olmayan çıkış kodu) durumunda durdurmak için `set -e` kullanın. Ayarlanmamış değişken kullanımlarını tespit etmek için `set -u` kullanın. Pipelar içindeki hatalarda durdurmak için `set -o pipefail` kullanmayı düşünün (bu konu biraz anlaması zor olduğu için konu hakkında daha fazla okuyun). Daha kapsamlı scriptler için EXIT veya ERR ile `trap` kullanın. Bir scripte bu şekilde başlamak faydalı bir alışkanlıktır. Yaygın hataları tespit eder, sonlandırır ve bir mesaj yazdırır:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Bash scriptlerinde, alt-shell'ler (parantez içinde yazılır) komutları gruplamanın kullanışlı bir yoludur. Yaygın bir örnek, geçici olarak farklı bir dizine geçmektir. Örneğin,
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- Bash içerisinde çok sayıda değişken açılımı bulunur. Bir değişkenin varlığını kontrol etme: `${name:?error message}`. Örneğin, eğer bir Bash scripti tek bir değer alıyorsa, sadece `input_file=${1:?usage: $0 input_file}` yazın. Değişken boşsa varsayılan bir değer kullanma: `${name:-default}`. Eğer önceki örneğe isteğe bağlı bir parametre eklemek istiyorsanız `output_file=${2:-logfile}` benzeri bir ifade kullanabilirsiniz. Eğer `$2` boşsa, `output_file`değişkeni `logfile` olacaktır. Aritmetik açılım: `i=$(( (i + 1) % 5 ))`. Diziler: `{1..10}`. String kırpma: `${var%suffix}` ve `${var#prefix}`. Örneğin, `var=foo.pdf` ise `echo ${var%.pdf}.txt` komutu `foo.txt` yazdıracaktır.

- `{`...`}` ile brace açılımı, benzer metinleri tekrar yazmayı azaltarak öğelerin kombinasyonlarını otmatikleştirebilir. Bu, `mv foo.{txt,pdf} some-dir` (her iki dosyayı da taşır), `cp somefile{,.bak}` (açılımı `cp somefile somefile.bak`'tır) veya `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (açılımı tüm olası kombinasyonlardır ve bir dizin ağacı oluşturur) gibi örneklerde faydalıdır. Brace açılımı herhangi bir başka açılımdan önce gerçekleşir.

- Açılımların sıralaması: brace açılımı; tilda açılımı, parametre ve değişken açılımı, aritmetik açılım ve komut değişimi (soldan sağa doğru gerçekleşir); kelime bölme; ve dosya adı açılımı. (Örneğin, `{1..20}` gibi bir aralık `{$a..$b}` şeklinde değişkenler ile ifade edilemez. Bunun yerine `seq` veya `for` döngüsü kullanın, örneğin, `seq $a $b` veya `for((i=a; i<=b; i++)); do ... ; done`.)

-  `<(bir komut)` ile bir komutun çıktısı bir dosya gibi kullanılabilir (process yerine koyma olarak bilinir). Örneğin, yerel `/etc/hosts` ile uzaktakini kıyaslamak:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Script yazarken tüm kodunuzu süslü parantez içine koymak isteyebilirsiniz. Eğer kapa parantez eksik ise scriptiniz sözdizim hatası nedeniyle çalıştırılamayacaktır. Bu, eğer scriptiniz internetten indirilecekse anlamlıdır. Böylelikle kısmen indirilmiş scriptler yanlışlıkla çalıştırılmayacaktır:
```bash
{
      # Kodunuz
}
```

- Bir "here document" [çok satırlı girdinin yönlendirilmesini](https://www.tldp.org/LDP/abs/html/here-docs.html) sağlar:
```
cat <<EOF
input
on multiple lines
EOF
```

- Bash'te, hem standart output, hem de standart hata `some-command >logfile 2>&1` veya `some-command &>logfile` ile yönlendirilir. Often, to ensure a command does not leave an open file handle to standard input, tying it to the terminal you are in, it is also good practice to add `</dev/null`.

- Onaltılık ve onluk sistemdeki değerleri de içeren iyi bir ASCII tablosu için `man ascii` kullanın. Genel kodlama bilgiisi için, `man unicode`, `man utf-8` ve `man latin1` komutları kullanışlıdır.

- Katmanlar oluşturmak için `screen` veya [`tmux`](https://tmux.github.io/). Bu özellikle uzaktan ssh bağlantılarında ve oturumlardan kopmak ve geri bağlanmak için kullanışlıdır. `byobu`, daha fazla bilgi vererek ve daha kolay yönetim sağlayarak screen veya tmux'un ötesine geçebilir.  Yalnızca oturum sürekliliği için daha minimal bir seçenek: [`dtach`](https://github.com/bogner/dtach).

- In ssh, knowing how to port tunnel with `-L` or `-D` (and occasionally `-R`) is useful, e.g. to access web sites from a remote server.

- Ssh ayarlarınızda bazı optimizasyonlar yapmak faydalı olabilir; örneğin, bu `~/.ssh/config` bazı ağ ortamlarındaki bağlantı kopmalarını önler, sıkıştırma kullanır (düşük bant genişlikli bağlantılarda kullanışlıdır):
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Bazı diğer ssh ile ilgili seçenekler güvenlik açısından hassastır ve özenle ayarlanmalıdır. Örneğin alt ağ veya güvenilen ağlarda: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- [`mosh`](https://mosh.mit.edu/) UDP kullanan bir ssh alternatifidir. Bağlantıda kopmalardan kaçınır ve avoiding dropped connections ve kolaylık sağlar (server tarafı kurulumu gerektirir).

- Bir dosyanın izinlerini sekizlik formda almak için (sistem kurulumunda kullanışlıdır ama `ls` çıktısında bulunmaz)
```sh
      stat -c '%A %a %n' /etc/timezone
```
kullanın.

- Başka bir komutun çıktısı üzerinden interaktif seçim yapmak için [`percol`](https://github.com/mooz/percol) veya [`fzf`](https://github.com/junegunn/fzf) kullanın.

- Dosyalarla başka bir komutun çıktısına bağlı olarak etkileşim için (`git` gibi), `fpp` ([PathPicker](https://github.com/facebook/PathPicker)) kullanın.

- Mevcut dizindeki (ve tüm alt dizinlerdeki) tüm dosyaları içeren ve ağınızdaki herkese açık bir web sunucusu için
`python -m SimpleHTTPServer 7777` (port 7777 ve Python 2 için) veya `python -m http.server 7777` (port 7777 ve Python 3 için) kullanın.

- Bir komutu başka bir kullanıcı olarak çalıştırmak için, `sudo` kullanın.Varsayılan olarak root olark çalıştırır; başka bir kullanıcı belirtmek için `-u` kullanın. Bu kullanıcı olarak giriş yapmak için `-i` kullanın (_sizin_ şifreniz sorulacaktır).

- Kullanıcı değiştirmek için `su username` veya `su - username` kullanın. İkinci komut başka bir kullanıcı yeni giriş yapmış gibi bir environment oluşturur. Kullanıcı adını boş bırakmak varsayılan olarak root'a geçer. _Geçiş yaptığınız kullanıcının_ şifresi sorulacaktır.

- Komut satırlarındaki [128K sınırı](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong)'nı öğrenin.  "Argüman listesi çok uzun" hatası bir sembol çok sayıda dosya ile eşleştiğinde yaygındır. (Bu olduğunda `find` ve `xargs` gibi alternatifler yardımcı olabilir.)

- Basit bir hesap makinesi (ve genel olarak Python) için, `python` yorumlayıcısı kullanın. Örneğin,
```
>>> 2+3
5
```


## Dosya ve veri işleme

- Mevcut dizin içerisinde bir dosyayı ismiyle bulmak için, `find . -iname '*something*'` (veya benzeri). Bir dosyayı herhangi bir yerde bulmak için, `locate something` kullanın (`updatedb`'nin yeni yaratılan dosyaları indekslememiş olabileceğini de göz önünde bulundurun).

- Kaynak veya veri dosyaları içinde genel arama için `grep -r`'den daha gelişmiş ve hızlı seçenekler vardır. Örneğin (kabaca eskiden yeniye doğru) [`ack`](https://github.com/beyondgrep/ack2), [`ag`](https://github.com/ggreer/the_silver_searcher) ("the silver searcher") ve [`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep).

- HTML'i metne çevirmek için: `lynx -dump -stdin`

- Markdown, HTML ve her çeşit döküman çevirme için [`pandoc`](http://pandoc.org/)'u deneyin. Örneğin, bir markdown dökümanını Word formatına dönüştürmek için: `pandoc README.md --from markdown --to docx -o temp.docx` kullanın.

- XML için, `xmlstarlet` eski ama iyidir.

- JSON için [`jq`](http://stedolan.github.io/jq/) kullanın. Etkileşimli kullanım için: [`jid`](https://github.com/simeji/jid) ve [`jiq`](https://github.com/fiatjaf/jiq).

- YAML için [`shyaml`](https://github.com/0k/shyaml) kullanın.

- Excel veya CSV belgeleri için, [csvkit](https://github.com/onyxfish/csvkit), provide `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, vb. sağlar.

- Amazon S3 için [`s3cmd`](https://github.com/s3tools/s3cmd) uygundur ve [`s4cmd`](https://github.com/bloomreach/s4cmd) daha hızlıdır. Amazon'un [`aws`](https://github.com/aws/aws-cli) ve daha gelişmiş [`saws`](https://github.com/donnemartin/saws) komutları AWS ile ilgili işler için önemlidir.

- `sort` ve `uniq`'i , uniq'in `-u` ve `-d` seçeneklerini  öğrenin -- aşağıda tek satırlık komutlar bölümüne bakın. Ayrıca `comm` komutunu öğrenin.

- Metin dosyalarını işlemek için `cut`, `paste` ve `join` komutlarını öğrenin. Çoğu kişi `cut` kullanır ama `join`'i unutur.

- Satırları (`-l`), karakterleri (`-m`), kelimeleri (`-w`) ve byte'ları (`-c`) saymak için `wc` kullanmayı öğrenin.

- Know about stdin'den bir dosyaya ve stdouta kopyalamak için `tee` kullanmayı öğrenin, `ls -al | tee file.txt`'de olduğu gibi.

- Daha karmaşık hesaplamalar için (gruplama, alanları tersine çevirme ve istatistiksel hesaplamalar gibi) [`datamash`](https://www.gnu.org/software/datamash/) kullanın.

- Yerel ayarların sıralama ve performans gibi bir çok komut satırı aracını etkilediğini bilin. Çoğu Linux kurulumu `LANG` veya diğer yerel ayar değişkenini US English olarak ayarlar. Ancak eğer yerel ayarları değiştirirseniz sıralamanın da değişeceğinin farkında olun. Ayrıca i18n rutinleri sort ve diğer komutların çalışmasını *birkaç kat* yavaşlatabilir. Bazı durumlarda (küme işlemleri ve özgünlük işlemleri gibi) yavaş i18n rutinlerini güvenle yoksayabilirsiniz ve `export LC_ALL=C` kullanarak geleneksel byte-tabanlı sıralama düzeni kullanabilirsiniz.

- Bir komutun ortamını belirlemek için komutun önüne ortam değişkeni ayarlarını ekleyin. Örneğin `TZ=Pacific/Fiji date`.

- Basit veri işleme için `awk` ve `sed` kullanın. Örnekler için [Tek-Satırlık-Komutlar](#tek-satırlık-komutlar) bölümüne bakın.

- Bir veya birden fazla dosyada bir stringi başka bir string ile değiştirmek için:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Birden fazla dosyayı yeniden adlandırmak ve/veya dosya içerisinde arama ve değiştirme yapmak için [`repren`](https://github.com/jlevy/repren)'i deneyin. (Bazı durumlarda `rename` komutu birden fazla yeniden adlandırma işlemine izin verir ancak çalışması tüm Linux dağıtımlarında aynı olmayacağından dikkatli olun.)
```sh
      # Dosya adlarının, dizinlerin ve içeriklerin tam yeniden adlandırılması foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Yedek dosyalarıni geri yükleme whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Yukarıdakinin aynısı, rename kullanarak:
      rename 's/\.bak$//' *.bak
```

- man sayfasında söylendiği gibi, `rsync` gerçekten hızlı ve çok yönlü bir dosya kopyalama aracıdır. Makineler arası senkronizasyon için kullanılmasıyla bilinir ancak yerel olarak da aynı derecede kullanışlıdır. Güvenlik kısıtlamaları el verdiğinde, using `scp` yerine `rsync` kullanmak aktarımın sıfırdan başlamak yerine kaldığı yerden devam etmesine izin verir. Ayrıca çok sayıda dosyayı silmenin [en hızlı yollarından](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) biridir:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Dosyaları işlerken ilerlemeyi takip etmek için  [`pv`](http://www.ivarch.com/programs/pv.shtml), [`pycp`](https://github.com/dmerejkowsky/pycp), [`pmonitor`](https://github.com/dspinellis/pmonitor), [`progress`](https://github.com/Xfennec/progress), `rsync --progress`, veya, blok seviyesinde kopyalama için, `dd status=progress` kullanın.

- Bir dosyayi karıştırmak veya rastgele satırlar seçmek için `shuf` kullanın.

- `sort` komutunun seçeneklerini bilin. Sayılar için `-n`, veya insan tarafından okunabilir sayılar için `-h` (örneğin `du -h` komutundan gelen) kullanın. Anahtarların nasıl çalıştığını bilin (`-t` ve `-k`). Özellikle yalnızca ilk alana göre sıralamak için `-k1,1` yazmanız gerektiğine dikkat edin; `-k1` tüm satıra göre sıralamak anlamına gelir. Stabil sıralama (`sort -s`) kullanışlı olabilir. Örneğin, öncelikle alan 2, sonra ikincil olarak alan 1'e göre sıralamak için `sort -k1,1 | sort -s -k2,2` kullanabilirsiniz.

- Eğer komut satırına Tab yazmak isterseniz (örneğin sort'un -t argümanı için),  **ctrl-v** **[Tab]**'ye basın veya `$'\t'` yazın (kopyalayıp yapıştırabileceğiniz için ikinci seçenek daha iyidir).

- Kaynak kodu yamalamak için standart araçlar `diff` ve `patch`'tir. Ayrıca diff ve `sdiff`'in özet istatistikleri ve yan yana diff için `diffstat` kullanın.  `diff -r` bütün dizinler için çalışır. Değişikliklerin özeti için `diff -r tree1 tree2 | diffstat` kullanın. Dosyaları karşılaştırmak ve düzenlemek için `vimdiff` kullanın.

- Binary dosyalar için, basit onaltılık gösterimler için `hd`, `hexdump` veya `xxd` ve temel binary düzenleme için `bvi`, `hexedit` veya `biew` kullanın.

- Ayrıca binary dosyalar için, `strings` (ve `grep`, vb.) metindeki bitleri bulmanıza izin verir.

- Binary diff için (delta sıkıştırması) `xdelta3` kullanın.

- Metin kodlamalarını dönüştürmek için, `iconv`'u deneyin. Daha ileri düzey kullanım için`uconv` kullanın; bazı ileri düzey Unicode işlevlerini destekler. Örneğin:
```sh
      # Onaltılık kodları veya karkaterlerin gerçek adlarını gösterir (hata ayıklama için kullanışlıdır):
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Tüm karakterleri küçük harf yapar ve aksan işaretlerini kaldırır (genişletip düşürerek):
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```

- Dosyaları parçalara ayırmak için `split` (boyuta göre ayırma) ve `csplit` (bir kalıba göre ayırma) kullanın.

- Tarih ve saat: Anlık tarih ve saati kullanışlı  [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) formatında almak için `date -u +"%Y-%m-%dT%H:%M:%SZ"` kullanın (Diğer [seçenekler](https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option) [problematic](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)). Tarih ve saat ifadelerini düzenlemek için from [`dateutils`](http://www.fresse.org/dateutils/)'ten `dateadd`, `datediff`, `strptime` vb. kullanın.

- Sıkıştırılmış dosyalar üzerinde işlem yapmak için `zless`, `zmore`, `zcat`, ve `zgrep` kullanın.

- Dosya özellikleri `chattr` ile belirlenebilir ve dosya izinlerine daha alt seviye bir alternatif sunar. Örneğin, yanlışlıkla dosya silmeye karşı koruma için: `sudo chattr +i /critical/directory/or/file`

- Dosya izinlerini kaydetmek ve geri getirmek için `getfacl` ve `setfacl` kullanın. Örneğin:
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

- Kolayca boş dosya yaratmak için `truncate` ([seyrek dosya](https://en.wikipedia.org/wiki/Sparse_file) yaratır), `fallocate` (ext4, xfs, btrfs ve ocfs2 dosya sistemleri), `xfs_mkfile` (neredeyse tüm dosya sistemleri, xfsprogs paketi ile gelir), `mkfile` (Solaris, Mac OS gibi Unix tarzı sistemler için) kullanın.

## Sistem hata ayıklama

- For web debugging, `curl` and `curl -I` are handy, or their `wget` equivalents, or the more modern [`httpie`](https://github.com/jkbrzt/httpie).

- To know current cpu/disk status, the classic tools are `top` (or the better `htop`), `iostat`, and `iotop`. Use `iostat -mxz 15` for basic CPU and detailed per-partition disk stats and performance insight.

- For network connection details, use `netstat` and `ss`.

- For a quick overview of what's happening on a system, `dstat` is especially useful. For broadest overview with details, use [`glances`](https://github.com/nicolargo/glances).

- To know memory status, run and understand the output of `free` and `vmstat`. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.

- Java system debugging is a different kettle of fish, but a simple trick on Oracle's and some other JVMs is that you can run `kill -3 <pid>` and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs. The JDK's `jps`, `jstat`, `jstack`, `jmap` are useful. [SJK tools](https://github.com/aragozin/jvm-tools) are more advanced.

- Use [`mtr`](http://www.bitwizard.nl/mtr/) as a better traceroute, to identify network issues.

- For looking at why a disk is full, [`ncdu`](https://dev.yorhel.nl/ncdu) saves time over the usual commands like `du -sh *`.

- To find which socket or process is using bandwidth, try [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs).

- The `ab` tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try `siege`.

- For more serious network debugging, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), or [`ngrep`](http://ngrep.sourceforge.net/).

- Know about `strace` and `ltrace`. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. Note the profiling option (`-c`), and the ability to attach to a running process (`-p`). Use trace child option (`-f`) to avoid missing important calls.

- Know about `ldd` to check shared libraries etc — but [never run it on untrusted files](http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).

- Know how to connect to a running process with `gdb` and get its stack traces.

- Use `/proc`. It's amazingly helpful sometimes when debugging live problems. Examples: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (where `xxx` is the process id or pid).

- When debugging why something went wrong in the past, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) can be very helpful. It shows historic statistics on CPU, memory, network, etc.

- For deeper systems and performance analyses, look at `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_%28Linux%29), and [`sysdig`](https://github.com/draios/sysdig).

- Check what OS you're on with `uname` or `uname -a` (general Unix/kernel info) or `lsb_release -a` (Linux distro info).

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).

- If you delete a file and it doesn't free up expected disk space as reported by `du`, check whether the file is in use by a process:
`lsof | grep deleted | grep "filename-of-my-big-file"`


## Tek satırlık komutlar

A few examples of piecing together commands:

- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via `sort`/`uniq`. Suppose `a` and `b` are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the `-T` option if `/tmp` is on a small root partition.) See also the note about `LC_ALL` above and `sort`'s `-u` option (left out for clarity below).
```sh
      sort a b | uniq > c   # c is a union b
      sort a b | uniq -d > c   # c is a intersect b
      sort a b b | uniq -u > c   # c is set difference a - b
```

- Pretty-print two JSON files, normalizing their syntax, then coloring and paginating the result:
```
      diff <(jq --sort-keys . < file1.json) <(jq --sort-keys . < file2.json) | colordiff | less -R
```

- Use `grep . *` to quickly examine the contents of all files in a directory (so each line is paired with the filename), or `head -100 *` (so each file has a heading). This can be useful for directories filled with config settings like those in `/sys`, `/proc`, `/etc`.


- Summing all numbers in the third column of a text file (this is probably 3X faster and 3X less code than equivalent Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- To see sizes/dates on a tree of files, this is like a recursive `ls -l` but is easier to read than `ls -lR`:
```sh
      find . -type f -ls
```

- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

- To continuously monitor changes, use `watch`, e.g. check changes to files in a directory with `watch -d -n 2 'ls -rtlh | tail'` or to network settings while troubleshooting your wifi settings with `watch -d -n 2 ifconfig`.

- Run this function to get a random tip from this document (parses Markdown and extracts an item):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          sed '/cowsay[.]png/d' |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80 | iconv -t US
      }
```


## Karmaşık ama kullanışlı

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `printenv`: print out environment variables (useful in debugging and scripts)

- `look`: find English words (or lines in a file) beginning with a string

- `cut`, `paste` and `join`: data manipulation

- `fmt`: format text paragraphs

- `pr`: format text into pages/columns

- `fold`: wrap lines of text

- `column`: format text fields into aligned, fixed-width columns or tables

- `expand` and `unexpand`: convert between tabs and spaces

- `nl`: add line numbers

- `seq`: print numbers

- `bc`: calculator

- `factor`: factor integers

- [`gpg`](https://gnupg.org/): encrypt and sign files

- `toe`: table of terminfo entries

- `nc`: network debugging and data transfer

- `socat`: socket relay and tcp port forwarder (similar to `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): network traffic visualization

- `dd`: moving data between files or devices

- `file`: identify type of a file

- `tree`: display directories and subdirectories as a nesting tree; like `ls` but recursive

- `stat`: file info

- `time`: execute and time a command

- `timeout`: execute a command for specified amount of time and stop the process when the specified amount of time completes.

- `lockfile`: create semaphore file that can only be removed by `rm -f`

- `logrotate`: rotate, compress and mail logs.

- `watch`: run a command repeatedly, showing results and/or highlighting changes

- [`when-changed`](https://github.com/joh/when-changed): runs any command you specify whenever it sees file changed. See `inotifywait` and `entr` as well.

- `tac`: print files in reverse

- `comm`: compare sorted files line by line

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split` and `csplit`: splitting files

- `sponge`: read all input before writing it, useful for reading from then writing to the same file, e.g., `grep -v something some-file | sponge some-file`

- `units`: unit conversions and calculations; converts furlongs per fortnight to twips per blink (see also `/usr/share/units/definitions.units`)

- `apg`: generates random passwords

- `xz`: high-ratio file compression

- `ldd`: dynamic library info

- `nm`: symbols from object files

- `ab` or [`wrk`](https://github.com/wg/wrk): benchmarking web servers

- `strace`: system call debugging

- [`mtr`](http://www.bitwizard.nl/mtr/): better traceroute for network debugging

- `cssh`: visual concurrent shell

- `rsync`: sync files and folders over SSH or in local file system

- [`wireshark`](https://wireshark.org/) and [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): packet capture and network debugging

- [`ngrep`](http://ngrep.sourceforge.net/): grep for the network layer

- `host` and `dig`: DNS lookups

- `lsof`: process file descriptor and socket info

- `dstat`: useful system stats

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat`: Disk usage stats

- `mpstat`: CPU usage stats

- `vmstat`: Memory usage stats

- `htop`: improved version of top

- `last`: login history

- `w`: who's logged on

- `id`: user/group identity info

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): historic system stats

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs): network utilization by socket or process

- `ss`: socket statistics

- `dmesg`: boot and system error messages

- `sysctl`: view and configure Linux kernel parameters at run time

- `hdparm`: SATA/ATA disk manipulation/performance

- `lsblk`: list block devices: a tree view of your disks and disk partitions

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, including CPU, BIOS, RAID, graphics, devices, etc.

- `lsmod` and `modinfo`: List and show details of kernel modules.

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## Sadece macOS

These are items relevant *only* on macOS.

- Package management with `brew` (Homebrew) and/or `port` (MacPorts). These can be used to install on macOS many of the above commands.

- Copy output of any command to a desktop app with `pbcopy` and paste input from one with `pbpaste`.

- To enable the Option key in macOS Terminal as an alt key (such as used in the commands above like **alt-b**, **alt-f**, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key".

- To open a file with a desktop app, use `open` or `open -a /Applications/Whatever.app`.

- Spotlight: Search files with `mdfind` and list metadata (such as photo EXIF info) with `mdls`.

- Be aware macOS is based on BSD Unix, and many commands (for example `ps`, `ls`, `tail`, `awk`, `sed`) have many subtle variations from Linux, which is largely influenced by System V-style Unix and GNU tools. You can often tell the difference by noting a man page has the heading "BSD General Commands Manual." In some cases GNU versions can be installed, too (such as `gawk` and `gsed` for GNU awk and sed). If writing cross-platform Bash scripts, avoid such commands (for example, consider Python or `perl`) or test carefully.

- To get macOS release information, use `sw_vers`.

## Sadece Windows

These items are relevant *only* on Windows.

### Ways to obtain Unix tools under Windows

- Access the power of the Unix shell under Microsoft Windows by installing [Cygwin](https://cygwin.com/). Most of the things described in this document will work out of the box.

- On Windows 10, you can use [Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about), which provides a familiar Bash environment with Unix command line utilities.

- If you mainly want to use GNU developer tools (such as GCC) on Windows, consider [MinGW](http://www.mingw.org/) and its [MSYS](http://www.mingw.org/wiki/msys) package, which provides utilities such as bash, gawk, make and grep. MSYS doesn't have all the features compared to Cygwin. MinGW is particularly useful for creating native Windows ports of Unix tools.

- Another option to get Unix look and feel under Windows is [Cash](https://github.com/dthree/cash). Note that only very few Unix commands and command-line options are available in this environment.

### Useful Windows command-line tools

- You can perform and script most Windows system administration tasks from the command line by learning and using `wmic`.

- Native command-line Windows networking tools you may find useful include `ping`, `ipconfig`, `tracert`, and `netstat`.

- You can perform [many useful Windows tasks](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) by invoking the `Rundll32` command.

### Cygwin tips and tricks

- Install additional Unix programs with the Cygwin's package manager.

- Use `mintty` as your command-line window.

- Access the Windows clipboard through `/dev/clipboard`.

- Run `cygstart` to open an arbitrary file through its registered application.

- Access the Windows registry with `regtool`.

- Note that a `C:\` Windows drive path becomes `/cygdrive/c` under Cygwin, and that Cygwin's `/` appears under `C:\cygwin` on Windows. Convert between Cygwin and Windows-style file paths with `cygpath`. This is most useful in scripts that invoke Windows programs.

## Daha fazla kaynak

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): A more in-depth guide for the macOS command line.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.
- [shellcheck](https://github.com/koalaman/shellcheck): A shell script static analysis tool. Essentially, lint for bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): The sadly complex minutiae on how to handle filenames correctly in shell scripts.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): More commands and tools helpful for doing data science, from the book of the same name

## Sorumluluk reddi

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)


## Lisans

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
