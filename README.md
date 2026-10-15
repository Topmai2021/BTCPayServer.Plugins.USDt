# BTCPay Server USDt Plugin

![BTCPay USDt Plugin](Docs/banner.png)

This repository contains the source code for the BTCPay Server plugin that enables the receipt of USDt payments on multiple blockchains. 
The plugin extends the functionality of BTCPay Server, a self-hosted cryptocurrency payment processor that allows merchants to accept Bitcoin and other cryptocurrencies.

## 🎨 Features

- **USDt Payments**: Receive USDt payments directly on your BTCPay Server instance.
- **Multi-Chain Support**: Accept USDt on TRON, Ethereum, Polygon, and BNB Smart Chain (BSC).
- **Customizable Settings**: Configure JSON RPC endpoints and addresses per blockchain to suit your requirements.
- **Invoice Generation**: Generate invoices with blockchain addresses as payment reception.
- **Blockchain Monitoring**: Scan supported blockchains to detect payments in full, overpaid, or partial amounts.
- **Automatic Settlement**: Continuously verify blockchains to settle payments securely and efficiently.

## Supported blockchains

- [x] TRON
- [x] Ethereum
- [x] Polygon
- [x] BNB Smart Chain (BSC)

## 📗 Requirements

- BTCPay Server 2.4.5 or newer. This branch is built and unit-tested against 2.4.5; newer releases require their own compatibility check.
- A compatible wallet for each chain you want to use (e.g., Ledger, MetaMask, TrustWallet...) to generate and manage addresses for receiving USDt payments.

## 🚀 Installation

Build a clean Release package with `BTCPayServer.PluginPacker`, then upload the `.btcpay` file under **Manage Plugins > Upload Plugin** and restart BTCPay Server. Test installation, store configuration, invoice creation, payment detection, and settlement on a disposable instance before accepting mainnet funds. A successful build and unit tests alone do not validate those live workflows.

From the repository root, with the BTCPay Server submodule initialized:

```sh
dotnet test --project BTCPayServer.Plugins.USDt.Tests/BTCPayServer.Plugins.USDt.Tests.csproj --configuration Release
dotnet build BTCPayServer.Plugins.USDt/BTCPayServer.Plugins.USDt.csproj --configuration Release
dotnet run --project submodules/btcpayserver/BTCPayServer.PluginPacker/BTCPayServer.PluginPacker.csproj --configuration Release -- BTCPayServer.Plugins.USDt/bin/Release/net10.0 BTCPayServer.Plugins.USDt artifacts
```

The BSC testnet configuration does not include a token contract. Supply a test-token contract address before testing BSC payments on testnet.

## 🧑‍💻 Developing
### Naming convention
This plugin aims to cover USDt payment over different chains, a rigorous naming convention was implemented to ensure readability but also allow extensibility:

### USD₮
- Currency: `USDt`  
- Currency Display Name: `USD₮` and `USD₮ on BLOCKCHAIN_NAME`

### TRON
- Blockchain: TRON
- PaymentMethodId for USDt: USDT-TRON
- TRON specific implementation: Tron* and TronUSDtLike* for TRC20 compatible stuff

### Ethereum
- Blockchain: Ethereum
- PaymentMethodId for USDt: USDT-Ethereum
- Ethereum specific implementation: Ethereum* and EthereumUSDtLike* for ERC20 compatible stuff

### Polygon
- Blockchain: Polygon
- PaymentMethodId for USDt: USDT-Polygon
- Polygon specific implementation: Polygon* and PolygonUSDtLike* for ERC20 compatible stuff

### BNB Smart Chain (BSC)
- Blockchain: BSC
- PaymentMethodId for USDt: USDT-BSC
- BSC specific implementation: reuses the EVMUSDtLike* implementation
- Mainnet chain ID: 56
- Mainnet USDt/BEP-20 contract: `0x55d398326f99059ff775485246999027b3197955`
- Default RPC endpoint: `https://bsc-rpc.publicnode.com`
- Block explorer: `https://bscscan.com/tx/{0}`
- Testnet chain ID: 97
- Testnet RPC endpoint: `https://bsc-testnet-rpc.publicnode.com`
- Testnet block explorer: `https://testnet.bscscan.com/tx/{0}`
- Testnet smart contract address is intentionally unconfigured by default. Configure a BEP-20 test token contract in the plugin server settings before testing BSC testnet payments.


## 💚 Support

For any questions, issues, or feedback related to the BTCPay Server USDt Plugin, please [open an issue](https://github.com/btcpayserver-tether/BTCPayServer.Plugins.TronUSDt/issues) in this repository.

## 📝 License

This project is licensed under the [MIT License](LICENSE).
