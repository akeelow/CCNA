
## Настройка маршрутизатора в качестве сервера DHCPv6 с отслеживанием состояния

```bash
interface GigabitEthernet0/0/1
  description Link to LAN
  ipv6 address fe80::1 link-local
  ipv6 address 2001:db8:acad:1::1/64
  ipv6 nd managed-config-flag             # 
  ipv6 nd prefix default no-autoconfig    # измените флаг A с 1 на 0
  ipv6 dhcp server IPV6-STATEFUL
  no shut
  end
```

## Маршрутизатор также может быть клиентом DHCPv6

```bash
ipv6 unicast-routing
interface g0/0/1
  ipv6 enable
  ipv6 address dhcp
```

## Ретрансляция

```bash
interface gi0/0/0
  ipv6 dhcp relay destination 2001:db8:acad:1::2 g0/0/1
```

## Команды проверки DHCPv6

```bash
show ipv6 interface brief        # посмотреть назначенный ip
show ipv6 dhcp interface g0/0/1  # посмотреть другие полученные параметры (днс, домен)
show ipv6 dhcp pool              # проверить имя DHCPv6-пула, параметры, количество активных клиентов
show ipv6 dhcp binding           # 
```
