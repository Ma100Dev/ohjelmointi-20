---
path: '/osa-4/2-oliot-listalla'
title: 'Oliot listalla'
hidden: false
---


<text-box variant='learningObjectives' name='Oppimistavoitteet'>

- Osaat lisätä olioita listalle.
- Osaat käydä listalla olevia olioita läpi.

</text-box>


Listalle lisättävien muuttujien tyyppi määrätään listan luomisen yhteydessä annettavan tyyppiparametrin avulla. Esimerkiksi `ArrayList<String>` sisältää merkkijonoja, `ArrayList<Integer>` sisältää kokonaislukuja, ja `ArrayList<Double>` sisältää liukulukuja.

Alla olevassa esimerkissä lisätään ensin merkkijonoja listalle, jonka jälkeen listalla olevat merkkijonot tulostetaan yksitellen.


```java
ArrayList<String> nimet = new ArrayList<>();

// merkkijono voidaan lisätä ensin muuttujaan
String nimi = "Betty Jennings";
// ja sitten lisätä se listalle
nimet.add(nimi);

// merkkijono voidaan myös lisätä suoraan listalle:
nimet.add("Betty Snyder");
nimet.add("Frances Spence");
nimet.add("Kay McNulty");
nimet.add("Marlyn Wescoff");
nimet.add("Ruth Lichterman");

// listan alkioiden läpikäynti onnistuu useamman erilaisen
// toistolauseen avulla

// 1. while-toistolause
int indeksi = 0;
while (indeksi < nimet.size()) {
    System.out.println(nimet.get(indeksi));
    indeksi = indeksi + 1;
}

// 2. for-toistolause indeksillä
for (int i = 0; i < nimet.size(); i++) {
    System.out.println(nimet.get(i));
}

System.out.println();
// 3. for-each toistolause (ei indeksiä)
for (String nimi: nimet) {
    System.out.println(nimi);
}
```

<sample-output>

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

Betty Jennings
Betty Snyder
Frances Spence
Kay McNulty
Marlyn Wescoff
Ruth Lichterman

</sample-output>


## Olioiden lisääminen listalle

Merkkijonot ovat olioita, joten ei liene yllätys että listalla voi olla muunkinlaisia olioita. Tarkastellaan seuraavaksi listan ja olioiden yhteistoimintaa tarkemmin.

Oletetaan, että käytössämme on alla oleva henkilöä kuvaava luokka.

```java
public class Henkilo {

    private String nimi;
    private int ika;
    private int paino;
    private int pituus;

    public Henkilo(String nimi) {
        this.nimi = nimi;
        this.ika = 0;
        this.paino = 0;
        this.pituus = 0;
    }

    public String getNimi() {
        return this.nimi;
    }

    public int getIka() {
        return this.ika;
    }

    public void vanhene() {
        this.ika = this.ika + 1;
    }

    public void setPituus(int uusiPituus) {
        this.pituus = uusiPituus;
    }

    public void setPaino(int uusiPaino) {
        this.paino = uusiPaino;
    }

    public double painoindeksi() {
        double pituusPerSata = this.pituus / 100.0;
        return this.paino / (pituusPerSata * pituusPerSata);
    }

    @Override
    public String toString() {
        return this.nimi + ", ikä " + this.ika + " vuotta";
    }
}
```

Olioiden käsittely listalla ei oikeastaan poikkea aiemmin näkemästämme listan käytöstä millään tavalla. Oleellista on vain listalle lisättävien olioiden tyypin määrittely listan luomisen yhteydessä.

Alla olevassa esimerkissä luodaan ensin Henkilo-tyyppisille olioille tarkoitettu lista, jonka jälkeen listalle lisätään henkilöolioita. Lopulta henkilöoliot tulostetaan yksitellen.

```java
ArrayList<Henkilo> henkilot = new ArrayList<>();

// henkilöolio voidaan ensin luoda
Henkilo juhana = new Henkilo("Juhana");
// ja sitten lisätä se listalle
henkilot.add(juhana);

// henkilöolio voidaan myös lisätä listalle "samassa lauseessa"
henkilot.add(new Henkilo("Matti"));
henkilot.add(new Henkilo("Martin"));

for (Henkilo henkilo: henkilot) {
    System.out.println(henkilo);
}
```

