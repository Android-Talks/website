---
title:  'AT 05 - [OWASP Mobile Top 10] M1: Improper Platform Usage - Nieprawidłowe używanie platformy'
date:   2023-03-20 06:00:00 +0300
image:  '/images/podcast-cover.jpg'
tags:   [Security]
---
Pierwszy odcinek z serii poświęconej OWASP Mobile Top 10, czyli listy dziesięciu najczęściej występujących słabości w aplikacjach mobilnych. Celem tej serii jest opisanie wszystkich słabości i pokazanie przykładów, które ilustrują jak duże zagrożenie stanowią dla bezpieczeństwa aplikacji.

Odcinek możesz przesłuchać poniżej lub na wszystkich większych platformach, m.in. [Spotify](/spotify), [Apple Podcasts](/apple) czy [Google Podcasts](/google).

<div class="buzzsprout-player-wrapper">
	<iframe src="https://www.buzzsprout.com/1820265/12474373-at-05-owasp-mobile-top-10-m1-improper-platform-usage-nieprawidlowe-uzywanie-platformy?client_source=admin&amp;iframe=true" width="100%" height="200" frameborder="0" scrolling="no"></iframe>
</div>

# Wstęp
Bezpieczeństwo to jeden z najważniejszych aspektów aplikacji. Niestety, w wielu firmach i projektach bywa pomijany. Widać to szczególnie dobrze w start-upach i mniejszych firmach, gdzie często brakuje wiedzy i zaniedbuje się kwestie związane z bezpieczeństwem, dopóki klienci nie doświadczą pierwszych ataków.

W jaki sposób zadbać o bezpieczeństwo? Skąd w ogóle wiedzieć, przed czym się zabezpieczyć i jak to zrobić? W jaki sposób testować aplikacje pod kątem bezpieczeństwa?

Jeśli nie znasz odpowiedzi na te pytania, lub po prostu ciekawi Cię ten temat, to bardzo dobrze trafiłeś. Dzisiejszy odcinek rozpoczyna cykl poświęcony bezpieczeństwu aplikacji mobilnych. W ramach tego cyklu szczegółowo omówię największe słabości i podatności aplikacji mobilnych. Przedstawię sposoby ich testowania oraz wymagania, jakie musi spełnić aplikacja, aby można było uznać ją za bezpieczną.

Ten odcinek jest również pierwszym odcinkiem z serii poświęconej OWASP Mobile Top 10, czyli listy dziesięciu najczęściej występujących słabości w aplikacjach mobilnych. Celem tej serii jest opisanie wszystkich słabości i pokazanie przykładów, które ilustrują, jak duże zagrożenie stanowią dla bezpieczeństwa aplikacji.

# Czym jest OWASP?
Najpierw zacznijmy od tego, czym w ogóle jest OWASP?

OWASP, czyli Open Web Application Security Project, jest to organizacja non profit zajmująca się różnymi aspektami bezpieczeństwa aplikacji. Jej celem jest poprawa bezpieczeństwa oprogramowania, między innymi dzięki prowadzonym przez społeczność projektom open source.

Jednym z tych projektów jest właśnie Mobile Top 10.

# Czym jest Top 10?

A czym jest Top 10? Top 10 to prawdopodobnie najbardziej znane projekty OWASP’a. Są to listy dziesięciu najczęściej występujących słabości w aplikacjach. Lista ta jest posortowana względem ryzyka, a więc chcąc uwzględnić ją w swojej organizacji słabość pierwsza powinna mieć dla nas dużo większy priorytet niż np. słabość dziesiąta.

I takich list Top 10 w OWASP’ie możemy znaleźć kilka, między innymi:

- OWASP Top 10, czyli ich najbardziej znana lista, dotycząca aplikacji webowych
- Top 10 Serverless
- Top 10 API
- czy Mobile Top 10.

Nas oczywiście najbardziej interesuje ta ostatnia.

