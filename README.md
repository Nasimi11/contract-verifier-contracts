# contract-verifier-contracts

A sources registry contract for registering a data url for a given code cell hash.
The contract accepts messages from a designated verifier registry contract.

Implementation is based on [TEP-91 suggestion](https://github.com/ton-blockchain/TEPs/pull/91).

This repo is a part of the following:
1. [contract-verifier-contracts](https://github.com/ton-community/contract-verifier-contracts) (this repo) - Sources registry contracts which stores an on-chain proof per code cell hash.
2. [contract-verifier-backend](https://github.com/ton-community/contract-verifier-backend) - Backend for compiling FunC and returning a signature over a message containing the resulting code cell hash.
3. [contract-verifier-sdk](https://github.com/ton-community/contract-verifier-sdk) - A UI component to fetch and display sources from Ton blockchain and IPFS, including code highlighting.
4. [contract-verifier](https://github.com/ton-community/contract-verifier) - A UI app to interact with the backend, contracts and publish an on-chain proof.

## E2E tests
(e2e.ts in test/e2e)
1. Pre-deploy (using `npm run build && npm run deploy`) the sources registry contract -> change min_tons in sources_registry.fc to a small amount, otherwise tests are too costly. 
2. Provide two mnemonics via .env
3. Flows carried out:
   * (Sender: wallet1) Change admin from wallet1 to wallet2
   * (Sender: wallet2) Change verifier address from actual to zero address; then revert to actual
   * (Sender: wallet2) Set code to `sources-registry-only-set-code.fc`; then revert to original
   * (Sender: wallet2) Change admin from wallet2 to wallet1
   * (Sender: wallet1) Set source item code to `...?.fc`; then revert to original
   
   
# License
MIT
MIT License

Copyright (c) 2022 Orbs.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.