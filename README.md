# Dog Adoption Helper
Projekt realizowany w ramach przedmiotu *Wprowadzenie do aplikacji i rozwiązań opartych o Sztuczną Inteligencję i Microsoft Azure* prowadzonym na Politechnice Warszawskiej.

## Opis i cel projektu
Każdego roku ogromna ilość psów trafia do schronisk. Często schroniska nie mają już miejsca na kolejne psy albo brak im funduszy. Przy poszukiwaniu psa, każdy chce mieć pewność, że znaleźliśmy tego odpowiedniego, który stanie się naszym nowym członkiem rodziny. Jest bardzo wiele ważnych czynników, które należy wziąć pod uwagę: styl życia, lokalizacja, harmonogram pracy. Sam problem adopcji może być dla nowicjuszy skomplikowany, przytłaczający. 
Celem naszego projektu jest stworzenie bota, który ułatwi ludziom znalezienie ich wymarzonego psa w schronisku i odpowie na pytania związane z procesem adopcji czy późniejszą opieką nad swoim nowym pupilem.

## Skład zespołu
* Luiza Krzepkowska - <a href ="https://github.com/luizalouise" targer="_blank">Link do konta</a>
* Katsiaryna Kutsepina - <a href ="https://github.com/kutsepka" targer="_blank">Link do konta</a>
* Agata Lachowiecka - <a href ="https://github.com/AgataLa" targer="_blank">Link do konta</a>

## Opis funkcjonalności
*Bot DogAdoptionHelper* zawiera rozbudowaną bazę wiedzy na temat procesu adopcyjnego, schronisk dla psów, opieki na psami. Bot ma dostęp do bazy danych, która zawiera informacje o psach do adopcji. Ma również dostęp do wizualizacji tej bazy przygotowanych w programie *PowerBI*. Funkcjonalności bota:
- Zwraca odpowiedzi tekstowe na zadane przez użytkownika pytania dotyczące wyżej wymienionej tematyki.
- Wyświetla wizualizację bazy danych o psach możliwych do adopcji.
- Zadaje pytania użytkownikowi o jego wymarzonego czworonoga i na podstawie uzyskanych odpowiedzi wyświetla propozycje możliwych psów do adopcji. Dodatkowo zwraca link do ogłoszenia.

## Architektura
<p align="center">
  <img src="https://user-images.githubusercontent.com/63157380/203542099-30f25e8b-e02e-4d4e-a20a-c031c3c98a61.png"/>
</p>

## Wybrany stos technologiczny

- Azure:
  - Azure Active Directory – organizacja Politechniki Warszawskiej na Azure nie pozwala na utworzenie bota, dlatego stworzyłyśmy własną organizację.
  - Bot Service – jest usługą, która pozwala stworzyć bota.
  - Language Studio – dzięki tej usłudze została przygotowana Knowledge Base, z której korzysta nasz bot.
  - SQL Database – baza danych, w której została stworzona tabela i gdzie są przechowywane dane dotyczące psów do adopcji.
  - Storage account (Blob storage) – wykorzystane do przechowanie obrazów z wizualizacją w blob storage.
- Środowisko Programistyczne:
  - Bot Framework Composer – środowisko to umożliwiło lokalne tworzenie bota.
  - Bot Framework Emulator – środowisko to umożliwiło przetestowanie powstałego bota.
  - PowerBI – środowisko to umożliwiło wizualizację informacji zawartych w bazie danych.
  
## Wyciągnięte wnioski
Podczas pracy nad tym projektem pojawiły się trzy znaczące przeszkody:
- Nie mogłyśmy połączyć naszego bota z dashboardem przygotowanym w *PowerBI*. Nasze konto studenckie nie pozwala na publikowanie wizualizacji i uzyskanie ich za pomocą REST API, do tego jest wymagana subskrypcja *PowerBI Pro*.
- Od 1 października 2022 nie można już tworzyć zasobów usługi *QnA Maker*, dzięki której przygotowywało się do niedawna Knowledge Base dla bota. Zamiast tego należy korzystać teraz z *Language Studio*. Niestety ta zmiana nie została wprowadzona w *Bot Framework Composer*. W programie tym dalej jest prośba o podłączenie się do *QnA Maker*, którego już nie można tworzyć. Udało się nam jednak rozwiązać ten problem poprzez łączenie się z *Language Studio* za pomocą zapytań HTTPS.
- Nie udało się nam niestety opublikować naszego bota na *Azure Portal*. Tworzyłyśmy go za pomocą *Bot Framework Composer* i przy próbie opublikowania go za każdym razem zwracany był nam błąd. Okazuje się, że żeby móc wykonać taką czynność potrzebne jest konto biznesowe na *Azure Portal*, a nie prywatne, które posiadamy. Próba stworzenia użytkownika w naszej organizacji kończyła się niepowodzeniem.  Miałyśmy możliwość tylko zaproszenia jakiegoś użytkownika zewnętrznego, ale stworzyć nowego użytkownika już nie mogłyśmy.

