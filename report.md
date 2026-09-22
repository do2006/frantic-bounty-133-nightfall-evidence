# Frantic #133 — Ausca Media Transcription

NightFall completed a real Ausca `media.transcription` run using a committed WAV artifact under the bounty limit.

## Run
1. Discovery: read the Media Transcription SKILL surface and `GET https://ausca.com/v1/offers/media.transcription`. The offer revision was `transcription-bytes-r6`; the discovery request took 266 ms.
2. Artifact: used `runx:artifact:sha256:e0567cd973eee9d29f6e90218928c37a6f60cc0bfe95dbfb14f42665aff52c07`, 284,858 bytes, `audio/wav`, with `media_format=wav` and `language_code=en-US`.
3. Challenge: the unsigned request returned HTTP 402 in 405 ms. The live x402 requirement was 400000 units of 6-decimal USDC = 0.40 USDC, network `eip155:8453` (Base), payTo `0x26572ff23c6c52bfb1a69cb0c9114a8be443b422`, EIP-3009 exact scheme.
4. Payment: MetaMask signed the authorization without exporting private material. The paid submission settled successfully in 3,532 ms. Transaction: `0xed8f7a7577e6c217121b248d632a63f44d6744ac545b9670f9b8d2a7985f3861`.
5. Invocation: the paid POST returned HTTP 202 with state `admitted`, not a final transcript.
6. Wait/result: one poll reached `succeeded` in 1,727 ms. The transcript output reported schema `ausca.transcription.output.v1`, source digest `sha256:f56dcb8fe9050dd464d8a999a91e3c66c89a4e10ae6b87af9488b3546b700eac`, and output digest `sha256:5c2c4f925bf551a322156970b2b3e6bc5a2e4e5be1fde87d448887fc1b121ff0`.
7. Receipt: `https://runx.ai/r/ea9b626d04b02577b5b81ea60fdfe8de315affb0c17e199b2ae770a9401ce029`.
8. Total elapsed from fresh prepare to terminal evidence capture: 176,585 ms.

## Transcript
“Nightfall frantic transcription test. The quick brown fox jumps over the lazy dog.”

## Issues / niggles
- The live price is not available from the descriptive workflow alone; the exact amount only became authoritative after the HTTP `402` challenge. A concrete docs note saying “always trust the live 402 amount over examples” would remove ambiguity.
- The paid request returned HTTP `202` with `state=admitted`, so a caller that assumes payment implies synchronous completion would stop too early. The docs should emphasize that Media Transcription is async and show the exact poll route directly beside the paid POST example.
- The settlement details arrive in the `PAYMENT-RESPONSE` header as base64-encoded JSON. That is machine-friendly but easy to miss during manual debugging. Showing one decoded example containing `network`, `payer`, `success`, and `transaction` would make evidence collection clearer.
- The offer metadata exposes `output_schema_url=/schemas/offers/transcription.output.schema.json`, while the execution path is separate. A single end-to-end example that links offer discovery, schema URL, paid route, polling, and receipt would reduce cross-surface hopping.

## Security
Requests and evidence use public identifiers only. No agent token, private key, seed phrase, or payment authorization signature is included.
