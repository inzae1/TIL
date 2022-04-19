

# NestJS DTO(Data Transfer Object)


### **DTO(Data Transfer Object)**
- 네트워크를 통해 데이터가 어떻게 전송될지 정의하는 객체이다.
- DTO 스키마를 클래스를 통해 쉽게 정의할 수 있다.

```typescript
//create-movie.dto.ts
export class CreateMovieDto {
  title: string;
  year: number;
  genres: string[];
}
```

- `class-validator` 와 `class-transformer` 를 설치하고 이를 기반으로 파이프를 만들어 이를 통해 객체의 유효성을 체크할 수 있다. (파이프는 일종의 미들웨어)

```bash
npm i class-validator class-transformer
```

- 위 명령어로 `class-validator` 와 `class-transformer` 를 설치할 수 있다.
```typescript
//create-movie.dto.ts
import { IsNumber, IsString } from 'class-validator';

export class CreateMovieDto {
    @IsString()
    readonly title: string;

    @IsNumber()
    readonly year: number;

    @IsString({ each: true })
    readonly genres: string[];
}
```

- `create-movie.dto.ts` 에서 dto에 형식을 체크할 수 있는 `@isString`, `@isNumber` 데코레이터를 추가해준다.

```typescript
//main.ts
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true,
      transform: true,
    }),
  );
  await app.listen(3000);
}
bootstrap();
```

- `main.ts` 파일에 위와 같이 `app.useGlobalPipes` 를 추가하고, 여기에 `ValidationPipe` 를 넣어 체크한다.
- `main.ts` 에 파이프를 설치하지 않으면 dto 파일에 타입체크 decorator 를 추가해도 걸러지지 않는다.
- whitelist: 아무 decorator 도 없는 속성을 가진 object 는 거를 수 있음
- forbidNonWhitelisted: 유효하지 않는 데이터의 request 자체를 막을 수 있음
- transfor: 가능한 경우 실제 데이터 타입으로 변환하여 처리해줌