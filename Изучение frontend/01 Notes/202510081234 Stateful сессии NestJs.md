---
created: 2025-10-08 12:34
tags:
  - nestjs
  - express
---
# 202510081234 Stateful сессии NestJs

*Ссылка на StructureNote:*[[Nest.js]]
*Ссылка на исходник или контекст (если есть):* 

Для реализации stateful сессий в основном используют обычные файлы. При первом запросе сервер создаёт файл с уникальным именем, в который можно сохранить нужные данные. А в куки устанавливается уникальный идентификатор, по которому этот файл можно прочитать.

Чтобы использовать stateful сессию в приложении на Express.js, достаточно установить пакет `express-session` и типизацию для него:

```ts
npm install --save express-session
npm install --save-dev @types/express-session
```

`express-session` предоставляет мидлвару, которую необходимо зарегистрировать в приложении:

```ts
import * as session from 'express-session';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.use(
    session({
      secret: 'my-secret',
      resave: false,
      saveUninitialized: false,
    }),
  );

  await app.listen(3000);
}

bootstrap();
```

Мидлвара сама позаботится о создании файлов сессий и об установке кук для клиентов.

Для доступа к данным сессии, в объект запроса добавится свойство `session`, в которое можно записывать данные. Чтобы получить доступ к объекту сессии внутри контроллера, нужно использовать декоратор `@Session`:

```ts
import { Get, Controller } from '@nestjs/common';

@Controller('posts')
export class PostsController {
  @Get(':id')
  find(@Param('id') postId: string, @Session() session: Record<string, any>) {
    // Сохраняем в сессии количество просмотров поста
        if (!session.visits) {
      session.visits = {
        [postId]: 1,
      };
    } else {
      session.visits[postId] = session.visits[postId] ? session.visits[postId] + 1 : 1;
    }
  }
}
```

У сессии ограниченное время жизни — если пользователь не отправлял никаких запросов в течение определённого времени, файл сессии удаляется. Обычно в сессию сохраняют данные пользователя, чтобы не проводить каждый раз аутентификацию.

# Связанные идеи:

* [[202510081233 Stateless и statefull]]
* 
---

*Что стоит развить? Какие вопросы возникли?*
