#ts #前端 

实战中一个项目需要定义的类型其实并不多，但是在处理数据过程中需要定义很多类型，功能type可以帮助我们减少很多工作，推荐阅读[官方文档](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type)

## `Record<Keys, Type>`

> Released:  
> [2.1](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html#partial-readonly-record-and-pick)

Constructs an object type whose property keys are `Keys` and whose property values are `Type`. This utility can be used to map the properties of a type to another type.

##### [](https://www.typescriptlang.org/docs/handbook/utility-types.html#example-4)Example

```ts
interface CatInfo {

age: number;

breed: string;

}

type CatName = "miffy" | "boris" | "mordred";

const cats: Record<CatName, CatInfo> = {

miffy: { age: 10, breed: "Persian" },

boris: { age: 5, breed: "Maine Coon" },

mordred: { age: 16, breed: "British Shorthair" },

};

cats.boris;
```

## 常见问题
`Element implicitly has an 'any' type because expression of type 'string' can't be used to index`

![[assets/media/Pasted image 20230403211755.png]]
![[assets/media/Pasted image 20230403211733.png]]

