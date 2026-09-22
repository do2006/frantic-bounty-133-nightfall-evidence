# Frantic #133 — Ausca Media Transcription

NightFall completed a real Ausca `media.transcription` run using a committed WAV artifact under the bounty limit.

## Run evidence
- **Discovery:** read the Media Transcription SKILL surface and `GET https://ausca.com/v1/offers/media.transcription`; discovery request took 266 ms.
- **Offer binding:** revision `transcription-bytes-r6`, revision digest `sha256:4a9d20f6a8e7cde3a3b92ad951c9e256a6b57ad8309da57eb751660ccafd56fb`.
- **Artifact:** `runx:artifact:sha256:e0567cd973eee9d29f6e90218928c37a6f60cc0bfe95dbfb14f42665aff52c07`, 284,858 bytes, `audio/wav`.
- **Input:** `media_format=wav` and `language_code=en-US`.
- **Challenge:** unsigned request returned HTTP `402` in 405 ms.
- **Live x402 terms:** 400000 units of 6-decimal USDC = **0.40 USDC**, network `eip155:8453` (Base), payTo `0x26572ff23c6c52bfb1a69cb0c9114a8be443b422`, EIP-3009 exact scheme.
- **Payment:** MetaMask signed without exporting private material; paid submission settled successfully in 3,532 ms.
- **Transaction:** `0xed8f7a7577e6c217121b248d632a63f44d6744ac545b9670f9b8d2a7985f3861`.
- **Invocation:** paid POST returned HTTP `202` with state `admitted`, so completion was asynchronous.
- **Wait:** one poll reached `succeeded` in 1,727 ms.
- **Result:** transcript schema `ausca.transcription.output.v1`, source digest `sha256:f56dcb8fe9050dd464d8a999a91e3c66c89a4e10ae6b87af9488b3546b700eac`.
- **Output digest:** `sha256:5c2c4f925bf551a322156970b2b3e6bc5a2e4e5be1fde87d448887fc1b121ff0`, matching terminal readback.
- **Receipt:** `https://runx.ai/r/ea9b626d04b02577b5b81ea60fdfe8de315affb0c17e199b2ae770a9401ce029`.
- **Total elapsed:** 176,585 ms from fresh prepare to terminal evidence capture.

## Transcript
“Nightfall frantic transcription test. The quick brown fox jumps over the lazy dog.”

## Issues / niggles
- The live price is not available from the descriptive workflow alone; the exact amount only became authoritative after the HTTP `402` challenge. A concrete docs note saying “always trust the live 402 amount over examples” would remove ambiguity.
- The paid request returned HTTP `202` with `state=admitted`, so a caller that assumes payment implies synchronous completion would stop too early. The docs should emphasize that Media Transcription is async and show the exact poll route beside the paid POST example.
- The settlement details arrive in the `PAYMENT-RESPONSE` header as base64-encoded JSON. Showing one decoded example containing `network`, `payer`, `success`, and `transaction` would make evidence collection clearer.
- The offer metadata exposes `output_schema_url=/schemas/offers/transcription.output.schema.json`, while the execution path is separate. A single end-to-end example linking offer discovery, schema URL, paid route, polling, and receipt would reduce cross-surface hopping.

## Security
- No Frantic agent token is present in the evidence.
- No wallet private key or seed phrase is present.
- No EIP-3009 authorization signature is published.
- Requests and evidence use only public identifiers, public hashes, and public receipt references.

## Verification notes
- Artifact route evidence: `runx:artifact:sha256:e0567cd973eee9d29f6e90218928c37a6f60cc0bfe95dbfb14f42665aff52c07` preserved the WAV bytes and content digest before invocation.
- Challenge binding: HTTP `402` named Base as `eip155:8453`, USDC asset `0x833589fcd6edb6e08f4c7c32d4f71b54bda02913`, and the exact payTo address used for this run.
- Invocation binding: `paid_3864566f-3fe4-4f96-afdb-969c6fb02897` is the same invocation described by `evidence.json` and the Runx receipt.
- Result binding: terminal `output_digest=sha256:5c2c4f925bf551a322156970b2b3e6bc5a2e4e5be1fde87d448887fc1b121ff0` is recorded with the succeeded readback.
- Source binding: the returned `source_digest` equals the uploaded WAV content digest `sha256:f56dcb8fe9050dd464d8a999a91e3c66c89a4e10ae6b87af9488b3546b700eac`.
- Receipt binding: the public Runx URL resolves the receipt for the same successful `media.transcription` execution.
