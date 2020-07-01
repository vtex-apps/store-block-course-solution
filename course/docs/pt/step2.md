## Passo 2: Componente
Em primeiro lugar, é necessário alterar o arquivo `Countdown.tsx`. Será adicionado um header com um texto em específico para que seja possível ver o bloco na _home page_ do tema.


```tsx
//react/Countdown.tsx
import React from 'react'

interface CountdownProps {}

const Countdown: StorefrontFunctionComponent<CountdownProps> = ({}) => {
    return (
        <div>
            <h1>Teste Countdown</h1>
        </div>
    )
}

Countdown.schema = {
    title: 'editor.countdown.title',
    description: 'editor.countdown.description',
    type: 'object',
    properties: {},
}

export default Countdown
```

Agora, com as alterações feitas no repositório correspondente ao bloco customizado que estamos criando, é necessário adicionar esse bloco em um tema em específico, para que possamos vê-lo. Para tanto, com o repositório do `store-theme` clonado, a fim de evitar conflitos entre possíveis temas instalados no workspace utilizado, é necessário fazer um _unlink_ de tudo:

```
vtex unlink --all
```

Com o workspace "limpo", iremos linkar o `store-theme` e também o `store-block`. Ou seja, temos dois _links_ ativos, um em cada terminal, como pode ser visto na figura abaixo:
![image](https://user-images.githubusercontent.com/19495917/86256364-a1a64500-bb8e-11ea-8f05-263efcb581ad.png)


Por fim, para inserir o bloco no tema, é necessário ir ao arquivo `store/home.jsonc` no repositório do `store-theme` e adicionar o bloco `countdown`:
```diff
{
    ...
    "dependencies": {
        ...
+        "vtex.countdown": "0.x",
        ...
    },
    ...
}
```

O resultado esperado é encontrar um *header* na home da sua loja, como a imagem abaixo:

![image](https://user-images.githubusercontent.com/19495917/74960422-11d7d980-53eb-11ea-9d32-f0aa1340f0af.png)

