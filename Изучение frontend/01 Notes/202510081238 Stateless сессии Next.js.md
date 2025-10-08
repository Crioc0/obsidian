---
created: 2025-10-08 12:38
tags:
  -
---
# 202510081238
*Ссылка на StructureNote:*[[Nest.js]]
*Ссылка на исходник или контекст (если есть):* 

Вместо того чтобы хранить данные пользователя на сервере, можно передавать их с каждым запросом. Таким образом они тоже будут доступны в рамках одной пользовательской сессии, но при этом на сервере не будет храниться её состояние — такой способ реализации сессии часто называют stateless.

Основной проблемой stateless сессии является безопасность. Сервер должен убедиться, что данные от пользователя не сфабрикованы. Поэтому чаще всего применяются уже знакомые вам JWT-токены, потому что в них можно закодировать любую информацию, подлинность которой, к тому же, можно верифицировать.

После валидации JWT-токена данные из него можно записать в объект запроса в свойство `locals`:
```ts
import { Injectable, CanAvtivate, ExecutionContext } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthGuard implements CanActivate {
  constructor(private jwtService: JwtSerivce) {}

  canActivate(context: ExecutionContext) {
    const request = context.switchToHttp().getRequest();
    const token = request.headers['authorization']
    let user;

    try {
      user = this.jwtService.verify(token);
    } catch (_) {
      return false;
    }

    req.locals.user = user;

    return true;
  }
} 
```
# Связанные идеи:
*
---

*Что стоит развить? Какие вопросы возникли?*