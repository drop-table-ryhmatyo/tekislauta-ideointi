# Taulukot

## Käsitteitä

* Lauta (Board)
 * Nimi (esim. `Satunnainen`)
 * Lyhenne (esim. `b`)
 * Kuvaus (esim. `The stories and information posted here are artistic works of fiction and falsehood.`)
* Lanka (Thread)
 * Langan ulkopuolelle näkyvä numero on sama kuin ensimmäisen viestin numero
 * Otsikko
 * Luomispäivä (toisaalta sama tieto löytyy langan ensimmäisestä viestistä)
* Viestit (Posts)
 * Viestin numero (lautakohtaisesti uniikki)
 * Tekstisisältö
 * Nimi? esim. tripcode tai vaihtoehtoisesti ID jonka voisi luoda esim hashaamalla (ip + langan id)
  * Sallii halutessa yksittäisten käyttäjien vastausten seurannan

Käsitteissä erikseen mainittu langan ja viestin numero, koska ne ovat lautakulttuurissa erityisesti esillä
 * Esim. toisen viestiin vastataan luomalla uusi viesti ja sisältämällä viestiin `>>1234` missä 1234 on vastattavan viestin uniikki numero
 * Viestinumeroiden tulee olla lautakohtaisesti uniikkeja, jotta voi viitata toiseen lankaan tai tehdä get-lankoja (nice quads bro)
