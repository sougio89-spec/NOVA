# NOVA ECOSYSTEM V32 — DUAL TOKEN DEVNET TEST

This package contains the five servers:

1. NOVA MINING
2. NOVA CORE (folder `NOVA`)
3. NEXUS
4. TOKENIA
5. OPUS

## Solana Devnet tokens

- NOVA-Test: `3TjaggzWLmy6c3PPFTUz63e5pr1RS2Hg25so5MRZRtRK`
- NEXUS-Test: `F2GTysEXAtra3KGvnwfqpcuypz3Mb4pfok4L4b6SteHZ`
- decimals: 9 / 9
- network: Solana Devnet
- real monetary value: none

## Economic separation

- NOVA / NOVA CORE / NOVA MINING -> NOVA-Test
- native NEXUS nodes / orchestration -> NEXUS-Test
- TOKENIA is the payment/economic rail
- OPUS submits jobs; it does not choose execution resources

## Security

No private key is included in this ZIP.
Create two dedicated Devnet treasury keypairs. Never use the Playground/main wallet key as a server secret.

Windows:

`TOKENIA\scripts\create_devnet_treasuries_v32.bat`

Linux/macOS:

`TOKENIA/scripts/create_devnet_treasuries_v32.sh`

Fund each treasury with Devnet SOL for transaction fees.
Then transfer test-token reserves from your current holder wallet to the corresponding treasury public key.

Example from the supply holder wallet:

```bash
spl-token transfer 3TjaggzWLmy6c3PPFTUz63e5pr1RS2Hg25so5MRZRtRK 100000 NOVA_TREASURY_PUBKEY --fund-recipient --allow-unfunded-recipient
spl-token transfer F2GTysEXAtra3KGvnwfqpcuypz3Mb4pfok4L4b6SteHZ 100000 NEXUS_TREASURY_PUBKEY --fund-recipient --allow-unfunded-recipient
```

For a first test, 100 or 1,000 tokens per treasury is enough; 100,000 is only an example.

## TOKENIA environment

Copy `TOKENIA/.env.example` and configure:

```text
TOKENIA_SOLANA_LIVE=true
TOKENIA_NOVA_TREASURY_KEYPAIR=<absolute path to nova treasury json>
TOKENIA_NEXUS_TREASURY_KEYPAIR=<absolute path to nexus treasury json>
TOKENIA_NEXUS_SERVICE_KEY=<random shared devnet service secret>
TOKENIA_NOVA_SERVICE_KEY=<different random devnet service secret>
```

NEXUS must use the same `TOKENIA_NEXUS_SERVICE_KEY`.

## V32 rails

NEXUS verified native node job:

`NEXUS -> TOKENIA /integrations/nexus/reward asset=NEXUS -> NEXUS-Test wallet`

NOVA/CORE verified job:

`NOVA -> TOKENIA /integrations/nova/onchain-reward -> NOVA-Test wallet`

## Check status

TOKENIA:

`GET /solana/status`

returns readiness for both NOVA and NEXUS independently.

Payout history:

`GET /solana/payouts`

Each payout records `asset`, `mint`, Solana signature, job ID, worker ID and destination wallet.
`job_id` is unique: retrying the same payout cannot produce a second chain payment.

## Offline self-test

From TOKENIA folder:

```bash
python scripts/selftest_v32_dual_token.py
```

Expected:

`V32 DUAL TOKEN SELFTEST: PASS`

This test does not spend Devnet tokens.

## Important

V32 is a development/test release. The reward rate is not final tokenomics and should not be used for mainnet economics.
