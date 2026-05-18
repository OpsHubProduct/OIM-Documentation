---
if: >-
  visitor.claims.unsigned.product === "OM4ADO"
---

# Resolving `HRESULT E_FAIL has been returned from a call to a COM component`

## Description

When you encounter an error such as:

`Error coming was HRESULT E_FAIL has been returned from a call to a COM component`

Perform the following steps:

1. Exit **Visual Studio** (if open).

2. Close **OM4ADO**.

3. Open a command window and navigate to the following folder:

   ```text
   %localappdata%\Microsoft\Team Foundation\<X.0>\Cache