# Exemplo: Navegação Completa com Formulário e AsyncStorage

Este exemplo demonstra como criar um fluxo de navegação completo em um app React Native usando [Expo Router](https://docs.expo.dev/router/introduction/), incluindo um formulário simples e persistência de dados com [`AsyncStorage`](https://react-native-async-storage.github.io/async-storage/).

## Funcionalidades

- <img src="assets/bullet.png" width="16" /> Navegação entre telas usando Expo Router (`Stack` e `Tabs`)
- <img src="assets/bullet.png" width="16" /> Formulário para entrada de dados do usuário (ex: nome e email)
- <img src="assets/bullet.png" width="16" /> Salvamento dos dados do formulário localmente usando AsyncStorage
- <img src="assets/bullet.png" width="16" /> Recuperação dos dados salvos ao abrir o app

## Estrutura de Pastas

```
app/
  _layout.tsx
  index.tsx           # Tela inicial
  formulario.tsx      # Tela do formulário
  perfil.tsx          # Tela de perfil (exibe dados salvos)
components/
  Formulario.tsx      # Componente de formulário reutilizável
hooks/
  useAsyncStorage.ts  # Hook customizado para AsyncStorage
```

## Exemplo de Uso

1. O usuário acessa a tela inicial e navega para o formulário.
2. Preenche os campos e salva.
3. Os dados são armazenados usando AsyncStorage.
4. Na tela de perfil, os dados salvos são exibidos.

## Instalação

```sh
npm install @react-native-async-storage/async-storage
```

## Exemplo de Hook para AsyncStorage

````typescript
// hooks/useAsyncStorage.ts
import AsyncStorage from '@react-native-async-storage/async-storage';

export function useAsyncStorage(key: string) {
  const getItem = async () => {
    const value = await AsyncStorage.getItem(key);
    return value ? JSON.parse(value) : null;
  };

  const setItem = async (value: any) => {
    await AsyncStorage.setItem(key, JSON.stringify(value));
  };

  return { getItem, setItem };
}
