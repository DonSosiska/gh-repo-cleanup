# gh-repo-cleanup

Маленький CLI для масового чищення старих/непотрібних репозиторіїв на GitHub.
Обгортка над [GitHub CLI](https://cli.github.com) (`gh`).

## Встановлення

Потрібен встановлений і авторизований `gh`:

```bash
gh auth login
gh auth refresh -h github.com -s delete_repo   # окремий scope для видалення
```

Клонуйте репозиторій і зробіть скрипт виконуваним:

```bash
git clone <your-repo-url>
cd gh-repo-cleanup
chmod +x gh-repo-cleanup
```

(За бажанням — додайте папку в `PATH`, щоб викликати `gh-repo-cleanup` звідусіль.)

## Використання

### 1. Отримати список усіх репозиторіїв

```bash
./gh-repo-cleanup list -o repos_review.txt
```

Створить файл, відсортований за датою останнього оновлення (найстаріші — зверху),
із позначками fork/archived/stars.

### 2. Обрати, що видалити

Відкрийте `repos_review.txt`, скопіюйте потрібні рядки (лише `власник/назва`)
у новий файл `to_delete.txt`, по одному репозиторію на рядок:

```
DonSosiska/old-lab-1
DonSosiska/old-lab-2
```

### 3. Видалити

```bash
./gh-repo-cleanup delete -f to_delete.txt
```

Скрипт покаже повний список репозиторіїв, попросить ввести `YES` для
підтвердження і лише після цього почне видаляти.

## ⚠️ Увага

Видалення репозиторію на GitHub **незворотне**. Завжди перевіряйте вміст
`to_delete.txt` перед запуском `delete`.
