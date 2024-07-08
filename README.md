# Staked Tensorians Snapshot

This repo contains historical snapshots of STAKED Tensorians.

- `staked_tensorians_YYYYMMDD.csv`: all Tensorians that are staked and their owners
- `staked_tensorians_UNIQUE_YYYYMMDD.csv`: all UNIQUE (de-duplicated) holders*

\* be aware that this is not sybil resistant: an individual can spin up multiple wallets and show up as multiple holders.

## Staked Tensorians

```sql
-- UNIQUES
SELECT DISTINCT owner
FROM "TStakeAccount"
WHERE "currentActive" IS TRUE
AND "nftMint" IN (SELECT "onchainId" FROM "MintV2" JOIN "VOCCollectionMap" ON "MintV2"."vocCollectionMapId" = "VOCCollectionMap".id JOIN "CollectionV2" ON "VOCCollectionMap"."collectionId" = "CollectionV2".id where "slugDisplay" = 'tensorians')
ORDER BY "owner"

-- ALL
SELECT "owner", "nftMint", "stakedDate"
FROM "TStakeAccount"
WHERE "currentActive" IS TRUE
AND "nftMint" IN (SELECT "onchainId" FROM "MintV2" JOIN "VOCCollectionMap" ON "MintV2"."vocCollectionMapId" = "VOCCollectionMap".id JOIN "CollectionV2" ON "VOCCollectionMap"."collectionId" = "CollectionV2".id where "slugDisplay" = 'tensorians')
ORDER BY "owner", "stakedDate"
```
