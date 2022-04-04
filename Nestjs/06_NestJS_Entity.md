

# NestJS Entity


#### TypeORM 을 이용하여 User Entity 만들기
- TypeORM 은 저장소 디자인 패턴을 지원하므로 각 엔터티에는 자체 저장소가 있다. 이런 레파지토리는 데이터베이스 연결을 통해 얻을 수 있다
- 기본적으로 테이블 컬럼과 1대1 관계로 만들어진다


```typescript
// user.entity.ts
import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column({ default: true })
    isActive: boolean;
}
```

- `User` 엔터티 파일은 `UserModule` 모델을 보관할 위치를 결정할 수 있지만 모듈 디렉토리의 해당 도메인 근처에 생성하는것이 좋다.  
```typescript
// app.module.ts
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './users/user.entity';

@Module({
    imports: [
        TypeOrmModule.forRoot({
            type: 'mysql',
            host: 'localhost',
            port: 3306,
            username: 'root',
            password: 'root',
            database: 'test',
            entities: [User],
            synchronize: true,
        }),
    ],
})
export class AppModule {}
}
```
