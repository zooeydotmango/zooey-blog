---
date created: Monday, February 20th 2023, 7:07:06 pm
date modified: Monday, March 6th 2023, 12:29:59 pm
---
#vue/vue3  #ts #vite #前端

# vue3

## Props

props经过definePorps接受的本身就是响应式的，即使是异步的props数据也可以watch接受到变化

props是只读的，如果出现了对props进行修改的行为，大概有两种情况：
1. props作为初始值，子组件需要对这个值进行操作，建议定义新的局部属性承载
2. 需要对props的值做仅供显示的修改，可以用computed承载

props的类型提示，推荐`definePorps<XXProps>()`的方式直接获取，但是注意这个ts接口不能是从外部引入的

props的默认值设置：

```ts
export interface Props {
  msg?: string
  labels?: string[]
}

const props = withDefaults(defineProps<Props>(), {
  msg: 'hello',
  labels: () => ['one', 'two']
})

```

如果父组件要传的props比较多可以合为一个对象通过v-bind传播

## 单组件

## Typescript

### 基础类型的写法：String-》string，全小写即可

### 数字类型的写法：`string[]`或者`Array<string>`，后面的写法基于泛型

### 对象/接口定义

```ts
type TypeUser={

}

interface InterfaceUser {

}
```
interface更接近object，对象的类型定义需要Upper Camel Case写法。
```ts
interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  friendList: UserItem[]
}

// 这里继承了 UserItem 的所有属性类型，并追加了一个权限等级属性
interface Admin extends UserItem {
  permissionLevel: number
}

const admin: Admin = {
  name: 'Petter',
  age: 18,
  enjoyFoods: ['rice', 'noodle', 'pizza'],
  friendList: [
    {
      name: 'Marry',
      age: 16,
      enjoyFoods: ['pizza', 'ice cream'],
      friendList: [],
    },
    {
      name: 'Tom',
      age: 20,
      enjoyFoods: ['chicken', 'cake'],
      friendList: [],
    }
  ],
  permissionLevel: 1,
}

```
如果在继承过程中想要去掉一些类型可以使用Omit
```ts
type Omit<T, K extends string | number | symbol>

interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  friendList?: UserItem[]
}

// 这里在继承 UserItem 类型的时候，删除了两个多余的属性
interface Admin extends Omit<UserItem, 'enjoyFoods' | 'friendList'> {
  permissionLevel: number
}

// 现在的 admin 就非常精简了
const admin: Admin = {
  name: 'Petter',
  age: 18,
  permissionLevel: 1,
}

```

### 类

ts中，类的类型就是类本身
```ts
// 定义一个类
class User {
  // constructor 上的数据需要先这样定好类型
  name: string

  // 入参也要定义类型
  constructor(userName: string) {
    this.name = userName
  }

  getName() {
    console.log(this.name)
  }
}

// 通过 new 这个类得到的变量，它的类型就是这个类
const petter: User = new User('Petter')
petter.getName() // Petter

```
类可以继承类
```ts
// 这是一个基础类
class UserBase {
  name: string
  constructor(userName: string) {
    this.name = userName
  }
}

// 这是另外一个类，继承自基础类
class User extends UserBase {
  getName() {
    console.log(this.name)
  }
}

// 这个变量拥有上面两个类的所有属性和方法
const petter: User = new User('Petter')
petter.getName()

```
接口也可以继承类
```ts
// 这是一个接口，可以继承自类
interface User extends UserBase {
  age: number
}

// 这样这个变量就必须同时存在两个属性
const petter: User = {
  name: 'Petter',
  age: 18,
}
```

### 函数

```ts
// 写法一：函数声明
function sum1(x: number, y: number): number {
  return x + y
}

// 写法二：函数表达式
const sum2 = function(x: number, y: number): number {
  return x + y
}

// 写法三：箭头函数
const sum3 = (x: number, y: number): number => x + y

// 写法四：对象上的方法
const obj = {
  sum4(x: number, y: number): number {
    return x + y
  }
}
// 没有返回值的函数，`void` 和 `null` 、 `undefined`不能混用
function sayHi(name: string): void { console.log(`Hi, ${name}!`) }
```
异步函数的返回值是`Promise<T>`，最终函数返回的值的类型就是T
```ts
// 注意这里的返回值类型
function queryData(): Promise<string> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Hello World')
    }, 3000)
  })
}

queryData().then((data) => console.log(data))

```

### Ts问题场景

![[assets/media/Pasted image 20230302192447.png]]  
![[assets/media/Pasted image 20230302192459.png]]

## Vite

- vite插件：mock、vueJsx
