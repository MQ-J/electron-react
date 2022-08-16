# Manual

- [passando variáveis do main para o renderer](#passando-variáveis-do-main-para-o-renderer)

## passando variáveis do main para o renderer

1. No arquivo **main/preload.ts** você cria as funções que usarão informações do sistema operacional.

```javascript
contextBridge.exposeInMainWorld('electron', {
  system: process.platform, //informa o sistema operacional
});
```

2. **renderer/preload.d.ts** existe pois estamos usando Typescript. É onde se criam as interfaces das funções que você criou no preload.ts

```javascript
declare global {
  interface Window {
    electron: {
      system: string; //a resposta é uma string
    };
  }
}
```

3. Pronto, pode usar a infomação em seus componentes do React, como mostra este exemplo no **App.tsx**:

```javascript
const Hello = () => {
  return (
    <p>{window.electron.system}</p> //retorna win32, caso seja windows
  );
};
```
