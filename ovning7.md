# git-conflict

> Kom ih�g att alltid kolla `git log` samt `git status`

1. Skapa en ny mapp (valfritt namn utan mellanslag) och st�ll dig i den i terminalen (`cd`) och initiera ett nytt git repository med: `git init`.
2. Skapa filen `script.php` och l�gg till f�ljande kod:
```php
function addNumbers($a, $b) {
  $sum = $a + $b;
  return $sum;
}
```
3. L�gg till filen till _Stageing area_ (`git add`)
4. G�r en commit `git commit -m "your message"`.
5. Kolla status och kolla `git log` f�r att se vad som har h�nt
5. Skapa en ny branch som heter `multiple-arguments` (`git branch multiple-arguments`)
6. Byt till den nya branchen: `git checkout multiple-arguments`
7. Ut�ka den redan existerande koden i  `script.php` p� f�ljande s�tt:
```php
function addNumbers($numbers) {
  $sum = $a + $b;
  foreach($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
```
8. L�gg till �ndringarna till Staging area (`git add script.php`)
9. Commita �ndringarna (`git commit -m ""`)
10. K�r `git log --oneline --decorate --graph` f�r att se vilka commits som finns.
11. V�xla till master igen: `git checkout master`
12. K�r `git log` h�r med och se vilka commits som finns.
13. Merga �ndringarna fr�n `multiple arguments` in i `master` genom att k�ra: `git merge multiple-arguments` n�r du st�r p� branchen `master`.
14. K�r `git log` igen och se �ndringarna. Kolla �ven p� koden i editorn f�r att se vad som har �ndrats.
15. Medan du st�r p� `master`: byt namn p� funktionen `addNumbers` s� att den heter enbart `add`.
16. Stagea �ndringarna (`git add script.php`) och g�r en ny commit (`git commit -m ""`) p� `master`.
17. V�xla tillbaka till `multiple-arguments`-branchen (`git checkout multiple-arguments`)
18. ta bort rad 2 d� du uppt�cker att den �r helt �verfl�dig
19. Stagea dina �ndringar och g�r en ny commit p� branchen `multiple-arguments`.
20. V�xla tillbaka till `master`
21. Merga in �ndringarna fr�n den andra branchen in i `master` genom att skriva: `git merge multiple-arguments`. Du borde f� f�ljande meddelande som betyder att du har st�tt p� en konflikt i din fil. Meddelandet s�ger att det finns flera rader som har �ndringar i b�da branches och du m�ste l�sa detta manuellt.
```bash
Auto-merging script.php
CONFLICT (content): Merge conflict in script.php
Automatic merge failed; fix conflicts and then commit the result.
```
22. �ppna filen `script.php` i din editor, koden borde nu se ut som nedan. Mellan `<<<<<<< HEAD` och `=======` �r den �ndring som �r p� `master` och mellan `=======` och `>>>>>>> multiple-arguments` �r de �ndringar som finns p� `multiple-arguments`. Du m�ste manuellt redigera denna fil s� den st�mmer �verens med hur du vill ha koden (du g�r det i n�sta steg).
```php
<<<<<<< HEAD
function add($numbers) {
  $sum = $a + $b;
=======
function addNumbers($numbers) {
>>>>>>> multiple-arguments
  foreach($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
```
23. �ndra (ta bort/omstrukturera) s� att koden ser ut som nedan n�r du �r klar
```php
function add($numbers) {
  foreach ($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
```
24. Du har gjort en �ndring i dina filer, detta betyder att du m�ste stagea dina �ndringar och g�ra en ny commit. N�r du har gjort denna commit har du l�st konflikten. Konflikten l�ses alltid av att du manuellt g�r in i filerna, v�ljer vad som ska vara kvar och sparar dessa �ndringar i en ny commit.
25. K�r `git log --oneline --decorate --graph` f�r att se vad som har h�nt i repot p� branchen `master`
26. V�xla till branchen `multiple-arguments` och k�r `git log --oneline --decorate --graph` f�r att se vad som har h�nt.
27. Du har i denna �vning l�st en mergekonflikt, detta �r n�got som h�nder ganska ofta och man m�ste alltid h�lla koll i Bash om det st�r att det har blivit en konflikt och manuellt g� in i filerna och l�sa dessa konflikter. G�r man inte det s� kommer koden att sluta fungera och man kommer ha �nnu mer problem.