Pierwsza wersja Mobile Top 10 została wydana w 2014 roku, natomiast druga, a zarazem najnowsza, dwa lata później. Na stronie możemy też znaleźć prezentację oraz film o liście z 2011 roku. Ta lista została oznaczona jako release candidate 1.0 i aktualnie jest zarchiwizowana, niemniej jednak warto ją zobaczyć i porównać, jakie zmiany zostały wprowadzane na przestrzeni lat.

Co ciekawe, od niedawna na stronie Mobile Top 10 widnieje informacja o rozpoczęciu prac nad aktualizacją listy w 2023 roku. Jest też link do Slacka, więc każdy może dołożyć od siebie cegiełkę, przyczyniając się do researchu, który jest aktualnie prowadzony.

W tej serii będę omawiał najnowszą dostępną listę, czyli tą z 2016 roku, natomiast jeśli dojdzie do wydania nowej wersji to znajdzie się też tu odcinek, w którym opowiem co się zmieniło.

Możliwe, że niektórzy zadają sobie teraz pytanie “Ale jak to, ta lista się zmienia?” Ano tak! Lista zmienia się, bo pewne problemy znikają, a inne się pojawiają.

To zjawisko widać szczególnie dobrze w webowej liście Top 10, która pierwsze swoje wydanie miała w 2003 roku, a najnowsze - siódme w 2021 roku. Na pierwszy rzut oka można by pomyśleć, że lista Mobile Top 10 jest trochę zaniedbywana, bo przecież webowa ma aż 7 wersji, a mobilna tylko dwie. Spokojnie, wynika to przede wszystkim z różnic pomiędzy aplikacjami webowymi i mobilnymi. Pamiętajmy, ze jedne uruchamiane są w przeglądarce, która w łatwy sposób może na przykład dokonać weryfikacji hosta czy certyfikatu, a drugie bezpośrednio na urządzeniach, które zrobią to i wiele innych rzeczy tylko wtedy gdy programista o to zadba. Stos technologiczny wykorzystywany do tworzenia jednych i drugich też się różni, zmienia się w czasie i ma swoje ograniczenia. A zatem, powinno być to dla nas zrozumiałe, że listy będą inaczej się zmieniać i opisywać inne słabości.

A jak wygląda aktualna lista Mobile Top 10 z 2016 roku? Prezentuje się następująco:

- M1: Improper Platform Usage (Nieprawidłowe używanie platformy)
- M2: Insecure Data Storage (Niezabezpieczone przechowywanie danych)
- M3: Insecure Communication (Niezabezpieczona komunikacja)
- M4: Insecure Authentication (Niezabezpieczone uwierzytelnianie)
- M5: Insufficient Cryptography (Niedostateczne użycie kryptografii)
- M6: Insecure Authorization (Niezabezpieczona autoryzacja)
- M7: Poor Code Quality (Słaba jakość kodu)
- M8: Code Tampering (Modyfikacja kodu)
- M9: Reverse Engineering (Inżynieria odwrotna)
- M10: Extraneous Functionality (Ukryte, niezabezpieczone funkcje w systemach)

W tym odcinku skupimy się na słabości pierwszej - nieprawidłowym używaniu platformy.

# Jak wygląda bezpieczeństwo dzisiejszych aplikacji?

Jeszcze przed przejściem do części głównej dzisiejszego odcinka, myślę, że warto byłoby sprawdzić jak bardzo bezpieczne lub niebezpieczne są aplikacje, które aktualnie znajdują się w sklepach. Oczywiście nie ma takiej strony, na której podamy nazwę aplikacji i dowiemy się czy jest bezpieczna bądź nie, najlepiej wypisując wszystkie jej podatności, ale z pewnością dostępne są jakieś statystyki na podstawie chociażby testów automatycznych, które coś już nam powiedzą.

