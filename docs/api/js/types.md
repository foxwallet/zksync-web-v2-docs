# Types

All the types which are used in the SDK are referenced here:

```typescript
import { BytesLike, BigNumberish, providers } from "ethers";

// 0x-prefixed, hex encoded, ethereum account address
export type Address = string;
// 0x-prefixed, hex encoded, ECDSA signature.
export type Signature = string;

// Ethereum network
export enum Network {
  Mainnet = 1,
  Ropsten = 3,
  Rinkeby = 4,
  Goerli = 5,
  Localhost = 9,
}

export enum PriorityQueueType {
  Deque = 0,
  HeapBuffer = 1,
  Heap = 2,
}

export enum PriorityOpTree {
  Full = 0,
  Rollup = 1,
}

export enum TransactionStatus {
  NotFound = "not-found", // transaction has not been submitted to zkSync node
  Processing = "processing", // transaction is in the mempool
  Committed = "committed", // transaction has been committed
  Finalized = "finalized", // transaction has been verified
}

export type Eip712Meta = {
  feeToken?: Address;
  ergsPerStorage?: BigNumberish;
  ergsPerPubdata?: BigNumberish;
  withdrawToken?: Address;
  factoryDeps?: BytesLike[];
};

// prettier-ignore
export type BlockTag =
    | number
    | string // hex number
    | 'committed'
    | 'finalized'
    | 'latest'
    | 'earliest'
    | 'pending';

export interface Token {
  address: Address;
  name: string;
  symbol: string;
  decimals: number;
}

export interface EventFilter {
  topics?: Array<string | Array<string> | null>;
  address?: Address | Array<Address>;
  limit?: number;
  fromBlock?: BlockTag;
  toBlock?: BlockTag;
  blockHash?: string;
}

export interface TransactionResponse extends providers.TransactionResponse {
  waitFinalize(): Promise<providers.TransactionReceipt>;
}

export type TransactionRequest = providers.TransactionRequest & { customData?: Eip712Meta };

export interface PriorityOpResponse extends TransactionResponse {
  waitL1Commit(confirmation?: number): Promise<providers.TransactionReceipt>;
}
```
