# 🚀 Deploying Vite App to GitHub Pages

## 📄 Источники

- [Документация Vite](https://vitejs.dev/)
- [gh-pages (npm)](https://www.npmjs.com/package/gh-pages)
- [Video: Deploying Vite App to GitHub Pages.](https://www.youtube.com/watch?v=sIL-C87po1s&t=1090s)
- [Manual](https://md-deploy.vercel.app/)
- [Git и GitHub, основа в виде команд](https://daniilminin.gitbook.io/git-i-github-osnova-v-vide-komand)

---

## 📦 Установка `gh-pages`

### Terminal

```bash
  pnpm add gh-pages
```

### package.json

```json
   "dependencies": {
   "gh-pages": "6.3.0" // Версия может отличаться
   }
```

---

## ⚙️ Добавляем скрипты для деплоя

### package.json

```json
   "scripts": {
      "dev": "vite",
      "build": "tsc -b && vite build --base=./",
      "lint": "eslint .",
      "preview": "vite preview",
      "predeploy": "pnpm run build",
      "deploy": "gh-pages -d dist"
   }
```

---

## 🚀 Запускаем процесс деплоя

### Terminal

```bash
  pnpm run deploy
```

---

## 🎉 Поздравляем!

Успешный деплой приложения на GitHub Pages!  
Теперь проект доступен по ссылке вида:  
`https://<username>.github.io/<repository-name>/`

---

## 🧠 Как это работает

1. **Запуск команды**  
   `pnpm run deploy` проверяет наличие скрипта `predeploy`.

2. **Если он есть**, сначала запускается:
   ```bash
   pnpm run predeploy
   ```

3. Это, в свою очередь, выполняет:
   ```bash
   pnpm run build
   ```

4. Что делает `build`:
    - `tsc -b`: компилирует TypeScript в JavaScript.
    - `vite build --base=./`: создаёт сборку в папке `dist`.

5. **Почему `--base=./` важно:**
    - По умолчанию Vite использует `/` как базовый путь.
    - GitHub Pages загружает сайт в подкаталог:  
      `https://username.github.io/repository-name/`
    - Чтобы пути к ресурсам были корректны, нужно использовать относительные пути (`./`).

6. После сборки запускается:
   ```bash
   gh-pages -d dist
   ```

7. Эта команда публикует содержимое папки `dist` на GitHub Pages.

---

8. vite.config.ts
```` json
   export default defineConfig({
       plugins: [react()],
       base: '/hw-deploy-pages/'
   })
````

👍 Готово! Можно делиться ссылкой на сайт.
