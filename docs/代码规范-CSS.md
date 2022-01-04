# CSS 规范

## 1、命名规范

---

**抽象模块或者公共组件样式采用 BEM(block-element-modifier)命名规范。**  
BEM 缺点是命名方式太长，看上去不太优雅；但是又是一个简单又非常有用的命名约定，可以让前端代码更容易阅读和理解，更容易协作，更容易控制，更加健壮和明确，而且更加严密。

- block: doraemon
- element: face、hand、footer
- modifier: eye、mouth、nose、finger、toe
- 命名方法：block\_\_element-modifer

```html
<template>
  <section>
    <div class="doraemon">
      <div class="doraemon__face">
        <span class="doraemon__face-eye"></span>
        <span class="doraemon__face-mouth"></span>
        <span class="doraemon__face-nose"></span>
      </div>
      <div class="doraemon__hand">
        <span class="doraemon__hand-finger"></span>
      </div>
      <div class="doraemon__footer">
        <span class="doraemon__footer-toe"></span>
      </div>
    </div>
  </section>
</template>
```

```html
<style lang="scss" scoped>
  .doraemon {
    .doraemon__face {
      .doraemon__face-eye {
      }
      .doraemon__face-mouth {
      }
      .doraemon__face-nose {
      }
    }
    /* 或者使用 @root */
    @at-root #{&}__face {
      @at-root #{&}-eye {
      }
    }
    .doraemon__hand {
      .doraemon__hand-finger {
      }
    }
    .doraemon__footer {
      .doraemon__footer-toe {
      }
    }
  }
</style>
```

## 2、公共 CSS

- 2.2 代码格式化、2.3 代码易读性基本根据指引，安装 Prettier 插件以及设置 ESlint 即可在保存代码时按项目标准自动格式化。

### 2.1 公共样式文件

#### 2.1.1 charset 规则

**样式文件必须写上 @charset 规则，并且一定要在样式文件的第一行首个字符位置开始写，编码名用 “UTF-8”。**

- 推荐：

```css
@charset "UTF-8";
.box {
}
```

- 不推荐：

```css
/* @charset规则不在文件首行首个字符开始 */
@charset "UTF-8";
.box {
}

/* @charset规则没有用小写 */
@charset "UTF-8";
.box {
}

/* 无@charset规则 */
.box {
}
```

#### 2.1.2 样式复用

公共样式在 src/common/cssBundle 目录统一管理，添加公共样式需要按照约定的规则添加：

- vars.scss: scss 全局变量。
- reset.scss: 重置全局默认样式。
- reset-mand.scss: 重置 mand-mobile 样式。
- atomic.scss: 公共原子 CSS，可组合使用实现样式。
- public.scss: 公共 CSS，放置全局样式。

### 2.2 代码格式化

样式书写一般有两种：一种是紧凑格式 （Compact），一种是展开格式（Expanded）。

- 推荐：展开格式（Expanded）

```css
.box {
  display: block;
  width: 50px;
}
```

- 不推荐：紧凑格式 （Compact）

```html
.box { display: block; width: 50px; }
```

### 2.3 代码易读性

1. 左括号与类名之间一个空格，冒号与属性值之间一个空格。

- 推荐：

```css
.box {
  width: 100%;
}
```

- 不推荐：

```javascript
.box{
    width:100%;
}
```

2. 逗号分隔的取值，逗号之后一个空格。

- 推荐：

```css
.box {
  box-shadow: 1px 1px 1px #333, 2px 2px 2px #ccc;
}
```

- 不推荐：

```javascript
.box {
  box-shadow: 1px 1px 1px #333,2px 2px 2px #ccc;
}
```

3. 为单个 CSS 选择器或新声明开启新行。

- 推荐：

```css
.block,
.block__header,
.block__footer {
  color: #ff0;
}

.nav {
  color: #fff;
}
```

4. 属性值十六进制数值能用简写的尽量用简写。

- 推荐：

```css
.box {
  color: #fff;
}
```

- 不推荐：

```css
.box {
  color: #ffffff;
}
```

5. 不要为 0 指明单位。

- 推荐：

```css
.box {
  margin: 0 10px;
}
```

- 不推荐：

```css
.box {
  margin: 0px 10px;
}
```

6. 属性书写建议
   建议遵循以下顺序：

- 布局定位属性：display / position / float / clear / visibility / overflow
- 自身属性：width / height / margin / padding / border / background
- 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
- 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background: linear-gradient …

7. CSS3 浏览器私有前缀
   CSS3 浏览器私有前缀在前，标准写法在后。
   利用 postcss-loader 可以在 webpack 打包时自动添加前缀，开发时可忽略，只写标准写法即可。

```css
.box {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -o-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```

### 2.4 全局污染

页面样式为防止全局污染，**请在 style 标签上加上 scoped 属性。**
