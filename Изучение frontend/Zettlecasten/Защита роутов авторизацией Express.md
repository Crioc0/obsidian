2025 09 2311 35
Tags: #express 
###### Links: 
1) 
# Заметка
Авторизация в приложении работает как мидлвар. Если представлен верный токен, запрос проходит на дальнейшую обработку. Иначе запрос переходит контроллеру, который возвращает клиенту сообщение об ошибке.

Сперва нужно извлечь токен из header или cookie. Затем его нужно верифицировать при помощи метода `verify` модуля `jsonwebtocken`. Метод принимает на вход два параметра — токен и секретный ключ, которым этот токен был подписан.
```ts
import { Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';

import { JwtPayload, jwtPayload } from '../types/jwtPayload';
import { UNAUTHORIZED_ERROR } from '../helpers/statusCodes';
import { ERROR_MESSAGES } from '../helpers/messages';

const auth = (req: JwtPayload, res: Response, next: NextFunction) => {
  try {
    const token = req.cookies.jwt;

    if (!token) {
      return res.status(UNAUTHORIZED_ERROR).json({ message: ERROR_MESSAGES.AUTH.UNAUTHORIZED });
    }

    const JWT_SECRET = process.env.JWT_SECRET || 'your-secret-key';
    req.user = jwt.verify(token, JWT_SECRET) as jwtPayload;
    return next();
  } catch (error) {
    if (error instanceof jwt.JsonWebTokenError) {
      return res.status(401).send({ message: 'Неверный токен' });
    }
    if (error instanceof jwt.TokenExpiredError) {
      return res.status(401).send({ message: 'Срок действия токена истек' });
    }
    return res.status(401).send({ message: 'Ошибка авторизации' });
  }
};

export default auth;
```
Для того, чтобы добавить авторизационный мидлвар в приложении 