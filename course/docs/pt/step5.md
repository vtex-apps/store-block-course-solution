## Passo 5: _CSS Handles_

A fim de customizar o bloco, será utilizado um novo _hook_, o `useCssHandles`, de forma a definir o _handle_ utilizado no componente `Countdown`. Além disso, os nomes dos _handles_ serão definidos em um _array_.

Por fim, para utilizá-los, basta colocá-los como classe no componente que é retornado. O resultado final do código pode ser visto abaixo:

```tsx
//react/Countdown.tsx
import React, { useState } from 'react'
import { TimeSplit } from './typings/global'
import { tick } from './utils/time'
import { useCssHandles } from 'vtex.css-handles'

interface CountdownProps {
    targetDate: string
}

const DEFAULT_TARGET_DATE = (new Date('2020-06-25')).toISOString()

const CSS_HANDLES = ['countdown']

const Countdown: StorefrontFunctionComponent<CountdownProps> = ({ targetDate = DEFAULT_TARGET_DATE }) => {
    const [timeRemaining, setTime] = useState<TimeSplit>({
        hours: '00',
        minutes: '00',
        seconds: '00'
    })
    const handles = useCssHandles(CSS_HANDLES)

    tick(targetDate, setTime)

    return (
        <div className={`${handles.countdown} t-heading-2 fw3 w-100 c-muted-1 db tc`}>
          {`${timeRemaining.hours}:${timeRemaining.minutes}:${timeRemaining.seconds}`}
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