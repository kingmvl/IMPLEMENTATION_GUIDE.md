# IMPLEMENTATION_GUIDE.md

# Phase 2: Implementation of the ZK-Compliance Gate

### 🧩 System Architecture: The "Compliance-Yield" Bridge
To solve bridge risk, we utilize **Circle CCTP** to burn USDC on Ethereum and mint Native USDC on Pharos. The "Gate" is a Smart Contract that only releases the minted USDC to a user if they present a valid **ZK-Proof** from our Compliance Module.

### 📝 Logic Flow: ZK-Identity Verification
1. **Off-Chain:** User submits PII to a trusted validator.
2. **ZK-Generation:** Validator generates a Zero-Knowledge Proof (circom/snarkjs) verifying "User is >18 and not on a Sanction List" without revealing the name.
3. **On-Chain:** The Pharos `ComplianceManager.sol` contract verifies the proof.
4. **Liquidity Release:** Once verified, the CCTP-minted USDC is unlocked for RWA vault deposits.

### 📊 Data Schema: Institutional Asset Passport (JSON)
```json
{
  "asset_id": "PHR-AGRI-001",
  "compliance_standard": "ERC-3643",
  "zk_verification_status": "VERIFIED",
  "liquidity_rail": "CCTP_NATIVE",
  "parallel_hint_group": "DP4_SETTLEMENT_A"
}
