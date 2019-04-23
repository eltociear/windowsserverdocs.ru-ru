## <a name="standard-configuration-considerations"></a>Рекомендации по стандартной конфигурации

AlwaysOn VPN имеет множество параметров конфигурации. Однако при выборе конфигурации VPN-, включите следующие сведения:

-   **Тип соединения.** Выбор протокола подключения важно и в конечном счете идет рука об руку с типом проверки подлинности, который будет использоваться. Дополнительные сведения о доступных протоколы туннелирования, см. в разделе [типы VPN-подключений](https://docs.microsoft.com/windows/access-protection/vpn/vpn-connection-type).

-   **Маршрутизация.** В этом контексте маршрутизации правила определяют, могут ли пользователи использовать другие сетевые маршруты, подключенных к виртуальной частной сети.

    -   _Раздельное туннелирование_ разрешает одновременный доступ к другим сетям, например в Интернете.

    -   _Принудительное туннелирование_ требует весь трафик должен проходить только через VPN и не поддерживает одновременный доступ к другим сетям.

-   **Активация.** _Активация_ определяет, как и когда VPN-подключение инициируется (например, при открытии приложения, при включении устройства, вручную пользователем). Активировать параметры, см. в разделе [VPN-подключения](#vpn-connectivity).

-   **Проверка подлинности пользователей или устройств.** AlwaysOn VPN использует сертификаты устройств и подключение инициированных устройством через функцию, называемую [туннель устройства](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-device-tunnel-config). Что подключения могут инициироваться автоматически и является постоянным, сходный туннельное подключение инфраструктуры DirectAccess.

>[!TIP]
>При миграции с DirectAccess AlwaysOn VPN, начните с параметрами конфигурации, которые сравнимы, что вы, а затем разверните оттуда.

С помощью сертификатов пользователей, всегда на VPN-клиент подключается автоматически, но это делается на уровне пользователей (после входа пользователей в систему) вместо на уровне устройства (до входа пользователей в систему). Процесс выполняется по-прежнему незаметно для пользователя, но она поддерживает более сложные механизмы проверки подлинности, например Windows Hello для бизнеса.