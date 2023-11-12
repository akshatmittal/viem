---
head:
  - - meta
    - property: og:title
      content: Getting started
  - - meta
    - name: description
      content: Getting started with the OP Stack in Viem
  - - meta
    - property: og:description
      content: Getting started with the OP Stack in Viem
---

# Getting started with OP Stack

Viem provides first-class support for chains implemented on the [OP Stack](https://docs.optimism.io/getting-started-op-stack).

The OP Stack is a set of modular open-source software that enable developers to build fast, secure, and scalable Layer 2 Ethereum protocols & applications. [Read more.](https://docs.optimism.io/getting-started-op-stack)

## Quick Start

### 1. Set up your Client & Transport

Firstly, set up your [Client](/docs/clients/intro) with a desired [Transport](/docs/clients/intro) & [OP Stack Chain](./op-stack/chains.md).

```ts {4-7}
import { createPublicClient, http } from 'viem'
import { base } from 'viem/chains'

const client = createPublicClient({
  chain: base,
  transport: http(),
})
```

::: info
In a production app, it is highly recommended to pass through your authenticated RPC provider URL (Alchemy, Infura, Ankr, etc). If no URL is provided, viem will default to a public RPC provider. [Read more](/docs/clients/transports/http.html#usage).
:::

### 2. Extend Client with the OP Stack

Now that you have a Client set up, you can extend it with OP Stack Actions! [Read more.](./op-stack/client.md)

```ts
import { createPublicClient, http } from 'viem'
import { base } from 'viem/chains'
import { l2PublicActions } from 'viem/op-stack' // [!code hl]

const client = createPublicClient({
  chain: base,
  transport: http(),
}).extend(l2PublicActions()) // [!code hl]
```

### 3. Consume OP Stack Actions

Now that you have an OP Stack Client set up, you can now interact with the OP Stack and consume [Actions](./op-stack/actions/estimateL1Gas.md)!

```tsx
import { createPublicClient, http, parseEther } from 'viem'
import { mainnet } from 'viem/chains'

const client = createPublicClient({
  chain: mainnet,
  transport: http(),
}).extend(l2PublicActions()) 

const l1Gas = await client.estimateL1Gas({ // [!code hl]
  account: '0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266', // [!code hl]
  to: '0x70997970c51812dc3a010c7d01b50e0d17dc79c8', // [!code hl]
  value: parseEther('1') // [!code hl]
}) // [!code hl]
```