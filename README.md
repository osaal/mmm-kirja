# Modernit määrälliset menetelmät

"Modernit määrälliset menetelmät" on avoimen lähdekoodin ja lisenssin oppikirja tilastollisille menetelmille. Kirja soveltuu niin opiskelijoille ja aloitteleville tilastoanalyytikoille kuin kokeneemmille tieteentekijöille.

Kirja on julkaistu osoitteessa https://osaal.github.io/mmm-kirja. Lähdekoodia ei tarvitse käsitellä lukeakseen kirjaa.

## Lataa ja muokkaa

Muokataksesi kirjaa tarvitset seuraavat työkalut:

-  `R`-kieli, versio 4.4.1 ("Race for Your Life")
-  `Quarto`-kirjoitusohjelma, versio 1.5
-  `git`-versiointijärjestelmä, mikä tahansa versio

Git tulee asennettuna Mac- ja Linux-järjestelmissä automaattisesti. Windows-järjestelmässä joudut asentamaan sen itse.

Quarto ja R tulee asentaa itse. Jos sinulla on käytössä RStudion versio `v2022.07` tai uudempi, sinulla on Quarto valmiiksi asennettuna.

Aloita avaamalla komentokehotteen siihen kansioon, johon haluat kopioida lähdekoodin. Lataa lähdekoodin Git-repositorio:

``` {bash}
git clone https://github.com/osaal/mmm-kirja
```

Muokkaukset tehdään `.qmd`-tiedostoihin (Quarto-järjestelmän oma Markdown-tiedostomuoto). Voit tehdä muutokset haluamallasi teksti- tai koodieditorilla -- Quarton tiedostot voidaan avata vaikka Windowsin Muistio-ohjelmassa, joskin suosittelen kunnon koodieditoria.

Verkkosivu renderöidään käyttäen kahta Quarto-profiilia: `finnish` ja `swedish`. Nimensä mukaisesti profiilit renderöivät eri kieliversiot. Renderitiedostot löytyvät renderöinnin jälkeen kansioista `docs/fi` ja `docs/sv`

Nähdäksesi muutokset liveversiossa, voit preview-renderöidä sivuston:

``` {bash}
quarto preview --profile $KIELIVERSIO
```

Vaihda `$KIELIVERSIO`-muuttujaksi joko `finnish` tai `swedish`, riippuen muokkaamastasi kieliversiotiedostosta.

Kun olet valmis muokkausten kanssa, voit renderöidä lopullisen sivuston:

``` {bash}
quarto render --profile finnish
quarto render --profile swedish
```

Muista renderöidä molemmat profiilit, jotta sekä suomen- että ruotsinkieliset verkkosivut päivittyvät! **Tee tämä riippumatta päivittämistäsi tiedostoista.**

## Repositorion rakenne

Repositorion päätasolta löytyy Quarton konfigurointitiedostot `.yml`-muodossa sekä koko kirjan viitetiedosto `.bib`-muodossa.

Päätasolla on kolme kansiota:

1.  `docs`: Sisältää Quarton renderöimät HTML-sivut
2.  `.quarto`: Sisältää Quarton metatietoja (jos tätä ei löydy, Quarto rakentaa oman kun renderöit ensimmäisen kerran)
3.  `src`: Sisältää kirjan lähdekooditiedostot

`Src`-kansiolla on oma rakenne:

1.  `fi` sisältää suomenkieliset `.qmd`-tiedostot
2.  `sv` sisältää ruotsinkieliset `.qmd`-tiedostot
3.  `platforms` sisältää alustakohtaiset, upotettavat kooditiedostot

## Muutosten ehdottaminen repositorioon

Jos olet tehnyt muutoksia, jotka haluat ehdottaa hyväksyttäväksi kirjan repositorioon, noudata seuraavia sääntöjä:

-  Jos lisäät viitteen tekstiin, käytä Quarton viittausmenettelyä. Varmista, että viitteen bibliograafiset tiedot ovat lisättynä `references.bib`-tiedostoon ja että Quarton renderöintiprosessi yhdistää tekstiviitteen oikein lähdeluetteloon. Virheelliset viitteet johtavat pull requestin hylkäämiseen, sillä en voi lähteä jahtaamaan kaikkia viitteitä vapaa-ajallani.

-  Lisää omat kontribuutiotietosi muokkaamasi tiedostojen YAML-metadataan `author`-kentällä. Lisää ainakin alakentät `name` ja `email`. Halutessasi voit myös lisätä ORCID-numerosi, oman verkkosivusi sekä affiliaatiosi. Kontribuutiotietojen täydellinen puute johtaa pull requestin hylkäämiseen! Esimerkki täydestä kontribuutiotiedosta:

```{yaml}
author:
  - name: Matti Meikäläinen
    email: matti.meikalainen@sahkoposti.fi
    orcid: 0000-0000-0000-0000
    url: http://www.example.com
    affiliation:
      - name: Helsingin yliopisto
        department: Helsingin yliopiston kirjasto
        city: Helsinki
        url: https://www.helsinki.fi
```

