# Kampus Token - Creating Token Using SUI and Move Network

A comprehensive project demonstrating how to create a custom token on the SUI blockchain using the Move programming language.

## Project Overview

This project implements **KAMPUS_COIN**, a custom token built on the SUI blockchain. It demonstrates the fundamental concepts of token creation, minting, and burning using Move smart contracts.

### Key Features

- Custom token implementation using SUI's `Coin` standard
- Treasury-controlled minting system
- Token burning capabilities
- Immutable metadata with icon support
- Secure ownership transfer mechanisms

## Project Structure

```
kampus_token/
├── Move.toml              # Project configuration
├── Move.lock              # Dependency lock file
├── sources/
│   └── kampus_token.move  # Main token contract
├── tests/
│   └── kampus_token_tests.move  # Unit tests
└── build/                 # Compiled bytecode (generated)
```

## Token Specifications

| Property | Value |
|----------|-------|
| **Name** | Kampus Token |
| **Symbol** | KAMPUS |
| **Decimals** | 9 |
| **Description** | Token untuk sistem kampus blockchain |
| **Icon URL** | https://kampus.io/icon.png |

## Smart Contract Details

### Core Components

#### 1. One Time Witness (OTW)
```move
public struct KAMPUS_COIN has drop {}
```
- Used for token initialization
- Ensures single-time currency creation
- Provides type safety for the token

#### 2. Initialization Function
```move
fun init(witness: KAMPUS_COIN, ctx: &mut TxContext)
```
- Creates the token currency with metadata
- Transfers treasury control to deployer
- Freezes metadata to prevent future changes

#### 3. Minting Function
```move
public fun mint(treasury_cap: &mut TreasuryCap<KAMPUS_COIN>, amount: u64, recipient: address, ctx: &mut TxContext)
```
- Allows treasury owner to mint new tokens
- Transfers minted tokens directly to specified recipient
- Requires treasury capability for authorization

#### 4. Burning Function
```move
public fun burn(treasury_cap: &mut TreasuryCap<KAMPUS_COIN>, coin: Coin<KAMPUS_COIN>)
```
- Permanently destroys tokens
- Reduces total supply
- Requires treasury capability

## Getting Started

### Prerequisites

1. **SUI CLI** - Install from [SUI Documentation](https://docs.sui.io/guides/developer/getting-started/sui-install)
2. **Move Language** - Comes with SUI CLI
3. **SUI Wallet** - For testnet/mainnet operations

### Installation & Setup

1. **Clone the project**
```bash
git clone <repository-url>
cd kampus_token
```

2. **Install dependencies**
```bash
sui move build
```

3. **Run tests**
```bash
sui move test
```

### Deployment

1. **Compile the contract**
```bash
sui move build
```

2. **Deploy to network**
```bash
sui client publish --gas-budget 10000000
```

3. **Note the package ID and treasury cap object ID from deployment output**

## Usage Examples

### Minting Tokens

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module kampus_coin \
  --function mint \
  --args <TREASURY_CAP_ID> <AMOUNT> <RECIPIENT_ADDRESS> \
  --gas-budget 10000000
```

**Example:**
```bash
sui client call \
  --package 0xb95d5dc781fed7f8eabd651fd6815a4668de60a50fbd1b2c38dae74c47b1177d \
  --module kampus_coin \
  --function mint \
  --args 0x2491a7f24ea71fada7193e27b0d6c782fe3a190a58f905ae91c61c24218a62a7 1000000000000 0x64e646adc3e6e0af412ce979765e67195ee758f603a324fc9c8af391fdb29892 \
  --gas-budget 10000000
```

### Burning Tokens

```bash
sui client call \
  --package <PACKAGE_ID> \
  --module kampus_coin \
  --function burn \
  --args <TREASURY_CAP_ID> <COIN_OBJECT_ID> \
  --gas-budget 10000000
```

## Security Features

- **Treasury Control**: Only treasury cap owner can mint tokens
- **Immutable Metadata**: Token information cannot be changed after deployment
- **Type Safety**: Move's type system prevents common token vulnerabilities
- **Object Ownership**: SUI's object model ensures secure asset management

## Testing

The project includes comprehensive tests in `tests/kampus_token_tests.move`:

```bash
# Run all tests
sui move test

# Run specific test
sui move test --filter <test_name>
```

## Learning Resources

### SUI & Move Documentation
- [SUI Documentation](https://docs.sui.io/)
- [Move Language Guide](https://move-language.github.io/move/)
- [SUI Move by Example](https://examples.sui.io/)

### Token Standards
- [SUI Coin Standard](https://docs.sui.io/concepts/sui-move-concepts/coin)
- [Token Creation Tutorial](https://docs.sui.io/guides/developer/sui-101/create-coin)

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Useful Links

- [SUI Explorer](https://suiexplorer.com/) - View transactions and objects
- [SUI Faucet](https://docs.sui.io/guides/developer/getting-started/get-coins) - Get testnet SUI
- [SUI Discord](https://discord.gg/sui) - Community support

## Support

If you have questions or need help:

1. Check the [SUI Documentation](https://docs.sui.io/)
2. Join the [SUI Discord Community](https://discord.gg/sui)
3. Open an issue in this repository

---

**Built with ❤️ using SUI and Move**
