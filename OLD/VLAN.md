___


## Rodzaje VLAN

- **VLAN default**: (VLAN 0) domyślny VLAN, przed konfiguracją każdy port należy do niego.

- **VLAN data**: Standardowa sieć VLAN przez którą przesyłane są dane generowane przez urządzenia takie jak stacje robocze.

- **VLAN native**: (domyślnie  VLAN 1) Jest to VLAN używany na interfejsach działających w trybie trunk. Przesyłany jest przez niego ruch pochodzący z wielu VLANów.

- **VLAN management**: Administratorzy tworzą go gdy chcą odseparować ruch użytkowników od ruchu związanego z zarządzaniem siecią.
___

## Ważne pojęcia

- **DTP** (Dynamic Trunking Protocol): Automatyczny tryb negocjacji pracy interfejsu.
	-  *Dynamic auto*: Interfejs dopasowywuje się do trybu na drugim interfejsie.
	-  *Dynamic desirable*: Interfejs negocjuje trunk, gdy po drugiej stronie jest desirable, auto lub trunk.

- **VTP** (VLAN Trunking Protocol): Protokół umożliwiający przesyłanie konfiguracji dotyczącej VLANów między przełącznikami. VTP posiada 3 różne tryby pracy:
	-  *Server*: w tym trybie może pracować tylko jeden przełącznik w danej domenie VTP. Z nim łączą się pozostałe przełączniki.
	-  *Client*: przełącznik łączy się z serwerem VTP i pobiera od niego konfiguracje.
	-  *Transparent*: Przełącznik nie uczestniczy w pobieraniu konfiguracji.

- **VTP pruning**: blokuje przesyłanie przez trunk VLANów do przełącznika na którym nie są skonfigurowane. 
___

## Komendy Konfiguracyjne
#### 1. Utworzenie sieci VLAN 10 i 20:
```
switch(config)# vlan 10
switch(config-vlan)# name NOWY_VLAN_10
switch(config-vlan)# vlan 20
switch(config-vlan)# name NOWY_VLAN_20
```
#### 2. Przypisanie interfejsów do VLANów:
```
switch(config)# int f0/1
switch(config-if)# switchport mode access
switch(config-if)# switchport access vlan 10
switch(config-if)# int f0/2
switch(config-if)# switchport mode access
switch(config-if)# switchport access vlan 20
```
#### 3. Utworzenie portów chronionych:
```
switch(config)# int f0/1
switch(config-if)# switchport protected
swtich(config-if)# int f0/2
switch(config-if)# switchport protected
```
#### 4. Konfiguracja portu typu *trunk*:
```
switch(config)# int f0/5
switch(config-if)# switchport trunk encapsulation dot1q
switch(config-if)# switchport mode trunk
```
#### 5. Określenie które VLANy mogą być przesyłane przez port *trunk*:
```
switch(config-if)# switchport trunk allowed vlan 10,20
```
#### 6. Zmiana VLANu natywnego:
```
switch(config-if)# switchport mode trunk native VLAN 999
```
#### 7. Wyłączenie *DTP*:
```
switch(config-if)# switchport nonegotiate
```
#### 8. Konfiguracja *VTP*:
```
1. Konfiguracja urządznia jako serwer VTP:
	switch1(config)# vtp mode server
	switch1(config)# vtp domain NAZWA_DOMENY
	switch1(config)# vtp password cisco

2. Utawienie urządzenia w tryb client:
	switch2(config)# vtp mode client
	switch2(config)# vtp password cisco
```
#### 9. Konfiguracja *VTP pruning*:
```
switch(config)# vtp pruning
```
#### 10. Usuwanie konfiguracji VLAN:
```
switch# delete vlan.dat
```


