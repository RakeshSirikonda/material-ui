# Часто задаваемые вопросы (FAQ)

<p class="description">Столкнулись с особой проблемой? Сначала посмотрите наиболее распространенные ошибки в нашем FAQ.</p>

Если вы все еще не можете найти то, что ищете, вы можете задать вопрос сообществу в [gitter](https://gitter.im/mui-org/material-ui). Для практических и других вопросов, пожалуйста, используйте [StackOverflow](https://stackoverflow.com/questions/tagged/material-ui) вместо вопросов на Github. На StackOverflow существует тег `material-ui`, который вы можете использовать для ваших вопросов.

## Why aren't my components rendering correctly in production builds?

This is likely an n°1 issue that happens due to class name conflicts once your code is in a production bundle. For Material-UI to work, the `clsx` values of all components on a page must be generated by a single instance of the [class name generator](/customization/css-in-js/#creategenerateclassname-options-class-name-generator).

To correct this issue, all components on the page need to be initialized such that there is only ever **one class name generator** between them.

You could end up accidentally using two class name generators in a variety of scenarios:

- You accidentally **bundle** two versions of Material-UI. You might have a dependency not correctly setting Material-UI as a peer dependency.
- You are using `JssProvider` for a **subset** of your React Tree.
- You are using a bundler and it is splitting code in a way results in multiple class name generator instances to be created. > If you are using webpack with the [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/), try configuring the [`runtimeChunk` setting under `optimizations`](https://webpack.js.org/configuration/optimization/#optimization-runtimechunk).

Overall, it's simple to recover from this problem by wrapping each Material-UI application with [`JssProvider`](/customization/css-in-js/#jssprovider) components at the top of their component trees **and using a single class name generator shared between them**.

[A resolution example](/customization/css-in-js/#jssprovider). The last part of any solution will vary based on what bundler you are using, but the overall goal is to ensure the common module that contains the first snippet above only gets loaded and run once.

⚠️ You are in the hurry? Rest assured, we provide an option to make the class names **deterministic** as a quick escape hatch: [`dangerouslyUseGlobalCSS`](/customization/css-in-js/#global-css).

## Why do the fixed positioned elements move when a modal is opened?

We block the scroll as soon as a modal is opened. This prevents interacting with the background when the modal should be the only interactive content, however, removing the scrollbar can make your **fixed positioned elements** move. In this situation, you can apply a global `.mui-fixed` class name to tell Material-UI to handle those elements.

## How can I disable the ripple effect globally?

The ripple effect is exclusively coming from the `BaseButton` component. You can disable the ripple effect globally by providing the following in your theme:

```js
import { createMuiTheme } from '@material-ui/core';

const theme = createMuiTheme({
  props: {
    // Name of the component ⚛️
    MuiButtonBase: {
      // The properties to apply
      disableRipple: true, // No more ripple, on the whole application 
    },
  },
});
```

## How can I disable animations globally?

You can disable animations globally by providing the following in your theme:

```js
import { createMuiTheme } from '@material-ui/core';

const theme = createMuiTheme({
  transitions: {
    // Então temos `transition: none;` everywhere
    create: () => 'none',
  },
});
```

Sometimes you will want to enable this behavior conditionally, for instance during testing or on low-end devices, in these cases, you can dynamically change the theme value.

## Должен ли я использовать JSS для стилизации своего приложения?

Это крайне рекомендуется:

- It comes built in, so carries no additional bundle size overhead.
- It's fast & memory efficient.
- It has a clean, consistent [API](https://cssinjs.org/json-api/).
- It supports a number of advanced features, either natively, or through [plugins](https://cssinjs.org/plugins/).

However perhaps you're adding some Material-UI components to an app that already uses another styling solution, or are already familiar with a different API, and don't want to learn a new one? In that case, head over to the [Style Library Interoperability](/guides/interoperability/) section, where we show how simple it is to restyle Material-UI components with alternative style libraries.

## When should I use inline-style vs classes?

As a rule of thumb, only use inline-style for dynamic style properties. The CSS alternative provides more advantages, such as:

- auto-prefixing
- better debugging
- медиа-запросы
- ключевые кадры

## Как мне использовать react-router?

Мы описали, как использовать [стороннюю библиотеку маршрутизации](/demos/buttons/#third-party-routing-library) с помощью компонента `ButtonBase`. A lot of our interactive components use it internally: `Button`, `MenuItem`, `<ListItem button />`, `Tab`, etc. Вы можете использовать то же решение с ними.

## How do I combine the `withStyles()` and `withTheme` HOCs?

Есть несколько разных вариантов:

**`withTheme` опция:**

```js
export default withStyles(styles, { withTheme: true })(Modal);
```

**`compose()` вспомогательная функция:**

```js
import { compose } from 'recompose';

export default compose(
  withTheme,
  withStyles(styles)
)(Modal);
```

**цепочка необработанных функций:**

```js
export default withTheme(withStyles(styles)(Modal));
```

## Как я могу получить доступ к элементу DOM?

Wrap the component with the [`RootRef`](/api/root-ref/) helper.

## Why are the colors I am seeing different from what I see here?

The documentation site is using a custom theme. Hence, the color palette is different from the default theme that Material-UI ships. Please refer to [this page](/customization/themes/) to learn about theme customization.

## Material-UI is awesome. How can I support the project?

There are many ways to support Material-UI:

- Improve [the documentation](https://github.com/mui-org/material-ui/tree/next/docs).
- Help others to get started.
- [Spread the word](https://twitter.com/MaterialUI).
- Answer questions on [StackOverflow](https://stackoverflow.com/questions/tagged/material-ui) or on [Spectrum](https://spectrum.chat/material-ui).

If you use Material-UI in a commercial project and would like to support its continued development by becoming a **Sponsor**, or in a side or hobby project and would like to become a backer, you can do so through [OpenCollective](https://opencollective.com/material-ui).

All funds raised are managed transparently, and Sponsors receive recognition in the README and on the Material-UI home page.