# AKAI DISCORD BOT

## Funkcje:

- zarządzanie rolami
- nadawanie ról projektowych i technologicznych
- Komunikat Pomocy
- System punktów


## Setup do testów:
1. Załóż serwer discord o podobnej strukturze do serwera AKAI
2. Na discordzie włącz tryb developera, by umożliwić kopiowanie ID postów i emotikonów - [Jak to zrobić?](https://www.howtogeek.com/714348/how-to-enable-or-disable-developer-mode-on-discord/)
3. Stworzyć nową aplikację na [Discord Developer Portal](https://discord.com/developers/applications/.)


## Pomocne linki: 
- [SQLAlchemy](https://docs.sqlalchemy.org/en/14/orm/tutorial.html)
- [DiscordAPI](https://discordpy.readthedocs.io/en/stable/api.html) 
Do developmentu trzeba założyć własny serwer discord, oraz aplikacje na platformie developerskiej  
- Do kopiowania ID postów, emotikon etc można enablować tryb developerski w discordzie https://www.howtogeek.com/714348/how-to-enable-or-disable-developer-mode-on-discord/.  

Dane zawarte w bazie danych zawartej na repo również należy zmienić: ustawić własny id kanałow, id postów, emoty etc. Setupu troche jest ale jest intuicyjny. Z głównych rzeczy jest tam używany natywny logger, orm sqlalchemy (choc bardzo amatorsko) oraz discord.py sdk.

## Baza danych
Baza danych składa się z 6 tabel, każda z kolumn ma property not null:
 1. **commands** - mapuje komendy wpisane przez użytkownika po znaku $ do odpowiedzi;
    - command - TEXT
    - response - TEXT
 2. **helper_ranges** - określa dolne przedziały ról dla  rang helpera;
    - bottom_threshold - INT - PK
    - role_id - INT
 3. **helper_ranking** - przechowuje ilość punktów zdobytych przez każdego użytkownika;
    - user_id - INT - PK
    - points - INT - default 0
 4. **helper_rewards** - mapuje reakcje pod odpowiedziami na pytania do punktów którymi nagradzany jest odpowiadający;
    - level - INT
    - reaction_id - INT
 5. **messages_to_roles** - mapuje id wiadomości projektowej do roli która została dla tego projektu utworzona;
    - message_id - INT
    - role_id - INT
 6. **settings** - zawiera pary key:value do konfiguracji bota
    - key - TEXT - PK
    - value - TEXT