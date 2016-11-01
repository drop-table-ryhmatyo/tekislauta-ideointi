# Ongelmat, joihin törmättiin kehityksen aikana

## Yleisiä
### Lauta vs. perinteinen foorumi
Päätimme alussa, että haluamme toteuttaa lautamaisen keskustelupalstan (vertaa 4chan, Ylilauta). Toteutusvaiheessa opimme, että lautamainen struktuuri (langat ovat ketju viestejä, langat ja viestit käyttävät samaa ID-ordinaalia) on epäkäytännöllinen toteuttaa ja luo ylimääräisiä ongelmia esimerkiksi serverin DAO-luokkia toteuttaessa.

Lautamainen foorumi on varmasti mahdollista toteuttaa elegantisti, mutta rajoitetun ajan, ajanhallinnan ja osaamisen takia emme päässeet sille tasolle tuotoksen kanssa, kuin olisimme halunneet.

### Projektin myöhästyminen
Ryhmän vältettävän projektin- ajanhallinnan takia keskityimme liikaa epäolennaisiin asioihin. Käytimme liikaa aikaa liian spesifeihin asioihin, sen sijaan, että saimme korkealla tasolla projektin vaaditut ominaisuudet toiminaan. Myönnämme, että projekti olisi varmasti mennyt paremmin, jos ryhmä ei olisi osallistunut ATK-YTP:lle ja KJYR:iin. Toivomme myös Ohjelmistotuotannon menetelmät -kurssin edesauttavan ajan- ja projektinhallinnassa tulevien kurssien harjoitustöissä.

## Front-end

### Miten Reactilla vaihdetaan renderöityjä komponentteja?

Nyt kun meillä ei ole erikseen reitittävää serveriä joka antaisi eri `html`-tiedostoja URL-reitin perusteella, meidän täytyy hoitaa reititys jotenkin muuten. Löysimme verkosta tähän ratkaisun kirjastosta `react-router`. Reititys toimii täysin client-sidessa.

### Miten tarjoillaan tiedostot?

Päätimme pitää `tekislauta-server`in dedikoituna pelkästään rajapinnalle, joten emme voi tarjoilla clientside-tiedostoja sitä kautta. Löysimme Herokun blogipostin [*Deploying React with Zero Configuration*](https://blog.heroku.com/deploying-react-with-zero-configuration), joka ehdotti Heroku buildpackia [`create-react-app-buildpack`](https://github.com/mars/create-react-app-buildpack).

`create-react-app-buildpack` tarjoilee buildatut, staattiset tiedostot nginx-serverillä.

### Miten `react-router`in rumat risuaidat saadaan pois?

`react-router`in reitti näyttää oletuksena `hashHistory`-historiatyyppiä käytettäessä esimerkiksi tältä:

    http://tekislauta.fi/#/boards/b/

Halusimme hienomman, virallisemmalta näyttävän reitin `http://tekislauta.fi/boards/b/`, mutta valitettavasti tämänlaisen reitin saa vain käyttäen `browserHistory`-historiatyyppiä. Valitettavasti yllä oleva reitti aiheuttaa sen, että selain tekee GET-pyynnön reitille `/boards/b/` eikä `/`, joten tarvitsisimme jonkinlaisen palvelimen tätä varten.

Meidän onneksemme, yllä mainittu `create-react-app-buildpack` [tekee tämän(kin) puolestamme](https://github.com/mars/create-react-app-buildpack/blob/1f5369bf4d0c11bed331f9986d573ec52c3d9c0d/README.md#user-content-routing-clean-urls)!

### Lankanäkymä kaatoi Chromen jos laudalla ei ollut yhtään lankaa
Lankanäkymä joutui loputtomaan looppiin jos laudalla ei ollut yhtää lankaa mukana. Ongelma johtui siitä, että sivun logiikka ohjaa selaimen ensimmäiselle lankasivulle (esim `/boards/b/0`) jos käyttäjä yrittää mennä olemassaolemattomalle sivulle (esim. sivulle 5 jos sivuja on 2). Logiikka toteutettiin käytännössä kyselyllä `if (nykyinenSivu >= sivumäärä)`, joka toimii kun `sivumäärä > 0`. Ongelma korjattiin varmistamalla lisäksi, että uudelleenohjausta ei tehdä jos sivuja on vain yksi ja ollaan jo kyseisellä sivulla.

## Server

### Projektin julkaisu herokuun
Applikaatio ei käynnisty herokussa, ja schema.sql tiedostoa ei löydy.

Ratkaisu

`mvn clean heroku:deploy`-kommennolla ja herokun maven riippuvuudella saatiin vihdoinkin sovelluus toimimaan. `this.getClass().getResourceAsStream()`-metodilla korjattiin tiedostonlukeminen. 
