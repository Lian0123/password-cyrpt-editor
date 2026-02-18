# WEBMCP Specification

`WEBMCP` (Web Manageable Crypto Pipeline) 是本專案的可交換設定格式，用於管理加密演算法節點與 UI 顯示行為。

## Goals
- 讓使用者可新增、刪除、調整演算法節點
- 以 JSON 格式可移植到其他系統
- 與 `index.html` / `webmcp-example.html` 共享設定

## File Format

```json
{
  "version": "1.0",
  "language": "zh",
  "theme": "dark",
  "source": "hello",
  "globalKey": "secret",
  "nodes": [
    {
      "id": "node-1",
      "enabled": true,
      "kind": "cipher",
      "algorithm": "AES",
      "mode": "encrypt",
      "iterations": 1,
      "key": ""
    }
  ]
}
```

## Supported `kind`
- `cipher`：AES / DES / TripleDES / Rabbit / RC4 / RC4Drop
- `hash`：MD5 / SHA1 / SHA224 / SHA256 / SHA384 / SHA512 / SHA3 / RIPEMD160
- `codec`：Base64 / Hex / URL / Reverse / ROT13
- `custom`：Caesar / XOR
- `asymmetric`：RSA / ECC / DLog

## Skill Integration
可搭配 `skill.json` 讓自動化代理知道如何呼叫：
- 匯入設定
- 匯出 Node.js / TypeScript
- 產生預設流程

## Best Practices
1. 先儲存 `WEBMCP` 設定，再執行流程。
2. 若有 Hash 節點，放在流程末端（不可逆）。
3. 生產環境請替換示範版 ECC/DLog 流程為正式密碼學套件。