Jedną z firm, która może nam w tym pomóc jest NowSecure. Firma NowSecure w dużym skrócie zajmuje się monitorowaniem zagrożeń związanych z bezpieczeństwem, prywatnością oraz słabościami aplikacji mobilnych. Z informacji na stronie wynika, że do tej pory przeprowadzili ponad 11 tysięcy pentestów, a aktualnie każdy taki pentest to ponad 600 testów wykonanych używając praktyk SAST, DAST, IAST i innych.

Oczywiście, wszystkie te testy są automatyczne, a niestety narzędzia automatyczne nie czynią oprogramowania bezpiecznym i nigdy nie będą efektywne w 100%. Ponadto, tego typu narzędzia są generyczne, a więc nie są dostosowane do konkretnej aplikacji. Największe i najważniejsze problemy bezpieczeństwa rzadko kiedy są generyczne i najczęściej wynikają z logiki biznesowej czy projektu architektury, a to oznacza, że narzędzia zautomatyzowane będą w stanie wykryć jedynie część podatności, które można uogólnić dla wszystkich aplikacji.

Niemniej jednak, warto do takich statystyk zajrzeć. Adres strony znajduje się w opisie odcinka. Na stronie znajdziesz wyniki wspomnianych testów, przedstawiające zagrożenia bezpieczeństwa i prywatności z podziałem na kategorie aplikacji, takie jak: social media, bankowość, podróże i inne.

Dodatkowo w 2018 roku NowSecure zgłosiło, że 85% najpopularniejszych aplikacji w sklepach naruszyło co najmniej jedną z OWASP Mobile Top 10, a większość z nich korzystała na przykład z niezabezpieczonego przechowywania danych czy niezabezpieczonej komunikacji. Oczywiście przez ostatnie 5 lat coś się zmieniło, ale myślę, że jeśli jesteś programistą aplikacji mobilnych i pracowałeś w różnych projektach to sam przyznasz, że były w tym czasie podatne, a może nawet nadal są na różnego rodzaju ataki.

# Omówienie słabości M1

Improper Platform Usage to słabość, która obejmuje niewłaściwe korzystanie z funkcji dostarczonych przez platformę lub niestosowanie mechanizmów jej bezpieczeństwa. Brzmi dość ogólnie i trochę niejasno, dlatego już tłumaczę o co chodzi.

Przede wszystkim wyjaśnijmy czym jest platforma. Gdy chcemy napisać aplikację mobilną to tworzymy ją w oparciu o funkcje dostarczone przez platformę. W przypadku aplikacji natywnych naszą platformą jest system, czyli Android lub iOS. Natomiast możemy też tworzyć aplikacje przy użyciu innych rozwiązań, np. Flutter’a czy React Native. Te frameworki posłużą jako pośrednik między programistą a platformą natywną, dostarczając również własne funkcje.

Platforma dostarcza programiście narzędzia, biblioteki i API, dzięki którym może w łatwy sposób korzystać z jej funkcji i finalnie przy ich pomocy zbudować działającą i bezpieczną aplikację. Problem pojawia się gdy programiście brakuje wiedzy o danej funkcji, nie zna jej aktualnych standardów, nie potrafi posługiwać się dokumentacją lub najzwyczajniej popełni błąd.

To wszystko obejmuje słabość pierwsza, a teraz czas na kilka przykładów 👇

## 1) KeyStore

Jedną z funkcji platformy Androida, która dość często używana jest w niepoprawny sposób to zarządzanie kluczami kryptograficznymi i sekretami, co wiąże się z użyciem KeyStore’a i często powiązanej z nim biometrii. Chcąc zapewnić ochronę wrażliwych danych użytkowników oraz zapobiegać nieautoryzowanemu dostępowi do aplikacji programista powinen użyć KeyStore’a w swoim kodzie. Umożliwia on przechowywanie kluczy kryptograficznych w bezpiecznym kontenerze i znacznie utrudnia wydobycie ich z urządzenia.

Najgorsze co można zrobić to oczywiście przechowywać klucze, sekrety, tokeny i inne wrażliwe dane w sposób jawny, na przykład zapisując je do pliku czy do zwykłych preferencji. Wydobycie takich danych z urządzenia jest banalne i może prowadzić do sporych konsekwencji.

