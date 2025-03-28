# テーマ tokens

## 型定義

```ts
type ThemeToken = {
  colors: ThemeTokenColor;
  boxShadow: {
    header: string;
    sider: string;
    tab: string;
  };
};
```

::: tip コードの場所
src/typings/app.d.ts
:::

## トークン（tokens）に基づく CSS 変数

初期化時に HTML にいくつかの CSS 変数が生成されます。これらの CSS 変数はテーマトークン（tokens）に基づいて作成されます。

```ts
/** Theme vars */
export const themeVars: App.Theme.ThemeToken = {
  colors: {
    ...colorPaletteVars,
    nprogress: 'rgb(var(--nprogress-color))',
    container: 'rgb(var(--container-bg-color))',
    layout: 'rgb(var(--layout-bg-color))',
    inverted: 'rgb(var(--inverted-bg-color))',
    base_text: 'rgb(var(--base-text-color))'
  },
  boxShadow: {
    header: 'var(--header-box-shadow)',
    sider: 'var(--sider-box-shadow)',
    tab: 'var(--tab-box-shadow)'
  }
};
```

::: tip コードの場所
src/theme/vars.ts
:::

## トークン（tokens）の初期化

```ts
/**
 * Create theme token
 *
 * @param colors Theme colors
 */
export function createThemeToken(colors: App.Theme.ThemeColor) {
  const paletteColors = createThemePaletteColors(colors);

  const themeTokens: App.Theme.ThemeToken = {
    colors: {
      ...paletteColors,
      nprogress: paletteColors.primary,
      container: 'rgb(255, 255, 255)',
      layout: 'rgb(247, 250, 252)',
      inverted: 'rgb(0, 20, 40)',
      base_text: 'rgb(31, 31, 31)'
    },
    boxShadow: {
      header: '0 1px 2px rgb(0, 21, 41, 0.08)',
      sider: '2px 0 8px 0 rgb(29, 35, 41, 0.05)',
      tab: '0 1px 2px rgb(0, 21, 41, 0.08)'
    }
  };

  const darkThemeTokens: App.Theme.ThemeToken = {
    colors: {
      ...themeTokens.colors,
      container: 'rgb(28, 28, 28)',
      layout: 'rgb(18, 18, 18)',
      base_text: 'rgb(224, 224, 224)'
    },
    boxShadow: {
      ...themeTokens.boxShadow
    }
  };

  return {
    themeTokens,
    darkThemeTokens
  };
}
```

::: tip コードの場所
src/store/modules/theme/shared.ts
:::
