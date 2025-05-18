# l1-fees-spike

Check out the docs for [`L1BlockInfo`](https://docs.rs/op-alloy-rpc-types/0.16.0/op_alloy_rpc_types/struct.L1BlockInfo.html):

```rust
pub struct L1BlockInfo {
    pub l1_gas_price: Option<u128>,
    pub l1_gas_used: Option<u128>,
    pub l1_fee: Option<u128>,
    pub l1_fee_scalar: Option<f64>,
    pub l1_base_fee_scalar: Option<u128>,
    pub l1_blob_base_fee: Option<u128>,
    pub l1_blob_base_fee_scalar: Option<u128>,
    pub operator_fee_scalar: Option<u128>,
    pub operator_fee_constant: Option<u128>,
}
```

>L1 block info extracted from inout of first transaction in every block.
>
>The subset of OpTransactionReceiptFields, that encompasses L1 block info: https://github.com/ethereum-optimism/op-geth/blob/f2e69450c6eec9c35d56af91389a1c47737206ca/core/types/receipt.go#L87-L87

```rust
//! rpc-types/src/receipt.rs

/// OP Transaction Receipt type
#[derive(Clone, Debug, PartialEq, Eq, Serialize, Deserialize)]
#[serde(rename_all = "camelCase")]
#[doc(alias = "OpTxReceipt")]
pub struct OpTransactionReceipt {
    /// Regular eth transaction receipt including deposit receipts
    #[serde(flatten)]
    pub inner: alloy_rpc_types_eth::TransactionReceipt<OpReceiptEnvelope<alloy_rpc_types_eth::Log>>,
    /// L1 block info of the transaction.
    #[serde(flatten)]
    pub l1_block_info: L1BlockInfo,
}
```
