---
title: Bevielio Zebra interneto konfigūravimas keliems kompiuteriams su Thomson SpeedTouch 585 v7
date: 2009-06-14 15:35:08
categories: .mp
---

**Problema**

Nusipirkome iš Teo bevielį modemą Thomson SpeedTouch 585 v7, kad galėtume ir staliniu, ir nešiojamuoju kompiuteriu namie naudotis (planas Optimalus+, internetas šviesolaidinis), bet, pasirodo, paršeliai sukonfigūravo taip, jog vienu metu abiem įrenginiais naudotis nebūtų negalima. Esu pasipiktinęs tokiu Teo elgesiu; aiškiai gviešiasi pinigo, pakiaulindami tūlam vartotojui taip, jog tektų skambinti pagalbos telefonu 1518 ir mokėti 2 Lt/min,– na kas gi perką tą bevielį modemą tam, kad ir toliau tik vienu kompiuteriu galėtų vienu metu naudotis?

Tegu jie paspringsta – čia pateikiu informaciją, kaip susitvarkyti pačiam. Labai paprasta, bet niekur aiškiai internete neradau parašyta. Man veikia tiek su Windows XP, tiek su Ubuntu 9.04.

 

**Sprendimas trumpai**

<span style="text-decoration:underline;">Pirma.</span> Iš [Zebra interneto pagalbos tinklapio DUK \#53](http://internetas.zebra.lt/pagalba/duk#53) parsisiunčiame tinkamą konfigūracinį failą:

– jei internetas šviesolaidinis – [Gala nerūp](http://m.zebra.lt/files/LAN_5xx_DHC_1tv_v6.ini)i (vienas modemo lizdas paliekamas televizijai) arba [Gala rūpi](http://m.zebra.lt/files/LAN_5xx_DHC_2tv_v6.ini) (du lizdai paliekami televizijai (vadinasi, galima du televizorius prisijungt));

– konfigūraciniai failai kitiems variantams ir kitiems modemo modeliams yra to DUK \#53 [pdf faile](http://m.zebra.lt/Zebra_internetas/Modemai/Senu_modemu_pritaikymas_plius_planams_20090407.pdf).

1518 man pasakė, kad nesvarbu, ar modemo versija 6 ar 7 (nors ten parašyta, jog tinka tik 6). Mano paties yra v7.

<span style="text-decoration:underline;">Antra.</span> Dėl visa ko, atjungiame modemą nuo interneto (ištraukiame laidą iš antro lizdo), bet paliekame prijungtą prie kompiuterio (per pirmą ar trečią lizdą). Prisijungiame prie modemo per naršyklę adresu [192.168.1.254](http://192.168.1.254), susirandame, kur išsaugoti esamą konfigūraciją (dėl visa ko) ir įkelti naują konfigūracinį failą (mano atveju, abu buvo Thomson Gateway \> Configure \> [Save or Restore Configuration](http://192.168.1.254/cgi/b/bandr/?be=0&l0=0&l1=1&tid=BACKUP_RESTORE)). Išsaugome seną ir įkeliame naują.

<span style="text-decoration:underline;">Trečia.</span> Baigiame DHCP sesiją savo kompiuteryje (žr. apačioj, jei neaišku kaip), išjungiame modemą ir skambiname į Teo numeriu 1817, renkamės ketvirtą meniu punktą („Interneto ryšio sutrikimai“). Reikia paprašyti, kad atlaisvintų DHCP sesiją, nes susikonfigūravome savo modemą, kad kelis kompus vežtų. Kai atlaisvina, įjungiame modemą ir viskas turėtų veikti.

Man neveikė. Tai aš sumąsčiau palaukti tas dvi valandas (atjungęs modemą nuo interneto), kol MAC adreso rezervacija bus atšaukta ir galima bus pakišti naujai sukonfigūruotą modemą su jo MAC adresu. Tada jau veikė.

 

**Ką pravartu žinoti**

**1.** Kiekvienas aparatas su tinklo plokšte turi unikalų [MAC adresą](http://en.wikipedia.org/wiki/Mac_address). Kad draugiški kaimynai nesidalintų ryšio, Teo riboja interneto naudojimą vienam MAC adresui vienu metu. Praktiškai tai reiškia, jog internetu gali naudotis tik vienas kompiuteris vienu metu. Mūsų tikslas – bevielio modemo MAC adresą pakišti Teo, o jau pačiame modeme informaciją paskirstyti dviem kompiuteriams (tai vadinama *bridging*).

**2.** Sykį prisijungus prie interneto su vienu įrenginiu, interneto ryšys rezervuojamas jo MAC adresui gal dviem valandoms nuo paskutinio duomenų siuntimo. Norint panaikinti rezervaciją, galima daryti vieną iš dviejų:

i\) atjungti visus įrenginius nuo interneto, palaukti dvi valandas, perkrauti ir prijungti reikiamą įrenginį;

ii\) sustabdyti DHCP sesiją (atsijungt nuo interneto ir išlaisvinti IP adresą) ir paleist iš naujo. Tai daroma šitaip:

**Windows XP**: pirmajame (atjungiamajame) įrenginyje

– atsidaryti konsolę (Start \> Run… \> Parašyti <span style="font-family:courier new, courier;">cmd</span>, spaust Enter);

– rašyti <span style="font-family:courier new, courier;">ipconfig/release</span>, spaust Enter.

Tada antrajame (prijungiamajame) įrenginyje

– atsidaryti konsolę;

– rašyti <span style="font-family:courier new, courier;">ipconfig/release</span>, spaust Enter;

– rašyti <span style="font-family:courier new, courier;">ipconfig/renew</span>, spaust Enter.

**Ubuntu 9.04**: pirmajame (atjungiamajame) įrenginyje

– atsidaryti terminalą;

– rašyti <span style="font-family:courier new, courier;">ifconfig eth0 down</span>, spaust Enter (<span style="font-family:courier new, courier;">eth0</span> yra mūsų Ethernet ryšys; gali būti ir kitoks, reikia žiūrėti, prie kurio čia mes prisijungę per <span style="font-family:courier new, courier;">ifconfig</span>).

Tada antrajame (prijungiamajame) įrenginyje

– atsidaryti konsolę;

– rašyti <span style="font-family:courier new, courier;">ifconfig eth0 down</span>, spaust Enter;

– rašyti <span style="font-family:courier new, courier;">ifconfig eth0 up</span>, spaust Enter.

**3.** Modemą galima pasiekti ir konfigūruoti adresu [192.168.1.254](http://192.168.1.254), kuris įvedamas naršyklėje.
