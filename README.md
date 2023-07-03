## CryptoAssetInsuranceFactory

### Description
The `CryptoAssetInsuranceFactory` contract serves as a factory contract responsible for creating and managing different `AssetWalletInsurance` contracts. It enables customers to purchase insurance for their asset wallets and provides functionality for claiming insurance amounts.

### Contracts and Libraries Used
- `AggregatorV3Interface`: An interface used for interacting with price oracle contracts.
- `IERC20`: An interface used for interacting with ERC20 token contracts.
- `ReentrancyGuard`: A library employed to prevent reentrancy attacks.

### Contract Variables
- `owner`: The address of the contract owner.
- `ethToUsd`: The address of the ETH to USD price oracle contract.
- `customers`: An array containing customer addresses.
- `customerToContract`: A mapping linking customer addresses to their insurance contract addresses.
- `contractToCustomer`: A mapping associating insurance contract addresses with customer addresses.
- `plans`: A mapping connecting insurance plans (1, 2, or 3) with their coverage percentages.

### Events
- `InsurancePurchased`: Triggered when a customer purchases insurance. Includes the customer address, contract address, and amount paid.
- `ClaimedInsurance`: Triggered when an insurance contract claims the insurance amount. Includes the contract address and the amount claimed.

### Constructor
- `constructor(address _ethToUsd) payable`: Initializes the contract with the ETH to USD price oracle address and requires a minimum initial value of 2 ether.

### Modifiers
- `onlyOwner`: Modifier used to check if the caller is the contract owner.

### Functions
- `getOwner()`: Returns the address of the contract owner.
- `withdraw(uint256 amount)`: Withdraws the specified amount of funds from the contract to the owner's address.
- `getCustomers()`: Returns an array of customer addresses.
- `getCustomerToContract(address customerAddress)`: Returns the insurance contract address associated with the given customer address.
- `getTokenBalance(address tokenAddress, address accountAddress)`: Returns the balance of the specified token for the given account address.
- `getFeedValueOfAsset(address _oracleAddress)`: Returns the latest feed value of the specified asset from the given oracle address.
- `getUsdToWei()`: Returns the conversion rate from USD to Wei.
- `calculateDepositMoney(uint256 _tokens, uint256 _plan, uint256 _priceAtInsurance, uint256 _decimals, uint256 _timePeriod)`: Calculates the deposit amount required for the insurance.
- `getInsurance(uint8 plan, address assetAddress, uint256 timePeriod, address oracleAddress, uint256 decimals, uint256 tokensInsured) payable`: Creates a new insurance contract for the specified asset.
- `claimInsurance() payable`: Allows an insurance contract to claim the insurance amount.

## AssetWalletInsurance

### Description
The `AssetWalletInsurance` contract represents insurance for an asset wallet. It is created by the `CryptoAssetInsuranceFactory` contract and allows the wallet owner to claim the insurance amount.

### Contract Variables
- `owner`: The address of the wallet owner.
- `assetAddress`: The address of the asset token.
- `tokensInsured`: The number of insured tokens.
- `plan`: The insurance plan (1, 2, or 3).
- `timePeriod`: The insurance time period in months.
- `claimAmount`: The amount of insurance that can be claimed.
- `factoryContract`: The address of the insurance factory contract.
- `oracleAddress`: The address of the price oracle contract for the asset.
- `priceAtInsurance`: The price of the asset at the time of insurance.
- `decimals`: The number of decimals for the asset token.

### Events
- `InsuranceClaimed`: Triggered when the insurance amount is successfully claimed. Includes the contract address and the amount claimed.

### Constructor
- `constructor(address _owner, address _assetAddress, uint256 _tokensInsured, uint8 _plan, uint256 _timePeriod, address _factoryContract, address _oracleAddress, uint256 _priceAtInsurance, uint256 _decimals)`: Initializes the contract with the provided parameters.

### Modifiers
- `onlyOwner`: Modifier used to check if the caller is the contract owner.

### Functions
- `getOwner()`: Returns the address of the wallet owner.
- `getAssetAddress()`: Returns the address of the asset token.
- `getTokensInsured()`: Returns the number of insured tokens.
- `getPlan()`: Returns the insurance plan.
- `getTimePeriod()`: Returns the insurance time period in months.
- `getClaimAmount()`: Returns the amount of insurance that can be claimed.
- `getFactoryContract()`: Returns the address of the insurance factory contract.
- `getOracleAddress()`: Returns the address of the price oracle contract for the asset.
- `getPriceAtInsurance()`: Returns the price of the asset at the time of insurance.
- `getDecimals()`: Returns the number of decimals for the asset token.
- `claimInsurance()`: Allows the wallet owner to claim the insurance amount.
