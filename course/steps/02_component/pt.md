# Linkando uma app e utilizando-a no tema da loja

## Introdução
Para desenvolver um bloco de frente de loja, similar aos que oferecemos nativamente no Store Framework, utilizamos a biblioteca de desenvolvimento de UIs **[React.js](https://reactjs.org/)**.

### Um pouco sobre a tecnologia

A unidade básica de desenvolvimento em **React** é o **componente**, onde pode ser implementada a interface visual do componente, como também sua lógica de estado, ou recuperação de dados. Seguindo as recomendações mais modernas de desenvolvimento, iremos focar no uso da [**API de Hooks**](https://reactjs.org/docs/hooks-intro.html) do *React*, não utilizando de *classes* para a construção dos componentes.

No VTEX IO, adotamos [**Typescript**](https://www.typescriptlang.org/) como linguagem padrão para programação *frontend*. Apesar de ser necessário aprender sintaxes novas, o esforço é rapidamente recompensado! Utilizando Typescript, ganha-se alta previsibilidade de *bugs*, por oferecer tipagem estática. Além disso, com as IDEs certas, é possível aumentar a velocidade de implementação através de um *code completion* mais esperto, com a tipagem de objetos no código.

Neste curso, **será utilizado exclusivamente Typescript**. Caso você não tenha familiaridade com a linguagem, será uma excelente oportunidade de experimentá-la!

### Objetivo dessa Etapa
Como você já tem familiaridade com o Store Framework, já sabe que utilizamos blocos, como `shelf` e  `sku-selector`, para a montagem de uma VTEX IO Store. Nesta etapa você irá criar um bloco que será utilizado no tema da *home page* de sua loja.

## Atividade
1. No *template* clonado localmente, abra o arquivo `Countdown.tsx`:

    ```tsx
    //react/Countdown.tsx
    import React from 'react'

    interface CountdownProps {}

    const Countdown: StorefrontFunctionComponent<CountdownProps> = ({}) => {
      return <div></div>
    }

    Countdown.schema = {
      title: 'editor.countdown.title',
      description: 'editor.countdown.description',
      type: 'object',
      properties: {},
    }

    export default Countdown
    ```

2. Para ver o seu componente na *home page*, linke o tema em um terminal e a app em outro terminal. Adicione uma *tag* `h1` dentro do nosso componente e declarar o bloco no tema.
    ```diff
    const Countdown: StorefrontFunctionComponent<CountdownProps> = ({}) => {
    -    return <div></div>
    +    return (
    +      <div>
    +        <h1>Teste Countdown</h1>
    +      </div>
    +    )
    }
    ```

    >Para que o componente seja visto funcionando na loja, é preciso declarar o bloco que a *app* define no tema. Em primeiro lugar, será necessário ter um tema para adicionar a *app*, para isso, será necessário cloná-lo do *Github*. Nesse curso, o `store-theme` será utilizado. Para clonar o repositório, basta executar o seguinte comando:

    ```
    git clone https://github.com/vtex-apps/store-theme.git
    ```

3. Com o repositório clonado, vá ao terminal para deslinkar quaisquer temas ou *apps* que estejam linkados. Para isso, basta digitar o seguinte comando:
    ```
    vtex unlink --all
    ```
4. Com o repositório já clonado, vá até a pasta com `cd store-theme`; linke o tema no seu *workspace*.
    ```
    vtex link
    ```
5. Agora, com o tema linkado, é preciso também linkar a *app*. Para isso, vá até a pasta da *app*, `store-block`, repositório do Github que foi criado quando você iniciou o curso, e faça o *link*.
    ```
    vtex link
    ```

5. Para que a *app* seja utilizada no tema, é preciso adicioná-la às suas dependências, que como visto anteriormente, ficam no `manifest.json`. Dessa forma, adicione ao manifesto do tema, que se encontra na pasta `store-theme`, "vtex.countdown" como dependência. A versão dela está definida no manifesto da *app* (`0.0.1`). Feito isso, o JSON terá mais uma linha, como mostrado abaixo:
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
5. Por fim, é preciso adicionar o bloco na loja. Dentro do arquivo `store-theme/store/blocks/home/home.jsonc`, declare um bloco chamado `"countdown"`. 
    ```
    {
        "store.home": {
            "blocks": [
                "countdown",
                ...
            ]
            ...
        }
        ...
    }
    ```
O resultado esperado é encontrar um *header* na home da sua loja, como a imagem abaixo:

![image](https://user-images.githubusercontent.com/19495917/74960422-11d7d980-53eb-11ea-9d32-f0aa1340f0af.png)

