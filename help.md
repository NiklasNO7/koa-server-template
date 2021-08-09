# `node`+`Typescript`+`koa`开发环境搭建

1. ## 需引入的第三方库

   ```powershell
   yarn add typescript ts-node nodemon -D
   ```

   1. `ts-node`:对指定入口`ts`文件进行编译，并执行；
   2. `nodemon`:监听指定目录下文件的改动，当文件发生变动时重新启动程序；

2. ## `Typescript`配置文件

   ```powershell
   tsc --init
   ```

   初始化`tsconfig.json`，当`ts`编译时会根据里面的配置进行编译，基本配置如下：

   ```json
   {
     "compilerOptions": {
       "target": "es5", /* 解析结果 */
       "module": "commonjs", /* 遵循的模块化规范 */
       "strict": true,
       "esModuleInterop": true, /* 支持以import xx from ‘xx’格式引入 */
       "skipLibCheck": true,/* 跳过声明文件的类型检查 */
       "forceConsistentCasingInFileNames": true /* 禁止对同一个文件的不一致的引用 */
     },
     "include": [
       "src/**/*"
     ],/* 指定需要编译的目录范围 */
     "exclude": ["node_modules"] /* 忽略类型检查的目录 */
   }
   ```

   更过详细的配置可以查看官网：https://www.tslang.cn/docs/handbook/tsconfig-json.html

3. ## `package.json`脚本

   ```json
   "scripts": {
       "build": "tsc",
       "start": "tsc dist/index.ts",
       "dev": "nodemon --watch src -e ts,tsx --exec ts-node src/index.ts"
     }
   ```

   "`dev`":

   1. `--watch src`:监听`src`目录下文件变化；
   2. `-e ts`:只监听后缀为`ts`的文件；
   3. `--exec`:执行命令

4. ## 引入`koa`

   ```powershell
   yarn add koa
   ```

   启动一个简单服务

   ```typescript
   import Koa from "koa";
   
   const app = new Koa();
   
   app.use(async (ctx) => {
     ctx.body = "Hello World";
   });
   
   app.listen(3000);
   ```

至此，一个简易的开发环境便搭建完成了。

