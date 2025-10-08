---
created: 2025-10-08 12:42
tags:
  - nestjs
---
# 202510081242
*Ссылка на StructureNote:*
*Ссылка на исходник или контекст (если есть):* 

Одним из способов передачи сесcионных данных или `id` сессии являются Cookies. 
Чтобы получить доступ кукам, понадобится пакет для Express.js, а именно `cookie-parser` и типы для него:
```ts
npm install --save cookie-parser
npm install --save-dev @types/cookie-parser
```
Регистрируем парсер в приложении:
```ts
import * as cookieParser from 'cookie-parser';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.use(cookieParser);

  await app.listen(3000);
}

bootstrap();
```
Этот пакет предоставляет мидлвару, которая парсит заголовки и добавляет в объект запроса свойство `cookies`. Чтобы получить доступ к кукам внутри контроллера, нужно обратиться к объекту запроса. Например, если у вас есть кука `authCookie`, вы можете получить её в контроллере и проверить, авторизован ли пользователь:
```ts
import { Get, Controller, ForbiddenException, Req } from '@nestjs/common';
import { Request } from 'express';

@Controller('users')
export class UsersController {
  @Get('me')
  me(@Req() request: Request) {
    const authCookie = request.cookies.authCookie;

    if (!isAuthorized(authCookie)) {
      throw new ForbiddenException();
    }

    return this.usersService.me();
  }
}
```
Чтобы установить куки в ответе, нужно использовать стандартный метод объекта ответа в Express — `res.cookie`:
```ts
import { Get, Controller, ForbiddenException, Req, Res } from '@nestjs/common';
import { Request, Response } from 'express';

@Controller('users')
export class UsersController {
  @Get('me')
  me(@Req() request: Request, @Res({ passthrough: true }) response: Response) {
    const authCookie = request.cookies.authCookie;

    if (isAuthorized(authCookie) {
      return this.usersService.me();
    }

    try {
      const token = this.authService.auth();

      // устанавливаем куку в ответ на запрос
      response.cookie('authCookie', token);
    } catch (_) {
      throw new ForbiddenException();
    }
  }
}
```
**Если не указать опцию `passthtrough : true`, Nest.js будет ждать ответа Response** 
# Связанные идеи:
* [[202510081233 Stateless и statefull]]
---

*Что стоит развить? Какие вопросы возникли?*