Złym pomysłem jest też tworzenie kryptografii na nowo, czyli niestosowanie metod kryptograficznych dostarczonych przez platformę, a pisanie ich samemu lub wykorzystywanie niesprawdzonych bibliotek znalezionych w Internecie. Takie działania prowadzą do powstawania dziur bezpieczeństwa w aplikacji.

A zatem absolutne minimum, jakie programista powinien zastosować w swojej aplikacji gdy ma do czynienia z wrażliwymi danymi to użyć właśnie KeyStore’a do kluczy kryptograficznych, a wszelkie sekrety, które mają być przechowane w sposób bezpieczny umieścić co najmniej w **EncryptedSharedPreferences** czyli szyfrowanych preferencjach aplikacji, do których klucz znajduje się w KeyStore.

Wspomniałem też wcześniej o biometrii, i to nie bez powodu, bo z nią problem jest równie poważny. A jaki to problem, spytacie? Ano taki, że bardzo dużo aplikacji prosi o odcisk palca, na przykład podczas logowania się albo autoryzacji, a tak naprawdę w ogóle nie wykorzystuje jego potencjału. Wtedy można śmiało powiedzieć, że tej biometrii tak naprawdę tam nie ma.

Niestety bardzo dużo aplikacji po przyłożeniu palca sprawdza jedynie czy palec jest poprawny. Często wygląda to tak: jeśli palec jest poprawny to wyciągnij wcześniej zapisany **refreshToken** z **SharedPreferences**, zaloguj użytkownika i przejdź do ekranu głównego aplikacji.

W takim podejściu problemy są co najmniej dwa:

1. **RefreshToken** znajduje się na urządzeniu, więc atakujący z dostępem do tego telefonu ma ułatwione zadanie by się do niego dostać i korzystać z niego dopóki nie wygaśnie
2. Sprawdzana jest tylko poprawność palca, bez wykonywania jakichkolwiek operacji kryptograficznych z użyciem KeyStore i bez weryfikacji po stronie Backendu

Musisz wiedzieć, że takie trywialne sprawdzenie palca można bardzo łatwo obejść rootując urządzenie i instalując pojedynczy moduł z Xposed. Aplikacja nagle zacznie akceptować wszystkie palce, nawet te niezarejestrowane w systemie.

Jak sobie z tym poradzić?

Gdy generowany jest nowy klucz w KeyStore, programista ma możliwość powiązać go z biometrią, ustawiając flagę **userAuthenticationRequired** na true. Wówczas taki klucz może być użyty tylko wtedy, gdy użytkownik zostanie uwierzytelniony. To daje nam gwarancję, że klucz powiązany z odciskiem pa lca zadziała poprawnie tylko wtedy, gdy zostanie przyłożony odpowiedni palec. Klucz może być wtedy użyty na przykład do odszyfrowania albo podpisania jakichś danych, aby następnie Backend zweryfikował ich poprawność i zautoryzował akcję użytkownika.

## 2) Intenty

Drugą funkcją platformy Androida, o której warto powiedzieć w przypadku tej słabości są Intenty. Intenty to obiekty, dzięki którym aplikacja może komunikować się i przesyłać dane pomiędzy innymi komponentami samej siebie albo pozostałymi aplikacjami na urządzeniu. Korzystając z nich aplikacja może na przykład wybrać plik z galerii, zrobić zdjęcie kamerą czy otworzyć przeglądarkę internetową. Najczęściej używane są po prostu do otwierania różnych aktywności w aplikacji. Oprócz tego, wykorzystywane są do obsługi deep linków, czyli funkcji, dzięki której po kliknięciu w link na telefonie, aplikacja może automatycznie otworzyć się na konkretnym ekranie.

