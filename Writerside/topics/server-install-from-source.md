# Установка из исходников GitHub

Добро пожаловать в раздел серверной части Gml.Backend. Здесь вы найдете инструкции по установке и настройке серверной части проекта.

### Репозиторий на GitHub

Ссылка на репозиторий: [Gml.Backend](https://github.com/GamerVII-NET/Gml.Backend)

### Инструкция по установке

#### Шаг 1: Клонирование репозитория

Выполните следующую команду в вашем терминале:

<tabs>
    <tab title="Стабильная версия">
      <code-block lang="bash">
        git clone --recursive https://github.com/GamerVII-NET/Gml.Backend.git
      </code-block>
    </tab>
    <tab title="Последняя актуальная">
      <code-block lang="bash">
            git clone --recursive \
                      --branch dev https://github.com/GamerVII-NET/Gml.Backend.git
      </code-block>
    </tab>
</tabs>

#### Шаг 2: Переход в директорию проекта

Выполните следующую команду в вашем терминале:

```bash
cd Gml.Backend
```

#### Шаг 3: Настройка config файла

Отредактируйте или создайте файл `.env` в корне папки `Gml.Backend`

```yaml
# Пример уже настроенного .env

# API Endpoint для запросов
# Необходимо заменить на свой адрес и порт,
# на котором расположело API
# порт должен совпадать с переменной PORT_GML_BACKEND
API_URL=http://localhost:5000

# UID (User Identifier) и GID (Group Identifier) используется 
# для указания id пользователя и группы в Linux.
UID=0
GID=0

S3_ENABLED=true # Вклуючить подключение к S3

MINIO_ROOT_USER=minioadmin # root пользователь панели управления
MINIO_ROOT_PASSWORD=minioadmin # root пароль панели управления
MINIO_ADDRESS=:9000 # адрес панели (:9000 или 10.2.0.1:9000)
MINIO_ADDRESS_PORT=9000 # Порт панели, должен совпадать с записью выше
MINIO_CONSOLE_ADDRESS=:9001 # адрес консоли (:9001 или 10.2.0.1:9001)
MINIO_CONSOLE_ADDRESS_PORT=9001 # Порт (совпадает с записью выше)                       

# Настройки внешнего доступа 
# Порты, на которых будут работать приложения
PORT_GML_BACKEND=5000         # Web Api
PORT_GML_FRONTEND=5003        # Панель управления проектом
PORT_GML_FILES=5005           # Файловый сервис
PORT_GML_SENTRY=5007          # Панель управления ошибками
PORT_GML_SKINS=5006           # Сервис скинов 
```

Отредактируйте или создайте файл `.env` в папке `src\Gml.Web.Client\.env`

```yaml
NEXT_PUBLIC_BASE_URL=http://localhost:5000 # Адрес к Web Api
NEXT_PUBLIC_PREFIX_API=api
NEXT_PUBLIC_VERSION_API=v1
```

#### Шаг 4: Настройка appsettings.json (Опционально)

Отредактируйте или создайте файл `appsettings.json` в папке `src\Gml.Web.Api\src\Gml.Web.Api`

<tabs>
    <tab title="Пример">
      <code-block lang="json">
        {
          "Logging": {
            "LogLevel": {
              "Default": "Information",
              "Microsoft.AspNetCore": "Warning"
            }
          },
          "ServerSettings": {
            "ProjectName": "GmlServer1", # Название проекта
            "ProjectDescription": "Project Description", # Описание проекта
            "ProjectPath": "", # Заполнить, если нужно переименовать папку
            "ProjectVersion": "1.0.0-alpha", # Версия приложения (Authlib)
            "SecretKey": "SecretKey", # Секретный ключ (openssl rand -hex 32)
            "SkinDomains": [ # Домены и поддомены, откуда берутся скины
                "localhost",
                "recloud.tech",
                ".recloud.tech"
            ],
            "PolicyName": "GmlPolicy" # Наименование CORS политики
          },
          "ConnectionStrings": {
            "SQLite": "Data Source=data.db" # Путь к локальной базе данных
          }
        }
        </code-block>
    </tab>
    <tab title="Чистый файл">
        <code-block lang="json">
        {
          "Logging": {
            "LogLevel": {
              "Default": "Information",
              "Microsoft.AspNetCore": "Warning"
            }
          },
          "ServerSettings": {
            "ProjectName": "",
            "ProjectPath": "",
            "ProjectVersion": "",
            "SkinDomains": [],
            "ProjectDescription": "",
            "SecretKey": "",
            "PolicyName": ""
          },
          "ConnectionStrings": {
            "SQLite": ""
          }
        }
        </code-block>
    </tab>
</tabs>

#### Шаг 5: Запуск проекта с использованием Docker

Выполните следующую команду в вашем терминале:

```bash
docker compose up
```

Пожалуйста, убедитесь, что Docker установлен и работает на вашем компьютере для выполнения этой команды.

После выполнения команды Docker загрузит необходимые образы и запустит проект.
После запуска проекта, вы сможете открыть его в браузере, используя следующие адреса:

## Инфраструктура

<procedure title="Сервеная инфраструктура" id="inject-a-procedure">
    <step>
        <p>
            <span>WebApi</span>
            <a href="http://localhost:5000">http://localhost:5000</a>
        </p>
    </step>
    <step>
        <p>
            <span>Web Dashboard</span>
            <a href="http://localhost:5003">http://localhost:5003</a>
            <br/>
            <code>необходимо пройти предварительную регистрацию</code>
        </p>
    </step>
    <step>
        <p>
            <span>Web FileBrowser</span>
            <a href="http://localhost:5005">http://localhost:5005</a>
            <br/>
            <code>логин и пароль по умолчанию: admin:admin</code>
        </p>
    </step>
    <step>
        <p>
            <span>Sentry (Журнал ошибок)</span>
            <a href="http://localhost:5007/register">http://localhost:5007</a>
            <br/>
            <code>Необходимо пройти предварительную регистрацию</code>
        </p>
    </step>
</procedure>


