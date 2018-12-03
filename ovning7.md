# git-conflict

> Kom ihåg att alltid kolla `git log` samt `git status`

1. Skapa en ny mapp (valfritt namn utan mellanslag) och ställ dig i den i terminalen (`cd`) och initiera ett nytt git repository med: `git init`.
2. Skapa filen `script.php` och lägg till följande kod:
```php
function addNumbers($a, $b) {
  $sum = $a + $b;
  return $sum;
}
```
3. Lägg till filen till _Stageing area_ (`git add`)
4. Gör en commit `git commit -m "your message"`.
5. Kolla status och kolla `git log` för att se vad som har hänt
5. Skapa en ny branch som heter `multiple-arguments` (`git branch multiple-arguments`)
6. Byt till den nya branchen: `git checkout multiple-arguments`
7. Utöka den redan existerande koden i  `script.php` på följande sätt:
```php
function addNumbers($numbers) {
  $sum = $a + $b;
  foreach($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
```
8. Lägg till ändringarna till Staging area (`git add script.php`)
9. Commita ändringarna (`git commit -m ""`)
10. Kör `git log --oneline --decorate --graph` för att se vilka commits som finns.
11. Växla till master igen: `git checkout master`
12. Kör `git log` här med och se vilka commits som finns.
13. Merga ändringarna från `multiple arguments` in i `master` genom att köra: `git merge multiple-arguments` när du står på branchen `master`.
14. Kör `git log` igen och se ändringarna. Kolla även på koden i editorn för att se vad som har ändrats.
15. Medan du står på `master`: byt namn på funktionen `addNumbers` så att den heter enbart `add`.
16. Stagea ändringarna (`git add script.php`) och gör en ny commit (`git commit -m ""`) på `master`.
17. Växla tillbaka till `multiple-arguments`-branchen (`git checkout multiple-arguments`)
18. ta bort rad 2 då du upptäcker att den är helt överflödig
19. Stagea dina ändringar och gör en ny commit på branchen `multiple-arguments`.
20. Växla tillbaka till `master`
21. Merga in ändringarna från den andra branchen in i `master` genom att skriva: `git merge multiple-arguments`. Du borde få följande meddelande som betyder att du har stött på en konflikt i din fil. Meddelandet säger att det finns flera rader som har ändringar i båda branches och du måste lösa detta manuellt.
```bash
Auto-merging script.php
CONFLICT (content): Merge conflict in script.php
Automatic merge failed; fix conflicts and then commit the result.
```
22. Öppna filen `script.php` i din editor, koden borde nu se ut som nedan. Mellan `<<<<<<< HEAD` och `=======` är den ändring som är på `master` och mellan `=======` och `>>>>>>> multiple-arguments` är de ändringar som finns på `multiple-arguments`. Du måste manuellt redigera denna fil så den stämmer överens med hur du vill ha koden (du gör det i nästa steg).
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
23. Ändra (ta bort/omstrukturera) så att koden ser ut som nedan när du är klar
```php
function add($numbers) {
  foreach ($numbers as $number) {
    $sum += $number;
  }
  return $sum;
}
```
24. Du har gjort en ändring i dina filer, detta betyder att du måste stagea dina ändringar och göra en ny commit. När du har gjort denna commit har du löst konflikten. Konflikten löses alltid av att du manuellt går in i filerna, väljer vad som ska vara kvar och sparar dessa ändringar i en ny commit.
25. Kör `git log --oneline --decorate --graph` för att se vad som har hänt i repot på branchen `master`
26. Växla till branchen `multiple-arguments` och kör `git log --oneline --decorate --graph` för att se vad som har hänt.
27. Du har i denna övning löst en mergekonflikt, detta är något som händer ganska ofta och man måste alltid hålla koll i Bash om det står att det har blivit en konflikt och manuellt gå in i filerna och lösa dessa konflikter. Gör man inte det så kommer koden att sluta fungera och man kommer ha ännu mer problem.