<sample-output>

Juhana, ikä 0 vuotta
Matti, ikä 0 vuotta
Martin, ikä 0 vuotta

</sample-output>



## Käyttäjän syöttämät oliot listalle

Aiemmin käyttämämme rakenne syötteiden lukemiseen on yhä varsin käytännöllinen.

```java
Scanner lukija = new Scanner(System.in);
ArrayList<Henkilo> henkilot = new ArrayList<>();

// Luetaan henkilöiden nimet käyttäjältä
while (true) {
    System.out.print("Kirjoita nimi, tyhjä lopettaa: ");
    String nimi = lukija.nextLine();
    if (nimi.isEmpty()) {
        break;
    }

    // Lisätään listalle uusi henkilo-olio, jonka
    // nimi on käyttäjän syöttämä
    henkilot.add(new Henkilo(nimi));
}

// Tulostetaan syötettyjen henkilöiden määrä sekä henkilöt
System.out.println();
System.out.println("Henkilöitä yhteensä: " + henkilot.size());
System.out.println("Henkilöt: ");

for (Henkilo henkilo: henkilot) {
    System.out.println(henkilo);
}
```

<sample-output>

Kirjoita nimi, tyhjä lopettaa: **Alan Kay**
Kirjoita nimi, tyhjä lopettaa: **Ivan Sutherland**
Kirjoita nimi, tyhjä lopettaa: **Kristen Nygaard**

Henkilöitä yhteensä: 3
Henkilöt:
Alan Kay, ikä 0 vuotta
Ivan Sutherland, ikä 0 vuotta
Kristen Nygaard, ikä 0 vuotta

</sample-output>

<programming-exercise name='Esineet' tmcname='osa04-Osa04_17.Esineet'>


Toteuta tässä kuvattu ohjelma luokkaan `Esineet`. **Huom!** Älä muuta luokkaa `Esine`.

Kirjoita ohjelma, joka lukee käyttäjältä esineiden nimiä. Mikäli nimi on tyhjä, lopeta lukeminen. Mikäli nimi ei ole tyhjä, luo nimen perusteella uusi esine, jonka lisäät `esineet`-listalle.

Tulosta tämän jälkeen esineet `Esine`-luokan `toString`-metodia hyödyntäen. Luokan `Esine` toteutus pitää syöttämäsi nimen lisäksi kirjaa esineen luomishetkestä.

Ohjelman esimerkkitulostus:

<sample-output>

Nimi: **Suo**
Nimi: **Kuokka**
Nimi:

Suo (luotu: 06.07.2018 12:34:56)
Kuokka (luotu: 06.07.2018 12:34:57)

</sample-output>

</programming-exercise>

## Useamman arvon lukeminen

Mikäli luokan konstruktori vaatii useampia parametreja, voi käyttäjältä kysyä enemmän tietoa. Oletetaan, että luokan `Henkilo` konstruktori on seuraavanlainen.

```java
public class Henkilo {

    private String nimi;
    private int ika;
    private int paino;
    private int pituus;

    public Henkilo(String nimi, int ika) {
        this.nimi = nimi;
        this.ika = ika;
        this.paino = 0;
        this.pituus = 0;
    }

    // metodit
}
```

Olion luominen vaatii siis kaksiparametrisen konstruktorin kutsumista.

Mikäli haluamme lukea tällaisia olioita käyttäjältä, tulee lukemisessa kysyä jokainen parametri erikseen. Alla olevassa esimerkissä käyttäjältä luetaan erikseen nimi ja ikä. Mikäli nimi on tyhjä, lukeminen lopetetaan.

Henkilöt tulostetaan lukemisen jälkeen.


```java
Scanner lukija = new Scanner(System.in);
ArrayList<Henkilo> henkilot = new ArrayList<>();

// Luetaan henkilöiden tiedot käyttäjältä
while (true) {
    System.out.print("Kirjoita nimi, tyhjä lopettaa: ");
    String nimi = lukija.nextLine();
    if (nimi.isEmpty()) {
        break;
    }

    System.out.print("Kirjoita henkilön " + nimi + " ikä: ");

    int ika = Integer.valueOf(lukija.nextLine());

    // Lisätään listalle uusi henkilo-olio, jonka
    // nimen ja iän käyttäjä syötti
    henkilot.add(new Henkilo(nimi, ika));
}

// Tulostetaan syötettyjen henkilöiden määrä sekä henkilöt
System.out.println();
System.out.println("Henkilöitä yhteensä: " + henkilot.size());
System.out.println("Henkilöt: ");

for (Henkilo henkilo: henkilot) {
    System.out.println(henkilo);
}
```

