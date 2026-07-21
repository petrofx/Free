Clickjacking

Podatna strona:  https://example_victim.com/


Czym jest Clickjacking?

Clickjacking (atak typu User Interface Redress, atak typu UI Redress, UI Redressing) to złośliwa technika polegająca na nakłonieniu użytkownika sieci do kliknięcia w coś innego niż to, co użytkownik postrzega jako klikalne, co potencjalnie może doprowadzić do ujawnienia poufnych informacji lub przejęcia kontroli nad komputerem podczas klikania pozornie nieszkodliwych stron internetowych.

Powodem jest brak nagłówka „X-Frame-Options”, który powinien być ustawiony na: SAMEORIGIN, DENY lub inną bezpieczną opcję w zależności od sytuacji.Równiez niwwłaściwa CSP - Content Security Policy , czyli Polityka Bezpieczeństwa Treści odgrywa tutaj rolę.



Odtworzenie:

Zapisz na swoim złośliwym serwerze plik HTML o następującej treści (nazwijmy go np. ClickjackingPoC.html):


<pre lang="JavaScript" line="1">
<html>
<head>
<title>Clickjacking PoC</title>
</head>

Clickjacking PoC

<h2>Your Web Application Can be mounted within an iframe wich makes it vulnerable to CLICKJACKING!</h2>
<iframe src="https://example_victim/" height="1000" width="2000"></iframe>
</html>
</pre>

Po dwukrotnym kliknięciu tego konkretnego pliku HTML, strona https://example.com/ ładuje się wewnątrz elementu IFRAME.
Oczywiście, aby uczynić ten atak groźniejszym, ramka iframe wymagałaby odpowiedniego ostylowania itp., a ofiara musiałaby kliknąć złośliwy link prowadzący do tego pliku HTML*, jednak jest to prosty dowód koncepcji (PoC) pokazujący, że taki atak jest możliwy – choć oczywiście w idealnym świecie nie powinien być możliwy ;)


*Plik musiałby oczywiście być udostępniony pod publicznym adresem aby mógł byc przesłany rzeczywistej ofierze, jednak ten test wystarczy aby udowodnic istnienie podatności.

Brak stosownych nagłówków powoduje, że atak jest możliwy w ramach innej domeny i/lub adresu niż domena/adres ofiary. W przeciwnym razie nasz ładunek musiałby znajdować się w lokalizacji w ramach atakowane domeny.

Stopień zagrożenia określa się zwykle  jako „niski”, ponieważ wymagane są dalsze testy – na przykład z użyciem rzeczywistego konta w serwisie https://example_victim.com/ – w celu zweryfikowania rzeczywistego wpływu ataku.

Naprawa:

X-Frame-Options header powinien być ustawiony na: SAMEORIGIN albo inne bezpieczne opcje typu: DENY.
                   
                   Albo:

Polityka CSP   -->  Content-Security-Policy: frame-ancestors 'none'
                    
                    or 

Polityka CSP   -->   Content-Security-Policy: frame-ancestors 'self'


Więcej odniesień:  https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/Clickjacking

https://portswigger.net/web-security/clickjacking#how-to-prevent-clickjacking-attacks

    Ww strony są w języku angielskim, ale wystarczy w przeglądarce google chrome uruchomic opcje `translate` i strona zostaje przetłumaczona na wybrany przez nas język.
