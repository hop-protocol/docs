---
description: Get contract state
---

# Contract State

### Contract state command

Prints the state of bridge and AMM contracts

{% tabs %}
{% tab title="Docker" %}
```bash
hop contract-state --token USDC --l1bridge --l2bridge --l2amm --l2ammwrapper
```
{% endtab %}

{% tab title="Node" %}
```bash
hop-node contract-state --token USDC --l1bridge --l2bridge --l2amm --l2ammwrapper
```
{% endtab %}
{% endtabs %}



Note: except for the token flag, all flags are optional.

### Output example

```json
{
  "l1Bridge": {
    "challengeAmountDivisor": "10",
    "timeSlotSize": "14400",
    "challengePeriod": "86400",
    "challengeResolutionPeriod": "1209600",
    "chainId": "1",
    "governance": "0x22e3F828b3f47dAcFACd875D20bd5cc0879C96e7",
    "minTransferRootBondDelay": "900",
    "chainStates": {
      "10": {
        "chainBalance": "6112490700021",
        "crossDomainMessengerWrapper": "0x1ba1f1368ecEB7bFcbdE20e1F803771b7B401F7d",
        "isChainIdPaused": false,
        "timeSlot": "0"
      },
      "100": {
        "chainBalance": "406180962091",
        "crossDomainMessengerWrapper": "0x12e59C59D282D2C00f3166915BED6DC2F5e2B5C7",
        "isChainIdPaused": false,
        "timeSlot": "0"
      },
      "137": {
        "chainBalance": "4616887310670",
        "crossDomainMessengerWrapper": "0x10541b07d8Ad2647Dc6cD67abd4c03575dade261",
        "isChainIdPaused": false,
        "timeSlot": "0"
      },
      "42161": {
        "chainBalance": "6673887957462",
        "crossDomainMessengerWrapper": "0xaC9BABf20eF2338D7F4a152Af43bedDC80C6ae2a",
        "isChainIdPaused": false,
        "timeSlot": "2"
      }
    },
    "bonderStates": {
      "0xa6a688F107851131F0E1dce493EbBebFAf99203e": {
        "credit": "22589161487578",
        "debitAndAdditionalDebit": "22401021943583",
        "isBonder": "true"
      }
    }
  },
  "l2Bridges": {
    "xdai": {
      "ammWrapper": "0x76b22b8C1079A44F1211D867D68b1eda76a635A7",
      "chainId": "100",
      "nextTransferNonce": "0x6ec3b5ad589fa51d75b8f24153d72114c94b826abef7755bfcba9416907632c5",
      "hToken": "0x9ec9551d4A1a1593b0ee8124D98590CC71b3B09D",
      "l1BridgeAddress": "0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a",
      "l1BridgeCaller": "0x12e59C59D282D2C00f3166915BED6DC2F5e2B5C7",
      "l1Governance": "0x22e3F828b3f47dAcFACd875D20bd5cc0879C96e7",
      "maxPendingTransfers": "128",
      "minBonderBps": "2",
      "minBonderFeeAbsolute": "0",
      "chainStates": {
        "1": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1631851515",
          "pendingAmountForChainId": "15479670558"
        },
        "10": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632007530",
          "pendingAmountForChainId": "76305479475"
        },
        "100": {
          "activeChainId": false,
          "lastCommitTimeForChainId": "0",
          "pendingAmountForChainId": "0"
        },
        "137": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632264635",
          "pendingAmountForChainId": "12712040065"
        },
        "42161": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632155810",
          "pendingAmountForChainId": "21996160771"
        }
      },
      "bonderStates": {
        "0xa6a688F107851131F0E1dce493EbBebFAf99203e": {
          "credit": "1670035438477",
          "debitAndAdditionalDebit": "1575783321453",
          "isBonder": "true"
        }
      }
    },
    "polygon": {
      "ammWrapper": "0x76b22b8C1079A44F1211D867D68b1eda76a635A7",
      "chainId": "137",
      "nextTransferNonce": "0x2d2f1042c518fa12e4b77fc1e5c73b995fdd0ae131075f11091c4aa617696c3a",
      "hToken": "0x9ec9551d4A1a1593b0ee8124D98590CC71b3B09D",
      "l1BridgeAddress": "0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a",
      "l1BridgeCaller": "0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a",
      "l1Governance": "0x22e3F828b3f47dAcFACd875D20bd5cc0879C96e7",
      "maxPendingTransfers": "128",
      "minBonderBps": "2",
      "minBonderFeeAbsolute": "0",
      "chainStates": {
        "1": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632587370",
          "pendingAmountForChainId": "4258981407"
        },
        "10": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632453762",
          "pendingAmountForChainId": "19406133313"
        },
        "100": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1631951255",
          "pendingAmountForChainId": "5932620396"
        },
        "137": {
          "activeChainId": false,
          "lastCommitTimeForChainId": "0",
          "pendingAmountForChainId": "0"
        },
        "42161": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632587500",
          "pendingAmountForChainId": "26876359528"
        }
      },
      "bonderStates": {
        "0xa6a688F107851131F0E1dce493EbBebFAf99203e": {
          "credit": "4099763736258",
          "debitAndAdditionalDebit": "4022821095435",
          "isBonder": "true"
        }
      }
    },
    "optimism": {
      "ammWrapper": "0x2ad09850b0CA4c7c1B33f5AcD6cBAbCaB5d6e796",
      "chainId": "10",
      "nextTransferNonce": "0xa3b20d425f59899c5f0e09f8e36dcb41380bdcaf42703c093f117853231e3610",
      "hToken": "0x25D8039bB044dC227f741a9e381CA4cEAE2E6aE8",
      "l1BridgeAddress": "0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a",
      "l1BridgeCaller": "0x1ba1f1368ecEB7bFcbdE20e1F803771b7B401F7d",
      "l1Governance": "0x22e3F828b3f47dAcFACd875D20bd5cc0879C96e7",
      "maxPendingTransfers": "128",
      "minBonderBps": "2",
      "minBonderFeeAbsolute": "0",
      "chainStates": {
        "1": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632480055",
          "pendingAmountForChainId": "99282640062"
        },
        "10": {
          "activeChainId": false,
          "lastCommitTimeForChainId": "0",
          "pendingAmountForChainId": "0"
        },
        "100": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632626825",
          "pendingAmountForChainId": "3816453963"
        },
        "137": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632403654",
          "pendingAmountForChainId": "42293513551"
        },
        "42161": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632603735",
          "pendingAmountForChainId": "6996809242"
        }
      },
      "bonderStates": {
        "0xa6a688F107851131F0E1dce493EbBebFAf99203e": {
          "credit": "3253669893410",
          "debitAndAdditionalDebit": "3197685446435",
          "isBonder": "true"
        }
      }
    },
    "arbitrum": {
      "ammWrapper": "0xe22D2beDb3Eca35E6397e0C6D62857094aA26F52",
      "chainId": "42161",
      "nextTransferNonce": "0xaa50a5b0f4e9e598d33bfca85fcf4d2593c276993d7991aab0f41b67daeda018",
      "hToken": "0x0ce6c85cF43553DE10FC56cecA0aef6Ff0DD444d",
      "l1BridgeAddress": "0x3666f603Cc164936C1b87e207F36BEBa4AC5f18a",
      "l1BridgeCaller": "0xBDaCAbf20ef2338D7F4A152aF43bedDC80c6BF3b",
      "l1Governance": "0x33F4F828b3F47dACfACd875d20bD5Cc0879CA7f8",
      "maxPendingTransfers": "128",
      "minBonderBps": "2",
      "minBonderFeeAbsolute": "0",
      "chainStates": {
        "1": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632604068",
          "pendingAmountForChainId": "10290010801"
        },
        "10": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "0",
          "pendingAmountForChainId": "42593547254"
        },
        "100": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632133224",
          "pendingAmountForChainId": "2928841269"
        },
        "137": {
          "activeChainId": true,
          "lastCommitTimeForChainId": "1632575038",
          "pendingAmountForChainId": "53434635349"
        },
        "42161": {
          "activeChainId": false,
          "lastCommitTimeForChainId": "0",
          "pendingAmountForChainId": "0"
        }
      },
      "bonderStates": {
        "0xa6a688F107851131F0E1dce493EbBebFAf99203e": {
          "credit": "2146919103909",
          "debitAndAdditionalDebit": "2012151631190",
          "isBonder": "true"
        }
      }
    }
  },
  "l2Amms": {
    "xdai": {
      "A": "200",
      "APrecise": "20000",
      "token0": "0xDDAfbb505ad214D7b80b1f830fcCc89B60fb7A83",
      "token1": "0x9ec9551d4A1a1593b0ee8124D98590CC71b3B09D",
      "token0Balance": "163104028207",
      "token1Balance": "176357831197",
      "virtualPrice": "1017070218286347997",
      "swapStorage": {
        "initialA": "20000",
        "futureA": "20000",
        "initialATime": "0",
        "futureATime": "0",
        "swapFee": "4000000",
        "adminFee": "0",
        "defaultWithdrawFee": "0",
        "lpToken": "0x9D373d22FD091d7f9A6649EB067557cc12Fb1A0A"
      }
    },
    "polygon": {
      "A": "200",
      "APrecise": "20000",
      "token0": "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174",
      "token1": "0x9ec9551d4A1a1593b0ee8124D98590CC71b3B09D",
      "token0Balance": "3591466737479",
      "token1Balance": "4354141459435",
      "virtualPrice": "1022227118817319093",
      "swapStorage": {
        "initialA": "20000",
        "futureA": "20000",
        "initialATime": "0",
        "futureATime": "0",
        "swapFee": "4000000",
        "adminFee": "0",
        "defaultWithdrawFee": "0",
        "lpToken": "0x9D373d22FD091d7f9A6649EB067557cc12Fb1A0A"
      }
    },
    "optimism": {
      "A": "200",
      "APrecise": "20000",
      "token0": "0x7F5c764cBc14f9669B88837ca1490cCa17c31607",
      "token1": "0x25D8039bB044dC227f741a9e381CA4cEAE2E6aE8",
      "token0Balance": "3589736061063",
      "token1Balance": "3276578935297",
      "virtualPrice": "1002972199941239661",
      "swapStorage": {
        "initialA": "20000",
        "futureA": "20000",
        "initialATime": "0",
        "futureATime": "0",
        "swapFee": "4000000",
        "adminFee": "0",
        "defaultWithdrawFee": "0",
        "lpToken": "0x2e17b8193566345a2Dd467183526dEdc42d2d5A8"
      }
    },
    "arbitrum": {
      "A": "200",
      "APrecise": "20000",
      "token0": "0xFF970A61A04b1cA14834A43f5dE4533eBDDB5CC8",
      "token1": "0x0ce6c85cF43553DE10FC56cecA0aef6Ff0DD444d",
      "token0Balance": "3507823521764",
      "token1Balance": "3691945785094",
      "virtualPrice": "1001742860866211679",
      "swapStorage": {
        "initialA": "20000",
        "futureA": "20000",
        "initialATime": "0",
        "futureATime": "0",
        "swapFee": "4000000",
        "adminFee": "0",
        "defaultWithdrawFee": "0",
        "lpToken": "0xB67c014FA700E69681a673876eb8BAFAA36BFf71"
      }
    }
  },
  "l2AmmWrappers": {
    "xdai": {
      "bridge": "0x25D8039bB044dC227f741a9e381CA4cEAE2E6aE8",
      "exchangeAddress": "0x5C32143C8B198F392d01f8446b754c181224ac26",
      "l2CanonicalToken": "0xDDAfbb505ad214D7b80b1f830fcCc89B60fb7A83",
      "l2CanonicalTokenIsEth": false
    },
    "polygon": {
      "bridge": "0x25D8039bB044dC227f741a9e381CA4cEAE2E6aE8",
      "exchangeAddress": "0x5C32143C8B198F392d01f8446b754c181224ac26",
      "l2CanonicalToken": "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174",
      "l2CanonicalTokenIsEth": false
    },
    "optimism": {
      "bridge": "0xa81D244A1814468C734E5b4101F7b9c0c577a8fC",
      "exchangeAddress": "0x3c0FFAca566fCcfD9Cc95139FEF6CBA143795963",
      "l2CanonicalToken": "0x7F5c764cBc14f9669B88837ca1490cCa17c31607",
      "l2CanonicalTokenIsEth": false
    },
    "arbitrum": {
      "bridge": "0x0e0E3d2C5c292161999474247956EF542caBF8dd",
      "exchangeAddress": "0x10541b07d8Ad2647Dc6cD67abd4c03575dade261",
      "l2CanonicalToken": "0xFF970A61A04b1cA14834A43f5dE4533eBDDB5CC8",
      "l2CanonicalTokenIsEth": false
    }
  }
}
```