<sample-output>

Kirjoita nimi, tyhjä lopettaa: **Grace Hopper**
Kirjoita henkilön Grace Hopper ikä: **85**
Kirjoita nimi, tyhjä lopettaa:

Henkilöitä yhteensä: 1
Henkilöt:
Grace Hopper, ikä 85 vuotta

</sample-output>

<programming-exercise name='Henkilotiedot' tmcname='osa04-Osa04_18.Henkilotiedot'>

Toteuta tässä kuvattu ohjelma luokkaan `Henkilotiedot`. **Huom!** Älä muuta luokkaa `Henkilotieto`.

Kirjoita ohjelma, joka lukee käyttäjältä henkilötietoja. Käyttäjä syöttää etunimen, sukunimen, ja henkilötunnuksen. Mikäli etunimi on tyhjä, lopeta lukeminen. Mikäli etunimi ei ole tyhjä, lue loput tiedot ja luo käyttäjän syöttämistä tiedoista olio, jonka lisäät `henkilotiedot`-listalle.

Kun käyttäjä on lopettanut tietojen syöttämisen (käyttäjä syöttää tyhjän etunimen), poistu toistolauseesta.

Tulosta tämän jälkeen henkilötiedot siten, että jokaisesta syötetystä oliosta tulostetaan etunimi ja sukunimi välilyönnillä erotettuna (henkilötunnusta ei tulosteta!). Alla esimerkki ohjelman suorituksesta.

<sample-output>

Etunimi: **Jean**
Sukunimi: **Bartik**
Henkilötunnus: **271224**
Etunimi: **Betty**
Sukunimi: **Holberton**
Henkilötunnus: **070317**
Etunimi:

Jean Bartik
Betty Holberton

</sample-output>

</programming-exercise>

<text-box type="info" name="Määrämuotoisen tiedon lukeminen">

Yllä olevassa esimerkissä ja tehtävässä tiedot syötettiin rivi riviltä. Ohjelmassa voisi toki pyytää tietoja määrämuotoisessa muodossa, esimerkiksi pilkulla eroteltuna.

Ohjelma, jossa nimi ja ikä tulisi syöttää pilkulla eroteltuna voisi toimia seuraavalla tavalla.

```java
Scanner lukija = new Scanner(System.in);
ArrayList<Henkilo> henkilot = new ArrayList<>();

// Luetaan henkilöiden tiedot käyttäjältä
System.out.println("Kirjoita tiedot pilkulla eroteltuna, esim: Leevi,2")
while (true) {
    System.out.print("Kirjoita tiedot, tyhjä lopettaa: ");
    String tiedot = lukija.nextLine();
    if (tiedot.isEmpty()) {
        break;
    }

    String[] palat = tiedot.split(",");
    String nimi = palat[0];
    int ika = Integer.valueOf(palat[1]);
    henkilot.add(new Henkilo(nimi, ika));
}

// Tulostetaan syötettyjen henkilöiden määrä sekä henkilöt
System.out.println();
System.out.println("Henkilöitä yhteensä: " + henkilot.size());
System.out.println("Henkilöt: ");

for (Henkilo henkilo: henkilot) {
    System.out.println(henkilo);
}
```

<sample-output>

Kirjoita tiedot pilkulla eroteltuna, esim: Leevi,2

Kirjoita tiedot, tyhjä lopettaa: **Leevi,2**
Kirjoita tiedot, tyhjä lopettaa: **Anton,2**
Kirjoita tiedot, tyhjä lopettaa: **Sylvi,0**
Kirjoita tiedot, tyhjä lopettaa:

Henkilöitä yhteensä: 3
Henkilöt:
Leevi, ikä 2 vuotta
Anton, ikä 2 vuotta
Sylvi, ikä 0 vuotta

</sample-output>

</text-box>


## Rajattu tulostus listalta

