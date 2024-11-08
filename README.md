# Hyperlane Bridge
Hello, although I think Hyperlane will not do a user-centric airdrop, let’s do a few transactions with warp routes here, as the user side has already been growing for a long time.

No need for a VPS; you can do it for free on Github Codespaces: https://github.com/codespaces 

# Requirements: 
 - On the Base Network: 0.0025 ETH; on the Zora Network: 0.002 ETH 
 - You’ll spend approximately 1-2$ on transactions which you can withdraw afterward.
 - To bridge: $BRETT token. You can buy any amount on Uniswap.

## # Updates
```console
sudo apt-get update && sudo apt-get upgrade -y

# Let's Switch to root

sudo su

apt install curl iptables build-essential jq git make gcc nano wget htop tmux pkg-config nvme-cli libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

## # nvm
```console
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"

# Node.js && npm && yarn
nvm install node
npm install -g yarn
```

## # Hyperlane
```console
git clone https://github.com/hyperlane-xyz/hyperlane-monorepo.git && cd hyperlane-monorepo && yarn install && yarn build && cd typescript/cli

# Create an EVM wallet, save the private key.
# Fund it with 0.0025 $ETH on Base Network, and 0.002 $ETH on Zora Network.
# You’ll spend approximately 1-2$ on transactions, which you can withdraw afterward.

export PVT_KEY="YourPrivKey"
export WALLET="YourWalletAddress"

export HYP_KEY="$PVT_KEY"

mkdir -p ./configs

# Enter the section starting with the cat command and ending with the second EOF all at once.
cat <<EOF > ./configs/warp-route-deployment.yaml
base:
  interchainSecurityModule:
    modules:
      - relayer: "$WALLET"
        type: trustedRelayerIsm
      - domains: {}
        owner: "$WALLET"
        type: defaultFallbackRoutingIsm
    threshold: 1
    type: staticAggregationIsm
  isNft: false
  mailbox: "0xeA87ae93Fa0019a82A727bfd3eBd1cFCa8f64f1D"
  owner: "$WALLET"
  token: "0x532f27101965dd16442e59d40670faf5ebb142e4"
  type: collateral
zoramainnet:
  interchainSecurityModule:
    modules:
      - relayer: "$WALLET"
        type: trustedRelayerIsm
      - domains: {}
        owner: "$WALLET"
        type: defaultFallbackRoutingIsm
    threshold: 1
    type: staticAggregationIsm
  isNft: false
  mailbox: "0xF5da68b2577EF5C0A0D98aA2a58483a68C2f232a"
  owner: "$WALLET"
  type: synthetic
EOF

yarn hyperlane warp deploy

# If there’s enough balance in the wallet, press Enter 3 times. It will then send a few transactions automatically, so wait.
# Then Copy the text below.
```
```console
tokens:
      - chainName: base
        standard: EvmHypCollateral
        decimals: 18
        symbol: BRETT
        name: Brett
        addressOrDenom: "0x538A34E1066cEf2C92472c267af673341c2791E5"
        collateralAddressOrDenom: "0x532f27101965dd16442e59d40670faf5ebb142e4"
        connections:
          - token: ethereum|zoramainnet|0xc264bBd7d3F1aE35215b2A128E0D5e7e702e7A50
      - chainName: zoramainnet
        standard: EvmHypSynthetic
        decimals: 18
        symbol: BRETT
        name: Brett
        addressOrDenom: "0xc264bBd7d3F1aE35215b2A128E0D5e7e702e7A50"
        connections:
          - token: ethereum|base|0x538A34E1066cEf2C92472c267af673341c2791E5
```

## # Bridge
> We’ll need some tokens for the bridge. You can bridge the $BRETT token between Base <> Zora. You can buy it on Uniswap.
> Go to https://hyperlane.superbridge.app. Normally, the Zora Network won’t be visible. Open the settings on the Superbridge site, click on “Customize,” paste the copied section, save and close it; the Zora network has been added. Select the Brett token and bridge.

> If you get stuck anywhere: ▪️ X : https://x.com/256_tr ▪️ X : https://x.com/256__en
