# NestJS Data Loader
- `N+1` 문제를 해결하기 위해 사용

## Installation
```bash
npm i nestjs-dataloader --save
```

## 사용 방법
### 1. DataLoader 생성
- 첫 번째 제네릭은 DB의 ID 타입
- 두 번째 제네릭은 return될 타입

```js
import { Injectable } from '@nestjs/common';
import * as DataLoader from 'dataloader';
import { NestDataLoader } from 'nestjs-dataloader';
import { RateplanService } from '../../service/rateplan.service';
import { RateplanInformationObjectType } from '../../type/rateplan-information.object.type';

@Injectable()
export class RateplanInformationLoader implements NestDataLoader<number, RateplanInformationObjectType> {
  constructor(private readonly rateplanService: RateplanService) {}

  generateDataLoader(): DataLoader<number, RateplanInformationObjectType> {
    return new DataLoader<number, RateplanInformationObjectType>(async (keys) => {
      const rateplanInformations: RateplanInformationObjectType = await this.rateplanService.getRateplanInformations(<number>keys);
    });
  }
}
```

### 2. DataLoader를 모듈에 provider로 추가
```js
import { Module } from '@nestjs/common';

import { RateplanResolver } from './resolver/rateplan.resolver';
import { RateplanService } from './service/rateplan.service';
import { CommonRateplanService, CommonRateplanTemplateService } from '@/services';
import { RateplanSubResolver } from './resolver/rateplan.sub-resolver';
import { RateplanInformationLoader } from './resolver/loader/rateplan-information.loader';
import { DataLoaderInterceptor } from 'nestjs-dataloader';
import { APP_INTERCEPTOR } from '@nestjs/core';
import { RateplanChildLoader } from './resolver/loader/rateplan-child.loader';
@Module({
  exports: [RateplanService],
  providers: [
    // Resolver
    RateplanResolver,
    RateplanSubResolver,

    //Service
    RateplanService,
    CommonRateplanService,
    CommonRateplanTemplateService,

    // DataLoader
    RateplanInformationLoader,
    RateplanChildLoader,
    {
      provide: APP_INTERCEPTOR,
      useClass: DataLoaderInterceptor,
    },
  ],
})
export class RateplanModule {}
```

### 3. Resolver에서 DataLoader 사용
- `@Loader` Decorator의 매개변수가 메소드에 주입하고자 하는 DataLoader class
- 주입된 DataLoader 메소드로 대량 검색 및 캐싱을 처리
```js
import { Resolver, ResolveField, Parent } from '@nestjs/graphql';
import { RateplanObjectType } from '../type/rateplan.object-type';
import { RateplanService } from '../service/rateplan.service';
import { RateplanInformationObjectType } from '../type/rateplan-information.object.type';
import { RateplanInformationLoader } from './loader/rateplan-information.loader';
import * as DataLoader from 'dataloader';
import { Loader } from 'nestjs-dataloader';
import { RateplanChildLoader } from './loader/rateplan-child.loader';

@Resolver((of) => RateplanObjectType)
export class RateplanSubResolver {
  constructor(private readonly rateplanService: RateplanService) {}

  @ResolveField((returns) => RateplanInformationObjectType)
  public async rateplanInformations(
    @Parent() rateplan: RateplanObjectType,
    @Loader(RateplanInformationLoader.name)
    rateplanLoader: DataLoader<RateplanObjectType['id'], RateplanInformationObjectType>,
  ): Promise<RateplanInformationObjectType> {
    return rateplanLoader.load(rateplan.id);
  }
}
```

## Array로 리턴하는 Case
```js
import { Injectable } from '@nestjs/common';
import * as DataLoader from 'dataloader';
import { NestDataLoader } from 'nestjs-dataloader';
import { RateplanService } from '../../service/rateplan.service';
import { RateplanInformationObjectType } from '../../type/rateplan-information.object.type';

@Injectable()
export class RateplanInformationLoader implements NestDataLoader<number, RateplanInformationObjectType[]> {
  constructor(private readonly rateplanService: RateplanService) {}

  generateDataLoader(): DataLoader<number, RateplanInformationObjectType[]> {
    return new DataLoader<number, RateplanInformationObjectType[]>(async (keys) => {
      const rateplanInformations: RateplanInformationObjectType[] = await this.rateplanService.getRateplanInformations(
        <number[]>keys,
      );
      return keys.map((key) =>
        rateplanInformations.filter((rateplanInformation) => rateplanInformation.rateplanId === key),
      );
    });
  }
}
```

```js
import { Resolver, ResolveField, Parent } from '@nestjs/graphql';
import { RateplanObjectType } from '../type/rateplan.object-type';
import { RateplanService } from '../service/rateplan.service';
import { RateplanInformationObjectType } from '../type/rateplan-information.object.type';
import { RateplanInformationLoader } from './loader/rateplan-information.loader';
import * as DataLoader from 'dataloader';
import { Loader } from 'nestjs-dataloader';
import { RateplanChildLoader } from './loader/rateplan-child.loader';

@Resolver((of) => RateplanObjectType)
export class RateplanSubResolver {
  constructor(private readonly rateplanService: RateplanService) {}

  @ResolveField((returns) => [RateplanInformationObjectType])
  public async rateplanInformations(
    @Parent() rateplan: RateplanObjectType,
    @Loader(RateplanInformationLoader.name)
    rateplanLoader: DataLoader<RateplanObjectType['id'], RateplanInformationObjectType[]>,
  ): Promise<RateplanInformationObjectType[]> {
    return rateplanLoader.load(rateplan.id);
  }
}
```