-  Jos olet muuttanut tiedostoja, varmista, että olet dokumentoinnut kaikki muutokset osana commitviestiäsi. Dokumentointi voi olla useammassa commitissa, kunhan tieto on saatavilla. Heikko tai olematon muutosdokumentointi johtaa pull requestin hylkäämiseen!

-  Muista renderöidä *molemmat* kieliversiot -- riippumatta siitä, oletko muokannut vain yhtä vai molempia! Renderöinti korjaa samalla muun muassa hakutoiminnon cachet sekä mahdolliset sivurakennemuutokset, eli pienikin muutos tekstissä vaikuttaa automaattisesti useampaan tiedostoon. Renderöinnin puute johtaa pull requestin branchmenettelyyn (ks. alla), jotta muistan varmistaa, että uuden version renderi on päivitetty -- tämä hidastaa julkaisuprosessia.

-  Voit nopeuttaa pull requestisi käsittelyä kääntämällä kaikki muuttamasi tai lisäämäsi tiedostot suomeksi ja ruotsiksi. Käännöstyö ei ole pakollista pull requestin hyväksymiselle, mutta en julkaise yhtään muutoksia ennen kuin muutokset on peilattu molempiin julkaisukieliin.

Kun olet varma, että ehdotuksesi sopii kirjaan ja noudattaa yllä olevia sääntöjä, tee Pull Request GitHub-palvelussa. Kuvaile selkeästi requestissasi mahdolliset muutos- tai lisäystarpeet ja niiden motivaatiot.

Pull requestisi lopputulos voi olla yksi seuraavista:

1.  Pull request hylätään. Teen tämän, jos jokin yllä olevista säännöistä ei täyty, tai jos teksti ei vastaa laadultaan ja/tai tyyliltään kirjan sisältöä. Älä kuitenkaan hätäänny: kommentoin requestiin, miksi hylkäsin sen. Voit aina korjata tilanteen ja jättää uuden pull requestin.
2.  Pull request hyväksytään käännettäväksi. Teen tämän, jos yllä olevat säännöt täyttyvät ja teksti vastaa laadultaan ja/tai tyyliltään kirjan sisältöä, mutta tekstiä ei ole käännetty molemmille kielille. Tuolloin PR hyväksytään omaan branchiin, jossa suoritan käännöksen jahka ehdin. Käännöksen jälkeen renderöin PR:n branchin uudelleen ja mergaan sen julkaisuversioon.
3.  Pull request hyväksytään sellaisenaan. Teen tämän, jos säännöt täyttyvät, teksti sopii kirjaan ja olet kääntänyt muutokset/lisäykset molemmille kielille. PR:n renderöity materiaali mergataan suoraan julkaisuversioon.

## Ongelmien ilmoittaminen ja keskustelu

Jos löydät ongelman tai virheen tekstistä mutta et osaa itse korjata sitä, tai jos koet, että ongelmasta pitäisi keskustella enemmän ennen kuin joku (mieluisesti sinä!) ehdottaa korjauksen, voit jättää Issue-viestin GitHub-palvelussa.

# Moderna statistiska metoder

"Moderna statistiska metoder" är en lärobok i statistiska metoder med öppen källkod och öppen licens. Boken passar såväl studerande och nybörjare i statistik som längre hunna forskare.

Boken är publicerad vid addressen https://osaal.github.io/mmm-kirja. Källkoden behövs inte för att läsa boken.

## Ladda ned och modifiera

För att modifiera boken behöver du följande verktyg:

-  `R`-språket, version 4.4.1 ("Race for Your Life")
-  `Quarto`-författningssystemet, version 1.5
-  `git`-versionkontrollsystemet, vilken som helst version

Git är förinstallerat på Mac- och Linux-system. På Windows-system bör du installera Git själv.

Quarto och R bör installeras själv. Om du använder RStudios version `v2022.07` eller nyare har du Quarto färdigt installerat.

Börja med att öppna en terminal i mappen du vill kopiera källkoden till. Ladda ned källkodens Git-repositorie:

``` {bash}
git clone https://github.com/osaal/mmm-kirja
```

Modifieringarna till texten görs i `.qmd`-filer (Quarto-systemets egen Markdown-filformat). Du kan göra ändringar i valfritt text- eller kodprogram -- Quartos filer kan till och med öppnas i Windows Notepad-program, men jag rekommenderar ett propert kodprogram.

Nätsidan sammanfogas med två Quarto-profiler: `finnish` och `swedish`. Så som namnen föreslår sammanfogar profilerna de olika språkversionerna. De sammanfogade filerna finns sedan i mapperna `docs/fi` och `docs/sv`.

För att se förändringarna i liveversionen kan du preview-sammanfoga nätsidan:

``` {bash}
quarto preview --profile $SPRÅKVERSION
```

