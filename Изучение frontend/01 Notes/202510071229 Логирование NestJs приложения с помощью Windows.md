---
created: 2025-10-07 12:29
tags:
  - nestjs
repeat: spaced every day
due_at: 2025-10-24T06:00:00.000+03:00
---
# 202510071229 Логирование NestJs приложения с помощью Windows

*Ссылка на StructureNote:*
*Ссылка на исходник или контекст (если есть):* 

Чтобы подключить Winston к приложению на Nest.js, нужно воспользоваться сторонним пакетом `nest-windows`. Также потребуется сам `winston`

```ts
$ npm install --save winston nest-winston
```

Этот пакет экспортирует динамический модуль `WinstonModule`, который мы можем подключить в корневой модуль приложения:

```ts
import { Module } from '@nestjs/common';
import { WinstonModule } from 'nest-winston';
import * as winston from 'winston';

@Module({
  imports: [
    WinstonModule.forRoot({
      levels: {
        critical_error: 0,
        error: 1,
        special_warning: 2,
        another_log_level: 3,
        info: 4,
      },
      transports: [
        new winston.transports.Console({ format: winston.format.simple() }),
        new winston.transports.File({ filename: 'error.log', level: 'error' }),
      ],
    }),
  ],
})
export class AppModule {}
```

В параметрах `forRoot` можно передать [конфигурацию для Winston](https://github.com/winstonjs/winston#usage)

Чтобы использовать `winston` внутри провайдеров или контроллеров, нужно внедрить логер с помощью константы `WINSTON_MODULE_PROVIDER`:

```ts
import { Injectable, Inject } from '@nestjs/common';
import { WINSTON_MODULE_PROVIDER } from 'nest-winston';
import { Logger } from 'winston';

@Injectable()
export class UsersService {
  constructor(@Inject(WINSTON_MODULE_PROVIDER) private logger: Logger) {}

  create() {
    this.logger.log('Creating a user');
  }
}
```

Чтобы подключить логер на корневом уровне, нужно использовать другую константу — `WINSTON_MODULE_NEST_PROVIDER` в `main.ts`:

```ts
const app = await NestFactory.create(AppModule);

app.useLogger(app.get(WINSTON_MODULE_NEST_PROVIDER));

await app.listen(3000);
```

### Связанные идеи:

* [[202509301412 Библиотека для логирования winston]]
* [[202510071219 Логирование в NestJs]]
---

*Что стоит развить? Какие вопросы возникли?*
