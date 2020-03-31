## Validation of forms with unform and Yup

- `yarn add @rocketseat/unform`

- `yarn add yup`

```js
import { Form, Input } from "@rocketseat/unform";
import * as Yup from "yup";

const schema = Yup.object().shape({
  name: Yup.string().required('O nome completo é obrigatório'),
  email: Yup.string()
    .email('Insira um e-mail válido')
    .required('O e-mail é obrigatório'),
  password: Yup.string()
    .min(6, 'A senha deve conter no mínimo 6 caracteres')
    .required('A senha é obrigatória'),
});

<Form schema={schema} onSubmit={handleSubmit}>
  <Input name="name" type="text" placeholder="Nome completo" />
  <Input name="email" type="email" placeholder="Seu e-mail" />
  <Input name="password" type="password" placeholder="Sua senha" />

  <button type="submit">Enviar</button>
</Form>;
```
