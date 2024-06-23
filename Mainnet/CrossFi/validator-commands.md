![CrossFi x BlockFarms](./logos.png)

# Validator Commands
Chain Id: 
```
mineplex-mainnet-1
```



### Daemon Commands
How to create a validator with 10,000 MPX tokens. [reference](https://docs.crossfi.org/crossfi-chain/technical-information/validators)
```
mineplex tx staking create-validator \
  --amount=10000000000000000000000mpx \
  --pubkey=$(mineplex --home /your/directory/path/crossfi/ tendermint show-validator) \
  --moniker="My Validator" \
  --website="My-website.com" \
  --identity=keybaseID \
  --details="My validator details" \
  --security-contact="email@gmail.com" \
  --chain-id=crossfi-evm-testnet-1 \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --gas="auto" \
  --gas-prices="10000000000000mpx" \
  --gas-adjustment=1.5 \
  --from=validator
```

How to edit validator details [reference](https://docs.crossfi.org/crossfi-chain/technical-information/validators)
```
mineplex tx staking edit-validator \
  --new-moniker="My Validator" \
  --website="My-website.com" \
  --identity=keybaseID \
  --details="My validator details" \
  --security-contact="email@gmail.com" \
  --chain-id=crossfi-evm-testnet-1 \
  --gas="auto" \
  --gas-prices="10000000000000mpx" \
  --gas-adjustment=1.5 \
  --from=validator \
  --commission-rate="0.050"
```

How to increase validator self MPX stake (delegation) by 10,000 MPX
```
mineplex tx staking delegate \
    yourValidatorValoperAddress \
    10000000000000000000000mpx \
    --from yourValidatorAddress \
    --gas="auto" \
    --gas-prices="10000000000000mpx" \
    --gas-adjustment=1.5 \
    --account-number=yourAccountNumber \
    --chain-id=crossfi-evm-testnet-1
```

How to withdraw all your validator rewards (self delegation & commission)
```
mineplex tx distribution withdraw-all-rewards \
    --from yourValidatorAddress \
    --chain-id crossfi-evm-testnet-1 \
    --gas auto \
    --gas-adjustment 1.5 \
    --gas-prices 10000000000000mpx
```

How to send 10,000 MPX to another address
```
mineplex tx bank send \
    fromAddress \
    toAddress \
    10000000000000000000000mpx \
    --gas auto \
    --gas-adjustment 1.5 \
    --gas-prices 10000000000000mpx \
    -y
```


How to unjail your validator
```
mineplex tx slashing unjail \
    --from yourValidatorAddress \
    --chain-id crossfi-evm-testnet-1 \
    --gas auto \
    --gas-adjustment 1.5 \
    --gas-prices 10000000000000mpx \
    -y
```

How to unbond 10,000 MPX or stop (if that is all the tokens) your validator
```
mineplex tx staking unbond \
    yourValidatorValoperAddress \
    10000000000000000000000mpx \
    --from yourValidatorAddress \
    --chain-id crossfi-evm-testnet-1 \
    --gas auto \
    --gas-adjustment 1.5 \
    --gas-prices 10000000000000mpx \
    -y
```

### Wallet & Balance Commands
List all wallets 
```
mineplex keys list
```

Import existing wallet
```
mineplex keys import yourWallet yourWallet.txt
```

Export existing wallet
```
mineplex keys export yourWallet
```

Create new wallet
```
mineplex keys add yourWallet
```

Delete wallet
```
mineplex keys delete yourWallet
```

Check token balances
```
mineplex q bank balances $(mineplex keys show yourWallet -a)
```

### Governance

View Proposals
```
mineplex query gov proposals
```

Vote on Proposals
```
mineplex tx gov vote \
    proposalNumber \
    yes/no \
    --from yourValidatorAddress \
    --chain-id crossfi-evm-testnet-1 \
    --gas auto \
    --gas-adjustment 1.5 \
    --gas-prices 10000000000000mpx \
    -y
```


### Basic DevOps & Monitoring

Check Logs
```
journalctl -u mineplex -f
```

Check syncing status (True/False), get latest block, and various validator info (Peer Address)
```
curl -s localhost:26657/status
```

Check validator status
```
systemctl status mineplex
```

Start validator
```
systemctl start mineplex
```

Reload daemon of the validator
```
systemctl daemon-reload
```

Stop Validator
```
systemctl stop mineplex
```

Restart Validator
```
systemctl restart mineplex
```

Enable Validator start upon machine startup
```
systemctl enable mineplex
```

Disable Validator start upon machine startup
```
systemctl disable mineplex
```


Check Prometheus metrics via Curl
```
curl localhost:26660/metrics
```
