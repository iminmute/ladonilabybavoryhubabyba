# Практическая работа № 8 — файловая почта

Реализация задания «Файловая почта: поиск, сортировка и безопасный обмен файлами»
(Python 3.9+, без интернета).

## Структура

| Файл / папка | Назначение |
|---|---|
| `file_exchange_starter.py` | Основная программа: все TODO 1–5 реализованы |
| `tamper_demo.py` | Создаёт испорченную копию ZIP для проверки отказа |
| `test_selfcheck.py` | 5 автоматических тестов |
| `Практическая_08_Студентам_каркас_и_подсказки.docx` | Оригинальное задание |
| `Ответы_на_вопросы.md` | Развёрнутые ответы на вопросы защиты |
| `ОТЧЁТ.md` | Краткий отчёт и шпаргалка |
| `selfcheck.log` | Лог запуска команд и тестов |
| `workspace/data/` | Учебные файлы (создаются командой `prepare`) |
| `workspace/outbox/` | Отправленный ZIP и испорченная копия |
| `workspace/inbox/notes.txt` | Принятый файл |
| `workspace/report.csv` | CSV-отчёт (дополнительное задание) |

## Как запустить

```powershell
python file_exchange_starter.py prepare
python file_exchange_starter.py scan --pattern "*.txt"
python file_exchange_starter.py pack --file notes.txt --sender team_A --recipient team_B
python file_exchange_starter.py receive --package "workspace/outbox/team_A__team_B__notes.zip" --recipient team_B
python tamper_demo.py "workspace/outbox/team_A__team_B__notes.zip"
python file_exchange_starter.py receive --package "workspace/outbox/corrupted_team_A__team_B__notes.zip" --recipient team_B
python file_exchange_starter.py report
python -m unittest test_selfcheck.py -v
```

## Результаты

- Все 5 тестов проходят (`OK`).
- Отправленный и принятый файлы имеют одинаковый SHA-256:
  `d2bc5eb722d041779bee8ea7f2e268af16fe51a89d89ef8f9946c03243d99777`.
- Испорченная копия отклоняется с `ValueError`, файл в `inbox` не создаётся.

> При повторном запуске `pack`/`receive` удалите старые файлы из `workspace/outbox` и `workspace/inbox` — режим `xb` и проверка существования пакета намеренно запрещают перезапись.

## Примечание об обмене

Обмен выполнен **локально между ролями team_A и team_B** на одном компьютере: пакет из `workspace/outbox` принят в `workspace/inbox`, хеши совпадают, испорченная копия отклонена. Если преподаватель требует обмен именно с соседней командой (другая машина / USB / общая папка), повторите шаги `pack → receive`, передав ZIP напарнику, и добавьте его лог/скриншот. Устную защиту нужно ответить по файлу `Ответы_на_вопросы.md` — один только файл заменой устному ответу не является.
