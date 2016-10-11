# Ongelmat, joihin törmättiin kehityksen aikana

## Front-end

### Miten Reactilla vaihdetaan renderöityjä komponentteja?

Nyt kun meillä ei ole erikseen reitittävää serveriä joka antaisi eri `html`-tiedostoja URL-reitin perusteella, meidän täytyy hoitaa reititys jotenkin muuten. Löysimme verkosta tähän ratkaisun kirjastosta `react-router`. Reititys toimii täysin client-sidessa.

### Miten tarjoillaan tiedostot?

Päätimme pitää `tekislauta-server`in dedikoituna pelkästään rajapinnalle, joten emme voi tarjoilla clientside-tiedostoja sitä kautta. Löysimme Herokun blogipostin [*Deploying React with Zero Configuration*](https://blog.heroku.com/deploying-react-with-zero-configuration), joka ehdotti Heroku buildpackia [`create-react-app-buildpack`](https://github.com/mars/create-react-app-buildpack).

`create-react-app-buildpack` tarjoilee buildatut, staattiset tiedostot nginx-serverillä.

### Miten `react-router`in rumat risuaidat saadaan pois?

`react-router`in reitti näyttää oletuksena esimerkiksi tältä:

    http://tekislauta.fi/#/boards/b/

Tämä johtuu siitä, että frontendin React-sovellus toimii periaatteessa täysin yhdestä .html tiedostosta käsin, eli index.html:stä. Jotta saisimme hienomman reitin, esim

    http://tekislauta.fi/boards/b/

...tarvitsisimme reititystä serverillä. Meidän onneksemme yllä mainittu `create-react-app-buildpack` [tekee tämän puolestamme](https://github.com/mars/create-react-app-buildpack/blob/1f5369bf4d0c11bed331f9986d573ec52c3d9c0d/README.md#user-content-routing-clean-urls).

## Server

### Ongelma 1

Ratkaisu
