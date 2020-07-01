## Passo 3: Implementação das _props_

No arquivo `Countdown.tsx`, é necessário adicionar uma _prop_ chamada `targetDate` e é feita na interface `CountdownProps`. Além disso, essa propriedade será utilizada no componente em si, substituindo o texto do passo anterior.

Por fim, para ser possível alterar essa propriedade no _Site Editor_, é preciso adicioná-la no schema. O resultado final da implementação no arquivo `Countdown.tsx` pode ser visto abaixo:

```tsx
//react/Countdown.tsx
import React from 'react'

interface CountdownProps {
    targetDate: string
}

const Countdown: StorefrontFunctionComponent<CountdownProps> = ({ targetDate }) => {
    return (
        <div>
            <h1>{ targetDate }</h1>
        </div>
    )
}

Countdown.schema = {
    title: 'editor.countdown.title',
    description: 'editor.countdown.description',
    type: 'object',
    properties: {
        targetDate: {
            title: 'Data final',
            description: 'Data final utilizada no contador',
            type: 'string',
            default: null
        }
    },
}

export default Countdown
```