### Что это

**Express** — это инструмент, который позволяет написать веб-сервер любой сложности. Даже некоторые высоконагруженные приложения работают, используя NodeJS и Express.

### Пример сервера

```
const PORT = 4000;

const express = require('express');
const app = express();

app.use(express.static('./'));

app.listen(PORT, function () {
  console.log(`Example app listening on port ${PORT}!`);
});
```

