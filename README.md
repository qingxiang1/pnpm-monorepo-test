#### 1、 配置文件

npm 和 yarn workspace 都是配置在 package.json 里的，而 pnpm workspace 是配置在 yaml 文件里的。

#### 2、初始化两个包

```js
 mkdir packages packages/core packages/cli

 cd packages/core

 npm init -y

 cd ../cli

 npm init -y

```

#### 3、在 cli 包添加 core 包为依赖

```js
  pnpm --filter cli add core --workspace
```
--filter 指定在哪个包下执行 add 命令

加上 --workspace 就是从本地查找

#### 4、改下包名，加上 scope

然后根目录执行 pnpm install

#### 5、cli 包下创建 tsconfig.json

```js
  pnpm --filter cli exec npx tsc --init
```

pnpm exec 来执行命令，用 --filter 来指定在哪些包执行命令。

#### 6、编译指定包

```js
  pnpm --filter core exec npx tsc
```

#### 7、修改 cli 包

```js
  // 添加依赖
  pnpm --filter cli add chalk commander
```
增加主文件

#### 8、全部编译

```js
  pnpm -r exec npx tsc
```
 -r 是递归的意思，就是在每个包下执行命令，特定的包下执行命令才需要 --filter

#### 9、执行 cli 命令

```js
pnpm --filter cli exec node ./dist/index.js add 1 2
pnpm --filter cli exec node ./dist/index.js minus 1 2
```

#### 10、发布包

```js
  pnpm add --save-dev -w @changesets/cli prettier-plugin-organize-imports prettier-plugin-packagejson

  npx changeset init
```