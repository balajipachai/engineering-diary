# Iden3 Identity Stack Deployment

## Goal

Deploy and configure the complete iden3 identity stack (zero-knowledge proof-based identity system) on Puppynet and Shibarium networks to enable decentralized identity verification for the ShibaOne ecosystem.

## Networks Targeted

- **Puppynet** (Chain ID: 157) - Shibarium testnet environment
- **Shibarium** (Chain ID: 109) - Shibarium mainnet

## Features & Components

### Core Identity Infrastructure

- [x] **State Contract**: Manages identity state transitions with zero-knowledge proofs
- [x] **Universal Verifier**: Central verification hub for different proof types
- [x] **Identity Tree Store**: Manages identity merkle trees and claims

### Validator Contracts

- [x] **MTP Validator**: Merkle Tree Proof credential validation
- [x] **Signature Validator**: Signature-based credential validation
- [x] **V3 Validator**: Next-generation proof validation
- [x] **Linked Multi-Query**: Complex multi-credential queries
- [x] **Auth V2**: Authentication proof validation
- [x] **ETH Identity**: Ethereum-based identity validation

### Supporting Libraries

- [x] **Poseidon Hash Functions**: zk-SNARK friendly hash functions (1-4 inputs)
- [x] **SMT Libraries**: Sparse Merkle Tree implementation
- [x] **Verifier Libraries**: Groth16 proof verification wrappers

### Cross-Chain Components

- [x] **Cross-Chain Proof Validator**: Multi-network proof verification
- [x] **Oracle Integration**: Trusted oracle for cross-chain state validation

## Timeline

### Phase 1: Network Configuration ✅

- **Duration**: 1 day (Sept 8, 2025)
- **Completed**:
  - Hardhat configuration for both networks
  - Etherscan/block explorer integration
  - Multiple Solidity compiler versions (0.4.11 - 0.8.27)
  - Parameter files for network-specific configurations

### Phase 2: Puppynet Deployment ✅

- **Duration**: 1 day (Sept 9, 2025)
- **Completed**:
  - All core contracts deployed successfully (Redeployment needed)
  - Contract verification working with multi-compiler setup
  - Configuration populated with actual deployment addresses

### Phase 3: Shibarium Deployment 🔄

- **Status**: Ready for deployment
- **Prerequisites**: Configuration files prepared with proper parameters

### Phase 4: Integration & Testing

- **Status**: Pending
- **Tasks**:
  - Cross-chain functionality testing
  - Integration with ShibaOne applications
  - Performance and gas optimization

## Technical Challenges & Solutions

### Challenge 1: CreateX Factory Configuration

- **Issue**: Puppynet had CreateX deployed at non-standard address
- **Impact**: Hardhat Ignition create2 strategy failed
- **Solution**: Deployment falls back to basic strategy, still achieves deterministic addresses
- **Custom Address**: `0x49b80787E663e4FE18A3d91e5a70bfD317e2834b`

- This needs redeployment, will be redeployed tomorrow.

### Challenge 2: Hardhat Ignition Deployment Errors

- **Issue**: "Invariant violated: neither timeouts or failures"
- **Root Cause**: Empty string parameters in configuration
- **Solution**: Populated all required addresses:
  - Oracle signing addresses: `0x0aD316c6D3F29B76cBd8f5a1ED5e3990c6B5174C`
  - Proxy admin owners: `0xf518CcaC8Adf316b99ca226FEC4359fAc56db5C6`

### Challenge 3: Contract Verification Issues

- **Issue**: "Etherscan only supports compiler versions 0.4.11 and higher"
- **Cause**: Some contracts compiled with older Solidity versions
- **Solution**: Added multiple compiler configurations:
  ```typescript
  compilers: [
    { version: "0.8.27" }, // Main contracts
    { version: "0.6.11" }, // Legacy libraries
    { version: "0.5.17" }, // Compatibility
    { version: "0.4.11" }, // Minimum supported
  ];
  ```

## Deployed Contract Addresses (Puppynet - Chain 157)

### Core Infrastructure

- **State Proxy**: `0x7df79166FcA19DB113C3f7a08E90991b2c1bea77`
- **Universal Verifier**: `0xE18fF67c11639966F1af3a60A9DB2FE202C84A38`
- **Identity Tree Store**: `0x9369bAD75BeD62775F7A53dd1336339294150e0b`

### Validators

- **MTP Validator**: `0x527486cdC434F6b851A0de70d5d9453335D77d35`
- **Signature Validator**: `0x9f4847dBB41DF8BB65A38cB5c54D2eaa148BCD88`
- **V3 Validator**: `0xE0141aa31fD8628679B0D14dce90743a5BA4897e`
- **Auth V2 Validator**: `0xd0608d9f2971332d0F9BCD31D0799fBf3f28639F`
- **ETH Identity Validator**: `0x3dF65a61f520A0F8625E10c8007767e7fC936F82`

### Libraries & Utilities

- **Poseidon1**: `0x55232dbDcc3dDF957408a4e017D606Cd8277dA74`
- **Poseidon2**: `0x002d062BD48C64DEEA614098bB12F89264648de1`
- **Poseidon3**: `0x6AF8587766a5E330721Bfc57BD23C75c9584E916`
- **Poseidon4**: `0x8F9A571753b0660f10909D4856BC20967d3a5838`
- **SMT Lib**: `0x733Ae7E2e497f8aCd87e9533e2895176e40e52EE`

## Lessons Learned

### 1. **Configuration Management**

- Empty string parameters cause deployment failures
- Always validate configuration files before deployment
- Network-specific parameters must be properly set

### 2. **Multi-Compiler Strategy**

- Complex projects may need multiple Solidity versions
- Block explorer verification requires supported compiler versions
- Optimizer settings should be consistent across versions

### 3. **Deployment State Management**

- Hardhat Ignition maintains deployment state in journal files
- Corrupted state requires cleanup and restart
- Always backup deployment artifacts before major changes

### 4. **Network Integration**

- Each network needs custom Etherscan/block explorer configuration
- API keys and URLs must match network requirements
- Gas settings should be network-appropriate

### 5. **Identity Stack Architecture**

- Modular design allows selective deployment of components
- Cross-chain functionality requires careful oracle configuration
- Zero-knowledge proof validation is computationally intensive

## Future Improvements

1. **Automation**: Create deployment scripts for multi-network deployment
2. **Monitoring**: Set up contract monitoring and alerting
3. **Documentation**: Create integration guides for developers
4. **Testing**: Comprehensive test suite for cross-chain functionality
5. **Optimization**: Gas usage optimization for production deployment

## Resources

- **Repository**: `identity-stack/iden3-contracts/contracts`
- **Documentation**: Iden3 protocol documentation
- **Networks**:
  - Puppynet Explorer: https://puppyscan.shib.io/
  - Shibarium Explorer: https://www.shibariumscan.io/
- **Configuration Files**:
  - `ignition/modules/params/chain-157.json`
  - `ignition/modules/params/chain-109.json`
