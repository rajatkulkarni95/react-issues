# [React 19] Can't use useActionState (NextJS)

> Issue #29017 - Created on 5/8/2024

> Original URL: https://github.com/facebook/react/issues/29017

## Description

I get this error, trying to useActionState in React19 and NextJS, I followed the documentation and tried using several approaches, but none worked, here's the code and the React Version below

![image](https://github.com/facebook/react/assets/62437672/4185fa8f-73c6-4470-8267-efefff020781)


```
"use client";

import { useActionState } from "react";
import * as S from "./styles";

interface PurchaseFormProps {
	priceId: string;
}

export function PurchaseForm({ priceId }: PurchaseFormProps): JSX.Element {
	const [state, formAction] = useActionState(() => {}, null);

	return (
		<form className={S.form}>
			<button className={S.formButton} type="submit" disabled={true}>
				Comprar agora
			</button>
		</form>
	);
}

```

`
    "react": "^19.0.0-beta-e7d213dfb0-20240507",
    "react-dom": "^19.0.0-beta-1beb73de0f-20240503",
`
