# V31 QUICK TEST — NEXUS -> TOKENIA -> NOVA-Test Devnet

Mint: `3TjaggzWLmy6c3PPFTUz63e5pr1RS2Hg25so5MRZRtRK`

## 1. Treasury
Create a dedicated Devnet treasury. Do not reuse the Playground wallet private key.

Windows: `TOKENIA/scripts/create_devnet_treasury.bat`

Linux/macOS: `TOKENIA/scripts/create_devnet_treasury.sh`

Fund the treasury with Devnet SOL and NOVA-Test.

## 2. Environment
TOKENIA:

```
TOKENIA_NOVA_MINT=3TjaggzWLmy6c3PPFTUz63e5pr1RS2Hg25so5MRZRtRK
TOKENIA_SOLANA_RPC=https://api.devnet.solana.com
TOKENIA_SOLANA_LIVE=true
TOKENIA_SOLANA_TREASURY_KEYPAIR=/absolute/path/tokenia_treasury_devnet.json
TOKENIA_NEXUS_SERVICE_KEY=choose-a-long-random-devnet-secret
```

NEXUS:

```
TOKENIA_URL=http://127.0.0.1:8410
TOKENIA_NEXUS_SERVICE_KEY=choose-the-same-long-random-devnet-secret
NEXUS_NOVA_REWARD_PER_SECOND=0.01
NEXUS_NOVA_REWARD_MAX=100
```

## 3. Worker registration
A NEXUS worker includes its Solana Devnet wallet in `capabilities`:

```json
{
  "name": "RTX-3090-WORKER",
  "capabilities": {
    "gpu": "RTX 3090",
    "vram_mb": 24576,
    "wallet_address": "WORKER_SOLANA_DEVNET_WALLET"
  }
}
```

## 4. Payment
When `/nodes/submit` verifies the result, NEXUS calls TOKENIA.
TOKENIA checks the NEXUS service credential, records a PENDING payout, transfers
NOVA-Test on Devnet, records the Solana signature, then credits its internal audit ledger.

A unique constraint on `job_id` makes the operation idempotent.

## 5. Status
TOKENIA:

- `GET /solana/status`
- `GET /solana/payouts`

The first endpoint must show `ready: true` before live Devnet payouts are enabled.

## Development warning
The current payout formula is a V31 test policy only. It is not the final NOVA tokenomics.
