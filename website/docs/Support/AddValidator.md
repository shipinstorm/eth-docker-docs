---
id: AddValidator
title:  Add or recover validators.
sidebar_label: Add Validators
---

You can use eth2.0-deposit-cli to either recover validator signing keys or add
additional ones, if you wish to deposit more validators against the same mnemonic.

> The same cautions apply as when creating keys in the first place. You
> may wish to take these steps on a machine that is disconnected from Internet
> and will be wiped immediately after creating the keys.

In order to recover all your validator signing keys, run `sudo docker-compose run --rm deposit-cli-existing --uid $(id -u)`
and provide your mnemonic, then set index to "0" and the number of validators to the number you had created previously
and are now recreating.
> Specifying the uid is optional. If this is not done, the generated files will be owned
> by the user with the user id `1000`

In order to add additional validator signing keys, likewise run `sudo docker-compose run --rm deposit-cli-existing --eth1_withdrawal_address YOURHARDWAREWALLETADDRESS --uid $(id -u)`
and provide your mnemonic, but this time set the index to the number of validator keys you had created previously,
for example, `4`. New validators will be created after this point. You will receive new `keystore-m` signing keys
and a new `deposit_data` JSON.
> This example assumes that you want to fix withdrawals to an Ethereum address you control,
> ideally a hardware wallet. You can leave the `--eth1_withdrawal_address` parameter out
> and withdrawals will work with your seed phrase (mnemonic), to any address you
> specify during withdrawal.

**Caution**

Please triple-check your work here. You want to be sure the new validator keys are created after
the existing ones. Launchpad will likely safeguard you against depositing twice, but don't rely
on it. Verify that the public keys in `deposit_data` are new and you did not deposit for them
previously.
