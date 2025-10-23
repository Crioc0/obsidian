---
created: 2025-10-05 18:01
tags:
  - nestjs
repeat: spaced every day
due_at: 2025-10-24T06:00:00.000+03:00
---
# 202510051801 Exeption Filter

*Ссылка на StructureNote:* [[Nest.js]]
*Ссылка на исходник или контекст (если есть):* 

При возникновении исключения в контроллере Nest.js сформирует стандартный ответ для клиента:

```ts
{
  "statusCode": 400,
  "message": "User already exists"
}
```

Фильтры исключений нужны как раз для того, чтобы изменить формат ответа при возникновении ошибки. Например, ответ должен выглядеть так:

```ts
{
  "error": {
    "status": 400,
    "message": "User already exists",
    "method": "POST",
    "url": "/users",
  }
}
```

Чтобы получить нужный формат, давайте создадим фильтр исключений. Для этого вам нужно применить декоратор `@Catch` к классу, который реализует интерфейс `ExceptionFilter`.

Декоратор `@Catch` в качестве аргумента принимает класс ошибки, для которой будет вызван метод `catch`. Если передать туда `HttpException`, то фильтр будет срабатывать для всех исключений. Давайте ограничим наш фильтр только для `UserAlreadyExistsException`:

```ts
import { ExceptionFilter, Catch, HttpException } from '@nestjs/common';
import { UserAlreadyExistsException } from '../exceptions/user-exists.exception';

@Catch(UserAlreadyExistsException)
export class UserAlreadyExistsExceptionFilter implements ExceptionFilter {
  catch() {}
}
```

Метод catch принимает два аргумента;

- объект исключения, которое было выброшено в контроллере;
- объект типа `ArgumentsHost`. `ArgumentsHost` — это почти то же самое, что и `ExecutionContext`, который мы использовали для гардов. Единственное отличие — у `ArgumentsHost` нет доступа к метаданным обработчика запроса.
Именно благодаря `ArgumentsHost` вы получаете доступ к объекту ответа, чтобы изменить его:

```ts
@Catch(UserAlreadyExistsException)
export class UserAlreadyExistsExceptionFilter implements ExceptionFilter {
  catch(exception: UserAlreadyExistsException, host: ArgumentsHost) {
    const status = exception.getStatus();
    const message = exception.getResponse();

    const ctx = host.switchToHttp();

    const request = ctx.getRequest();
    const response = ctx.getReponse();

    // меняем объект ответа
    reponse
      .status(status)
      .json({
        error: {
          status: status,
          message: message,
          method: request.method,
          url: req.url,
        }
      });   
  }
}
```

Для подключения нужно использовать декоратор `@useFilter`

```ts
import { Controller, UseFilters } from '@nestjs/common';
import { UserAlreadyExistsExceptionFilter } from '../filters/user-exists.filter';

@Controller('users')
@UseFilters(UserAlreadyExistsExceptionFilter)
export class UsersController {}
```

Или можно подключить фильтр для всех запросов сразу в файле `main.ts`:

```ts
async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.useGlobalFilters(new UserAlreadyExistsExceptionFilter());

  await app.listen(3000);
}
```

### Связанные идеи:

* 
---

*Что стоит развить? Какие вопросы возникли?*
