---
description: Running Hop node on Kubernetes
---

# Running on Kubernetes

## This doc has exercise to deploy USDC Hop/Bonder on testnet ( Goerli ).

### Steps to follow

- Create a KeyStore, follow this [doc](https://docs.hop.exchange/hop-node/keystore)

- Create a `config.json` , follow [this](https://docs.hop.exchange/hop-node/configuration) config

  - We will use `Goerli` Network

- Make sure you have `Funds` in your wallet! with the amount you want to `Stake`

  - You can mint Test USDC on Goerli using [this](https://goerli.etherscan.io/token/0x98339d8c260052b7ad81c28c16c0b98420f2b46a?a=0x9Dc99fAf98d363Ec0909D1f5C3627dDdEA2a85D4#writeContract) Contract! Connect your wallet and use mint function!


- Modify the given k8s manifest files!

### Deployment.yaml

```bash
 nano deployment.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hop
  namespace: hop
  labels:
    app: hop
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hop
  template:
    metadata:
      labels:
        app: hop
    spec:
      volumes:
      - name: hop-volume
        persistentVolumeClaim:
          claimName: hop-volume
      - name: json-configmap-volume
        configMap:
          name: json-configmap
      containers:
      - name: hop
        image: hopprotocol/hop-node:mainnet
        # imagePullPolicy: Always
        ports:
        - containerPort: 8080
        command: ['/usr/src/app/bin/hop-node', '--config', '/tmp/config.json']
        volumeMounts:
        - mountPath: /root
          name: hop-volume

        - mountPath: /tmp/
          name: json-configmap-volume
        env:
          - name: KEYSTORE_PASS
            valueFrom:
              secretKeyRef:
                name: hop-secret
                key: keystorepass

        resources:
          requests:
            memory: "8Gi"
            cpu: "4"
          # limits:
          #   memory: "10Gi"
          #   cpu: "5"

```

### Configmap.yaml

```bash
nano cm.yaml
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: json-configmap
  namespace: hop
data:
  config.json: |
    {
      "network": "goerli",
      "chains": {
        "ethereum": {
          "rpcUrl": "https://goerli.infura.io/v3/YourInfuraKey",
          "maxGasPrice": 500
        },
        "polygon": {
          "rpcUrl": "https://polygon-mumbai.infura.io/v3/YourInfuraKey",
          "maxGasPrice": 5000
        },
        "arbitrum": {
          "rpcUrl": "https://arbitrum-goerli.infura.io/v3/YourInfuraKey",
          "maxGasPrice": 500
        },
        "optimism": {
          "rpcUrl": "https://optimism-goerli.infura.io/v3/YourInfuraKey",
          "maxGasPrice": 500
        }
      },
      "tokens": {
        "USDC": true
      },
      "watchers": {
        "bondTransferRoot": true,
        "bondWithdrawal": true,
        "commitTransfers": true,
        "settleBondedWithdrawals": true,
        "confirmRoots": true,
        "L1ToL2Relay": true
      },
      "db": {
        "location": "/root/db"
      },
      "logging": {
        "level": "debug"
      },
      "keystore": {
        "location": "/tmp/keystore.json"
      },
        "routes": {
              "ethereum": {
                      "polygon": true,
                      "arbitrum": true,
                      "optimism": true
              },
              "polygon": {
                      "ethereum": true,
                      "arbitrum": true,
                      "optimism": true
              },
              "arbitrum": {
                      "ethereum": true,
                      "polygon": true,
                      "optimism": true
              },
              "optimism": {
                      "ethereum": true,
                      "polygon": true,
                      "arbitrum": true
              }
      },
      "commitTransfers": {
        "minThresholdAmount": {
          "USDC": {
            "polygon": {
              "ethereum": 50000,
              "optimism": 10000,
              "arbitrum": 10000
            },
            "optimism": {
              "ethereum": 50000,
              "polygon": 10000,
              "arbitrum": 10000
            },
            "arbitrum": {
              "ethereum": 50000,
              "polygon": 10000,
              "optimism": 10000
            }
          }
        }
      },
      "fees": {
        "USDC": {
          "ethereum": 1,
          "polygon": 1,
          "optimism": 1,
          "arbitrum": 1
        }
      },
      "metrics": {
        "enabled": true,
        "port": 8080
      },

      "bonders": {
        "USDC": {
          "ethereum": {
          "optimism": "YourPublicKey",
          "arbitrum": "YourPublicKey",
          "polygon": "YourPublicKey"
          },
          "optimism": {
          "ethereum": "YourPublicKey",
          "arbitrum": "YourPublicKey",
          "polygon": "YourPublicKey"
          },
          "arbitrum": {
          "ethereum": "YourPublicKey",
          "optimism": "YourPublicKey",
          "polygon": "YourPublicKey"
          },
          "polygon": {
          "ethereum": "YourPublicKey",
          "arbitrum": "YourPublicKey",
          "optimism": "YourPublicKey"
          }
        }
      } 

    }


  keystore.json: |
    {"address":"YourKeyStoreJsonData,"version":3}

```

Note: Please change the required data on above config example!!

### Secret.yaml

```bash
nano secret.yaml
```

```yaml
apiVersion: v1
data:
  keystorepass: ## output of `echo -n "YourKeystorePassphrase" | base64`
kind: Secret
metadata:
  name: hop-secret
  namespace: hop
type: Opaque

```

### Volume.yaml

```bash
nano volume.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: hop-volume
  namespace: hop
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Gi
  #storageClassName: do-block-storage

```


- Then we will use the `Staking` commands to stake the funds!

  Ignore the `Ethereum` in first command (it will pick the goerli network from the config)

  Understand that staking is one time procedure, so we will run this command in standalone container and once we are done, we will run actual `Deployment` with the help of `Kubernetes`

  We need to use the config for this, so please create a temporary dir named `hop-node` and place your `config.json` in it also create `tmp` and place  `keystore.json` in it for a while!

  - I hop (pun intendent) your directory structure looks like below

    ```
    project
    └───hop-node
    │   |- config.json
    |
    └───tmp
    |   |- keystore.json
    │       
    └───k8s
        │- cm.yaml
        │- Deployment.yaml
        │- secret.yaml
        │- volume.yaml

    ```


  Follow this [commands](https://docs.hop.exchange/hop-node/staking) 

  OR these 

  ```
  docker run -it -v $PWD/hop-node:/root -v $PWD/tmp:/tmp hopprotocol/hop-node:mainnet stake --config=/root/config.json --chain=ethereum --token=USDC --amount=500000

  docker run -it -v $PWD/hop-node:/root -v $PWD/tmp:/tmp hopprotocol/hop-node:mainnet stake --config=/root/config.json --chain=polygon --token=USDC --amount=100000 

  docker run -it -v $PWD/hop-node:/root -v $PWD/tmp:/tmp hopprotocol/hop-node:mainnet stake --config=/root/config.json --chain=optimism --token=USDC --amount=100000 

  docker run -it -v $PWD/hop-node:/root -v $PWD/tmp:/tmp hopprotocol/hop-node:mainnet stake --config=/root/config.json --chain=arbitrum --token=USDC --amount=100000

  ```
  
  You can stop the container once the staking is done!

- Run actual `kubernetes deployment`  

  ```kubectl create ns hop```

  We will deploy it using `kubectl apply -f ./k8s/` 

- Watch out logs!


Note: The given config will be modified with the Mainnet network! for more clarity contatct on [Hop Discord](https://docs.hop.exchange/on-the-web)