Byt ut `$SPRÅKVERSION`-variabeln till antingen `finnish` eller `swedish` enligt vilken språkversion du har modifierat.

När du är färdig med dina modifikationer kan du sammanfoga den slutliga nätsidan:

``` {bash}
quarto render --profile finnish,swedish
```

Kom ihåg att sammanfoga bägge profilerna så att både den finska och svenska versionen uppdateras! **Gör detta oavsett vilken version du har uppdaterat.**

## Strukturena av filrepositoriet

Repositoriets huvudnivå innehåller Quarto-konfigureringsfilerna i `.yml`-format samt hela bokens referensfil i `.bib`-format.

Huvudnivån har tre mapper:

1.  `docs`: Innehåller HTML-filerna som Quarto sammanfogar
2.  `.quarto`: Innehåller Quartos metadata (Quarto skapar denna vid första sammanfogningen om den inte finns)
3.  `src`: Innehåller bokens källfiler

`Src`-mappen har en egen struktur:

1.  `fi` innehåller de finska `.qmd`-filerna
2.  `sv` innehåller de svenska `.qmd`-filerna
3.  `platforms` innehåller plattformsspecifika kodfiler för inbäddning i textfilerna

## Förändringsförslag

Om du har gjort förändringar som du vill föreslå till inkludering i bokens repositorium, följ följande regler:

-  Om du lägger till en referens, använd Quartos referenspraxis. Säkerställ att referensens bibliografiska information finns tillagd i `references.bib`-filen och att Quartos sammanfogningsprocess korrekt associerar textreferenserna med referensfilens innehåll. Felaktiga referenser leder till förnekande av din pull request, eftersom jag inte har tid att jaga referenser i min fritid.

-  Lägg till dina uppgifter i YAML-metadata för de filer du har modifierat, i `author`-fältet. Lägg åtminstone till underfälten `name` och `email`. Om du vill kan du även lägga till ditt ORCID-nummer, din webbplats samt din affiliation. Om kontributionsuppgifterna fullständigt saknas förnekar jag din pull request! Exempel på fullständiga kontributionsuppgifter:

```{yaml}
author:
  - name: Matti Meikäläinen
    email: matti.meikalainen@sahkoposti.fi
    orcid: 0000-0000-0000-0000
    url: http://www.example.com
    affiliation:
      - name: Helsingin yliopisto
        department: Helsingin yliopiston kirjasto
        city: Helsinki
        url: https://www.helsinki.fi
```

-  Om du har ändrat på filer ska du säkerställa att alla ändringar är dokumenterade i dina commit-meddelande. Dokumentationen kan ske över flera commits, så länge informationen är tillgänglig. Svag eller obefintlig ändringsdokumentation leder till förnekande av din pull request!

-  Kom ihåg att sammanfoga *bägge* språkversion, oavsett om du har modifierat ena eller båda. Sammanfogningen fixar bland annat sökfunktionens cache samt eventuella ändringar i webbsidestrukturen, så en liten förändring i texten påverkar automatiskt på flera olika filer. Avsaknaden av sammanfogning leder till branch-processering av din pull request (se nedan), för att säkerställa att den nya versionens sammanfogning är korrekt. Detta saktar ned publikationsprocessen.

-  Du kan försnabba behandlingen av din pull request genom att översätta alla förändringar och tilläggningar du gjort till finska och svenska. Översättningsarbetet är inte obligatoriskt för ett godkännande av din pull request, men inga förändringar blir publicerade före de är reflekterade i bägge språkversion.

När du är säker att ditt förslag passar till boken och följer ovannämnda regler kan du göra en Pull Request i GitHub. Beskriv alla ändrings- eller tilläggsförslag samt deras motivationer tydligt i din request.

Slutresultaten på din pull request kan vara en av följande:

1.  Din pull request förkastas. Jag gör detta om någon av ovannämnda regler inte uppfylls, eller om texten inte motsvarar bokens stil eller kvalitet. Ge inte genast upp: jag kommenterar requesten med förklaring på varför den blev förkastad. Du kan alltid fixa problemet och lämna en ny pull request.
2.  Din pull request godkänns för översättning. Jag gör detta om de ovannämnda reglerna uppfylls och texten motsvarar bokens stil och kvalitet, men texten är inte översatt till bägge språk. I detta fall godkänner jag PR:en till sin egen branch och översätter den så fort jag hinner. Efter översättningen sammanfogar jag PR:ens branch på nytt och publicerar den i huvudversionen.
3.  Din pull request godkänns som sådan. Jag gör detta om de ovannämnda reglerna uppfylls, texten motsvarar bokens stilistiska krav och du har översätt alla förändringar eller tillägg till bägge språk. De sammanfogade filerna i PR:en publiceras direkt i huvudversionen.

## Rapportering av problem samt diskussion

Om du finner ett problem eller fel i boken men inte vet hur du fixar det själv, eller om du känner att problemet bör diskuteras före någon (helst du!) föreslår en lösning, så kan du lämna ett Issue-meddelande i GitHub.
