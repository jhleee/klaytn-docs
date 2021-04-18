# caver.contract <a id="caver-contract"></a>

The `caver.contract` object makes it easy to interact with smart contracts on the Klaytn blockchain platform. When you create a new contract object, you have to provide the JSON interface for that smart contract and caver-js will automatically convert all calls with the contract object in javascript into low-level ABI calls over RPC for you.

이를 통해 스마트 컨트랙트가 마치 자바스크립트 객체인 것처럼 스마트 컨트랙트와 상호작용할 수 있습니다.

## caver.contract.create <a id="caver-contract-create"></a>

```javascript
caver.contract.create(jsonInterface [, address] [, options])
```
JSON 인터페이스 오브젝트에 정의된 모든 메소드 및 이벤트로 새 컨트랙트 인스턴스를 생성합니다. This function works the same as [new caver.contract](#new-contract).

**NOTE** `caver.contract.create` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

See the [new caver.contract](#new-contract).

**리턴값**

See the [new caver.contract](#new-contract).


**예시**

```javascript
const contract = caver.contract.create([
    {
        constant: true,
        inputs: [{ name: 'interfaceId', type: 'bytes4' }],
        name: 'supportsInterface',
        outputs: [{ name: '', type: 'bool' }],
        payable: false,
        stateMutability: 'view',
        type: 'function',
    },
    ...
  ], '0x{address in hex}')
```

## caver.contract <a id="new-contract"></a>

```javascript
new caver.contract(jsonInterface [, address] [, options])
```
JSON 인터페이스 오브젝트에 정의된 모든 메소드 및 이벤트로 새 컨트랙트 인스턴스를 생성합니다.

**매개변수**

| 명칭            | 타입     | 설명                                                                                        |
| ------------- | ------ | ----------------------------------------------------------------------------------------- |
| jsonInterface | object | 컨트랙트를 인스턴스화하기 위한 JSON 인터페이스                                                               |
| address       | 문자열    | (선택 사항) 호출할 스마트 컨트랙트의 주소. `myContract.options.address = '0x1234..'`를 사용하여 나중에 추가할 수 있습니다. |
| options       | object | (선택 사항) 컨트랙트 옵션. 자세한 내용은 아래 표를 참조하세요.                                                     |

옵션 개체에는 다음이 포함됩니다:

| 명칭            | 타입      | 설명                                                                                                                                                                                                                                                                                                 |
| ------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| from          | 문자열     | (선택 사항) 트랜잭션이 만들어진 송신자 주소.                                                                                                                                                                                                                                                                         |
| gasPrice      | 문자열     | (선택 사항) 트랜잭션에 사용할 peb 단위의 가스 가격.                                                                                                                                                                                                                                                                   |
| gas           | number  | (선택 사항) 트랜잭션에 규정된 최대 가스 (가스 제한).                                                                                                                                                                                                                                                                   |
| data          | 문자열     | (선택 사항) 컨트랙트의 바이트 코드. 컨트랙트가 배포될 때 사용됩니다.                                                                                                                                                                                                                                                           |
| feeDelegation | boolean | (optional) Whether to use fee delegation transaction.                                                                                                                                                                                                                                              |
| feePayer      | 문자열     | (optional) The address of the fee payer paying the transaction fee. When `feeDelegation` is `true`, the value is set to the `feePayer` field in the transaction.                                                                                                                                   |
| feeRatio      | 문자열     | (optional) The ratio of the transaction fee the fee payer will be burdened with. If `feeDelegation` is `true` and `feeRatio` is set to a valid value, a partial fee delegation transaction is used. The valid range of this is between 1 and 99. The ratio of 0, or 100 and above are not allowed. |

**리턴값**

| 타입     | 설명                         |
| ------ | -------------------------- |
| object | 모든 메소드와 이벤트가 있는 컨트랙트 인스턴스. |


**예시**

```javascript
const myContract = new caver.contract([...], '0x{address in hex}', { gasPrice: '25000000000' })
```

## myContract.options <a id="mycontract-options"></a>

```javascript
myContract.options
```

컨트랙트 인스턴스에 대한 `options` 객체. `from`, `gas`, `gasPrice`, `feePayer` and `feeRatio` are used as fallback values when sending transactions.

**속성**

| 명칭            | 타입      | 설명                                                                                                                                                                                                                                                                                                 |
| ------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| address       | 문자열     | 컨트랙트가 배포된 주소.                                                                                                                                                                                                                                                                                      |
| jsonInterface | 배열      | 컨트랙트의 JSON 인터페이스.                                                                                                                                                                                                                                                                                  |
| from          | 문자열     | The default address from which the contract deployment/execution transaction is sent. If the `from` address is not defined when creating the transaction, this `myContract.options.from` is always used to create the transaction.                                                                 |
| gasPrice      | 문자열     | 트랜잭션에 사용할 peb 단위의 가스 가격.                                                                                                                                                                                                                                                                           |
| gas           | number  | 트랜잭션에 제공된 최대 가스 (가스 제한).                                                                                                                                                                                                                                                                           |
| data          | 문자열     | 컨트랙트의 바이트 코드. 컨트랙트가 배포될 때 사용됩니다.                                                                                                                                                                                                                                                                   |
| feeDelegation | boolean | (optional) Whether to use fee delegation transaction.                                                                                                                                                                                                                                              |
| feePayer      | 문자열     | (optional) The address of the fee payer paying the transaction fee. When `feeDelegation` is `true`, the value is set to the `feePayer` field in the transaction.                                                                                                                                   |
| feeRatio      | 문자열     | (optional) The ratio of the transaction fee the fee payer will be burdened with. If `feeDelegation` is `true` and `feeRatio` is set to a valid value, a partial fee delegation transaction is used. The valid range of this is between 1 and 99. The ratio of 0, or 100 and above are not allowed. |

**NOTE** `feeDelegation`, `feePayer` and `feeRatio` are supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).


**예시**

```javascript
> myContract.options
{
  address: [Getter/Setter],
  jsonInterface: [Getter/Setter],
  from: [Getter/Setter],
  feePayer: [Getter/Setter],
  feeDelegation: [Getter/Setter],
  feeRatio: [Getter/Setter],
  gasPrice: [Getter/Setter],
  gas: [Getter/Setter],
  data: [Getter/Setter]
}

> myContract.options.from = '0x1234567890123456789012345678901234567891' // default from address
> myContract.options.gasPrice = '25000000000000' // default gas price in peb
> myContract.options.gas = 5000000 // provide as fallback always 5M gas
> myContract.options.feeDelegation = true // use fee delegation transaction
> myContract.options.feePayer = '0x1234567890123456789012345678901234567891' // default fee payer address
> myContract.options.feeRatio = 20 // default fee ratio when send partial fee delegation transaction
```


## myContract.options.address <a id="mycontract-options-address"></a>

```javascript
myContract.options.address
```

이 컨트랙트 인스턴스 `myContract`에 사용된 주소. All transactions generated by caver-js from this contract will contain this address as the `to` of the transaction.

**속성**

| 명칭      | 타입                   | 설명                                      |
| ------- | -------------------- | --------------------------------------- |
| address | string &#124; `null` | 이 컨트랙트의 주소이거나, 아직 설정되지 않은 경우 `null`입니다. |

**예시**

```javascript
>  myContract.options.address
'0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae'

// set a contract address
>  myContract.options.address = '0x1234FFDD...'
```

## myContract.options.jsonInterface <a id="mycontract-options-jsoninterface"></a>

```javascript
myContract.options.jsonInterface
```
이 컨트랙트 `myContract`의 ABI에서 파생된 JSON 인터페이스 객체.

**속성**

| 명칭            | 타입 | 설명                                                         |
| ------------- | -- | ---------------------------------------------------------- |
| jsonInterface | 배열 | 이 컨트랙트의 JSON 인터페이스. 이를 재설정하면 컨트랙트 인스턴스의 메소드 및 이벤트가 재생성됩니다. |


**예시**

```javascript
> myContract.options.jsonInterface
[
  {
    constant: true,
    inputs: [ { name: 'interfaceId', type: 'bytes4' } ],
    name: 'supportsInterface',
    outputs: [ { name: '', type: 'bool' } ],
    payable: false,
    stateMutability: 'view',
    type: 'function',
    signature: '0x01ffc9a7',
  },
  ...
  {
    anonymous: false,
    inputs: [
      { indexed: true, name: 'owner', type: 'address' },
      { indexed: true, name: 'spender', type: 'address' },
      { indexed: false, name: 'value', type: 'uint256' }
    ],
    name: 'Approval',
    type: 'event',
    signature: '0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925',
  },
]

// set a new jsonInterface
> myContract.options.jsonInterface = [...]
```


## myContract.clone <a id="mycontract-clone"></a>

```javascript
myContract.clone([contractAddress])
```

현재 컨트랙트 인스턴스를 복제합니다.

**매개변수**

| 명칭              | 타입     | 설명                                                                                                                                                   |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| contractAddress | String | (optional) The address of the new contract. If omitted, it will be set to the address in the original instance (e.g., `myContract.options.address`). |

**리턴값**

| 타입     | 설명                |
| ------ | ----------------- |
| object | 새로 복제된 컨트랙트 인스턴스. |


**예시**

```javascript
> myContract.clone()
Contract {
  currentProvider: [Getter/Setter],
  ...
  _keyrings: KeyringContainer { ... }
}
```

## myContract.deploy <a id="mycontract-deploy2"></a>

```javascript
myContract.deploy(options, byteCode [, param1 [, param2 [, ...]]])
```

Deploys the contract to the Klaytn network. After a successful deployment, the promise will be resolved with a new contract instance. Unlike the usability of the existing [myContract.deploy](#mycontract-deploy) function, this function sends a transaction directly to the Klaytn network. You don't need to call `send()` with the returned object.

**NOTE** `caver.wallet` must contains keyring instances corresponding to `from` and `feePayer` in `options` or `myContract.options` to make signatures.

**NOTE** `myContract.deploy` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭         | 타입     | 설명                                                                                                 |
| ---------- | ------ | -------------------------------------------------------------------------------------------------- |
| options    | object | 전송에 사용되는 옵션. See the table in [methods.methodName.send](#methods-methodname-send) for the details. |
| byteCode   | 문자열    | 컨트랙트의 바이트 코드.                                                                                      |
| parameters | 복합     | (optional) The parameters that get passed to the constructor on deployment.                        |


**리턴값**

`Promise` returning `PromiEvent`: The promise will be resolved with the new contract instance.

| 타입         | 설명                                                                                                                                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PromiEvent | 프로미스(promise)가 조합된 이벤트 이미터(event emitter). It will be resolved when the transaction receipt is available. If `send()` is called from a `myContract.deploy()`, then the promise will be resolved with the new contract instance. |

PromiEvent에서는 다음 이벤트가 발생할 수 있습니다.

- `transactionHash`: it is fired right after the transaction is sent and a transaction hash is available. Its type is `string`.
- `receipt`: It is fired when the transaction receipt is available. See [caver.rpc.klay.getTransactionReceipt](./caver.rpc/klay.md#caver-rpc-klay-gettransactionreceipt) for more details. Its type is `object`.
- `error`: It is fired if an error occurs during sending. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다. Its type is `Error`.

**예시**

```javascript
// Deploy a smart contract without constructor arguments
> myContract.deploy({
      from: '0x{address in hex}',
      gas: 1500000,
  }, '0x{byte code}')
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress) // contains the new contract address
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address) // instance with the new contract address
  })

// Deploy a smart contract with constructor arguments
> myContract.deploy({
      from: '0x{address in hex}',
      gas: 1500000,
  }, '0x{byte code}', 'keyString', ...)
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress) 
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address)
  })

// Deploy a smart contract with fee delegation transaction (TxTypeFeeDelegatedSmartContractDeploy)
> myContract.deploy({
      from: '0x{address in hex}',
      feeDelegation: true,
      feePayer: '0x{address in hex}',
      gas: 1500000,
  }, '0x{byte code}')
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress)
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address)
  })

// Deploy a smart contract with partial fee delegation transaction (TxTypeFeeDelegatedSmartContractDeployWithRatio)
> myContract.deploy({
      from: '0x{address in hex}',
      feeDelegation: true,
      feePayer: '0x{address in hex}',
      feeRatio: 30,
      gas: 1500000,
  }, '0x{byte code}')
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress)
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address)
  })
```

## myContract.deploy <a id="mycontract-deploy"></a>

```javascript
myContract.deploy(options)
```

Returns the object used when deploying the smart contract to the Klaytn. You can send the smart contract deploy transaction via calling `myContract.deploy({ data, arguments }).send(options)`. After a successful deployment, the promise will be resolved with a new contract instance.

**매개변수**

| 명칭      | 타입     | 설명                                                           |
| ------- | ------ | ------------------------------------------------------------ |
| options | object | The options object used for deployment. 자세한 내용은 아래 표를 참조하세요. |

옵션 개체에는 다음이 포함됩니다:

| 명칭        | 타입  | 설명                                                                         |
| --------- | --- | -------------------------------------------------------------------------- |
| data      | 문자열 | 컨트랙트의 바이트 코드.                                                              |
| arguments | 배열  | (optional) The arguments that get passed to the constructor on deployment. |

**리턴값**

`Promise` returning `object` - An object in which arguments and functions for contract distribution are defined.:

| 명칭                                                   | 타입       | 설명                                                                                                                                                                 |
| ---------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| arguments                                            | 배열       | The arguments passed in `options.arguments`.                                                                                                                       |
| [send](#methods-methodname-send)                     | function | The function that will deploy the contract to the Klaytn. The promise as the result of this function will be resolved with the new contract instance.              |
| [sign](#methods-methodname-sign)                     | function | The function that will sign a smart contract deploy transaction as a sender. The sign function will return signed transaction.                                     |
| [signAsFeePayer](#methods-methodname-signasfeepayer) | function | The function that will sign a smart contract deploy transaction as a fee payer. The signAsFeePayer function will return signed transaction.                        |
| [estimateGas](#methods-methodname-estimategas)       | function | The function that will estimate the gas used for the deployment. The execution of this function does not deploy the contract.                                      |
| [encodeABI](#methods-methodname-encodeabi)           | function | The function that encodes the ABI of the deployment, which is contract data + constructor parameters. The execution of this function does not deploy the contract. |

**NOTE** `myContract.deploy({ data, arguments }).sign(options)` and `myContract.deploy({ data, arguments }).signAsFeePayer(options)` are supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**예시**

```javascript
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My string']
  })
  .send({
      from: '0x1234567890123456789012345678901234567891',
      gas: 1500000,
      value: 0,
  }, function(error, transactionHash) { ... })
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress) // contains the new contract address
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address) // instance with the new contract address
  })

// When the data is already set as an option to the contract itself
> myContract.options.data = '0x12345...'

> myContract.deploy({
        arguments: [123, 'My string']
  })
  .send({
      from: '0x1234567890123456789012345678901234567891',
      gas: 1500000,
      value: 0,
  })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address) // instance with the new contract address
  })

// Simply encoding
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My string']
  })
  .encodeABI()
'0x12345...0000012345678765432'

// Gas estimation
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My string']
  })
  .estimateGas(function(err, gas) {
      console.log(gas)
  })
```


## myContract.send <a id="mycontract-send"></a>

```javascript
myContract.send(options, methodName [, param1 [, param2 [, ...]]])
```

Submits a transaction to execute the function of the smart contract. This can alter the smart contract state.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. If you want to use a fee-delegated transaction through `myContract.send`, `feeDelegation` and `feePayer` should be set properly.

- `feeDelegation` is not defined or defined to `false`: [SmartContractExecution][]
- `feeDelegation` is defined to `true`, but `feePayer` is not defined : Throws an error.
- `feeDelegation` is defined to `true` and `feePayer` is defined, but `feeRatio` is not defined: [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feePayer` and `feeRatio` are defined: [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `from` and `feePayer` in `options` or `myContract.options` to make signatures.

**NOTE** `myContract.send` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭         | 타입     | 설명                                                                                                 |
| ---------- | ------ | -------------------------------------------------------------------------------------------------- |
| options    | object | 전송에 사용되는 옵션. See the table in [methods.methodName.send](#methods-methodname-send) for the details. |
| methodName | 문자열    | The method name of the contract function to execute.                                               |
| parameters | 복합     | (optional) The parameters that get passed to the smart contract function.                          |

**리턴값**

`Promise` returns `PromiEvent`

| 타입         | 설명                                                                                                                                                                     |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PromiEvent | 프로미스(promise)가 조합된 이벤트 이미터(event emitter). It will be resolved when the transaction receipt is available. The promise will be resolved with the new contract instance. |

PromiEvent에서는 다음 이벤트가 발생할 수 있습니다.

- `transactionHash`: It is fired right after the transaction is sent and a transaction hash is available. Its type is `string`.
- `receipt`: It is fired when the transaction receipt is available. See [caver.rpc.klay.getTransactionReceipt](./caver.rpc/klay.md#caver-rpc-klay-gettransactionreceipt) for more details. Its type is `object`.
- `error`: It is fired if an error occurs during sending. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다. Its type is `Error`.

**예시**

```javascript
// Send a SmartContractExecution and use the promise
> myContract.send({ from: '0x{address in hex}', gas: 1000000 }, 'methodName', 123).then(console.log)
{
  blockHash: '0x294202dcd1d3c422880e2a209b9cd70ce7036300536c78ab74130c5717cb90da',
  blockNumber: 16342,
  contractAddress: null,
  from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  gas: '0xf4240',
  gasPrice: '0x5d21dba00',
  gasUsed: 47411,
  input: '0x983b2...',
  logsBloom: '0x00800...',
  nonce: '0x1cd',
  senderTxHash: '0xe3f50d2bab2c462ef99379860d2b634d85a0c9fba4e2b189daf1d96bd4bbf8ff',
  signatures: [ { V: '0x4e43', R: '0x2ba27...', S: '0x50d37...' } ],
  status: true,
  to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  transactionHash: '0xe3f50d2bab2c462ef99379860d2b634d85a0c9fba4e2b189daf1d96bd4bbf8ff',
  transactionIndex: 0,
  type: 'TxTypeSmartContractExecution',
  typeInt: 48,
  value: '0x0',
  events: {...}
}

// Send a SmartContractExecution and use the event emitter
> myContract.send({ from: '0x{address in hex}', gas: 1000000 }, 'methodName', 123)
  .on('transactionHash', function(hash) {
    ...
  })
  .on('receipt', function(receipt) {
    console.log(receipt)
  })
  .on('error', console.error)

// Send a FeeDelegatedSmartContractExecution
> myContract.send({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
    feePayer: '0x{address in hex}',
  }, 'methodName', 123).then(console.log)
{
  blockHash: '0x149e36f279577c306fccb9779a0274e802501c32f7054c951f592778bd5c168a',
  blockNumber: 16458,
  contractAddress: null,
  feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  feePayerSignatures: [ { V: '0x4e43', R: '0x48c28...', S: '0x18413...' } ],
  from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  gas: '0xf4240',
  gasPrice: '0x5d21dba00',
  gasUsed: 57411,
  input: '0x983b2d5600000000000000000000000022bb89bd35e7b12bd25bea4165cf0f9330032f8c',
  logsBloom: '0x00800...',
  nonce: '0x1f5',
  senderTxHash: '0x5b06ca5046229e066c11dfc0c74fcbc98509294370981f9b142378a8f2bd5fe8',
  signatures: [ { V: '0x4e44', R: '0xfb707...', S: '0x641c6...' } ],
  status: true,
  to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  transactionHash: '0x0e04be479ad06ec87acbf49abd44f16a56390c736f0a7354860ebc7fc0f92e13',
  transactionIndex: 1,
  type: 'TxTypeFeeDelegatedSmartContractExecution',
  typeInt: 49,
  value: '0x0',
  events: {...}
}

// Send a FeeDelegatedSmartContractExecutionWithRatio
> myContract.send({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
    feePayer: '0x{address in hex}',
    feeRatio: 30,
  }, 'methodName', 123).then(console.log)
{
  blockHash: '0x8f0a0137cf7e0fea503c818910140246437db36121871bc54b2ebc688873b3f3',
  blockNumber: 16539,
  contractAddress: null,
  feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  feePayerSignatures: [ { V: '0x4e43', R: '0x80db0...', S: '0xf8c7c...' } ],
  feeRatio: '0x1e',
  from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  gas: '0xf4240',
  gasPrice: '0x5d21dba00',
  gasUsed: 62411,
  input: '0x983b2d560000000000000000000000007ad1a538041fa3ba1a721f87203cb1a3822b8eaa',
  logsBloom: '0x00800...',
  nonce: '0x219',
  senderTxHash: '0x14c7b674a0e253b31c85c7be8cbfe4bf9d86e66e940fcae34b854e25eab1ce15',
  signatures: [ { V: '0x4e43', R: '0xd57ef...', S: '0xe14f3...' } ],
  status: true,
  to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  transactionHash: '0xfbf00ec189aeb0941d554384f1660ffdac7768b3af2bb1526bcb3983215c1183',
  transactionIndex: 0,
  type: 'TxTypeFeeDelegatedSmartContractExecutionWithRatio',
  typeInt: 50,
  value: '0x0',
  events: {...}
}
```

## myContract.sign <a id="mycontract-sign"></a>

```javascript
myContract.sign(options, methodName [, param1 [, param2 [, ...]]])
```

Signs a smart contract transaction as a sender to deploy the smart contract or execute the function of the smart contract.

If a smart contract is deployed, 'constructor' can be entered in the methodName, such as `myContract.sign({ from, ... }, 'constructor', byteCode, ...)`.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. If you want to use a fee-delegated transaction through `myContract.sign`, `feeDelegation` should be defined as `true`.

- `feeDelegation` is not defined or defined to `false`: [SmartContractDeploy][] / [SmartContractExecution][]
- `feeDelegation` is defined to `true`, but `feeRatio` is not defined: [FeeDelegatedSmartContractDeploy][] / [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feeRatio` is defined: [FeeDelegatedSmartContractDeployWithRatio][] / [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `from` in `options` or `myContract.options` to make signatures.

**NOTE** `myContract.sign` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭         | 타입     | 설명                                                                                                                                                                               |
| ---------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options    | object | 전송에 사용되는 옵션. See the table in [methods.methodName.send](#methods-methodname-send) for the details.                                                                               |
| methodName | 문자열    | The method name of the contract function to execute. If you want to sign a transaction for deploying the smart contract, use 'constructor' string instead of method name.        |
| parameters | 복합     | (optional) The parameters that get passed to the smart contract function. If you want to sign a smart contract deploy transaction, pass the byteCode and constructor parameters. |

**리턴값**

`Promise` returning [Transaction](./caver.transaction/README.md) - The signed smart contract transaction.

**예시**

```javascript
// Sign a SmartContractDeploy
> myContract.sign({ from: '0x{address in hex}', gas: 1000000 }, 'constructor', byteCode, 123).then(console.log)
SmartContractDeploy {
  _type: 'TxTypeSmartContractDeploy',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e43', _r: '0xeb6b5...', _s: '0x5e4f9...' } ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2a5'
}

// Sign a FeeDelegatedSmartContractDeploy
> myContract.sign({ from: '0x{address in hex}', feeDelegation: true, gas: 1000000 }, 'constructor', byteCode, 123).then(console.log)
FeeDelegatedSmartContractDeploy {
  _type: 'TxTypeFeeDelegatedSmartContractDeploy',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e43', _r: '0xee0f5...', _s: '0x31cbf...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x320'
}

// Sign a FeeDelegatedSmartContractDeployWithRatio
> myContract.sign({ from: keyring.address, feeDelegation: true, feeRatio: 30, gas: 1000000 }, 'constructor', byteCode, 123).then(console.log)
FeeDelegatedSmartContractDeployWithRatio {
  _type: 'TxTypeFeeDelegatedSmartContractDeployWithRatio',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e44', _r: '0x4c2b0...', _s: '0x47df8...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feeRatio: '0x1e',
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x306'
}

// Sign a SmartContractExecution
> myContract.sign({ from: '0x{address in hex}', gas: 1000000 }, 'methodName', 123).then(console.log)
SmartContractExecution {
  _type: 'TxTypeSmartContractExecution',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e44', _r: '0xb2846...', _s: '0x422c1...' } ],
  _to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  _value: '0x0',
  _input: '0x983b2...',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x23b'
}

// Sign a FeeDelegatedSmartContractExecution
> myContract.sign({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
  }, 'methodName', 123).then(console.log)
FeeDelegatedSmartContractExecution {
  _type: 'TxTypeFeeDelegatedSmartContractExecution',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e43', _r: '0xf7676...', _s: '0x42673...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  _value: '0x0',
  _input: '0x983b2...',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x254'
}

// Sign a FeeDelegatedSmartContractExecutionWithRatio
> myContract.sign({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
    feeRatio: 30,
  }, 'methodName', 123).then(console.log)
FeeDelegatedSmartContractExecutionWithRatio {
  _type: 'TxTypeFeeDelegatedSmartContractExecutionWithRatio',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x4e44', _r: '0x58b06...', _s: '0x637ff...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feeRatio: '0x1e',
  _to: '0x361870b50834a6afc3358e81a3f7f1b1eb9c7e55',
  _value: '0x0',
  _input: '0x983b2...',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x262'
}
```

## myContract.signAsFeePayer <a id="mycontract-signasfeepayer"></a>

```javascript
myContract.signAsFeePayer(options, methodName [, param1 [, param2 [, ...]]])
```

Signs a smart contract transaction as a fee payer to deploy the smart contract or execute the function of the smart contract.

If a smart contract is deployed, 'constructor' can be entered in the methodName, such as `myContract.signAsFeePayer({ from, feeDelegation: true, feePayer, ... }, 'constructor', byteCode, ...)`.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. The `signAsFeePayer` is a function that signs as a transaction fee payer, so `feeDelegation` field must be defined as `true`. Also, the address of the fee payer must be defined in the `feePayer` field.

- `feeDelegation` is not defined : Throws an error.
- `feeDelegation` is defined, but `feePayer` is not defined : Throws an error.
- `feeDelegation` is defined to `true` and `feePayer` is defined, but `feeRatio` is not defined: [FeeDelegatedSmartContractDeploy][] / [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feePayer` and `feeRatio` are defined: [FeeDelegatedSmartContractDeployWithRatio][] / [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `feePayer` in `options` or `myContract.options` to make signatures.

**NOTE** `myContract.signAsFeePayer` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭         | 타입     | 설명                                                                                                                                                                               |
| ---------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options    | object | 전송에 사용되는 옵션. See the table in [methods.methodName.send](#methods-methodname-send) for the details.                                                                               |
| methodName | 문자열    | The method name of the contract function to execute. If you want to sign a transaction for deploying the smart contract, use 'constructor' string instead of method name.        |
| parameters | 복합     | (optional) The parameters that get passed to the smart contract function. If you want to sign a smart contract deploy transaction, pass the byteCode and constructor parameters. |

**리턴값**

`Promise` returning [Transaction](./caver.transaction/README.md) - The signed smart contract transaction.

**예시**

```javascript
// Sign a FeeDelegatedSmartContractDeploy
> myContract.signAsFeePayer({ from: '0x{address in hex}', feeDelegation: true, feePayer: '0x{address in hex}', gas: 1000000 }, 'constructor', byteCode, 123).then(console.log)
FeeDelegatedSmartContractDeploy {
  _type: 'TxTypeFeeDelegatedSmartContractDeploy',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _feePayerSignatures: [ SignatureData { _v: '0x4e43', _r: '0xe0641...', _s: '0x1d21e...' } ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x32a'
}

// Sign a FeeDelegatedSmartContractDeployWithRatio
> myContract.signAsFeePayer({ from: keyring.address, feeDelegation: true, feePayer: '0x{address in hex}', feeRatio: 30, gas: 1000000 }, 'constructor', byteCode, 123).then(console.log)
FeeDelegatedSmartContractDeployWithRatio {
  _type: 'TxTypeFeeDelegatedSmartContractDeployWithRatio',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _feePayerSignatures: [ SignatureData { _v: '0x4e44', _r: '0x307bd...', _s: '0x75110...' } ],
  _feeRatio: '0x1e',
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x359'
}

// Sign a FeeDelegatedSmartContractExecution
> myContract.signAsFeePayer({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
    feePayer: '0x{address in hex}',
  }, 'methodName', 123).then(console.log)
FeeDelegatedSmartContractExecution {
  _type: 'TxTypeFeeDelegatedSmartContractExecution',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _feePayerSignatures: [ SignatureData { _v: '0x4e43', _r: '0xc58ba...', _s: '0x76fdb...' } ],
  _to: '0x4a9d979707aede18fa674711f3b2fe110fac4e7e',
  _value: '0x0',
  _input: '0x983b2...',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x36c'
}

// Sign a FeeDelegatedSmartContractExecutionWithRatio
> myContract.signAsFeePayer({
    from: '0x{address in hex}',
    gas: 1000000,
    feeDelegation: true,
    feePayer: '0x{address in hex}',
    feeRatio: 30,
  }, 'methodName', 123).then(console.log)
FeeDelegatedSmartContractExecutionWithRatio {
  _type: 'TxTypeFeeDelegatedSmartContractExecutionWithRatio',
  _from: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x69c3a6e3485446118d8081063dcef2e65b69ae91',
  _feePayerSignatures: [ SignatureData { _v: '0x4e44', _r: '0xeb78d...', _s: '0x2864d...' } ],
  _feeRatio: '0x1e',
  _to: '0x4a9d979707aede18fa674711f3b2fe110fac4e7e',
  _value: '0x0',
  _input: '0x983b2...',
  _chainId: '0x2710',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x37b'
}
```

## myContract.call <a id="mycontract-call"></a>

```javascript
myContract.call('methodName', [param1 [, param2 [, ...]]])
myContract.call(options, 'methodName', [param1 [, param2 [, ...]]])
```

Will call a constant method and execute its smart contract method in the Klaytn Virtual Machine without sending any transaction. Note that calling cannot alter the smart contract state.

**NOTE** `myContract.call` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭         | 타입     | 설명                                                                                                         |
| ---------- | ------ | ---------------------------------------------------------------------------------------------------------- |
| options    | object | (선택 사항) 호출에 사용되는 옵션. See the table in [methods.methodName.call](#methods-methodname-call) for the details. |
| methodName | 문자열    | The method name of the contract function to call.                                                          |
| parameters | 복합     | (optional) The parameters that get passed to the smart contract function.                                  |


**리턴값**

`Promise` returning `Mixed` - The return value(s) of the smart contract method. 하나를 반환하면, 그대로 반환됩니다. If it has multiple return values, it returns an object with properties and indices.

**예시**

```javascript
> myContract.call('methodName').then(console.log)
Jasmine

> myContract.call({ from: '0x{address in hex}' }, 'methodName', 123).then(console.log)
Test Result
```

## myContract.methods <a id="mycontract-methods"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]])
myContract.methods['methodName']([param1 [, param2 [, ...]]])
```
호출, 전송, 추정 또는 ABI 인코딩될 수 있는 해당 메소드에 대한 트랜잭션 객체를 생성합니다.

이 스마트 컨트랙트의 메소드는 다음을 통해 이용할 수 있습니다:

- The name with parameters: `myContract.methods.methodName(123)` or `myContract.methods[methodName](123)`
- The string-formatted name and the parameter type, and parameters: `myContract.methods['methodName(uint256)'](123)`
- The signature* for the method and parameters: `myContract.methods['0x58cf5f10'](123)`

이를 통해 자바스크립트 컨트랙트 객체로부터 이름은 같지만 매개변수가 다른 함수를 호출할 수 있습니다.

## cf) \*function signature (function selector)   <a id="cf-function-signature-function-selector"></a>
The first four bytes of the call data for a function call specifies the function to be called.  
It is the first (left, high-order in big-endian) four bytes of the Keccak-256 (SHA-3) hash of the signature of the function.

The function signature can be made by 2 different methods.  
`1. caver.abi.encodefunctionSignature('funcName(paramType1,paramType2,...)')`  
`2. caver.utils.sha3('funcName(paramType1,paramType2,...)').substr(0, 10)`

ex)
```javascript
caver.abi.encodefunctionSignature('methodName(uint256)')
> 0x58cf5f10

caver.utils.sha3('methodName(uint256)').substr(0, 10)
> 0x58cf5f10
```

**매개변수**

Parameters of any method that belongs to this smart contract, defined in the JSON interface.

**리턴값**

`Promise` returning `object` - An object in which arguments and functions for contract execution are defined.:

| 명칭                                                   | 타입       | 설명                                                                                                                                                                               |
| ---------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| arguments                                            | 배열       | The arguments passed to this method.                                                                                                                                             |
| [call](#methods-methodname-call)                     | function | The function that will call and execute a constant method in its smart contract on Klaytn Virtual Machine without sending a transaction (cannot alter the smart contract state). |
| [send](#methods-methodname-send)                     | function | The function that will send a transaction to the Klaytn and execute its method (can alter the smart contract state).                                                             |
| [sign](#methods-methodname-sign)                     | function | The function that will sign a transaction as a sender. The sign function will return signed transaction.                                                                         |
| [signAsFeePayer](#methods-methodname-signasfeepayer) | function | The function that will sign a transaction as a fee payer. The signAsFeePayer function will return signed transaction.                                                            |
| [estimateGas](#methods-methodname-estimategas)       | function | The that function will estimate the gas used for the execution.                                                                                                                  |
| [encodeABI](#methods-methodname-encodeabi)           | function | The function that encodes the ABI for this method. This can be sent using a transaction, calling the method, or passing into another smart contract method as its argument.      |

**NOTE** `sign` and `signAsFeePayer` are supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**예시**

```javascript
// Calling a method
> myContract.methods.methodName(123).call({ ... }, function(error, result) { ... })
> myContract.methods.methodName(123).call({ ... }).then((result) => { ... })

// Sending basic transaction and using the promise
> myContract.methods.methodName(123).send({
    from: '0x{address in hex}',
    ...
  }).then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  })

// Sending basic transaction and using the eventEmitter
> myContract.methods.methodName(123).send({
    from: '0x{address in hex}',
    ...
  }).on('transactionHash', function(hash) {
      ...
  })
  .on('receipt', function(receipt) {
      ...
  })
  .on('error', console.error)

// Sending fee delegation transaction and using the promise
> myContract.methods.methodName(123).send({
    from: '0x{address in hex}',
    feePayer: '0x{fee-payer address}',
    feeDelegation: true,f
    ...
  }).then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  })

// Sending partial fee delegation transaction and using the promise
> myContract.methods.methodName(123).send({
    from: '0x{address in hex}',
    feePayer: '0x{fee-payer address}',
    feeDelegation: true,
    feeRatio: 30,
    ...
  }).then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  })

// sign the basic transaction
> myContract.methods.methodName(123).sign({
    from: '0x{address in hex}',
    feeDelegation: true,
    ...
  }).then(function(signedTx) { ... })

// sign the fee delegation transaction
> myContract.methods.methodName(123).sign({
    from: '0x{address in hex}',
    feeDelegation: true,
    ...
  }).then(function(signedTx) { ... })

// sign the partial fee delegation transaction
> myContract.methods.methodName(123).sign({
    from: '0x{address in hex}',
    feeDelegation: true,
    feeRatio: 30,
    ...
  }).then(function(signedTx) { ... })

// sign the fee delegation transaction as a fee payer
> myContract.methods.methodName(123).signAsFeePayer({
    from: '0x{address in hex}',
    feePayer: '0x{fee-payer address}',
    feeDelegation: true,
    ...
  }).then(function(signedTx) { ... })

// sign the partial fee delegation transaction as a fee payer
> myContract.methods.methodName(123).signAsFeePayer({
    from: '0x{address in hex}',
    feePayer: '0x{fee-payer address}',
    feeDelegation: true,
    feeRatio: 30,
    ...
  }).then(function(signedTx) { ... })
```


## methods.methodName.call <a id="methods-methodname-call"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]]).call(options [, callback])
myContract.methods['methodName']([param1 [, param2 [, ...]]]).call(options [, callback])
```

Will call a constant method and execute its smart contract method in the Klaytn Virtual Machine without sending any transaction.  Note that calling cannot alter the smart contract state. You can use the [myContract.call](#mycontract-call) provided as a short-cut function.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                                                                                   |
| -------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options  | object   | (선택 사항) 호출에 사용되는 옵션. 자세한 내용은 아래 표를 참조하세요.                                                                                                                            |
| callback | function | (optional) This callback will be fired with the result of the smart contract method execution as the second argument, or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 명칭       | 타입     | 설명                                                                         |
| -------- | ------ | -------------------------------------------------------------------------- |
| from     | 문자열    | (optional) The address which calling contract methods should be made from. |
| gasPrice | 문자열    | (optional) The gas price in peb to use for this call.                      |
| gas      | number | (optional) The maximum gas provided for this call (gas limit).             |

**리턴값**

`Promise` returning `Mixed` - The return value(s) of the smart contract method. 하나를 반환하면, 그대로 반환됩니다. If it has multiple return values, it returns an object with properties and indices.

**예시**

```javascript
// using the promise
> myContract.methods.methodName(123).call({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(result) {
      ...
  })
```

```solidity
// Solidity: MULTIPLE RETURN VALUES
contract MyContract {
    function myFunction() public returns(uint256 myNumber, string memory myString) {
        return (23456, "Hello!%");
    }
}
```

```javascript
> var MyContract = new caver.contract(abi, address)
> MyContract.methods.myfunction().call().then(console.log)
Result {
      mynumber: '23456',
      mystring: 'Hello!%',
      0: '23456',
      1: 'Hello!%'
}
```

```solidity
// Solidity: SINGLE RETURN VALUE
contract MyContract {
    function myfunction() public returns(string memory mystring) {
        return "Hello!%";
    }
}
```

```javascript
> var MyContract = new caver.contract(abi, address)
> MyContract.methods.myfunction().call().then(console.log)
"Hello!%"
```


## methods.methodName.send <a id="methods-methodname-send"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]]).send(options [, callback])
myContract.methods['methodName']([param1 [, param2 [, ...]]]).send(options [, callback])
```

Will send a transaction to deploy the smart contract or execute the function of the smart contract. This can alter the smart contract state. You can use the [myContract.send](#mycontract-send) provided as a short-cut function.

If a smart contract is deployed, 'constructor' can be entered in the methodName, such as `myContract.methods.constructor` or `myContract.methods['constructor']`.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. If you want to use a fee-delegated transaction through `methods.methodName.send`, `feeDelegation` and `feePayer` should be set properly.

- `feeDelegation` is not defined or defined to `false`: [SmartContractDeploy][] / [SmartContractExecution][]
- `feeDelegation` is defined to `true`, but `feePayer` is not defined : Throws an error.
- `feeDelegation` is defined to `true` and `feePayer` is defined, but `feeRatio` is not defined: [FeeDelegatedSmartContractDeploy][] / [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feePayer` and `feeRatio` are defined: [FeeDelegatedSmartContractDeployWithRatio][] / [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `from` and `feePayer` in `options` or `myContract.options` to make signatures.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                                      |
| -------- | -------- | ----------------------------------------------------------------------------------------------------------------------- |
| options  | object   | 전송에 사용되는 옵션. 자세한 내용은 아래 표를 참조하세요.                                                                                       |
| callback | function | (optional) This callback will be fired first with the "transactionHash", or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 명칭            | 타입                                              | 설명                                                                                                                                                                                                                                                                                                                                                         |
| ------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| from          | 문자열                                             | 트랜잭션을 보낼 송신자 주소. If omitted, `myContract.options.from` will be used.                                                                                                                                                                                                                                                                                       |
| gas           | number                                          | The maximum gas provided for this transaction (gas limit).                                                                                                                                                                                                                                                                                                 |
| gasPrice      | 문자열                                             | (선택 사항) 트랜잭션에 사용할 peb 단위의 가스 가격.                                                                                                                                                                                                                                                                                                                           |
| value         | number &#124; string &#124; BN &#124; Bignumber | (optional) The value in peb to be transferred to the address of the smart contract by this transaction.                                                                                                                                                                                                                                                    |
| feeDelegation | boolean                                         | (optional, default `false`) Whether to use fee delegation transaction. If omitted, `myContract.options.feeDelegation` will be used.                                                                                                                                                                                                                        |
| feePayer      | 문자열                                             | (optional) The address of the fee payer paying the transaction fee. When `feeDelegation` is `true`, the value is set to the `feePayer` field in the transaction. If omitted, `myContract.options.feePayer` will be used.                                                                                                                                   |
| feeRatio      | 문자열                                             | (optional) The ratio of the transaction fee the fee payer will be burdened with. If `feeDelegation` is `true` and `feeRatio` is set to a valid value, a partial fee delegation transaction is used. The valid range of this is between 1 and 99. The ratio of 0, or 100 and above are not allowed. If omitted, `myContract.options.feeRatio` will be used. |

**NOTE** `feeDelegation`, `feePayer` and `feeRatio` are supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**리턴값**

`Promise` returns `PromiEvent`

| 타입         | 설명                                                                                                                                                                     |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PromiEvent | 프로미스(promise)가 조합된 이벤트 이미터(event emitter). It will be resolved when the transaction receipt is available. The promise will be resolved with the new contract instance. |

PromiEvent에서는 다음 이벤트가 발생할 수 있습니다.

- `transactionHash`: It is fired right after the transaction is sent and a transaction hash is available. Its type is `string`.
- `receipt`: It is fired when the transaction receipt is available. See [caver.rpc.klay.getTransactionReceipt](./caver.rpc/klay.md#caver-rpc-klay-gettransactionreceipt) for more details. Its type is `object`.
- `error`: It is fired if an error occurs during sending. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다. Its type is `Error`.

**예시**

```javascript
// using the promise
> myContract.methods.methodName(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  })


// using the event emitter
> myContract.methods.methodName(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .on('transactionHash', function(hash) {
    ...
  })
  .on('receipt', function(receipt) {
    console.log(receipt)
  })
  .on('error', console.error) // If there is an out-of-gas error, the second parameter is the receipt.

// receipt example
{
   "transactionHash": "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b",
   "transactionIndex": 0,
   "blockHash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
   "blocknumber": 3,
   "contractAddress": "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
   "gasUsed": 30234,
   "events": {
     "eventName": {
       returnValues: {
         myIndexedParam: 20,
         myOtherIndexedParam: '0x123456789...',
         myNonIndexParam: 'My string'
       },
       raw: {
         data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
         topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
       },
       event: 'eventName',
       signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
       logIndex: 0,
       transactionIndex: 0,
       transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
       blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
       blocknumber: 1234,
       address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
    },
    "MyOtherEvent": {
      ...
    },
    "MyMultipleEvent":[{...}, {...}] // If there are multiples of the same events, they will be in an array.
  }
}
```

## methods.methodName.sign <a id="methods-methodname-sign"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]]).sign(options)
myContract.methods['methodName']([param1 [, param2 [, ...]]]).sign(options)
```

Signs a smart contract transaction as a sender to deploy the smart contract or execute the function of the smart contract. You can use the [myContract.sign](#mycontract-sign) provided as a short-cut function.

If a smart contract is deployed, 'constructor' can be entered in the methodName, such as `myContract.methods.constructor` or `myContract.methods['constructor']`.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. If you want to use a fee-delegated transaction through `methods.methodName.sign`, `feeDelegation` should be defined as `true`.

- `feeDelegation` is not defined or defined to `false`: [SmartContractDeploy][] / [SmartContractExecution][]
- `feeDelegation` is defined to `true`, but `feeRatio` is not defined: [FeeDelegatedSmartContractDeploy][] / [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feeRatio` is defined: [FeeDelegatedSmartContractDeployWithRatio][] / [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `from` in `options` or `myContract.options` to make signatures.

**NOTE** `methods.methodName.sign` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭      | 타입     | 설명                                                                                                                                           |
| ------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| options | object | The options used for creating a transaction. See the parameter table in [methods.methodName.send](#methods-methodname-send) for the details. |

**리턴값**

`Promise` returning [Transaction](./caver.transaction/README.md) - The signed smart contract transaction.

**예시**

```javascript
// Sign a SmartContractDeploy transaction
> myContract.methods.constructor(byteCode, 123).sign({ from: '0x{address in hex}', gas: 1000000 }).then(console.log)
SmartContractDeploy {
  _type: 'TxTypeSmartContractDeploy',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [
    SignatureData {
      _v: '0x07f6',
      _r: '0x26a05...',
      _s: '0x3e3e4...'
    }
  ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}
> myContract.methods['constructor'](byteCode, 123).sign({ from: '0x{address in hex}', gas: 1000000 }).then(console.log)

// Sign a FeeDelegatedSmartContractDeploy transaction
> myContract.methods.constructor(byteCode, 123).sign({ from: '0x{address in hex}', feeDelegation: true, gas: 1000000 }).then(console.log)
FeeDelegatedSmartContractDeploy {
  _type: 'TxTypeFeeDelegatedSmartContractDeploy',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x07f5', _r: '0xa74f7...', _s: '0x0991e...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}
> myContract.methods['constructor'](byteCode, 123).sign({ from: '0x{address in hex}', feeDelegation: true, gas: 1000000 }).then(console.log)

// Sign a SmartContractExecution transaction
> myContract.methods.methodName('0x...').sign({ from: '0x{address in hex}', gas: 1000000 }).then(console.log)
SmartContractExecution {
  _type: 'TxTypeSmartContractExecution',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x07f5', _r: '0xafbf9...', _s: '0x10ea0...' } ],
  _to: '0xbc6723431a57abcacc4016ae664ee778d313ca6e',
  _value: '0x0',
  _input: '0x983b2d5600000000000000000000000060498fefbf1705a3db8d7bb5c80d5238956343e5',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}

> myContract.methods['methodName']('0x...').sign({ from: '0x{address in hex}', gas: 1000000 }).then(console.log)

// Sign a FeeDelegatedSmartContractExecution transaction
> myContract.methods.methodName('0x...').sign({ from: '0x{address in hex}', feeDelegation: true, gas: 1000000 }).then(console.log)
FeeDelegatedSmartContractExecution {
  _type: 'TxTypeFeeDelegatedSmartContractExecution',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x07f6', _r: '0xdfc14...', _s: '0x38b9c...' } ],
  _feePayer: '0x0000000000000000000000000000000000000000',
  _feePayerSignatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _to: '0xbc6723431a57abcacc4016ae664ee778d313ca6e',
  _value: '0x0',
  _input: '0x983b2d5600000000000000000000000060498fefbf1705a3db8d7bb5c80d5238956343e5',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}
> myContract.methods['methodName']('0x...').sign({ from: '0x{address in hex}', feeDelegation: true, gas: 1000000 }).then(console.log)
```

## methods.methodName.signAsFeePayer <a id="methods-methodname-signasfeepayer"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]]).signAsFeePayer(options)
myContract.methods['methodName']([param1 [, param2 [, ...]]]).signAsFeePayer(options)
```

Signs a smart contract transaction as a fee payer to deploy the smart contract or execute the function of the smart contract. You can use the [myContract.signAsFeePayer](#mycontract-signasfeepayer) provided as a short-cut function.

If a smart contract is deployed, 'constructor' can be entered in the methodName, such as `myContract.methods.constructor` or `myContract.methods['constructor']`.

The transaction type used for this function depends on the `options` or the value defined in `myContract.options`. The `signAsFeePayer` is a function that signs as a transaction fee payer, so `feeDelegation` field must be defined as `true`. Also, the address of the fee payer must be defined in the `feePayer` field.

- `feeDelegation` is not defined : Throws an error.
- `feeDelegation` is defined, but `feePayer` is not defined : Throws an error.
- `feeDelegation` is defined to `true` and `feePayer` is defined, but `feeRatio` is not defined: [FeeDelegatedSmartContractDeploy][] / [FeeDelegatedSmartContractExecution][]
- `feeDelegation` is defined to `true` and `feePayer` and `feeRatio` are defined: [FeeDelegatedSmartContractDeployWithRatio][] / [FeeDelegatedSmartContractExecutionWithRatio][]

**NOTE** `caver.wallet` must contains keyring instances corresponding to `feePayer` in `options` or `myContract.options` to make signatures.

**NOTE** `methods.methodName.signAsFeePayer` is supported since caver-js [v1.6.1](https://www.npmjs.com/package/caver-js/v/1.6.1).

**매개변수**

| 명칭      | 타입     | 설명                                                                                                                                           |
| ------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| options | object | The options used for creating a transaction. See the parameter table in [methods.methodName.send](#methods-methodname-send) for the details. |

**리턴값**

`Promise` returning [Transaction](./caver.transaction/README.md) - The signed smart contract transaction.

**예시**

```javascript
// Sign a FeeDelegatedSmartContractDeploy transaction
> myContract.methods.constructor(byteCode, 123).signAsFeePayer({ from: '0x{address in hex}', feeDelegation: true, feePayer: '0x{address in hex}', gas: 1000000 }).then(console.log)
> FeeDelegatedSmartContractDeploy {
  _type: 'TxTypeFeeDelegatedSmartContractDeploy',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _feePayerSignatures: [ SignatureData { _v: '0x07f6', _r: '0x2c385...', _s: '0x7fa79...' } ],
  _to: '0x',
  _value: '0x0',
  _input: '0x60806...',
  _humanReadable: false,
  _codeFormat: '0x0',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}
> myContract.methods['constructor'](byteCode, 123).signAsFeePayer({ from: '0x{address in hex}', feeDelegation: true, feePayer: '0x{address in hex}', gas: 1000000 }).then(console.log)

// Sign a FeeDelegatedSmartContractExecution transaction
> myContract.methods.methodName(123).signAsFeePayer({ from: '0x{address in hex}', feeDelegation: true, feePayer: '0x{address in hex}', gas: 1000000 }).then(console.log)
> FeeDelegatedSmartContractExecution {
  _type: 'TxTypeFeeDelegatedSmartContractExecution',
  _from: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _gas: '0xf4240',
  _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
  _feePayer: '0x60498fefbf1705a3db8d7bb5c80d5238956343e5',
  _feePayerSignatures: [ SignatureData { _v: '0x07f6', _r: '0x793eb...', _s: '0x0f776...' } ],
  _to: '0x294b2618f29714732cfc202d7be53bf5efee90dd',
  _value: '0x0',
  _input: '0x983b2d5600000000000000000000000060498fefbf1705a3db8d7bb5c80d5238956343e5',
  _chainId: '0x3e9',
  _gasPrice: '0x5d21dba00',
  _nonce: '0x2f6'
}
> myContract.methods['methodName'](123).signAsFeePayer({ from: '0x{address in hex}', feeDelegation: true, feePayer: '0x{address in hex}', gas: 1000000 }).then(console.log)
```

## methods.methodName.estimateGas <a id="methods-methodname-estimategas"></a>

```javascript
myContract.methods.methodName([param1 [, param2 [, ...]]]).estimateGas(options [, callback])
```

Will estimate the gas that a method execution will take when executed in the Klaytn Virtual Machine. The estimation can differ from the actual gas used when later sending a transaction, as the state of the smart contract can be different at that time.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                                                                  |
| -------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| options  | object   | (선택 사항) 호출에 사용되는 옵션. 자세한 내용은 아래 표를 참조하세요.                                                                                                           |
| callback | function | (optional) This callback will be fired with the result of the gas estimation as the second argument, or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 명칭    | 타입                                              | 설명                                                                                                                                                                     |
| ----- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| from  | 문자열                                             | (optional) The address from which calling the contract method should be made.                                                                                          |
| gas   | number                                          | (optional) The maximum gas provided for this call (gas limit). 특정 값을 설정하면 가스 부족 오류를 감지하는 데 도움이 됩니다. 모든 가스가 사용되면 같은 숫자를 반환합니다.                                          |
| value | number &#124; string &#124; BN &#124; Bignumber | (optional) The value in peb that would be transferred to the address of the smart contract if the transaction for executing this contract function was sent to Klaytn. |

**리턴값**

`프로미스`는 `Number`을 반환합니다.

| 타입     | 설명                                               |
| ------ | ------------------------------------------------ |
| number | The used gas for the simulated call/transaction. |

**예시**

```javascript
> myContract.methods.methodName(123).estimateGas({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(gasAmount) {
    ...
  })
  .catch(function(error) {
    ...
  })
```


## methods.methodName.encodeABI <a id="methods-methodname-encodeabi"></a>

```javascript
myContract.methods.methodName([param1 [, param2[, ...]]]).encodeABI()
```

이 메소드에 대한 ABI를 인코딩합니다. This can be used to send a transaction or call a method, or pass it into another smart contract method as arguments.


**매개변수**

Parameters of any method that belongs to this smart contract, defined in the JSON interface.

**리턴값**

| 타입  | 설명                                  |
| --- | ----------------------------------- |
| 문자열 | 트랜잭션 또는 호출을 통해 전송할 인코딩된 ABI 바이트 코드. |


**예시**

```javascript
> myContract.methods.methodName(123).encodeABI()
'0x58cf5f1000000000000000000000000000000000000000000000000000000000000007B'
```


## myContract.once <a id="mycontract-once"></a>

```javascript
myContract.once(event [, options], callback)
```

Subscribes to an event and unsubscribes immediately after the first event or error. 단일 이벤트에 대해서만 발생합니다.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                                                        |
| -------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| event    | 문자열      | The name of the event in the contract, or `allEvents` to get all events.                                                                  |
| options  | object   | (optional) The options used for subscription. 자세한 내용은 아래 표를 참조하세요.                                                                        |
| callback | function | 이 콜백은 첫 번째 이벤트를 두 번째 인수로, 또는 오류를 첫 번째 인수로 하여 발생됩니다. See [myContract.getPastEvents](#getpastevents) for details about the event structure. |

옵션 개체에는 다음이 포함됩니다:

| 명칭     | 타입     | 설명                                                                                                                                                                    |
| ------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 필터     | object | (optional) Lets you filter events by indexed parameters, *e.g.*, `{filter: {mynumber: [12,13]}}` means all events where "mynumber" is 12 or 13.                       |
| topics | 배열     | (optional) This allows you to manually set the topics for the event filter. Given the filter property and event signature, `topic[0]` would not be set automatically. |

**리턴값**

`Promise` returns `object` - An event object. For more detail about event object, please refer to [myContract.getPastEvents](#getpastevents).

**예시**

```javascript
> myContract.once('eventName', {
    filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
  }, function(error, event) { console.log(event) })

// event output example
{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My string'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'eventName',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blocknumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
}
```


## myContract.events <a id="mycontract-events"></a>

```javascript
myContract.events.eventName([options][, callback])
```

이벤트를 구독합니다.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                               |
| -------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| options  | object   | (optional) The options used for subscription. 자세한 내용은 아래 표를 참조하세요.                                               |
| callback | function | (optional) This callback will be fired for each event as the second argument, or an error as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 명칭        | 타입     | 설명                                                                                                                                                                    |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 필터        | object | (optional) Lets you filter events by indexed parameters, *e.g.*, `{filter: {mynumber: [12,13]}}` means all events where "mynumber" is 12 or 13.                       |
| fromBlock | number | (optional) The block number from which to get events.                                                                                                                 |
| topics    | 배열     | (optional) This allows you to manually set the topics for the event filter. Given the filter property and event signature, `topic[0]` would not be set automatically. |


**리턴값**

`EventEmitter`: 이벤트 이미터는 다음 이벤트를 가집니다:

| 명칭        | 타입     | 설명                                                                                        |
| --------- | ------ | ----------------------------------------------------------------------------------------- |
| data      | object | Fires on each incoming event with the event object as an argument.                        |
| connected | 문자열    | Fires once after the subscription successfully connected. It returns the subscription ID. |
| error     | object | 구독 오류가 발생하면 발생합니다.                                                                        |

**NOTE** `connected` is available with caver-js [v1.5.7](https://www.npmjs.com/package/caver-js/v/1.5.7).

The structure of the returned event `object` looks as follows:

| 명칭               | 타입                   | 설명                                                                                                      |
| ---------------- | -------------------- | ------------------------------------------------------------------------------------------------------- |
| event            | 문자열                  | 이벤트 이름.                                                                                                 |
| 서명 값입니다.         | string &#124; `null` | The event signature, `null` if it is an anonymous event.                                                |
| address          | 문자열                  | 이 이벤트가 발생한 주소.                                                                                          |
| returnValues     | object               | The return values coming from the event, *e.g.*, `{myVar: 1, myVar2: '0x234...'}`.                      |
| logIndex         | number               | 블록에서 이벤트 인덱스 위치의 정수값.                                                                                   |
| transactionIndex | number               | 이벤트가 생성된 트랜잭션의 인덱스 위치의 정수값.                                                                             |
| transactionHash  | 32바이트 문자열            | 이 이벤트가 생성된 트랜잭션의 해시. 아직 보류 중인 경우 `null`.                                                                |
| blockHash        | 32바이트 문자열            | 이 이벤트가 생성된 블록의 해시. 아직 보류 중인 경우 `null`.                                                                  |
| blocknumber      | number               | 이 로그가 생성된 블록 번호. 아직 보류 중인 경우 `null`.                                                                    |
| raw.data         | 문자열                  | 색인화되지 않은 로그 매개변수를 포함하는 데이터.                                                                             |
| raw.topics       | 배열                   | An array with a maximum of four 32-byte topics, and topic 1-3 contains indexed parameters of the event. |
| id               | 문자열                  | 로그 식별자. `keccak256(blockHash + transactionHash + logIndex).substr(0, 8)`을 사용하여 "log_" 문자열을 연결하여 작성됩니다.  |

**예시**

```javascript
> myContract.events.eventName({
    filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
    fromBlock: 0
  }, function(error, event) { console.log(event) })
  .on('connected', function(subscriptionId){
      console.log(subscriptionId)
  })
  .on('data', function(event){
      console.log(event) // same results as the optional callback above
  })
  .on('error', console.error)

// event output example
{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My string'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'eventName',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blocknumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    id: 'log_41d221bc',
}
```


## events.allEvents <a id="events-allevents"></a>

```javascript
myContract.events.allEvents([options] [, callback])
```
Same as [myContract.events](#mycontract-events) but receives all events from this smart contract. 선택적으로 filter 속성은 해당 이벤트를 필터링할 수 있습니다.


## getPastEvents <a id="getpastevents"></a>

```javascript
myContract.getPastEvents(event [, options] [, callback])
```
이 컨트랙트의 이전 이벤트를 가져옵니다.

**매개변수**

| 명칭       | 타입       | 설명                                                                                                                            |
| -------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| event    | 문자열      | 컨트랙트, 또는 모든 이벤트를 받기 위한 `"allEvents"`에서의 이벤트 이름.                                                                               |
| options  | object   | (optional) The options used for subscription. 자세한 내용은 아래 표를 참조하세요.                                                            |
| callback | function | (optional) This callback will be fired with an array of event logs as the second argument, or an error as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 명칭        | 타입     | 설명                                                                                                                                                                 |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 필터        | object | (optional) Lets you filter events by indexed parameters, *e.g.*, `{filter: {mynumber: [12,13]}}` means all events where "mynumber" is 12 or 13.                    |
| fromBlock | number | (optional) The block number from which to get events.                                                                                                              |
| toBlock   | number | (optional) The block number to get events up to (defaults to `"latest"`).                                                                                          |
| topics    | 배열     | (optional) This allows manually setting the topics for the event filter. Given the filter property and event signature, `topic[0]` would not be set automatically. |

**리턴값**

`Promise` returns `Array` - An array with the past event objects, matching the given event name and filter.

An event object can contain the following:

| 명칭               | 타입                   | 설명                                                                                                                                                                                                            |
| ---------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| event            | 문자열                  | 이벤트 이름.                                                                                                                                                                                                       |
| 서명 값입니다.         | string &#124; `null` | The event signature, `null` if it’s an anonymous event.                                                                                                                                                       |
| address          | 문자열                  | Address this event originated from.                                                                                                                                                                           |
| returnValues     | object               | The return values coming from the event, e.g. {myVar: 1, myVar2: '0x234...'}.                                                                                                                                 |
| logIndex         | number               | The event index position in the block.                                                                                                                                                                        |
| transactionIndex | number               | The transaction’s index position the event was created in.                                                                                                                                                    |
| transactionHash  | 문자열                  | The hash of the transaction this event was created in.                                                                                                                                                        |
| blockHash        | 문자열                  | The hash of the block this event was created in. null when it’s still pending.                                                                                                                                |
| blockNumber      | number               | The block number this log was created in. null when still pending.                                                                                                                                            |
| raw              | object               | An object defines `data` and `topic`. `raw.data` containing non-indexed log parameter. `raw.topic` is an array with a maximum of four 32 Byte topics, and topic 1-3 contains indexed parameters of the event. |

**예시**

```javascript
> myContract.getPastEvents('eventName', {
      filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
      fromBlock: 0,
      toBlock: 'latest'
  }, function(error, events) { console.log(events) })
  .then(function(events) {
      console.log(events) // same results as the optional callback above
  })

[{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My string'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'eventName',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blocknumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
},{
      ...
}]
```

[SmartContractDeploy]: ./caver.transaction/basic.md#smartcontractdeploy
[SmartContractExecution]: ./caver.transaction/basic.md#txtypesmartcontractexecution
[FeeDelegatedSmartContractDeploy]: ./caver.transaction/fee-delegation.md#txtypefeedelegatedsmartcontractdeploy
[FeeDelegatedSmartContractExecution]: ./caver.transaction/fee-delegation.md#txtypefeedelegatedsmartcontractexecution
[FeeDelegatedSmartContractDeployWithRatio]: ./caver.transaction/partial-fee-delegation.md#txtypefeedelegatedsmartcontractdeploywithratio
[FeeDelegatedSmartContractExecutionWithRatio]: ./caver.transaction/partial-fee-delegation.md#txtypefeedelegatedsmartcontractexecutionwithratio