## Opis działania rozwiązania
Po uruchomieniu bota zostanie nam wyświetlony chat. Dostajemy od bota trzy opcje do wyboru, w których może nam pomóc. 

![bot1](https://user-images.githubusercontent.com/63157380/203542546-31fa4f86-3258-4273-aa52-c66fde1af123.png)

Po kliknięciu przycisku *Chcę znaleźć wymarzonego psa!*, bot zacznie zadawać użytkownikowi różne pytania, na podstawie których zdecyduje jakie psy z bazy danych są najbardziej odpowiednie. Przykładowe pytania to:
- Jakiej rasy szukasz?
- Czy musi być przyjazny dzieciom?
- Czy musi być już wychowany?
- W jakim wieku?

![bot7](https://user-images.githubusercontent.com/63157380/203542691-9c97fd6e-bf58-4b93-8a22-93901a4a2f60.png)
![bot10](https://user-images.githubusercontent.com/63157380/203542832-f0720973-83f0-4028-be97-7e541a36c70f.png)

Po udzieleniu odpowiedzi na wszystkie pytania, bot wyświetli propozycje psów do adopcji. Zostaną wypisane jego imię, rasa i link do ogłoszenia. W przypadku, gdyby nie udało się dopasować ani jednego psa do przedstawionych wymagań, użytkownik zostanie o tym poinformowany.

![bot11](https://user-images.githubusercontent.com/63157380/203542988-fc37f82a-3d0b-4a87-b342-316b0d180f27.png)

Po kliknięciu w link do ogłoszenia użytkownikowi otworzy się w przeglądarce karta z szczegółowymi informacjami o psie.

![bot12](https://user-images.githubusercontent.com/63157380/203543029-3c126385-00a5-457d-9f67-522359f18ce4.png)

Po kliknięciu przycisku *Chcę uzyskać informacje o procesie adopcji lub porady dotyczące opieki nad psem* użytkownik może zacząć zadawać pytania związane z tematyką adopcji albo opieką nad psem.  Po zadaniu pytania bot zwróci swoją odpowiedź. Po naciśnięciu przycisku *Już wszystko wiem!* zostanie wyświetlone użytkownikowi początkowe menu z trzeba opcjami do wyboru. Jeżeli okaże się, że bot nie zna odpowiedzi na postawione pytanie to zwróci komunikat: *Niestety nie znam odpowiedzi na Twoje pytanie*. Przykładowe pytania to:
- Czy muszę być osobą pełnoletnią, żeby adoptować psa?
- Jak przebiega proces adopcji psa?
- Jak nauczyć psa zostawania w domu?
- Jaki jest pierwszy etap adopcji?
- Jak często chodzić z psem do weterynarza?

![bot13](https://user-images.githubusercontent.com/63157380/203543212-f77ce9a3-4a93-43c6-a1df-e6f3be9d504a.png)

Po kliknięciu przycisku *Chcę zobaczyć statystyki psów w schroniskach*. Zostaną wyświetlone możliwe wizualizacje do wyboru.

![bot2](https://user-images.githubusercontent.com/63157380/203543350-feb02b62-9cf7-460a-bc47-6aa8a51b834e.png)

Należy teraz zdecydować jaka wizualizacja nas interesuje i kliknąć na nią. Po wybraniu zostanie nam ona wyświetlona. Mamy również możliwość kliknięcia w podpis wizualizacji, aby obejrzeć powiększony wykres w przeglądarce.

![bot3](https://user-images.githubusercontent.com/63157380/203543419-53b4f497-9960-4321-8923-ca43b0e27da7.png)
![bot4](https://user-images.githubusercontent.com/63157380/203543432-fff9a2c4-ec0b-43de-8f77-c7821092ad09.png)

## Demo na kanale YouTube







