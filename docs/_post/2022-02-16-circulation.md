---
title: ICX circulation
author: yakkle
date: 2022-02-16
category: Jekyll
layout: post
---

# ICX circulation

## foundation addresses
 - [addresses](https://github.com/geometry-labs/icon-metrics/blob/main/icon_metrics/data/organization-addresses.csv)

## python script

```python
from iconsdk.icon_service import IconService
from iconsdk.builder.call_builder import CallBuilder
from iconsdk.providers.http_provider import HTTPProvider


LOOP_UNIT = 0xde0b6b3a7640000   # 10 ** 18

addresses = [
    "hx0cc3a3d55ed55df7c8eee926a4fafb5412d0cca4",
    "hx10ed7a7065d920e146c86d3915491f5a67248647",
    "hx1216aa95cf2aea0a387b7c243412022f3d7cf29f",
    "hx206846faa5ba46a3717e7349bff9c20d6fe1bba3",
    "hx25c5dace83bceae42c11360a07c9e42a3b5c6122",
    "hx266c053380ad84224ea64ab4fa05541dccc56f5f",
    "hx27664cffd284b8cf488eefb7880f55ce82f42297",
    "hx314348ecbaf01ff6c65c2877a6c593a5facecb35",
    "hx3f945d146a87552487ad70a050eebfa2564e8e5c",
    "hx465a11b018bf72febe40d54bce71f3860695d4c2",
    "hx4d83813703f81cdb85f952a1d1ee736faf732655",
    "hx4df036dcb1809743e677681d43cf2e904421f1eb",
    "hx558b4cd8cd7c25fa25e3109414bb385e3c369660",
    "hx64e40ddd929de5d15b2aab2ef4a3a47f8fe40b3b",
    "hx6b38701ddc411e6f4e84a04f6abade7661a207e2",
    "hx6c22cdba886614d3173e3d2499dc1597bdb57f2c",
    "hx6d2240f9c5fd0db5df6977ee586c3d74e1b1e4aa",
    "hx7062a97bed64624846f3134fdab3fb856dce7075",
    "hx7cdec6f51903ec274e01722bed4c60b6e88ebcbd",
    "hx87b6da94535754c2baee9d69010eb1b91eaa4c37",
    "hx8913f49afe7f01ff0d7318b98f7b4ae9d3cd0d61",
    "hx8d6aa6dce658688c76341b7f70a56dce5361e7ef",
    "hx930bb66751f476babc2d49901cf77429c5cf05c1",
    "hx94a7cd360a40cbf39e92ac91195c2ee3c81940a6",
    "hx980ab0c7473013f656339795a1c63bf44898ce95",
    "hx9913b07fbb31f5e334547bdaa880a767b52e45e1",
    "hx9d9ad1bc19319bd5cdb5516773c0e376db83b644",
    "hx9db3998119addefc2b34eaf408f27ab8103edaef",
    "hx9e19d60c9d6a0ecc2bcace688eff9053622c0c4c",
    "hxa55446e81997c03ee856a58ee18432325a4ef924",
    "hxa9c54005bfa47bb8c3ff0d8adb5ddaac141556a3",
    "hxaafc8af9559d5d320745345ec006b0b2170194aa",
    "hxabdde23cda5b425e71907515940a8f23e29a3134",
    "hxb7750699ca417561b170a980017bfc5fc9cef42e",
    "hxbc2f530a7cb6170daae5876fd24d5d81170b93fe",
    "hxc05ec08b6446a2a16b64eb19b96ea02225b840ab",
    "hxc1481b2459afdbbde302ab528665b8603f7014dc",
    "hxc17ff524858dd51722367c5b04770936a78818de",
    "hxcd6f04b2a5184715ca89e523b6c823ceef2f9c3d",
    "hxcf1b360dbb5818940acc05198d9966e639380b54",
    "hxd3b53e10d8c4c755879be09ff9ba975069664b7a",
    "hxd3f062437b70ab6d6a5f21b208ede64973f70567",
    "hxd42f6e3abfb7f5b14dbdafa34f03ffecf2a53a92",
    "hxd8ba6317da2eec0d9d7d1feed4c9c1f3cf358ae1",
    "hxdd4bc4937923dc140adba57916e3559d039f4203",
    "hxded0165517700240279be84d532b683a8531d76d",
    "hxdf6bd350edae21f84e0a12392c17eac7e04817e7",
    "hxe322ab9b11b63c89b85b9bc7b23350b1d6604595",
    "hxf1b55731e7f597c4e2b8014b5bfb05ce4976d6bc",
    "hxf1e3d780c589901d8af69629d1ffae0ff8c92b1d",
    "hxfc7888bf63d45df125cf567fd8753c05facb3d12"
]


def get_balance(icon_service: IconService, addr: str) -> int:
    balance_loop = icon_service.get_balance(addr)
    balance = balance_loop / LOOP_UNIT

    return balance


def get_stake(call_builder: CallBuilder, icon_service: IconService, addr: str) -> int:
    call = call_builder.params({"address": addr}).build()
    stake_result = icon_service.call(call)
    stake = int(stake_result['stake'], 16) / LOOP_UNIT

    return stake


def main():
    icon_service = IconService(HTTPProvider("https://ctz.solidwallet.io", 3))

    call_builder = CallBuilder()
    (call_builder.to("cx0000000000000000000000000000000000000000")
                    .method("getStake"))

    total_balance = 0
    total_stake = 0

    for addr in addresses:
        balance = get_balance(icon_service, addr)
        print(f"balance : {balance}")
        total_balance = total_balance + balance

        stake = get_stake(call_builder, icon_service, addr)
        print(f"stake : {stake}")
        total_stake = total_stake + stake

    print(f"total balance : {total_balance}")
    print(f"total stake : {total_stake}")
    print(f"total balance + stake : {total_balance + total_stake}")


if __name__ == "__main__":
    main()
```