Listalla olevia olioita voidaan myös tarkastella listan läpikäynnin yhteydessä. Alla olevassa esimerkissä käyttäjältä kysytään ensin ikäraja, jonka jälkeen tulostetaan ne oliot, joiden ikä on vähintään käyttäjän syöttämä ikäraja.

```java
// Oletetaan, että käytössämme on henkilot-lista,
// joka sisältää henkilöolioita

System.out.print("Mikä ikäraja? ");
int ikaraja = Integer.valueOf(lukija.nextLine());

for (Henkilo henkilo: henkilot) {
    if (henkilo.getIka() >= ikaraja) {
        System.out.println(henkilo);
    }
}
```


<programming-exercise name='Televisio-ohjelmat' tmcname='osa04-Osa04_19.TelevisioOhjelmat'>

Tehtäväpohjassa on valmiina televisio-ohjelmaa kuvaava luokka TelevisioOhjelma. Luokalla on oliomuuttujat nimi ja pituus, konstruktori, ja muutamia metodeja.

Toteuta ohjelma, joka ensin lukee käyttäjältä televisio-ohjelmia. Kun käyttäjä syöttää tyhjän ohjelman nimen, televisio-ohjelmien lukeminen lopetetaan.

Tämän jälkeen käyttäjältä kysytään ohjelman maksimipituutta. Kun käyttäjä on syöttänyt ohjelman maksimipituuden, tulostetaan kaikki ne ohjelmat, joiden pituus on pienempi tai yhtäsuuri kuin haluttu maksimipituus.

<sample-output>

Nimi: **Salatut elämät**
Pituus: **30**
Nimi: **Miehen puolikkaat**
Pituus: **30**
Nimi: **Remppa vai muutto**
Pituus: **60**
Nimi: **House**
Pituus: **60**

Ohjelman maksimipituus? **30**
Salatut elämät, 30 minuuttia
Miehen puolikkaat, 30 minuuttia

</sample-output>

</programming-exercise>


<programming-exercise name='Kirjat (2 osaa)' tmcname='osa04-Osa04_20.Kirjat'>

Toteuta ohjelma, joka ensin lukee kirjojen tietoja käyttäjältä. Jokaisesta kirjasta tulee lukea kirjan nimi, sivujen lukumäärä sekä julkaisuvuosi. Kirjojen lukeminen lopetetaan kun käyttäjä syöttää tyhjän kirjan nimen.

Tämän jälkeen käyttäjältä kysytään mitä tulostetaan. Jos käyttäjä syöttää merkkijonon "kaikki", tulostetaan kirjojen nimet, sivujen lukumäärät sekä julkaisuvuodet. Jos taas käyttäjä syöttää merkkijonon "nimi", tulostetaan vain kirjojen nimet.

Ohjelmaa varten kannattanee toteuttaa yksittäistä kirjaa kuvaava Kirja-luokka. Tehtävä on kokonaisuudessaan kahden tehtäväpisteen arvoinen.

<sample-output>

Nimi: **Minä en sitten muutu**
Sivuja: **201**
Julkaisuvuosi: **2010**
Nimi: **Nalle Puh ja elämisen taito**
Sivuja: **100**
Julkaisuvuosi: **2005**
Nimi: **Beautiful Code**
Sivuja: **593**
Julkaisuvuosi: **2007**
Nimi: **KonMari**
Sivuja: **222**
Julkaisuvuosi: **2011**
Nimi:

Mitä tulostetaan? **kaikki**
Minä en sitten muutu, 201 sivua, 2010
Nalle Puh ja elämisen taito, 100 sivua, 2005
Beautiful Code, 593 sivua, 2007
KonMari, 222 sivua, 2011

</sample-output>


<sample-output>

Nimi: **Minä en sitten muutu**
Sivuja: **201**
Julkaisuvuosi: **2010**
Nimi: **Nalle Puh ja elämisen taito**
Sivuja: **100**
Julkaisuvuosi: **2005**
Nimi: **Beautiful Code**
Sivuja: **593**
Julkaisuvuosi: **2007**
Nimi: **KonMari**
Sivuja: **222**
Julkaisuvuosi: **2011**
Nimi:

Mitä tulostetaan? **nimi**
Minä en sitten muutu
Nalle Puh ja elämisen taito
Beautiful Code
KonMari

</sample-output>

</programming-exercise>
