## Passo 4: Implementação do contador

Nesse passo, será necessária a utilização de um _hook_ de atualizaçõa de estado, o `useState`. Além disso, uma data padrão será adicionada, em caso dela não ser definida no _Site Editor_ e, por fim, utilizaremos algumas funções que já estão implementadas para fazer a contagem em si.

> A formatação da *string* do contador está no formato `HH:MM:SS`, feita através do *split* em `hours`, `minutes` e `seconds`.

Abaixo, você encontra o código final do bloco do contador:

```tsx
//react/Countdown.tsx
import React, { useState } from 'react'
import { TimeSplit } from './typings/global'
import { tick } from './utils/time'

interface CountdownProps {
    targetDate: string
}

const DEFAULT_TARGET_DATE = (new Date('2020-06-25')).toISOString()

const Countdown: StorefrontFunctionComponent<CountdownProps> = ({ targetDate = DEFAULT_TARGET_DATE }) => {
    const [timeRemaining, setTime] = useState<TimeSplit>({
        hours: '00',
        minutes: '00',
        seconds: '00'
    })

    tick(targetDate, setTime)

    return (
        <div>
            <h1>{ `${timeRemaining.hours}:${timeRemaining.minutes}:${timeRemaining.seconds}` }</h1>
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

