___
Żeby można było skonfigurować na porcie **Port Security**, należy ustawić tryb portu na access lub trunk. Nie można korzystać z trybów dostępnych w DTP dlatego najlepiej jest tą funkcjonalność wyłączyć na portach, które konfigurujemy.
___

## Ważne pojęcia

- **switchport port-security mac-address [opcja]**: umożliwia przydzielenie dostępu urządzeniu z konkretnym adresem MAC. Dostępne opcje dla tej komendy:
	- *x.x.x.x*: Ręczne przydzielenie adresu MAC urządzenia końcowego.
	- *forbidden*: Pozwala na ręczne zablokowanie konkretnego adresu MAC.
	- *sticky*: Przydziela adres MAC interfejsu który podłączył się jako pierwszy do portu.


## Komendy konfiguracyjne
#### 1. Uruchomienie Port Security na interfejsie:
```
switch(config)# int f0/1
switch(config-if)# switchport port-security
```
#### 2. Przydzielenie dostępu dla pierwszego adresu MAC podłączonego do portu:
```
switch(config-if)# switchport port-security mac-address sticky
```
#### 3. Ustawienie ilości adresów MAC które mogą się komunikować na tym porcie:
```
switch(config-if) switchport port-security maximum 10
```
#### 4. Określenie zachowania przełącznika w przypadku naruszenia parametrów bezpieczeństwa:
```
switch(config-if) switchport port-security violation [opcja]

Opcje:
- protect:  Blokuje ruch, nie rejestruje zdarzenia
- restrict: Blokuje ruch, rejestruje zdarzenie
- shutdown (default): Wyłącza interfejs 
```
#### 5. Sprawdzenie rejestru zdarzeń:
```
switch# show port-security interface [numer interfejsu]
```

