## Passo 6: _Messages_

Você já deve ter aprendido a usar o nosso **builder _messages_**, e será através dele que serão adicionadas _strings_ internacionalizadas nos componentes.

1. Para isso, **na pasta `/messages`**, adicione agora uma mensagem de **título para o componente**:

   `messages/pt.json`

   ```diff
   {
     ...,
   +  "countdown.title": "Contagem Regressiva"
   }
   ```

   `messages/en.json`

   ```diff
   {
     ...,
   +  "countdown.title": "Countdown"
   }
   ```

   `messages/es.json`

   ```diff
   {
     ...,
   +  "countdown.title": "Cuenta Regresiva"
   }
   ```

   `messages/context.json`

   ```diff
   {
     ...,
   +  "countdown.title": "Countdown"
   }
   ```

2. Feito isso, para **renderizar o título** deve-se usar o componente `FormattedMessage` da biblioteca [react-intl](https://github.com/formatjs/react-intl).

   > A biblioteca _react-intl_ dá suporte a várias maneiras de configuração e internacionalização, vale a pena verificá-las.

3. Adicione a biblioteca usando `yarn add react-intl` na pasta _react_
4. No código do seu componente `Countdown.tsx` **importe o FormattedMessage**
   ```diff
   //react/Countdown.tsx
   +  import { FormattedMessage } from 'react-intl'
   ```
5. Adicione uma constante que será o seu título:
   ```tsx
   //react/Countdown.tsx
   const titleText = title || <FormattedMessage id="countdown.title" />
   ```
6. Agora, junte o título e o contador para renderizá-los. Para isso, defina um container por fora. Além disso, o texto do título será passado através da _prop_ `title`:

   ```tsx
   //react/Countdown.tsx
   const Countdown: StorefrontFunctionComponent<CountdownProps> = ({
     title,
     targetDate,
   }) => {
     const [timeRemaining, setTime] = useState<TimeSplit>({
       hours: '00',
       minutes: '00',
       seconds: '00',
     })

     const titleText = title || <FormattedMessage id="countdown.title" />
     const handles = useCssHandles(CSS_HANDLES)

     tick(targetDate, setTime)

     return (
       <div className={`${handles.container} t-heading-2 fw3 w-100 c-muted-1`}>
         <div className={`${handles.title} db tc`}>{titleText}</div>
         <div className={`${handles.countdown} db tc`}>
           {`${timeRemaining.hours}:${timeRemaining.minutes}:${timeRemaining.seconds}`}
         </div>
       </div>
     )
   }
   ```

   Note que são utilizados três _handles_ **novos**: _container_, _countdown_ e _title_. Dessa forma, lembre-se de declará-los na constante `CSS_HANDLES`, vista na etapa anterior:

   ```tsx
   //react/Countdown.tsx
   const CSS_HANDLES = ["container", "countdown", "title"]
   ```

7. Por fim, é preciso adicionar a _prop_ de `title` no _schema_:
   ```diff
   //react/Countdown.tsx
   Countdown.schema = {
     title: 'editor.countdown.title',
     description: 'editor.countdown.description',
     type: 'object',
     properties: {
   +   title: {
   +     title: 'Sou um título',
   +     type: 'string',
   +     default: null,
   +   },
       targetDate: {
         title: 'Data final',
         description: 'Data final usada no contador',
         type: 'string',
         default: null,
       },
     },
   }
   ```