Wiedząc już jak działają Intenty, pomyślmy nad przykładem aplikacji, która z nich korzysta i mogłaby być zaatakowana. Wyobraźmy sobie taką aplikację, która pewne swoje funkcjonalności otwiera w **WebView**, czyli wbudowanym oknie przeglądarki. Jest to powszechna praktyka, szczególnie gdy część funkcji całego systemu opiera się na internetowym interfejsie użytkownika. Ponadto jest to tańsze i bardziej elastyczne rozwiązanie, bo w przypadku zmian na stronie nie ma potrzeby wypuszczania nowej wersji aplikacji. W naszej aplikacji znajduje się aktywność z **WebView**, którą można uruchomić przy użyciu Intentu. Do Intentu należy podać parametr “url”, który zostanie odczytany przez aktywność na starcie i otworzy ten adres w **WebView**. Programista skonfigurował **WebView** w taki sposób, że może uruchomić kod w JavaScript’cie i oznaczył w Manifeście aplikacji, że ta aktywność jest wyeksportowana, co oznacza, że może być uruchamiana przez inne aplikacje.

I tak oto powstała aplikacja podatna na wstrzyknięcie adresu url, umożliwiając osobie atakującej uruchomienie dowolnego kodu w JavaScript’cie. Tego typu atak może doprowadzić do wycieku session cookie, tokenów, danych sesji czy innych poufnych informacji.

I wiesz co? Aplikacja, którą przed chwilą opisałem nie jest przykładem wymyślonym przeze mnie, a sytuacją, która naprawdę miała miejsce w aplikacji **“rif is fun for Reddit”**. Dokładnie w taki sam sposób można było wstrzyknąć dowolny kod w JavaScript’cie i wykradać dane logowanie użytkownika. Co więcej, przedstawiony przykład to zaledwie jeden z najprostszych scenariuszy ataków, które można zastosować gdy programista nie do końca przemyśli użycie Intentów w swojej aplikacji.

Jeśli jesteś ciekawy innych aplikacji, które można było zhackować Intentami i jak te ataki wyglądały to koniecznie zajrzyj do opisu odcinka. Znajdziesz tam kilka ciekawych artykułów, w których dokładnie to przedstawiono.

To tyle o intentach, a teraz przejdźmy do ostatniego punktu na dzisiaj, czyli nieprawidłowego zarządzania uprawnieniami.

## 3) Uprawnienia

Jak często zdarza Ci się zainstalować nową aplikację na telefonie, która na dzień dobry prosi Cię o mnóstwo różnych uprawnień? Zezwól na dostęp do lokalizacji, zezwól na dostęp plików, zezwól na dostęp do odczytywania smsów, kontaktów, stanu telefonu, i tak dalej, i tak dalej. Osobiście używam całkiem prostej zasady. Jeśli nie jestem w stanie odpowiedzieć sobie na pytanie “Dlaczego ta aplikacja wymaga ode mnie tych uprawnień?” to po prostu z niej nie korzystam. Dbam o swoje bezpieczeństwo i nie chcę używać podejrzanego software’u na swoich urządzeniach. Niestety, nie każdy jest programistą i wie co nieco jak to działa, tak samo nie każdy czyta prośby o przyznanie uprawnień aplikacji i akceptuje je bez zastanowienia.

Mówiąc wcześniej o intentach, przedstawiłem w jak prosty sposób można manipulować działaniem aplikacji. Idąc o krok dalej, moglibyśmy pomyśleć nad przykładem aplikacji, którą można nie tylko zmanipulować, ale także wykorzystać ją do wykonania operacji, do których sami nie mamy uprawnień, ale ta aplikacja akurat ma. I znowu, nie posłużę się tutaj przykładem wymyślonym przeze mnie, a sytuacją z 2019 roku kiedy to w aplikacjach Google i Samsung Camera znaleziono dziurę. Aplikacje te umożliwiały innym aplikacjom na robienie zdjęć lub nagrywanie filmów za pośrednictwem aparatu. Zdjęcia były zapisywane na karcie SD, a złośliwa aplikacja była w stanie poprosić o dostęp do pamięci telefonu, co samo w sobie nie jest bardzo podejrzane, a następnie wysłać Intent do podatnej aplikacji aparatu i wyodrębnić pliki. Ponadto, jeśli podczas robienia zdjęć włączona była geolokalizacja, to w zasadzie złośliwa aplikacja była w stanie śledzić użytkownika, wyciągając te informacje z metadanych.

