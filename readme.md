## 开发工具介绍

1. babel-eslint：这个包让你可以轻松在 Babel 上使用 lint。如果你不使用 ESLint 尚不支持的 Flow 或实验性功能，则不一定需要这个插件。

2. eslint：这是 lint 代码所需的主要工具。

3. eslint-config-airbnb：这个包提供了所有 Airbnb 的 ESLint 配置，你可以修改它们。

4. eslint-plugin-babel：babel-eslint 的插件伴侣。

5. eslint-plugin-import：这个插件旨在支持 ES2015+（ES6+）的导入 / 导出语法，并防止出现拼写错误的文件路径和导入名称。

6. eslint-plugin-jsx-a11y：适用于 JSX 元素可访问性规则的 linting 规则。

7. eslint-plugin-prettier：让 ESLint 与 Prettier 的使用更顺畅。

8. eslint-plugin-react：特定于 React 的 linting 规则。

9. eslint-config-jest-enzyme：用于特定于 React 和 Enzyme 的全局变量。这个 lint 配置让 ESLint 知道有哪些全局变量，并且不会针对它们发出警告——有点像断言 it 和 describe。

10. eslint-plugin-jest：Jest 的 ESLint 插件。

11. husky：在自动化部分会进行更多介绍。

12. lint-staged：在自动化部分会进行更多介绍。

## husky

> [husky](https://github.com/typicode/husky)是一个 Git 钩子，你可以在提交代码前或在将代码推送到分支时执行某些特定的操作。

1. 安装 husky

   ```shell
   yarn add --dev husky
   ```

2. package.json 中添加配置

   ```json
    "husky": {
      "hooks": {
        "pre-commit": "lint-staged",
        "pre-push": "YOUR_COMMAND_HERE"
      }
    },
   ```

   每次在提交或推送代码时，它都会执行某个脚本或命令——比如运行测试用例或格式化代码。

## lint-staged

> [lint-staged](https://github.com/okonet/lint-staged) 可以在暂存（Git staged）文件上运行 linter，这样就不会将错误的代码推送到分支上。

1. 安装 lint-staged

   ```shell
    yarn add --dev lint-staged
   ```

2. package.json 配置

   ```json
    "lint-staged": {
      "*.(js|jsx)": ["npm run lint:write", "git add"]
    },
   ```

   这段配置的意思是先运行 lint:write 命令，然后将文件添加到暂存区域。它仅针对.js 和.jsx 文件运行这个命令，但你也可以根据需要针对其他文件运行这个命令。

3. 每当你提交代码时：

   ```shell
    $ git add .
    $ git commit -m "代码被commit之前都会执行lint-staged命令"
   ```

   它将根据.eslintrc.js 文件的所有规则对代码进行 lint 和格式化。有了这个，你就可以确保没有坏代码被推到生产环境中。
