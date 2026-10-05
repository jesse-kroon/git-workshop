# Wat is Git?

Git is een *gedistribueerd* **versiebeheersysteem** [1].

[1] <a href="http://git-scm.com/about">http://git-scm.com/about</a>

## Git installeren

Eerst een paar voorbereidende zaken. We gaan er natuurlijk van uit dat je Git hebt geïnstalleerd (hopelijk versie 1.7.0 of hoger).

Als dat niet zo is, kun je Git downloaden via de Git-homepage of [GitHub's Git GUI](https://help.github.com/articles/set-up-git/) installeren.

## Instellen

Het eerste wat je moet doen, is je identiteit instellen. Hiermee kunnen andere mensen die het project downloaden zien wie je bent.

    $ git config --global user.name "Your Name"

    $ git config --global user.email your.email@example.com


## Je reis beginnen

Clone eerst deze repository:

    $ git clone https://github.com/jesse-kroon/git-workshop.git

Je kunt het project eventueel op GitHub forken (je eigen kopie maken) en vervolgens je eigen repository clonen. De knop **Fork** staat rechtsboven in een GitHub-repository. Meer uitleg vind je [hier](https://help.github.com/articles/fork-a-repo/).

Nadat je de repository hebt gecloned, zie je een map met de naam `git-workshop`. Dit is je `working directory`.

    $ cd git-workshop

    $ ls

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

Als je nieuwsgierig bent, kun je ook de submap `.git` bekijken. Hier worden alle gegevens en de volledige geschiedenis van je repository opgeslagen.

    $ ls -a .git

Je ziet:

    branches  config  description  HEAD  hooks  info  objects  refs

## De staging area

Laten we nu enkele bestanden aan het project toevoegen. Maak een paar bestanden.

We maken twee bestanden met de namen `bob.txt` en `alice.txt`.

    $ touch alice.txt bob.txt

We gebruiken een vergelijking met post versturen.

In Git voeg je inhoud eerst toe aan de `staging area` met `git add`. Dit kun je vergelijken met spullen die je wilt versturen in een kartonnen doos stoppen.

Daarna rond je het proces af en leg je het vast in Git met `git commit`. Dit is alsof je de doos dichtplakt: hij is nu klaar om te worden verzonden.

Voeg de bestanden toe aan de staging area:

    $ git add alice.txt bob.txt

## Committen

Je bent nu klaar om een commit te maken. Met de optie `-m` kun je meteen een bericht aan de commit toevoegen.

    $ git commit -m "I am adding two new files"

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Bekijken wat er zojuist is gebeurd

We zouden nu een nieuwe commit moeten hebben. Gebruik `git log` om alle commits tot nu toe te bekijken.

    $ git log

Het logboek toont alle commits, met de nieuwste bovenaan en de oudste onderaan. Je ziet verschillende gegevens, zoals de naam van de auteur, de datum waarop de commit is gemaakt, een commit-SHA en het commitbericht.

Je ziet ook je meest recente commit, waarin je in het vorige onderdeel de twee nieuwe bestanden hebt toegevoegd. `git log` laat echter niet zien welke bestanden bij iedere commit betrokken waren. Gebruik `git show` om meer informatie over een commit te bekijken.

    $ git show

Je ziet iets wat hierop lijkt:

    commit 5a1fad96c8584b2c194c229de7e112e4c84e5089

    Author: kuahyeow

    Date:   Sun Jul 17 19:13:42 2011 +1200

        I am adding two new files

    diff --git a/alice.txt b/alice.txt

    new file mode 100644

    index 0000000..e69de29

    diff --git a/bob.txt b/bob.txt

    new file mode 100644

    index 0000000..e69de29

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Een noodzakelijke uitweiding

In dit onderdeel gaan we meer wijzigingen toevoegen en proberen we fouten te herstellen.

Wees gewaarschuwd: deze volgende stap wordt lastig. We moeten inhoud toevoegen aan `alice.txt`.

Open `alice.txt` en typ je favoriete regel uit een liedje, of bijvoorbeeld:

    Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit
    voluptatem accusantium doloremque laudantium

**Sla** het bestand daarna op.

Wat hebben we gewijzigd? Een erg nuttig commando is `git diff`. Hiermee kun je precies bekijken welke wijzigingen je hebt aangebracht.

    $ git diff

Je ziet iets wat hierop lijkt:

    diff --git a/alice.txt b/alice.txt

    index e69de29..2aedcab 100644

    --- a/alice.txt

    +++ b/alice.txt

    @@ -0,0 +1 @@

    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Opnieuw de staging area

Voeg nu ons gewijzigde bestand `alice.txt` toe aan de staging area. Weet je nog hoe dat moet?

Controleer daarna de `status` van `alice.txt`. Staat het bestand nu in de staging area?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Ongedaan maken

Stel dat we de Lorem ipsum-tekst toch niet in `alice.txt` willen zetten. Een voordeel van de staging area is dat we nog terug kunnen voordat we committen; een commit ongedaan maken is wat lastiger. Denk weer aan de vergelijking met post: het is makkelijker om een brief uit een kartonnen doos te halen voordat je de doos dichtplakt dan erna.

Zo verwijder je een bestand weer uit de staging area:

    $ git reset HEAD alice.txt

    Unstaged changes after reset:

    M   alice.txt

Vergelijk de uitvoer van `git status` nu met die uit het vorige onderdeel. Wat is er anders?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

Je staging area zou nu leeg moeten zijn. Wat is er met de Lorem ipsum-wijzigingen gebeurd? Ze zijn er nog steeds. We zijn terug bij de situatie van vlak voordat we het bestand aan de staging area toevoegden. In de vergelijking met post hebben we onze brief zojuist uit de doos gehaald.

## Ongedaan maken II

Soms zijn we niet tevreden met wat we hebben gedaan en willen we terug naar de laatst *vastgelegde* toestand. In dit geval willen we terug naar de toestand van vlak voordat we de Lorem ipsum-tekst aan `alice.txt` toevoegden.

Hiervoor gebruiken we `git checkout`:

    $ git checkout alice.txt

Je hebt je wijzigingen nu ongedaan gemaakt. Het bestand is weer leeg.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Branches

De meeste grote codebases hebben minstens twee branches: een `live` branch en een `development` branch. De live branch bevat code die zonder problemen op een website kan worden geplaatst of door klanten kan worden gedownload. In de development branch kunnen ontwikkelaars werken aan functionaliteiten die mogelijk nog fouten bevatten. Pas wanneer iedereen tevreden is met de development branch, wordt deze samengevoegd met de live branch.

Een branch maken in Git is eenvoudig. Als je het commando `git branch` zonder verdere opties gebruikt, krijg je een lijst van de branches die je momenteel hebt.

    $ git branch

De `*` geeft aan op welke branch je je momenteel bevindt. Dat is `master`.

Gebruik `git checkout -b (new-branch-name)` als je een nieuwe branch wilt maken:

    $ git checkout -b exp1

Voer `git branch` nogmaals uit om te controleren op welke branch je je momenteel bevindt:

    $ git branch

      exp1

    * master

De nieuwe branch is nu gemaakt. Laten we in die branch gaan werken. Schakel over naar de nieuwe branch:

    $ git checkout exp1

`git checkout (branch-name)` wordt gebruikt om tussen branches te wisselen.

Laten we nu een paar commits maken:

    $ echo 'some content' > test.txt

    $ git add test.txt

    $ git commit -m "Added experimental txt"

Vergelijk de branch nu met de master branch. Gebruik `git diff`:

    $ git diff master

De uitvoer hierboven zegt in feite dat `test.txt` wel aanwezig is in de branch `exp1`, maar niet in de branch `master`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Nu zie je me, nu niet meer

Git kan goed omgaan met je bestanden wanneer je tussen branches wisselt. Schakel terug naar de branch `master`.

Probeer zelf terug te schakelen naar de master branch. Tip: het is hetzelfde commando dat we hierboven gebruikten om naar de branch `exp1` te schakelen.

Waar is ons bestand `test.txt` nu?

    $ ls

    README.textile  alice.txt   bob.txt     gamow.txt

Zoals je ziet, is het nieuwe bestand dat je in de andere branch hebt gemaakt verdwenen. Geen zorgen: het is veilig opgeslagen en verschijnt weer wanneer je terugschakelt naar die branch.

Schakel nu terug naar de branch `exp1` en controleer of `test.txt` weer aanwezig is.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Mergen

We gaan nu mergen uitproberen. Wanneer het werk klaar is, wil je uiteindelijk twee branches samenvoegen. Met `git merge` kun je dat doen.

Bij mergen in Git schakel je eerst over naar de branch *waarin* je de wijzigingen wilt opnemen. Vervolgens voer je het commando uit om de andere branch daarin te mergen.

We willen onze branch `exp1` nu in `master` mergen. Schakel eerst over naar de branch `master`.

    git checkout master

Vervolgens mergen we de branch `exp1` in `master`:

    $ git merge exp1

Zie je de volgende uitvoer?

    Merge made by recursive.

     test.txt |    1 +

     1 files changed, 1 insertions(+), 0 deletions(-)

     create mode 100644 test.txt

Je moet je bevinden in de branch *waarin* je wilt mergen. Daarna geef je altijd de branch op die je wilt samenvoegen.

Je kunt nu ook `gitk` uitproberen om de wijzigingen en het samenvoegen van de twee branches visueel te bekijken.

## Mergeconflicten

Git kan bestanden meestal automatisch samenvoegen, zelfs wanneer hetzelfde bestand is bewerkt. Er zijn echter situaties waarin dezelfde coderegel is aangepast en een computer onmogelijk kan bepalen hoe de wijzigingen moeten worden samengevoegd.

Daardoor ontstaat een conflict dat je zelf moet oplossen.

We gaan nu oefenen met het oplossen van mergeconflicten. Conflicten ontstaan wanneer merges hetzelfde codeblok beïnvloeden.

Hier is een branch die ik eerder heb voorbereid. De branch heet `alpher`. Voer de onderstaande code uit om deze klaar te zetten. Maak je geen zorgen als je de code niet begrijpt.

    $ git checkout alpher

Je zou nu een nieuwe branch met de naam `alpher` moeten hebben. Probeer die branch in `master` te mergen en los het conflict op dat hierdoor ontstaat.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

## Een conflict oplossen

Je ziet als het goed is een `conflict` met het bestand `gamow.txt`. Dit betekent dat dezelfde tekstregel zowel in de master branch als in de alpher branch is bewerkt en gecommit. De onderstaande uitvoer vertelt je wat de huidige situatie is:

    Auto-merging gamow.txt

    CONFLICT (content): Merge conflict in gamow.txt

    Automatic merge failed; fix conflicts and then commit the result.

Als je het bestand `gamow.txt` opent, zie je iets wat hierop lijkt:

    $ cat gamow.txt

    <<<<<<< HEAD

    It was eventually recognized that most of the heavy elements observed in the present universe are the result of stellar nucleosynthesis (http://en.wikipedia.org/wiki/Stellar_nucleosynthesis) in stars, a theory largely developed by Bethe.

    =======

    http://en.wikipedia.org/wiki/Stellar_nucleosynthesis

    Stellar nucleosynthesis is the collective term for the nuclear reactions taking place in stars to build the nuclei of the elements heavier than hydrogen. Some small quantity of these reactions also occur on the stellar surface under various circumstances. For the creation of elements during the explosion of a star, the term supernova nucleosynthesis is used.

    >>>>>>> alpher

Git gebruikt vrij gangbare markeringen voor het oplossen van conflicten. Het bovenste gedeelte van het blok, alles tussen `<<<<<<< HEAD` en `=======`, is afkomstig uit je huidige branch.

De onderste helft is de versie uit de branch `alpher`.

Om het conflict op te lossen, kies je één van beide versies of voeg je ze naar eigen inzicht samen.

Ik zou er bijvoorbeeld voor kunnen kiezen om de versie uit de branch `alpher` te gebruiken.

Probeer nu het **mergeconflict op te lossen**. Kies de tekst die jij beter vindt. Vraag om hulp als je vastloopt.

Wanneer dat is gedaan, kun je het conflict met `git add` en `git commit` als opgelost markeren.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)

Loop je vast? Vraag de workshopbegeleiders om hulp.

    $ git add gamow.txt

    $ git commit -m "Fixed conflict"

Gefeliciteerd. Je hebt het conflict opgelost. Alles is weer in orde.

## Einde

Je hebt het volgende geleerd:

1. Een repository clonen
2. Bestanden committen
3. De status controleren
4. Verschillen controleren
5. Wijzigingen ongedaan maken
6. Branches maken en mergen
7. Conflicten oplossen

Je kunt nu uit twee routes kiezen: deel II hieronder behandelt tijdreizen en het aanpassen van je Git-geschiedenis. Deel III, nog verder naar beneden, behandelt pull requests op GitHub en katten-gifs.

# Deel II

Check de branch `revert` van deze repository uit voor verdere instructies!

Je kunt altijd terugkeren naar deze versie van het README-bestand door de master branch uit te checken.

# Deel III

## GitHub

Maar wacht, er is meer. Hoe zit het met dat gedistribueerd delen met Git?

Om te kunnen delen, hebben we een server nodig waarop we onze Git-repositories kunnen hosten.

GitHub (<a href="https://github.com/">github.com</a>) is waarschijnlijk de eenvoudigste plek om te beginnen.

## Inloggen bij of aanmelden voor GitHub

Als je al een account hebt, kun je doorgaan met het maken van een repository op GitHub of deze repository forken en naar je lokale computer clonen.

Zo niet...

Ga naar GitHub en <a href="https://github.com/signup">maak een account aan</a>. Log in als je al eerder een account hebt aangemaakt.

Tip: mogelijk moet je Git instellen om je GitHub-wachtwoord te onthouden. Bekijk hiervoor <a href="https://help.github.com/articles/set-up-git">https://help.github.com/articles/set-up-git</a>.

Kom daarna hier terug; we wachten op je.

## Je eerste GitHub-repository maken

Een repository, kortweg repo, is een plek waar je code opslaat. In deel I heb je zojuist al in je eigen repo geoefend!

De volgende <a href="https://help.github.com/articles/create-a-repo">tutorial</a> laat zien hoe je een GitHub-repository maakt die je daarna met anderen kunt delen.

Kom daarna hier terug; we wachten op je.

## Een repository forken

Ga naar [deze tutorial](https://help.github.com/articles/fork-a-repo).

Kom daarna hier terug; we wachten op je.

## Laten we samenwerken!

Check de branch `pull_request` van deze repository uit voor verdere instructies!

Je kunt altijd terugkeren naar deze versie van het README-bestand door de master branch uit te checken.

## Einde

Je hebt het volgende geleerd:

1. Een repository op GitHub forken
2. Git push
3. Git pull

### Bronnen en meer informatie

Ik raad deze bronnen ten zeerste aan om verder met Git te oefenen:

- <a href="http://try.github.com">http://try.github.com</a> — Nog een tutorial voor beginners over Git
- <a href="http://git-scm.com">http://git-scm.com</a> — De officiële website, met zeer nuttige hulp, een boek en video's
- <a href="http://gitref.org">http://gitref.org</a>
- <a href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html">http://www.kernel.org/pub/software/scm/git/docs/everyday.html</a>

## Auteur

Dit werk valt onder de Creative Commons Attribution-NonCommercial-ShareAlike 3.0-licentie.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">http://creativecommons.org/licenses/by-nc-sa/3.0/</a>

Auteur: Thong Kuah  
Bijdragen van: Andy Newport, Nick Malcolm