A zatem, praktycznie każda prośba aplikacji o przyznanie uprawnienia powinna być traktowana, zarówno przez programistę jak i użytkownika jako ryzyko dostępu do danych przez inne aplikacje czy osoby niepożądane. Oczywiście jako programista czasami nie masz wyjścia. Jeżeli feature, nad którym aktualnie pracujesz wymaga pewnych uprawnień to musisz o nie poprosić. Pamiętaj tylko aby zawsze korzystać z nich w sposób minimalny, bezpieczny i zgodny z aktualnymi praktykami w dokumentacji. Przykładem braku znajomości dokumentacji jest wymaganie uprawnień do pamięci i kamery, gdy aplikacja chce tylko zrobić zdjęcie lub wybrać je z galerii i zapisać je do pamięci wewnętrznej w katalogu aplikacji. Zgodnie z najnowszą dokumentacją wystarczy skorzystać ze Storage Access Framework’u lub MediaStore. Niestety, spotkałem się już z wieloma programistami, którzy o tym nie wiedzieli i ich aplikacje niepotrzebnie prosiły o te uprawnienia.

# I to by było na tyle
Pierwszy odcinek serii OWASP Mobile Top 10 powoli dobiega końca. Przypominam, że w tym odcinku omówiłem jedynie kilka przykładów związanych z pierwszą słabością, natomiast w praktyce, tak jak mówiłem wcześniej, dotyczy ona całej platformy. Oznacza to, że jako programista musisz być na bieżąco z dokumentacją, zalecanymi praktykami bezpieczeństwa, a także śledzić zmiany wprowadzane w kolejnych wersjach systemu.

Jeżeli spodobał Cię się ten odcinek to w zależności od platformy, na której mnie słuchasz zachęcam Cię do subskrybowania, zostawienia swojej opinii, a także udostępniania dalej.

Przypominam również o moim newsletterze, na który możesz się zapisać na stronie [androiddevnews.com](http://androiddevnews.com) i zapraszam na moją stronę [patrykkosieradzki.com](http://patrykkosieradzki.com) gdzie znajdziesz wszystkie moje artykuły.

Nowe odcinki serii OWASP Mobile TOP 10 pojawią się tu już niedługo.

Dzięki za uwagę i do usłyszenia w kolejnym odcinku, Cześć!

## Przydatne linki:

- [Blog](https://patrykkosieradzki.com/)
- [Kanał YouTube](https://www.youtube.com/channel/UCJ71FwtAaIfNp0N9VnzJyJg)
- [Android Dev Newsletter - cotygodniowa dawka wiedzy o tworzeniu aplikacji mobilnych](https://androiddevnews.com/)

## Linki z odcinka:

- [OWASP Mobile Top 10](https://owasp.org/www-project-mobile-top-10/)
- [M1: Improper Platform Usage](https://owasp.org/www-project-mobile-top-10/2016-risks/m1-improper-platform-usage)
- [Mobile App Security and Privacy Tracker (NowSecure)](https://mobilerisktracker.nowsecure.com/)
- [Mobile AppSec 101 (NowSecure)](https://mobilerisktracker.nowsecure.com/)
- [Exploring intent-based Android security vulnerabilities on Google Play](https://snyk.io/blog/exploring-android-intent-based-security-vulnerabilities-google-play/)
- [Hunting intent-based Android security vulnerabilities with Snyk Code](https://snyk.io/blog/hunting-intent-based-android-security-vulnerabilities-with-snyk-code/)
- [How malicious applications abuse Android permissions](https://blog.nviso.eu/2021/09/01/how-malicious-applications-abuse-android-permissions/)